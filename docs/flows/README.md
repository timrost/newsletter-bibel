# Flows – Phase 2 (Multi‑Region, MVP Hannover)

Diese Seite dokumentiert die produktiven Flows für Phase 2 sowie den Umgang mit älteren (Legacy) Flows.

## Produktive Flows

### 1) Ingest (Loop Feeds → articles.json)
**Datei:** `n8n-phase2-ingest-loop-feeds.json`  
**Zweck:** Liest alle Feeds aus `/data/config/feeds.json` (Fallback enthalten), normalisiert die Items auf das `Article`‑Schema und schreibt **immer** eine Datei:
``/data/staging/articles.json``

**Highlights**
- **Multi‑Region‑Scoring**: setzt `detected_region`, `region_score`, `region_scores{}` je Artikel.
- **Fallback**: Falls `feeds.json` fehlt/leer ist, werden 1–2 Start‑Feeds genutzt.
- **Einfach skalierbar**: Feeds nur in `/data/config/feeds.json` pflegen (Discovery‑Flow erzeugt/aktualisiert sie).

**Voraussetzungen**
- In deinem Docker‑Setup muss `/home/timrost/n8n/data` nach **`/data`** im Container gemountet sein (ist bei dir der Fall).
- Ordner `/home/timrost/n8n/data/staging/` existiert (wird bei Bedarf angelegt).

**Scheduling (Beispiel)**
- Stündlich: Cron‑Node in n8n (z. B. *At minute 5, every hour*).  
- **Wichtig:** Nur **einen** Ingest‑Flow aktiv haben, damit `articles.json` nicht parallel überschrieben wird.

---

### 2) Export (→ newsletter.json, `?region=` Filter)
**Datei:** `n8n-phase2-export-by-region.json`  
**Webhook:** `GET /webhook/phase2/export`

**Parameter**
- `?region=region-hannover` (oder `berlin`, `muenchen`, …) – optional. Ohne Parameter: alle Regionen.

**Antwort (verkürzt)**
```json
{
  "export_version": "1.1.0",
  "generated_at": "…",
  "region_filter": "region-hannover",
  "count": 42,
  "articles": [ … ]
}
```

**Sortierung & Dedupe**
- Sortierung: `region_score` DESC, dann `published_at` DESC.
- Dedupe: nach `url`/`id`.

**Test**
```bash
curl "http://192.168.178.4:5678/webhook/phase2/export?region=region-hannover"
```

---

### 3) Discovery (Seeds → feeds.json)
**Datei:** `n8n-phase2-discovery-seeds-to-feeds.json`  
**Zweck:** Nimmt eine Liste **Start‑URLs** (Behörden, lokale Medien, Hochschulen …), extrahiert **RSS/Atom** aus dem HTML‑Head und schreibt:
``/data/config/feeds.json``

**Ablauf**
1. Seeds pflegen (Function‑Node „Seeds“).
2. **Execute** → Ergebnis unter `/data/config/feeds.json`.
3. Ingest‑Loop nutzt diese Feeds automatisch.

**Tipp:** pro Region eigene Seeds pflegen und `feeds.json` nach Regionen segmentieren (z. B. `/data/config/feeds.region-hannover.json`).

---

## Umgang mit Legacy‑Flows

**Ältere Dateien** (u. a. `n8n-phase2-ingest.json`, `n8n-phase2-ingest-mvp-hannover.json`, `n8n-phase2-export.json`) dienen als Referenz.

Empfehlung:
- In n8n **deaktivieren** und mit Präfix **„LEGACY – …“** umbenennen, **oder**
- im Repo unter `docs/flows/legacy/` archivieren (Navigation optional).

**Wichtig:** Aktiv lasse **nur**:
- `Ingest (Loop Feeds → articles.json)`  
- `Export (→ newsletter.json, ?region=)`  
- (Discovery nur manuell/zeitgesteuert nach Bedarf.)

---

## Fehlerbilder & Checks

- **`articles.json` fehlt/leer** → Ingest nicht gelaufen? `staging/` vorhanden? Feeds in `feeds.json` korrekt?  
- **Export 404** → Export‑Flow nicht **aktiviert**.  
- **`count` sehr niedrig** → Feeds liefern wenig Regionales *oder* Scoring zu streng → Region‑Keywords/Pfadregeln erweitern.  
- **Cookie/HTTPS‑Hinweis** → In LAN `N8N_SECURE_COOKIE=false`; später über Reverse‑Proxy + TLS wieder aktivieren.

---

Stand: 2025-09-04
