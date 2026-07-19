---
title: ConcurrentHashMap
aliases:
  - ConcurrentHashMap
domain: Java
module: Collections Framework
status: Not Started
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 17
tags:
  - java
  - collections
  - concurrency
related:
  - "[[Map]]"
  - "[[Concurrent Collections]]"
  - "[[HashMap]]"
---

# ConcurrentHashMap

## Overview
Thread-safe `Map` designed for high concurrency. Reads are lock-free; writes lock only a single bin, so many threads update different buckets in parallel.

## Internal Working
- **Java 8+**: array of bins; writes use CAS to install the first node and `synchronized` on the bin head for collisions. No global lock, no segments (the pre-8 design).
- Bins treeify after 8 collisions (like HashMap). Size tracked via striped counters (`CounterCell`) to avoid contention.
- **Weakly consistent** iterators: reflect some but not necessarily all concurrent updates; never throw `ConcurrentModificationException`.

## Why Not synchronizedMap / Hashtable
- Those lock the **entire** map per operation; ConcurrentHashMap locks per bin → far better throughput under contention.

## Atomic Operations
Use built-ins instead of check-then-act:
```java
map.putIfAbsent(k, v);
map.computeIfAbsent(k, key -> load(key));
map.merge(k, 1L, Long::sum);   // atomic counter
```

## Gotchas
- No `null` keys or values (ambiguous with "absent").
- `size()` is an estimate under concurrency.
- Compound logic across multiple calls is still not atomic — use the functional methods.

## Interview Questions
- How does ConcurrentHashMap achieve thread safety (Java 8 design)?
- Why is it better than `Collections.synchronizedMap`/`Hashtable`?
- Why no null keys/values? Are iterators fail-fast?

## Related Topics
- [[Map]] · [[Concurrent Collections]] · [[HashMap]]

## Quick Revision
- Lock-free reads, per-bin CAS/synchronized writes (Java 8, no segments), weakly consistent iterators, no nulls. Use computeIfAbsent/merge.
