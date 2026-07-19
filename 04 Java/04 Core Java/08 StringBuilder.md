---
title: StringBuilder
aliases:
  - StringBuilder
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: Medium
interview: 4
revision: Weekly
order: 8
tags:
  - java
  - core
related:
  - "[[String]]"
  - "[[StringBuffer]]"
---

# StringBuilder

## Overview
Mutable, resizable character sequence for efficient string construction. Not synchronized — the right choice for single-threaded building (the common case).

## Why It Matters
`String` concatenation in a loop is O(n²) (new object each step). `StringBuilder` appends in amortized O(1).

## Example
```java
var sb = new StringBuilder(expectedSize);   // presize to avoid resizes
for (var part : parts) sb.append(part).append(',');
String result = sb.toString();
```
Note: the compiler already rewrites simple `a + b + c` into `StringBuilder` — the win is in **loops**.

## Performance
- Presize with an initial capacity for large builds.
- Faster than `StringBuffer` (no synchronization).

## Best Practices
- Use in loops / conditional building.
- For joining collections, prefer `String.join` / `Collectors.joining`.

## Common Mistakes
- `+=` on `String` inside loops.
- Using `StringBuffer` when no cross-thread sharing exists.

## Interview Questions
- StringBuilder vs StringBuffer vs String?
- Why is `+` in a loop bad?
- Does the compiler optimize simple concatenation? (yes)

## Related Topics
- [[String]] · [[StringBuffer]]

## Quick Revision
- Mutable, unsynchronized, amortized O(1) append. Use in loops, presize for big builds. Prefer over StringBuffer single-threaded.
