---
title: Interface Segregation Principle
aliases:
  - Interface Segregation Principle
  - ISP
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - computer-science
  - solid
related:
  - "[[SOLID Principles]]"
  - "[[Abstraction]]"
---

# Interface Segregation Principle (ISP)

## Definition
No client should be forced to depend on methods it does not use. Prefer **many small, focused interfaces** over one large "fat" interface.

## Violation
```java
interface Worker {
    void work();
    void eat();
}
class Robot implements Worker {
    public void work() {}
    public void eat() { throw new UnsupportedOperationException(); } // robots don't eat
}
```

## Fix — Split Interfaces
```java
interface Workable { void work(); }
interface Eatable { void eat(); }

class Robot implements Workable { public void work() {} }
class Human implements Workable, Eatable { public void work() {} public void eat() {} }
```

## Benefits
- Clients depend only on what they need.
- Reduces the impact of changes and avoids empty/`UnsupportedOperation` implementations.

## Interview Questions
- What is a "fat" interface and why is it a problem?
- How does ISP relate to SRP?

## Related Notes
- [[SOLID Principles]]
- [[Abstraction]]

## Revision Summary
- Split large interfaces so clients depend only on methods they use.
