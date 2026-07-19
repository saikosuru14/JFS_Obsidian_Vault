---
title: Streams
aliases:
  - Streams
domain: Java
module: Streams API
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Streams API Index|Streams API]]"
---

# Streams

## Overview
A stream is a lazy, single-use pipeline over a data source. It is **not** a data structure — it carries no storage and doesn't mutate its source. A pipeline = **source -> intermediate operations (lazy) -> one terminal operation (eager)**.

## Why It Matters
Streams replace verbose loops with declarative transformations and enable easy parallelism. Collectors and reduction are heavily tested, and misusing laziness/parallelism causes real bugs.

## Pipeline Anatomy
```java
List<String> names = people.stream()          // source
    .filter(p -> p.age() >= 18)                // intermediate (lazy)
    .map(Person::name)                         // intermediate (lazy)
    .sorted()                                  // intermediate (lazy)
    .collect(Collectors.toList());             // terminal (eager)
```

- **Intermediate** (return a Stream, lazy): `filter`, `map`, `flatMap`, `sorted`, `distinct`, `limit`, `peek`.
- **Terminal** (produce a result/side-effect, trigger execution): `collect`, `reduce`, `forEach`, `count`, `anyMatch`, `findFirst`, `toList` (Java 16+).

## Laziness & Short-Circuiting
Nothing runs until the terminal op. Operations are fused and executed element-by-element, so `filter(...).findFirst()` stops at the first match instead of processing everything. `limit`/`anyMatch`/`findFirst` short-circuit even infinite streams (`Stream.iterate`, `generate`).

## Collectors
```java
Map<Dept,List<Emp>> byDept = emps.stream()
    .collect(Collectors.groupingBy(Emp::dept));

Map<Boolean,List<Emp>> parts = emps.stream()
    .collect(Collectors.partitioningBy(e -> e.salary() > 100_000));

String csv = names.stream().collect(Collectors.joining(", "));
double avg = emps.stream().collect(Collectors.averagingDouble(Emp::salary));
```
Common: `toList/toSet/toMap`, `groupingBy`, `partitioningBy`, `joining`, `counting`, `summingInt`, `mapping`.

## reduce vs collect
- `reduce` — immutable combination into a single value (`sum`, `min`): `reduce(0, Integer::sum)`.
- `collect` — mutable accumulation into a container (list, map, string).

## Primitive Streams
`IntStream`/`LongStream`/`DoubleStream` avoid boxing and add `sum()`, `average()`, `range()`. Use `mapToInt`/`boxed` to convert.

## Parallel Streams (careful)
`.parallelStream()` splits work across the common [[ForkJoinPool]]. Use only for large, CPU-bound, stateless, associative work on splittable sources. Pitfalls: shared mutable state, ordering costs, and blocking tasks starving the shared pool.

## Common Mistakes
- **Reusing a stream** — a stream is single-use; a second terminal op throws `IllegalStateException`.
- **Side effects in `map`/`peek`** — keep operations pure; don't mutate external state.
- **`forEach` on parallel streams** expecting order — use `forEachOrdered` or avoid.

## Streams vs Collections
| | Collection | Stream |
|--|-----------|--------|
| Storage | stores elements | no storage |
| Evaluation | eager | lazy |
| Reuse | reusable | single-use |
| Purpose | store/access | compute/transform |

## Interview Questions
- **Intermediate vs terminal operation?** Intermediate returns a lazy Stream; terminal triggers execution and yields a result.
- **Are streams lazy?** Yes — intermediates run only when a terminal op executes, enabling fusion and short-circuiting.
- **reduce vs collect?** Immutable reduction to one value vs mutable accumulation into a container.
- **When to use parallel streams?** Large, CPU-bound, stateless, associative operations on splittable sources — never with blocking I/O or shared mutable state.
- **Can you reuse a stream?** No — it's single-use.

## Related Topics
- [[Functional Programming Index|Functional Programming]] · [[Collections Framework]] · [[ForkJoinPool]]

## Quick Revision
- Lazy, single-use pipeline: source -> intermediate (filter/map/sorted) -> terminal (collect/reduce). Collectors for grouping. Primitive streams avoid boxing. Parallel only for big CPU-bound stateless work.
