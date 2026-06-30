---
title: Craftsmanship Low-Level II
description: Testing protocol parsers and concurrent code, fuzzing binary formats, property-based testing, and TDD when state lives on disk.
tags: [testing, tdd, fuzzing, craftsmanship, always-active]
order: 0
updated: 2026-06-30
---

# Craftsmanship Low-Level II

The direct continuation of Atlas I's [Craftsmanship Low-Level](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/craftsmanship-low-level/index.html) — always active across every branch, the same way the original was. Where Atlas I applied TDD, fuzzing, and contracts to memory-unsafe C in general, this branch applies the same discipline to *stateful, concurrent systems*: protocol parsers, the database engine, and code where the bug only shows up under load or after a crash.

## Planned notes

- Testing a protocol parser: feeding the HTTP parser malformed input as a first-class test case
- Testing Git's object format parser: corrupted objects, truncated files, wrong hashes
- Race conditions in practice: writing a test that reliably reproduces one
- ThreadSanitizer (TSan) in the build: what it catches that review doesn't
- Fuzzing binary formats: the B-Tree page format and the WAL format with libFuzzer/AFL++
- Fuzzing the HTTP parser against the spec's edge cases
- Property-based testing for the database engine: invariants that must hold after any sequence of operations
- TDD when state lives on disk, not memory: structuring tests around a throwaway data directory
- Crash-recovery testing: killing the process mid-write and asserting on recovery
- Contracts and asserts for the B-Tree's structural invariants
- Code review checklist for memory-unsafe, concurrent C

## Core sources

- *Test-Driven Development for Embedded C* (Grenning) — TDD discipline for systems code, already the spine of Atlas I's craftsmanship branch.
- libFuzzer and AFL++ documentation — fuzzing binary formats and parsers, reused from Atlas I.
- "Property-Based Testing with PropEr, Erlang, and Elixir" — referenced only for the *technique* of property-based testing, not the language.
- ThreadSanitizer documentation — practical TSan usage on real concurrent C code.

**Connects to:** [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]] · [[lowlevel-ii/mini-git/index|Mini Git]] · [[lowlevel-ii/kv-store-and-durability/index|KV Store & Durability]]
