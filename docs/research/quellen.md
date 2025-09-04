# Quellen & Discovery

**Ziel:** Pro Landkreis lokale **und** überregionale Anbieter automatisch identifizieren und gewichten.

## Saatlisten
- BDZV‑Verzeichnis (Zeitungen DE), IVW‑Daten, Wikipedia‑Listen.
- Offizielle Feeds (Presseportal/Polizei, Landtage, IHK/HWK).

## Regeln
- **RSS bevorzugen**, ansonsten HTML mit Robots/TDM‑Check.
- Überregionale Quellen zulassen; **Geo‑Aboutness** entscheidet.
- Domains mit TDM‑Opt‑out nur über Feeds/APIs nutzen.

## Qualität
- Dubletten via MinHash/LSH bündeln, eine Story je Thema.
- Review‑Gate für mittlere Konfidenz.
