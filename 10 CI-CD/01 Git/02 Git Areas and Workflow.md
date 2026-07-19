---
title: Git Areas and Workflow
aliases:
  - Git Areas and Workflow
domain: CI-CD
module: Git
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - ci-cd
  - git
related:
  - "[[Version Control Basics]]"
  - "[[Branching]]"
---

# Git Areas and Workflow

## The Three (Four) Areas
```
Working Directory  --git add-->  Staging Area (Index)  --git commit-->  Local Repo  --git push-->  Remote Repo
        ^                                                                   |
        |------------------------- git checkout / restore ------------------|
```
- **Working directory** — your files on disk.
- **Staging area (index)** — changes marked for the next commit.
- **Local repository** — committed history in `.git`.
- **Remote repository** — the shared server copy.

## Everyday Workflow
```bash
git pull                 # get latest from remote
# ...edit files...
git status               # what changed
git add <file>           # stage specific changes
git commit -m "message"  # snapshot
git push                 # publish to remote
```

## Undoing Things
```bash
git restore <file>          # discard working-dir changes
git restore --staged <file> # unstage
git commit --amend          # fix the last commit
git revert <sha>            # new commit that undoes a commit (safe on shared history)
git reset --hard <sha>      # move branch back (destructive; local only)
```

## Inspecting
```bash
git diff                 # working dir vs staged
git diff --staged        # staged vs last commit
git log --oneline --graph --all
```

## Interview Questions
- Difference between working directory, staging area, and repository?
- `git revert` vs `git reset` — which is safe on shared branches?
- What does `git commit --amend` do?

## Related Notes
- [[Version Control Basics]]
- [[Branching]]

## Revision Summary
- add → commit → push across working dir → index → local → remote.
- Prefer `revert` over `reset` on shared history.
