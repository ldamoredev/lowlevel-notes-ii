---
title: Must Know
description: The load-bearing ideas of this atlas, and where each one lives.
tags: [orientation, fundamentals]
order: 2
updated: 2026-06-30
---

# Must Know

A handful of ideas that hold the rest of this atlas up.

## The ideas

- **A real system is the bar, not a toy.** Every branch produces something that builds, runs, and does what production code does — at smaller scale, not lower rigor.
- **Concurrency is a property of the project, not a chapter.** It gets harder exactly where the server and the database engine make it hard, not in the abstract.
- **Durability means you tested the crash, not that you wrote `fsync()`.** A database engine that has never been killed mid-write hasn't proven anything.
- **Parsing shows up everywhere.** The shell, HTTP, Git's object format, and SQL are all "turn text into a structure" — the regex-engine branch teaches the technique once, on purpose.
- **The spine project is versioned, not monolithic.** v0 → v3, same discipline as Atlas I's OS milestones — a working v0 beats an imagined v3.
- **Atlas I is a prerequisite, not a reference you skim mid-project.** If a syscall or a memory concept feels unfamiliar here, that's a sign to go back, not push through.

## Where they live

- Real-system bar and concurrency-as-a-property: [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]], threaded through [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]] and the database engine.
- Durability and crash testing: [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] and [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]].
- Parsing as a reusable skill: [[lowlevel-ii/regex-engine-from-scratch/index|Regex Engine from Scratch]], [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]], [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]].
- The versioned spine project: [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] → [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]].

See also: [[lowlevel-ii/start-here|Start Here]] · [[lowlevel-ii/index|Full Index]]
