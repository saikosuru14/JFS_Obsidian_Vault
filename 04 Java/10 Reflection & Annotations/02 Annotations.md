---
title: Annotations
aliases:
  - Annotations
domain: Java
module: "Reflection & Annotations"
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Reflection]]"
---

# Annotations

## Overview
Annotations attach **metadata** to code (classes, methods, fields, parameters). They don't change behavior by themselves — a processor reads them at compile time or runtime (via [[Reflection]]) and acts on them.

## Why It Matters
They replaced XML config across the ecosystem. Every Spring/JPA/JUnit app is driven by annotations, and interviewers ask about retention policies and custom annotations.

## Built-in & Meta-Annotations
- **Standard**: `@Override`, `@Deprecated`, `@SuppressWarnings`, `@FunctionalInterface`, `@SafeVarargs`.
- **Meta-annotations** (annotate annotations): `@Retention`, `@Target`, `@Documented`, `@Inherited`, `@Repeatable`.

## Retention Policies (key concept)
| Policy | Kept until | Example |
|--------|-----------|---------|
| `SOURCE` | discarded after compile | `@Override`, Lombok |
| `CLASS` | in `.class`, not at runtime (default) | bytecode tools |
| `RUNTIME` | available via reflection | Spring/JPA/JUnit |
Only `RUNTIME` annotations are visible to reflection — the most common gotcha.

## Custom Annotation
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Audited {
    String value() default "";
}

// read it
Method m = ...;
if (m.isAnnotationPresent(Audited.class)) {
    String v = m.getAnnotation(Audited.class).value();
}
```

## How Frameworks Use Them
- **Runtime** (Spring `@Autowired`, JPA `@Entity`): reflection scans and reacts at startup.
- **Compile-time** (annotation processors: Lombok, MapStruct, Dagger): generate code during compilation — no runtime cost.

## Interview Questions
- **What are the retention policies and which is refl-visible?** SOURCE, CLASS, RUNTIME — only RUNTIME is visible via reflection.
- **Do annotations change behavior?** No — they're metadata; a processor/framework interprets them.
- **How do you create a custom annotation?** `@interface` with `@Retention`/`@Target`, then read via reflection or an annotation processor.
- **Runtime vs compile-time processing?** Reflection at startup vs codegen during compilation (faster, no runtime overhead).

## Related Topics
- [[Reflection]] · [[Functional Interfaces]]

## Quick Revision
- Metadata read by reflection/processors. Retention SOURCE/CLASS/RUNTIME (only RUNTIME is reflective). Custom via `@interface` + `@Retention`/`@Target`. Basis of Spring/JPA/JUnit.
