# Phase 2 – Technik: n8n‑Flow, JSON‑Schemas, Export & Pilot

**Stand:** 2025‑09‑04 · **Region:** Hannover · **Upload‑Methode:** GitHub‑Weboberfläche (Option A)

## Überblick
Diese Anleitung führt dich durch Import & Konfiguration der n8n‑Workflows, die Schemas, das Exportformat sowie den Pilotbetrieb. Keine Terminal‑Kommandos nötig.

## Artefakte
- `flows/n8n-phase2-ingest.json` – RSS → `articles.json` (inkl. Geo‑Scoring nach ADR‑0003, vereinfacht)
- `flows/n8n-phase2-export.json` – Webhook → `newsletter.json` (sortiert, dedupliziert)
- `docs/specs/article.schema.json`, `sourceprofile.schema.json`, `consentlog.schema.json`
- `docs/specs/newsletter.example.json` – Beispielausgabe
- `scripts/github-commit-step.md` – Idiotensicher committen via Browser
- `docs/runbooks/phase2-pilot.md` – Pilotplan

## n8n Import (Option A)
1. In n8n: **Workflows → Import from File** und jeweils die JSON aus `flows/` wählen.
2. Öffne **Ingest‑Workflow** und bearbeite den **RSS Feed Read**‑Knoten:
   - Setze deine RSS‑URL(s) ein (vorerst eine URL, mehrere per Duplizieren des Knotens).
3. Prüfe den **Write Binary File**‑Knoten:
   - Standardpfad: `/data/staging/articles.json`. Stelle sicher, dass dieses Verzeichnis im Container gemountet ist.
4. Testlauf: **Execute Workflow** → sollte `articles.json` erzeugen (Anzahl im JSON‑Output sichtbar).

## Export via Webhook
1. Starte den **Export‑Workflow**.
2. Rufe im Browser/HTTP‑Client auf: `GET https://<dein-n8n-host>/webhook/phase2/export`
3. Du erhältst `newsletter.json` (siehe `docs/specs/newsletter.example.json`).

## Anpassung Geo‑Scoring
Im Knoten **Function: Geo Score** kann die Keyword‑Liste leicht erweitert/angepasst werden (Orte in der Region Hannover, Synonyme, Stadtteile). Der Schwellwert liegt bei `0.5` (IF‑Knoten).

## JSON‑Schemas anwenden
- Validierung im Build/QA (empfohlen) oder in n8n per **Function** + Schema‑Check (z. B. `ajv` im Code‑Node eines Selbst‑Hostings).

## Commit ins Repo
Siehe `scripts/github-commit-step.md` – alles per Browser‑Upload. Master‑Versionen haben Vorrang, Navigation ggf. in `mkdocs.yml` ergänzen (existierende Einträge nicht löschen).

