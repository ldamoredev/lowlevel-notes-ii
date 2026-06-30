---
title: KV Store & Durability
description: The spine project, first half — a persistent key-value store on a copy-on-write B-Tree with fsync durability, WAL, and crash recovery.
tags: [database, b-tree, durability, wal, spine]
order: 0
updated: 2026-06-30
featured: true
---

# KV Store & Durability

The first half of this atlas's spine project — see the [v0 → v3 roadmap](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/index.html) on the home page. Where Atlas I's spine project ([OS from Scratch](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/os-from-scratch/index.html)) built a kernel from boot to shell, this one builds a database engine from a bare B-Tree to a durable, crash-safe key-value store. [Relational Layer & Query Engine](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/relational-layer-and-query-engine/index.html) builds the SQL layer on top of what gets built here.

## Milestones (v0 → v1)

**v0 — the structure.** An in-memory copy-on-write B-Tree (or B+Tree): node format, search, insert, delete, splitting and merging — no disk involved yet.

**v1 — real durability.** Persisting pages to disk, `fsync` discipline, a write-ahead log, crash recovery, and free-space management. This is the point where it becomes an actual database instead of a fancy in-memory map.

## Planned notes

- Why a B-Tree (not a hash table) for a disk-backed KV store
- B-Tree vs B+Tree: which one and why
- The on-disk page format: fixed-size pages, headers, and why page size matters
- Copy-on-write nodes: how updates avoid in-place mutation
- Search, insert, and split — building the tree node by node
- Deletion and merging underflowed nodes
- Free-space management: tracking and reusing freed pages
- `fsync`, `fdatasync`, and what "durable" actually guarantees (and doesn't)
- The write-ahead log: format, append discipline, and replay
- Crash recovery: replaying the WAL on startup, and testing it by actually killing the process mid-write
- Checkpointing: when to truncate the WAL
- Benchmarking write throughput vs durability guarantees (`fsync` every write vs batched)

## Core sources

- "Build Your Own Database From Scratch" (build-your-own.org) — the pedagogical spine for this branch and its sequel.
- *Database Internals* (Alex Petrov) — the conceptual backbone for B-Tree storage engines and WAL design.
- *Designing Data-Intensive Applications* (Kleppmann), ch. 3 — storage and retrieval fundamentals.
- "Architecture of SQLite" (sqlite.org/arch.html) and the SQLite file format spec — a real-world reference implementation.
- cstack's `db_tutorial` — a from-scratch SQLite clone in C, close to this branch's scope.

**Connects to:** [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]] · [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]] · [[lowlevel-ii/malloc-from-scratch/index|malloc from Scratch]]
