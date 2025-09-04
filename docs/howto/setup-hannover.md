# Setup Hannover MVP (n8n Flow)

(n8n‑Flow)

### Ziel
Automatischer stündlicher Pull von Hannover‑Quellen (RSS/HTML), **Geo‑Aboutness** bewerten, Duplikate filtern, Policies beachten, JSON‑Export fürs Newsletter‑Build.

### Überblick Workflow
1. **Trigger**: *Cron* (z. B. alle 60 min).
2. **Quellen laden**: *HTTP Request* (für HTML) und *RSS Read* (für Feeds) – pro Quelle parallel.
3. **Normalisieren**: *Function* → {title, link, pubDate, summary, source, source_domain}.
4. **Policy‑Gate**: *IF* → `source_policy` entscheidet, ob HTML‑Teaser verworfen wird.
5. **Geo‑Scoring** (Function, siehe unten) → `geo_score`, `geo_bucket`.
6. **Dedup**: *Data Store* (n8n) – upsert by `hash`.
7. **Export**: *Write Binary File* → `/data/hannover_feed.json` **und** *HTTP Request (GitHub API)* → Commit nach `docs/data/…` im „Bibel“-Repo.
8. **Notify (optional)**: *Discord/Email* mit Count & Top‑Items.

### Variablen (n8n → Credentials/Env)
- `HN_CENTER_LAT=52.3745`, `HN_CENTER_LON=9.7386`
- `STRICT_OPT_OUT_DOMAINS=["haz.de","rnd.de","bild.de"]` (erweiterbar)
- `RSS_SOURCES=[ … ]` (Liste aus *research/quellen.md*)
- `HTML_SOURCES=[ … ]` (nur Quellen mit **OK/html_allowed**)

### Beispiel: Geo‑Scoring (Function‑Node, JavaScript)
```js
// Input: items[] mit { title, link, summary, content, pubDate, source, source_domain, geo }
const CENTER = { lat: 52.3745, lon: 9.7386 };
function distKm(lat, lon){
  const R=6371, dLat=(lat-CENTER.lat)*Math.PI/180, dLon=(lon-CENTER.lon)*Math.PI/180;
  const a=Math.sin(dLat/2)**2 + Math.cos(lat*Math.PI/180)*Math.cos(CENTER.lat*Math.PI/180)*Math.sin(dLon/2)**2;
  return 2*R*Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
}
const districts = [
  "Mitte","Calenberger Neustadt","Zoo","Oststadt","List","Vahrenwald","Bothfeld","Vahrenheide","Sahlkamp","Hainholz","Nordstadt","Linden","Ricklingen","Ahlem","Badenstedt","Davenstedt","Wettbergen","Südstadt","Bult","Döhren","Wülfel","Mittelfeld","Bemerode","Kirchrode","Anderten","Misburg","Heideviertel","Groß-Buchholz","Kleefeld","Vinnhorst","Marienwerder","Lahe","Isernhagen-Süd","Seelhorst","Waldheim","Wülferode","Herrenhausen","Stöcken","Limmer" // erweiterbar
];
const entities = [
  "Hannover 96","Leibniz Universität Hannover","LUH","Medizinische Hochschule Hannover","MHH","ÜSTRA","GVH","Region Hannover","Herrenhäuser Gärten","Maschsee","Lister Meile","Ihme-Zentrum","HDI Arena","ZAG Arena","Messe Hannover","Kröpcke","Eilenriede","Sprengel Museum","Kestnergesellschaft","Leine","Expo Plaza"
].map(e => e.toLowerCase());

return items.map(item => {
  const text = ((item.title||'')+' '+(item.summary||'')+' '+(item.content||'')).toLowerCase();
  let score = 0;
  if (text.includes('hannover')) score += 5;             // Stadtname im Titel/Text
  if (text.includes('region hannover')) score += 4;       // Verwaltungsbezug
  score += districts.filter(d => text.includes(d.toLowerCase())).length * 2;  // Stadtteile
  score += entities.filter(e => text.includes(e)).length * 3;                 // markante Orte/Institutionen
  if (item.source_domain && /(^|\.)hannover\.(de|com)$/.test(item.source_domain)) score += 4; // Domainbonus
  if (item.source_domain && /(haz\.de|neuepresse\.de|ndr\.de|rtl\.de|sat1regional\.de)/.test(item.source_domain)) score += 3; // Regionale Medien
  if (/30[1-6]\d{2}\b/.test(text)) score += 2;           // PLZ 301xx–306xx
  if (item.geo && item.geo.lat && item.geo.lon){
    const d = distKm(item.geo.lat, item.geo.lon);
    if (d <= 5) score += 6; else if (d <= 15) score += 4; else if (d <= 30) score += 2; // Stadt/Region
  }
  const bucket = score >= 9 ? 'hannover-core' : score >= 6 ? 'region-hannover' : score >= 3 ? 'niedersachsen' : 'noise';
  return { ...item, geo_score: score, geo_bucket: bucket };
});
```

### Policy‑Gate (Function‑Node)
```js
const STRICT = (process.env.STRICT_OPT_OUT_DOMAINS||'[]');
const blocked = new Set(JSON.parse(STRICT));
return items.filter(i => {
  const host = (i.source_domain||'').toLowerCase();
  if (blocked.has(host)) return false; // komplett sperren
  if (i.source_policy === 'rss_only') { i.content = ''; i.summary = i.summary?.slice(0,160)||''; }
  if (i.source_policy === 'html_allowed') { /* belassen */ }
  return true;
});
```

### Dedup (Data Store)
- Key: `sha256(canonical_url)`
- Felder: `title, link, pubDate, source, source_domain, geo_score, geo_bucket, summary`.

### Export
- `Write Binary File` → `/data/hannover-items.json`
- GitHub API: Commit nach `docs/data/hannover-items.json` im Bibel‑Repo (Branch `main`).

### Minimaler Workflow‑Export (Skelett)
```json
{
  "name": "hannover_mvp_ingest",
  "nodes": [
    {"parameters": {"triggerTimes": {"item": [{"hour": ["*/1"], "minute": ["0"]}]}}, "id": "cron", "name": "Cron hourly", "type": "n8n-nodes-base.cron", "typeVersion": 1},
    {"parameters": {"urls": "={{$json.RSS_SOURCES}}"}, "id": "rss", "name": "RSS Read", "type": "n8n-nodes-base.rssFeedRead", "typeVersion": 1},
    {"parameters": {"functionCode": "// normalize items to common schema\nreturn items.map(i=>({json:{title:i.json.title,link:i.json.link,pubDate:i.json.isoDate||i.json.pubDate,summary:i.json.contentSnippet||'',source:i.json.feedTitle||'',source_domain:(new URL(i.json.link)).hostname,source_policy:'rss_only'}}));"}, "id": "normalize", "name": "Normalize", "type": "n8n-nodes-base.function", "typeVersion": 2},
    {"parameters": {"functionCode": "// policy gate (env STRICT_OPT_OUT_DOMAINS)\nconst blocked=new Set((process.env.STRICT_OPT_OUT_DOMAINS?JSON.parse(process.env.STRICT_OPT_OUT_DOMAINS):[]));\nreturn items.filter(i=>!blocked.has(i.json.source_domain));"}, "id": "policy", "name": "Policy Gate", "type": "n8n-nodes-base.function", "typeVersion": 2},
    {"parameters": {"functionCode": "// geo scoring (gekürzt)\nconst CENTER={lat:52.3745,lon:9.7386};\nreturn items.map(i=>{const t=(i.json.title+' '+i.json.summary).toLowerCase();let s=0;if(t.includes('hannover'))s+=5;if(t.includes('region hannover'))s+=4;return {json:{...i.json,geo_score:s,geo_bucket:(s>=9?'hannover-core':s>=6?'region-hannover':s>=3?'niedersachsen':'noise')}}});"}, "id": "score", "name": "Geo Score", "type": "n8n-nodes-base.function", "typeVersion": 2},
    {"parameters": {"operation": "upsert","schema": {"fields": [{"fieldName": "id","type": "string","isPrimaryKey": true},{"fieldName":"title","type":"string"},{"fieldName":"link","type":"string"},{"fieldName":"pubDate","type":"string"},{"fieldName":"source","type":"string"},{"fieldName":"source_domain","type":"string"},{"fieldName":"geo_score","type":"number"},{"fieldName":"geo_bucket","type":"string"}]}}, "id": "store", "name": "Data Store Upsert", "type": "n8n-nodes-base.datastore", "typeVersion": 1},
    {"parameters": {"fileName": "/data/hannover-items.json", "data": "={{JSON.stringify($items(\"score\").map(i=>i.json))}}"}, "id": "file", "name": "Write JSON", "type": "n8n-nodes-base.writeBinaryFile", "typeVersion": 1}
  ],
  "connections": {"Cron hourly": {"main": [[{"node": "RSS Read","type": "main","index": 0}]]},"RSS Read": {"main": [[{"node": "Normalize","type": "main","index": 0}]]},"Normalize": {"main": [[{"node": "Policy Gate","type": "main","index": 0}]]},"Policy Gate": {"main": [[{"node": "Geo Score","type": "main","index": 0}]]},"Geo Score": {"main": [[{"node": "Data Store Upsert","type": "main","index": 0},{"node": "Write JSON","type": "main","index": 0}]]}}
}
```

> **Austauschbare Teile:** Ergänze `HTML_SOURCES` + zusätzliche „HTTP Request“‑Nodes für Quellen mit `html_allowed`; die Normalisierung erwartet {title, link, summary, pubDate}.

### Compliance‑Check (automatisiert)
- Bei jedem Run wird **robots.txt** der HTML‑Quellen wöchentlich gecacht und nach Sperren (`GPTBot`, `CCBot`, `PerplexityBot`, `ClaudeBot`, `noai`, `tdm‑reservation`) gescannt. Falls Treffer → auf `rss_only` setzen oder komplett blocken.
- Header‑Checks (optional): `X‑Robots‑Tag`, `tdm-reservation: 1`.