# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio and blog site for Gene Ting-Chun Kao (www.geneatcg.com), built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme with a custom homepage layout.

## Common Commands

```sh
# First-time setup
git submodule update --init   # pulls PaperMod theme
brew install hugo             # macOS

# Local dev server — always use this to preview, never open public/ directly
hugo server --port 1313
# Access at http://localhost:1313

# Manual build (CI does this automatically on push to main)
hugo --minify
cp CNAME public/
```

**Deployment is automatic** — push to `main` and GitHub Actions builds and deploys to `genekao.github.io`.

## Architecture

```
content/          Hugo content (.md files, page bundles)
  blog/<slug>/    Each post is a directory with index.md + images alongside
  archives.md     Year/month archive page (layout: "archives")
  publications/   Single page driven by data/publications.yaml
  resume/         Single page driven by data/resume.yaml
  talks/          Single page driven by data/talks.yaml
data/             Structured YAML — resume timeline, publication cards, talk cards
layouts/          Custom templates overriding PaperMod defaults
  index.html      Full custom homepage (cover, overview, highlights, recent posts, about)
  partials/
    comments.html   giscus comment system (theme-aware, synced via localStorage)
    cover.html      Custom override supporting external URL cover images
  publications/   Card layout rendered from data/publications.yaml
  talks/          Card layout rendered from data/talks.yaml
  resume/         Timeline layout rendered from data/resume.yaml
assets/css/extended/custom.css   All color, spacing, and component overrides
themes/PaperMod/  Git submodule — do not edit directly
static/
  images/
    talks/        Talk card images (referenced from data/talks.yaml)
    publications/ Publication card images (referenced from data/publications.yaml)
  favicon.ico / favicon-16x16.png / favicon-32x32.png / apple-touch-icon.png
.github/workflows/deploy.yml   CI/CD pipeline
```

## Content Format

Blog posts use Hugo front matter:
```markdown
---
title: "Post Title"
date: 2024-01-15
tags: ["tag1", "tag2"]
description: "Short summary shown in listings"
cover:
  image: "cover-image.jpg"
  alt: "Description"
  relative: true
  hiddenInSingle: true   # hides cover on single page; use inline image instead
---

Post body in Markdown here.
```

Images placed in the same directory as `index.md` can be referenced relatively (`![alt](image.jpg)`).

**Cover image pattern for posts with a GitHub repo:** use `hiddenInSingle: true` in front matter and add a clickable inline image at the top of the body:
```markdown
[![Repo name](repo-github.png)](https://github.com/GeneKao/repo-name)
```

To download a GitHub repo's OG preview image:
```sh
# 1. Get the OG image URL
curl -s https://github.com/GeneKao/repo-name | grep -o 'property="og:image" content="[^"]*"'
# 2. Download it (needs Mozilla UA and a few seconds between requests to avoid rate limiting)
sleep 5 && curl -sL -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36" \
  "<og-image-url>" -o content/blog/<slug>/repo-github.png
```

To add a new post:
```sh
hugo new content/blog/my-post-title/index.md
```

**Image compression:** Always compress images before adding to posts. Large images are the main mobile performance bottleneck. Use `sips` on macOS:
```sh
# Convert and compress PNG to JPG (adjust width and quality as needed)
sips --resampleWidth 1600 image.png --out image.jpg -s format jpeg -s formatOptions 75
```
Keep the original in the repo but add it to `ignoreFiles` in `hugo.toml` so it isn't deployed.

**Math posts:** Add `math: true` to front matter to enable KaTeX rendering. Use `$$...$$` for display math and `$...$` for inline. Wide equations scroll horizontally on mobile automatically.

**Geometry Toolbox series:** Tag posts with `geometry-toolbox` to group them as a series.

## Structured Data (resume, publications, talks)

- `data/resume.yaml` — experience and education entries; supports `url` field for hyperlinked org names
- `data/publications.yaml` — grouped by year, rendered as image cards
- `data/talks.yaml` — grouped by year, rendered as image cards; supports `url` field linking to blog post or external

Editing these YAML files updates the respective pages automatically.

## Theme & Customization

- Accent color: dark slate `#334155` (hover: `#1e293b`)
- Content width: `760px` globally (set via `--main-width` in custom.css)
- Homepage uses full-bleed cover photo via negative margin trick (`100vw`)
- All custom styles in `assets/css/extended/custom.css` — PaperMod picks this up automatically
- Syntax highlighting: github (light) + github-dark (dark) Chroma themes defined in `custom.css`
- `layouts/partials/cover.html` is a custom override that supports external URLs in `cover.image`

## Comments

giscus is set up via `layouts/partials/comments.html`, backed by GitHub Discussions on `GeneKao/geneatcg` (must remain public). The script is injected dynamically so the initial theme is read from `localStorage` (matching the site's light/dark toggle) rather than hardcoded.

## Google Analytics

Configured in `hugo.toml` via `googleAnalytics = 'G-QM94B0JX4Q'`. Only injected in production builds (not `hugo server`).

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml` which runs `hugo --minify`, copies `CNAME`, and force-pushes to `genekao.github.io`. The `DEPLOY_TOKEN` secret in the repo settings must have write access to `GeneKao/genekao.github.io`.
