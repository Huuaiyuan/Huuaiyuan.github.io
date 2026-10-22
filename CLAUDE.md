# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal academic website built from the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template (v0.9.x, itself a detached fork of Minimal Mistakes). This is the user's own site (repo `Huuaiyuan/Huuaiyuan.github.io`, served at https://huuaiyuan.github.io/), not the upstream template — **do not open PRs back to `academicpages/academicpages.github.io`** (see `AGENTS.md`). Most work here is editing content and `_config.yml`, not changing the theme.

## Commands

```bash
bundle install                          # Ruby deps (if permission errors: bundle config set --local path 'vendor/bundle')
bundle exec jekyll serve -l -H localhost  # Preview at http://localhost:4000 with livereload
bundle exec jekyll build                # Build into _site/ (what CI runs, with JEKYLL_ENV=production)
bundle exec jekyll build --strict_front_matter  # Stricter check, catches bad YAML front matter

# Containerized preview (Ruby isn't installed locally). docker-compose.yaml only runs `sleep infinity` for the devcontainer, so use:
docker build -t jekyll-site .
docker run --rm -it -p 4000:4000 -e JEKYLL_ENV=docker -v "$PWD":/usr/src/app -u 1000:1000 jekyll-site \
  bundle exec jekyll serve -H 0.0.0.0 --config _config.yml,_config_docker.yml
# -> http://localhost:4000/

npm install && npm run build:js         # Rebuild assets/js/main.min.js after editing assets/js/*.js
python3 markdown_generator/publications.py markdown_generator/publications.csv  # Generate publication .md files (accepts .csv or .tsv)
python3 markdown_generator/talks.py markdown_generator/talks.tsv _talks/          # Generate talk .md files (optional output dir)
python3 scripts/make-og-image.py        # Regenerate images/og-image.png (needs Pillow)
```

There are no tests or linters; "verification" means a clean `jekyll build` and checking the page locally. `_config.yml` is **not** reloaded by `jekyll serve` — restart the server after changing it.

## Architecture

- **`_config.yml`** is the central control point: site identity (`url`, `repository`, `title`), the sidebar author profile (`author:` — blank fields hide their icon), `site_theme` (default/air/sunrise/mint/dirt/contrast, each with light+dark variants in `_sass/theme/`), `publication_category` (groups publications on `/publications/` by each file's `category:` front matter), collections, and per-collection `defaults` (layout, author_profile, etc.).
- **Collections** — `_publications`, `_talks`, `_teaching`, `_portfolio` — plus `_posts` (blog). Each item is a Markdown file whose front matter drives rendering (e.g. publications use `venue`, `citation`, `paperurl`, `slidesurl`, `bibtexurl`, `category`; talks use `type`, `venue`, `location`). Filenames follow `YYYY-MM-DD-slug.md`. Copy an existing sample file's front matter when adding new items.
- **`_pages/`** holds top-level pages (`about.md` is the homepage at `/`, `cv.md`, and archive pages like `publications.html`/`talks.html` that loop over collections). Header navigation order is set in `_data/navigation.yml`, separately from the pages themselves.
- **`_layouts/` + `_includes/`** are the theme templates (Liquid). `_includes/author-profile.html` renders the sidebar from `site.author`; `_includes/seo.html` handles meta/OG tags (falls back to `images/og-image.png`).
- **Static files**: `files/` (PDFs etc., served at `/files/...`) and `images/` (avatar referenced by `author.avatar`).
- **JS**: `assets/js/main.min.js` is a committed build artifact concatenated by `npm run uglify` from jQuery + `assets/js/_main.js` + plugins + `theme.js`; the sources are excluded from the Jekyll build, so edits to them have no effect until rebuilt.
- **Talk map**: `talkmap.ipynb` / `talkmap.py` geocode `location:` from `_talks` into `talkmap/`; the `scrape_talks.yml` workflow runs this and auto-commits on pushes touching `_talks/`. The link is shown only if `talkmap_link: true`.

## Deployment

Pushing to `master` triggers `.github/workflows/jekyll.yml`, which builds with Ruby 3.1 and deploys to GitHub Pages (repo Settings → Pages → Source must be "GitHub Actions"). `bad-pr.yml` / `jekyll-build.yml` are upstream-template PR checks and target `main`, so they don't run here.
