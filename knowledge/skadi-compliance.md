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
