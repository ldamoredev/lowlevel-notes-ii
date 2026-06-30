---
title: malloc from Scratch
description: A real malloc/free/realloc — free lists, coalescing, sbrk vs mmap, alignment, measured against glibc.
tags: [malloc, memory-allocator, warmup]
order: 0
updated: 2026-06-30
---

# malloc from Scratch

[Atlas I](https://ldamoredev.github.io/lowlevel-notes/en/index.html) explained the heap and a custom bump/arena/pool allocator conceptually in [pointers & memory](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/pointers-and-memory/custom-allocators-arena-pool-and-bump.html). This branch builds the general-purpose case those simpler allocators avoid: a `malloc`/`free`/`realloc` that has to handle arbitrary alloc/free order without leaking or corrupting itself.

## Planned notes

- The contract: what `malloc`/`free`/`realloc`/`calloc` actually promise
- Requesting memory from the OS: `sbrk` vs `mmap`, and where the line is
- A first-fit free list — the simplest allocator that works
- Block headers, footers, and the bookkeeping tax of every allocation
- Alignment requirements and why they're not optional
- Coalescing adjacent free blocks on `free()`
- Splitting blocks on allocation to fight fragmentation
- Best-fit vs first-fit vs segregated free lists — a measured comparison
- Implementing `realloc` without always copying
- Thread-safety: a global lock, then why that doesn't scale
- Benchmarking against glibc's `malloc` and `mimalloc` under real workloads
- Where this allocator breaks (and what production allocators do instead)

## Core sources

- *Computer Systems: A Programmer's Perspective* (Bryant & O'Hallaron) — the dynamic memory allocation chapter, already cited in Atlas I.
- Doug Lea's malloc design notes — the design that shaped glibc's allocator.
- "Understanding and Using C Pointers" (Reese) — pointer arithmetic discipline this build leans on hard.

**Connects to:** [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] · [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]]
