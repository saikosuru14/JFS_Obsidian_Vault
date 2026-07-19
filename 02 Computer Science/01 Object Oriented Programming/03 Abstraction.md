---
title: Abstraction
aliases:
  - Abstraction
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - computer-science
  - oop
related:
  - "[[Object-Oriented Programming]]"
  - "[[Encapsulation]]"
  - "[[Polymorphism]]"
---

# Abstraction

## Definition
**Abstraction** exposes only the essential behavior of an object while hiding the implementation details. Callers work with *what* something does, not *how* it does it.

## How It Works in Java
- **Interfaces** define a contract with no implementation.
- **Abstract classes** provide partial implementation plus abstract methods.

```java
interface PaymentGateway {
    void pay(double amount);   // what, not how
}

class StripeGateway implements PaymentGateway {
    public void pay(double amount) {
        // Stripe-specific implementation hidden from the caller
    }
}

PaymentGateway gateway = new StripeGateway();
gateway.pay(100);   // caller only knows the contract
```

## Interface vs Abstract Class
| | Interface | Abstract Class |
|---|-----------|----------------|
| Multiple inheritance | Yes | No |
| State (fields) | Constants only | Yes |
| Constructors | No | Yes |
| Use when | Defining a capability/contract | Sharing common base behavior |

## Why It Matters
- Reduces complexity by hiding detail.
- Enables swapping implementations (Stripe → PayPal) without changing callers.
- Foundation for **polymorphism** and **dependency inversion** (Spring DI).

## Interview Questions
- Abstraction vs encapsulation?
- When would you use an abstract class over an interface?
- How does abstraction enable loose coupling?

## Related Notes
- [[Object-Oriented Programming]]
- [[Encapsulation]]
- [[Polymorphism]]
- [[SOLID Principles]]

## Revision Summary
- Hide implementation, expose a contract.
- Interfaces for capabilities, abstract classes for shared base behavior.
