---
title: Reflection
aliases:
  - Reflection
domain: Java
module: "Reflection & Annotations"
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Reflection & Annotations Index|Reflection & Annotations]]"
  - "[[Annotations]]"
---

# Reflection

## Overview
Reflection (`java.lang.reflect`) lets code inspect and manipulate classes, methods, fields, and constructors at **runtime** — reading metadata, creating instances, and invoking members without knowing them at compile time.

## Why It Matters
It's the engine behind frameworks: Spring's dependency injection, Hibernate's entity mapping, Jackson's (de)serialization, and JUnit's test discovery all use reflection + [[Annotations]]. You rarely write it directly, but you must understand its cost and risks.

## Core API
```java
Class<?> c = Class.forName("com.example.User");     // or user.getClass() / User.class
Object obj = c.getDeclaredConstructor().newInstance();

Method m = c.getDeclaredMethod("setName", String.class);
m.setAccessible(true);                                // bypass access checks
m.invoke(obj, "Alice");

Field f = c.getDeclaredField("id");
f.setAccessible(true);
f.set(obj, 42);
```

## Trade-offs
- **Slower** — dynamic dispatch and access checks; JIT can't optimize as well (though modern JVMs cache/inline hot reflective calls).
- **Breaks encapsulation** — `setAccessible(true)` reaches private members (restricted by the module system / strong encapsulation since Java 9+).
- **No compile-time safety** — errors surface at runtime (`NoSuchMethodException`, `IllegalAccessException`).
- **Refactor-fragile** — string-based names don't get renamed by IDEs.

## When to Use
- Building frameworks/libraries, plugin systems, generic serializers, or test tooling.
- Avoid in ordinary application logic — prefer interfaces/polymorphism.

## Modern Alternatives
`MethodHandles`/`VarHandle` (faster, type-safe) and annotation processing / codegen (compile-time) reduce the need for runtime reflection.

## Interview Questions
- **What is reflection used for?** Runtime inspection and dynamic invocation — the basis of DI, ORM, serialization, testing frameworks.
- **Downsides?** Performance overhead, broken encapsulation, no compile-time checks, refactor fragility.
- **How do frameworks use it?** Scan for annotated classes/fields, instantiate beans, inject dependencies, map columns.
- **Alternative to reflection?** MethodHandles/VarHandle or compile-time annotation processing.

## Related Topics
- [[Annotations]] · [[Type Erasure]] · [[Class Loading]]

## Quick Revision
- Runtime introspection/invocation via `java.lang.reflect`. Powers Spring/Hibernate/Jackson/JUnit with annotations. Slower, breaks encapsulation, no compile-time safety. Prefer MethodHandles/codegen where possible.
