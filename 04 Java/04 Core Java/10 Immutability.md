---
title: Immutability
aliases:
  - Immutability
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 10
tags:
  - java
  - core
related:
  - "[[String]]"
  - "[[Object Class]]"
---

# Immutability

## Overview
An immutable object's state cannot change after construction. Immutability is the simplest path to thread safety and predictable code.

## How To Make a Class Immutable
1. `final` class (or all-final via other means).
2. All fields `private final`.
3. No setters; set state only in the constructor.
4. Defensive-copy mutable inputs in, and mutable outputs out.
5. Don't leak `this` during construction.

```java
public final class Money {
    private final long cents;
    private final String currency;
    public Money(long cents, String currency) { this.cents = cents; this.currency = currency; }
    public Money add(Money o) { return new Money(cents + o.cents, currency); } // returns new instance
}
```
`record Money(long cents, String currency) {}` gives most of this for free.

## Why It Matters
- Thread-safe with no locking; safe to share and cache.
- Valid as [[HashMap]] keys (stable hash).
- Easier reasoning; no aliasing surprises.

## Common Mistakes
- Storing a mutable collection/array reference without defensive copies.
- Exposing internal mutable state via getters.

## Interview Questions
- How do you design an immutable class?
- Why are immutable objects thread-safe?
- Role of defensive copying?

## Related Topics
- [[String]] · [[clone()]] · [[Coding Best Practices]]

## Quick Revision
- final class, final private fields, no setters, defensive copies. Thread-safe, cacheable, safe map keys. Records help.
