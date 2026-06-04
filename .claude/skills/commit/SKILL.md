---
name: commit
description: "Session-Commit: /track ausführen, Firewall prüfen, dann committen und pushen. Standard für Sessionende."
---

Führe einen Session-Commit durch:

1. Rufe `/track` auf -- aktualisiert project-status.md mit dem Session-Fortschritt.
2. `git add -u` -- alle getrackten Änderungen stagen.
3. `git diff --cached --stat` -- Überblick zeigen.
4. **Firewall-Check (Pflichtschritt, nicht überspringen):** Spawne den `firewall-reviewer`-Subagenten (Agent-Tool, `subagent_type: firewall-reviewer`). Er prüft die gestageten Henrik-sichtbaren Änderungen gegen die Firewall-Heuristik -- ein frischer Kopf ohne den Schreib-Kontext dieser Session.
   - Meldet er **„✓ FIREWALL SAUBER"** -> weiter zu Schritt 5.
   - Meldet er **Verdachtsfälle** -> committe NICHT. Leg Andi die Fälle vor und lass ihn entscheiden (verschieben / umformulieren / bewusst drin lassen). Setze erst nach Andis Entscheidung fort -- ggf. korrigieren, neu stagen (zurück zu Schritt 2), dann erneut prüfen.
   - Der Reviewer flaggt nur, er ändert nichts. Auch ein „mild"-Fall geht an Andi, nicht stillschweigend durch.
5. Commit-Message aus den Änderungen ableiten (kurz, deutsch, beschreibend).
6. `git commit` mit der Message.
7. Prüfe ob ein Remote existiert (`git remote`). Wenn ja: `git push`. Wenn nein: "Kein Remote konfiguriert, nur lokal committed." melden.

Wenn nichts zu committen ist (keine staged changes nach Schritt 2), melde das und überspringe Schritt 3-7.
