---
title: Serialization Index
aliases:
  - Serialization Index
domain: Java
module: Serialization
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 0
tags:
  - java
  - index
related:
  - "[[Java Index|Java]]"
  - "[[Serialization]]"
  - "[[NIO]]"
---

# Serialization

> Module index - part of the [[Java Index|Java]] learning path.

## Overview
This module covers turning objects into bytes and back (**serialization**) and the modern **NIO** I/O model. Built-in Java serialization is convenient but has real security and versioning problems, so most services use text/binary formats (JSON, Protobuf) instead.

## Branches (expand each)
- **[[Serialization]]** — `Serializable`, `transient`, `serialVersionUID`, and why to avoid native serialization.
- **[[NIO]]** — channels, buffers, selectors, and non-blocking I/O.

## Learning Roadmap
1. [[Serialization]]
2. [[NIO]]

## Prerequisites
- [[Reflection & Annotations Index|Reflection & Annotations]]

## Next
- [[Concurrency Index|Concurrency]]

## Related Modules
- [[Java Index|Java]]

## Quick Revision
- Serialization = object <-> bytes; native form is risky (security/versioning) -> prefer JSON/Protobuf. NIO = buffer/channel-based, non-blocking, scalable I/O.
