# Site Structure & Editing Guide

This document explains the structure of this Jekyll academic website and where to make manual edits.

---

## Quick Reference: What to Edit

| What you want to change | File to edit |
|---|---|
| Name, bio, email, social links | `_config.yml` (author section) |
| Site title & description | `_config.yml` (top section) |
| Profile picture | Replace `images/profile.png` |
| Homepage greeting & content | `_pages/about.md` and `_layouts/homepage.html` |
| Homepage tarot cards (projects & music) | `_layouts/homepage.html` |
| CV / Resume | `_pages/cv.md` |
| Publications list | `_pages/publications.html` |
| Library (books & podcasts) | `_pages/reading.html` |
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
│   └── navigation.yml       # Top navigation bar links
├── _pages/                  # Top-level pages
│   ├── about.md             # Homepage (permalink: /)
│   ├── projects.html        # Projects archive page (permalink: /projects/)
│   ├── music.html           # Music page (permalink: /music/)
│   ├── reading.html         # Library page (permalink: /library/, redirects from /reading/)
│   ├── publications.html    # Publications page
│   ├── cv.md                # CV page
│   └── 404.md               # 404 error page
├── _portfolio/              # Project collection pages
│   ├── histopath-dl.md      # Deep Learning for Histopathology project
│   └── multimodal-cancer.md # Multi-modal Cancer Analysis project
├── _layouts/                # HTML page templates
│   ├── homepage.html        # Homepage layout (hero + tarot side cards)
│   ├── single.html          # Single page layout (used by library, projects)
│   ├── archive.html         # Archive layout (used by publications, CV, projects, music)
│   └── default.html         # Base layout wrapping all pages
├── _includes/               # Reusable HTML partials
├── _sass/                   # SCSS stylesheets
│   ├── _homepage.scss       # Homepage hero, tarot cards, project/music archive styles
│   ├── _reading.scss        # Library page card & rating styles
│   ├── _page.scss           # Single page layout styles
│   ├── _archive.scss        # Archive layout styles
│   ├── _sidebar.scss        # Sidebar/author profile styles
│   ├── _variables.scss      # Colors, fonts, breakpoints
│   └── ...
├── assets/                  # CSS, JS, fonts
├── images/                  # Site images (profile photo, icons, etc.)
├── files/                   # Downloadable static files (PDFs, slides)
├── markdown_generator/      # Scripts to generate content from TSV data
└── .github/workflows/       # GitHub Actions CI/CD config
```

---

## Detailed Editing Guide

### 1. Personal Information (`_config.yml`)

The author section controls the homepage hero and metadata:

```yaml
author:
  avatar:    "profile.png"
  name:      "Yingrui Ma (Ryan)"
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

### 2. Profile Picture (`images/profile.png`)

Replace this file with your own photo. Keep the filename `profile.png` or update the `author.avatar` value in `_config.yml`.

### 3. Homepage (`_pages/about.md` + `_layouts/homepage.html`)

- **Permalink:** `/` (this is the landing page)
- **Layout:** `homepage` — displays a hero section with your avatar, name, bio, and social icons
- The big greeting ("Hey there, I'm ...") is generated from `author.name` in `_config.yml`. To change the greeting text itself, edit `_layouts/homepage.html`
- Edit the markdown body in `about.md` to change the introductory text below the hero

#### Homepage Tarot Cards

The homepage features tarot-style cards that peek from the sides of the main content column. On desktop (≥1100px), cards are partially tucked behind the center column and slide out on hover. On mobile, they stack below the content.

There are two card types, each with a distinct color scheme:
- **Project cards** (warm parchment, gold border) — link to portfolio pages
- **Music card** (violet/rose, purple border) — links to the music page

Cards are defined directly in `_layouts/homepage.html`. Each card uses CSS classes to control its side and vertical position:
- Side: `tarot-card--left` or `tarot-card--right`
- Position: `tarot-card--pos-top`, `tarot-card--pos-mid`, or `tarot-card--pos-bottom`
- Type: `tarot-card--project` or `tarot-card--music`

To add a new card, add an `<a class="tarot-card ...">` block in `homepage.html`. Styles are in `_sass/_homepage.scss`.

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

### 6. Publications (`_pages/publications.html`)

- **Permalink:** `/publications/`
- Papers are listed directly in HTML as an ordered list, in reverse chronological order
- Each entry includes: title, authors (your name bolded), venue, year, and DOI link
- To add a new paper, add a new `<li>` entry in the appropriate position

### 7. Library (`_pages/reading.html`)

- **Permalink:** `/library/` (redirects from `/reading/`)
- **Layout:** `single` with body class `page--reading` (enables emoji background)
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

### 8. CV Page (`_pages/cv.md`)

- **Permalink:** `/cv/`
- Contains: Education, Research Experience, Research Interests, Skills
- All content is hand-written markdown — update directly

### 9. Navigation Bar (`_data/navigation.yml`)

Controls which links appear in the top menu bar:

```yaml
main:
  - title: "Projects"
    url: /projects/
  - title: "Music"
    url: /music/
  - title: "Library"
    url: /library/
  - title: "Publications"
    url: /publications/
  - title: "CV"
    url: /cv/
```

To add a new page: add an entry here and create a corresponding file in `_pages/`.

### 10. Downloadable Files (`files/`)

Place any PDFs, slides, or documents here. They'll be accessible at `/files/filename.pdf`.

---

## Layout Notes

- Pages with `author_profile: false` (Library, Publications, CV, Projects, Music, Portfolio) display content centered without the sidebar
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
