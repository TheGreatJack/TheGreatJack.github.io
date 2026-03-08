# BioFlor — Bioinformatics Blog

Personal blog built with [Quarto](https://quarto.org/) and deployed to GitHub Pages via GitHub Actions.

Live site: **https://thegreatjack.github.io/**

## Repo Structure

```
├── _quarto.yml          # Site configuration (theme, navbar, site URL)
├── custom.scss           # Theme color overrides (navbar, links, code blocks)
├── index.qmd             # Landing page
├── about.qmd             # About me page
├── blog/
│   ├── index.qmd         # Blog listing page (auto-generates from posts/)
│   └── posts/
│       └── my-post/      # Each post = a folder with its own index.qmd
│           ├── index.qmd
│           └── data/     # Optional: data, images, etc. for that post
├── images/
│   └── bioflor_logo_V1.png
├── references/           # BibTeX files and citation styles
└── .github/workflows/
    └── quarto-publish.yml  # CI/CD: renders and deploys on push to main
```

## How To

### Add a new blog post

1. Create a folder: `blog/posts/my-post-name/`
2. Add an `index.qmd` inside it with this front matter:

```yaml
---
title: "Post Title"
description: "Short description"
date: "2026-03-08"
categories: [bioinformatics, rad-seq]  # whatever tags you want
---
```

3. Write your content. The blog listing page picks it up automatically.

### Add interactive plots

Quarto renders Python/R code blocks natively. For interactive plots, use libraries like:

- **Plotly** (Python/R) — `fig.show()` in a code block just works
- **Observable JS** — use `{ojs}` code blocks directly in `.qmd`
- **htmlwidgets** (R) — DT, leaflet, plotly, etc.

Example with Plotly in Python:

````markdown
```{python}
import plotly.express as px
df = px.data.iris()
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species")
fig.show()
```
````

### Change the theme

Edit `_quarto.yml`, change the theme name:

```yaml
format:
  html:
    theme: [cosmo, custom.scss]     # replace 'sandstone' with any Bootswatch theme
```

Available themes: `cosmo`, `flatly`, `litera`, `darkly`, `journal`, `lumen`, `minty`, `pulse`, `sandstone`, `simplex`, `sketchy`, `slate`, `solar`, `spacelab`, `superhero`, `united`, `vapor`, `yeti`, `zephyr`, `cerulean`, `lux`, `materia`, `morph`, `quartz`.

For light/dark toggle:

```yaml
format:
  html:
    theme:
      light: [flatly, custom.scss]
      dark: [darkly, custom.scss]
```

Note: some themes may clash with `custom.scss` since the colors were tuned for Sandstone. If you switch themes, you may want to adjust or temporarily remove `custom.scss`.

### Local preview

Install [Quarto](https://quarto.org/docs/get-started/) if you haven't, then from the repo root:

```bash
quarto preview
```

This starts a local server (usually `http://localhost:4200`) with live reload — edits to `.qmd` files are reflected instantly in the browser. Press `Ctrl+C` to stop.

To render without previewing (just generate the HTML):

```bash
quarto render
```

### Deployment

Automatic. Push to `main` → GitHub Actions renders the site → publishes to `gh-pages` branch → GitHub Pages serves it.

### Drafts

Unfinished posts live in separate git branches (e.g., `drafts/allium-cepa`). They won't render or deploy until merged to `main`.

## Branches

- `main` — published site
- `drafts/allium-cepa` — unfinished Allium cepa RAD-seq reanalysis (with references)
