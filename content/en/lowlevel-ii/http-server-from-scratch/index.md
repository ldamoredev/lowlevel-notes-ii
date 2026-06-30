---
title: HTTP Server from Scratch
description: A real HTTP/1.1 server — raw BSD sockets, hand-written parsing, an epoll/kqueue event loop, keep-alive.
tags: [http, sockets, networking, event-loop]
order: 0
updated: 2026-06-30
---

# HTTP Server from Scratch

The entry point into networked systems: a real HTTP/1.1 server built on raw BSD sockets, with the protocol parsed by hand and an event loop driving thousands of concurrent connections. This is the project that makes you understand what Node, Fastify, or nginx are actually doing underneath the API. Shorter than the other project branches by design — it's the on-ramp to [Concurrency in Practice](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/concurrency-in-practice/index.html) and the spine project's network layer.

Builds directly on Atlas I's [systems programming](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/systems-programming/index.html) branch (syscalls, low-level I/O) — sockets are just file descriptors, and this branch assumes you already know why.

## Planned notes

- The socket API: `socket`, `bind`, `listen`, `accept` — and what each one actually does in the kernel
- A blocking, one-connection-at-a-time server (the version you outgrow on purpose)
- Parsing the HTTP request line, headers, and body by hand — no library
- Handling chunked transfer-encoding
- Why `fork`-per-connection and thread-per-connection don't scale to C10K
- The event loop: `epoll` on Linux, `kqueue` on macOS — same idea, different API
- Edge-triggered vs level-triggered epoll, and the bugs each mode invites
- Keep-alive connections and connection-state machines
- A minimal router: path matching, methods, and handlers
- Writing responses: status lines, headers, `Content-Length` vs chunked
- Backpressure: what happens when a client reads slower than you write
- Load-testing with `wrk`/`hey` and reading the latency distribution, not just the average

## Core sources

- "Beej's Guide to Network Programming" — free, the backbone of the sockets material.
- RFC 7230 / RFC 7231 — the HTTP/1.1 spec itself, for anything the guide simplifies.
- "Build Your Own HTTP Server" (codecrafters) — staged milestones with a test harness.
- `man epoll`, `man kqueue` — read the man pages, not just tutorials about them.
- Dan Kegel, "The C10K Problem" — the classic argument for event loops over thread-per-connection.

**Connects to:** [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]] · [[lowlevel-ii/regex-engine-from-scratch/index|Regex Engine from Scratch]]
