---
title: Method References
aliases:
  - Method References
domain: Java
module: Functional Programming
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[Lambda Expressions]]"
---

# Method References

## Overview
A method reference is shorthand for a lambda that does nothing but call one existing method. `list.forEach(System.out::println)` reads better than `x -> System.out.println(x)`.

## Why It Matters
They make functional code cleaner and signal intent ("just call this method"). Recognizing the four forms is a common interview and readability point.

## The Four Forms
| Form | Syntax | Equivalent lambda |
|------|--------|-------------------|
| Static method | `Integer::parseInt` | `s -> Integer.parseInt(s)` |
| Instance of a particular object | `System.out::println` | `x -> System.out.println(x)` |
| Instance of an arbitrary object of a type | `String::toLowerCase` | `s -> s.toLowerCase()` |
| Constructor | `ArrayList::new` | `() -> new ArrayList<>()` |

## The Subtle One
`String::toLowerCase` (unbound) — the first lambda parameter becomes the **receiver**: `(String s) -> s.toLowerCase()`. Contrast with a bound reference like `str::toLowerCase`, which fixes the receiver to `str`.

```java
list.stream().map(String::toUpperCase)          // arbitrary-object
    .sorted(Comparator.comparing(String::length))
    .collect(Collectors.toList());

Supplier<List<String>> factory = ArrayList::new; // constructor
```

## Best Practices
- Prefer a method reference when the lambda only forwards its arguments to one method.
- Keep an explicit lambda when you need extra logic, argument reordering, or clarity.

## Interview Questions
- **Four kinds of method references?** Static, bound instance, unbound instance (arbitrary object), and constructor.
- **What does `String::length` mean as an argument?** An unbound reference where the receiver is the first parameter — `s -> s.length()`.
- **Method reference vs lambda?** Same result; reference is cleaner when the body is a single method call.

## Related Topics
- [[Lambda Expressions]] · [[Functional Interfaces]] · [[Streams API Index|Streams API]]

## Quick Revision
- Shorthand for single-call lambdas. Forms: Class::static, obj::instance, Class::instance (receiver = first arg), Class::new. Use when the lambda just forwards args.
