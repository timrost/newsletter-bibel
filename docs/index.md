# Regionaler KI‑Newsletter (DE) – Projekt‑Bibel

Diese Dokumentation ist die **einzige verbindliche Quelle** für Ziele, Entscheidungen und Abläufe unseres Projekts.  
Chats dienen nur zur Erarbeitung – relevante Ergebnisse landen **immer hier**.

## Leitprinzipien
- **Rechtskonform (DE/EU):** UWG/DSGVO/DDG/**TDDDG**/UrhG; Snippet‑Ausnahme & TDM‑Opt‑out beachten.
- **Regionaltreue:** 100 % passende Inhalte je Landkreis (Geo‑Scoring & Aboutness, ADR‑0003).
- **Vollautomatisierung + Review‑Gate:** Mensch‑im‑Loop anfangs aktivierbar.
- **Vendor‑neutral:** Self‑host‑fähig; **Git‑Repo als Single Source of Truth**.

#### Prompt für neue Themen (für Chat)
```json
{
  "Update": "Bitte beachten 🚨",
  "Projekt-Bibel": "https://timrost.github.io/newsletter-bibel/",
  "Repo": "https://github.com/timrost/newsletter-bibel",
  "Phase": "1 – Doku zuerst (Phase 2 Technik danach)",
  "Ziel dieses Chats": "<Thema>",
  "Deliverables": ["<…>"],
  "Arbeitsweise": {
    "Uploads": "GitHub-Weboberfläche (Option A)",
    "Master-Versionen": "haben Vorrang vor Kurzfassungen",
    "Bibelbasiert": "ja – mit frischer Web-Recherche & Zitaten (Primärquellen)",
    "Navigation": "mkdocs.yml ergänzen, bestehende Einträge nicht löschen"
  },
  "ADR-Hinweis": {
    "ADR-0003": "Geo-Aboutness / Region-Scoring (Accepted)",
    "ADR-0004": "Bild-Policy (folgt)"
  },
  "Bitte liefern": [
    "upload-fertige Markdown/ZIPs unter docs/",
    "README mit Merge-Schritten + mkdocs.yml-Nav-Snippet"
  ],
  "Sonstiges": {
    "Zeitzone": "Europe/Berlin",
    "Citations": "Primärquellen mit Links; für seit 2024/25 veränderte Themen aktiv browsen"
  }
}
```
