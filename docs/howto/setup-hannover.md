# Setup Hannover MVP (n8n Flow)

Automatisierter Ingest von Quellen für Hannover.

## Workflow
1. **Trigger**: Cron (stündlich).
2. **Fetch**: RSS (Feeds) + HTTP (nur html_allowed).
3. **Normalize**: Vereinheitlichung Felder.
4. **Policy Gate**: Quelle-Policy anwenden (rss_only/html_allowed).
5. **Geo-Scoring**: Punkte-System, Bucket-Einordnung (ADR-0003).
6. **Dedup**: via Data Store (sha256 URL).
7. **Export**: JSON schreiben + ins Repo committen.

## Variablen
- `HN_CENTER_LAT=52.3745`, `HN_CENTER_LON=9.7386`
- `STRICT_OPT_OUT_DOMAINS=["haz.de","neuepresse.de"]`
- `RSS_SOURCES=[…]`
- `HTML_SOURCES=[…]`

## Beispiel Geo-Scoring
Siehe ADR-0003: Punkte für Stadtteile, Institutionen, Domains, PLZ, Geokoordinaten.

## Export
- JSON-Datei `/data/hannover-items.json`
- Commit ins Repo `docs/data/hannover-items.json`

---
