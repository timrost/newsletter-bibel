# Specs – Übersicht

Willkommen im Bereich **Spezifikationen** der Projekt‑Bibel.  
Hier findest du alle JSON‑Schemas und ein Beispiel‑Export, jeweils kurz erklärt und verlinkt.

## Inhalte

| Datei | Zweck | Typ |
|---|---|---|
| `article.schema.json` | Normiertes Artikelobjekt aus dem Ingest (Titel, URL, Zeiten, Quelle, `region_score`, Bilder) | JSON Schema |
| `sourceprofile.schema.json` | Metadaten zu Quellen (Domain, RSS, robots.txt, TDM‑Opt‑out, Kontakt) | JSON Schema |
| `consentlog.schema.json` | Ereignisse zu Zustimmung/DOI/Tracking gem. DSGVO/TTDSG | JSON Schema |
| `newsletter.example.json` | Beispielausgabe des Exports (`newsletter.json`) | Beispiel‑JSON |

**Direktlinks:**  
- [Article Schema](article.schema.json)  
- [SourceProfile Schema](sourceprofile.schema.json)  
- [ConsentLog Schema](consentlog.schema.json)  
- [Newsletter Beispiel](newsletter.example.json)

## Wann welches Schema?

- **Article**: Für alle Einträge, die aus Feeds/Quellen ins System kommen und im Export erscheinen können.  
- **SourceProfile**: Für die Pflege von Quellen inkl. Robots/TDM‑Status und Kontakt‑Infos.  
- **ConsentLog**: Für Nachweise zu Double‑Opt‑In & Tracking‑Einwilligung (Audit‑Trail).

## Versionierung & Kompatibilität

- Schemas basieren auf **JSON Schema Draft 2020‑12**.  
- Export nutzt `export_version` (aktuell `1.0.0`).  
- **Breaking Changes** → Major erhöhen; optionale Felder möglichst additive Änderungen.

## Validierung (Empfehlung)

- In QA/CI oder n8n (Code‑Node) mit einem JSON‑Schema‑Validator prüfen.  
- `newsletter.json` sollte immer gegen `article.schema.json` (für Items) validieren.

---

*Stand: 2025-09-04 · Region: Hannover*
