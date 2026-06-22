---
name: status
description: "Kompakter Überblick: Wo stehen wir? Liest alle Progress-Dateien und zeigt Stand, offene Actions, nächste Steps."
allowed-tools: "Read, Glob"
---

Lies die folgenden Dateien und gib einen kompakten Überblick:

1. `progress/session-log.md` -- Letzte Session-Einträge (nur die letzten 2-3)
2. `progress/bestandsaufnahme.md` -- Fakten über Algron (Zusammenfassung)
3. `progress/vision.md` -- Aktueller Visions-Stand
4. `progress/action-plan.md` -- Offene und erledigte Actions

Ausgabe-Format:
```
## Stand

[2-3 Sätze: Wo wir gerade sind, was zuletzt erarbeitet wurde]

## Offene Actions

[Liste offener Steps aus action-plan.md -- max 5, mit Fälligkeitsdatum wenn vorhanden]

## Nächste Steps

[Was als nächstes ansteht -- konkret]

## Offene Fragen

[Was noch ungeklärt ist -- falls vorhanden]
```

Wenn eine Datei leer ist: kurz notieren ("Bestandsaufnahme noch nicht gestartet"), nicht auslassen.
