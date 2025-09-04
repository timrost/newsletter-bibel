# ADR-0003: Geo-Aboutness / Region-Scoring

**Status:** Accepted  
**Datum:** 2025-09-04

## Kontext
Wir brauchen ein Verfahren zur Bewertung lokaler Relevanz („Geo-Aboutness“) für Hannover-Inhalte.

## Entscheidung
Einführung eines punktbasierten Scoring mit Buckets:
- `hannover-core` (Score >= 9)
- `region-hannover` (>= 6)
- `niedersachsen` (>= 3)
- `noise` (< 3)

## Signale & Gewichte
- „Hannover“ im Text: +5
- „Region Hannover“: +4
- Stadtteile (Whitelist): +2
- Institutionen/Orte (LUH, MHH, ÜSTRA, etc.): +3
- Domain-Bonus (hannover.de, visit-hannover.com): +4; regionale Medien (haz.de, np.de, ndr.de): +3
- PLZ 301xx–306xx: +2
- Geokoordinaten: <=5km +6; <=15km +4; <=30km +2

## Governance
- Konfigurierbar per JSON/YAML
- Transparenz: Score + Bucket werden mitgespeichert
- Redaktion prüft Stichproben und passt Gewichte an

## Compliance
- Keine Volltexte aus Quellen mit TDM-Sperre
- Speicherung minimaler Metadaten (Titel, Link, Datum, Quelle, Score)

## Beispiel
- „Sperrung Lister Meile am Wochenende“ → hannover-core
- „Landtag beschließt Gesetz“ → niedersachsen/region-hannover (abhängig vom Kontext)
- „Sturmwarnung Küste“ → noise

---
