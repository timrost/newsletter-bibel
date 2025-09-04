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

---

## Appendix – Implementation Notes (merged 2025-09-04)

# ADR‑0003 Appendix (v2): Implementation Notes & Schema.org
**Bezug:** ADR‑0003 „Geo‑Aboutness/Region‑Scoring“ (**Accepted**).  
**Änderung in v2:** Vereinheitlichte `source_policy`‑Werte und Beispiele.

## 1) `source_policy` – zulässige Werte
| Wert            | Bedeutung                                          | Beispiel‑Domains              |
|-----------------|-----------------------------------------------------|-------------------------------|
| `rss_only`      | Nur bereitgestellte RSS/Atom‑Feeds verarbeiten.     | `haz.de` (robots Restriktionen) |
| `html_allowed`  | HTML‑Seiten dürfen gecrawlt/geparst werden.         | `hannover.de`, `visit-hannover.com` |
| `block_tdm`     | Kein TDM erlaubt (Opt‑out/robots/Terms), respektieren. | ggf. Verlagsseiten mit KI‑Sperren |

> **HAZ robots.txt:** „The use of robots or other automated means to access haz.de or collect or minedata … is strictly prohibited …“ → `rss_only`/`block_tdm` je nach Vertragssituation.

## 2) Schema.org‑Anreicherung
`NewsArticle` mit mindestens `contentLocation` (Place) und `spatialCoverage` (AdministrativeArea: „Region Hannover“). Optional: `locationCreated` (Events).

## 3) Persistenz (DSGVO‑minimal)
Speichere: `title`, `link`, `pubDate`, `source(_domain)`, `geo_score`, `geo_bucket`, optionale `geo`‑Koordinate, `source_policy`. Keine personenbezogenen Daten.

## 4) Einheitliches Beispiel
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
  "source_policy": "html_allowed"
}
```

## 5) Governance & Evaluation
- Gazetteer/Whitelists versionieren (YAML).  
- Regel‑Änderungen via Review (±1 Gewichtungen).  
- Evaluation: n≥500 Items / Bucket‑Verteilung / Fehlklassifikationen.

## 6) Belege
- HAZ robots.txt (Automatisierung untersagt): https://www.haz.de/robots.txt
