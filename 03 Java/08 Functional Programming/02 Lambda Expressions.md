---
title: Lambda Expressions
aliases:
  - Lambda Expressions
domain: Java
module: Functional Programming
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Functional Interfaces]]"
  - "[[Method References]]"
---

# Lambda Expressions

## Overview
A lambda is an anonymous function that implements a [[Functional Interfaces|functional interface]] inline. `(args) -> body`. It replaces verbose anonymous classes and is the syntax that makes streams readable.

## Why It Matters
Lambdas turn behavior into data you can pass around. They're everywhere in modern Java: streams, `Optional`, `CompletableFuture`, event handlers.

## Syntax
```java
Runnable r = () -> System.out.println("hi");
Comparator<String> byLen = (a, b) -> a.length() - b.length();
Function<Integer,Integer> sq = x -> x * x;
list.forEach(x -> { log(x); process(x); });   // block body
```

## Lambda vs Anonymous Class
| | Lambda | Anonymous class |
|--|--------|-----------------|
| `this` | enclosing instance | the anonymous instance |
| Compiles to | `invokedynamic` (no extra .class) | a new `.class` file |
| Target | functional interface only | any interface/class |
| Fields/state | none | can have fields |

Lambdas do **not** create a new scope for `this` and can't shadow enclosing variables — they're lexically scoped.

## Effectively Final Capture
A lambda can capture local variables only if they're **final or effectively final** (never reassigned). This avoids the mutable-capture bugs anonymous classes had and keeps captured state safe across threads.

## Best Practices
- Keep lambdas short; extract to a named method (then a [[Method References|method reference]]) if logic grows.
- Don't mutate captured state or perform side effects inside stream lambdas.

## Interview Questions
- **Lambda vs anonymous class?** Lambda has no own `this`, compiles via `invokedynamic` (no extra class file), and targets only functional interfaces.
- **What does `this` refer to inside a lambda?** The enclosing instance, not the lambda.
- **What is "effectively final"?** A local not reassigned after initialization — required for capture.

## Related Topics
- [[Functional Interfaces]] · [[Method References]] · [[Streams API Index|Streams API]]

## Quick Revision
- Anonymous function implementing a SAM interface. `this` = enclosing; captures effectively-final locals; `invokedynamic` (no extra class). Keep short; avoid side effects.
