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
  publications/   Single page driven by data/publications.yaml
  resume/         Single page driven by data/resume.yaml
  talks/          Single page driven by data/talks.yaml
data/             Structured YAML — resume timeline, publication cards, talk cards
layouts/          Custom templates overriding PaperMod defaults
  index.html      Full custom homepage (cover, overview, highlights, recent posts, about)
  publications/   Card layout rendered from data/publications.yaml
  talks/          Card layout rendered from data/talks.yaml
  resume/         Timeline layout rendered from data/resume.yaml
assets/css/extended/custom.css   All color, spacing, and component overrides
themes/PaperMod/  Git submodule — do not edit directly
static/images/    Profile photos, cover image, publication/talk images
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
---

Post body in Markdown here.
```

Images placed in the same directory as `index.md` can be referenced relatively (`![alt](image.jpg)`).

To add a new post:
```sh
hugo new content/blog/my-post-title/index.md
```

## Structured Data (resume, publications, talks)

- `data/resume.yaml` — experience and education entries rendered as a timeline
- `data/publications.yaml` — grouped by year, rendered as image cards
- `data/talks.yaml` — grouped by year, rendered as image cards

Editing these YAML files updates the respective pages automatically.

## Theme & Customization

- Accent color: dark slate `#334155` (hover: `#1e293b`)
- Content width: `760px` globally (set via `--main-width` in custom.css)
- Homepage uses full-bleed cover photo via negative margin trick (`100vw`)
- All custom styles in `assets/css/extended/custom.css` — PaperMod picks this up automatically

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml` which runs `hugo --minify`, copies `CNAME`, and force-pushes to `genekao.github.io`. The `DEPLOY_TOKEN` secret in the repo settings must have write access to `GeneKao/genekao.github.io`.
