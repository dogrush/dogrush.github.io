# AGENTS.md

Jekyll-based academic personal website (fork of Academic Pages / Minimal Mistakes). Serves as a static portfolio site — no server-side logic, no DB, no CI, no tests.

## Commands

```bash
bundle install                        # first-time setup
bundle exec jekyll serve -l -H localhost  # dev server at http://localhost:4000
```

- Changes to `_config.yml` require a server restart; Markdown files reload automatically.
- Docker: `chmod -R 777 . && docker compose up`
- JS minification: `npm run uglify` or `npm run build:js` (only needed after editing `assets/js/_main.js`)

## Architecture

- **Single collection defined in `_config.yml`:** `teaching` (dir `_teaching/`). All other content types (publications, talks, projects, posts) use static pages under `_pages/` with frontmatter-driven layouts.
- **Frontmatter required for collection entries:** `collection: teaching`, `layout: single`, plus `type`, `venue`, `date`, `location`.
- **Pages** (`_pages/`) use `layout: single` or `layout: archive-taxonomy`, with `author_profile: true` by default.
- **Data dirs:** `_data/navigation.yml` (header menu), `_data/cv.json` (CV content), `_data/ui-text.yml` (i18n strings).
- **Custom SCSS** in `_sass/_custom.scss` overrides theme defaults (font, link hover, masthead). Theme switched via `site_theme` in `_config.yml`.
- **CV generation:** `scripts/update_cv_json.sh` converts `_pages/cv.md` → `_data/cv.json` via `scripts/cv_markdown_to_json.py`.
- **Talk map:** `talkmap.py` geolocates talk locations from `_talks/*.md` (requires `geopy`, `getorg`).

## Quirks

- MathJax uses `$$...$$` or `\[...\]` delimiters — `$...$` does NOT work.
- `Gemfile` includes both `github-pages` (pins Jekyll for GitHub Pages compat) and individual plugins — prefer `github-pages` for accurate local preview.
- No lint, test, or typecheck framework exists in this repo.
