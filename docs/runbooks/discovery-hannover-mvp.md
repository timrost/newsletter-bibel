# Discovery-Flow (Hannover MVP) – Automatische Feed-Suche

Ziel: Aus wenigen Seed-Homepages automatisch **echte RSS/Atom-Feeds** finden – inkl. HAZ/Neue Presse Arc-Feeds – und in `/data/config/feeds.json` dedupliziert speichern.

## Pipeline (3 Hops)

1. Seeds → GET homepage (Text) → **Extract Feeds (1st hop)**
2. IF `followUrl` (Guard `starts with http`) → HTTP Follow → **Extract Feeds (2nd hop)**
3. Optionaler 3. Hop (gleiches Muster) → **Extract Feeds (3rd hop)**
4. IF `feedUrl` → Merge (Append) → **Aggregate → feeds.json** → Write Binary File

### Node-Settings (Kurz)
- **HTTP Request (alle):** Response Text, Redirects **ON**, Header `User-Agent`
- **IFs:** `feedUrl is not empty` → True-Branch in Merge, `followUrl starts with http` → True-Branch in HTTP
- **Merge:** Append aller *feedUrl*-True-Zweige
- **Aggregator:** dedupliziert & validiert, schreibt `/data/config/feeds.json`

### Test
- Manuell starten → `feeds.json` sollte Einträge wie `.../arc/outboundfeeds/rss/tags_slug/hannover/` (HAZ) und NP-Feeds enthalten.
