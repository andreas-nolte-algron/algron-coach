# Projektstatus -- Algron Coach

## Ziel

Strategischer Sparringspartner für Henrik (CEO, Algron GmbH). Drei Aufgaben: Vision entwickeln, 10x-Denken verankern, Entwickler-Engpass lösen.

## Stand

Leitthema: **KI nutzbar machen für die Kanzlei Voigt** (Hauptkunde). Der GF weiß, dass er KI braucht, aber nicht wohin -- gibt den Ball an Henrik. Move: nicht visionieren, sondern entflechten.

09.06. **Ebene-2-Durchbruch (Henrik selbst am Stift):** die Stränge teilen sich in zwei Welten -- **Klassische SE** (GF wenig involviert, „WIE?") vs. **KI-Entwicklung** (GF stark involviert, „WAS?" + „WIE?"). Kern: KI ist ein WAS-Thema (was will man überhaupt?), nicht nur WIE. Daraus die Erkenntnis des Tages: **zielgerichtete GF-Kommunikation ist dringend** -- die bisherigen KI-Versuche waren nie auf die echten Wünsche ausgelegt. (KI-spezifisch: bei klassischer SE kennt Henrik die GF-Wünsche gut.) Henrik überlegt schriftlich (Folgetag), ob er sich darauf committet. Stand gepflegt in `progress/strategie-landkarte.html` (Ground Truth).

10.06. (kein Coaching): Vormittags Werkzeug-/Doku-Pflege -- Landkarte Ebene 2 auf die Zwei-Welten-Struktur + direkte Bearbeitung; `action-plan` auf Status-Achse, `session-log` neueste-oben. Nachmittags operativ: **Speicherform für die Standort-/Personen-Infos mit Paula gelöst** -- Paula baute die Liste, Andi ergänzte eine Filter-Lösung; zwei Ebenen (Standort ⊃ Person) + Feedback-Typ-Feld. Details in `context/handovers/`.

12.06. **Henriks Commitment ist da:** Er hat sich gemeldet -- bei der zielgerichteten GF-Kommunikation weiterhin dabei. Damit ist der Messpunkt vom 09.06. positiv gefallen. Vormittags zudem Werkzeug-Pflege: Session-Vorbereitungs-Ablauf systematisiert (Andi-Bereich).

13.06. **Durchbruch -- der fehlende vierte Kanal.** Henrik beschrieb den GF-Draht über 10 Jahre: heute drei Email-Typen (weitergeleitet / Informationsanfrage / eigens ausgearbeitet), **alle feature-/auftragsgetrieben** = fertige WAS → WIE. Roter Faden: der GF macht die WAS-Arbeit vorgelagert und allein, in 10 Jahren nie ein gemeinsames Gespräch übers WAS -- genau deshalb scheiterte KI (kein fertiges WAS). Erkenntnis: es braucht einen **vierten, strategischen Kanal**, der nicht rein über Email laufen kann (Henriks Einwand, zugleich die nächste Spannung -- er ist nicht gern in Meetings). Abschluss zeit-/telefonbedingt abrupt, per Slack repariert. **Werkzeug:** neuer `/nachbereitung`-Skill gebaut + am ersten echten Fall getestet (Miro→Session-Datei→Spine→Archiv); `miro-import.html` als Transport-Tool (Hierarchie-erhaltend). Session-Datei graduiert nach `strategy/archive/session-2026-06-13.html`.

13.06. (Nachtrag, Prep/Pflege): **next-session für die Vierter-Kanal-Form-Session gebaut** (normale Stunde, Form-Knoten knacken; Schritt 1 spiegelt Henriks eigenen Durchbruch, gegen die „wusste-ich-eh"-Signatur). **Kategorienfehler gestoppt (Andi):** Der vierte Kanal war versuchsweise als Karte in die `strategie-landkarte.html` gesetzt -- Landkarte ist aber WAS-verfolgen-wir (Themen), Kanäle sind WIE-kommunizieren (anderes Modell). Rückgängig. **Job des Kanäle-Modells geklärt:** Befund + einmaliges Gerüst, kein eigenes Artefakt -- Heimat ist Text in `bestandsaufnahme.md`. Dauer-Linse (Mail-Triage) nicht vorab entscheiden; nur wenn Henrik es selbst will.

Vorlauf: 04.06. Workshop -- Top-Level-Sicht bottom-up zu 4 Strängen, Ziel-Ebene noch offen (nur „guten Gewissens höhere Rechnungen"). 29.05./02.06. Wissenstransfer-Übereinkunft + erster Delegations-Fall (Leerlauf → Paula) + Themen-Tunnel-Muster gespiegelt. Sessions 1–3: Schleife erkannt (Henrik im Code), Vision da, Brücke zum Heute fehlt.

## Die vier Fragen (aktueller Arbeitsrahmen)

- **A -- Voigt: Wo lohnt sich KI im Alltag?** ← die Wurzel. Einstieg über den Alltag, NICHT über Tools.
- **B -- Voigt: Wie befähigen wir die Mitarbeitenden?** Kommt nach A.
- **C -- Skadi: Was muss Skadi können, damit die Use-Cases gehen?** = Skadi-Roadmap, hängt an A. (Skadi ist der Kanal, über den KI bei Voigt ankommt -- damit die Antwort aufs Klumpenrisiko.)
- **D -- Algron: Wie gehen wir strategisch ran?** Ergibt sich aus A–C, muss Henrik NICHT vorab erfinden.
- **Geparkt:** Tooling / EU-fähiger Anbieter -- laut Henrik nicht die Herausforderung.
- **Filter „sinnvoll":** Ein Use-Case taugt, wenn beides stimmt -- echter Alltagsschmerz UND mit heutiger KI realistisch machbar.

## Der Engpass (präzisiert)

Henrik ist das **Nadelöhr**: einziger Kanal zum GF Voigt *und* alleiniger Wissensträger. Das ist eine strukturelle Frage (Wissen externalisieren + Kanal öffnen), nicht nur eine des Loslassens.

## Kernerkenntnisse bisher

- Algron hat kein Geschäftsmodell, sondern Projekte mit Umsatz-Decke (Skadi + Quality Connect)
- Henrik will raus aus Entwicklung -- hin zu Problemlöser/strategischer Partner
- Skadi Feature A: Schwärzungs-*Mechanik* an Florian delegiert -- ABER die Versand-Frage (sendet Skadi selbst?) ist eine strategische Haftungs-Weiche, kein technisches Detail. Entscheidungsgrundlage liegt vor (Compliance-Sichtung): Empfehlung Szenario B (Skadi sendet nicht selbst), echt offen, heutiger Flow tendiert ohnehin B
- Skadi als Kanal für KI bei Voigt = strategische Antwort aufs Klumpenrisiko
- Übersehener Risikovektor: Produkthaftung (Algron = Hersteller, verschuldensunabhängig) -- größer als die AI-Act-Klasse. Voigt hat eigene Rechtsabteilung -- Compliance nicht allein stemmen, an der Schnittstelle souverän sein
- **Wissenstransfer ist der Hebel gegen das Nadelöhr:** Delegieren ohne Wissensübergabe frustriert Henrik (andere fabrizieren auf dünner Lage). Lösung als Standardschritt jeder Übergabe verankert: erst Wissen übertragen + verschriftlichen, dann sinkt Henriks Aufwand auf Feinjustierung
- **Geld-Realität:** Bei stundenbasierter Abrechnung bringt Effizienz keine Mehreinnahmen -- der Kommunikations-/Experimentier-Strang zahlt auf Haltung und Struktur ein, aber nicht direkt auf den Geld-Schmerz. Offene Brücke: Henriks freigewordene Zeit muss in geld-bringende Arbeit fließen, sonst Effizienz ohne Ertrag

## Offene Punkte

- Quality Connect: strategische Neubewertung steht weiter aus (Nebenstrang, in den aktuellen Briefings nicht berührt)
- Berater-Aversion vs. eigenes Modell noch nicht aufgelöst; Netzwerk-Frage durch Voigt-Co-Explorer-Richtung teils adressiert, aber kein zweiter Kunde in Sicht

## Nächste Steps

1. **Nächste Session: Form des vierten Kanals knacken.** Prep liegt fertig in `strategy/next-session.html` (Datum + Offtopics live ergänzen). Normale Stunde: Henrik benennt eine Kandidaten-Form (zwischen „nicht Email" und „kein Meeting") -- oder dimensioniert es selbst als eigenen Workshop. Das eigentliche Vorstoß-Design (Rollenspiel/Gesprächsplan) bleibt ein späterer Termin.
2. **Frühwarn-Faden** (optionale zweite Hälfte): wann überschreitet eine Mail die Feature-Grenze = Trigger für den vierten Kanal. NICHT als „mach dir die 3 Typen bewusst" framen; nur wenn Henrik den Bedarf selbst zeigt.
3. Paula-Delegation: Henrik beauftragt kommende Woche -- Evaluation/Checkup terminieren.
