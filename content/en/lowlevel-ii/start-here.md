---
title: Start Here
description: The build order for this atlas, and what you need from Atlas I before starting.
tags: [orientation, path]
order: 1
updated: 2026-06-30
---

# Start Here

This atlas is read as a build queue, not a course catalog. Each branch is a real program; you finish one before the next one needs it.

## Before you start

Do [Low-Level Atlas I](https://ldamoredev.github.io/lowlevel-notes/en/index.html) first, completely — at minimum its [machine model](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/machine-model/index.html), [C from the metal](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/c-from-the-metal/index.html), [pointers & memory](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/pointers-and-memory/index.html), and [systems programming](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/systems-programming/index.html) branches. Nothing here re-teaches what a syscall, a stack frame, or `fork()` is.

## The build queue

1. **Warm up.** [[lowlevel-ii/shell-from-scratch/index|Shell from Scratch]], [[lowlevel-ii/malloc-from-scratch/index|malloc from Scratch]], and [[lowlevel-ii/regex-engine-from-scratch/index|Regex Engine from Scratch]] — short, self-contained, one to two weeks each. Pick any order.
2. **Build something with state.** [[lowlevel-ii/mini-git/index|Mini Git]] — content-addressed storage, a result you'll actually keep using.
3. **Talk to the network.** [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]] — the shortest of the project branches, the on-ramp to everything that follows.
4. **Make it concurrent.** Start [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]] alongside the HTTP server — don't wait until it's "done."
5. **Build the spine.** [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] (v0 → v1), then [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]] (v2 → v3) — the project that consumes everything else.
6. **Never stop testing it.** [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]] runs alongside every branch above, not after them.

## How to read it

- Every branch is a real, runnable program — not a set of notes about a program. The deliverable is code that builds and runs, same bar as Atlas I's examples.
- Concurrency is not a separate phase you do once. It's threaded through the network and database phases on purpose.
- The database engine is versioned (v0 → v3) the same way Atlas I's OS was built in milestones — read the roadmap on the home page before diving in.

See also: [[lowlevel-ii/must-know|Must Know]] · [[lowlevel-ii/index|Full Index]]
