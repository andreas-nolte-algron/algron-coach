---
name: reflect
description: Ehrliche Selbstanalyse des Agent-Teams
allowed-tools: "Read, Glob, Grep, Write"
context: fork
model: claude-sonnet-4-5
---

Analysiere das eigene Team schonungslos ehrlich.

1. Lies: CLAUDE.md, alle Agents (.claude/agents/), alle Skills (.claude/skills/*/SKILL.md), main-agent.md, project-status.md
2. Analysiere: Rollen-Klarheit, Überschneidungen, Nutzungshäufigkeit (aus session-log.md und progress-Dateien)
3. Prinzip-Konsistenz:
   - Extrahiere die Kernprinzipien aus main-agent.md (Bohren, 10x-Linse, Fallstricke ansprechen, Orchestrieren)
   - Prüfe: Hat jedes Prinzip das nötige Werkzeug (Skill/Agent)?
   - Suche nach Lücken: Was sollte da sein, ist aber nicht?
4. Identifiziere: Schwachstellen, fehlende Skills, Ineffizienzen, Überschneidungen zwischen Agents
5. Schreibe nach `.claude/team-reflection.md`

Format für `.claude/team-reflection.md`:
```
# Team Reflection -- [Datum]

## Stärken
[Was funktioniert gut]

## Schwachstellen
[Was nicht funktioniert oder fehlt]

## Prinzip-Konsistenz
[Welche Prinzipien haben kein Werkzeug? Wo gibt es Lücken?]

## Empfehlungen
[Konkrete Änderungsvorschläge]
```
