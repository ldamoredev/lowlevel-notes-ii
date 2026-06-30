---
title: Relational Layer & Query Engine
description: The spine project, second half — tables and indexes over the B-Tree, a minimal SQL subset, a planner/executor, concurrent transactions.
tags: [database, sql, query-engine, transactions, spine]
order: 1
updated: 2026-06-30
---

# Relational Layer & Query Engine

The second half of the spine project, built directly on [KV Store & Durability](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/kv-store-and-durability/index.html) — see the [v0 → v3 roadmap](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/index.html) on the home page. This is where the atlas converges: manual memory management and the toolchain from Atlas I, concurrency from [Concurrency in Practice](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/concurrency-in-practice/index.html), durability from the KV store, and parsing technique from [Regex Engine from Scratch](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/regex-engine-from-scratch/index.html) all land in one project.

## Milestones (v2 → v3)

**v2 — the relational layer.** Tables and secondary indexes as B-Trees keyed by row ID and by indexed column, built entirely on the KV store's primitives — no new storage engine.

**v3 — SQL and transactions.** A parser for a useful subset of SQL (`SELECT`, `INSERT`, `WHERE`, simple indexes), a minimal planner/executor, and concurrent transactions via MVCC or copy-on-write — load-tested, not just demoed.

## Planned notes

- Mapping tables onto the KV store: row encoding and primary-key B-Trees
- Secondary indexes: a second B-Tree mapping column value → row ID
- A minimal SQL grammar: what subset is worth parsing
- Lexing and parsing SQL with the same technique as the regex-engine branch
- An AST for `SELECT … WHERE …` and a simple query planner
- Index selection: when the planner uses an index vs a full scan
- A row-at-a-time executor (the simplest correct design)
- Transactions: what "ACID" actually requires from this engine
- Copy-on-write transactions vs MVCC — picking one and justifying it
- Concurrent readers and writers: what can run in parallel safely
- Write-write conflict detection and resolution
- Benchmarking query throughput under concurrent load, with `concurrency-in-practice`'s tooling

## Core sources

- "Build Your Own Database From Scratch" (build-your-own.org) — carries the pedagogical thread from the KV-store branch into the relational layer.
- *Database Internals* (Alex Petrov) — query execution and transaction chapters.
- *Designing Data-Intensive Applications* (Kleppmann), ch. 3 and the transactions chapters.
- "Architecture of SQLite" (sqlite.org/arch.html) — VDBE/bytecode executor as a real-world reference.
- cstack's `db_tutorial` — SQL front-end over a B-Tree, the same shape as this branch.

**Connects to:** [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] · [[lowlevel-ii/regex-engine-from-scratch/index|Regex Engine from Scratch]] · [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]]
