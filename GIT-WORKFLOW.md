# PRS Git Workflow

## Purpose

Maintain a continuous safe git backup trail for PRS. Every useful, stable change should become a clear local save point and should normally be pushed to GitHub so the repository always has the latest recoverable backup.

This workflow is for AI agents working inside this repository.

**Remote:** https://github.com/JinJanMcFlan/PRS.git  
**Branch:** main

---

## Required Pre-Work Check

Before changing files, run:

```powershell
git status
```

Read the result before making edits. Do not assume the working tree is clean.

## Dirty Tree Rule

If `git status` shows files that are modified, deleted, renamed, staged, untracked, or otherwise already changed:

1. Report the changed files to the user.
2. Stop work.
3. Continue only if the user explicitly says to continue with the dirty tree.

Do not silently build on top of unknown changes.

## Commit Rule

After a stable useful change:

1. Run `git status`.
2. Summarize the changed files for the user.
3. Commit the change with a clear message.
4. Push the commit to `origin/main`.
5. Confirm the latest commit hash, branch, and whether the working tree is clean.

## Push Rule

Every commit should normally be pushed after it is created:

```powershell
git push origin main
```

If a push fails, report that clearly — do not pretend the checkpoint is safely backed up online.

## Restore Rule

Never run destructive rollback commands without explicit user approval:

```powershell
# NEVER run these without approval:
git reset --hard
git clean -fd
git checkout -- path/to/file
git restore path/to/file
git push --force
git branch -D branch-name
```

If restoration is needed: explain what will be restored, what will be lost, ask for approval first.

## Review-First Rule

If something breaks:
1. Do not immediately overwrite or roll back.
2. Run `git status`.
3. Show the changed files.
4. Explain the likely cause.
5. Propose the smallest safe fix.
6. Fix forward when practical. Roll back only after explicit approval.

## Commit Message Format

Short, specific, imperative:

```
Add CORE-NARRATIVE first draft
Update CURRENT-STATE with full audit results
Fix deal structure terms in narrative doc
Add investor playbook Q&A
Checkpoint stable pitch draft v1
```

Avoid: `updates`, `changes`, `fix stuff`, `wip`

## Common Agent Prompts

**Start Work Safely**
```
Before changing anything, run git status. If the tree is dirty, show me what changed and stop.
```

**Checkpoint Current Work**
```
Summarize the current changes, commit with a clear message, push to origin/main, and confirm the commit hash and clean status.
```

**Inspect What Changed**
```
Show me what files changed and summarize the actual edits before doing anything else.
```
