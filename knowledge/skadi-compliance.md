# Skadi Feature A (Dokument-Schwärzung) – Compliance-by-Design

> Erstellt 2026-05-28, eingepflegt 2026-05-29. Praktische Checkliste für Henrik / Dev-Team (Florian).
> Ziel: das KI-Feature von Anfang an AI-Act-, DSGVO- und verschwiegenheits-sicher bauen, statt teuer nachzurüsten.
> Firmenkontext: `progress/bestandsaufnahme.md`. (Hinweis: eine eigene EU-AI-Act-Wissensdatei existiert in diesem Repo noch nicht.)

## Ausgangslage

- **Feature:** Skadi nimmt Dokumente und schwärzt sensible Inhalte. Läuft auf Algrons eigener hauseigener GPU (on-prem). Die Kanzlei füttert die *geschwärzten* Dokumente danach in externe LLMs (Claude / ChatGPT).
- **Nutzer:** Anwälte intern. Keine End-Mandanten.
- **Rolle Algron:** Provider (Downstream-Provider auf GPAI-Basis).
- **Risikoklasse:** minimal/begrenzt – NICHT Anhang-III-Hochrisiko (Justiz-Hochrisiko meint Gerichte/Justizbehörden, nicht ein internes Tool einer privaten Kanzlei; rein unterstützende Tools sind ausgenommen).
- **Die echte Exposition liegt nicht in der AI-Act-Klasse**, sondern in Schwärzungs-Genauigkeit + dem externen LLM-Schritt.

## Die 3 nicht-verhandelbaren Design-Entscheidungen

1. **Menschlicher Gate vor Versand.** Kein Auto-Send geschwärzter Dokumente an externe LLMs ohne explizite Anwalts-Bestätigung („Schwärzung geprüft & freigegeben"). Bestätigung protokollieren. Der UX-Komfort eines Auto-Send wiegt das Haftungsrisiko nicht auf.
2. **Externe LLMs nur über API/Enterprise mit AVV, nie Consumer.** ChatGPT-Consumer trainiert standardmäßig auf den Eingaben und hat keinen AVV – für (auch geschwärzte) Anwaltsdaten tabu. Nur OpenAI-API/Enterprise bzw. Anthropic-API mit No-Training-Einstellung + abgeschlossenem AVV.
3. **False-Negative-Rate messen & schwellen.** Die gefährliche Richtung ist der *übersehene* sensible Inhalt. An repräsentativen Echt-Dokumenten testen, Trefferquote dokumentieren, akzeptable Schwelle definieren, laufend monitoren.

## Die Versand-Frage: sendet Skadi selbst? (Architektur-Weiche, bewusst entscheiden)

> Ergänzt 2026-05-29 aus der Weiterbildungs-Sichtung „KI fair & sicher nutzen".

Die scheinbar technische Frage aus Checklisten-Punkt „übernimmt Skadi den Versand?" ist in Wahrheit eine Haftungs-Weiche. Sie entscheidet, ob Algron in die Auftragsverarbeitungs-Kette eintritt:

- **Szenario A – Skadi sendet selbst ans LLM:** Algron wird Auftragsverarbeiter von Voigt, das LLM wird Algrons *Sub*-Auftragsverarbeiter. Algron muss den AVV mit dem LLM-Anbieter halten, Serverstandort/Drittlandtransfer absichern, haftet für die Kette. §203-Daten fließen durch Algron.
- **Szenario B – Skadi schwärzt on-prem, gibt nur aus, Voigt sendet:** Algron bleibt für den Außentransfer Werkzeug-Lieferant. AVV mit dem LLM, Serverstandort, Drittlandtransfer liegen bei Voigt (die dafür eine Rechtsabteilung hat). Algron verarbeitet zwar weiterhin (Schwärzung on-prem = Auftragsverarbeitung), aber das LLM wird nicht Algrons Sub-AV.

**Empfehlungsrichtung: B.** Hält Algron aus der AVV-Maschinerie und der §203-Haftung heraus. Der heutige Flow tendiert ohnehin Richtung B — die Weiche sollte bewusst so festgenagelt werden, nicht implizit durch die Implementierung fallen.

Wichtig: Man kann sich aus dieser Weiche **nicht herausanonymisieren.** Auch perfekte Schwärzung macht den Versand nicht DSGVO-frei (siehe nächster Abschnitt) — die Entscheidung A vs. B muss so oder so getroffen werden.

## Warum Schwärzung allein nicht „anonym" bedeutet

- **Pseudonym ≠ anonym.** Direkt-Identifikatoren schwärzen mit interner Zuordnung = Pseudonymisierung; die Daten bleiben rechtlich personenbezogen. Echte (irreversible) Anonymisierung ist deutlich schwerer — kein EU-Gericht hat kommerzielle Anonymisierung bisher als ausreichend akzeptiert.
- **Der Sachverhalt ist selbst ein Identifikator.** Kanzlei-Fälle sind oft Einzelfälle (k=1): der seltene Erbstreit, der prominente Beklagte ist durch die Konstellation re-identifizierbar, auch ohne Namen. Direkt-Identifikatoren schwärzen macht den Fall nicht anonym, ohne ihn fürs LLM unbrauchbar zu machen. Reines Regex/Namenslisten reicht nicht.
- **Mapping-Tabelle bei Voigt halten.** Bleibt die Zuordnung bei Voigt (nicht in Skadi/beim Versand), ist der ausgehende Text *für das LLM* faktisch anonym (EuGH-Linie zur Empfänger-Anonymität), obwohl er für Voigt personenbezogen bleibt. Stützt Szenario B.
- **Verschlüsselung hilft hier nicht** — das stärkste Sachargument für Feature A: Das LLM braucht Klartext, während der Verarbeitung liegt alles offen, E2EE ist bei generativer KI unmöglich. Der einzige Schutz vor dem LLM selbst ist, identifizierende Inhalte gar nicht erst reinzugeben.
- **Technischer Bauplan:** automatische Entity-Erkennung in Freitext via Microsoft Presidio / spaCy-NER, nicht nur Pattern-Matching. Auch die Rückrichtung beachten — die LLM-Antwort kann re-kontextualisiert wieder personenbezogen werden.

## Der übersehene Risikovektor: Produkthaftung

Algrons größtes Risiko ist nicht die AI-Act-Klasse (Skadi ist begrenztes Risiko), sondern: Skadi auszuliefern macht Algron nach reformierter EU-Produkthaftung zum **Hersteller** — verschuldensunabhängig. Bei KI greift zudem eine **Beweislastumkehr**: ohne dokumentierte Entwicklung/Tests/Grenzen wird im Streitfall die Kausalität gegen Algron vermutet. Die schlanke technische Doku (siehe Checkliste) ist damit nicht Bürokratie, sondern Haftungsabwehr.

> Caveat: Produkthaftung und Versand-Frage stammen aus generischem KMU-Schulungsmaterial, das den „Anbieter, der KI-Funktionen liefert"-Fall (= Algron) nur am Rand behandelt. Vor einer Festlegung mit Voigts Rechtsabteilung gegenchecken — nicht als Rechtsberatung verwenden.

## Checkliste

**Klassifizierung & Doku (schlanke Provider-Pflicht)**
- [ ] Rolle + Risikoklasse schriftlich festhalten (Provider, Downstream-GPAI, begrenztes Risiko, kein Anhang III – mit Ein-Satz-Begründung)
- [ ] Schlanke technische Doku: Zweck, genutztes Modell, beabsichtigte Verwendung, bekannte Grenzen („nicht 100% – Anwalts-Review zwingend"), gemessene Genauigkeit

**Menschliche Aufsicht**
- [ ] Verbindlicher Review-/Freigabeschritt im UI vor jedem Versand
- [ ] Freigabe wird geloggt (wer, wann, welches Dokument)

**Externer LLM-Schritt**
- [ ] Klären: nutzt die Kanzlei ChatGPT-Consumer oder API/Enterprise? Falls Consumer → umstellen
- [ ] AVV (DPA) mit jedem LLM-Anbieter abgeschlossen und abgelegt
- [ ] No-Training / Zero-Retention bei Anthropic & OpenAI bestätigt
- [ ] Entscheiden & dokumentieren: übernimmt Skadi den Versand (dann mit Gate aus Punkt 1) oder gibt es nur das Dokument aus?

**Schwärzungs-Genauigkeit / Datengovernance**
- [ ] Test an repräsentativen Echt-Dokumenten, False-Negative-Rate gemessen
- [ ] Akzeptable Schwelle definiert + dokumentiert
- [ ] Monitoring + Incident-Prozess, falls doch ungeschwärzte Daten rausgehen

**DSGVO-Verzahnung**
- [ ] Geschwärzte Daten = personenbezogen/besondere Kategorien → AVV-Kette zu Sub-Prozessoren steht
- [ ] On-prem-GPU für Schwärzung = Datenminimierung dokumentiert (gutes Argument)
- [ ] Mit der von der Kanzlei durchgeführten Legalitätsprüfung abgleichen (worauf stützt sie sich genau?)

**KI-Kompetenz (Art. 4, seit Feb 2025 Pflicht)**
- [ ] Anwälte, die das Tool bedienen, kurz auf Grenzen/Bedienung einweisen (= zugleich Türöffner für Feature B)

## Was Henrik hören muss

Compliance kostet hier fast nichts extra, weil ihr früh dran seid – und sie ist keine Bürokratie, sondern Produktqualität: Sie schützt die Verschwiegenheit der Kanzlei und die Mandantendaten und hält Algron aus der Haftung. Genau das, was ein Legal-Tech-Produkt robust und vertrauenswürdig macht.
