# Site Structure & Editing Guide

This document explains the structure of this Jekyll academic website and where to make manual edits.

---

## Quick Reference: What to Edit

| What you want to change | File to edit |
|---|---|
| Name, bio, email, social links | `_config.yml` (lines 22–47) |
| Site title & description | `_config.yml` (lines 9–12) |
| Profile picture | Replace `images/profile.png` |
| Homepage content | `_pages/about.md` |
| Detailed About page | `_pages/about-detail.md` |
| CV / Resume | `_pages/cv.md` |
| Top navigation bar | `_data/navigation.yml` |
| Publications list | Create files in `_publications/` |
| Talks list | Create files in `_talks/` |
| Teaching entries | Create files in `_teaching/` |
| Portfolio items | Create files in `_portfolio/` |
| Blog posts | Create files in `_posts/` |
| Downloadable PDFs | Add files to `files/` |

---

## Directory Structure

```
.
├── _config.yml              # MAIN config — personal info, site settings
├── _data/
│   └── navigation.yml       # Top navigation bar links
├── _pages/                  # Top-level pages (about, cv, publications, etc.)
├── _publications/           # Publication markdown files (currently empty)
├── _talks/                  # Talk/presentation markdown files (currently empty)
├── _teaching/               # Teaching entry markdown files (currently empty)
├── _portfolio/              # Portfolio item markdown files (currently empty)
├── _posts/                  # Blog post markdown files (currently empty)
├── _drafts/                 # Draft posts (not published)
├── _layouts/                # HTML page templates (rarely need editing)
├── _includes/               # Reusable HTML partials (rarely need editing)
├── _sass/                   # SCSS stylesheets (edit for visual customization)
├── assets/                  # CSS, JS, fonts
├── images/                  # Site images (profile photo, icons, etc.)
├── files/                   # Downloadable static files (PDFs, slides)
├── markdown_generator/      # Scripts to generate content from TSV data
└── .github/workflows/       # GitHub Actions CI/CD config
```

---

## Detailed Editing Guide

### 1. Personal Information (`_config.yml`)

This is the **single most important file**. The author section (around lines 22–47) controls everything shown in the sidebar profile:

```yaml
author:
  avatar:    "profile.png"        # Your photo filename in images/
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

**To add more social links**, simply uncomment or add lines. Supported platforms include: ORCID, ResearchGate, arXiv, Twitter/X, Mastodon, Bluesky, YouTube, Medium, Kaggle, Stack Overflow, and many more. See `_includes/author-profile.html` for the full list.

**Important:** Changes to `_config.yml` require restarting the Jekyll server — live reload won't pick them up.

### 2. Profile Picture (`images/profile.png`)

Replace this file with your own photo. Keep the filename `profile.png` or update the `author.avatar` value in `_config.yml` to match your new filename.

Other images in `images/` are mostly template examples (alignment demos, placeholder bios) and can be deleted if unused.

### 3. Homepage (`_pages/about.md`)

- **Permalink:** `/` (this is the landing page)
- **Layout:** `homepage` — displays a hero section with your avatar, name, bio, and social icons
- Edit the markdown body to change the introductory text visitors see first

### 4. Detailed About Page (`_pages/about-detail.md`)

- **Permalink:** `/about-me/`
- **Linked from:** the "About" navigation item
- Contains sections for Research Interests, Education, and Publications
- Edit directly — it's plain markdown

### 5. CV Page (`_pages/cv.md`)

- **Permalink:** `/cv/`
- Contains: Education, Research Experience, Research Interests, Skills, Publications
- All content is hand-written markdown — update with your actual CV details

### 6. Navigation Bar (`_data/navigation.yml`)

Controls which links appear in the top menu bar:

```yaml
main:
  - title: "About"
    url: /about-me/
  - title: "Publications"
    url: /publications/
  - title: "CV"
    url: /cv/
```

To add a new page: add an entry here and create a corresponding file in `_pages/`.

### 7. Adding Publications

**Option A: Manual** — Create a markdown file in `_publications/`, e.g. `_publications/2024-my-paper.md`:

```markdown
---
title: "Your Paper Title"
collection: publications
category: manuscripts
permalink: /publication/2024-my-paper
date: 2024-01-15
venue: "Journal Name"
paperurl: "https://doi.org/..."
citation: "Ma, Y. et al. (2024). Your Paper Title. <i>Journal Name</i>."
---

Optional abstract or description here.
```

**Option B: Batch generate** — Edit `markdown_generator/publications.tsv` with your publication data, then run:

```bash
cd markdown_generator
python publications.py
```

This generates markdown files automatically. The TSV currently has template sample data — replace it with your actual publications.

**Upload PDFs** to `files/` and reference them via `paperurl: "/files/your-paper.pdf"`.

### 8. Adding Talks

Same pattern as publications. Create files in `_talks/` or edit `markdown_generator/talks.tsv` and run `python talks.py`.

Example front matter for `_talks/2024-my-talk.md`:

```markdown
---
title: "Talk Title"
collection: talks
type: "Conference presentation"
permalink: /talks/2024-my-talk
venue: "Conference Name"
date: 2024-06-01
location: "City, Country"
---

Description of your talk.
```

Upload slide PDFs to `files/` and link with `slides_url`.

### 9. Adding Teaching Entries

Create files in `_teaching/`, e.g. `_teaching/2024-course-name.md`:

```markdown
---
title: "Course Name"
collection: teaching
type: "Teaching Assistant"
permalink: /teaching/2024-course-name
venue: "King's College London"
date: 2024-09-01
---

Description of your teaching role.
```

### 10. Adding Portfolio Items

Create files in `_portfolio/`, e.g. `_portfolio/project-name.md`:

```markdown
---
title: "Project Name"
excerpt: "Short description"
collection: portfolio
---

Full project description with images, links, etc.
```

### 11. Downloadable Files (`files/`)

Place any PDFs, slides, or documents here. They'll be accessible at `/files/filename.pdf`.

Currently contains template placeholder PDFs (`paper1-3.pdf`, `slides1-3.pdf`) — replace or delete these.

### 12. Publication Categories

Defined in `_config.yml` (around lines 78–84):

```yaml
publication_category:
  books:
    title: "Books"
  manuscripts:
    title: "Journal Articles"
  papers:
    title: "Conference Papers"
```

Set the `category` field in each publication's front matter to group them under these headings.

---

## Template Cleanup Checklist

These template leftovers can be cleaned up:

- [ ] `_data/authors.yml` — Contains placeholder authors ("Name Name", "Name2 Name2"). Update or delete.
- [ ] `files/paper1.pdf`, `paper2.pdf`, `paper3.pdf` — Template sample PDFs. Delete when adding your own.
- [ ] `files/slides1.pdf`, `slides2.pdf`, `slides3.pdf` — Template sample slides. Delete when adding your own.
- [ ] `images/bio-photo.jpg`, `bio-photo-2.jpg` — Template bio photos. Safe to delete.
- [ ] `images/foo-bar-identity.jpg`, `images/500x300.png`, etc. — Template example images. Safe to delete.
- [ ] `_pages/markdown.md`, `_pages/non-menu-page.md`, `_pages/terms.md` — Template example/demo pages. Safe to delete.
- [ ] `markdown_generator/publications.tsv` and `talks.tsv` — Replace sample data with your actual data.

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
