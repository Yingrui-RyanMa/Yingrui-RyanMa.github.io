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
| CV / Resume | `_pages/cv.md` |
| Publications list | `_pages/publications.html` |
| Reading list | `_pages/reading.html` |
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
│   ├── reading.html         # Reading list page
│   ├── publications.html    # Publications page
│   ├── cv.md                # CV page
│   └── 404.md               # 404 error page
├── _layouts/                # HTML page templates
│   ├── homepage.html        # Homepage layout (hero with photo, greeting, social links)
│   ├── single.html          # Single page layout (used by reading)
│   ├── archive.html         # Archive layout (used by publications, CV)
│   └── default.html         # Base layout wrapping all pages
├── _includes/               # Reusable HTML partials
├── _sass/                   # SCSS stylesheets
│   ├── _reading.scss        # Reading page card styles
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

### 3. Homepage (`_pages/about.md`)

- **Permalink:** `/` (this is the landing page)
- **Layout:** `homepage` — displays a hero section with your avatar, name, bio, and social icons
- The big greeting ("Hey there, I'm ...") is generated from `author.name` in `_config.yml`. To change the greeting text itself, edit `_layouts/homepage.html` line 20
- Edit the markdown body in `about.md` to change the introductory text below the hero

### 4. Publications (`_pages/publications.html`)

- **Permalink:** `/publications/`
- Papers are listed directly in HTML as an ordered list, in reverse chronological order
- Each entry includes: title, authors (your name bolded), venue, year, and DOI link
- To add a new paper, add a new `<li>` entry in the appropriate position

### 5. Reading Page (`_pages/reading.html`)

- **Permalink:** `/reading/`
- **Layout:** `single` with body class `page--reading` (enables emoji background)
- Books are displayed as cards in a grid, organized into sections ("Reading - Books", "Done - Books")
- To add a book: add a new `<a class="reading-card">` block inside the appropriate `.reading-grid`

### 6. CV Page (`_pages/cv.md`)

- **Permalink:** `/cv/`
- Contains: Education, Research Experience, Research Interests, Skills
- All content is hand-written markdown — update directly

### 7. Navigation Bar (`_data/navigation.yml`)

Controls which links appear in the top menu bar:

```yaml
main:
  - title: "Reading"
    url: /reading/
  - title: "Publications"
    url: /publications/
  - title: "CV"
    url: /cv/
```

To add a new page: add an entry here and create a corresponding file in `_pages/`.

### 8. Downloadable Files (`files/`)

Place any PDFs, slides, or documents here. They'll be accessible at `/files/filename.pdf`.

---

## Layout Notes

- Pages with `author_profile: false` (Reading, Publications, CV) display content centered without the sidebar
- The centered layout is handled via CSS `#main > &:first-child` rules in `_page.scss` and `_archive.scss`
- The homepage uses its own `homepage` layout with a hero section

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
