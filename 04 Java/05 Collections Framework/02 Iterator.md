---
title: Iterator
aliases:
  - Iterator
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
  - collections
related:
  - "[[Collections Framework]]"
---

# Iterator

## Overview
`Iterator` provides sequential traversal of a `Collection` with safe removal during iteration. `ListIterator` adds bidirectional traversal and index-aware operations for lists.

## How It Works
- `hasNext()` / `next()` walk elements; `remove()` deletes the last returned element safely.
- Most collection iterators are **fail-fast**: structurally modifying the collection outside the iterator increments a `modCount`, and the next `next()` throws `ConcurrentModificationException`.
- **Fail-safe** iterators (e.g., `CopyOnWriteArrayList`, `ConcurrentHashMap`) iterate over a snapshot and don't throw.

## Example
```java
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (it.next().isBlank()) it.remove();  // safe removal
}
```

## Best Practices
- Use `Iterator.remove()` (or `removeIf`) instead of removing inside a for-each loop.
- Prefer enhanced for-each / streams for read-only traversal.

## Common Mistakes
- Modifying a collection inside a for-each loop → `ConcurrentModificationException`.

## Interview Questions
- `Iterator` vs `ListIterator`?
- Fail-fast vs fail-safe iterators — how does fail-fast work (`modCount`)?

## Related Topics
- [[Collections Framework]]

## Quick Revision
- `hasNext/next/remove`; fail-fast via `modCount` throws CME; fail-safe iterates a snapshot. Remove via iterator, not the loop.
