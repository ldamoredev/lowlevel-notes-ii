---
title: Shell from Scratch
description: A minimal bash-like shell in C — parsing, fork/exec, pipes, redirection, signals, and job control.
tags: [shell, posix, systems-programming, warmup]
order: 0
updated: 2026-06-30
---

# Shell from Scratch

The first "real" program that crosses [Low-Level Atlas I](https://ldamoredev.github.io/lowlevel-notes/en/index.html)'s systems-programming theory into code you use every day. A shell is a small, sharp lens on fork/exec, process groups, signals, and file descriptors — all things Atlas I covered conceptually and this branch makes load-bearing.

Builds on Atlas I's [systems programming](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/systems-programming/index.html) and [pointers & memory](https://ldamoredev.github.io/lowlevel-notes/en/lowlevel/pointers-and-memory/index.html) branches — this note assumes you already know what a syscall is and how `fork()` works; it does not re-explain them.

## Planned notes

- The read–parse–execute loop and where a shell fits between you and the kernel
- Tokenizing a command line: quoting, escaping, and word splitting
- Building an AST for pipelines, redirections, and `&&`/`||`/`;`
- `fork()` + `exec()`: why two syscalls, not one
- Wiring pipes between processes (`pipe()`, `dup2()`)
- I/O redirection: `>`, `>>`, `<`, and file descriptor bookkeeping
- Built-ins vs external commands: `cd`, `exit`, `export`, why `cd` can't be a subprocess
- Signal handling: `SIGINT`, `SIGTSTP`, and not killing the shell itself
- Job control: foreground/background (`&`), `Ctrl-Z`, `fg`/`bg`, process groups and `setpgid`
- Environment variables and `$PATH` resolution
- A minimal `.shellrc` and command history
- Comparing against dash/bash source for what we deliberately left out

## Core sources

- "Build Your Own Shell" (codecrafters) — staged, testable milestones for this exact build.
- *Advanced Programming in the UNIX Environment* (Stevens & Rago) — process control, signals, and job-control chapters.
- *The Linux Programming Interface* (Kerrisk) — the canonical reference for every syscall this shell touches.

**Connects to:** [[lowlevel-ii/concurrency-in-practice/index|Concurrency in Practice]] · [[lowlevel-ii/craftsmanship-low-level-ii/index|Craftsmanship Low-Level II]]
