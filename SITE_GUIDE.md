# Site Structure & Editing Guide

This document explains the structure of this Jekyll academic website and where to make manual edits.

---

## Quick Reference: What to Edit

| What you want to change | File to edit |
|---|---|
| Name, bio, email, social links | `_config.yml` (author section) |
| Site title & description | `_config.yml` (top section) |
| Profile picture | Replace `images/profile.jpg` |
| Homepage greeting & content | `_pages/about.md` and `_layouts/homepage.html` |
| CV timeline on the homepage | `_data/cv.yml` |
| Colours, fonts, dark theme | `_sass/_theme.scss` |
| Publications list | `_pages/publications.html` |
| Library (books & podcasts) | `_pages/reading.html` |
| Writing page (dream stories) | `_pages/writing.html` |
| Individual stories | `_writing/*.md` |
| Projects page | `_pages/projects.html` |
| Individual project pages | `_portfolio/*.md` |
| Music page | `_pages/music.html` |
| Top navigation bar | `_data/navigation.yml` |
| Downloadable PDFs | Add files to `files/` |

---

## Directory Structure

```
.
├── _config.yml              # MAIN config — personal info, site settings
├── _data/
│   ├── navigation.yml       # Top navigation bar links
│   └── cv.yml               # CV timeline shown on the homepage
├── _pages/                  # Top-level pages
│   ├── about.md             # Homepage (permalink: /)
│   ├── projects.html        # Projects archive page (permalink: /projects/)
│   ├── music.html           # Music page (permalink: /music/)
│   ├── reading.html         # Library page (permalink: /library/, redirects from /reading/)
│   ├── writing.html         # Writing page (permalink: /writing/)
│   ├── publications.html    # Publications page
│   ├── cv.md                # Redirect only: /cv/ -> homepage
│   ├── resume.md            # Redirect only: /resume -> homepage
│   └── 404.md               # 404 error page
├── _portfolio/              # Project collection pages
│   ├── histopath-dl.md      # Deep Learning for Histopathology project
│   └── multimodal-cancer.md # Multi-modal Cancer Analysis project
├── _writing/                # Writing collection (dream stories)
│   └── a-dream-story.md     # "The Greatest" — first dream story
├── _layouts/                # HTML page templates
│   ├── homepage.html        # Homepage layout (hero + tarot side cards)
│   ├── writing.html         # Writing story layout (bionic reading toggle)
│   ├── single.html          # Single page layout (used by library, portfolio pages)
│   ├── archive.html         # Archive layout (publications, projects, music, writing)
│   └── default.html         # Base layout wrapping all pages
├── _includes/               # Reusable HTML partials
├── _sass/                   # SCSS stylesheets
│   ├── _theme.scss          # Colour tokens for both themes
│   ├── _homepage.scss       # Homepage hero, project/music/writing archive styles
│   ├── _cv.scss             # Homepage CV timeline
│   ├── _reading.scss        # Library page card & rating styles
│   ├── _page.scss           # Single page layout styles
│   ├── _archive.scss        # Archive layout styles
│   ├── _sidebar.scss        # Sidebar/author profile styles
│   ├── _variables.scss      # Colors, fonts, breakpoints
│   └── ...
├── assets/                  # CSS, JS, fonts
├── images/                  # Site images (profile photo, icons, etc.)
├── files/                   # Downloadable static files (PDFs, slides)
└── .github/workflows/       # GitHub Actions CI/CD config
```

---

## Detailed Editing Guide

### 1. Personal Information (`_config.yml`)

The author section controls the homepage hero and metadata:

```yaml
author:
  avatar:    "profile.jpg"
  name:      "Yingrui Ma"
  pronouns:  "he/his"
  bio:       "PhD Student in AI..."
  location:  "London, UK"
  employer:  "King's College London"
  email:     "ryanma0427@gmail.com"
  googlescholar: "https://scholar.google.com/citations?user=..."
  github:    "ryan-yingrui-ma"
  linkedin:  "yingruima"
```

**Important:** Changes to `_config.yml` require restarting the Jekyll server — live reload won't pick them up.

### 2. Profile Picture (`images/profile.jpg`)

Replace this file with your own photo. Keep the filename `profile.jpg` or update the `author.avatar` value in `_config.yml`.

### 3. Homepage (`_pages/about.md` + `_layouts/homepage.html`)

- **Permalink:** `/` (this is the landing page)
- **Layout:** `homepage` — displays a hero section with your avatar, name, bio, and social icons
- The big greeting ("Hey there, I'm ...") is generated from `author.name` in `_config.yml`. To change the greeting text itself, edit `_layouts/homepage.html`
- Edit the markdown body in `about.md` to change the introductory text below the hero

#### CV timeline

Below the introduction the homepage shows your career as a two-track timeline:
study runs down the left of a central spine, work down the right, so the years
where the two overlap are visible at a glance. It is deliberately static — no
scroll animation — and folds to a single column on narrow screens.

The entries come from **`_data/cv.yml`**, not from markup. To add a role:

```yaml
timeline:
  - period: "2024 — Present"   # years only, no months
    kind: education            # "education" (left lane) or "research" (right lane)
    role: "PhD, Cancer &amp; Pharmaceutical Sciences"
    place: "King's College London"
    current: true              # optional; adds the halo on the marker
```

Each entry shows just those three lines — years, role, place. Entries render in
file order, so keep them newest first. The same file holds the `interests` and
`skills` lists shown underneath. Styles are in `_sass/_cv.scss`.

### 4. Projects (`_pages/projects.html` + `_portfolio/`)

- **Archive page permalink:** `/projects/`
- Lists all items from the `_portfolio/` collection in a grid
- To add a new project: create a markdown file in `_portfolio/` with front matter:

```yaml
---
title: "Project Title"
excerpt: "Short description for the archive card."
collection: portfolio
permalink: /portfolio/your-project-slug/
author_profile: false
---
```

- Portfolio pages have `author_profile: false` (no sidebar) set in `_config.yml` defaults

### 5. Music (`_pages/music.html`)

- **Permalink:** `/music/`
- Displays favourite artists in a grid with violet-themed cards
- Each artist card includes a vinyl icon, name, genre, and a short note
- Edit `_pages/music.html` directly to add or remove artists

### 6. Writing (`_pages/writing.html` + `_writing/`)

- **Archive page permalink:** `/writing/`
- **Body class:** `page--writing` (puts 🌙😴 in the header band and justifies the text)
- Lists all items from the `_writing/` collection in a card grid
- Individual story pages use the `writing` layout (`_layouts/writing.html`), which includes an **ADHD-friendly bionic reading toggle** in the top-right corner. When enabled, the first half of each word is bolded to aid focus.
- To add a new story: create a markdown file in `_writing/` with front matter:

```yaml
---
title: "Story Title"
excerpt: "Short description for the archive card."
collection: writing
permalink: /writing/your-story-slug/
author_profile: false
---
```

- The `writing` layout, `body_class`, and `author_profile: false` are set automatically via `_config.yml` defaults for the `writing` collection

### 7. Publications (`_pages/publications.html`)

- **Permalink:** `/publications/`
- Papers are listed directly in HTML as an ordered list, in reverse chronological order
- Each entry includes: title, authors (your name bolded), venue, year, and DOI link
- To add a new paper, add a new `<li>` entry in the appropriate position

### 8. Library (`_pages/reading.html`)

- **Permalink:** `/library/` (redirects from `/reading/`)
- **Layout:** `single` with body class `page--reading` (puts 📚📖 in the header band)
- Items are displayed as cards in a grid, organized into sections:
  - **Reading - Books** — currently reading
  - **Done - Books** — finished books
  - **Listening - Podcasts** — currently listening
  - **Done - Podcasts** — finished podcasts

#### Adding a book or podcast

Add a new `<a class="reading-card">` block inside the appropriate `.reading-grid`:

```html
<a class="reading-card" href="LINK_URL" target="_blank" rel="noopener">
  <div class="reading-card__cover">
    <img src="COVER_IMAGE_URL" alt="Title">
  </div>
  <div class="reading-card__info">
    <div class="reading-card__title">Title</div>
    <div class="reading-card__author">Author</div>
    <div class="reading-card__rating">
      <span class="star star--filled">&#9733;</span>
      <span class="star star--filled">&#9733;</span>
      <span class="star star--filled">&#9733;</span>
      <span class="star star--empty">&#9733;</span>
      <span class="star star--empty">&#9733;</span>
    </div>
  </div>
</a>
```

#### Star ratings

Each item has a 5-star rating using Unicode star characters (`★`) with CSS classes:
- `star--filled` — gold star (`#e8a92e`)
- `star--half` — half-gold, half-grey (CSS clip overlay)
- `star--empty` — grey star (`#ddd`)

Example for 3.5 stars: 3× `star--filled`, 1× `star--half`, 1× `star--empty`.

### 9. CV (`_data/cv.yml`)

The standalone CV page was removed — the content now lives on the homepage as
the two-track timeline described above. Edit `_data/cv.yml`.

`_pages/cv.md` and `_pages/resume.md` survive as redirect stubs only, so the
old `/cv/` and `/resume` URLs still land somewhere useful instead of 404ing.
Both are excluded from the sitemap.

### 10. Navigation Bar (`_data/navigation.yml`)

Controls which links appear in the top menu bar:

```yaml
main:
  - title: "Projects"
    url: /projects/
  - title: "Music"
    url: /music/
  - title: "Writing"
    url: /writing/
  - title: "Library"
    url: /library/
  - title: "Publications"
    url: /publications/
```

To add a new page: add an entry here and create a corresponding file in `_pages/`.

### 11. Downloadable Files (`files/`)

Place any PDFs, slides, or documents here. They'll be accessible at `/files/filename.pdf`.

---

### 12. Colours and the dark theme (`_sass/_theme.scss`)

The palette is drawn from H&E staining: haematoxylin violet `#5b4b8a` and
eosin rose `#c9587b` on a slide-white ground. Every colour is a CSS custom
property in `_sass/_theme.scss`, and the Sass variables in `_variables.scss`
point at those — so changing a colour there changes it site-wide, in both
themes.

**Light is the default for everyone.** The operating system preference is
deliberately not consulted; dark is opt-in via the toggle in the header. The
choice is kept in the reader's browser and applied before the page paints, so
it never flashes the wrong theme.

To retune a colour, edit the matching pair in `:root` (light) and the
`theme-dark` mixin (dark). Keep both in step or one theme will drift.

### 13. The header emoji band

The emoji sit in a strip behind the navigation rather than tiling the page.
Each area of the site carries its own set — science site-wide, 🌙😴 on the
writing pages, 📚📖 in the library — so the band says which room you are in.
They are defined in `_sass/_masthead.scss` as SVG data URIs.

Emoji built from a zero-width joiner (👨‍🔬, 👨‍💻) are percent-encoded there
rather than pasted in literally: the joiner is invisible and does not reliably
survive an edit, and without it the emoji renders as two separate glyphs.

---

## Gotcha: inline scripts

**Never use `//` comments inside an inline `<script>` in this repo. Use `/* */`.**

The `compress.html` layout strips newlines, so a `//` comment swallows the rest
of the script once it is collapsed onto one line — including the closing
`})();` — and the whole block fails to parse with
`SyntaxError: Unexpected end of input`.

It only breaks in the built output, never in the source, so check a built page
rather than the file if a script mysteriously does nothing. This silently
disabled the bionic reading toggle for months.

---

## Layout Notes

- Pages with `author_profile: false` (Library, Writing, Publications, Projects, Music, Portfolio) display content centered without the sidebar
- The centered layout is handled via CSS `#main > &:first-child` rules in `_page.scss` and `_archive.scss`
- The homepage uses its own `homepage` layout with a hero section and tarot side cards
- The main content column has a thin border (`rgba(201, 185, 154, 0.35)`) that visually connects with the tarot cards

---

## Local Development

```bash
# Install dependencies
bundle install

# Serve locally with live reload at localhost:4000
bundle exec jekyll serve -l -H localhost

# Docker alternative
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

---

## Deployment

The site auto-deploys to GitHub Pages via GitHub Actions (`.github/workflows/jekyll.yml`) whenever you push to the `master` branch. No manual deployment steps needed.
