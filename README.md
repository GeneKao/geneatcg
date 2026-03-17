# GENEATCG — Personal Website Source

Source code for [geneatcg.com](https://www.geneatcg.com), the personal portfolio and blog of Gene Ting-Chun Kao.

Built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, with a fully custom homepage, structured data pages (resume, publications, talks), comments via [giscus](https://giscus.app/), and automated deployment to GitHub Pages via GitHub Actions.

Feel free to explore the code, borrow ideas, or open an issue if you spot something broken.

## Features

- Custom homepage — cover hero, highlights grid, recent posts with thumbnails, about section
- Structured data pages — resume timeline, publication cards, talk cards — driven by YAML
- Comments via [giscus](https://giscus.app/) (GitHub Discussions), with light/dark theme sync
- Syntax highlighting with separate light and dark Chroma themes
- Cover image support for external URLs (e.g. GitHub OG preview images)
- Archives page + tag browsing
- Google Analytics (GA4)
- Automated deployment to GitHub Pages via GitHub Actions
- RSS feed + JSON search index

## Setup

```sh
git submodule update --init   # pull PaperMod theme
brew install hugo             # macOS
```

## Dev server

```sh
hugo server --port 1313
```

Access at http://localhost:1313. Always use the dev server for previewing — do not open `public/` directly.

## Deploy

Pushing to `main` triggers GitHub Actions which builds and deploys to [genekao.github.io](https://github.com/GeneKao/genekao.github.io) automatically.

## Project structure

| Path | Description |
|---|---|
| `content/blog/<slug>/` | Each post is a directory with `index.md` + images alongside |
| `content/archives.md` | Year/month archive page |
| `data/` | Structured YAML for resume (timeline), publications and talks (cards) |
| `layouts/index.html` | Fully custom homepage |
| `layouts/partials/comments.html` | giscus comment system |
| `layouts/partials/cover.html` | Cover partial override (supports external image URLs) |
| `assets/css/extended/custom.css` | All custom styles and theme overrides |
| `themes/PaperMod/` | Git submodule — do not edit directly |
| `static/` | Favicons, cover photo, publication/talk images |
| `.github/workflows/deploy.yml` | CI/CD pipeline |

## Adding a new blog post

```sh
hugo new content/blog/my-post-title/index.md
```

Place images in the same directory as `index.md` and reference them relatively.
