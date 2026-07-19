---
title: Wrapper Classes
aliases:
  - Wrapper Classes
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - java
related:
  - "[[Java Fundamentals Index|Java Fundamentals]]"
  - "[[Autoboxing and Unboxing]]"
---

# Wrapper Classes

## Overview
Wrapper classes (`Integer`, `Long`, `Double`, `Boolean`, ...) box each primitive as an object. They exist because generics and collections work only with objects, not primitives.

## Why It Matters
Wrappers enable `List<Integer>`, allow `null` (a "no value" state primitives lack), and provide parsing/utility methods — but they cost memory and can surprise you with `==`.

## Primitive -> Wrapper
| Primitive | Wrapper |
|-----------|---------|
| int | Integer |
| long | Long |
| double | Double |
| boolean | Boolean |
| char | Character |
| byte/short/float | Byte/Short/Float |

## Key Behaviors
- **Immutable** — like `String`; operations return new objects.
- **Parsing/utilities** — `Integer.parseInt`, `Integer.MAX_VALUE`, `Integer.compare`.
- **Integer cache** — `Integer.valueOf` caches -128..127, so `==` may accidentally "work" for small values but fail for larger ones (see [[Autoboxing and Unboxing]]).

## Costs
- Boxing allocates an object (~16 bytes) vs 4 bytes for `int` — heavy in large collections.
- For primitive-heavy numeric work prefer arrays/`IntStream`/specialized collections over `List<Integer>`.

## Best Practices
- Compare wrappers with `.equals()` or unbox to primitives, never `==`.
- Beware `NullPointerException` when unboxing a `null` wrapper.
- Use primitive streams (`IntStream`) and arrays for hot numeric paths.

## Interview Questions
- **Why do wrapper classes exist?** Collections/generics need objects; wrappers also allow `null` and provide utilities.
- **Are wrappers mutable?** No — immutable.
- **Cost of wrappers vs primitives?** Extra heap allocation and indirection; significant at scale.

## Related Topics
- [[Autoboxing and Unboxing]] · [[Collections Framework]] · [[Generics Index|Generics]]

## Quick Revision
- Objects wrapping primitives; immutable; needed for collections/generics/null. Watch memory cost and the Integer cache. Compare with equals, not ==.
