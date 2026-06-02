# Bestandsaufnahme Algron

Fakten über Algron und Henrik -- wächst mit jeder Session.

## Firma

- **Algron GmbH**, gegründet vor 4 Jahren (2022)
- Gründungsgrund: Henrik brauchte eine Struktur um Leute einstellen zu können, nachdem sein Freund (vorherige Firma) kein C# mehr machen wollte
- **Kein Businessplan bei Gründung** -- Firma entstand aus Projektnotwendigkeit, nicht aus Ambition
- Bisher zu keinem Zeitpunkt eine formulierte Vision oder Strategie

## Team (4 Personen)

Rollen-Zuordnung bestätigt (2026-05-29):

- **Henrik** -- CEO, Entwickler, Teamleitung, Kundenkontakt. Steckt in allem drin.
- **Philipp** -- Dev (Skadi-Kernprodukt). Quereinsteiger, 3 Jahre dabei, voll ausgelastet. Konzepte haben "Luft nach oben", braucht Anleitung.
- **Paula** -- PM, noch recht neu, braucht viel Input von Henrik (Funktionen, Priorisierung). Sucht aktiv Co-Explorer bei Voigt (Leute, die mit Algron an den großen Fragen arbeiten wollen).
- **Florian** -- KI-/LLM-Mann. Hat Algrons eigenes On-prem-LLM gebaut (datenschutz-stark). Arbeitet NICHT am Skadi-Kernprodukt, sondern baut Skadi Feature A (Dokument-Schwärzung). Technisch zuverlässig, "persönlich nicht ganz einfach".
- Ein früherer Mitarbeiter (längste Zugehörigkeit) wurde Anfang 2025 getrennt wegen starker inhaltlicher Differenzen.

## Projekte

### Skadi (Hauptprojekt)
- Läuft seit 9 Jahren (5 Jahre vor Algron gestartet)
- **1 Kunde:** Die Anwaltskanzlei **Voigt** (Klumpenrisiko, ~100% Umsatz-Abhängigkeit)
- Vereinfacht Bearbeitung digitaler Akten
- Entwicklung: Anfangs Datensammlung, jetzt Automatisierung + Anbindung externer Dienstleister
- Aktuell spannendste Funktion: Dashboard für Fallstatus-Überblick
- **Budget-Decke erreicht** -- kein Wachstum möglich, weder Stundenansatz noch Headcount
- Gegenseitige Abhängigkeit: Kanzlei braucht Henrik (kennt Software + Prozesse besser als jeder dort), Henrik braucht den Umsatz

### Skadi -- aktuelles Leitthema: KI für Voigt (Stand 2026-05-29)
- Der GF von Voigt weiß, dass er KI braucht, aber nicht wohin -- gibt den Ball an Henrik.
- Skadi ist der Kanal, über den KI bei Voigt ankommt -- damit die strategische Antwort aufs Klumpenrisiko.
- **Voigt hat eine eigene Rechtsabteilung, die sich bereits mit KI befasst.** Algron muss die Compliance nicht allein stemmen -- Ziel ist, an der Schnittstelle zur Rechtsabteilung souverän zu sein (richtige Fragen stellen, technisches Gegenstück liefern, Delegierbares abgeben).
- **Feature A (Dokument-Schwärzung):** läuft on-prem auf Algrons GPU. Die Schwärzungs-*Mechanik* ist technisches Detail (an Florian). ABER eine Teilfrage ist strategisch, nicht technisch -- siehe Versand-Frage. Compliance-Checkliste: `knowledge/skadi-compliance.md`.
- **Versand-Frage (offen, strategisch):** Sendet Skadi selbst ans LLM (Szenario A) oder gibt nur geschwärzt aus und Voigt sendet (Szenario B)? Entscheidet, ob Algron in die AVV-/Haftungskette eintritt. Empfehlungsrichtung B; heutiger Flow tendiert ohnehin B, ist aber nicht festgenagelt. Darf nicht implizit durch die Implementierung fallen. (Szenario C: Florians eigenes On-prem-LLM nutzen -- kein externer Versand, Haftungskette bleibt intern; sauberste Variante, sofern das eigene LLM die Use-Cases trägt.)
- **Produkthaftung als Risikovektor:** Skadi auszuliefern macht Algron zum Hersteller (verschuldensunabhängig, Beweislastumkehr bei KI) -- nicht der EU AI Act ist Algrons Hauptrisiko, sondern das. Mit Voigts Juristen gegenchecken.

### Feedback-Plan / Co-Explorer bei Voigt (Stand 2026-06-02)
- **Aufwand aktive Mitarbeit ≈ 20-30 min/Woche** (Henriks Schätzung). Geringe Hürde -- kein schwerer Vergütungs-/Freistellungsapparat nötig. Die eigentliche Herausforderung ist nicht die Zeit, sondern die Bindung über Leerlauf-Phasen (Wochen ohne neue Features).
- **GF-Beziehung (8-Jahre-Modus):** GF lässt viel Freiraum, hakt wenig nach. Reaktiv: Henrik klärt mit NL-Leitung → die erwähnt es beim GF → GF wird hellhörig, fragt Henrik → Henrik erklärt → GF ist fein. Vorab um Erlaubnis fragen ist nicht der übliche Weg.
- **Voigt-Kanal:** Henrik hat direkten Draht zu NL-Leitungen und bekannten Mitarbeitenden -- braucht keine GF-Erlaubnis, um mit ihnen zu arbeiten.

### Quality Connect (Nebenprojekt)
- Lange Findungsphase, jetzt konkreter
- Bestehende QA-Software modernisieren (wenig Weiterentwicklung in letzten 5-10 Jahren)
- **Temporär: 3-5 Jahre**, dann schrumpfend (Web-Umstellung durch Partnerfirma)
- **Max. 1/3 des Skadi-Volumens**
- Besserer Stundenlohn als Skadi (v.a. mit KI-Unterstützung)
- Bindet Henriks Kapazität (Vier-Augen-Prinzip)

## Henriks Zeitverteilung (geschätzt, Session 1)

| Bereich | Anteil |
|---------|--------|
| Skadi-Entwicklung | 20% |
| Quality Connect | 10% |
| PM-Einarbeitung | 10% |
| KI-Projekt | 5% |
| Skadi-Planung & Kunden | 5% |
| **Nicht zugeordnet** | **50%** |

Henrik erfasst seine Arbeitszeit aktuell nicht systematisch.

## Henrik persönlich

- Entwickler durch und durch, aber will raus
- 8 Jahre quasi ohne Freizeit gearbeitet -- Anfang 2025 schmerzlich bewusst geworden
- Auslöser für Veränderungswunsch war Schmerz, nicht Ambition
- Letztes Jahr: Stabilisierung nach Teamumbruch, "ganz gut geklappt"
- Skeptisch gegenüber Beratern ("haben keinen Plan, kassieren viel Geld, liefern keinen Mehrwert")
- Software ist für ihn Mittel, nicht Zweck
- Will an sinnvollen Zielen arbeiten, die ihn persönlich berühren
- Interessensgebiete: Bahn, Verwaltung -- "verkrustete Systeme verbessern"

## Kernproblem: Die Schleife

Henrik steckt in einem Kreislauf fest:
1. Steckt im Code, weil andere es nicht gut genug können
2. Andere können es nicht, weil Henrik immer da ist und alles weiß
3. Kann niemanden einstellen, weil Budget nicht reicht
4. Budget reicht nicht, weil Geschäftsmodell nicht skaliert
5. Geschäftsmodell skaliert nicht, weil keine Zeit für Strategie
6. Keine Zeit für Strategie, weil er im Code steckt

Diese Schleife bricht nicht von innen durch Optimierung.
