---
title: String
aliases:
  - String
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 7
tags:
  - java
  - core
related:
  - "[[Immutability]]"
  - "[[StringBuilder]]"
---

# String

## Overview
`String` is immutable and backed by a `byte[]` (compact strings, Java 9+). Literals live in the **string pool**; `new String()` creates a distinct heap object.

## Why Immutable
- Safe as [[HashMap]] keys (hash cached, never changes).
- Thread-safe and freely shareable.
- Enables the string pool (deduped literals) — memory + `==` interning benefits.
- Security: paths, class names, connection strings can't be mutated under you.

## String Pool
- Literals are interned automatically; `new String("x")` is not (call `.intern()` to add).
- `"a" + "b"` of compile-time constants is folded to `"ab"` at compile time.

## Performance
- Concatenation in a loop creates many temporaries → use [[StringBuilder]].
- `substring` (Java 7u6+) copies the array (no shared backing → no leak).

## Best Practices
- Compare with `.equals` / `Objects.equals`, not `==`.
- Use `StringBuilder` for loops; `String.join`/`Collectors.joining` for lists; text blocks for multiline.

## Common Mistakes
- `==` on strings; heavy `+` concatenation in loops.
- Overusing `intern()` (can pressure the pool).

## Interview Questions
- Why is String immutable, and how does the pool work?
- `new String("x")` vs `"x"` — identity and pool?
- Why is String a good HashMap key?

## Related Topics
- [[Immutability]] · [[StringBuilder]] · [[StringBuffer]] · [[equals() vs ==]]

## Quick Revision
- Immutable, byte[]-backed, pooled literals. Great map key. Use StringBuilder in loops; compare with equals.
