---
title: Regex Engine from Scratch
description: A minimal Thompson-NFA regex engine — pattern to state machine, no exponential backtracking.
tags: [regex, automata, parsing, warmup]
order: 0
updated: 2026-06-30
---

# Regex Engine from Scratch

A small, self-contained project at the intersection of parsing and automata theory: turn a regular-expression pattern into a state machine that matches in linear time, instead of a backtracking engine that can blow up exponentially on pathological input. Based on Russ Cox's classic series on Thompson NFA construction.

This branch doesn't lean on Atlas I as directly as the others — it's the odd one out in the warm-up phase, included because parsing and small-automaton construction are foundational skills the rest of the atlas (the SQL parser in [relational-layer-and-query-engine](https://ldamoredev.github.io/lowlevel-notes-ii/en/lowlevel-ii/relational-layer-and-query-engine/index.html), the HTTP parser) will reuse directly.

## Planned notes

- Why backtracking regex engines go exponential, with a constructed pathological pattern
- Regular expressions as a tiny language: writing a parser for `concat`, `alternation` (`|`), `kleene star` (`*`), `+`, `?`, groups
- From AST to Thompson NFA: the construction rules for each operator
- Representing NFA states and epsilon transitions
- Simulating the NFA: running all active states in parallel per input character
- From NFA to DFA (subset construction) — and the tradeoff it buys you
- Character classes (`[a-z]`), anchors (`^`/`$`), and where they fit in the model
- Capture groups — why they're hard to add to an NFA simulation, and one way to do it
- Benchmarking against a naive backtracking implementation on adversarial input
- Comparing the design against `grep`'s and RE2's real-world engines

## Core sources

- Russ Cox, "Regular Expression Matching Can Be Simple And Fast" (swtch.com/~rsc/regexp/) — the spine of this entire branch.
- "Regular Expression Matching: the Virtual Machine Approach" (Cox, same series) — for the capture-group extension.
- *Compilers: Principles, Techniques, and Tools* (Aho et al.) — NFA/DFA construction as taught in the dragon book.

**Connects to:** [[lowlevel-ii/relational-layer-and-query-engine/index|Relational Layer & Query Engine]] · [[lowlevel-ii/http-server-from-scratch/index|HTTP Server from Scratch]]
