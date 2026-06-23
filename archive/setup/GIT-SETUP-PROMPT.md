# VS Code Agent Prompt — Initialize PRS Git Repository

**Use this prompt with a VS Code agent (Claude Code / Sr tier) to initialize the PRS folder as a git repository and push all current files to GitHub.**

---

## Context

The PRS project folder at `D:\Deuterium3D\PRS` contains the investor pitch pipeline documents for ProjectARC / Deuterium3D. A GitHub repository has been created at:

```
https://github.com/JinJanMcFlan/PRS.git
```

The repository is currently empty. This folder needs to be initialized as a git repo and all current files pushed as the first commit.

---

## Current Files in D:\Deuterium3D\PRS\

- `CURRENT-STATE.md` — project status, master reference, build order
- `WORKFLOW-ROLES.md` — how work flows through the AI pipeline
- `GIT-WORKFLOW.md` — git safety rules for all agents
- `CORE-NARRATIVE.md` — source of truth for all pitch materials (tentative, pending approval)
- `GIT-SETUP-PROMPT.md` — this file

---

## Prompt for VS Code Agent

```
You are setting up git for the PRS project. Follow every step exactly. Do not skip steps. Do not run destructive commands.

Working directory: D:\Deuterium3D\PRS
Remote: https://github.com/JinJanMcFlan/PRS.git
Branch: main

Step 1 — Check current state
Run: git status
If git is already initialized and the tree has uncommitted changes, show me what they are and stop. Wait for instructions.
If git is not initialized, continue to Step 2.

Step 2 — Initialize the repository
Run: git init
Run: git branch -M main

Step 3 — Add the remote
Run: git remote add origin https://github.com/JinJanMcFlan/PRS.git

Step 4 — Stage all files
Run: git add .
Run: git status
Show me what files are staged before committing.

Step 5 — First commit
Run: git commit -m "Initialize PRS — core project documents and narrative"

Step 6 — Push to GitHub
Run: git push -u origin main
If the push fails, show me the exact error message and stop. Do not attempt workarounds.

Step 7 — Confirm
Run: git status
Run: git log --oneline -5
Report: the latest commit hash, the branch name, and whether the working tree is clean.
```

---

## After This Is Done

The repo is live. Future agents follow the rules in `GIT-WORKFLOW.md` for all subsequent commits and pushes.

The next task after git setup is building the investor Playbook — see `CURRENT-STATE.md` for the full deliverable list and build order.
