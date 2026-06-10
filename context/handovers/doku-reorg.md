---
type: handover
status: done
actor: maintainer
created: 2026-06-09
updated: 2026-06-10
summary: "Doku-Reorg KOMPLETT (10.06.): action-plan auf Status-Achse, session-log neueste-oben, Firewall = ganze Doks pro Ebene + Leak-Check, Landkarte-HTML Ebene 2 auf Zwei-Welten. Offen nur noch Andis Browser-Sichtprüfung der Landkarte (Pixel-Feintuning per Drag)."
next-steps:
  - "ERLEDIGT (10.06.): Design-Entscheidungen -- action-plan Status-primär mit Themen-Tag; Firewall = ganze Doks pro Ebene + Leak-Check (kein Split pro Dokument)"
  - "ERLEDIGT (10.06.): action-plan auf Status-Achse umgebaut (Stehende Prinzipien / Offen / In Arbeit / Ruhend / Erledigt), Themen-Tags + Herkunfts-Datum"
  - "ERLEDIGT (10.06.): session-log auf neueste-oben gedreht; Meta-Labels (firewall-reviewer) kosmetisch geglättet"
  - "ERLEDIGT (10.06.): Landkarte-HTML Ebene 2 auf Zwei-Welten (worlds-Metadaten, Trennlinie, WAS/WIE-Badges, Schlüssel-Karte s4); JSON + JS validiert"
  - "REST (Andi): Landkarte einmal im Browser sichten, Karten-Positionen bei Bedarf per Drag justieren + exportieren"
---

# Doku-Reorg — progress/ + strategy/ Struktur

## Kontext

Die Doku-Struktur ist über mehrere Sessions gewachsen und reibt jetzt. Die Diagnose wurde in einer Strategie-Session (09.06.2026) gestellt, der Umbau aber bewusst verschoben: Kontext-Ökonomie (Hauptsession war voll) + die offenen Design-Entscheidungen brauchen frisches Sparring, keinen müden Durchmarsch.

## Diagnose (steht)

- `progress/session-log.md` und `progress/action-plan.md` sind BEIDE nach Herkunfts-Session (Zeit-Achse) gegliedert -- "Aus Session 1", "Aus Workshop 04.06." usw. Dadurch überschneiden sie sich: jede Session erscheint zweimal, einmal narrativ (Log), einmal als Tasks (Plan).
- Folge: Der action-plan kann seine eigentliche Aufgabe nicht erfüllen -- "was ist JETZT offen?". Die offenen Tasks sind über viele Herkunfts-Blöcke verstreut, durchmischt mit erledigten/`[~]`-Tasks. Man muss alles scannen und im Kopf filtern.

## Zielbild (Richtung steht, Details offen)

Drei getrennte Achsen statt zwei konkurrierender Zeit-Achsen:

| Zeit | Dokument | Achse |
|------|----------|-------|
| Vergangenheit | `session-log` | Zeit (neueste oben), narrativ + Feedback |
| Gegenwart | `action-plan` | Zustand/Thema -- nach Strängen ODER Offen/In Arbeit/Erledigt; Herkunft nur als Tag |
| Zukunft | `next-session` | die eine kommende Session (existiert bereits, strategy/, Andi-only, HTML) |

Darüber: `project-status` (Vogelperspektive), `vision` + `bestandsaufnahme` (langsame Referenz, Henrik-sichtbar).

Sobald der action-plan themen-/zustands-gegliedert ist, verschwindet die Konkurrenz zum session-log -- sie teilen keine Achse mehr.

## Offene Design-Entscheidungen (NICHT getroffen -- hier liegt die Sparring-Arbeit)

1. **Firewall-Split:** Was von session-log/action-plan wandert nach `strategy/`, was bleibt Henrik-sichtbar? Angedacht war "Split pro Dokument" (Substanz sichtbar, Read → strategy). NICHT final. **Achtung:** Henriks `talk`-Coach liest nur `progress/`. Wandert zu viel nach `strategy/`, sieht der Coach keinen Projektstand mehr. (Aktuell ist der Split faktisch schon da: der taktische Read lebt in `strategy/henrik-strategie.md`, session-log/action-plan sind Henrik-sichtbar. Frage ist, ob das so reicht oder bewusster getrennt werden soll.)
2. **action-plan-Achse:** nach den Ebene-2-Strängen (Klassische SE / KI-Entwicklung) oder schlicht nach Status (Offen/In Arbeit/Erledigt)?
3. **Reihenfolge:** session-log + action-plan auf neueste-oben umdrehen (Andis Präferenz, bestätigt). Mechanisch.
4. **Reformat:** Einträge teils inkonsistent (fett/nicht-fett gemischt, besonders der Workshop-04.06.-Block im action-plan). Glätten.

## Was schon entschieden/gebaut ist

- `next-session` als HTML in `strategy/` (Andi-only, Vorbereitungs-Leitfaden mit taktischer Schicht, Schema wiederverwendbar). Nach jeder Session: Inhalt → session-log, neues anlegen.
- `strategie-landkarte.html` als HTML in `progress/` (Henrik-sichtbar, Ground Truth, interaktiv mit Karten-Drag/Edit/Export).
- Firewall-Prinzip: `progress/` = Henrik-sichtbar, `strategy/` = Andi-only.

## Offene Punkte (über die Struktur hinaus)

- **Landkarte-HTML Ebene 2 ist veraltet:** Sie zeigt noch die alte 4-Stränge-Ebene-2. Im Workshop-Nachgang (Session 09.06.) hat Henrik Ebene 2 in zwei Welten umgebaut: LINKS "Klassische SE" (GF wenig involv., "WIE?") mit Strängen Ressourcen-Einsatz + Alltägliche Feature-Entwicklung; RECHTS "KI-Entwicklung" (GF stark involv., "WAS?" + "WIE?") mit hinterliegende GF-Wünsche + Aufklärungsarbeit + KI-Mehrwert; dazwischen eine Trennlinie. Das ist ein Layout-Umbau (zwei Spalten, WAS/WIE-Tags, Trennlinie), nicht bloßes Karten-Verschieben. OFFEN: baut Andi via Miro→Export selbst, oder eigener Bau-Task.

## Scope-Grenzen

NICHT in diesem Strang: das inhaltliche Coaching; das Einpflegen einzelner Sessions (die 09.06.-Session läuft separat über einen Subagent, baut bewusst auf der AKTUELLEN Struktur auf -- unten anhängen). Dieser Reorg organisiert danach um. Kein Konflikt, nur Reihenfolge: erst einpflegen (Daten sichern), dann reorganisieren.
