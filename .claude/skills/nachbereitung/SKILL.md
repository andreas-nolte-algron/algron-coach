---
name: nachbereitung
description: "Post-Session-Verarbeitung: Miro-Ergebnis als Ground Truth sichern, geplant-vs-tatsächlich analysieren, in den Spine projizieren, Prep ins Archiv graduieren, frische next-session, dann /save. Aufrufen am Ende einer Henrik-Session."
---

Verarbeitet eine gerade gelaufene Henrik-Session: bringt das echte Ergebnis an die richtigen Stellen und schärft das Henrik-Modell für die nächste Vorbereitung.

**Leitprinzip -- Projektion, nicht Neuerzählung.** Die Session-Datei (gefülltes Miro + Analyse) ist die Ground Truth. session-log und henrik-strategie sind *abgeleitete Sichten* davon -- gefiltert und komprimiert, aber strukturgleich. Nie unabhängig neu generieren (erzeugt Drift).

## Voraussetzung

Das **gefüllte Miro-Ergebnis** (was tatsächlich lief). Claude kann Miro nicht lesen -- Andi liefert den Inhalt. Ohne ihn nicht starten; stattdessen fragen.

**Transport (gelernt 13.06.):** Roh-Paste aus Miro in den Chat verliert die Hierarchie (verschachtelte Bullets flachen ab). Stattdessen: Andi öffnet **`strategy/miro-import.html`** im Browser, pastet die Miro-Karte rein, klickt „umwandeln" → das Tool erzeugt **Dash-Tiefe** (`-`, `--`, `---` je Ebene, plus `**fett**`/`*kursiv*`), die den Chat unbeschadet übersteht. Andi pastet den Dash-Text in den Chat, Claude parst ihn zurück. (Farbe/Highlight gehen so nicht mit -- nur falls nötig, HTML-Export-Weg.)

## Ablauf

1. **Ground Truth sichern.** Den Miro-Block (aus dem Dash-Text rekonstruiert) **verbatim** als neuen Abschnitt **oben** in die aktuelle `strategy/next-session.html` einsetzen (Überschrift „Was tatsächlich war"), als verschachtelte HTML-Liste. Andis Notation, ungefiltert -- nichts paraphrasieren, nichts glätten. Andi prüft gegen. (Kleine Tool-Macke: Fett über einer Span-Grenze kann einen Leerraum mit ins `**…**` nehmen -- beim Rendern glätten.)

2. **Analyse: geplant vs. tatsächlich** (gemeinsam mit Andi, das Herz der Nachbereitung).
   - Hat das Henrik-Modell aus der Prep gehalten? Wo wich die Session ab -- positiv wie negativ?
   - Was lehrt das Delta über das Henrik-Modell und über Andis eigene Muster (Output-Druck, Flucht ins Tun, Validieren-statt-Generieren)?
   - Ergebnis als Abschnitt „Analyse / geplant vs. tatsächlich" in die Datei, **zwischen** „Was tatsächlich war" (oben) und der Original-Prep (unten).

3. **In den Spine projizieren** (abgeleitet aus der Session-Datei, nicht neu erzählt):
   - **`progress/session-log.md`** -- kompakter Eintrag, neueste oben. Henrik-sichtbar: Fakten + Coaching-Substanz, **kein taktischer Read**.
   - **`strategy/henrik-strategie.md`** -- datierter Abschnitt, Andi-only: der taktische Read + das geplant-vs-tatsächlich-Delta.
   - **`progress/action-plan.md`** -- erledigte Tasks schließen, neue/veränderte aufnehmen.
   - **`progress/strategie-landkarte.html`** -- nur wenn sich die Struktur bewegt hat.
   - **`progress/bestandsaufnahme.md`** -- nur wenn bestätigte Fakten reif sind (z.B. ein verifizierter GF-Kanal-Stand).

4. **Prep graduieren.** Die jetzt vollständige Datei (Tatsächlich + Analyse + Prep) nach **`strategy/archive/session-YYYY-MM-DD.html`** verschieben (`git mv` wenn möglich). Andi blättert das Archiv visuell -- soll lesbar/ansehnlich bleiben. (git ist die eigentliche Versionssicherung; das Archiv ist Andis Lesefläche.)

5. **Energie-Fork -- frische next-session jetzt oder später?** Andi entscheidet, nicht drängen.
   - **Energie da:** neue `strategy/next-session.html` nach dem Vorbereitungs-System bauen (Henrik-Modell-Test vor dem Vorschlag, Adapter Werkstatt→Artefakt, Miro-Karten-Block mit Granularitäts-Test -- alles im strategy-Modus-Systemprompt verankert).
   - **Ausgelaugt:** hier stoppen. In `project-status.md` vermerken, dass next-session noch aussteht -- wird zu Beginn der nächsten Vorbereitung gebaut.

6. **Firewall + Save.** `/save` aufrufen (enthält Firewall-Check + commit + push). Besonders prüfen lassen: Ist in die Henrik-sichtbaren Projektionen (session-log, action-plan, landkarte) kein taktischer Read durchgesickert? Liegt die graduierte Session-Datei in `strategy/` (Andi-only)?

## Abbruch-Sauberkeit

Wird mitten im Ablauf gestoppt (z.B. nach Schritt 3, Rest später): in `project-status.md` festhalten, welche Schritte offen sind, damit die nächste Session sauber aufsetzt. Nie halb-projiziert ohne Vermerk liegen lassen.
