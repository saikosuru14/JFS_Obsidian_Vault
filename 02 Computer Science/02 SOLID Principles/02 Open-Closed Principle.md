---
title: Open-Closed Principle
aliases:
  - Open-Closed Principle
  - OCP
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - computer-science
  - solid
related:
  - "[[SOLID Principles]]"
  - "[[Polymorphism]]"
---

# Open-Closed Principle (OCP)

## Definition
Software entities should be **open for extension but closed for modification**. Add new behavior by adding new code, not by editing existing, tested code.

## Violation
```java
double area(Object shape) {
    if (shape instanceof Circle) { /* ... */ }
    else if (shape instanceof Square) { /* ... */ }
    // adding a new shape forces editing this method
}
```

## Fix — Extend via Abstraction
```java
interface Shape { double area(); }
class Circle implements Shape { public double area() { return 0; } }
class Square implements Shape { public double area() { return 0; } }
// new shapes = new classes, no changes to existing code
```

## How to Achieve It
- Program to interfaces/abstract classes.
- Use polymorphism and the Strategy pattern.

## Benefits
- Existing code stays stable; less regression risk.

## Interview Questions
- How do you make code open for extension but closed for modification?
- Which design patterns support OCP?

## Related Notes
- [[SOLID Principles]]
- [[Polymorphism]]

## Revision Summary
- Extend behavior with new types, don't modify existing code. Enabled by polymorphism.
