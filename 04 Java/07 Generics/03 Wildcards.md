---
title: Wildcards
aliases:
  - Wildcards
domain: Java
module: Generics
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[Generics]]"
---

# Wildcards

## Overview
Wildcards (`?`) express **unknown** type arguments, letting APIs accept a family of parameterized types. Bounded wildcards (`? extends T`, `? super T`) trade what you can read vs write for flexibility.

## Why It Matters
Generics are **invariant**: `List<Integer>` is *not* a `List<Number>`. Wildcards restore the flexibility you'd otherwise lose, and PECS is a guaranteed interview question.

## The Three Forms
```java
List<?>            // unbounded: unknown type; read as Object, can't add (except null)
List<? extends Number>  // upper-bounded: read Number; producer (can't add)
List<? super Integer>   // lower-bounded: write Integer; consumer (read as Object)
```

## PECS - Producer Extends, Consumer Super
- **Producer** (you read T out) -> `? extends T`.
- **Consumer** (you write T in) -> `? super T`.
```java
// Copies from a producer (src) into a consumer (dest)
static <T> void copy(List<? extends T> src, List<? super T> dest) {
    for (T t : src) dest.add(t);
}
```
`Collections.copy` and `Stream`/`Collectors` signatures follow exactly this.

## Why extends can't add
With `List<? extends Number>` the compiler only knows the element is *some* subtype of Number — it can't verify that an `Integer` you add is the right subtype, so adds are rejected (except `null`).

## Interview Questions
- **What is PECS?** Producer Extends, Consumer Super — use `extends` when reading from a structure, `super` when writing to it.
- **Why can't you add to a `List<? extends Number>`?** The exact element type is unknown, so no value is provably type-safe to add.
- **Are generics covariant?** No — invariant; wildcards add controlled covariance/contravariance.
- **`List<?>` vs `List<Object>`?** `List<?>` accepts any parameterization but is read-only; `List<Object>` only accepts a list declared with `Object`.

## Related Topics
- [[Generics]] · [[Type Erasure]] · [[Collections Framework]]

## Quick Revision
- `?` = unknown type. `? extends T` produce/read, `? super T` consume/write (PECS). Generics are invariant; wildcards add flexibility. `extends` lists are read-only.
