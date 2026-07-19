---
title: StringBuffer
aliases:
  - StringBuffer
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: Low
interview: 3
revision: Monthly
order: 9
tags:
  - java
  - core
related:
  - "[[StringBuilder]]"
  - "[[String]]"
---

# StringBuffer

## Overview
Legacy thread-safe counterpart of [[StringBuilder]] — same API, but every method is `synchronized`. Rarely the right choice today.

## StringBuilder vs StringBuffer
| | StringBuilder | StringBuffer |
|---|---------------|--------------|
| Thread-safe | No | Yes (synchronized) |
| Speed | Faster | Slower |
| Since | 1.5 | 1.0 |

## Why It Matters
Interview comparison, and the reason `StringBuilder` exists (drop the sync you almost never need). Per-method synchronization doesn't make a *sequence* of appends atomic anyway — a shared builder usually needs external coordination.

## Best Practices
- Default to `StringBuilder`. Use a local builder per thread rather than sharing one.

## Interview Questions
- StringBuffer vs StringBuilder?
- Does method-level synchronization make multi-step building thread-safe? (No)

## Related Topics
- [[StringBuilder]] · [[String]]

## Quick Revision
- Synchronized (slow) sibling of StringBuilder. Prefer StringBuilder; per-method sync ≠ compound atomicity.
