---
title: Reference Registry
description: Books, specs, tools, and the build-your-own-X hubs this atlas draws from.
tags: [reference, registry, sources]
order: 3
updated: 2026-06-30
---

# Reference Registry

External references normalized in one place instead of repeated across every branch index.

## Books (canonical)

- *Database Internals* — Alex Petrov. Storage engines, B-Trees, WAL, and transactions — the conceptual spine of the database-engine branches.
- *Designing Data-Intensive Applications* — Martin Kleppmann. Storage and retrieval, replication, and transactions, ch. 3 especially.
- *Advanced Programming in the UNIX Environment* — Stevens & Rago. Process control, signals, and job control for the shell branch.
- *The Linux Programming Interface* — Michael Kerrisk. The canonical syscall reference, used throughout.
- *Test-Driven Development for Embedded C* — James Grenning. TDD discipline for systems code, carried over from Atlas I.
- *The Art of Multiprocessor Programming* — Herlihy & Shavit. Lock-free data structures, for concurrency-in-practice.

## Specifications & references

- RFC 7230 / RFC 7231 — HTTP/1.1, the normative spec behind the HTTP server.
- SQLite file format spec and "Architecture of SQLite" (sqlite.org/arch.html) — a real-world reference implementation for the database engine.
- `man epoll`, `man kqueue` — read past the tutorials.

## Tools & hubs

- codecrafters.io — "Build Your Own Redis/Git/SQLite/HTTP-Server/Shell" — staged, testable milestones for most of these branches.
- build-your-own.org — the Go database-in-a-book that this atlas's database-engine progression mirrors (in spirit; this atlas is C-first).
- swtch.com/~rsc/regexp/ — Russ Cox's regex-engine series, the spine of the regex-engine branch.
- `wrk` / `hey` — HTTP load-testing tools used for every benchmark in concurrency-in-practice.
- libFuzzer / AFL++ — binary-format and parser fuzzing, carried over from Atlas I's craftsmanship branch.

See also: [[lowlevel-ii/index|Full Index]]
