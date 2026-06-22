---
name: research
description: "Web-Recherche zu einem konkreten Thema. Ergebnisse werden in knowledge/research-notes.md gespeichert."
argument-hint: "[thema]"
context: fork
model: claude-sonnet-4-5
allowed-tools: "Read, Edit, Grep, Glob, WebSearch, WebFetch"
---

Recherchiere das Thema: $ARGUMENTS

Vorgehen:
1. Lies `knowledge/research-notes.md` (falls vorhanden) -- prüfe was bereits bekannt ist
2. Recherchiere im Web: Fakten, Benchmarks, Fallbeispiele, relevante Entwicklungen
3. Fokus auf Relevanz für Algron/Henrik: Was ist konkret anwendbar?
4. Schreibe Ergebnisse in `knowledge/research-notes.md` via Edit (akkumulativ, nie Write)
   - Format: `## [Thema] -- [Datum]` als Abschnittsüberschrift
   - Nur Erkenntnisse mit direkter Relevanz für Algron/Henrik
5. Gib eine kompakte Zusammenfassung zurück (3-5 Kernpunkte, was bedeutet das für Henrik/Algron?)

Qualitätscheck:
- Sind die Quellen belastbar (keine Meinungen als Fakten)?
- Gibt es einen unangenehmen Befund dabei -- einen den Henrik vielleicht nicht hören will?
- Ist die Relevanz für Algron explizit (nicht nur allgemeine Marktinfos)?
