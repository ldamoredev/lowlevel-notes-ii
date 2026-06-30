# Low-Level Atlas II

Part 2 of the Low-Level Atlas series: real systems built from scratch in C.

This is the practical continuation of [Low-Level Atlas](https://github.com/ldamoredev/lowlevel-notes) — same author, same framework-free static-site architecture, a "Blueprint & Graphite" visual identity (sibling of Atlas I's "Copper & Graphite"). Atlas I built the mental model of the machine, top to bottom, ending in a small OS. This atlas assumes that's done and builds real, everyday systems on top of it: a shell, a malloc, a regex engine, a Git clone, an HTTP server, and a database engine with a B-Tree, a WAL, and a SQL layer.

## Structure

```
content/en/lowlevel-ii/<branch>/   # canonical English notes
content/es/lowlevel-ii/<branch>/   # Spanish overlay (same relative paths; missing files fall back to EN)
static/                            # CSS, icons, search.js — copied verbatim into site/
scripts/                           # rasterize-brand-assets.sh — SVG → PNG icon generation
build.py                           # the entire build, Python stdlib only
```

## Build

Requires **Python 3.12+** (build.py uses a PEP 701 f-string). The `markdown` package is used if installed; otherwise a built-in fallback renderer is used (CI always installs `markdown`+`pygments`).

```sh
python3 build.py
```

Refuses to wipe `site/` if zero notes are found.

## Serve Locally

```sh
python3 -m http.server 8021 --directory site
```

## Add a Note

```markdown
---
title: Note Title
description: One sentence, used for SEO and search.
tags: [tag-a, tag-b]
order: 4
updated: 2026-06-30
---

# Note Title

Mental-model-first paragraph. Then mechanism, a runnable example, pitfalls.

**Connects to:** [[lowlevel-ii/other-branch/index|Label]]

## Sources

- **Author — *Title*** — one line on relevance. url
```

## Add a Branch

1. Add an entry to `BRANCHES` in `build.py` (label, group, summary, accent, icon).
2. Add a matching entry to `BRANCHES_ES`.
3. Create `content/en/lowlevel-ii/<branch>/index.md`.
4. Optionally create `content/es/lowlevel-ii/<branch>/index.md`.
5. Rebuild.

## Add a Translation

Spanish is an overlay, not a parallel tree: create a file at the identical relative path under `content/es/`. Missing overlays render the English source with a "translation pending" banner — never a broken page. See [GLOSSARY.md](GLOSSARY.md) for register and terminology rules before translating.

## SEO and Deployment

`build.py` emits canonical URLs, hreflang alternates, full OpenGraph/Twitter meta, PWA icons, JSON-LD, `sitemap.xml`, `robots.txt`, and `.nojekyll` — all SEO surface area is generated, none hand-written. `SITE_URL`/`GITHUB_URL` are overridable via env vars (CI sets `SITE_URL` from `actions/configure-pages`). Run `scripts/rasterize-brand-assets.sh` after editing `static/favicon.svg` or `static/assets/og-image.svg`.

## Content

Nine branches across six phases — three short warm-up builds, then data, networking, and concurrency-in-practice, converging on a two-branch database engine built in milestones (v0 → v3), with a testing/craftsmanship branch active throughout. Full taxonomy, per-branch outlines, and progress tracking: [CONTENT-PLAN.md](CONTENT-PLAN.md).
