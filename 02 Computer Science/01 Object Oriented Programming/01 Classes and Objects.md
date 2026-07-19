---
title: Classes and Objects
aliases:
  - Classes and Objects
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - computer-science
  - oop
related:
  - "[[Object-Oriented Programming]]"
  - "[[Encapsulation]]"
  - "[[Inheritance]]"
---

# Classes and Objects

## Definition
A **class** is a blueprint that defines the state (fields) and behavior (methods) of a type. An **object** is a concrete instance of a class, created at runtime and living on the heap.

```java
class Account {
    private String owner;      // field (state)
    private double balance;    // field (state)

    Account(String owner) {    // constructor
        this.owner = owner;
    }

    void deposit(double amount) {   // method (behavior)
        balance += amount;
    }
}

Account a = new Account("Alice");   // 'a' is an object (instance)
```

## Class Members
- **Fields** hold the object's state.
- **Methods** define behavior operating on that state.
- **Constructors** initialize a new object.
- **Static members** belong to the class itself, shared across all instances.

## Object Creation
1. `new` allocates memory on the heap.
2. Fields are set to default values, then the constructor runs.
3. A reference to the object is returned and stored in a variable.

```
Reference (stack) ──▶ Object (heap)
        a                { owner, balance }
```

## Class vs Object
| Class | Object |
|-------|--------|
| Blueprint / template | Instance of a class |
| Defined once | Created many times |
| No memory until instantiated | Occupies heap memory |

## Interview Questions
- What is the difference between a class and an object?
- Where do objects live in memory? Where do references live?
- What is the difference between an instance member and a static member?

## Related Notes
- [[Object-Oriented Programming]]
- [[Encapsulation]]
- [[Object Lifecycle]]

## Revision Summary
- Class = blueprint, object = instance.
- Objects live on the heap, references on the stack.
- Constructors initialize state; static members are shared.
