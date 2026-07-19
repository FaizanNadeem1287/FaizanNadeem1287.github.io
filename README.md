# faaaizan.space

Personal portfolio of Faizan Nadeem, built with [Hugo](https://gohugo.io/) and deployed to GitHub Pages via GitHub Actions ([.github/workflows/hugo.yml](.github/workflows/hugo.yml)).

```
hugo server        # live preview at http://localhost:1313
hugo               # production build into public/
```

---

## Adding a new project

Every project is one file in `content/projects/`. The project cards on the homepage ("Selected work") and on `/projects/` are generated automatically from these files — adding a file adds the project everywhere it belongs.

### 1. Create the file

```
hugo new projects/my-cool-project.md
```

This scaffolds `content/projects/my-cool-project.md` from [archetypes/projects.md](archetypes/projects.md). The filename becomes the URL: `https://faaaizan.space/projects/my-cool-project/`.

### 2. Fill in the front matter

```yaml
---
title: "My Cool Project — Realtime Analytics Engine | Faizan Nadeem"
name: "My Cool Project — Realtime Analytics Engine"
description: "Case study: a realtime analytics engine built with Python and FastAPI by Faizan Nadeem."
weight: 6
featured: true
cardDescription: "A realtime analytics engine that ingests 50k events/sec. Built with FastAPI, Kafka, and ClickHouse."
tags:
  - Python
  - FastAPI
  - Kafka
---
```

| Field | Required | What it does |
|---|---|---|
| `title` | yes | Full `<title>` tag — shows in the browser tab, search results, and og:/twitter: cards. Convention: `Project Name | Faizan Nadeem`. |
| `name` | yes | Short project name. Used in JSON-LD structured data and the breadcrumb trail. |
| `description` | yes | Meta description for search engines (~150 chars). |
| `cardDescription` | yes | The paragraph shown on the project card. |
| `tags` | yes | The small tag pills on the card. |
| `weight` | yes | Position in the `/projects/` list — lower numbers appear first. |
| `featured` | no | `true` puts the project on the homepage "Selected work" grid too. Default `false`. |
| `cardTitle` | no | Card heading, only if it should differ from `name`. |
| `socialDescription` | no | Shorter description for og:/twitter: tags. Falls back to `description`. |
| `jsonldDescription` | no | Description for JSON-LD structured data. Falls back to `description`. |
| `highlightNames` | no | List of identifier names the case-study code-block highlighter should color (only relevant if the page has `code-panel` blocks). |

### 3. Write the case study

Everything below the front matter is the case-study page body. Markdown works:

```markdown
## Overview

The client needed X, so I built Y...
```

Raw HTML also works if you want the full designed layout — see the three existing case studies (they are `.html` content files using classes from `styles/project.css` such as `proj-header`, `overview-section`, `tech-grid`, `timeline-section`, `outcomes-section`).

### The three kinds of project cards

**A. Full case study (default)** — just write the body as above. The card links to the generated page with "Case Study →".

**B. External link only** (like Adaptive Media Streaming) — no page is generated; the card says "View project →" and links out:

```yaml
caseStudy: false
externalUrl: https://github.com/FaizanNadeem1287/my-cool-project
build:
  render: never
  list: local
```

**C. Card with no link at all** (like Video Automation) — same as B but without `externalUrl`:

```yaml
caseStudy: false
build:
  render: never
  list: local
```

For B and C, leave the body empty. `build.render: never` also keeps the entry out of `sitemap.xml`.

### 4. Preview and publish

```
hugo server
```

Check http://localhost:1313/ (homepage grid, if `featured: true`), http://localhost:1313/projects/ (list), and the project page itself. Then commit and push — merging to `main` triggers the deploy workflow.

---

## Repo layout

| Path | Purpose |
|---|---|
| `content/projects/` | One file per project (see above) |
| `layouts/` | Templates — `home.html`, `projects/section.html` (list), `projects/page.html` (case study) |
| `layouts/_partials/` | Shared pieces: `head.html` (all meta/SEO tags), `jsonld.html` (structured data), `nav.html`, `footer.html`, `project-card.html`, `ga.html`, social icons |
| `static/` | Served as-is: fonts, favicons, CSS, `CNAME`, `robots.txt`, `llm.txt` |
| `archetypes/projects.md` | Template used by `hugo new projects/...` |
| `hugo.toml` | Site config: base URL, contact/social links, GA ID, sitemap defaults |

SEO (canonical URLs, Open Graph, Twitter cards, JSON-LD, sitemap) is generated from front matter by the templates — there is nothing to hand-edit per page.

Note: the three original case studies pin their old `.html` URLs with a `url:` field in front matter to preserve SEO. New projects should **not** set `url:` — they get clean directory URLs automatically.
