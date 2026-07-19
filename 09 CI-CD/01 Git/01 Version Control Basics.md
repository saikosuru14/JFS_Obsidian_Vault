---
title: Version Control Basics
aliases:
  - Version Control Basics
domain: CI-CD
module: Git
status: Learning
difficulty: Easy
priority: High
interview: 3
revision: Weekly
order: 1
tags:
  - ci-cd
  - git
related:
  - "[[Git Areas and Workflow]]"
  - "[[Branching Strategies]]"
---

# Version Control Basics

## What Is Version Control?
A version control system (VCS) records changes to files over time so you can recall specific versions, collaborate, and recover from mistakes. **Git** is a distributed VCS — every clone is a full repository with complete history.

## Why Git
- Full history and the ability to revert.
- Branching and merging for parallel work.
- Distributed: work offline; every clone is a backup.
- The foundation of CI/CD — pipelines trigger on commits/merges.

## Centralized vs Distributed
| | Centralized (SVN) | Distributed (Git) |
|---|-------------------|-------------------|
| Repo copies | One central server | Full copy per clone |
| Offline work | Limited | Full |
| Branching | Heavy | Cheap and fast |

## Core Concepts
- **Repository** — the project and its full history.
- **Commit** — an immutable snapshot with a unique SHA hash.
- **Branch** — a movable pointer to a commit.
- **Remote** — a shared repository (e.g., GitHub/GitLab).

## First Commands
```bash
git init                # start a repo
git clone <url>         # copy a remote repo
git status              # see changes
git add .               # stage changes
git commit -m "msg"     # record a snapshot
git log --oneline       # view history
```

## Interview Questions
- Git vs SVN (distributed vs centralized)?
- What is a commit and what makes it unique (SHA)?
- Why is branching cheap in Git?

## Related Notes
- [[Git Areas and Workflow]]
- [[Branching]]

## Revision Summary
- Git = distributed VCS; commits are immutable snapshots; branches are pointers.
