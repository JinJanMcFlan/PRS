# Workflow Roles — How Work Flows Through the Pipeline

**What this file is:** the reference for how chats are structured and how a task moves from idea to execution. It exists because the layers below are easy to confuse, and confusing them is what breaks projects — an orchestrator chat that writes a prompt as if it *is* the VS Code agent, or a VS Code agent handed the brain files and told to figure out the mission. This document keeps the lanes clear.

It is written to be read by an AI with zero prior context, so it states the obvious on purpose.

---

## The three layers

There are three distinct layers. They must not be mixed.

### Claude Orchestrator
- Strategy, audit, and re-anchoring. Decides direction; catches drift.
- Has direct file access (via MCP) for reading and, when something is wrong, directly fixing files.
- All Claude chats for a project live inside the same **Claude Project** — a named container in Claude.ai, not a folder on disk. That project holds key files, manually added and manually updated when needed.
- Can write a specialized file directly into the ChatGPT project sources when a ChatGPT chat needs guidance the shared files don't carry.
- Used **sparingly** — Claude.ai chat and Claude Code share one usage pool, so every orchestration chat spends the same budget Claude Code draws from. Use Claude to orchestrate and audit (where its context is worth the spend); push the conversational legwork to ChatGPT.

### ChatGPT orchestrator chats
- The conversational build layer. Each chat has one defined job (MainOrch, SubOrch, TaskOrch, TaskRunner).
- All ChatGPT chats for a project live inside the same **ChatGPT Project** — a named container in ChatGPT, not a folder on disk.
- Reads project files from attached files or the ChatGPT project sources.
- Manages context for its task, makes decisions within its scope, and writes distilled prompts when VS Code execution is needed.
- Conversational thinking and prompt writing only. It executes nothing itself.

### VS Code agents
- Execution only. Receives one self-contained prompt, does the file/code work, returns the result.
- Has full drive access.
- Reads no orchestration docs. It is told exactly what to do.
- Tiers are just which AI does the work: Sr = Claude Code (multi-file, architecture-aware), Mid = Codex / Deepseek (bulk well-specified work), Jr = small / free / local AIs (small targeted edits).

---

## The shared project files

The project's living files exist in three places at once:

1. **Claude project (claude.ai)** — uploaded into the Claude Project sources.
2. **ChatGPT project sources** — the same files, uploaded into the ChatGPT Project.
3. **The project on disk** — the source of truth, which VS Code agents access directly.

The disk copy is the real one. The two AI-project copies are mirrors of it. Only the disk copy is edited; the two mirrors are then refreshed from it. Only orchestrator chats write the prompts that update the files, and updates happen on disk after the orchestrator approves. The human then manually re-uploads the changed files into the Claude and ChatGPT projects. This is a manual process, not automated.

---

## The chats — what each one is

- **MainOrch** — the top orchestrator for a project. One per project. Holds the full project direction, decides what gets delegated and to what level. Direction-deciding work (where the project is going, course-correction) is the orchestrator's *own* job and stays here — it is not delegated down.
- **SubOrch** — handles one focused design or planning problem too large for MainOrch to hold alongside everything else. Produces a clear output (a doc, a spec, a decision) and hands it back up. If a SubOrch has only one task under it, it collapses straight into being the TaskManager — no empty layer.
- **TaskManager** — exists only when a task is big. "Big" means it needs **2 or more TaskOrchestrators** to write the volume of prompts required. The TaskManager coordinates them.
- **TaskOrch** — the chat the human actually converses in about a task and its runners. Manages its TaskRunners.
- **TaskRunner** — writes the actual back-and-forth prompts to the VS Code agents. One task. It iterates with VS Code (prompt → result → check → next prompt) until the task is fully done, then writes a summary and closes.

---

## The pipeline — how a task flows

1. **Orient.** A fresh chat reads the project files directly (or is given them) to confirm where the project is. State lives in files; the chat is just today's working memory.
2. **Claude Orchestrator** decides whether the work is *direction* (strategy/audit — stays here) or *production* (a deliverable — goes down).
3. **ChatGPT MainOrch** takes a production task, breaks it down, and decides whether it stays flat (straight to a runner) or needs a SubOrch.
4. **SubOrch** (only if needed) works one focused problem, produces its output, hands back up.
5. **TaskOrch** (only if the task is big enough to need 2+ runners) manages the runners under it.
6. **TaskRunner** writes a self-contained prompt, sends it to a VS Code agent, and goes back and forth with that agent — prompt, result, check, next prompt — until every prompt the task needs is done. It commits stable changes locally as it goes (short-term safety). When the task is complete it writes a summary and closes.
7. **VS Code agent** executes each prompt and returns the result to the TaskRunner.
8. **The result flows back up.** The TaskRunner's summary climbs to the TaskOrch / MainOrch, and ultimately to the Claude Orchestrator. The orchestrator checks the returned work against the project's direction — if it drifted, that kickback is the audit, and the file gets reconciled. When the orchestrator approves, that approval is the trigger to push to GitHub — the hard milestone backup.

**Default flat, deepen one level only on overflow.** A task that fits one prompt and one worker bypasses straight to a runner — no SubOrch, no manager. Deepen only when the current level genuinely can't hold the work. The hierarchy grows on demand; it never locks you in.

**Work flows down, problems flow up.** A problem too big for a level climbs until it reaches a level that can decide it.

---

## Naming convention

Status prefix in square brackets, then role, then project acronym (all caps, 3 letters max — HKB, OCC, ORG):

- `MainOrch [ACR]`
- `([task]) SubOrch#N [ACR]`
- `([task]) TaskManager#N [ACR]`
- `([task]) TaskOrch#N [ACR]`
- `([task]) TaskRunner#N [ACR]`

Status prefixes: `[Complete]`, `[In Progress]`, `[Waiting]`. Prefix when the chat's status changes.

---

## Git — the safety trail

Git is the backup spine. Two distinct safety levels:

- **Commit + push as work happens (short-term safety).** The TaskRunner commits stable, useful changes locally as it works, with clear focused messages, and pushes to `origin/main` so the online copy is current. Markdown and creative files get committed the same as code.
- **Approval = hard milestone backup.** When work climbs back to the orchestrator and is approved, that approved state is the milestone. Approval is the human gate, not a git command.

Operating rules for any chat touching the repo:
- **Before changing files:** check `git status`. If the tree is dirty (modified, staged, untracked, etc.), report what changed and stop until the human says to continue. Don't silently build on unknown changes.
- **After a stable change:** summarize the changed files, commit with a clear message, push to `origin/main`, and confirm the commit hash, branch, and clean status. If a push fails, say so — don't pretend it's backed up online.
- **Never run destructive commands without explicit approval** — no `reset --hard`, `clean -fd`, `checkout --`, `restore`, `push --force`, or branch deletion. If a restore is needed, explain what will be restored, what will be lost, and ask first.
- **If something breaks:** don't roll back reflexively. Check `git status`, show the changed files, explain the likely cause, propose the smallest safe fix. Fix forward when practical; roll back only after approval.
- **Commit messages:** short, specific, imperative ("Add routing classifier", "Fix chat-naming counter"). Not "updates", "wip", "fix stuff".

---

## The failure mode this prevents

Collapsing the layers into one. An orchestrator chat writing a prompt as though it is the VS Code agent. A VS Code agent handed the orchestration files and told to figure out the mission. Each layer hands *down* a distilled instruction and hands *up* a result — context is not inherited wholesale across layers.

---

*Amendment note — ORG:* This document is a manually-operated proof-of-concept for the ORG (Organization) project. ORG will eventually give each layer its own system prompt; those system prompts do not exist yet. When ORG is built, this doc is the reference it grows from.
