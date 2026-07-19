---
title: Branching Strategies
aliases:
  - Branching Strategies
domain: CI-CD
module: Git
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 6
tags:
  - ci-cd
  - git
related:
  - "[[Branching]]"
  - "[[GitOps]]"
  - "[[Build Pipelines]]"
---

# Branching Strategies

How a team organizes branches to release software reliably.

## Trunk-Based Development
- Everyone commits to a single `main` (trunk) with very short-lived branches.
- Requires strong CI and feature flags.
- Best for continuous delivery; minimizes merge pain.

## GitHub Flow
- `main` is always deployable.
- Branch → commit → pull request → review → merge → deploy.
- Simple; great for web apps with continuous deployment.

## Git Flow
- Long-lived `main` and `develop`, plus `feature/*`, `release/*`, `hotfix/*`.
- Structured releases; heavier process.
- Suits scheduled releases and versioned products.

## Comparison
| Strategy | Branches | Best for |
|----------|----------|----------|
| Trunk-based | main + tiny branches | Continuous delivery, mature CI |
| GitHub Flow | main + feature | Web apps, continuous deploy |
| Git Flow | main/develop/release/hotfix | Scheduled, versioned releases |

## Conventions
- Name branches `feature/`, `bugfix/`, `hotfix/`, `release/`.
- Protect `main` (require PR + green CI before merge).
- Use meaningful commit messages (consider Conventional Commits).

## Relation to CI/CD
The strategy drives pipeline triggers: PRs run tests; merges to `main` trigger [[Build Pipelines|builds]] and deployments ([[GitOps]]).

## Interview Questions
- Trunk-based vs Git Flow — when to use each?
- How do feature flags enable trunk-based development?
- Why protect the main branch?

## Related Notes
- [[Branching]]
- [[Build Pipelines]]
- [[GitOps]]

## Revision Summary
- Trunk-based (CD-friendly), GitHub Flow (simple), Git Flow (structured releases). Protect main; PR + CI before merge.
