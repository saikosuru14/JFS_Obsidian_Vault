---
title: Generics
aliases:
  - Generics
domain: Java
module: Generics
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Generics Index|Generics]]"
  - "[[Type Erasure]]"
  - "[[Wildcards]]"
---

# Generics

## Overview
Generics parameterize types, letting a class or method work over many types while keeping compile-time type safety. `List<String>` guarantees only strings go in and come out — no casts, no `ClassCastException` at runtime.

## Why It Matters
They move type errors from runtime to compile time and make APIs self-documenting. Every collection, `Optional`, `CompletableFuture`, and stream is generic.

## Forms
```java
// Generic class
class Box<T> { private T value; T get() { return value; } }

// Bounded type parameter (T must be Comparable)
<T extends Comparable<T>> T max(List<T> list) { ... }

// Multiple bounds
<T extends Number & Comparable<T>> ...

// Generic method (independent of the class's type params)
static <T> List<T> singleton(T item) { ... }
```

## Bounded Type Parameters
- `<T extends Number>` — upper bound; T is a Number or subtype, so you can call Number methods.
- Enables generic algorithms (`max`, `sort`) that need capabilities from the bound.

## Type Inference
The diamond `<>` and method inference reduce noise: `var list = new ArrayList<String>();`, `List.of(1, 2, 3)`.

## Best Practices
- Prefer generic types/methods over raw types (`List` without a parameter) — raw types disable type checking.
- Use bounded parameters when the algorithm needs specific behavior.
- See [[Wildcards]] (PECS) for flexible parameter types.

## Common Mistakes
- Using **raw types** (`List list`) — loses safety and triggers unchecked warnings.
- Expecting generic type info at runtime (it's erased — see [[Type Erasure]]).

## Interview Questions
- **Why generics?** Compile-time type safety and elimination of casts; reusable, self-documenting APIs.
- **Generic method vs generic class?** A generic method declares its own type parameter, independent of any class-level parameter.
- **What's a bounded type parameter?** `<T extends X>` restricts T and grants access to X's members.

## Related Topics
- [[Type Erasure]] · [[Wildcards]] · [[Collections Framework]]

## Quick Revision
- Parameterized types = compile-time safety + no casts. Bounded params (`extends`) for capability. Avoid raw types. Erased at runtime.
