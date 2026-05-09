# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based academic personal website using the [Academic Pages](https://academicpages.github.io/) theme (forked from Minimal Mistakes Jekyll Theme). The site serves as a portfolio showcasing research, publications, talks, teaching, and projects.

## Running Locally

### Standard Jekyll Development
```bash
# Install dependencies (run once)
bundle install

# Start local development server (serves at http://localhost:4000)
bundle exec jekyll serve -l -H localhost
# Or use the provided script:
./start_jekyll_serve.sh
```

Note: Changes to `_config.yml` require restarting Jekyll. Changes to markdown files are auto-reloaded.

### Docker/DevContainer
```bash
# Using Docker Compose
chmod -R 777 .
docker compose up

# Using VS Code DevContainer: F1 -> DevContainer: Reopen in Container
```

## Architecture

### Collections
The site uses Jekyll collections for different content types, each with its own directory and frontmatter requirements:

- `_posts/` - Blog posts (uses `layout: single`)
- `_publications/` - Academic publications (uses `layout: single`, frontmatter includes `collection: publications`)
- `_talks/` - Conference talks/presentations (uses `layout: talk`, frontmatter includes `collection: talks`)
- `_teaching/` - Teaching materials (uses `layout: single`, frontmatter includes `collection: teaching`)
- `_portfolio/` - Project portfolio entries (uses `layout: single`, frontmatter includes `collection: portfolio`)
- `_pages/` - Static pages (uses `layout: single` or `layout: archive-taxonomy`)

### Configuration Files
- `_config.yml` - Main Jekyll configuration (site settings, author info, collections, plugins)
- `_data/navigation.yml` - Header navigation menu structure
- `_data/ui-text.yml` - UI text strings (supports internationalization)
- `_data/cv.json` - Structured CV data for generating CV pages
- `_data/authors.yml` - Multi-author blog configuration

### Content Generation
The `markdown_generator/` directory contains Jupyter notebooks (`.ipynb`) and Python scripts (`.py`) for bulk-generating publication/talk markdown files from TSV data. This is useful for importing large bibliographies.

### Layouts and Includes
- `_layouts/` - Page templates (single, talk, archive, cv-layout, splash)
- `_includes/` - Reusable components (author-profile, masthead, footer, comments, analytics)

### Assets
- `_sass/` - SCSS stylesheets
- `assets/js/` - JavaScript (main.js, plugins)
- `assets/css/` - Compiled CSS
- `images/` - Static images
- `files/` - Downloadable files (PDFs, etc.) - served at `/files/`

### Key Behaviors
- Site theme can be changed via `site_theme` in `_config.yml` (options: default, dark, contrast, air, aqua, mint, neon)
- Comments can be enabled via provider in `_config.yml` (disqus, discourse, facebook, staticman, custom)
- Publication categories are defined in `publication_category` section of `_config.yml`
- MathJax is supported for equations using `$$...$$` or `\\[...\\]` delimiters (NOT `$...$`)
