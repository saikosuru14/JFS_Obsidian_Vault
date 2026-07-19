---
title: Liskov Substitution Principle
aliases:
  - Liskov Substitution Principle
  - LSP
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - computer-science
  - solid
related:
  - "[[SOLID Principles]]"
  - "[[Inheritance]]"
---

# Liskov Substitution Principle (LSP)

## Definition
Objects of a subclass must be **substitutable** for objects of their base class without breaking correctness. A subtype must honor the contract of its supertype.

## Classic Violation
```java
class Rectangle { void setWidth(int w){} void setHeight(int h){} }
class Square extends Rectangle {
    // forcing width == height breaks code that sets them independently
}
```
Code that works with `Rectangle` breaks when given a `Square`.

## Signs of a Violation
- Overridden methods that throw `UnsupportedOperationException`.
- Subclasses that strengthen preconditions or weaken postconditions.
- Type checks (`instanceof`) to special-case a subtype.

## Fix
- Model with correct abstractions (e.g., an immutable `Shape` with `area()` instead of Square extends Rectangle).
- Favor composition when an is-a relationship doesn't truly hold.

## Interview Questions
- Explain the Rectangle/Square problem.
- How does LSP relate to inheritance and polymorphism?

## Related Notes
- [[SOLID Principles]]
- [[Inheritance]]

## Revision Summary
- Subtypes must be usable anywhere the base type is, honoring its contract.
