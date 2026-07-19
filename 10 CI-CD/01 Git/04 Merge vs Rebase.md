---
title: Merge vs Rebase
aliases:
  - Merge vs Rebase
domain: CI-CD
module: Git
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - ci-cd
  - git
related:
  - "[[Branching]]"
  - "[[Merge Conflicts]]"
---

# Merge vs Rebase

Both integrate changes from one branch into another; they differ in the history they produce.

## Merge
```bash
git switch main
git merge feature/x
```
- Creates a **merge commit** joining two histories (unless fast-forward).
- Preserves the exact history and branch topology.
- Non-destructive; safe for shared branches.

## Rebase
```bash
git switch feature/x
git rebase main
```
- **Replays** your commits on top of the target branch, creating new commits (new SHAs).
- Produces a **linear**, clean history.
- Rewrites history — never rebase commits that are already pushed/shared.

## Comparison
| | Merge | Rebase |
|---|-------|--------|
| History | Preserved, with merge commits | Linear, rewritten |
| SHAs | Unchanged | New |
| Shared branches | Safe | Dangerous |
| Use for | Integrating into main | Cleaning up a local feature branch |

## The Golden Rule
Do not rebase commits that exist outside your local repository (i.e., already pushed and used by others).

## Fast-Forward
If the target has no new commits, merge just moves the pointer forward (no merge commit). Use `--no-ff` to force a merge commit.

## Interview Questions
- Merge vs rebase — trade-offs?
- Why is rebasing shared history dangerous?
- What is a fast-forward merge?

## Related Notes
- [[Branching]]
- [[Merge Conflicts]]

## Revision Summary
- Merge = preserve history (+merge commit); rebase = linear history (new SHAs). Never rebase shared commits.
