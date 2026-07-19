---
title: Dependency Inversion Principle
aliases:
  - Dependency Inversion Principle
  - DIP
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 5
tags:
  - computer-science
  - solid
related:
  - "[[SOLID Principles]]"
  - "[[Dependency Injection]]"
  - "[[Spring IoC]]"
---

# Dependency Inversion Principle (DIP)

## Definition
- High-level modules should not depend on low-level modules. Both should depend on **abstractions**.
- Abstractions should not depend on details; details should depend on abstractions.

## Violation
```java
class MySQLRepository {}
class OrderService {
    private final MySQLRepository repo = new MySQLRepository(); // tied to a concretion
}
```

## Fix — Depend on an Abstraction
```java
interface OrderRepository {}
class MySQLRepository implements OrderRepository {}

class OrderService {
    private final OrderRepository repo;          // depends on abstraction
    OrderService(OrderRepository repo) { this.repo = repo; }  // injected
}
```

## Relationship to Spring
Spring's **[[Dependency Injection]]** and IoC container are a direct application of DIP: high-level services receive abstractions (interfaces) that the container wires at runtime.

## Benefits
- Swap implementations (MySQL → Mongo) without touching high-level logic.
- Easy mocking for tests.

## Interview Questions
- Difference between dependency inversion and dependency injection?
- How does Spring implement DIP?

## Related Notes
- [[SOLID Principles]]
- [[Dependency Injection]]
- [[Spring IoC]]

## Revision Summary
- Depend on abstractions, not concretions. Inject implementations. Basis of Spring DI.
