---
title: Low-Level Atlas II Index
description: Nine branches across six phases, all assuming Atlas I — the full map of this atlas.
tags: [index, map]
order: 0
updated: 2026-06-30
---

# Low-Level Atlas II Index

Nine branches across six phases, every one of them a real system built from scratch in C. This atlas assumes [Low-Level Atlas I](https://ldamoredev.github.io/lowlevel-notes/en/index.html) is already done — the machine model, C, pointers and memory, assembly, the toolchain, systems programming, concurrency basics, and a small OS. Nothing here re-explains that; everything here builds on it.

## 01 · Warm-up Builds

- [[lowlevel-ii/shell-from-scratch/index|Shell from Scratch]] — fork/exec, pipes, redirection, signals, job control.
- [[lowlevel-ii/malloc-from-scratch/index|malloc from Scratch]] — free lists, coalescing, sbrk vs mmap.
- [[lowlevel-ii/regex-engine-from-scratch/index|Regex Engine from Scratch]] — Thompson NFA, no exponential backtracking.

## 02 · Data & Serialization

- [[lowlevel-ii/mini-git/index|Mini Git]] — content-addressed object store, the commit graph, a working .git.

## 03 · Networked Systems

- [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]] — raw sockets, hand-parsed HTTP/1.1, epoll/kqueue.

## 04 · Concurrency & Performance II

- [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]] — thread pools, lock-free vs locks, real load benchmarking.

## 05 · The Database Engine

- [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]] — a B-Tree, fsync, WAL, crash recovery. v0 → v1.
- [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]] — tables, indexes, SQL, transactions. v2 → v3.

## ★ · Always Active

- [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]] — testing parsers, concurrency bugs, fuzzing, TDD on disk-backed state.

## Reference

- [[lowlevel-ii/reference-registry|Reference Registry]] — sources, tools, and the codecrafters/build-your-own-X hubs this atlas draws from.
