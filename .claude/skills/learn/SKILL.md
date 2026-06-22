---
name: learn
description: "Wissen integrieren: URL oder Thema in die knowledge/-Dateien einarbeiten. Verdichtet, nicht gesammelt."
argument-hint: "[url oder thema]"
context: fork
model: claude-sonnet-4-5
allowed-tools: "Read, Edit, Grep, Glob, WebSearch, WebFetch"
---

Integriere neues Wissen: $ARGUMENTS

Knowledge-Dateien (Routing-Logik):
- `knowledge/ceo-transition.md` -- Führung, 10x-Denken, Founder-Transition, E-Myth
- `knowledge/saas-strategy.md` -- Diversifikation, Moats, Legal-Tech-Markt, Klumpenrisiko
- `knowledge/team-scaling.md` -- Micro-Team, Fractional, KI-augmented Dev, Engpass
- `knowledge/algron-context.md` -- Firmenfakten (nur gesicherte Infos über Algron/Henrik)
- `knowledge/research-notes.md` -- Akkumulierte Recherche (alles was keiner der obigen Dateien passt)

Vorgehen:
1. Lies `knowledge/index.md` -- Überblick der Dateien
2. Falls URL: Lade und extrahiere relevante Informationen (WebFetch)
3. Falls Thema: Recherchiere (WebSearch + WebFetch)
4. Bestimme welche knowledge/-Datei(en) relevant sind
5. Integriere via Edit (akkumulativ, nie Write):
   - Verdichten, nicht sammeln: Kernpunkte extrahieren, nicht Copy-Paste
   - Widersprüche zum bestehenden Inhalt explizit markieren
   - Datum und Quelle in Klammern hinter neue Erkenntnisse
6. Gib zurück: Was wurde integriert, in welche Datei, was war neu vs. bestätigt

Qualitätsprinzip: Lieber weniger aber hochwertig. Wenn eine Info nichts Neues bringt: weglassen.
