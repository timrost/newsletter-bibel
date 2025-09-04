# ADR‑0003 Appendix: Implementation Notes & Schema.org‑Anreicherung
**Bezug:** _ADR‑0003: Geo‑Aboutness/Region‑Scoring_ (Status: Accepted, 2025‑09‑04) – **nicht überschreiben**, sondern **ergänzen**.

## Ziel dieses Anhangs
- **Kompatibilität**: Beibehaltung der in ADR‑0003 akzeptierten **Buckets** (`noise`/`niedersachsen`/`region-hannover`/`hannover-core`).
- **Operationalisierung**: Konkrete Felder, Parser und **Schema.org**‑Anreicherung (`NewsArticle`, `contentLocation`, `spatialCoverage`).
- **Transparenz**: Speicherung `geo_bucket`, `geo_score`, Quelle, Regeln (für Audits).

## 1) Feature‑Mapping (ADR‑0003 → Implementierung)
- **Toponyme/Entitäten (Titel/Text)** → NER (de/en) + Gazetteer (Hannover, Stadtteile, Umland).  
- **Institutionen/Orte** → Whitelists (LUH, MHH, ÜSTRA, GVH, Herrenhäuser Gärten …).  
- **Domain‑Bonus** → Source‑Profiles (`hannover.de`, `visit-hannover.com`, `haz.de`, `ndr.de`, `rtl.de`, `sat1regional.de`).  
- **PLZ‑Muster** → Regex `30[1-6][0-9][0-9]`.  
- **Geokoordinaten** → Distanz zum Zentrum (52.3745, 9.7386) mit Schwellen (≤5/≤15/≤30 km).

## 2) Schema.org‑Anreicherung (für Web/Archiv)
Auf Artikel‑Detailseiten `NewsArticle` nutzen und **mindestens** setzen:
- `contentLocation`: Hannover bzw. Stadtteil/Ort (Thing → Place)
- `spatialCoverage`: „Region Hannover“ (AdministrativeArea)
- optional `locationCreated` (bei Events)
Dies erleichtert **Maschinenverständnis** & spätere **Re‑Scorings**.

## 3) Persistenz & Telemetrie (DSGVO‑minimal)
Speichere **nur**: `title`, `link`, `pubDate`, `source(_domain)`, `geo_score`, `geo_bucket`, optionale `geo`‑Koordinate, `source_policy`.  
Keine personenbezogenen Daten. Audit‑Stichprobe wöchentlich beibehalten.

## 4) Beispiel (vereinheitlicht)
```json
{
  "title": "Sperrung Lister Meile am Wochenende",
  "link": "https://visit-hannover.com/...",
  "pubDate": "2025-09-04T09:00:00Z",
  "source": "visit-hannover",
  "source_domain": "visit-hannover.com",
  "geo": { "lat": 52.391, "lon": 9.750 },
  "geo_score": 11,
  "geo_bucket": "hannover-core",
  "source_policy": "rss_only"
}
```

## 5) Roadmap‑Hinweise
- Gazetteer & Whitelists versionieren (YAML), kleine **Gewicht‑Anpassungen** (±1) per Review‑Zyklus.
- Evaluation: n≥500 Items / Bucket‑Verteilung / Fehlklassifikationen.

_Anmerkung:_ Diese Datei ist eine **Ergänzung**; die akzeptierte ADR‑0003 bleibt maßgeblich.
