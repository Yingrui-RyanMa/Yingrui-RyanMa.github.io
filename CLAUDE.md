# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Yingrui Ma (Ryan), deployed to GitHub Pages at
https://yingrui-ryanma.github.io/. Originally derived from the
[Academic Pages](https://academicpages.github.io/) template (a fork of the Minimal
Mistakes Jekyll theme), but the unused template machinery has been removed — see
"What is intentionally absent" below before adding anything back.

## Development Commands

```bash
# Install Ruby dependencies
bundle install

# Serve locally with live reload (available at localhost:4000)
bundle exec jekyll serve -l -H localhost

# Docker alternative
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

**Note:** `_config.yml` changes require a server restart — they are not picked up by live reload.

## Architecture

- **`_config.yml`** — Site metadata, author profile/social links, collection definitions, plugin list. Primary file for site-wide changes.
- **`_data/navigation.yml`** — Top navigation bar: Projects, Music, Writing, Library, Publications.
- **`_data/cv.yml`** — The CV, rendered as the two-track timeline on the homepage. There is no `/cv/` page; `_pages/cv.md` and `resume.md` are redirect stubs.
- **`_data/ui-text.yml`** — Theme i18n strings, read via `site.data.ui-text[site.locale]`.
- **`_pages/`** — Top-level pages. `about.md` (permalink `/`) is the homepage.
- **`_portfolio/`**, **`_writing/`** — The only two Jekyll collections. `_portfolio` is listed by `_pages/projects.html`; `_writing` by `_pages/writing.html`.
- **`_layouts/`** — `homepage`, `archive`, `single`, `writing`, all extending `default.html` → `compress.html`.
- **`_includes/`** — Reusable partials (head, masthead, footer, sidebar, author profile, SEO, social share).
- **`_sass/`** — SCSS, compiled by Jekyll via `assets/css/main.scss`. Site-specific styles live in `_homepage.scss`, `_cv.scss` and `_reading.scss`. `_theme.scss` holds the colour tokens for both themes; the Sass variables in `_variables.scss` point at them, so the rest of the stylesheet inherits light and dark for free. Light is the default and the OS preference is deliberately ignored — dark is opt-in via the header toggle.
- **`files/`** — Static files served at `/files/filename`.
- **`images/`** — Site images including the author avatar (`profile.jpg`, set by `author.avatar`).

`SITE_GUIDE.md` is the human-facing editing guide and covers each page in detail.

## What is intentionally absent

The following template features were removed because this site does not use them.
Do not reintroduce them incidentally:

- Collections: `_posts`, `_publications`, `_talks`, `_teaching`. Publications are hand-written HTML in `_pages/publications.html`.
- Comments (Disqus/Discourse/Facebook/staticman) and analytics providers.
- Pagination, category/tag archives, related posts, talk map, `markdown_generator/`.
- Layouts `talk`, `splash`, `archive-taxonomy`.

## Gotchas

- **Inline `<script>` blocks must use `/* */`, never `//`.** `compress.html`
  strips newlines, so a line comment swallows the rest of the script — closing
  `})();` included — and it fails to parse. This only breaks in the built
  output, so verify against a built page, not the source.
- Sass colour functions (`mix`, `rgba`, `darken`) cannot operate on a `var()`.
  Anything that needs them takes a literal colour; see `_notices.scss`.

## Content Workflow

- **New project:** add a markdown file to `_portfolio/` with `collection: portfolio` and a `permalink`.
- **New story:** add a markdown file to `_writing/` with `collection: writing` and a `permalink`.
- **New publication:** add an `<li>` to `_pages/publications.html`.
- **New nav item:** edit `_data/navigation.yml` and create the target page in `_pages/`.
- **New CV entry:** add to `_data/cv.yml`, newest first.
