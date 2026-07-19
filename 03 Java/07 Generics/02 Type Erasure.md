---
title: Type Erasure
aliases:
  - Type Erasure
domain: Java
module: Generics
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
---

# Type Erasure

Generic type information is removed during compilation.

Example:
List<String> and List<Integer> become List at runtime.

Interview:
- Why can't you create T[]?
- Why doesn't instanceof work with generic types?
