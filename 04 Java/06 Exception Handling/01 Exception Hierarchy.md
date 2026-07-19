---
title: Exception Hierarchy
aliases:
  - Exception Hierarchy
domain: Java
module: Exception Handling
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
  - exceptions
related:
  - "[[Checked vs Unchecked Exceptions]]"
---

# Exception Hierarchy

## Overview
All errors in Java derive from `Throwable`, which splits into `Error` (JVM-level, unrecoverable) and `Exception` (application-level, often recoverable). `RuntimeException` is the unchecked branch of `Exception`.

## Why It Matters
Knowing the hierarchy tells you what to catch, what to let propagate, and what never to swallow.

```
Throwable
├── Error                (OutOfMemoryError, StackOverflowError) — do not catch
└── Exception
    ├── RuntimeException  (NPE, IllegalArgument, IndexOutOfBounds) — unchecked
    └── (checked)         (IOException, SQLException) — must handle or declare
```

## How It Works
- The compiler enforces handling only for **checked** exceptions (Exception minus RuntimeException).
- `catch` matches by type, including subclasses — order catch blocks most-specific first.
- Catching `Throwable`/`Error` is almost always wrong; the JVM may be in an unrecoverable state.

## Best Practices
- Catch the most specific type you can act on.
- Never catch `Error`.
- Don't catch `Exception` broadly except at well-defined boundaries (e.g., a request handler).

## Common Mistakes
- `catch (Exception e) {}` — swallowing everything, hiding bugs.
- Catching `Throwable` and masking `OutOfMemoryError`.

## Interview Questions
- Difference between `Error` and `Exception`?
- Where does `RuntimeException` sit and why is it unchecked?
- Is it ever correct to catch `Throwable`?

## Related Topics
- [[Checked vs Unchecked Exceptions]]

## Quick Revision
- `Throwable` → `Error` (don't catch) + `Exception`; `RuntimeException` = unchecked branch.
