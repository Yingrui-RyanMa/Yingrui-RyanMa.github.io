# Yingrui-RyanMa.github.io

Personal website for **Yingrui Ma (Ryan)** — PhD student in AI for cancer and
pharmaceutical science at King's College London.

Live at <https://yingrui-ryanma.github.io/>.

Built with Jekyll. Originally derived from the
[Academic Pages](https://academicpages.github.io/) template (a fork of Minimal
Mistakes), since stripped down to just the parts this site uses.

## Local development

```bash
bundle install
bundle exec jekyll serve -l -H localhost   # http://localhost:4000
```

`_config.yml` is not picked up by live reload — restart the server after editing it.

Docker alternative:

```bash
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

## Where things live

| | |
|---|---|
| Site + author config | `_config.yml` |
| Top navigation | `_data/navigation.yml` |
| Pages (`/`, `/cv/`, `/library/`, …) | `_pages/` |
| Project write-ups | `_portfolio/` |
| Dream stories | `_writing/` |
| Page templates | `_layouts/` |
| Reusable partials | `_includes/` |
| Styles | `_sass/`, `assets/css/main.scss` |
| Downloadable files (`/files/…`) | `files/` |

See [SITE_GUIDE.md](SITE_GUIDE.md) for a detailed editing guide.

## Deployment

Pushing to `master` triggers `.github/workflows/jekyll.yml`, which builds the
site and deploys it to GitHub Pages.

## License

The underlying theme is MIT licensed (see [LICENSE](LICENSE)). Site content is
© Yingrui Ma.
