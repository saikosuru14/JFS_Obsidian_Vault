---
title: Coding Best Practices
aliases:
  - Coding Best Practices
domain: Java
module: Best Practices
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
  - best-practices
related:
  - "[[API and Class Design]]"
  - "[[Immutability]]"
---

# Coding Best Practices

## Overview
High-leverage Java coding rules (Effective Java distilled) for day-to-day engineering.

## Rules
- **Prefer immutability** — final fields, no setters; simpler reasoning and thread safety. See [[Immutability]].
- **Program to interfaces**, not implementations (`List` not `ArrayList` in signatures).
- **Favor composition over inheritance**; use inheritance only for true is-a.
- **Use `Optional` for return values** that may be absent — never for fields or parameters. See [[Optional]].
- **Validate arguments early**; fail fast with `IllegalArgumentException`/`Objects.requireNonNull`.
- **Respect the `equals`/`hashCode` contract** together. See [[equals() vs ==]], [[hashCode()]].
- **Prefer enums** over int constants; use `EnumMap`/`EnumSet`.
- **Minimize mutability and scope** — smallest visibility, narrowest type.
- **Use `var`** for obvious local types; keep it readable.
- **Avoid premature optimization** — measure (see [[Performance Profiling]]).

## Common Mistakes
- Returning `null` collections instead of empty ones.
- Public mutable fields; leaking internal collections (return copies/unmodifiable views).
- Overriding `equals` without `hashCode`.

## Interview Questions
- Why favor composition over inheritance?
- When is `Optional` appropriate?
- Why program to interfaces?

## Related Topics
- [[API and Class Design]] · [[Immutability]] · [[Optional]]

## Quick Revision
- Immutable, interface-typed, composed, validated-early, correct equals/hashCode, enums over ints, measure before optimizing.
