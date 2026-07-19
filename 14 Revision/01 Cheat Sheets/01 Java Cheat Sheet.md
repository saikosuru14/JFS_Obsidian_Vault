---
title: Java Cheat Sheet
aliases:
  - Java Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - revision
  - java
---

# Java Cheat Sheet

> Mid-level recall for [[Java]] — internals, gotchas, and trade-offs.

## Collections (know the trade-offs)
- `HashMap`: bucket array; treeifies a bin at 8 nodes when cap ≥ 64; resize at load factor 0.75 (doubles). Never mutate key fields after insertion.
- `ArrayList` grows 1.5×; `LinkedList` loses on cache locality — default to `ArrayList`. `ArrayDeque` > `Stack`/`LinkedList` for stacks/queues.
- `ConcurrentHashMap` (Java 8): lock-free reads, per-bin CAS/`synchronized` writes, weakly-consistent iterators, no nulls. Use `computeIfAbsent`/`merge` for atomic updates.
- Fail-fast (`modCount` → CME) vs fail-safe (snapshot) iterators.
- Immutable: `List.of`, `Map.of` (throw on null, reject dupes).

## equals / hashCode / Comparable
- Equal ⇒ equal hashCode; use `Objects.hash`, same fields in both. `records` generate value-based equals/hashCode/toString.
- Comparators: `Comparator.comparingInt(...).thenComparing(...).reversed()`; never `a - b` (overflow). Keep `compareTo` consistent with `equals` for sorted sets/maps.

## Concurrency
- **JMM / happens-before**: `volatile` write→read, `synchronized` unlock→lock, thread start/join, final-field publication. `volatile` = visibility only (no compound atomicity).
- Prefer `java.util.concurrent`: `ExecutorService`, `CompletableFuture` (composition), `Atomic*`/`LongAdder` (hot counters), `ConcurrentHashMap`.
- `ThreadLocal` leaks in pools — always `remove()` in a finally.
- Sizing: CPU-bound ≈ cores; IO-bound higher. Java 21 **virtual threads** for high-concurrency blocking IO (don't pool them; avoid `synchronized` pinning — use `ReentrantLock`).
- Deadlock: lock ordering; `tryLock` with timeout.

## JVM & GC
- Heap: young (eden+2 survivors) + old; **Metaspace** (native, not heap). Most objects die young (generational hypothesis).
- Collectors: **G1** default (region-based, pause target); **ZGC/Shenandoah** for low pause on large heaps; Parallel for batch throughput.
- Allocation rate drives GC frequency → cut object churn first. Set `-Xms == -Xmx`.
- Diagnose: `-Xlog:gc*`, heap dump + MAT (leaks = dominators), JFR/async-profiler.

## Language (modern)
- `record`, `sealed`, pattern matching + `switch` expressions, text blocks, `var`.
- `Optional` for return values only (not fields/params); `orElseGet` for costly defaults.
- Streams: lazy, single-use; avoid side effects; a plain loop can beat streams in hot paths — measure (JMH).

## Sharp Interview Answers
- HashMap O(1)? direct bucket index from hash; degrades with poor hashing (→ O(log n) after treeify).
- String immutable → pooled, cacheable hash, safe map key, thread-safe.
- Fail-fast vs fail-safe; `volatile` vs `synchronized`; `wait/notify` require the monitor.
- `ConcurrentHashMap` vs `Collections.synchronizedMap` (per-bin vs whole-map lock).

## Revision Checklist
- [ ] Collections complexity + concurrency variants
- [ ] JMM happens-before rules
- [ ] Executors, CompletableFuture, virtual threads
- [ ] GC selection + diagnosis
- [ ] records/sealed/pattern matching
