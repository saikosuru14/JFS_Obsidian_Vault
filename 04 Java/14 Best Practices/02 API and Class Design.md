---
title: API and Class Design
aliases:
  - API and Class Design
domain: Java
module: Best Practices
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 2
tags:
  - java
  - best-practices
related:
  - "[[Coding Best Practices]]"
  - "[[SOLID Principles]]"
---

# API and Class Design

## Overview
Designing classes and public APIs that are hard to misuse and easy to evolve.

## Principles
- **Minimize accessibility** — make classes and members as private as possible; expose the smallest surface.
- **Make classes immutable** unless there's a reason not to.
- **Design for extension or prohibit it** — document and design for subclassing, or make the class `final`.
- **Favor static factory methods** over constructors when naming/ caching / return-type flexibility helps (`List.of`, `Optional.of`).
- **Use the Builder** for objects with many optional parameters.
- **Return empty, never null** for collections/arrays; `Optional` for scalar absence.
- **Keep methods focused** (Single Responsibility) — see [[SOLID Principles]].
- **Prefer unchecked exceptions** for API errors; document all thrown exceptions.

## Evolving APIs
- Adding to an interface breaks implementers — use `default` methods deliberately.
- Don't change published method semantics; deprecate, then remove.

## Common Mistakes
- Long constructors with many params (use Builder).
- Leaking mutable internals; exposing implementation types in signatures.
- Boolean parameters that obscure call sites (`create(true, false)`).

## Interview Questions
- Static factory vs constructor — trade-offs?
- When do you use the Builder pattern?
- How do you evolve an interface without breaking callers?

## Related Topics
- [[Coding Best Practices]] · [[SOLID Principles]] · [[Design Patterns Overview]]

## Quick Revision
- Minimal surface, immutable, final-or-designed-for-extension, factories/builders, return empty not null, document exceptions.
