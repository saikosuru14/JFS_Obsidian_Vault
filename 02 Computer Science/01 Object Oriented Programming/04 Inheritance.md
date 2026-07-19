---
title: Inheritance
aliases:
  - Inheritance
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - computer-science
  - oop
related:
  - "[[Object-Oriented Programming]]"
  - "[[Polymorphism]]"
  - "[[Composition vs Inheritance]]"
---

# Inheritance

## Definition
**Inheritance** lets a class (subclass/child) acquire the fields and methods of another class (superclass/parent), modeling an **"is-a"** relationship and enabling code reuse.

```java
class Animal {
    void eat() { System.out.println("eating"); }
}

class Dog extends Animal {   // Dog IS-A Animal
    void bark() { System.out.println("barking"); }
}

Dog d = new Dog();
d.eat();   // inherited
d.bark();  // own
```

## Types of Inheritance
- **Single** – one parent (`Dog extends Animal`).
- **Multilevel** – chain (`Puppy extends Dog extends Animal`).
- **Hierarchical** – many children share one parent.
- **Multiple** – Java does **not** support multiple class inheritance (diamond problem), but a class can implement multiple interfaces.

## `super` Keyword
- `super()` calls the parent constructor.
- `super.method()` calls the parent's version of an overridden method.

## Method Overriding
A subclass redefines an inherited method with the same signature. This is the basis of runtime **polymorphism**.

## When to Use / Avoid
- Use when there is a genuine **is-a** relationship and shared behavior.
- Avoid deep hierarchies; prefer **composition** for "has-a" relationships to reduce coupling.

## Interview Questions
- Why does Java not support multiple class inheritance?
- Difference between overriding and overloading?
- What does `super` do?
- When would you prefer composition over inheritance?

## Related Notes
- [[Object-Oriented Programming]]
- [[Polymorphism]]
- [[Composition vs Inheritance]]

## Revision Summary
- "is-a" relationship + code reuse via `extends`.
- Java: single class inheritance, multiple interface inheritance.
- Overriding enables runtime polymorphism.
