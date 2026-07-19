---
title: Branching
aliases:
  - Branching
  - Git Branching
domain: CI-CD
module: Git
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - ci-cd
  - git
related:
  - "[[Merge vs Rebase]]"
  - "[[Branching Strategies]]"
---

# Branching

## What Is a Branch?
A branch is a lightweight, movable pointer to a commit. Creating one just writes a new pointer — it does not copy files, which is why branching is cheap in Git. `HEAD` points to the current branch.

## Commands
```bash
git branch                 # list branches
git branch feature/login   # create
git switch feature/login   # switch (or: git checkout)
git switch -c feature/x     # create + switch
git branch -d feature/x     # delete (merged)
git branch -D feature/x     # force delete
```

## Tracking Remote Branches
```bash
git push -u origin feature/x   # push and set upstream
git fetch                      # update remote-tracking refs
git branch -vv                 # see upstream mapping
```

## Typical Feature Flow
1. Branch off the main line: `git switch -c feature/x`.
2. Commit work on the branch.
3. Push and open a [[Pull Requests and Code Review|pull request]].
4. Merge back after review; delete the branch.

## Interview Questions
- Why is creating a branch cheap in Git?
- What is `HEAD`?
- Difference between `git switch` and `git checkout`?

## Related Notes
- [[Merge vs Rebase]]
- [[Branching Strategies]]

## Revision Summary
- Branch = pointer to a commit; `HEAD` = current position. Branch → commit → PR → merge.
