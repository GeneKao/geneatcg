# GENEATCG — Personal Website Source

Source code for [geneatcg.com](https://www.geneatcg.com), the personal portfolio and blog of Gene Ting-Chun Kao.

Built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme with a custom homepage layout.

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

Manual build:

```sh
hugo --minify
cp CNAME public/
```

## Project structure

| Path | Description |
|---|---|
| `content/` | Site content in `.md` files — `blog/`, `portfolio/`, `publications/`, `resume/`, `talks/` |
| `data/` | Structured YAML for resume (timeline), publications (cards), talks (cards) |
| `layouts/` | Custom templates: `index.html` (homepage), section layouts, partials |
| `assets/css/extended/custom.css` | All custom styles and theme overrides |
| `themes/PaperMod/` | Git submodule — do not edit directly |
| `static/` | Static assets: images, favicon |
| `.github/workflows/deploy.yml` | CI/CD pipeline |

## Adding a new blog post

```sh
hugo new content/blog/my-post-title/index.md
```

Place images in the same directory as `index.md` and reference them relatively.
