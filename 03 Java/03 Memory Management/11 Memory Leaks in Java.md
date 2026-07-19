---
title: Memory Leaks in Java
aliases:
  - Memory Leaks in Java
domain: Java
module: Memory Management
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 11
tags:
  - java
---

# Memory Leaks in Java

GC does not prevent all memory leaks.

Common Causes:
- Static collections
- Unclosed resources
- Listener leaks
- Cache growth
- ThreadLocal misuse

Tools:
- VisualVM
- JConsole
- Java Flight Recorder
- Eclipse MAT
