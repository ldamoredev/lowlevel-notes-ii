# AGENTS.md — Low-Level Atlas II

Read this first, then [CONTENT-PLAN.md](CONTENT-PLAN.md), then [SOURCES.md](SOURCES.md).

## What this is

A framework-free, bilingual (EN canonical / ES overlay) static site — sibling of [`lowlevel-notes`](https://github.com/ldamoredev/lowlevel-notes) (Atlas I), same `build.py` architecture, different visual identity ("Blueprint & Graphite" vs Atlas I's "Copper & Graphite"). Where Atlas I is a knowledge atlas (fundamentals, top to bottom), this is a **project atlas**: every branch is a real system built from scratch in C, assuming Atlas I is already done. The spine project is the database engine (`kv-store-and-durability` → `relational-layer-and-query-engine`), built in milestones v0 → v3, the way Atlas I's spine (`os-from-scratch`) was built bootloader to shell.

## Build, run, verify

```sh
python3 build.py
python3 -m http.server 8021 --directory site
```

The build prints `Built N localized pages from M notes into site (unresolved links: K).` — **K must be 0**. Verify with:

```sh
grep -rl 'class="unresolved-link"' site/en site/es | wc -l
```

`build.py` wipes and regenerates `site/` on every run — never hand-edit it. Sanity-check the script itself with `python3 -m py_compile build.py`. **Requires Python 3.12+** (PEP 701 f-strings are used).

## Repo layout

```
content/en/lowlevel-ii/<branch>/*.md   # canonical notes
content/es/lowlevel-ii/<branch>/*.md   # ES overlay, same relative paths, sparse is fine
content/en/lowlevel-ii/index.md        # section index (distinct from the generated home page)
content/en/lowlevel-ii/start-here.md   # entry-layer note (slug fixed: render_sidebar hardcodes it)
content/en/lowlevel-ii/must-know.md    # entry-layer note (slug fixed)
content/en/lowlevel-ii/reference-registry.md   # sources/tools registry
content/en/lowlevel-ii/phase-*.md      # one page per PHASES entry
examples/<branch>/<note-slug>/demo.c   # runnable artifact per atomic note (+ optional run.sh)
static/assets/atlas.css                # all visual identity; named --vars only, see CSS header comment
build.py                               # everything else
```

## Taxonomy

Branch config lives in `BRANCHES`/`BRANCHES_ES` in `build.py`. Phases live in `PHASES`/`PHASE_KEYS`, with `tag_<Key>`/`intent_<Key>` pairs required in `UI_STRINGS` for every phase key. `validate_taxonomy()` warns (non-fatal) on drift between `BRANCHES` and actual content folders — read its stderr output after every build. The spine project also has `SPINE_BRANCHES`/`SPINE_ROADMAP` constants powering the home page's v0→v3 panel; update both if the roadmap shape changes.

## How to write a note (match the bar)

```yaml
---
title: Note Title
description: One sentence, used for SEO + search index + auto-description.
tags: [tag-a, tag-b]
order: 4                # sort key within the branch; index.md is 0
updated: 2026-06-30
# featured: true         # at most one across the whole atlas
# draft: true            # excludes from build/search/sitemap
---
```

Body shape, in order: H1 matching the title; a mental-model-first paragraph; "how it really works" sections; a runnable artifact (the matching `examples/<branch>/<slug>/demo.c` **must build and run as written** — this is non-negotiable, same bar as Atlas I); named failure modes / pitfalls; a closing `**Connects to:** [[wikilink|Label]] · ...` line; a `## Sources` section with primary sources, one line of relevance each. Link format: prefer the path form `[[lowlevel-ii/branch/slug|Label]]` over a bare slug — it disambiguates instantly and that's one less thing to verify.

## Renderer gotcha (important)

The `markdown` package usually isn't installed locally, so the fallback renderer (`simple_markdown_to_html`) is what you're actually testing against. Write flat lists, avoid nested lists and exotic Markdown — verify what you wrote renders correctly without the optional dependency, not just with it.

## Conventions & constraints

- EN-first; ES is Rioplatense (voseo), not literal translation — see [GLOSSARY.md](GLOSSARY.md) before translating anything.
- Every branch is a **real, runnable program** — code that builds and runs, not notes about a program. This is the one hard rule that's different from Atlas I.
- Concurrency is not a phase to finish once — `concurrency-in-practice` develops in parallel with the networked-systems and database-engine phases. Don't write it as if it precedes or follows them.
- Target 8–12 rich notes per branch (CONTENT-PLAN.md tracks progress per branch).
- Build and check `(unresolved links: 0)` after every branch you write.
- Do not commit unless the user explicitly asks. Branch first if currently on `main`.
- Cross-link generously, both within this atlas (wikilinks) and out to Atlas I (full external URLs to `https://ldamoredev.github.io/lowlevel-notes/...` — never wikilinks across repos).

## Deploy

GitHub Pages via `.github/workflows/deploy.yml` (Actions-based, copied near-verbatim from Atlas I). `SITE_URL` is injected by `actions/configure-pages`; no manual config needed beyond enabling Pages → "GitHub Actions" as the source in repo settings.

## What's next

Skeleton complete: all 9 branch `index.md` files, the root entry/phase/registry notes, `build.py` fully adapted (taxonomy, copy, the spine-roadmap home section), and the "Blueprint & Graphite" CSS identity are in place and build clean. No atomic notes or `examples/` code exist yet — see CONTENT-PLAN.md's progress checklist for the suggested write order (warm-up branches first).
