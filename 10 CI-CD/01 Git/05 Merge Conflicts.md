---
title: Merge Conflicts
aliases:
  - Merge Conflicts
domain: CI-CD
module: Git
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - ci-cd
  - git
related:
  - "[[Merge vs Rebase]]"
---

# Merge Conflicts

## When They Happen
A conflict occurs when two branches change the **same lines** of a file (or one edits a file the other deletes) and Git can't auto-merge.

## Conflict Markers
```
<<<<<<< HEAD
your current branch's version
=======
the incoming branch's version
>>>>>>> feature/x
```

## Resolving
```bash
git merge feature/x          # conflict reported
git status                   # list conflicted files
# edit files, remove markers, keep the correct content
git add <resolved-file>
git commit                   # completes the merge
```
During a rebase, resolve then `git rebase --continue` (or `git rebase --abort`).

## Reducing Conflicts
- Pull/rebase frequently; keep branches short-lived.
- Make small, focused commits.
- Agree on formatting to avoid noise.

## Helpful Tools
```bash
git mergetool          # launch a visual merge tool
git merge --abort      # bail out and restore pre-merge state
```

## Interview Questions
- What causes a merge conflict?
- How do you resolve one, step by step?
- How can a team reduce conflicts?

## Related Notes
- [[Merge vs Rebase]]

## Revision Summary
- Conflicts = same lines changed. Edit markers → add → commit. Small, frequent merges reduce them.
