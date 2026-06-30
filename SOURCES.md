# SOURCES.md — curated reference sources for Low-Level Atlas II

Cite these in each branch's `index.md` under "Core sources", and in individual notes under `## Sources`. Prefer primary sources (specs, canonical books, the original author's own writeup) over secondary blog posts.

## Cross-cutting / general

- codecrafters.io — "Build Your Own Redis/Git/SQLite/HTTP-Server/Shell." Staged, testable milestones; the structural backbone for most branches in this atlas.
- build-your-own.org — the Go database-in-a-book. Pedagogical progression for the database engine; this atlas is C-first, the book is Go, but the milestone shape transfers directly.
- [Low-Level Atlas I](https://github.com/ldamoredev/lowlevel-notes) — the prerequisite atlas; its own SOURCES.md covers the machine model, C, assembly, and toolchain sources this atlas assumes.

## shell-from-scratch

- "Build Your Own Shell" (codecrafters) — staged milestones for this exact build.
- *Advanced Programming in the UNIX Environment* — Stevens & Rago. Process control, signals, job control.
- *The Linux Programming Interface* — Michael Kerrisk. The syscall reference for everything this shell touches.

## malloc-from-scratch

- *Computer Systems: A Programmer's Perspective* — Bryant & O'Hallaron. The dynamic memory allocation chapter.
- Doug Lea's malloc design notes — the design that shaped glibc's allocator.
- "Understanding and Using C Pointers" — Richard Reese.

## regex-engine-from-scratch

- Russ Cox, "Regular Expression Matching Can Be Simple And Fast" (swtch.com/~rsc/regexp/) — the spine of this entire branch.
- Russ Cox, "Regular Expression Matching: the Virtual Machine Approach" — for the capture-group extension.
- *Compilers: Principles, Techniques, and Tools* — Aho, Lam, Sethi, Ullman. NFA/DFA construction.

## mini-git

- "Write yourself a Git" (wyag) — the most complete from-scratch walkthrough of the object model.
- "Build Your Own Git" (codecrafters) — staged milestones with test coverage.
- *Pro Git* — Chacon & Straub, "Git Internals" chapter (free).

## http-server-from-scratch

- "Beej's Guide to Network Programming" (free) — the backbone of the sockets material.
- RFC 7230 / RFC 7231 — the HTTP/1.1 spec.
- "Build Your Own HTTP Server" (codecrafters).
- `man epoll`, `man kqueue`.
- Dan Kegel, "The C10K Problem" — the classic argument for event loops over thread-per-connection.

## concurrency-in-practice

- *C++ Concurrency in Action* — Anthony Williams.
- Preshing on Programming (preshing.com) — memory ordering and lock-free patterns.
- Herlihy & Shavit, *The Art of Multiprocessor Programming* — lock-free data structure design.
- Dan Kegel, "The C10K Problem" — shared with http-server-from-scratch.
- `wrk` / `hey` documentation — load-testing tools used throughout this branch.

## kv-store-and-durability

- "Build Your Own Database From Scratch" (build-your-own.org) — pedagogical spine for both database-engine branches.
- *Database Internals* — Alex Petrov. B-Tree storage engines and WAL design.
- *Designing Data-Intensive Applications* — Martin Kleppmann, ch. 3.
- "Architecture of SQLite" (sqlite.org/arch.html) and the SQLite file format spec.
- cstack's `db_tutorial` — a from-scratch SQLite clone in C.

## relational-layer-and-query-engine

- "Build Your Own Database From Scratch" (build-your-own.org) — continues from kv-store-and-durability.
- *Database Internals* — Alex Petrov. Query execution and transactions.
- *Designing Data-Intensive Applications* — Martin Kleppmann, transactions chapters.
- "Architecture of SQLite" (sqlite.org/arch.html) — the VDBE/bytecode executor as a real-world reference.
- cstack's `db_tutorial`.

## craftsmanship-low-level-ii

- *Test-Driven Development for Embedded C* — James Grenning. Carried over from Atlas I's craftsmanship branch.
- libFuzzer / AFL++ documentation — fuzzing binary formats and parsers, carried over from Atlas I.
- "Property-Based Testing with PropEr, Erlang, and Elixir" — referenced only for the *technique*, not the language.
- ThreadSanitizer (TSan) documentation.
