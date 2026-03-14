# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio and blog site for Gene Ting-Chun Kao (www.geneatcg.com), built with [Lektor](https://www.getlektor.com/) (Python static site generator) and the [lektor-icon](https://github.com/spyder-ide/lektor-icon) theme.

## Common Commands

```sh
# Install dependencies (first time setup)
python3 -m venv .venv
.venv/bin/pip install lektor lektor-google-analytics lektor-atom

# Initialize theme submodule (first time setup)
git submodule update --init

# Run local dev server (port 5000 is taken by macOS, use 8000)
.venv/bin/lektor server --port 8000
# Access at http://127.0.0.1:8000
```

**Deployment is automatic** — push to `main` and GitHub Actions builds and deploys to `genekao.github.io`. No manual deploy step needed.

For a manual build locally:
```sh
.venv/bin/lektor build --output-path ../genekao.github.io --no-prune
cp CNAME ../genekao.github.io/
```

## Architecture

Content, theme, and configuration are strictly separated:

- **`content/`** — All site content in `.lr` files (Lektor's YAML-like format with `---` separators). Each subdirectory is a page/collection. Key sections: `blog/`, `publications/`, `talks/`, `resume/`.
- **`themes/lektor-icon/`** — Git submodule for the theme (Jinja2 templates + assets). Avoid editing directly; customize via project settings or `assets/`.
- **`assets/`** — Files here are overlaid on top of the theme output. Used for `favicon.ico` and `static/css/custom-styles.css`.
- **`geneatcg.lektorproject`** — Project config: theme, plugins, deployment server, and all `[theme_settings]` (title, colors, nav links, footer).
- **`configs/google-analytics.ini`** — Plugin config for `lektor-google-analytics`.
- **`configs/atom.ini`** — Plugin config for `lektor-atom` (generates RSS feed at `/blog/feed.xml`).
- **`.github/workflows/deploy.yml`** — CI/CD pipeline: builds and deploys on every push to `main`.

## Content Format (`.lr` files)

```
title: My Blog Post
---
pub_date: 2024-01-15
---
author: Gene Ting-Chun Kao
---
body:

Markdown content here.
```

Fields are separated by `---`. The available fields depend on the data model defined in the theme.

## Theme & Customization

- Theme accent/pipe color: `#cd0067`
- Custom CSS: `assets/static/css/custom-styles.css`
- Theme settings live in `[theme_settings]` block of `geneatcg.lektorproject`
- The theme is a git submodule — run `git submodule update --init` after cloning

## Deployment

Pushing to `main` automatically triggers `.github/workflows/deploy.yml`, which builds and force-pushes to `genekao.github.io`. The `CNAME` file is copied automatically by the workflow to preserve the custom domain `www.geneatcg.com`. The `--no-prune` flag is required so the generated `feed.xml` is not deleted during build.
