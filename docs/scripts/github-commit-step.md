# GitHub Commit (Option A – Browser‑Upload)

**Ziel:** Dateien ohne Terminal direkt ins Repo hochladen.  
Repo: https://github.com/timrost/newsletter-bibel

## Schritt‑für‑Schritt
1. Öffne das Repo im Browser → **Add file** → **Upload files**.
2. Ziehe die Dateien/Ordner in den Upload‑Bereich **oder** wähle sie aus:
   - `flows/n8n-phase2-ingest.json`
   - `flows/n8n-phase2-export.json`
   - `docs/specs/article.schema.json`
   - `docs/specs/sourceprofile.schema.json`
   - `docs/specs/consentlog.schema.json`
   - `docs/specs/newsletter.example.json`
   - `docs/runbooks/phase2-readme.md`
   - `docs/runbooks/phase2-pilot.md`
3. Commit‑Message (z. B.): `feat(phase2): n8n flows, schemas, export example & runbooks`
4. **Commit directly to main** (oder Branch → PR), dann **Commit changes**.

## Navigation (mkdocs)
- Falls nötig, `mkdocs.yml` per Browser öffnen → **Edit** → neue Einträge ergänzen (bestehende nicht löschen):
  ```yaml
  nav:
    - Runbooks:
      - Phase 2 Readme: docs/runbooks/phase2-readme.md
      - Pilotplan: docs/runbooks/phase2-pilot.md
    - Specs:
      - Article Schema: docs/specs/article.schema.json
      - SourceProfile Schema: docs/specs/sourceprofile.schema.json
      - ConsentLog Schema: docs/specs/consentlog.schema.json
      - Newsletter Beispiel: docs/specs/newsletter.example.json
  ```

## Hinweise
- Keine API‑Keys im Repo ablegen. Sensible Daten nur lokal in `.env`.
- Bei großen Dateien vorher prüfen, ob sie wirklich ins Repo gehören.
