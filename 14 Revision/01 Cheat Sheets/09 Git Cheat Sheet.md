---
title: Git Cheat Sheet
aliases:
  - Git Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 9
tags:
  - revision
  - git
---

# Git Cheat Sheet

> Mid-level recall for [[Git Index|Git]] — everyday flow plus recovery and history surgery.

## Everyday Flow
```bash
git switch -c feature/x
git add -A && git commit -m "msg"
git push -u origin feature/x     # first time sets upstream
git pull --rebase                # linear history, avoid noisy merge commits
```

## Merge vs Rebase
- **Merge**: preserves history + merge commit; safe on shared branches.
- **Rebase**: linear history, rewrites SHAs. **Golden rule:** never rebase commits already pushed/shared.
- `git rebase -i` (interactive): squash/fixup/reword/reorder before opening a PR.

## Undo / Recovery (senior moves)
```bash
git restore <f> / --staged <f>   # discard / unstage
git commit --amend               # fix last unpushed commit
git revert <sha>                 # safe undo on shared history (new commit)
git reset --soft|--mixed|--hard <sha>  # move HEAD (hard = destructive, local)
git reflog                       # find "lost" commits after a bad reset/rebase
git cherry-pick <sha>            # copy a commit to current branch
git stash [push -m] / pop        # shelve WIP
git bisect start/good/bad        # binary-search a regression
```
- Recovered a botched reset? `git reflog` → `git reset --hard <good-sha>`.

## Branching Strategies
- **Trunk-based** (short-lived branches + CI + feature flags) for continuous delivery; **GitHub Flow** (PR per feature); **Git Flow** (structured releases, heavier).
- Protect `main`: require PR + green CI + review before merge. Squash-merge for clean history.

## Conflicts
Edit between `<<<<<<<`/`=======`/`>>>>>>>`, remove markers, `git add`, then `git commit` (or `git rebase --continue`). `git merge --abort` / `git rebase --abort` to bail.

## Sharp Interview Answers
- Merge vs rebase + the golden rule.
- `revert` (safe, shared) vs `reset` (rewrites); recover with `reflog`.
- Trunk-based vs Git Flow; why protect main.
- What `cherry-pick` / `bisect` are for.

## Revision Checklist
- [ ] Rebase (incl. interactive) vs merge
- [ ] revert vs reset + reflog recovery
- [ ] cherry-pick, stash, bisect
- [ ] branching strategies + branch protection
