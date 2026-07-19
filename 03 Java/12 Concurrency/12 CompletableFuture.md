---
title: CompletableFuture
aliases:
  - CompletableFuture
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 12
tags:
  - java
related:
  - "[[Callable & Future]]"
---

# CompletableFuture

## Overview
`CompletableFuture<T>` (Java 8+) is a composable, non-blocking `Future`. You build a pipeline of stages that run as results become available, and you can combine multiple async operations without blocking.

## Why It Matters
It's the modern way to orchestrate async work (parallel service calls, fan-out/fan-in) with proper error handling — a frequent senior interview and code-review topic.

## Core Operations
```java
CompletableFuture
  .supplyAsync(() -> fetchUser(id), pool)   // run async, returns value
  .thenApply(User::name)                    // transform (sync stage)
  .thenCompose(name -> lookupAsync(name))   // flatMap: chain another future
  .thenCombine(otherFuture, (a, b) -> merge(a, b))  // combine two
  .exceptionally(ex -> "fallback")          // recover from failure
  .thenAccept(System.out::println);         // consume result
```

- `thenApply` vs `thenCompose`: apply = map (returns a value); compose = flatMap (returns another `CompletableFuture`, avoids nesting).
- `thenCombine`: join two independent futures.
- `allOf` / `anyOf`: wait for all / first of many.
- `*Async` variants run the stage on a supplied executor (or the common ForkJoinPool by default).

## Error Handling
- `exceptionally(fn)` — recover with a fallback value.
- `handle((res, ex) -> ...)` — see both outcome and exception.
- `whenComplete` — side-effect without altering the result.

## Best Practices
- Always pass an explicit executor to `*Async` for I/O; the default common pool is shared and small.
- Don't call `get()`/`join()` mid-pipeline — that reintroduces blocking.
- Propagate errors through the chain rather than swallowing them.

## Interview Questions
- **thenApply vs thenCompose?** map vs flatMap — compose returns a future and flattens nested `CompletableFuture`.
- **CompletableFuture vs Future?** CF is non-blocking, composable, supports callbacks, combination, and error recovery.
- **Which pool runs the stages?** The common ForkJoinPool unless you pass an executor to the `*Async` methods.

## Related Topics
- [[Callable & Future]] · [[Executor Framework]] · [[ForkJoinPool]]

## Quick Revision
- Composable non-blocking future. thenApply=map, thenCompose=flatMap, thenCombine/allOf to join, exceptionally/handle for errors. Pass your own executor.
