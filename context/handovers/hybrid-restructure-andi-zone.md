---
type: handover
status: done
actor: maintainer
created: 2026-05-29
updated: 2026-06-10
summary: "algron-coach von Henrik-only-Coach zu Hybrid (Henrik-sichtbar + Andi-only strategy/-Zone) umgebaut, mit Firewall. DONE: Struktur + Firewall stehen, strategy-Modus laeuft produktiv (mehrere Andi-Sessions seit 29.05.), 29.05.-Gespraech nachgetragen. Restpunkte ausgelagert."
next-steps:
  - "ERLEDIGT: strategy-Modus getestet -- laeuft produktiv (Sessions 29.05./02.06./04.06./09.06.)"
  - "ERLEDIGT: Henrik-Gespraech 29.05. nachgetragen (henrik-strategie.md + session-log)"
  - "AUSGELAGERT: Cross-Team-Cleanup -> Memory deferred-cross-team-cleanup (eigener Strang)"
  - "OFFEN (Maintenance, low prio): Server-Symlink aufs Script pruefen -- pro-Maschine, blockiert nichts"
---

# Hybrid-Restruktur — Andi-Zone & Firewall

## Kontext

ki-berater-Uebergabe (29.05.2026) brachte drei Briefings + Auftrag, die Algron-Strategie ins Team-Gedaechtnis zu holen. Beim Einpflegen kam raus: die Briefings drehen den Adressaten von Henrik auf Andi (sie sind Spickzettel fuer Andi, der Henrik coacht — nicht fuer Henrik, der mit dem Agenten redet). Daraus wurde eine Architektur-Entscheidung statt einer reinen Ablage.

## Kernerkenntnisse

### 2026-05-29
- **Ein Team, zwei Ebenen** — statt zwei Repos. Andy wollte Datei-Drift bei geteilten Fakten vermeiden; deshalb eine Quelle mit interner Trennung.
- **Firewall = Whitelist + Instruktion.** `talk` (Henriks Coach) laedt nur main-agent.md + project-status.md + progress/. `strategy/` liegt bewusst top-level (NICHT unter progress/), weil `/status` dort sweept. main-agent.md + CLAUDE.md sperren `strategy/` explizit fuer den Coach.
- **Split-Faustregel:** Substanz, die Henrik klueger macht → sichtbar (progress/). Der Read, wie man Henrik bewegt → `strategy/`.
- **Coach-facing Beschreibungen abgehaertet:** CLAUDE.md/main-agent.md nennen `strategy/` nur noch "Andis Admin-/Strategie-Bereich, gesperrt" — nicht mehr "taktischer Read ueber Henrik". Der Coach weiss damit *dass* gesperrt, nicht *was* drin ist. Volle Beschreibung nur in `strategy/README.md` (Coach sieht es nie).
- **Zwei Uebergabe-Punkte korrigiert:** (1) Sync war NICHT "push disabled" — dieser Klon pusht, Server zieht beim Session-Start selbst. (2) "Einpflegen" war keine Ablage, sondern eine Zielgruppen-Entscheidung.
- **Restrisiko bewusst akzeptiert:** Firewall ist Whitelist + Instruktion, keine harte Mauer. Landet versehentlich ein Andi-Fakt in progress/, sieht Henrik ihn.

## Erfolgskriterien

Henrik nutzt `talk` ohne je `strategy/` zu sehen; Andi nutzt `strategy` mit voller Sicht auf beide Ebenen; Fakten leben einmal (kein Drift). Kern erreicht & committet (✅ 7129641 + Firewall-Haertung). Bleibende Arbeit = Disziplin beim Schreiben + Folge-Cleanup.

## Naechste Schritte

1. **strategy-Modus real testen** — eine Andi-Session fahren (`algron-coach strategy`), pruefen ob Lade-Verhalten + Trennung in der Praxis halten.
2. **Server-Symlink** aufs Script pruefen; falls er fehlt, per SSH (`my-server`) setzen. Script-Inhalt synct via git, nur der Symlink ist pro-Maschine.
3. **Cross-Team-Cleanup** (skadi-doku, algron-strategist) in eigener Session — siehe Memory `deferred-cross-team-cleanup`. algron-strategist vorher auf `analyze_code_embeds.js` + `iqhub-offline-clone.md` pruefen.
4. **Henrik-Gespraech 29.05. nachtragen** — Ergebnis (Antworten auf die vier Fragen) in `strategy/henrik-strategie.md` und ggf. progress/.

## Offene Fragen

- Haelt die Trennung allein durch Disziplin beim laufenden Schreiben, oder braucht es einen Hook/Pre-Commit-Check, der Andi-Begriffe in progress/ flaggt?
- Mapping Florian/Paula auf die alten unbenannten Rollen (Quereinsteiger-Dev? PM? KI-Person?) — unbestaetigt.
- Wie wird "ruhend markieren" fuer die Cleanup-Teams ueberhaupt dargestellt?

## Scope-Grenzen

Nicht in diesem Strang: das inhaltliche Henrik-Coaching (die vier Fragen mit Henrik durcharbeiten), die Cross-Team-Cleanups (eigener Strang), die Quality-Connect-Neubewertung.

## Abhaengigkeiten

Blockiert nichts hart. Cross-Team-Cleanup ist ein Folge-Strang (Memory). Server-Sync laeuft ueber normales push/pull (steht).

## Artefakte

| Datei | Inhalt |
|-------|--------|
| `strategy/strategy-agent.md` | System-Prompt fuer den strategy-Modus (Andis Strategist) |
| `strategy/henrik-strategie.md` | Taktischer Read, Engpaesse, Interventions-Design (Andi-only) |
| `strategy/README.md` | Firewall-Regel dokumentiert |
| `main-agent.md` | Coach-Prompt, `strategy/`-Sperre verankert |
| `CLAUDE.md` | Struktur + Firewall-Erklaerung, strategy-Modus |
| `scripts/algron-coach` | Modi talk/strategy/admin |
| `project-status.md`, `progress/*` | Henrik-sichtbare Faktenlage, KI/Voigt reconciled |
| `knowledge/skadi-compliance.md` | Feature-A-Compliance-Checkliste |
| Memory `deferred-cross-team-cleanup` | Folge-Strang skadi-doku + algron-strategist |
