---
title: Optional
aliases:
  - Optional
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: Medium
interview: 4
revision: Weekly
order: 12
tags:
  - java
  - core
related:
  - "[[Java]]"
  - "[[Streams]]"
---

# Optional

## Overview
`Optional<T>` is a container that explicitly models "value or absent," making nullability visible in the type and API.

## Core API
```java
Optional<User> u = repo.findById(id);          // may be empty
return u.map(User::email)
        .filter(e -> e.contains("@"))
        .orElseThrow(() -> new NotFoundException(id));
```
- Create: `of`, `ofNullable`, `empty`.
- Consume: `map`, `flatMap`, `filter`, `ifPresent`, `orElse`, `orElseGet`, `orElseThrow`.

## When to Use
- **Return types** that may legitimately have no value (esp. from lookups/finders).

## When NOT to Use
- Entity/DTO **fields** (breaks serialization, adds overhead).
- Method **parameters** (overload or accept nullable instead).
- Collections — return an empty collection, not `Optional<List>`.

## Best Practices
- `orElseGet(supplier)` when the default is expensive (`orElse` always evaluates its argument).
- Don't call `get()` without `isPresent()` — prefer `orElseThrow`.
- Don't wrap-then-immediately-unwrap; chain `map/filter`.

## Common Mistakes
- `optional.get()` blindly → `NoSuchElementException`.
- `Optional` fields in JPA entities.
- Using `orElse(expensiveCall())` (always runs).

## Interview Questions
- When is `Optional` appropriate vs a bad fit?
- `orElse` vs `orElseGet`?
- Why avoid `Optional` fields on entities?

## Related Topics
- [[Streams]] · [[Coding Best Practices]]

## Quick Revision
- Model absence in return types. Chain map/filter/orElseThrow; use orElseGet for costly defaults. Not for fields/params/collections.
