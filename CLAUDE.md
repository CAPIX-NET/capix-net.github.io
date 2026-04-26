# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

CAPIX Treasury Software company website — a Jekyll static site hosted on GitHub Pages at capix.net.

## Build & Development

```bash
bundle exec jekyll serve        # Local dev server (auto-reloads on file changes, but NOT _config.yml)
bundle exec jekyll build         # Build static site to _site/
```

No Gemfile is tracked in the repo — GitHub Pages provides the default Jekyll environment. For local development, install the `github-pages` gem.

There are no tests, linters, or CI workflows. Deployment is automatic via GitHub Pages on push to `main`.

## Architecture

- **Theme**: minima (gem-based) with local overrides in `_layouts/`, `_includes/`, and `_sass/`. Layout shells are in `_layouts/default.html`, `home.html`, `page.html`. Head/header/footer partials are in `_includes/`.
- **Content**: All pages are Markdown with YAML front matter. No blog posts collection (`_posts/`), no data files (`_data/`).
- **Styling**: All custom styling lives in `_sass/capix-custom.scss` (colors, navbar, footer, hero, cards, tables, 404 page, etc.). The entry point is `assets/main.scss`, which imports `minima` and then `capix-custom`. The legacy commented-out colour vars in `_config.yml` are inert — edit the SCSS partial instead.
- **Front matter pattern**: Content pages use `layout: page` with `title`, `subtitle`, `description` (for SEO), and `permalink`.

## Key Configuration (_config.yml)

- Navigation order is explicitly set via `header_pages` — adding a new top-level page requires updating this list.
- Colours/visuals are NOT in `_config.yml` (the variables under `# --- Colours / background image ---` are commented out and unused). Edit `_sass/capix-custom.scss` instead.
- Excerpt separator is `<!--more-->` with length of 50 words.
- Plugins: jekyll-feed, jekyll-seo-tag, jekyll-paginate, jekyll-sitemap, jekyll-github-metadata.
- `CLAUDE.md` is in the `exclude:` list and won't appear on the built site.

## Content Sections

Main sections are directories with `index.md`: `products/`, `services/`, `news/`, `about/`, `support/`, `contact/`, `ai/`.

Product-specific pages: `cct/` (Cloud Treasury), `cim/` (Investment Manager), `ctc/` (Treasury Centre), `ctm/` (Treasury Manager).

Additional: `staff/`, `values/`, `research/`, `dynamics-365/`.

## Important Notes

- **CNAME**: The `CNAME` file maps the site to `capix.net`. Do not delete it — GitHub Pages needs it for the custom domain.
- Changes to `_config.yml` require restarting `jekyll serve` (it is not auto-reloaded). SCSS and content changes are picked up automatically.
- Files listed under `exclude:` in `_config.yml` are not processed into the built site (Gemfile, README.md, LICENSE, docs/, `ausindustry/`, etc.).
- **Root-level standalone `.md` files** (`dynamics-365.md`, `copilot-modernization.md`, `Web-enabled-treasury-application-project.md`) are internal project documents without YAML front matter. They are excluded in `_config.yml` so Jekyll will not process them. Note the collision risk: `dynamics-365.md` (excluded internal doc) and `dynamics-365/index.md` (published page) share a slug.
- Use **relative links** (e.g. `/products/`) not absolute URLs (e.g. `https://capix.net/products/`) when linking between pages.
