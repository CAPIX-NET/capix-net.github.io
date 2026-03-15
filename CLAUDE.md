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

- **Theme**: minima (not overridden locally — no `_layouts/`, `_includes/`, or `_sass/` directories). All layout customization is via `_config.yml` settings.
- **Content**: All pages are Markdown with YAML front matter. No blog posts collection (`_posts/`), no data files (`_data/`).
- **Styling**: Theme colors/images are configured in `_config.yml` (navbar, footer, page background). A legacy `assets/CAPIX.css` exists but is not the primary styling mechanism.

## Key Configuration (_config.yml)

- Navigation order is explicitly set via `header_pages` — adding a new top-level page requires updating this list.
- `_config.yml` has duplicate color/image sections at the bottom that override earlier values (lines ~206-227 override ~160-177). The **last values win**.
- Excerpt separator is `<!--more-->` with length of 50 words.
- Plugins: jekyll-feed, jekyll-seo-tag, jekyll-paginate, jekyll-sitemap, jekyll-github-metadata.

## Content Sections

Main sections are directories with `index.md`: `products/`, `services/`, `news/`, `about/`, `support/`, `contact/`, `ai/`.

Product-specific pages: `cct/` (Cloud Treasury), `cim/` (Investment Manager), `ctc/` (Treasury Centre), `ctm/` (Treasury Manager).

Additional: `staff/`, `values/`, `research/`.

## Important Notes

- The CNAME file (mapping to capix.net) is currently deleted in the working tree — this must exist for the custom domain to work on GitHub Pages.
- Changes to `_config.yml` require restarting `jekyll serve` (it is not auto-reloaded).
- Files listed under `exclude:` in `_config.yml` are not processed into the built site (Gemfile, README.md, LICENSE, docs/, etc.).
