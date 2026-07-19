---
title: Java Index
aliases:
  - Java
  - Java Index
domain: Java
module: Index
status: Learning
difficulty: Easy
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - java
  - index
---

# Java

> Engineering handbook for Java — a sequenced path from language fundamentals to JVM performance, written for a 4–5 YOE full-stack engineer. Study top to bottom; revise from the module indexes and bases.

## Overview
Java is a statically typed, object-oriented language running on the JVM. This handbook is organized as 14 modules; each module has an index, ordered topic notes (each with internals, examples, performance notes, best practices, and interview questions), and a tracker base.

## Learning Roadmap
1. [[Java Fundamentals Index|Java Fundamentals]] — JDK/JRE/JVM, compilation, bytecode, wrappers.
2. [[JVM Internals Index|JVM Internals]] — architecture, class loading, execution engine.
3. [[Memory Management Index|Memory Management]] — memory model, heap/stack, generations, GC.
4. [[Core Java Index|Core Java]] — Object methods, String, immutability, Optional.
5. [[Collections Framework Index|Collections Framework]] — List, Set, Map, Queue.
6. [[Exception Handling Index|Exception Handling]] — hierarchy, checked/unchecked, best practices.
7. [[Generics Index|Generics]] — type parameters, erasure, wildcards.
8. [[Functional Programming Index|Functional Programming]] — functional interfaces, lambdas, method refs.
9. [[Streams API Index|Streams API]] — declarative data processing.
10. [[Reflection & Annotations Index|Reflection & Annotations]] — runtime metadata.
11. [[Serialization Index|Serialization]] — persistence and I/O.
12. [[Concurrency Index|Concurrency]] — threads, locks, executors, virtual threads.
13. [[JVM Performance Index|JVM Performance]] — JIT, escape analysis, GC tuning, profiling.
14. [[Best Practices Index|Best Practices]] — coding, API design, performance.

## Suggested Study Order
Fundamentals → JVM → Memory build the mental model. Core Java and Collections are daily drivers. Exception Handling, Generics, Functional, Streams sharpen language fluency. Concurrency and JVM Performance are the deep, interview-heavy topics; finish with Best Practices.

## Prerequisites
- [[Object-Oriented Programming]] and [[SOLID Principles]] from [[Computer Science]].

## Related Modules
- [[Spring]] — the framework built on Java.
- [[System Design]] — where these building blocks are applied at scale.

## Trackers (Bases)
Whole domain plus per-area views:
- [[Collections Framework Index|Collections]], [[Concurrency Index|Concurrency]], [[JVM Internals Index|JVM]], [[Memory Management Index|Memory]], [[Streams API Index|Streams]], [[Exception Handling Index|Exception Handling]], [[Reflection & Annotations Index|Reflection]], [[JVM Performance Index|Performance]].

## Interview Focus
- Collections internals (HashMap, ConcurrentHashMap), equals/hashCode contract.
- Memory model, GC generations and tuning.
- Concurrency: threads, locks, executors, virtual threads.
- Exceptions: checked vs unchecked, boundary handling.

## Topic Tracker

> Live, auto-updating table of every Java note, grouped by module.

![[Java.base]]
