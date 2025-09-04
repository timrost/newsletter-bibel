# Systemübersicht

**Pipeline:**
1. Ingestion (RSS/HTML) → Robots/TDM‑Check
2. Extraktion (Titel, Text, Metadaten)
3. Geo‑Aboutness (Toponyme, Gazetteer, PostGIS, LLM‑Classifier)
4. Dedup/Clustering
5. Teaser (neutral, kurz) + Link
6. Ausspielung: Newsletter (Listmonk) & Website (CMS/SSG)
7. Monitoring & Review‑Gate
