# ADR‑0003: Geo‑Aboutness / Region‑Scoring

**Status:** *Accepted*  
**Datum:** 2025‑09‑04

### Kontext
Für den Hannover‑Newsletter braucht es ein robustes, transparentes Verfahren, um die **räumliche Relevanz („Geo‑Aboutness“)** von Inhalten zu bestimmen. Datenquellen sind unterschiedlich (RSS, HTML), Metadaten (GeoRSS, Kategorien) sind inkonsistent. Gleichzeitig sind rechtliche Rahmenbedingungen (UWG/DSGVO/TDDDG/UrhG, TDM‑Opt‑out) zu beachten.

### Entscheidung
Wir führen ein **punktbasiertes Scoring** mit vier Buckets ein: `noise` < `niedersachsen` < `region-hannover` < `hannover-core`. Das Scoring ist **deterministisch**, erklärbar und kann pro Quelle feinjustiert werden.

#### Signalgruppen & Gewichte (Baseline)
- **Toponyme (Titel/Text)**: „Hannover“ +5; „Region Hannover“ +4; **Stadtteilnamen** je +2 (Whitelist, pflegbar).
- **Institutionen/Orte**: LUH/MHH/ÜSTRA/GVH/Herrenhäuser Gärten/Maschsee/Expo Plaza/ZAG/HDI etc.: je +3.
- **Domain‑Bonus**: `hannover.de`/`visit-hannover.com`: +4; regionale Medien (haz.de, neuepresse.de, ndr.de, rtl.de, sat1regional.de): +3.
- **PLZ‑Muster**: 301xx–306xx: +2.
- **Geokoordinaten**: ≤5 km vom Zentrum (52.3745, 9.7386) +6; ≤15 km +4; ≤30 km +2.

**Buckets:** `>=9` → **hannover‑core**, `>=6` → **region‑hannover**, `>=3` → **niedersachsen**, sonst `noise`.

#### Datenmodell
```json
{
  "title": "…",
  "link": "https://…",
  "pubDate": "2025-09-04T09:00:00Z",
  "source": "…",
  "source_domain": "…",
  "summary": "…",
  "geo": { "lat": 52.37, "lon": 9.74 },
  "geo_score": 11,
  "geo_bucket": "hannover-core",
  "source_policy": "rss_only|html_allowed|block_tdm"
}
```

#### Governance
- **Konfigurierbar** per YAML/JSON: Stadtteil‑Liste, Entitäten, Domain‑Gewichte, Schwellwerte.
- **Transparenz**: Jeder Newsletter‑Eintrag zeigt `geo_bucket` + Quelle.
- **Auditing**: Wöchentliche Stichprobe (20 Items) durch Redaktion → Feedback fließt in Gewichte (kleine Schritte ±1).

### Konsequenzen
- Erhöhte Präzision bei lokaler Relevanz, weniger Rauschen.
- Geringes Risiko von Fehlklassifikationen bei Ambiguitäten (z. B. „Hannover Messe“ vs. Standort CeBIT‑Historie) → Redaktionskontrolle behält Vetorecht (`force_bucket`).
- Einfach erweiterbar auf andere Regionen (nur Konfig tauschen).

### Abgrenzung/Compliance
- **Keine Volltexte** von Quellen mit TDM‑Sperre; nur Teaser/Links aus RSS.
- **Speicherung** nur minimaler Metadaten (Titel, Link, Datum, Quelle, Bucket, Score). Keine personenbezogenen Daten.

### Tests (Beispiele)
- **Positiv**: „Sperrung Lister Meile am Wochenende“ (visit‑hannover.com) → viele Stadtteil/Orts‑Treffer → `hannover-core`.
- **Grenzfall**: „Landtag beschließt Gesetz X“ → `niedersachsen`; wird `region-hannover`, wenn Ort/Institution in Hannover referenziert.
- **Negativ**: „Niedersachsen: Sturmwarnung Küste“ → `noise` für Hannover‑Newsletter (sofern keine lokale Relevanz im Text).

---