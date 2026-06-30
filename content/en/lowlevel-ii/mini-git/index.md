---
title: Mini Git
description: A minimal Git — content-addressed object store, SHA hashing, the commit graph, a working .git of your own.
tags: [git, content-addressed-storage, hashing, serialization]
order: 0
updated: 2026-06-30
---

# Mini Git

Data structures and binary serialization, with a result you'll actually use: a working `.git` implementation that can hash, store, and version real files. The core idea — content-addressed storage — reappears later as the conceptual root of the [B-Tree pages](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/kv-store-and-durability/index.html) in the database engine, just keyed by offset instead of hash.

## Planned notes

- The object model: blobs, trees, and commits as a content-addressed graph
- Hashing objects: SHA-1 (Git's legacy default) and the SHA-256 migration
- The blob: how Git stores file contents, zlib-compressed, keyed by hash
- The tree object: directories as ordered lists of (mode, name, hash)
- The commit object: parent pointers, author/committer, message — and how history becomes a DAG
- Writing objects to `.git/objects/<aa>/<bb...>` and reading them back
- A minimal `init`, `hash-object`, and `cat-file`
- Building a tree from the working directory (`write-tree`)
- Creating commits and walking parent pointers (`log`)
- Branches and refs: just files containing a hash, and why that's enough
- The index/staging area: what `add` actually does before `commit`
- Diffing two trees — the first real algorithmic piece of the project

## Core sources

- "Write yourself a Git" (wyag) — the most complete from-scratch walkthrough of the object model.
- "Build Your Own Git" (codecrafters) — staged milestones with test coverage.
- *Pro Git* (Chacon & Straub), "Git Internals" chapter — free, canonical, and short.

**Connects to:** [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] · [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]]
