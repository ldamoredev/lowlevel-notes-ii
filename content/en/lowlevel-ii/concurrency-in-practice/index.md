---
title: Concurrency in Practice
description: Atlas I's concurrency theory anchored in the HTTP server and the database engine — thread pools, lock-free structures, real load benchmarking.
tags: [concurrency, performance, benchmarking, always-developing]
order: 0
updated: 2026-06-30
---

# Concurrency in Practice

The direct continuation of Atlas I's [Concurrency & Performance](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/concurrency-and-performance/index.html) branch — but applied, not isolated. Every concept here is anchored in a problem the [HTTP server](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/http-server-from-scratch/index.html) or the [database engine](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/kv-store-and-durability/index.html) actually has, measured under real load instead of in a microbenchmark.

This branch develops *in parallel* with the networked-systems and database-engine phases, not before or after them — notes get written as the projects that motivate them get built.

## Planned notes

- Thread pools: sizing, work queues, and avoiding thundering-herd wakeups
- Locks vs lock-free structures for the database engine's hot paths
- Event-loop (epoll/kqueue) vs thread-per-connection — measured, not argued
- False sharing in the connection table and the B-Tree page cache
- Cache-aware data layout for hot structures, revisited under concurrent access
- Read-write locks vs a single mutex for the KV store's B-Tree
- Memory ordering bugs that only show up under real concurrent load
- Lock contention profiling: finding the actual bottleneck, not the suspected one
- Benchmarking methodology: `wrk`/`hey`, percentiles over averages, warm-up effects
- A load test of the HTTP server at increasing connection counts, with a written postmortem
- A load test of the database engine under concurrent writers

## Core sources

- *C++ Concurrency in Action* (Williams) and Preshing's blog — already the backbone of Atlas I's concurrency branch, reused here.
- Herlihy & Shavit, *The Art of Multiprocessor Programming* — lock-free data structure design.
- Dan Kegel, "The C10K Problem" — shared spine with the HTTP server branch.
- `wrk` / `hey` documentation — the actual tools used for every benchmark in this branch.

**Connects to:** [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]] · [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] · [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]]
