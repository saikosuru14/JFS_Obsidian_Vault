---
title: Generics Index
aliases:
  - Generics Index
domain: Java
module: Generics
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - java
  - index
related:
  - "[[Java Index|Java]]"
  - "[[Generics]]"
---

# Generics

> Module index - part of the [[Java Index|Java]] learning path.

## Overview
Generics add compile-time type parameters to classes, interfaces, and methods, giving type safety and removing casts. The catch is **type erasure**: generics exist only at compile time, which explains most of their quirks (`instanceof`, arrays, overloading). **Wildcards** (`? extends` / `? super`) control API flexibility.

## Branch (expand)
- **[[Generics]]** — the hub: type parameters, bounded types, generic methods.
  - [[Type Erasure]] — why generics vanish at runtime and what breaks.
  - [[Wildcards]] — `?`, `extends`, `super`, and the PECS rule.

## Learning Roadmap
1. [[Generics]]
2. [[Type Erasure]]
3. [[Wildcards]]

## Prerequisites
- [[Exception Handling Index|Exception Handling]]

## Next
- [[Functional Programming Index|Functional Programming]]

## Related Modules
- [[Java Index|Java]] · [[Collections Framework]]

## Quick Revision
- Compile-time type safety + no casts. Erased at runtime (no `new T[]`, limited `instanceof`). Wildcards + PECS for flexible APIs.
