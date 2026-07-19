---
title: Comparable vs Comparator
aliases:
  - Comparable vs Comparator
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 11
tags:
  - java
  - core
related:
  - "[[TreeMap]]"
  - "[[TreeSet]]"
---

# Comparable vs Comparator

## Overview
`Comparable` defines a type's **natural ordering** (`compareTo`, one per class). `Comparator` defines **external, swappable** orderings (`compare`, many possible) without touching the class.

## Comparison
| | Comparable | Comparator |
|---|-----------|------------|
| Method | `compareTo(T)` | `compare(T,T)` |
| Location | Inside the class | Separate/lambda |
| Count | One natural order | Many |
| Use | Default sort, TreeMap/TreeSet keys | Ad-hoc / multiple sorts |

## Example
```java
list.sort(Comparator.comparing(User::lastName)
                     .thenComparing(User::firstName)
                     .reversed());
users.sort(Comparator.comparingInt(User::age));   // avoids boxing
```

## Best Practices
- Use `Comparator.comparing/thenComparing/reversed` — don't hand-write subtraction (`a - b` overflows).
- Keep `compareTo` **consistent with `equals`** (esp. for [[TreeSet]]/[[TreeMap]], which use ordering for equality).
- Use `nullsFirst`/`nullsLast` for nullable keys.

## Common Mistakes
- `return a - b` integer overflow → use `Integer.compare`.
- Comparator inconsistent with equals → elements "missing" from tree collections.

## Interview Questions
- Comparable vs Comparator — when each?
- Why avoid `a - b` in comparators?
- Why must ordering be consistent with equals for TreeSet?

## Related Topics
- [[TreeMap]] · [[TreeSet]]

## Quick Revision
- Comparable = one natural order (compareTo); Comparator = many external orders (compare). Use Comparator combinators; keep consistent with equals; no subtraction.
