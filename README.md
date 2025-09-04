# Projekt‑Bibel (GitHub Pages, MkDocs Material)

## Schnellstart
```bash
pip install mkdocs-material
mkdocs build
mkdocs serve  # lokal testen
```

## GitHub Pages
- Per GitHub Actions (siehe `.github/workflows/gh-pages.yml`).
- Oder lokal: `mkdocs gh-deploy` (legt Branch `gh-pages` an).

## Hinweise
- Keine Secrets/Personendaten in `docs/`.
- Jede Entscheidung als ADR ablegen.
- Neue Erkenntnisse aus dem Chat → Commit hier.
