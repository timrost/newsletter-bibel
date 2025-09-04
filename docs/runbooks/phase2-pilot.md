# Phase 2 – Pilotplan

**Ziel:** End‑to‑End‑Test des regionalen KI‑Newsletters (Hannover) mit minimalem Setup.

## Testdaten & Quellen
- Mindestens 3 RSS‑Feeds aus der Region (z. B. Stadt/Region‑Portale, Hochschulen, Wirtschaftsförderung). Platzhalter im Ingest‑Workflow ersetzen.
- Optional: 1–2 neutrale Tech‑Feeds zum Negativtest (sollten durch Geo‑Score < 0.5 herausfallen).

## Schritte
1. **Import & Konfiguration** der beiden n8n‑Workflows (siehe Phase2‑README).
2. **Testlauf Ingest:** erzeugt `/data/staging/articles.json`.
3. **Export‑Webhook aufrufen:** `GET /webhook/phase2/export` → `newsletter.json` prüfen.
4. **Validierung gegen Schemas:** 
   - `articles` gegen `article.schema.json`
   - Quellenliste gegen `sourceprofile.schema.json` (falls gepflegt)
   - DOI/Tracking‑Ereignisse (falls vorhanden) gegen `consentlog.schema.json`
5. **Review & Redaktion:** Auswahl, Kürzung, Betitelung im Redaktionsdokument (außerhalb n8n).
6. **Ablage:** `newsletter.json` in Repo unter `data/` oder `docs/samples/` committen.

## Erfolgskriterien
- ≥ 80 % der relevanten Regional‑Artikel werden korrekt erkannt (Stichprobe).
- Keine Feeds mit TDM‑Opt‑out werden verarbeitet (Check der Quellenliste/robots).
- `newsletter.json` validiert gegen Schema, dedupliziert & nach Relevanz sortiert.
- Durchlaufzeit von Ingest bis Export < 5 Minuten (manuell angestoßen).

## Rollback
- In n8n beide Workflows **deaktivieren** (Toggle off).
- Entferne/archiviere `articles.json` und Testdateien aus dem gemounteten Pfad.
- Im Repo den Pilot‑Branch zurücksetzen oder PR schließen, falls unerwünscht.

## Nächste Schritte (nach Pilot)
- Mehrfach‑Feeds (Duplizierte RSS‑Knoten) + Fehlerhandling (HTTP‑Codes, Timeouts).
- Zusätzliche Provider (z. B. JSON APIs) & Bild‑Policy gemäß **ADR‑0004 (Proposed)**.
- Automatisierter DOI‑/Consent‑Log bei Pilot‑Abonnenten (Schema vorhanden).
