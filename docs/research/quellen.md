# Quellen – Hannover MVP

Seed-Liste für den Hannover-MVP. Grundlage: ADR-0002 Snippet/Teaser-Policy (nur kurze Teaser + Link, keine Bilder). Robots/TDM-Opt-outs strikt beachtet.

## Kategorien
- **P0** Offizielle Stellen/Behörden
- **P1** Öffentlich-rechtliche Medien, Landesorgane
- **P2** Lokalpresse, Hochschulen/Kliniken
- **P3** Verkehr, Events, Tourismus

## Seed-Tabelle (Auszug)
| Quelle | Typ | URL | Feed/RSS | Robots/TDM | Priorität | Policy |
|--------|-----|-----|----------|------------|-----------|--------|
| Landeshauptstadt Hannover – Presseservice | Offizielle Stelle | https://presse.hannover-stadt.de/ | – | OK | P0 | html_allowed |
| Hannover.de – Aktuelles | Offizielle Stelle | https://www.hannover.de/Service/Presse-Medien/Hannover.de/Aktuelles | – | OK | P0 | html_allowed |
| Hannover.de – Sitzungsmanagement | Offizielle Stelle | https://e-government.hannover-stadt.de/lhhsimwebre.nsf/RSSUebersicht.xsp | RSS | OK | P0 | rss_only |
| Region Hannover – PresseBox | Offizielle Stelle | https://www.pressebox.de/newsroom/region-hannover/pressemitteilungen | RSS | OK | P1 | rss_only |
| NDR Niedersachsen | ÖR | https://www.ndr.de/nachrichten/niedersachsen/ | RSS | OK | P1 | rss_only |
| HAZ – Hannoversche Allgemeine | Lokalpresse (RND) | https://www.haz.de/ | RSS | RESTRICT (KI/TDM-Sperre) | P2 | rss_only |
| Neue Presse | Lokalpresse (RND) | https://www.neuepresse.de/ | RSS | RESTRICT (KI/TDM-Sperre) | P2 | rss_only |
| Leibniz Uni Hannover – Presse | Hochschule | https://www.uni-hannover.de/en/universitaet/aktuelles/rss-feeds | RSS | OK | P2 | rss_only |
| MHH – Presse | Hochschule/Klinik | https://www.mhh.de/presse | – | OK | P2 | html_allowed |
| ÜSTRA – Pressemitteilungen | ÖPNV | https://www.uestra.de/presse/pressemitteilungen/ | – | OK | P3 | html_allowed |

### Robots/TDM-Check
- **haz.de / neuepresse.de**: robots.txt enthält explizite Verbote für GPTBot, CCBot, Perplexity, ClaudeBot → nur RSS (Titel/Link). Quelle: robots.txt Stand 04.09.2025.
- **hannover.de**: keine KI-Sperren, Standard-Crawl erlaubt.
- **ndr.de**: Feeds vorgesehen, OK.
- **uni-hannover.de**: Feeds vorgesehen, OK.

---
