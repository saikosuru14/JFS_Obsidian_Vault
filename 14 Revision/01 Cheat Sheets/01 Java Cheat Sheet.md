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

> Fast recall for [[Java]]. See the [[Java Index|Java domain]] for depth.

## Collections
- `ArrayList` O(1) get, O(n) insert-middle; `LinkedList` O(1) ends, O(n) index.
- `HashMap` avg O(1); treeifies a bucket to a red-black tree after 8 entries (cap ≥ 64). Load factor 0.75.
- `HashMap` allows one null key; `Hashtable`/`ConcurrentHashMap` allow none.
- `TreeMap`/`TreeSet` O(log n), sorted. `LinkedHashMap` keeps insertion (or access) order.
- Fail-fast iterators throw `ConcurrentModificationException`.

## equals() / hashCode()
- Equal objects **must** have equal hashCodes. Override both together.
- Use immutable keys in maps/sets.

## Concurrency
- `synchronized` = intrinsic lock; `ReentrantLock` = explicit, supports `tryLock`, fairness.
- `volatile` = visibility (no atomicity for compound ops); use `Atomic*` for atomic counters.
- Prefer `ExecutorService` over raw threads; `CompletableFuture` for async composition.
- `ConcurrentHashMap` for concurrent maps; never `HashMap` across threads.
- Java 21: virtual threads (`Thread.ofVirtual`) for high-concurrency I/O.

## JVM & Memory
- Areas: heap (young: eden+survivors, old), metaspace, stacks, PC register.
- GC: G1 (default), ZGC/Shenandoah for low pause. Minor GC = young, Major/Full = old.
- Common leaks: static collections, unclosed resources, listeners not removed.

## Modern Java
- `record`, `sealed`, pattern matching, `var`, `Optional`, Streams, lambdas, `switch` expressions.
- Streams: lazy, single-use; prefer `map/filter/collect`; avoid side effects.

## Top Interview One-Liners
- Why HashMap O(1)? Direct bucket index from hash.
- String immutability → thread-safe, cacheable (string pool).
- `==` compares references; `.equals()` compares value.
- Checked vs unchecked exceptions; try-with-resources for `AutoCloseable`.

## Revision Checklist
- [ ] Collections complexity table
- [ ] equals/hashCode contract
- [ ] Concurrency utilities
- [ ] GC generations and collectors
- [ ] Streams and functional APIs
