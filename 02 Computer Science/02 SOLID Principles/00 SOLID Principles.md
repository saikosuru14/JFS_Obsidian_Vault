---
title: SOLID Principles
aliases:
  - SOLID Principles
  - SOLID
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - computer-science
  - solid
  - index
related:
  - "[[Object-Oriented Programming]]"
  - "[[Design Patterns Overview]]"
---

# SOLID Principles

> Module index — five object-oriented design principles for maintainable, extensible code.

## Overview
SOLID is a set of five principles (Robert C. Martin) that reduce coupling, improve cohesion, and make code easier to change and test.

## The Five Principles
1. [[Single Responsibility Principle]] — one reason to change.
2. [[Open-Closed Principle]] — open for extension, closed for modification.
3. [[Liskov Substitution Principle]] — subtypes must be substitutable for their base types.
4. [[Interface Segregation Principle]] — prefer small, focused interfaces.
5. [[Dependency Inversion Principle]] — depend on abstractions, not concretions.

## Why It Matters
- Localizes change and reduces ripple effects.
- Enables testing through abstractions and mocks.
- Underpins most [[Design Patterns Overview|design patterns]] and frameworks like Spring (DIP via dependency injection).

## Interview Questions
- Explain each SOLID principle with an example.
- How does Spring's dependency injection relate to DIP?
- Give a real Single Responsibility violation and how to fix it.

## Revision Summary
- S O L I D = SRP, OCP, LSP, ISP, DIP.
- Goal: low coupling, high cohesion, easy change.
