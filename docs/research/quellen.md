# Quellen – Hannover MVP

(Hannover)

### Zweck
Seed‑Liste für den Hannover‑MVP: verlässliche, rechtssichere Quellen für Nachrichten, Termine und Pressemeldungen aus Stadt & Region Hannover. **Policy‑Hinweis:** Gemäß ADR‑0002 (Snippet/Teaser‑Policy) werden nur kurze, eigenständige Teaser + Link verwendet; keine Bilder; respektiert Robots/TDM‑Opt‑outs.

### Kategorien & Prioritäten
- **P0 – Offizielle Stellen & Behörden** (stabil, lizenzklar, hohe Relevanz)
- **P1 – Öffentlich‑rechtliche Medien & Landesorgane** (stabil, neutral)
- **P2 – Lokalpresse & Verlage** (teils Paywall/Opt‑out; ggf. nur Titel/Link via RSS)
- **P2 – Hochschulen/Institute/Kliniken** (wissenschaftlich, regional stark)
- **P3 – Verkehr/ÖPNV & Infrastruktur** (Störungsmeldungen, Tarife, Bau)
- **P3 – Tourismus/Eventkalender/Kultur** (Termine, Highlights)

### Robots/TDM – Legende
- **OK**: keine expliziten KI/TDM‑Sperren erkennbar; Standard‑Crawl erlaubt.
- **OK (RSS only)**: HTML ggf. eingeschränkt; RSS ausdrücklich vorgesehen.
- **RESTRICT**: KI‑Bots/LLM/TDM explizit untersagt; **kein HTML‑Scrape**; wenn RSS angeboten → nur Titel/Link, kein Volltext.
- **TBD**: manuell prüfen/klären.

### Seed‑Tabelle (Stand: 04.09.2025)

| Quelle | Typ | URL | Feed/RSS | Robots/TDM | Priorität | Notizen |
|---|---|---|---|---|---:|---|
| Landeshauptstadt Hannover – Presseservice | Offizielle Stelle | https://presse.hannover-stadt.de/ | – (keinen Feed gefunden) | OK | P0 | Pressemeldungen, Rubriken; HTML parsen erlaubt, respektiert robots.
| Hannover.de – Aktuelles/Service | Offizielle Stelle | https://www.hannover.de/Service/Presse-Medien/Hannover.de/Aktuelles | – | OK | P0 | Regionalportal (Stadt+Region); tagesaktuelle Hinweise.
| Hannover.de – Sitzungsmanagement (RSS) | Offizielle Stelle | https://e-government.hannover-stadt.de/lhhsimwebre.nsf/RSSUebersicht.xsp | **RSS** | OK | P0 | Offizielle Gremien‑/Sitzungstermine als RSS.
| Region Hannover – Portal | Offizielle Stelle | https://www.hannover.de/Leben-in-der-Region-Hannover/Verwaltungen-Kommunen/Die-Verwaltung-der-Region-Hannover/Region-Hannover | – | OK | P0 | Übersicht, Pressekontakte; eigene Meldungen teils im Portal.
| Region Hannover – PresseBox | Offizielle Stelle (Newsroom) | https://www.pressebox.de/newsroom/region-hannover/pressemitteilungen | **RSS über PresseBox** | OK (RSS only) | P1 | Drittplattform; Terms beachten; RSS vorhanden.
| Niedersächsischer Landtag – Presse/RSS | Landesorgan | https://www.landtag-niedersachsen.de/rss-feeds/ | **RSS** | OK | P1 | Relevante Landesthemen; filter „Hannover“.
| Leibniz Universität Hannover – Pressemeldungen | Hochschule | https://www.uni-hannover.de/en/universitaet/aktuelles/rss-feeds | **RSS** (z. B. Pressemeldungen) | OK (RSS) | P2 | LUH News/Events/Jobs; mehrere Feeds (Online‑Aktuell, Presse, Events).
| Hochschule Hannover – Presse | Hochschule | https://www.hs-hannover.de/…/service-fuer-presse-und-medien | – | OK | P2 | Pressekontakte; ggf. Newsletter/Feeds projektweise.
| MHH – Presse | Klinik/Hochschule | https://www.mhh.de/presse | – (TBD) | OK | P2 | Pressemeldungen, Forschung; Feeds prüfen, ggf. Newsletter.
| KRH Klinikum Region Hannover – Presse | Klinik | https://www.krh.de/das-krh/presse | – | OK | P2 | Regionale Klinik‑Meldungen.
| HANNOVER MESSE – Presse | Messe/Events | https://www.hannovermesse.de/de/presse/ | – / Newsletter | OK | P2 | Großevents/Termine; Pressenewsletter.
| ÜSTRA – Pressemitteilungen | ÖPNV | https://www.uestra.de/presse/pressemitteilungen/ | – (Newsletter) | OK | P3 | Bau/Umleitungen/Service; eigene Inhalte.
| Visit Hannover (HMTG) – Events/Highlights | Tourismus | https://www.visit-hannover.com/…/Events-Veranstaltungen… | – | OK | P3 | Event‑Seeding; HTML Titel/Link.
| Hannover.de – Veranstaltungskalender | Offizielle Stelle | https://www.hannover.de/Veranstaltungskalender | – | OK | P3 | Termine; teils Detailseiten ohne Feed.
| HAZ – Hannoversche Allgemeine (RND) | Lokalpresse | https://www.haz.de/ | **RSS** (Info‑Seite) | **RESTRICT** | P2 | RSS verfügbar; robots enthält KI/TDM‑Sperren → nur Titel/Link, kein Scrape.
| Neue Presse (RND) | Lokalpresse | https://www.neuepresse.de/ | **RSS** (Info‑Seite) | **TBD/likely RESTRICT** | P2 | RSS verfügbar; robots gesondert prüfen; konservativ: nur Titel/Link.
| NDR – Niedersachsen/Hannover | ÖR‑Sender | https://www.ndr.de/nachrichten/niedersachsen/ | (Feeds vorhanden, Kanal wählen) | OK (RSS) | P1 | Regionale News; Themenfilter.
| RTL Nord – NDS/Bremen | TV/Regional | https://www.rtl.de/rtl-nord/ | – | OK | P2 | Regionales Magazin (Online/Videos); nur Titel+Link übernehmen.
| SAT.1 REGIONAL – NDS/Bremen | TV/Regional | https://www.sat1regional.de/niedersachsen/ | – | OK | P2 | Regionales Magazin; nur Titel+Link.
| Radio Hannover 100,0 – News | Radio | https://www.radio-hannover.de/ | – | OK | P3 | Lokale Kurzmeldungen/Audio; kein RSS → manuell/HTML mit Zurückhaltung.
| IPH Hannover – Presse | Institut | https://www.iph-hannover.de/de/presse/pressemitteilungen/ | **RSS** | OK (RSS) | P2 | Wissenschaft/Industrie 4.0.

> **Hinweis:** Für jede Quelle wird im Flow eine `source_policy` gesetzt: `html_allowed`, `rss_only`, `block_tdm`.

### Robots/TDM‑Check‑Log (Kurznotizen)
- **hannover.de** → Robots erlaubt Standard‑Crawl; keine spezifischen KI‑Sperren gefunden. TDM‑Opt‑out nicht ersichtlich. (robots.txt prüfen; Terms beachten.)
- **presse.hannover-stadt.de** → kein eigenes robots.txt gefunden; folgt Portalregeln; HTML erlaubt.
- **haz.de** → **RESTRICT**: robots.txt enthält explizite Sperren gegen GPTBot/CCBot/Perplexity/ClaudeBot etc. + Hinweis auf Rechtevorbehalt für kommerzielles TDM (§44b UrhG). → **Nur RSS‑Titel/Link speichern**, kein HTML‑Volltext.
- **neuepresse.de** → RSS vorhanden; robots gesondert verifizieren; bis dahin **RSS only** und **kein HTML**.
- **uni-hannover.de** → RSS explizit angeboten; Verwendung gemäß Feed‑Nutzungsrahmen; HTML optional.
- **ustra.de** → kein RSS, Newsletter möglich; HTML nur für Überschriften/Teaser mit Link; keine Bilder übernehmen.

### Operative Regeln
1. **Kein Volltext‑Scraping** aus Verlagsseiten (RND etc.).
2. **RSS bevorzugt**: Wo Feeds existieren, nur Feed‑Items (Titel, Link, Datum, ggf. Teaser) nutzen.
3. **TDM‑Opt‑out respektieren** (robots.txt, `X‑Robots‑Tag`, TDM‑ReP). Bei **RESTRICT**: `html_allowed=false`, `rss_only=true`.
4. **Attribution & Link**: immer Quelle, Rubrik (falls vorhanden) und kanonische URL speichern.
5. **Dedup**: per `hash = sha256(canonical_url)`. URL‑Normalisierung (UTM entfernen).

---