---
title: Stack
aliases:
  - Stack
domain: DSA
module: Stacks and Queues
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Stacks and Queues Index|Stacks and Queues]]"
  - "[[Monotonic Stack]]"
---

# Stack

## Overview
A stack is a LIFO (last-in, first-out) structure: you push/pop/peek at one end (the top). All three operations are O(1).

## Why It Matters
Stacks model nested/reversible processes: recursion call stack, expression parsing, matching brackets, undo, and DFS. Recognizing "most recent unmatched thing" signals a stack.

## Java Usage
```java
Deque<Integer> stack = new ArrayDeque<>();   // preferred over legacy Stack
stack.push(1);          // add to top
int top = stack.peek();  // view top
int val = stack.pop();   // remove top
boolean empty = stack.isEmpty();
```
Prefer `ArrayDeque` over the legacy `java.util.Stack` (which is synchronized and extends Vector).

## Classic Problems
- **Balanced parentheses** — push openers, pop/match on closers.
- **Expression evaluation** — infix->postfix, evaluate postfix.
- **[[Monotonic Stack]]** — next greater/smaller element.
- **DFS (iterative)** and function-call simulation.

```java
// Valid parentheses: O(n)
Deque<Character> st = new ArrayDeque<>();
for (char c : s.toCharArray()) {
    if (c == '(' || c == '[' || c == '{') st.push(c);
    else { if (st.isEmpty() || !matches(st.pop(), c)) return false; }
}
return st.isEmpty();
```

## Interview Questions
- **Why `ArrayDeque` over `Stack`?** `Stack` is legacy, synchronized, and extends Vector; `ArrayDeque` is faster and the modern choice.
- **How does recursion relate to a stack?** The call stack is a stack; any recursion can be simulated iteratively with an explicit stack.
- **Detect balanced brackets?** Push openers, match closers via pops; stack empty at end = valid.

## Related Topics
- [[Monotonic Stack]] · [[Queue]] · [[Recursion]] · [[DFS]]

## Quick Revision
- LIFO, O(1) push/pop/peek. Use `ArrayDeque`, not legacy `Stack`. Great for brackets, expression eval, iterative DFS, monotonic-stack problems.
