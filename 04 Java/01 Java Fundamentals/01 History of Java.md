---
title: History of Java
aliases:
  - History of Java
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 1
tags:
  - java
related:
  - "[[Java Fundamentals Index|Java Fundamentals]]"
---

# History of Java

## Overview
Java's evolution matters mainly for knowing which features exist in which version and why the release model changed. Focus on the releases that changed how we write code.

## Milestones That Matter
| Version | Year | Key additions |
|---------|------|---------------|
| 1.0 | 1995 | "Write once, run anywhere"; JVM + bytecode |
| **5** | 2004 | Generics, annotations, enums, autoboxing, enhanced for |
| 7 | 2011 | try-with-resources, diamond operator, NIO.2 |
| **8** | 2014 | Lambdas, Streams, `Optional`, default methods, new Date/Time |
| 9 | 2017 | Module system (JPMS), JShell |
| 11 | 2018 | First LTS after new cadence; `var` in lambdas, HTTP client |
| **17** | 2021 | LTS; records, sealed classes, pattern matching, switch expressions |
| **21** | 2023 | LTS; virtual threads, pattern matching for switch, record patterns |

## Release Model
Since Java 9 (2017), a new feature release ships every **6 months**, with an **LTS** every ~2 years (8, 11, 17, 21). Most companies standardize on LTS versions.

## Interview Questions
- **Why was Java 8 significant?** Lambdas + Streams brought functional-style programming; `Optional` and the new Date/Time API modernized the language.
- **What is an LTS release?** A long-term-support version with extended updates — the ones teams run in production (8, 11, 17, 21).
- **What did Java 21 add?** Virtual threads (Loom), pattern matching for switch, record patterns.

## Related Topics
- [[JDK vs JRE vs JVM]] · [[Virtual Threads]] · [[Functional Programming Index|Functional Programming]]

## Quick Revision
- Java 5 = generics/annotations; Java 8 = lambdas/streams; Java 17/21 = records, sealed, pattern matching, virtual threads. 6-month cadence, LTS every ~2 years.
