---
# Full <title> tag (shows in browser tab and search results)
title: "{{ replace .File.ContentBaseName "-" " " | title }} | Faizan Nadeem"
# Short project name, used in JSON-LD structured data and breadcrumbs
name: "{{ replace .File.ContentBaseName "-" " " | title }}"
# Meta description for search engines (~150 chars)
description: ""
# Shorter variant for og:/twitter: description (optional; falls back to description)
socialDescription: ""
date: {{ .Date }}
# Position in the projects list (lower = earlier)
weight: 99
# Set true to also show this project on the homepage "Selected work" grid
featured: false
# Card text shown on the project grids
cardDescription: ""
tags:
  - Python
# --- Pick ONE of the three link styles below ---
# 1. Case study page (default): just write the case study below the front matter.
# 2. External link only: uncomment these two lines.
#caseStudy: false
#externalUrl: https://github.com/FaizanNadeem1287/...
# 3. Card with no link at all: uncomment caseStudy: false and add build:
#build:
#  render: never
#  list: local
---

Write the case study here in Markdown (or HTML).
