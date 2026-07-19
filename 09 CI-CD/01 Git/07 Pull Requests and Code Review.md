---
title: Pull Requests and Code Review
aliases:
  - Pull Requests and Code Review
  - Pull Requests
domain: CI-CD
module: Git
status: Learning
difficulty: Easy
priority: High
interview: 3
revision: Weekly
order: 7
tags:
  - ci-cd
  - git
related:
  - "[[Branching Strategies]]"
  - "[[Build Pipelines]]"
---

# Pull Requests and Code Review

## What Is a Pull Request?
A pull request (PR) / merge request (MR) proposes merging one branch into another. It's the gate where CI runs and teammates review before code reaches `main`.

## Typical PR Flow
1. Push a feature branch and open a PR against `main`.
2. CI runs automatically (build, tests, lint, [[SonarQube|quality gate]]).
3. Reviewers comment and request changes.
4. Author updates; discussions resolve.
5. Merge (squash / merge commit / rebase) once approved and green.

## Merge Options
- **Squash and merge** — collapse the branch into one commit (clean main history).
- **Merge commit** — preserve all commits + a merge commit.
- **Rebase and merge** — linear history, replays commits.

## Good Review Practices
- Keep PRs small and focused.
- Write a clear description (what/why, testing, screenshots).
- Automate style so reviews focus on logic.
- Require at least one approval and green CI (branch protection).

## What Reviewers Look For
- Correctness, edge cases, tests.
- Readability and naming.
- Security and performance concerns.
- Adherence to [[SOLID Principles]] and team conventions.

## Interview Questions
- What is a pull request and why use one?
- Squash vs merge commit vs rebase merge?
- What makes a good code review?

## Related Notes
- [[Branching Strategies]]
- [[Build Pipelines]]

## Revision Summary
- PR = review + CI gate before main. Keep PRs small; require approval + green checks; pick a merge style deliberately.
