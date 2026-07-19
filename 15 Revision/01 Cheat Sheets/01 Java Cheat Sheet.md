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

> Interview-ready revision for [[Java]] (4–5 YOE). Concepts, code, tables, and Q&A with answers.

---

## 1. Collections

### Complexity
| Structure | get/contains | add | remove | Ordered? |
|-----------|--------------|-----|--------|----------|
| ArrayList | O(1) index / O(n) search | amortized O(1) end | O(n) | insertion |
| LinkedList | O(n) | O(1) ends | O(1) at node | insertion |
| HashMap/HashSet | O(1) avg | O(1) | O(1) | none |
| LinkedHashMap | O(1) | O(1) | O(1) | insertion/access |
| TreeMap/TreeSet | O(log n) | O(log n) | O(log n) | sorted |
| ArrayDeque | O(1) ends | O(1) | O(1) | insertion |

### HashMap internals
Buckets = an array of `Node<K,V>`. Index = `(n-1) & hash`, where `hash = h ^ (h >>> 16)` (spreads high bits). Collisions form a linked list; a bin **treeifies to a red-black tree at 8 nodes** *only if* table capacity ≥ 64 (else it resizes instead), and untreeifies at 6. Default capacity 16, load factor 0.75 → resize (double) at 12 entries. Resize rehashes all entries — presize for large maps.

```java
Map<String,Integer> m = new HashMap<>(1 << 16);   // presize: avoid rehash storms
m.merge(word, 1, Integer::sum);                    // atomic-ish count idiom
m.computeIfAbsent(key, k -> new ArrayList<>()).add(v);  // multimap idiom
```
- One `null` key allowed (bucket 0); `Hashtable`/`ConcurrentHashMap` allow none.
- Mutating a key's `equals`/`hashCode` fields after insertion "loses" the entry.

### ConcurrentHashMap (Java 8+)
No segments (pre-8 design gone). Reads are lock-free; a write CASes the first node into an empty bin or `synchronized`-locks the bin head on collision. Size is tracked with striped counters (`CounterCell`, LongAdder-style). Iterators are **weakly consistent** (never throw `ConcurrentModificationException`). Use `computeIfAbsent`/`merge` for atomic compound updates; a sequence of separate calls is still not atomic.

### Gotchas
- Fail-fast iterators (`ArrayList`, `HashMap`) use `modCount` → `ConcurrentModificationException`; remove via `Iterator.remove()`/`removeIf`.
- `Arrays.asList` is fixed-size; `List.of` is immutable and rejects nulls.
- Prefer `ArrayDeque` over `Stack`/`LinkedList`.

---

## 2. equals / hashCode / Comparable

**Contract:** if `a.equals(b)` then `a.hashCode() == b.hashCode()`. Unequal objects *may* collide. Reflexive, symmetric, transitive, consistent.

```java
@Override public boolean equals(Object o){
    if (this == o) return true;
    if (!(o instanceof User u)) return false;      // pattern matching
    return id == u.id && Objects.equals(email, u.email);
}
@Override public int hashCode(){ return Objects.hash(id, email); }
```
- `record User(long id, String email){}` generates value-based `equals`/`hashCode`/`toString`.
- `Comparable` = natural order (`compareTo`); `Comparator` = external, composable. Never `a - b` (overflow) → use `Integer.compare` / `Comparator.comparingInt`. Keep `compareTo` **consistent with equals** for `TreeSet`/`TreeMap`.

```java
users.sort(Comparator.comparing(User::name).thenComparingInt(User::age).reversed());
```

---

## 3. Strings
Immutable, backed by `byte[]` + a coder (Latin-1/UTF-16, "compact strings" since Java 9). Literals are interned in the string pool.

```java
String a = "abc", b = new String("abc");
a == b;          // false (different objects)
a.equals(b);     // true
a == b.intern(); // true (pool)
```
- Immutable ⇒ safe map key (cached hash), thread-safe, poolable.
- Concatenation in a loop is O(n²) → use `StringBuilder` (compiler already optimizes simple `a+b+c`).
- `Integer` caches −128..127 → `==` "works" for small boxed ints only. Always `.equals`.

---

## 4. Concurrency

### Java Memory Model — happens-before
Establishes visibility + ordering. Key edges: program order in a thread; `volatile` write → subsequent read; `synchronized` unlock → next lock on same monitor; `Thread.start()` → thread's actions; thread's actions → `join()`; `final` field init → publication.

### Coordination primitives
| Tool | Guarantees | Use for |
|------|-----------|---------|
| `volatile` | visibility + ordering (no atomicity) | flags, double-checked locking ref |
| `synchronized` | mutual exclusion + visibility | simple critical sections |
| `ReentrantLock` | tryLock, timeout, fairness, conditions | advanced locking |
| `Atomic*` / `LongAdder` | lock-free CAS | counters (LongAdder wins under contention) |
| `ConcurrentHashMap` | concurrent map | shared maps |

```java
ExecutorService pool = Executors.newFixedThreadPool(n);
CompletableFuture
    .supplyAsync(() -> fetch(id), pool)
    .thenApply(this::transform)
    .exceptionally(ex -> fallback())
    .thenAccept(this::save);
```
- Pool sizing: CPU-bound ≈ cores; IO-bound higher (`~cores * (1 + wait/compute)`).
- **Virtual threads (Java 21):** `Thread.ofVirtual().start(...)` / `newVirtualThreadPerTaskExecutor()` for high-concurrency **blocking IO**; don't pool them; avoid `synchronized`/native calls in hot paths (they *pin* the carrier) — use `ReentrantLock`.
- `ThreadLocal` in a pool leaks unless you `remove()` in a finally.
- Deadlock: acquire locks in a global order; use `tryLock(timeout)`.

### Common bugs
- Check-then-act (`if(!map.containsKey) map.put`) → use `putIfAbsent`/`computeIfAbsent`.
- `volatile` counter `++` is not atomic → `AtomicInteger`.
- Double-checked locking needs `volatile` on the instance field.

---

## 5. JVM & Memory

**Runtime areas:** heap (shared) — young (Eden + 2 Survivors) + Old; **Metaspace** (native memory, class metadata — not the heap); per-thread stacks + PC register. Most objects die young (generational hypothesis) → cheap minor GCs.

### Garbage collectors
| GC | Best for | Notes |
|----|----------|-------|
| Serial | tiny heaps / single core | stop-the-world |
| Parallel | batch throughput | multi-threaded young+old |
| **G1** (default 9+) | balanced, large heaps | region-based, pause target `-XX:MaxGCPauseMillis` |
| ZGC | low pause, huge heaps | sub-ms pauses, concurrent |
| Shenandoah | low pause | concurrent compaction |

- Allocation rate drives GC frequency → reduce object churn first.
- Set `-Xms == -Xmx`; in containers use `-XX:MaxRAMPercentage`.
- Diagnose: `-Xlog:gc*`, heap dump (`jmap`) + Eclipse MAT (leak = dominator tree), JFR / async-profiler. `OutOfMemoryError: Metaspace` ≠ heap (usually classloader leak).

---

## 6. Modern Java (8 → 21)
```java
record Point(int x, int y) {}                       // immutable data carrier
sealed interface Shape permits Circle, Square {}     // closed hierarchy
String s = switch (day) {                            // switch expression
    case MON, TUE -> "start";
    default -> "other";
};
Object o = ...;
if (o instanceof String str && !str.isBlank()) {}    // pattern matching
var list = new ArrayList<String>();                  // local type inference
String json = """
    { "id": 1 }""";                                  // text block
```
- Streams: lazy, single-use, no side effects; `map/filter/collect`; use `IntStream` to avoid boxing; a plain loop can beat a stream in hot paths — measure with JMH.
- `Optional` for **return values** (never fields/params/collections); `orElseGet` for costly defaults.

---

## 7. Exceptions
- `Throwable` → `Error` (never catch) / `Exception` → `RuntimeException` (unchecked).
- Checked = recoverable + compiler-enforced; unchecked = programming errors. Modern APIs favor unchecked; wrap+translate at layer boundaries and **keep the cause**.
- `try-with-resources` auto-closes (reverse order); close errors are **suppressed** (`getSuppressed()`). Don't `return` in `finally`. Don't use exceptions for control flow (stack-trace fill is costly).

---

## 8. Interview Q&A (with answers)

**Q: Why is HashMap O(1) average, and when does it degrade?**
A: The key's hash maps directly to a bucket, so no linear scan on average. It degrades to O(n) with many collisions (bad `hashCode`); Java 8 mitigates by treeifying a bin to a red-black tree (O(log n)) at 8 nodes when capacity ≥ 64.

**Q: `volatile` vs `synchronized`?**
A: `volatile` gives visibility + ordering for a single variable but not atomicity for compound ops. `synchronized` gives mutual exclusion *and* visibility for a critical section. Use `volatile` for flags/publication, `synchronized`/locks for multi-step invariants.

**Q: What does happens-before guarantee?**
A: If action A happens-before B, A's memory writes are visible to B and ordered before it. Provided by volatile, synchronized, thread start/join, and final-field publication.

**Q: When do you pick virtual threads?**
A: High-concurrency **blocking IO** (thousands of concurrent requests). They're cheap to create (don't pool). Avoid `synchronized` blocks around blocking calls (pinning) — use `ReentrantLock`. CPU-bound work still wants a bounded pool.

**Q: `ConcurrentHashMap` vs `Collections.synchronizedMap` vs `Hashtable`?**
A: The latter two lock the whole map per operation; CHM locks per bin (or CAS), so it scales under contention, with weakly-consistent iterators. CHM disallows null keys/values.

**Q: How do you find and fix a memory leak?**
A: Reproduce, take a heap dump, open in MAT, inspect the dominator tree / GC roots for the retained set. Common causes: static collections/caches without bounds, unremoved listeners, `ThreadLocal` in pools, classloader leaks (Metaspace).

**Q: `equals`/`hashCode` contract and why it matters?**
A: Equal objects must have equal hash codes; otherwise a `HashMap`/`HashSet` stores under one bucket and looks up in another → entries "disappear." Override both together with the same fields.

**Q: String immutability — benefits?**
A: Thread-safety, safe sharing, cached hash (fast map keys), and the string pool. Trade-off: transformations allocate new objects.

---

## Revision Checklist
- [ ] Collections complexity + HashMap/CHM internals
- [ ] equals/hashCode contract + Comparator combinators
- [ ] JMM happens-before + volatile/synchronized/atomic
- [ ] Executors, CompletableFuture, virtual threads (+ pinning)
- [ ] GC collectors + leak diagnosis (MAT/JFR)
- [ ] records/sealed/pattern matching/streams
- [ ] Checked vs unchecked + try-with-resources
