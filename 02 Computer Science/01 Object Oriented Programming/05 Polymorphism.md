---
title: Polymorphism
aliases:
  - Polymorphism
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 5
tags:
  - computer-science
  - oop
related:
  - "[[Object-Oriented Programming]]"
  - "[[Inheritance]]"
  - "[[Abstraction]]"
---

# Polymorphism

## Definition
**Polymorphism** ("many forms") lets the same interface or method call behave differently depending on the underlying object type. Code written against an abstraction works with any implementation.

## Two Kinds

### Compile-time (Static) — Overloading
Same method name, different parameter lists. Resolved by the compiler.
```java
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
```

### Runtime (Dynamic) — Overriding
A subclass overrides a parent method; the actual method runs based on the object's real type at runtime (dynamic dispatch).
```java
class Shape { double area() { return 0; } }
class Circle extends Shape { double area() { return 3.14 * r * r; } }

Shape s = new Circle();
s.area();   // Circle.area() runs at runtime
```

## Overloading vs Overriding
| | Overloading | Overriding |
|---|-------------|-----------|
| Binding | Compile-time | Runtime |
| Signature | Must differ | Must match |
| Inheritance | Not required | Required |
| Return type | Can differ | Same/covariant |

## Why It Matters
- Write flexible code against interfaces (`List`, `PaymentGateway`).
- Foundation for the **Open/Closed Principle** and most design patterns.

## Interview Questions
- Difference between compile-time and runtime polymorphism?
- What is dynamic method dispatch?
- Can you override a static or private method? (No — they're not polymorphic.)

## Related Notes
- [[Object-Oriented Programming]]
- [[Inheritance]]
- [[Abstraction]]
- [[SOLID Principles]]

## Revision Summary
- Overloading = compile-time; overriding = runtime dispatch.
- Enables coding to abstractions and the Open/Closed Principle.
