---
title: Tags and Releases
aliases:
  - Tags and Releases
domain: CI-CD
module: Git
status: Learning
difficulty: Easy
priority: Medium
interview: 2
revision: Weekly
order: 8
tags:
  - ci-cd
  - git
related:
  - "[[Branching Strategies]]"
  - "[[Artifact Repositories]]"
---

# Tags and Releases

## Tags
A tag marks a specific commit — usually a release point. Unlike branches, tags don't move.
```bash
git tag v1.2.0                    # lightweight tag
git tag -a v1.2.0 -m "Release"    # annotated (recommended: has author/date/message)
git push origin v1.2.0            # push a tag
git push origin --tags            # push all tags
git tag                           # list
```

## Semantic Versioning (SemVer)
`MAJOR.MINOR.PATCH` (e.g., `2.4.1`):
- **MAJOR** — breaking changes.
- **MINOR** — backward-compatible features.
- **PATCH** — backward-compatible fixes.
Pre-release/build suffixes: `1.0.0-rc.1`, `1.0.0+build.5`.

## Releases
- A release pairs a tag with notes and built artifacts (jars, images).
- Tags commonly **trigger CI/CD release pipelines** that build, publish to an [[Artifact Repositories|artifact repository]] / registry, and deploy.

## Annotated vs Lightweight
- **Annotated** — a full object (author, date, message, can be signed). Use for releases.
- **Lightweight** — just a pointer; fine for private/temporary marks.

## Interview Questions
- Difference between a tag and a branch?
- Annotated vs lightweight tags?
- Explain semantic versioning.

## Related Notes
- [[Branching Strategies]]
- [[Artifact Repositories]]

## Revision Summary
- Tags mark releases (use annotated); follow SemVer; tags often trigger release pipelines.
