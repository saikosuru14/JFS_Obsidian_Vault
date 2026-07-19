---
title: Functional Interfaces
aliases:
  - Functional Interfaces
domain: Java
module: Functional Programming
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Functional Programming Index|Functional Programming]]"
  - "[[Lambda Expressions]]"
---

# Functional Interfaces

## Overview
A functional interface has exactly **one abstract method** (SAM), so a lambda or method reference can implement it. `@FunctionalInterface` makes the compiler enforce that. This is the target type every lambda binds to.

## Why It Matters
Lambdas don't have a type of their own — they're assigned to a functional interface. Knowing the built-in ones in `java.util.function` is essential for streams and callbacks.

## Built-in Interfaces (java.util.function)
| Interface | Signature | Use |
|-----------|-----------|-----|
| `Predicate<T>` | `T -> boolean` | filtering |
| `Function<T,R>` | `T -> R` | mapping/transform |
| `Consumer<T>` | `T -> void` | side effects (forEach) |
| `Supplier<T>` | `() -> T` | lazy/factory |
| `BiFunction<T,U,R>` | `(T,U) -> R` | two-arg transform |
| `UnaryOperator<T>` | `T -> T` | same-type transform |
| `BinaryOperator<T>` | `(T,T) -> T` | reduce/combine |

Primitive specializations (`IntPredicate`, `ToIntFunction`, `IntUnaryOperator`) avoid boxing in hot paths.

## @FunctionalInterface
```java
@FunctionalInterface
interface Validator<T> { boolean validate(T t); }   // one abstract method
```
`default` and `static` methods are allowed — only one *abstract* method counts. `Runnable`, `Callable`, `Comparator` are functional interfaces too.

## Best Practices
- Prefer built-in interfaces over custom ones for interoperability with streams.
- Use primitive specializations to avoid autoboxing in numeric pipelines.
- Add `@FunctionalInterface` to custom ones to catch accidental extra abstract methods.

## Interview Questions
- **What is a functional interface?** An interface with exactly one abstract method, usable as a lambda target.
- **Can it have other methods?** Yes — any number of `default`/`static` methods; only one abstract.
- **Name the core four.** Predicate, Function, Consumer, Supplier.
- **Why primitive specializations?** To avoid boxing overhead in numeric-heavy code.

## Related Topics
- [[Lambda Expressions]] · [[Method References]] · [[Streams API Index|Streams API]]

## Quick Revision
- One abstract method (SAM) = lambda target. Core: Predicate/Function/Consumer/Supplier. `@FunctionalInterface` enforces it; use primitive variants to skip boxing.
