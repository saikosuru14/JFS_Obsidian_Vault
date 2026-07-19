---
title: Autoboxing and Unboxing
aliases:
  - Autoboxing and Unboxing
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 6
tags:
  - java
related:
  - "[[Wrapper Classes]]"
---

# Autoboxing & Unboxing

## Overview
Autoboxing is the compiler automatically converting a primitive to its [[Wrapper Classes|wrapper]] (`int` -> `Integer`); unboxing is the reverse. It's syntactic sugar — the compiler inserts `Integer.valueOf` / `intValue()` calls.

## Why It Matters
Convenient, but it hides two real bugs: **NullPointerException** on unboxing `null`, and surprising **`==`** results due to the Integer cache. Both are classic interview traps.

## The `==` Trap
```java
Integer a = 127, b = 127;
System.out.println(a == b);   // true  - cached (-128..127)

Integer c = 128, d = 128;
System.out.println(c == d);   // false - different objects
System.out.println(c.equals(d)); // true - correct way
```
`Integer.valueOf` caches -128..127, so `==` compares the same cached reference for small values but different objects beyond the cache. **Always use `.equals()`** for wrapper equality.

## The NullPointerException Trap
```java
Map<String,Integer> m = new HashMap<>();
int x = m.get("missing");   // NPE: unboxing null Integer
```

## Performance Trap
```java
Long sum = 0L;                       // WRONG: boxes on every iteration
for (long i = 0; i < 1_000_000; i++) sum += i;   // ~1M allocations
```
Use the primitive `long` instead.

## Best Practices
- Compare wrappers with `.equals()`, never `==`.
- Watch for unboxing `null` (map misses, nullable columns).
- Avoid autoboxing in loops and hot paths; use primitives / primitive streams.

## Interview Questions
- **Why can `Integer == Integer` be surprising?** Values -128..127 are cached and share references; larger values are distinct objects.
- **When does autoboxing throw NPE?** Unboxing a `null` wrapper (e.g., a missing map value into an `int`).
- **Performance concern?** Autoboxing in loops allocates many wrapper objects and pressures the GC.

## Related Topics
- [[Wrapper Classes]] · [[Collections Framework]]

## Quick Revision
- Auto primitive<->wrapper conversion via valueOf/intValue. Traps: `==` (Integer cache -128..127), NPE unboxing null, boxing in loops. Use equals + primitives.
