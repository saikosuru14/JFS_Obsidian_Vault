---
title: Composition vs Inheritance
aliases:
  - Composition vs Inheritance
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 6
tags:
  - computer-science
  - oop
related:
  - "[[Inheritance]]"
  - "[[Association Aggregation Composition]]"
  - "[[Object-Oriented Programming]]"
---

# Composition vs Inheritance

## The Core Idea
- **Inheritance** models **is-a** (`Car is-a Vehicle`) and reuses behavior via `extends`.
- **Composition** models **has-a** (`Car has-a Engine`) by holding references to other objects and delegating to them.

> "Favor composition over inheritance." — *Design Patterns* (Gang of Four)

## Inheritance Example
```java
class Engine { void start() {} }
class Car extends Engine {}   // WRONG: a Car is not an Engine
```

## Composition Example
```java
class Engine { void start() { /* ... */ } }

class Car {
    private final Engine engine = new Engine();   // has-a
    void start() { engine.start(); }              // delegate
}
```

## Why Prefer Composition
| Concern | Inheritance | Composition |
|---------|-------------|-------------|
| Coupling | Tight (to parent internals) | Loose |
| Flexibility | Fixed at compile time | Swap parts at runtime |
| Encapsulation | Can leak parent details | Preserved |
| Fragile base class | Yes | No |
| Multiple behaviors | Limited (single inheritance) | Combine many objects |

## When Inheritance Is Still Right
- A true, stable **is-a** relationship.
- You need polymorphic substitution (Liskov).
- The base class is designed and documented for extension.

## Interview Questions
- Why favor composition over inheritance?
- What is the "fragile base class" problem?
- Give an example where inheritance is the correct choice.

## Related Notes
- [[Inheritance]]
- [[Association Aggregation Composition]]
- [[SOLID Principles]]

## Revision Summary
- is-a → inheritance; has-a → composition.
- Composition = looser coupling and runtime flexibility; prefer it by default.
