---
name: commit
description: "Session-Commit: /track ausführen, dann committen und pushen. Standard für Sessionende."
---

Führe einen Session-Commit durch:

1. Rufe `/track` auf -- aktualisiert project-status.md mit dem Session-Fortschritt.
2. `git add -u` -- alle getrackten Änderungen stagen.
3. `git diff --cached --stat` -- Überblick zeigen.
4. Commit-Message aus den Änderungen ableiten (kurz, deutsch, beschreibend).
5. `git commit` mit der Message.
6. Prüfe ob ein Remote existiert (`git remote`). Wenn ja: `git push`. Wenn nein: "Kein Remote konfiguriert, nur lokal committed." melden.

Wenn nichts zu committen ist (keine staged changes nach Schritt 2), melde das und überspringe Schritt 3-6.
