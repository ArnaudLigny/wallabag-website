# wallabag.org

[![Netlify Status](https://api.netlify.com/api/v1/badges/627b4b15-3230-4d88-9829-919b4e93e846/deploy-status)](https://app.netlify.com/sites/wallabag-website/deploys)
[![CI](https://github.com/wallabag/website/actions/workflows/ci.yml/badge.svg)](https://github.com/wallabag/website/actions/workflows/ci.yml)

This is the official website of wallabag.  
It's powered by [Cecil](https://cecil.app) and hosted on Netlify.

## Run it locally

Requirements: PHP 8.3+ with the `fileinfo`, `gd` and `mbstring` extensions.

```bash
# download Cecil
curl -LO https://cecil.app/cecil.phar

# preview the website on http://localhost:8000, with live reload
php cecil.phar serve

# build the website in _site/
php cecil.phar build
```

## Structure

| Path                | Content                                                                        |
|---------------------|--------------------------------------------------------------------------------|
| `cecil.yml`         | Configuration, including the latest release (version, blog post and checksum)  |
| `pages/`            | Pages, in Markdown                                                             |
| `pages/news/`       | News posts: one `<slug>/index.md` per post, published at `/news/<slug>/`       |
| `assets/news/`      | Images of the news posts, used with `![alt](/news/<slug>/image.png)`           |
| `assets/`           | Stylesheets, scripts and images used by templates (minified, fingerprinted)    |
| `static/`           | Files copied as is (fonts, images used by the stylesheets, favicon)            |
| `data/`             | Data files (`readers.json`: RSS readers compatible with wallabag)              |
| `layouts/`          | Twig templates                                                                 |

## Publish a release

1. Add the blog post in `pages/news/<date>-new-release-wallabag-<version>/index.md`.
2. Update `release` in `cecil.yml` (`version`, `blogpost` and `checksum`).

The version displayed in the download section and used by the `/latest-v2` redirects
is fetched from the GitHub API when the website is built (`release.version` is the fallback).

## Deployment

- Netlify builds the website with the official Cecil build script (see `netlify.toml`).
- Forks can preview the website on GitHub Pages with the `pages.yml` workflow
  (enable GitHub Pages in the repository settings, with "GitHub Actions" as source).
