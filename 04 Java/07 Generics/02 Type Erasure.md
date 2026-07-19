---
title: Type Erasure
aliases:
  - Type Erasure
domain: Java
module: Generics
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Generics]]"
---

# Type Erasure

## Overview
Java generics are a **compile-time** feature. The compiler checks types, then **erases** type parameters, replacing them with their bounds (or `Object`) and inserting casts. At runtime `List<String>` and `List<Integer>` are both just `List`.

## Why It Matters
Erasure was chosen for **backward compatibility** with pre-generics code. It explains a whole family of "why can't I..." limitations that show up constantly in interviews.

## What Erasure Does
```java
// You write:
class Box<T extends Number> { T value; }
// Compiler produces (roughly):
class Box { Number value; }   // T -> its bound (Number), or Object if unbounded
```

## Consequences (the gotchas)
- **No `new T()` / `new T[]`** — the type isn't known at runtime.
- **`instanceof List<String>` is illegal** — only `instanceof List<?>` works.
- **No generic overloading clash** — `foo(List<String>)` and `foo(List<Integer>)` have the same erased signature.
- **Can't have `catch (MyException<T>)`** — exceptions are runtime types.
- **Static fields are shared** across all parameterizations.
- **Unchecked warnings** appear where the compiler can't verify a cast.

## Getting Type Info Back
- Pass a `Class<T>` token (`Class<T> type`) for reflective operations.
- Use super-type tokens (`TypeReference`, as in Jackson) to capture generic types via anonymous subclasses.
- Reifiable arrays: use `Array.newInstance(clazz, n)`.

## Interview Questions
- **What is type erasure?** The compiler removes generic type parameters after checking, replacing them with bounds/Object plus casts.
- **Why can't you do `new T[]`?** The runtime doesn't know T; arrays are reified and need a real type.
- **Why doesn't `instanceof List<String>` compile?** Runtime has no `<String>` info — only the raw `List` exists.
- **Why was erasure chosen?** Backward compatibility with legacy non-generic bytecode.

## Related Topics
- [[Generics]] · [[Wildcards]] · [[Reflection]]

## Quick Revision
- Generics erased after compile: T -> bound/Object + casts. No `new T[]`, no `instanceof List<String>`, no generic overloading, shared statics. Use Class<T> tokens to recover type.
