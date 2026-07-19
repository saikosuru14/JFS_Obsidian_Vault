---
title: Association Aggregation Composition
aliases:
  - Association Aggregation Composition
domain: Computer Science
module: Object Oriented Programming
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 7
tags:
  - computer-science
  - oop
related:
  - "[[Composition vs Inheritance]]"
  - "[[Object-Oriented Programming]]"
---

# Association, Aggregation, Composition

These describe **how objects relate** to one another, from weakest to strongest coupling.

## Association
A general "uses-a" relationship between independent objects. Neither owns the other.
```java
class Teacher {}
class Student { void learnFrom(Teacher t) {} }   // a Student uses a Teacher
```
- Lifetimes are independent.

## Aggregation ("has-a", weak ownership)
A whole–part relationship where the part can exist without the whole.
```java
class Department {
    private List<Professor> professors;   // department HAS professors
}
```
- If the `Department` is deleted, the `Professor` objects can still exist elsewhere.

## Composition ("owns-a", strong ownership)
A whole–part relationship where the part **cannot** exist without the whole.
```java
class House {
    private final Room room = new Room();   // Room's lifetime is tied to House
}
```
- Destroying the `House` destroys its `Room`s.

## Comparison
| Relationship | Meaning | Ownership | Lifetime |
|--------------|---------|-----------|----------|
| Association | uses-a | none | independent |
| Aggregation | has-a | weak | part survives whole |
| Composition | owns-a | strong | part dies with whole |

## UML Notation
- Association → plain line
- Aggregation → hollow diamond at the whole
- Composition → filled diamond at the whole

## Interview Questions
- Difference between aggregation and composition?
- Give a real example of each relationship.
- How are these shown in a UML class diagram?

## Related Notes
- [[Composition vs Inheritance]]
- [[Object-Oriented Programming]]
- [[UML Class Diagrams]]

## Revision Summary
- Association (uses-a) < Aggregation (has-a, weak) < Composition (owns-a, strong).
- Composition ties the part's lifetime to the whole.
