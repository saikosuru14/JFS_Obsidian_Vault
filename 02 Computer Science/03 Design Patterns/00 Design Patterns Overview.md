---
title: Design Patterns Overview
aliases:
  - Design Patterns Overview
  - Design Patterns
domain: Computer Science
module: Design Patterns
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - computer-science
  - design-patterns
  - index
related:
  - "[[SOLID Principles]]"
  - "[[Object-Oriented Programming]]"
---

# Design Patterns Overview

> Module index — reusable, proven solutions to recurring design problems.

## The Three Categories

### Creational — how objects are created
- **Singleton** — a single shared instance (Spring beans are singletons by default).
- **Factory Method / Abstract Factory** — create objects without exposing concretions.
- **Builder** — construct complex objects step by step.
- **Prototype** — clone existing objects.

### Structural — how objects are composed
- **Adapter** — bridge incompatible interfaces.
- **Decorator** — add behavior without subclassing.
- **Proxy** — a stand-in controlling access (Spring AOP uses proxies).
- **Facade** — a simple interface over a complex subsystem.
- **Composite** — treat individual and grouped objects uniformly.

### Behavioral — how objects interact
- **Strategy** — swap algorithms at runtime.
- **Observer** — publish/subscribe notifications (events).
- **Template Method** — fixed skeleton, overridable steps.
- **Command** — encapsulate a request as an object.
- **Chain of Responsibility** — pass a request along handlers (filter chains).

## Patterns in Spring
Spring relies heavily on **Factory** (bean factory), **Proxy** (AOP, transactions), **Singleton** (default bean scope), **Template Method** (`JdbcTemplate`, `RestTemplate`), and **Strategy**.

## Relationship to SOLID
Most patterns are concrete applications of [[SOLID Principles]] — especially the Open-Closed and Dependency Inversion principles.

## Interview Questions
- Difference between Factory and Abstract Factory?
- How does Spring use the Proxy pattern?
- Strategy vs Template Method?
- Where would you use the Decorator pattern?

## Revision Summary
- Three families: Creational, Structural, Behavioral.
- Patterns apply SOLID; Spring uses Factory, Proxy, Singleton, Template, Strategy.
