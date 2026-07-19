---
title: Checked vs Unchecked Exceptions
aliases:
  - Checked vs Unchecked Exceptions
domain: Java
module: Exception Handling
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - java
  - exceptions
related:
  - "[[Exception Hierarchy]]"
  - "[[Custom Exceptions]]"
---

# Checked vs Unchecked Exceptions

## Overview
**Checked** exceptions must be declared (`throws`) or handled at compile time. **Unchecked** exceptions (`RuntimeException` and subclasses) need neither.

## Why It Matters
The choice shapes your API contract. Overusing checked exceptions creates boilerplate and leaky abstractions; overusing unchecked ones hides failure modes.

## How It Works
| | Checked | Unchecked |
|---|---------|-----------|
| Base | `Exception` (not Runtime) | `RuntimeException` |
| Compiler | Must handle/declare | No requirement |
| Examples | `IOException`, `SQLException` | `NPE`, `IllegalArgumentException` |
| Use for | Recoverable, expected conditions | Programming errors / precondition violations |

## Example
```java
// checked: caller can reasonably recover or must acknowledge
void load(Path p) throws IOException { Files.readAllLines(p); }

// unchecked: caller violated a precondition
void setAge(int age) {
    if (age < 0) throw new IllegalArgumentException("age < 0");
}
```

## Best Practices
- Use unchecked for programming errors (bad arguments, illegal state).
- Use checked only when the caller can realistically recover.
- Modern frameworks (Spring) favor unchecked exceptions; wrap checked ones at boundaries.
- Don't declare `throws Exception` — be specific.

## Common Mistakes
- Wrapping everything in checked exceptions, forcing `try/catch` noise.
- Losing the original cause when rethrowing (always pass `cause`).

## Interview Questions
- When would you choose checked over unchecked?
- Why does Spring's `DataAccessException` hierarchy use unchecked exceptions?
- How do you preserve the root cause when rethrowing?

## Related Topics
- [[Exception Hierarchy]]
- [[Custom Exceptions]]

## Quick Revision
- Checked = compiler-enforced, recoverable; unchecked = programming errors. Prefer unchecked; wrap at boundaries; keep the cause.
