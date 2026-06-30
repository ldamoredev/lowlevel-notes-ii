# Low-Level Atlas II — Content Plan

Target: 8–12 rich notes per branch (Atlas I targeted 10–15; this atlas's notes are tied to runnable artifacts, so slightly fewer, denser notes per branch is the right calibration). Reader profile: already completed [Low-Level Atlas I](https://github.com/ldamoredev/lowlevel-notes) in full.

## Throughline

Atlas I took the reader from "I can program" to "I understand the machine," top-down through the machine model, C, assembly, the toolchain, systems programming, concurrency basics, and a small OS. This atlas assumes all of that and inverts the motion: instead of descending through layers of abstraction, the reader climbs *project by project*, building real systems the industry actually runs — a shell, a malloc, a regex engine, a Git clone, an HTTP server, and a database engine — with concurrency depth developed *in situ*, anchored in the server and the database engine rather than taught in isolation.

## Fixed decisions (do not revisit)

- Language: C throughout, no frameworks, no high-level libraries beyond libc (sockets are raw BSD sockets, not libcurl/libuv; the regex/SQL parsers are hand-written, not generated).
- Every branch must produce a runnable artifact, not just notes — this is the one rule that differentiates this atlas from Atlas I's note-first approach.
- The database engine is the spine project, built in two branches and four milestones (v0 → v3), mirroring Atlas I's OS-from-scratch milestone structure.
- Concurrency (`concurrency-in-practice`) develops in parallel with the networked-systems and database-engine phases — never write it as a standalone phase completed before or after them.
- Topic slug: `lowlevel-ii` (fixed — referenced throughout `build.py` and every wikilink).
- Atlas I is referenced via full external URLs (`https://ldamoredev.github.io/lowlevel-notes/...`) — never wikilinks, the repos are separate.

## Taxonomy (phase → branch)

- **00 · Orientation** — no branches; entry-layer notes only (`start-here`, `must-know`, the section `index`).
- **01 · Warm-up Builds** — `shell-from-scratch`, `malloc-from-scratch`, `regex-engine-from-scratch`.
- **02 · Data & Serialization** — `mini-git`.
- **03 · Networked Systems** — `http-server-from-scratch`.
- **04 · Concurrency & Performance II** — `concurrency-in-practice`.
- **05 · The Database Engine** — `kv-store-and-durability`, `relational-layer-and-query-engine`.
- **★ · Always Active** — `craftsmanship-low-level-ii`.

## Progress

Skeleton phase complete: every branch has a populated `index.md` (intro + planned-notes roadmap + core sources + connects-to), but **zero atomic notes and zero `examples/` artifacts exist yet** anywhere in the atlas. This mirrors exactly where Atlas I started.

- [ ] **shell-from-scratch** — index ✓ · 0/12 notes written. Suggested write order: the read-parse-execute loop → tokenizing → fork+exec → pipes → redirection → built-ins → signals → job control → environment/PATH → history.
- [ ] **malloc-from-scratch** — index ✓ · 0/12 notes written. Suggested write order: the contract → sbrk vs mmap → first-fit free list → headers/alignment → coalescing → splitting → realloc → thread-safety → benchmarking vs glibc.
- [ ] **regex-engine-from-scratch** — index ✓ · 0/10 notes written. Suggested write order: why backtracking explodes → parsing the pattern → Thompson construction → NFA simulation → character classes/anchors → capture groups → benchmarking.
- [ ] **mini-git** — index ✓ · 0/12 notes written. Suggested write order: the object model → hashing → blobs → trees → commits → init/hash-object/cat-file → write-tree → log → branches/refs → the index → diffing.
- [ ] **http-server-from-scratch** — index ✓ · 0/12 notes written. Suggested write order: the socket API → blocking server → parsing the request → chunked encoding → why fork/thread-per-connection doesn't scale → epoll/kqueue → keep-alive → router → responses → backpressure → load testing.
- [ ] **concurrency-in-practice** — index ✓ · 0/11 notes written. Written *as* the HTTP server and database engine get built, not before. Suggested anchors: thread pools (HTTP server) → event-loop vs thread-per-connection (HTTP server) → locks vs lock-free (KV store) → false sharing (B-Tree page cache) → benchmarking methodology (both).
- [ ] **kv-store-and-durability** — index ✓ (featured) · 0/12 notes written. v0 first (in-memory B-Tree), then v1 (durability). Suggested write order: why a B-Tree → page format → copy-on-write nodes → search/insert/split → delete/merge → free-space management → fsync semantics → WAL → crash recovery → checkpointing → benchmarking.
- [ ] **relational-layer-and-query-engine** — index ✓ · 0/12 notes written. Depends on kv-store-and-durability v1 being functionally complete first. v2 (relational layer) before v3 (SQL + transactions).
- [ ] **craftsmanship-low-level-ii** — index ✓ · 0/11 notes written (playbooks). Written alongside whichever branch is currently active — e.g. write the HTTP-parser fuzzing playbook while http-server-from-scratch is in progress, not after the whole atlas is done.
- [ ] ES overlay pass — not started; currently relying on build.py's EN-fallback-with-banner for all ES pages (same situation Atlas I was in for 6 of its 10 branches).

## Per-branch note outlines + core sources

### shell-from-scratch *(Warmup)*

*Sources: "Build Your Own Shell" (codecrafters) ← spine; APUE (Stevens & Rago); The Linux Programming Interface (Kerrisk).*

The read–parse–execute loop · tokenizing a command line · building an AST for pipelines/redirections/`&&`/`||`/`;` · `fork()`+`exec()` · wiring pipes (`pipe()`, `dup2()`) · I/O redirection · built-ins vs external commands · signal handling (`SIGINT`/`SIGTSTP`) · job control (`&`, `Ctrl-Z`, `fg`/`bg`, process groups) · environment variables and `$PATH` · a minimal `.shellrc` and history · comparing against dash/bash.

### malloc-from-scratch *(Warmup)*

*Sources: CS:APP (Bryant & O'Hallaron) ← spine; Doug Lea malloc design notes; Understanding and Using C Pointers (Reese).*

The malloc/free/realloc/calloc contract · sbrk vs mmap · a first-fit free list · block headers/footers · alignment · coalescing · splitting · best-fit vs first-fit vs segregated lists · implementing realloc without always copying · thread-safety · benchmarking vs glibc and mimalloc · where this allocator breaks.

### regex-engine-from-scratch *(Warmup)*

*Sources: Russ Cox's regexp series (swtch.com/~rsc/regexp/) ← spine; Compilers (Aho et al.).*

Why backtracking goes exponential · parsing the pattern language · AST to Thompson NFA · NFA states and epsilon transitions · simulating the NFA · subset construction (NFA→DFA) · character classes and anchors · capture groups · benchmarking vs naive backtracking · comparing to grep/RE2.

### mini-git *(Data)*

*Sources: "Write yourself a Git" (wyag) ← spine; codecrafters Build Your Own Git; Pro Git "Git Internals".*

The object model (blobs/trees/commits) · hashing (SHA-1/SHA-256) · the blob object · the tree object · the commit object and the DAG · writing/reading `.git/objects` · `init`/`hash-object`/`cat-file` · `write-tree` · `log` · branches/refs as files · the index/staging area · diffing two trees.

### http-server-from-scratch *(Networked)*

*Sources: Beej's Guide to Network Programming ← spine; RFC 7230/7231; codecrafters Build Your Own HTTP Server; The C10K Problem (Kegel).*

The socket API · a blocking single-connection server · parsing the request line/headers/body by hand · chunked transfer-encoding · why fork/thread-per-connection doesn't scale · the epoll/kqueue event loop · edge- vs level-triggered epoll · keep-alive and connection state machines · a minimal router · writing responses · backpressure · load-testing with wrk/hey.

### concurrency-in-practice *(Concurrency)*

*Sources: C++ Concurrency in Action (Williams); Preshing on Programming; The Art of Multiprocessor Programming (Herlihy & Shavit); The C10K Problem (Kegel) ← shared with http-server-from-scratch.*

Thread pools and work queues · locks vs lock-free for the KV store's hot paths · event-loop vs thread-per-connection, measured · false sharing in the connection table and page cache · cache-aware layout under concurrent access · read-write locks vs a single mutex · memory-ordering bugs under real load · lock-contention profiling · benchmarking methodology (percentiles, warm-up) · an HTTP-server load test with a written postmortem · a database-engine load test under concurrent writers.

### kv-store-and-durability *(Engine, v0 → v1)*

*Sources: Build Your Own Database From Scratch (build-your-own.org) ← spine; Database Internals (Petrov); Designing Data-Intensive Applications ch. 3 (Kleppmann); Architecture of SQLite; cstack's db_tutorial.*

Why a B-Tree, not a hash table · B-Tree vs B+Tree · the on-disk page format · copy-on-write nodes · search/insert/split · deletion and merging · free-space management · fsync/fdatasync semantics · the write-ahead log (format, append, replay) · crash recovery (and testing it by actually killing the process) · checkpointing · benchmarking write throughput vs durability guarantees.

### relational-layer-and-query-engine *(Engine, v2 → v3)*

*Sources: Build Your Own Database From Scratch (build-your-own.org) ← spine, continued; Database Internals (Petrov); Designing Data-Intensive Applications (Kleppmann); Architecture of SQLite (VDBE); cstack's db_tutorial.*

Mapping tables onto the KV store · secondary indexes · a minimal SQL grammar · lexing/parsing SQL (shared technique with regex-engine-from-scratch) · an AST and query planner · index selection · a row-at-a-time executor · what ACID requires here · copy-on-write transactions vs MVCC · concurrent readers/writers · write-write conflict detection · benchmarking query throughput under concurrent load.

### craftsmanship-low-level-ii *(Always-on)*

*Sources: Test-Driven Development for Embedded C (Grenning) ← spine, continued from Atlas I; libFuzzer/AFL++ docs; Property-Based Testing with PropEr (technique reference only); TSan docs.*

Testing a protocol parser with malformed input · testing Git's object-format parser against corruption · reproducing race conditions reliably · TSan in the build · fuzzing the B-Tree page format and the WAL format · fuzzing the HTTP parser against spec edge cases · property-based testing for the database engine's invariants · TDD when state lives on disk · crash-recovery testing · contracts/asserts for B-Tree invariants · a code-review checklist for memory-unsafe concurrent C.

## Conventions

- Atomic note shape: H1 = title, mental-model-first paragraph, mechanism sections, a runnable artifact under `examples/<branch>/<slug>/` that **must build and run as written**, named pitfalls, a closing `**Connects to:**` line, a `## Sources` section.
- `featured: true` is set on at most one note across the whole atlas (currently `kv-store-and-durability/index.md`, marking the spine project — note `build_home()` only promotes `concept`/`playbook` kind notes to the featured slot, not `index` notes, so once atomic notes exist in that branch, move `featured: true` onto the most representative one).
- `draft: true` excludes a note from the build, search index, and sitemap — use it for in-progress notes instead of half-publishing them.
- Wikilinks use the path form: `[[lowlevel-ii/branch/slug|Label]]`.
- Cite primary sources; one line of relevance per citation, no bare link dumps.

## Checklist (repo-level)

- [x] Repo scaffold (`content/`, `static/`, `scripts/`, `.github/workflows/`) mirroring Atlas I.
- [x] `build.py` adapted: `SECTION`, site metadata, `PHASES`, `BRANCHES`/`BRANCHES_ES`, `UI_STRINGS`, spine-roadmap home section, atlas-I continuity CTA.
- [x] "Blueprint & Graphite" visual identity applied to `atlas.css`.
- [x] All 9 branch `index.md` + root entry/phase/registry notes (EN).
- [x] Root docs: README, AGENTS, CONTENT-PLAN, SOURCES, GLOSSARY.
- [x] Static assets: favicon, OG image, PWA icons, deploy workflow.
- [ ] Clean `python3 build.py` run with `(unresolved links: 0)` — verify after this checklist is read.
- [ ] First atomic notes (suggested start: `shell-from-scratch`, per the write order above).
- [ ] ES overlays (currently 100% EN-fallback).
