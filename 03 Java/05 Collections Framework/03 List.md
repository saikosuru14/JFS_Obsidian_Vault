---
title: List
aliases:
  - List
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
  - collections
related:
  - "[[Collections Framework]]"
  - "[[ArrayList]]"
  - "[[LinkedList]]"
  - "[[Vector]]"
---

# List

## Overview
`List` is an ordered collection allowing duplicates and positional (index) access. Main implementations: [[ArrayList]] (array-backed), [[LinkedList]] (doubly linked), [[Vector]] (legacy, synchronized).

## When to Use
- Need ordering and/or index access → `List`.
- Random access + mostly reads → `ArrayList` (the default choice).
- Frequent add/remove at both ends / as a queue → `ArrayDeque` or `LinkedList`.

## Key Operations
`get(i)`, `set(i,e)`, `add(e)`, `add(i,e)`, `remove(i)`, `indexOf(e)`, `subList()`.

## Best Practices
- Default to `ArrayList`.
- Create immutable lists with `List.of(...)`; unmodifiable views with `Collections.unmodifiableList`.
- Prefer `list.removeIf(...)` over manual iteration for bulk removal.

## Common Mistakes
- Using `LinkedList` expecting speed — it rarely beats `ArrayList` due to cache locality.
- Structural modification during for-each iteration.

## Interview Questions
- `ArrayList` vs `LinkedList` — when does each win?
- How does `subList` relate to the backing list (view semantics)?

## Related Topics
- [[ArrayList]] · [[LinkedList]] · [[Vector]] · [[Collections Framework]]

## Quick Revision
- Ordered, indexed, duplicates allowed. Default to ArrayList; LinkedList only for heavy end operations.
