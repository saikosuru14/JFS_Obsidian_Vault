---
title: Encapsulation
aliases:
  - Encapsulation
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - computer-science
  - oop
related:
  - "[[Object-Oriented Programming]]"
  - "[[Abstraction]]"
---

# Encapsulation

## Definition
**Encapsulation** bundles data (fields) and the methods that operate on that data into a single unit (the class), while **hiding internal state** behind a controlled public interface.

## How It Works
- Mark fields `private`.
- Expose access through `public` getters/setters or behavior methods.
- Validate and protect invariants inside the class.

```java
class Account {
    private double balance;   // hidden state

    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("amount must be positive");
        balance += amount;
    }

    public double getBalance() {   // controlled read access
        return balance;
    }
}
```

The caller cannot set `balance` directly to an invalid value; the class enforces its own rules.

## Benefits
- **Data protection** – invariants can't be broken from outside.
- **Maintainability** – internal representation can change without breaking callers.
- **Loose coupling** – callers depend on the interface, not the implementation.
- **Testability** – behavior is centralized and easy to verify.

## Encapsulation vs Abstraction
- **Encapsulation** = hiding *state* (the "how it's stored").
- **Abstraction** = hiding *implementation* behind a simpler interface (the "what it does").
They are complementary, not the same.

## Interview Questions
- What problem does encapsulation solve?
- Difference between encapsulation and abstraction?
- Why expose behavior methods instead of public fields?

## Related Notes
- [[Object-Oriented Programming]]
- [[Abstraction]]

## Revision Summary
- Private state + public controlled access.
- Protects invariants and enables change without breaking callers.
