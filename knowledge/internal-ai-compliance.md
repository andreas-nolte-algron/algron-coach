# Interne KI im Dev-Alltag — Compliance-Inventar

> Erstellt 2026-06-16. Schwester-Datei zu `skadi-compliance.md`: die deckt das *Produkt* Skadi ab — diese hier das *interne Tooling* (KI in der Entwicklung).
> Firmenkontext: `progress/bestandsaufnahme.md`. Anthropic-Policy-Quelle: anthropic.com/news/updates-to-our-consumer-terms (Stand 06/2026).
> Entstanden aus der Weiterbildungs-Sichtung „Datenschutz & KI" (Modul 6/Sektion 2). Single Point of Truth für den internen-KI-Kontext — damit das Prüfungs-Mapping (iqhub-backup) keine Firmen-Fakten doppelt hält, sondern hier liest.

## Ausgangslage (Fakten)

Zwei KI-Flächen in der Entwicklung, beide gegen Anthropic/Claude:

1. **Claude Code im täglichen Dev** — jeder Entwickler + Henrik, interaktiv beim Bauen von Skadi.
2. **`mr-review` — selbstgebauter Merge-Request-Review-Bot** auf algron-server. Reviewt automatisch Merges im Skadi-Repo und gibt Feedback an die Devs. Getriggert per N8N/ClickUp-Webhook („Ready for Review").

**Abo-Situation:** Claude Code **Max 20x** pro Person — von der Firma bezahlt, aber **Consumer-Tier** (Plan-Typ `claude_max`, Consumer Terms). „Firmen-Abo" heißt hier *wer zahlt*, NICHT *kommerzieller Vertrag*: es ist KEIN Claude for Work/Enterprise und KEINE Anthropic-API mit AVV. Der mr-review-Bot läuft **headless (`claude -p`) unter Andis persönlichem Max-Abo** — KEIN separater Bot-/Org-Account. Folge: ein und dasselbe Privacy-Setting regelt die interaktive Dev-Nutzung UND den Bot. (Falls in Wahrheit Claude Team/for Work mit AVV → entschärft; soweit erkennbar `claude_max` = Consumer.)

**Inhalt:** laut Henrik **Quellcode only**, keine echten Personen-/Mandantendaten. Deckt sich mit dem Bot-Scope (reviewt nur das Skadi-.NET-Repo) — aber ohne technische Garantie (s. „Die Lücke").

## Welcher Rechtsrahmen greift — nicht alles ist DSGVO

- **DSGVO: dünn.** Kein Personenbezug im Flow → DSGVO greift kaum direkt. Nicht der Haupthebel.
- **§203 StGB / Verschwiegenheit + Geschäftsgeheimnis: DAS ist der Hebel.** Skadi-Code bildet Voigts Kanzlei-Prozesse und Domänenregeln ab und ist Algrons Kern-IP. Er geht an einen US-Anbieter.
- **Drittlandtransfer: nachrangig**, weil kein Personenbezug — relevant nur als Vertraulichkeits-/Jurisdiktionsfrage (US-Anbieter, US-Zugriffsrechte), nicht als DSGVO-Drittland-Pflicht.

## Kern-Befund: Consumer-Abo für Firmen-Produktivcode

Anthropic-Consumer-Terms (Free/Pro/Max, **inkl. Claude Code**), Stand 06/2026:

- Modelltraining = **Opt-in pro Nutzer** (Privacy Settings, jederzeit änderbar) — keine Firmen-/Org-Kontrolle.
- Training **AN → 5 Jahre Retention**. Training **AUS → 30 Tage**.
- **Kommerziell** (Claude for Work/Enterprise, API, Bedrock, Vertex) = separate Commercial Terms, **kein Training by default**, AVV/DPA verfügbar.

→ **Implikation:** Ob Skadi-Quellcode bei Anthropic ins Training fließt + 5 Jahre liegt, hängt an der individuellen Einstellung *jedes Entwicklers* — auf Firmenebene nicht kontrollierbar und nicht nachweisbar. Kein AVV, keine garantierte Zero-Retention. Exakt der „Privat- vs. Enterprise-Account"-Fall der Weiterbildung (Lektion 2), nur auf Code statt Personendaten gedreht.

## mr-review im Detail (Forensik 2026-06-16, read-only)

- **Auth:** headless (`claude -p`) unter Andis persönlichem **Max**-Abo (Plan-Typ `claude_max`) — also **Consumer-Tier**, KEIN separater Bot-/Org-Account, kein kommerzieller API-Key/Plan, kein eigener Endpoint. Folge: Andis Account-Privacy-Setting regelt auch den Bot. Modelle Sonnet + Opus über `api.anthropic.com`.
- **Was an Anthropic geht — mehr als der Diff:** voller MR-Diff PLUS Laufzeit-Lesezugriff der Agenten aufs **gesamte Skadi-Repo + komplette Git-History** (Read/Grep/Glob, `git log/show/blame`). Kein Sandbox-Diff-Review — die Exposition ist potenziell die *ganze* Codebasis, nicht nur die Änderung.
- **Keine Redaction/Sanitization** vor dem Senden. Enthält ein Diff/eine gelesene Datei Secrets, Connection-Strings oder versehentlich Personendaten, gehen sie ungefiltert raus.
- **Retention lokal, unbegrenzt:** 148 Review-Verzeichnisse (Roh-Diffs, Reviews, Agent-Findings) + **389 Claude-CLI-Transcripts (51 MB)** mit vollen Prompts inkl. eingebetteter Diffs/Repo-Inhalte — keine Rotation/Löschung. Liegt auf algron-server (gitignored, nicht gepusht, aber dauerhaft on-disk).
- **Scope:** nur `gitlab.com/algron/skadi`.
- **Betrieb:** algron-server, N8N (Docker) per SSH; kein Cron/systemd. v5-Engine aktiv (v6 vorhanden, nicht aktiviert).

## Die Lücke in „Code only"

„Quellcode only" ist eine **Disziplin-Annahme, kein technischer Zwang**: mr-review hat keine Redaction und vollen Repo-Lesezugriff; die interaktive Dev-Nutzung erlaubt jedes Paste. Ein versehentlich eingefügter Stacktrace, ein Test-Fixture mit echtem Mandantennamen, eine Migration mit Echtdaten oder ein Connection-String kippt die Annahme — und dann ist es DSGVO + §203 zugleich.

## Zweite Fläche: das Coaching-Repo selbst (algron-coach)

Nicht nur Skadi-Code läuft über Claude Code — auch dieses Strategie-/Coaching-Repo wird über dasselbe Consumer-Abo verarbeitet. Pro Byte sensibler als der Code:

- **Eigene Mitarbeiter-PII inkl. Werturteile** (Leistungs-/Charaktereinschätzungen, Trennungsgrund eines Ex-MA). Rahmen: **Beschäftigtendatenschutz (§26 BDSG)**, NICHT §203 — es sind eigene Leute, nicht Voigts Mandanten. Im Leak-Fall das reputativ + DSGVO-heikelste Material.
- **Namentlich genannter Kunde** (Voigt) + Geschäftsgeheimnisse (Klumpenrisiko, Budget-Decke, Strategie).

Training-aus (Andis Account) deckt Training/Retention auch hier ab; der Rest ist dasselbe Voigt-Gate wie beim Code.

**Offen (Scope noch zu entscheiden, Stand 16.06.):**
- [ ] Mitarbeiter-Werturteile entschärfen: Charakter-Label → funktionale Arbeitsnotiz (Signal behalten, Verdikt raus). Höchster Hebel.
- [ ] Kunde + Team pseudonymisieren — senkt Blast-Radius, ist aber **k=1** (einziger Kunde, 4-Personen-Team = trivial re-identifizierbar): Schadensbegrenzung, keine Anonymisierung.

## Mapping auf die Weiterbildung (Modul 6 / Sektion 2)

- **Lektion 2 (Enterprise vs. Privat-Account):** direkter Treffer → kommerzieller Plan/AVV/No-Training.
- **Lektion 2 (Input-Filterung):** mr-review hat keine — die Sektion empfiehlt genau das (Regex/Presidio/Proxy vor dem Senden).
- **Lektion 5 (Datenminimierung/Retention):** 51 MB Transcripts + 148 Review-Dirs ohne Löschkonzept = Gegenteil von Speicherbegrenzung.
- **Lektion 3 (Drittland):** US-Anbieter — hier vertraulichkeits-, nicht DSGVO-getrieben.

## Handlungsoptionen

**Sofort / billig:**
- [x] Modelltraining-Setting **AUS** → Retention 5 Jahre → 30 Tage. **Erledigt bei Andi** — und weil mr-review headless unter Andis Abo läuft, ist der Bot damit mitabgedeckt. Verbleibt: jeder weitere Entwickler mit eigenem Max-Abo muss es selbst setzen (auf Firmenebene nicht erzwingbar). Prüfpfad: `claude.ai/settings/data-privacy-controls`, Toggle „Help improve Claude" — gilt laut Doku auch für Claude Code inkl. headless `-p`. Caveat: safety-flagged Conversations können laut Policy (08.06.2026) trotz Opt-out genutzt werden, Trigger nicht definiert — kleines Restloch.
- [ ] Lokale Retention auf algron-server begrenzen: Cleanup-/Rotations-Job für `reviews/` und die CLI-Transcripts (51 MB und wachsend).

**Strukturell — aber NICHT als reflexhaftes „Upgrade":**
- [ ] Kommerzielle Terms (Claude **Team**/**Enterprise** seat-basiert, oder **API** per Token) bringen **AVV + No-Training by default + Org-Kontrolle/Nachweisbarkeit**. Das ist der einzige Weg zu einem *vertraglichen* No-Training statt eines Per-User-Toggles (+ schließt das safety-flag-Restloch).
- **Kosten-Tradeoff (ehrlich, geprüft 16.06.):** NICHT zwingend „5-10x". Team/Enterprise sind seat-basiert (~$20-100/Seat/Monat); reine API-Token-Kosten sind das teure Szenario. ABER: Max ist flat mit großzügigen Limits — die Token-Overage bei Team/Enterprise ist nicht öffentlich gelistet und skaliert mit intensiver Claude-Code-Nutzung. Der echte Vergleich ist *flat Max* vs. *seat + variable Token-Bill*, kein fixes Vielfaches.
- **Das Gate liegt nicht intern, sondern bei Voigt:** Ob der Wechsel nötig ist, hängt an EINER Frage — verlangt §203 / die Voigt-Beziehung eine AVV-feste *Nachweisbarkeit*, oder ist „Training aus + disziplinierter Code-only-Betrieb" verteidigbar? Mit Voigts Rechtsabteilung klären (analog zur Skadi-Versand-Weiche), nicht intern entscheiden. Falls ja → Wechsel lohnt; falls nein → Max bleiben + mr-review härten reicht.
- [ ] mr-review: Repo-Lesezugriff der Agenten einschränken (Diff-fokussiert statt Voll-Repo) + eine Secret-/PII-Scan-Stufe vor dem Senden — analog zur Skadi-Schwärzung im Produkt.

**Optional:**
- [ ] „Code only" technisch absichern (Pre-Send-Scan), damit die Annahme nicht an Disziplin hängt.

## Vor Festlegung gegenchecken (ggf. mit Voigts Rechtsabteilung)

- Reicht für die Verschwiegenheit der Kanzlei, dass Algrons Entwickler Skadi-Code (der Voigts Prozesse abbildet) über einen US-Anbieter prozessieren? Im Kanzlei-Vertrag/AVV abgedeckt?
- Anthropic-Policy ändert sich — vor jeder Festlegung gegen aktuelle Terms prüfen.

## Was Henrik hören muss

Bei „nur Code" ist das kein DSGVO-Feuer — aber euer Kern-Asset (Skadi-Code = eure IP + Voigts Prozesse) läuft aktuell über ein **Consumer-Tier-Abo (Max, von der Firma bezahlt) ohne AVV und ohne Retention-Kontrolle**, und der mr-review-Bot schickt potenziell die ganze Codebasis automatisiert raus. Der Fix ist billig und größtenteils ein Setting-/Plan-Wechsel — und derselbe „wir sind sauber"-Nachweis, der euch gegenüber Voigts Rechtsabteilung souverän macht. Gleiche Linie wie skadi-compliance.md: Compliance ist hier Produktqualität/Vertrauen, nicht Bürokratie.

> Caveat: Forensik read-only 2026-06-16; Anthropic-seitige Retention für diesen Abo-Typ nicht direkt geprüft (nur Policy-Doku). Kein Rechtsrat.
