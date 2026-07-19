---
title: clone()
aliases:
  - clone()
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: Low
interview: 3
revision: Monthly
order: 6
tags:
  - java
  - core
related:
  - "[[Object Class]]"
  - "[[Immutability]]"
---

# clone()

## Overview
`Object.clone()` makes a field-by-field copy. It's widely considered a flawed API — prefer copy constructors or static factories.

## How It Works
- Requires implementing `Cloneable` (a marker interface) or `clone()` throws `CloneNotSupportedException`.
- Default is a **shallow copy**: object references are copied, not the referenced objects — mutable fields are shared.
- Deep copy requires manually cloning nested mutable fields.

## Shallow vs Deep
- **Shallow**: top-level fields copied; nested objects shared.
- **Deep**: nested mutable objects copied recursively (independent graphs).

## Best Practices
- Prefer a **copy constructor** (`new Foo(other)`) or static factory (`Foo.copyOf`) — clearer and type-safe.
- Make classes [[Immutability|immutable]] so copying is unnecessary.

## Common Mistakes
- Assuming `clone()` is deep.
- Forgetting `Cloneable`, or breaking `final` fields (clone bypasses constructors).

## Interview Questions
- Shallow vs deep copy?
- Why is `clone()`/`Cloneable` considered broken?
- Alternatives to `clone()`?

## Related Topics
- [[Object Class]] · [[Immutability]]

## Quick Revision
- Shallow field copy via Cloneable; nested mutables shared. Prefer copy constructors/factories; better yet, be immutable.
