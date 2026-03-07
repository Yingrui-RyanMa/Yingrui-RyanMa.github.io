# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Yingrui Ma (Ryan), built with the [Academic Pages](https://academicpages.github.io/) template — a fork of the Minimal Mistakes Jekyll theme. Deployed to GitHub Pages at https://yingrui-ryanma.github.io/.

## Development Commands

```bash
# Install Ruby dependencies
bundle install

# Serve locally with live reload (available at localhost:4000)
jekyll serve -l -H localhost
bundle exec jekyll serve -l -H localhost

# Docker alternative
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site

# Rebuild minified JS (rarely needed)
npm run build:js
```

**Note:** `_config.yml` changes require a server restart — they are not picked up by live reload.

## Architecture

- **`_config.yml`** — Central configuration: site metadata, author profile/social links, collection definitions, plugin list. This is the primary file for site-wide changes.
- **`_data/navigation.yml`** — Controls the top navigation bar links. Currently shows Publications and CV.
- **`_pages/`** — Top-level site pages. `about.md` (permalink `/`) is the homepage.
- **`_publications/`**, **`_talks/`**, **`_teaching/`**, **`_portfolio/`**, **`_posts/`** — Jekyll collections for content. Each collection has a corresponding archive page in `_pages/` and is configured in `_config.yml` under `collections` and `defaults`.
- **`_layouts/`** — Page templates (`single.html`, `talk.html`, `archive.html`, etc.) extending `default.html` → `compress.html`.
- **`_includes/`** — Reusable HTML partials (author profile sidebar, head, footer, etc.). `author-profile.html` renders the sidebar from `_config.yml` author settings.
- **`_sass/`** — SCSS stylesheets, compiled automatically by Jekyll.
- **`files/`** — Static files (PDFs, etc.) served at `/files/filename`.
- **`images/`** — Site images including author avatar (`profile.png`).
- **`markdown_generator/`** — Python/Jupyter scripts to generate publication and talk markdown files from TSV data.

## Content Workflow

To add a publication, talk, or teaching entry: create a markdown file in the corresponding `_collection/` directory with appropriate front matter (see existing examples or use `markdown_generator/`).

To add a new navigation item: edit `_data/navigation.yml` and create the target page in `_pages/`.
