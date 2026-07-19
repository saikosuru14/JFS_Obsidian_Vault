---
title: Interview Strategy
aliases:
  - Interview Strategy
domain: DSA
module: Greedy and Patterns
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Daily
order: 4
tags:
  - dsa
related:
  - "[[Greedy and Patterns Index|Greedy and Patterns]]"
  - "[[Common Coding Patterns]]"
---

# Interview Strategy

## Overview
A repeatable method for solving a coding-interview problem calmly and completely — the process matters as much as the answer, because interviewers grade communication, correctness, and analysis.

## Why It Matters
Strong coders fail interviews by jumping to code, missing edge cases, or going silent. A structured approach demonstrates the exact signals interviewers look for.

## The Method (UMPIRE-style)
1. **Understand / clarify** — restate the problem; ask about input size, ranges, duplicates, empties, and constraints. Confirm expected output.
2. **Examples** — walk a normal case and edge cases (empty, single, duplicates, negatives, overflow).
3. **Brute force first** — state the naive solution and its complexity; it shows correctness and a baseline.
4. **Optimize** — identify the bottleneck; match to a [[Common Coding Patterns|pattern]]; state the target complexity and the idea *before* coding.
5. **Code** — write clean, modular code; narrate as you go; use good names.
6. **Test** — trace through examples and edge cases; fix bugs; confirm complexity.

## Communication
- Think out loud — the interviewer follows your reasoning, not just the final code.
- Ask before assuming; state trade-offs (time vs space).
- If stuck, verbalize what you know and try a smaller example or a brute force.

## Complexity Discipline
Always state time and space in [[Big O Notation|Big O]] for both the brute force and the optimized solution, and confirm it meets the input constraints.

## Common Mistakes
- Coding before clarifying / choosing an approach.
- Ignoring edge cases (empty, single element, overflow, duplicates).
- Silent problem-solving; not testing the final code.

## Interview Questions (meta)
- **First thing to do on a new problem?** Clarify constraints and outputs; do examples — don't code yet.
- **How to handle being stuck?** Talk through knowns, try brute force, shrink the example, look for a pattern.
- **Why start with brute force?** Establishes correctness + a baseline and often reveals the optimization.

## Related Topics
- [[Common Coding Patterns]] · [[Complexity Analysis Index|Complexity Analysis]] · [[Big O Notation]]

## Quick Revision
- Clarify -> examples -> brute force (+complexity) -> optimize via pattern -> code cleanly (narrate) -> test edge cases. State Big O for both solutions. Think out loud; handle edges.
