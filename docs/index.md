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
  "Phase": "2 – Technik (nach Doku-Phase abgeschlossen am 2025-09-04)",
  "Ziel dieses Chats": "<Thema>",
  "Deliverables": ["<…>"],
  "Arbeitsweise": {
    "Uploads": "GitHub-Weboberfläche (Option A)",
    "Master-Versionen": "haben Vorrang vor Kurzfassungen",
    "Bibelbasiert": "ja – nur Inhalte der Bibel + frische Web-Recherche mit Primärquellen",
    "Navigation": "mkdocs.yml ergänzen, bestehende Einträge nicht löschen",
    "Keine Hintergrundarbeit": "Alles im Chat, sofort lieferbar"
  },
  "ADR-Hinweis": {
    "ADR-0003": "Geo-Aboutness / Region-Scoring (Accepted, Appendix integriert)",
    "ADR-0004": "Bild-Policy (Proposed)"
  },
  "Bitte liefern": [
    "upload-fertige Markdown/ZIPs unter docs/",
    "n8n-Flows (export JSON), JSON-Schemas, GitHub-Commit-Step",
    "README mit Merge-Schritten + mkdocs.yml-Nav-Snippet"
  ],
  "Sonstiges": {
    "Zeitzone": "Europe/Berlin",
    "Citations": "Primärquellen mit Links; für seit 2024/25 veränderte Themen aktiv browsen"
  }
}
```
