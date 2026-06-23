# Git Workflow — PRS

This document defines git safety rules for PRS. The goal is reliable recovery checkpoints: the human should always be able to get back to a known good state if something breaks.

Verified PRS repository context as of 2026-06-23:

- Repository root: `D:\Deuterium3D\PRS`
- Branch: `main`
- Remote: `origin` -> `https://github.com/JinJanMcFlan/PRS.git`

Do not alter the remote or branch unless the founder explicitly asks.

---

## Required pre-work

Before changing any files, inspect repository state:

```
git rev-parse --show-toplevel
git status
git branch --show-current
git remote -v
```

Confirm:
- The repository root is `D:\Deuterium3D\PRS` — not a parent or sibling.
- The branch is `main`.
- The remote exists and points to `https://github.com/JinJanMcFlan/PRS.git`.
- The working tree state is understood.

---

## Dirty tree handling

If `git status` shows changes before your edits begin, assess what they are:

- **Known, explicitly authorized in-progress work:** continue — these are expected.
- **Unknown or unexpected changes:** stop. Report the changed files and do not proceed until the human explicitly authorizes continuation.

Do not silently build on top of unknown changes. They may be another agent's checkpoint or an unfinished task.

---

## Commit rule

After a human-approved stable change, create a focused commit.

When committing:

1. Run `git status`.
2. Summarize the changed files.
3. Stage only the relevant files — never blindly stage the entire repo.
4. Commit with a clear, specific message in imperative form.
5. Confirm the latest commit hash, branch, and whether the working tree is clean.

Use focused commits. One commit should describe one coherent checkpoint.

Commit message style — short, specific, imperative:
```
Add _system folder and governance docs
Initialize project as standalone git repo
Update CURRENT-STATE with research reconciliation notes
```

Avoid vague messages: `updates`, `changes`, `fix stuff`, `wip`.

---

## Push rule

If a verified remote exists, push the stable checkpoint by default unless the human explicitly says not to.

After confirming the remote is correct and the branch is correct, push. Report the push result and commit hash.

If no remote exists, commit locally and report that no online backup was made.

Never claim an online backup exists unless the push succeeded and the commit hash is reported.

If a push fails, report it clearly. Do not assume the work is safely backed up online.

---

## Destructive command rule

Never run destructive rollback, reset, checkout, restore, clean, branch deletion, or force push without explicit human approval.

This includes:
```
git reset --hard
git clean -fd
git checkout -- <path>
git restore <path>
git push --force
git branch -D <branch>
```

If something breaks:

1. Do not immediately overwrite or roll back files.
2. Run `git status`.
3. Show the changed files.
4. Inspect and explain the likely cause.
5. Propose the smallest safe fix.
6. Prefer fix-forward.
7. Wait for explicit approval before running anything destructive.

---

## General reusable prompts

### Start work safely
```
Before changing anything, confirm the git repo root, branch, and remote. Run git status. If you find unknown changes or the repo root is not what you expect, show me what you found and stop.
```

### Checkpoint and push
```
Stage only the relevant project files, commit with a clear message, then push to the verified remote. Show me the commit hash and push result.
```

### Inspect what changed
```
Show me what files changed and summarize the actual edits before doing anything else.
```

### Rollback review before action
```
Do not roll back yet. First show me the changed files, explain the likely cause, and tell me exactly what rollback command you would run. Wait for my approval.
```
