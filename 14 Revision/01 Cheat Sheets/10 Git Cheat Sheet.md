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
order: 10
tags:
  - revision
  - git
---

# Git Cheat Sheet

> Interview-ready revision for [[Git Index|Git]] (4–5 YOE). Commands, recovery, and Q&A with answers.

---

## 1. Model (mental picture)
Working directory → **staging (index)** → local repo (commits) → remote. A commit is an immutable snapshot with a SHA; a branch is a movable pointer; `HEAD` is where you are.

## 2. Everyday Flow
```bash
git switch -c feature/x            # create + switch
git add -p                         # stage hunks interactively
git commit -m "msg"
git pull --rebase                  # linear history, no noisy merge commits
git push -u origin feature/x       # first push sets upstream
git status ; git log --oneline --graph --all
```

## 3. Merge vs Rebase
- **Merge**: preserves history, adds a merge commit; safe on shared branches.
- **Rebase**: replays your commits onto the target → linear history, **new SHAs**. **Golden rule:** never rebase commits already pushed/shared.
- **Interactive rebase** to clean up before a PR:
```bash
git rebase -i main       # squash / fixup / reword / reorder / drop
```

## 4. Undo & Recovery (senior moves)
```bash
git restore <f>              # discard working-dir changes
git restore --staged <f>     # unstage (keep changes)
git commit --amend           # fix the last (unpushed) commit
git revert <sha>             # NEW commit that undoes <sha> — safe on shared history
git reset --soft  <sha>      # move HEAD, keep changes staged
git reset --mixed <sha>      # (default) keep changes unstaged
git reset --hard  <sha>      # discard changes — destructive, local only
git reflog                   # history of HEAD moves → recover "lost" commits
git cherry-pick <sha>        # copy a specific commit to current branch
git stash push -m "wip" ; git stash pop
git bisect start / bad / good <sha>   # binary-search a regression
```
- Recovered a bad `reset --hard`? `git reflog` → find the good SHA → `git reset --hard <sha>`.
- **`revert` vs `reset`:** revert is safe on shared branches (adds a commit); reset rewrites history (only for local/unpushed work).

## 5. Conflicts
Markers `<<<<<<<` / `=======` / `>>>>>>>` → edit to the correct content, remove markers, `git add`, then `git commit` (merge) or `git rebase --continue`. Bail with `git merge --abort` / `git rebase --abort`. `git mergetool` for a GUI.

## 6. Branching Strategies
| Strategy | Branches | Best for |
|----------|----------|----------|
| Trunk-based | main + short-lived + feature flags | continuous delivery, strong CI |
| GitHub Flow | main + feature → PR | web apps, continuous deploy |
| Git Flow | main/develop/release/hotfix | scheduled, versioned releases |
- Protect `main`: require PR + green CI + review. **Squash-merge** for a clean history; conventional commits for automated changelogs/releases.

## 7. Tags & Releases
```bash
git tag -a v1.2.0 -m "Release"    # annotated (author/date/msg) — use for releases
git push origin v1.2.0
```
SemVer `MAJOR.MINOR.PATCH`; tags often trigger release pipelines.

---

## 8. Interview Q&A (with answers)

**Q: Merge vs rebase, and when do you use each?**
A: Merge preserves the true history with a merge commit — use it to integrate into shared branches. Rebase rewrites commits onto a new base for a linear history — use it to tidy a local feature branch before a PR. Never rebase commits already pushed/shared (the golden rule).

**Q: `git revert` vs `git reset`?**
A: `revert` creates a new commit that undoes a previous one — safe on shared branches. `reset` moves the branch pointer (optionally discarding changes with `--hard`) and rewrites history — only for local/unpushed work.

**Q: You did a bad `reset --hard` — how do you recover?**
A: `git reflog` shows every position HEAD held; find the SHA before the reset and `git reset --hard <sha>` (or `git checkout <sha>`).

**Q: What are cherry-pick and bisect for?**
A: `cherry-pick` copies a specific commit onto the current branch (e.g., backport a fix). `bisect` binary-searches commits (mark good/bad) to find the one that introduced a regression.

**Q: Trunk-based vs Git Flow?**
A: Trunk-based uses very short-lived branches merged to `main` frequently behind feature flags — great for continuous delivery with strong CI. Git Flow uses long-lived develop/release/hotfix branches — heavier, suited to scheduled, versioned releases.

**Q: How do you keep `main` healthy?**
A: Branch protection: require PRs, passing CI, and reviews before merge; squash-merge to keep history readable; small, frequent PRs.

**Q: How do you resolve a conflict during rebase?**
A: Edit the conflicted files, remove markers, `git add`, then `git rebase --continue` (or `--abort` to bail). Conflicts recur per commit during a rebase (vs once for a merge).

---

## Revision Checklist
- [ ] add/commit/push + pull --rebase
- [ ] merge vs rebase + golden rule + interactive rebase
- [ ] revert vs reset + reflog recovery
- [ ] cherry-pick, stash, bisect
- [ ] conflict resolution (merge vs rebase)
- [ ] branching strategies + branch protection + tags/SemVer
