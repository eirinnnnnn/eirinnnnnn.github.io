# eirin.github.io
# 📁 Repository layout

```
<your-username>.github.io/
├─ _config.yml
├─ index.md
├─ notes.md
├─ _includes/
│  └─ head-custom.html
├─ _data/
│  └─ hackmd.yml  # optional: list of your HackMD notes
├─ assets/
│  └─ css/
│     └─ custom.css
└─ README.md
```

---

# _config.yml
```yaml
title: "Eirin — Notes & Projects"
description: "Communication engineering, information theory, and math notes."
# Use a supported Jekyll theme via remote_theme (works on GitHub Pages)
remote_theme: just-the-docs/just-the-docs
# If you prefer a built-in theme, comment the line above and use one of:
# theme: minima

url: "https://<your-username>.github.io"
baseurl: ""

# Just the Docs options
just_the_docs:
  logo: 
  search_enabled: true
  nav_external_links:
    - title: HackMD Workspace
      url: https://hackmd.io/@<your-hackmd-handle>
      hide_icon: false

# Markdown + Math
markdown: kramdown
kramdown:
  input: GFM
  math_engine: mathjax
  hard_wrap: false

plugins:
  - jekyll-feed
  - jekyll-seo-tag

# Collections (optional)
collections:
  posts:
    output: true

# Build settings
exclude:
  - Gemfile
  - Gemfile.lock
  - node_modules
```

---

# index.md
```markdown
---
layout: default
title: Home
nav_order: 1
---

# Eirin — Research & Notes

Welcome! I write about communication engineering, information theory, and math.

- 📚 **Notes**: see [Notes](./notes)
- 🧪 **Projects**: coming soon
- 🧮 Supports inline math like $I(X;Y) = H(X) - H(X\mid Y)$.

> This site is powered by GitHub Pages + Jekyll (Just the Docs).
```

---

# notes.md
```markdown
---
layout: default
title: Notes
nav_order: 2
---

# Notes

A curated list of my HackMD documents and local posts.

## HackMD (external)

- **Soft decoding (KV) quick notes** — <https://hackmd.io/@<your-hackmd-handle>/<note-id-1>>
- **Guruswami–Sudan (GS) scratchpad** — <https://hackmd.io/@<your-hackmd-handle>/<note-id-2>>
- **Detection & Estimation cheatsheet** — <https://hackmd.io/@<your-hackmd-handle>/<note-id-3>>

> Tip: keep titles stable in HackMD; they auto-update nicely here.

## Local posts (optional)

- [Example local note](./posts/example-local-note)
```

---

# _includes/head-custom.html
```html
<!-- Extra head content: MathJax (for Just the Docs) -->
<script>
  window.MathJax = { tex: { inlineMath: [['$','$'], ['\\(','\\)']] } };
</script>
<script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<link rel="stylesheet" href="/assets/css/custom.css">
```

---

# assets/css/custom.css
```css
/* Minor polish */
:root { --brand-color: #0ea5e9; }
.site-title, .site-button { color: var(--brand-color); }
```

---

# _data/hackmd.yml (optional)
```yaml
- title: Soft decoding (KV) quick notes
  url: https://hackmd.io/@<your-hackmd-handle>/<note-id-1>
- title: Guruswami–Sudan (GS) scratchpad
  url: https://hackmd.io/@<your-hackmd-handle>/<note-id-2>
- title: Detection & Estimation cheatsheet
  url: https://hackmd.io/@<your-hackmd-handle>/<note-id-3>
```

> If you keep this YAML updated, you can auto-generate the list in `notes.md` later.

---

# README.md
```markdown
# Eirin — GitHub Pages + HackMD

This repository hosts my personal site: <https://<your-username>.github.io>.

## Quick start
1. Create a repo named `<your-username>.github.io`.
2. Copy these files into the repo and commit.
3. In **Settings → Pages**, set **Build and deployment** to `GitHub Actions` or `Deploy from a branch` (root on `main`).
4. Wait for Pages to publish, then visit your URL.

### Add a note link
Edit `notes.md` and append your HackMD URL(s). Make sure each HackMD doc is **published** or **shared** publicly, or the link will be inaccessible.

### Math
MathJax is configured via `_includes/head-custom.html`.

### Custom domain (optional)
Add a `CNAME` file containing `your.domain`, and point your DNS (A or CNAME) to GitHub Pages as documented.

### Local development (optional)
If you want to run locally: install Ruby + Bundler, then
```bash
bundle add jekyll just-the-docs jekyll-seo-tag jekyll-feed
bundle exec jekyll serve
```
Open <http://127.0.0.1:4000>.
