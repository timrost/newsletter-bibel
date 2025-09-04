# Flows (n8n Workflows)

In diesem Ordner liegen die exportierten **n8n-Workflows** als JSON-Dateien.  
Sie können direkt in n8n über **Workflows → Import from File** eingelesen werden.

## Dateien
- **n8n-phase2-ingest.json** – Liest RSS-Feeds, berechnet einen Geo-Score für die Region Hannover (ADR‑0003), mappt auf das `Article`-Schema und erzeugt `articles.json`.
- **n8n-phase2-export.json** – Stellt einen Webhook (`/webhook/phase2/export`) bereit, liest `articles.json`, dedupliziert, sortiert und gibt `newsletter.json` zurück.

## Nutzung
1. In n8n einloggen → **Import from File**.
2. Den gewünschten Flow auswählen und aktivieren.
3. RSS-Quellen bzw. Pfade anpassen (siehe Runbooks).
