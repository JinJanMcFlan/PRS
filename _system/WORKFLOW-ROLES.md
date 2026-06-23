# Workflow Roles — PRS

This document defines roles, lanes, and handoff protocols for PRS. It is written to be read by an AI with zero prior context — it states the obvious on purpose. Collapsing these lanes is what breaks projects.

This PRS copy keeps the reusable three-layer workflow, but applies it to the PRS business strategy and communications workspace.

PRS-specific boundaries:
- PRS `_system` files are the minimal ChatGPT source set.
- PRS owns business strategy, communications, website strategy/review, networking context, founder operating information, and cross-project business snapshots.
- OCC and TRC repositories remain authoritative for their own execution.
- Claude Code and other VS Code agents execute bounded tasks only; they do not become PRS orchestrators.

---

## Source of truth

Disk is the source of truth. ChatGPT project sources are mirrors. Only the disk copy is edited. When a file changes on disk, the human manually re-uploads it to the relevant AI project containers. This is a deliberate manual step.

Claude Code is an execution agent. It receives task-specific execution prompts only. It is not an orchestration chat and does not receive a full project-source mirror.

Work flows down. Problems flow up.

Default flat. Deepen only on overflow.

## Named-chat authority and continuity

Creating a named orchestration chat authorizes it to begin and continue its assigned lane with Jonathan. Its opening handoff is a working brief, not a request for immediate MainOrch approval, an immediate return handoff, or immediate prompt creation. It begins by discussing and developing the work with Jonathan in normal human terms.

The chat remains responsible for the original task through planning, execution coordination, review, iteration, and recommended next steps as the scope requires. Completing one phase — such as orientation, planning, organization, a specification, or an execution prompt — does not complete the original task. It returns a MainOrch handoff early only for a genuine cross-lane decision, material blocker, scope conflict, or meaningful discovery requiring higher-level review. Work already authorized by creating the chat does not require routine re-approval.

---

## Roles

### MainOrch

The top orchestrator for the project. One per project. Holds the full project direction. Decides what is delegated and to what level. Direction-deciding work (where the project is going, course-correction, final calls) stays here — it is not delegated down.

MainOrch is the final project and product authority.

### SubOrch

Handles one focused design, planning, or research problem too large for MainOrch to hold alongside everything else. Collaborates with Jonathan and remains active through its original scoped task as needed. It hands work back to MainOrch when it reaches a genuine decision-ready, execution-ready, final, or materially blocked result — not merely after an early planning, organization, or drafting phase.

A SubOrch may remain one focused chat. A TaskManager layer is only needed when there are two or more TaskOrchs that need coordination. A one-chat task can remain at MainOrch, SubOrch, TaskOrch, or direct-execution level depending on its actual scale.

### TaskManager

Exists only when a task is big enough to need two or more TaskOrchestrators that must be coordinated. Do not create a TaskManager unless that threshold is met.

### TaskOrch

The chat the human converses in about a specific task. Manages its TaskRunners. Makes decisions within its task scope.

### TaskRunner

Writes the actual prompts to execution agents. One task. Iterates with the execution agent (prompt → result → check → next prompt) and continues until the original assigned task is complete, materially blocked, or explicitly transferred or re-scoped by MainOrch.

Completing a planning, setup, or prompt-writing phase is not task completion. When they belong to its scope, the TaskRunner continues through execution follow-up, result audit, correction rounds, and next-step coordination.

TaskRunner-owned work must not be delegated to an execution agent:
- Prompt writing
- Research-prompt drafting
- Orchestration planning
- Returned-result auditing
- Next-step sequencing

These stay in the correct orchestrator chat. A TaskRunner is a prompt writer and result auditor — it is not an execution agent.

### ResearchOrch (optional)

A specialized SubOrch for high-level research direction. Handles hypothesis framing, evidence review, synthesis, decision-ready handoffs, and research department coordination.

ResearchOrch does not write worker research prompts itself. Named research TaskRunners do that. ResearchOrch stays at the direction and synthesis level.

### Execution agents

Execution-only. Receive one self-contained prompt, do the file or code work, and return the result as evidence.

Execution agents must not be handed broad orchestration docs and told to figure out the mission. Context is distilled by the orchestrator before it reaches the agent.

Named chats are orchestration chats only. VS Code agent runs are unnamed execution prompts. Claude Code is one execution-agent option; it is not an orchestration chat or project-source mirror.

---

## The direct execution lane

When a task is fully specified, bounded, and needs one execution pass, MainOrch, SubOrch, or TaskOrch may send an execution prompt directly to a VS Code agent without creating a TaskRunner.

Use a TaskRunner only when the task genuinely requires multiple execution rounds, prompt revisions, or active result-checking between rounds.

---

## Coding-agent execution and escalation

Orchestrators resolve ambiguity, missing requirements, architecture choices, research questions, and scope tradeoffs before an implementation prompt reaches a coding agent. A coding agent must not be handed open-ended problems or broad orchestration context.

Coding agents receive exact bounded specifications and execute within that scope. They do not conduct open-ended research, alter architecture, or silently expand scope without orchestrator authorization.

Coding agents may escalate upward when they find a contradiction, unmet assumption, material risk, or evidence-backed improvement opportunity within their assigned work. Escalation must include: the evidence, expected impact, affected files or boundary, and a recommended next decision. Research guardrails and existing decisions are not hard ceilings — credible adjacent improvements may be surfaced for orchestrator review, but must not be acted on without authorization.

One bounded implementation slice may use the direct execution lane. When two or more substantial code workstreams are truly independent and safely parallelizable, MainOrch creates separate implementation SubOrchs before assigning parallel execution agents. Do not create parallel lanes when they would edit overlapping files or depend on unresolved shared contracts.

---

## Mandatory prompt-delivery protocol

Before every copyable prompt, the orchestrator must provide a separate plain-text destination block.

The destination block must state:
- Exact destination (which tool, which chat, which agent)
- Platform (VS Code, ChatGPT, etc.)
- Purpose of this specific prompt
- Where not to paste it

The destination block must remain outside the copyable prompt. It is context for the human, not content for the agent.

---

## External research-run naming and retrieval

When a human manually launches research in an external research system that has its own project, folder, or chat history, the research run must receive a stable, searchable title before it is launched.

Use this format:

`R{queue ID} — {short plain-English research title} [{Project Code}]`

Example:

`R1 — General Router Task Facts [OCC]`

Rules:

- The queue ID must match the approved research queue and must not change later.
- Use the same queue ID and core title in the external research chat, the returned-result handoff, and the related disk research record. Adjust only file-safe characters when needed for filenames.
- Keep temporary status, provider name, model name, and date out of the title. Those belong in the queue record or result metadata, not the stable research title.
- A follow-up run keeps the original ID and title, then adds a clear suffix before the project code. Example: `R1 — General Router Task Facts — Follow-up 1 [OCC]`.
- The title must describe the research question in plain language so a human can find the run later without opening it.

### External research capacity management

External research providers may have separate limits for concurrent runs, rolling time windows, daily usage, weekly usage, model choice, file size, or account tier.

Before launching a research run, the responsible orchestrator must identify the provider's currently available capacity from the provider interface when possible.

For each external research provider, keep a lightweight queue record containing:

- Current observed concurrent-run capacity
- Current observed reset or refresh time, when shown
- Active research runs
- Approved ready-to-run research items
- Items blocked by dependencies or missing inputs
- Whether a provider limit is confirmed, estimated, or unknown

Use available capacity efficiently:

- Launch up to the currently available number of approved, independent research runs.
- Do not launch dependent runs before their required inputs exist.
- Do not invent research merely to fill unused capacity.
- Prefer the highest-priority ready items that produce a clear decision, evidence artifact, or required dependency.
- When a run finishes or a usage window refreshes, launch the next approved ready item.
- Preserve the provider's stable research-run title so the result can be found later.

Provider limits are operational constraints, not architecture decisions. Do not hardcode a provider's observed quota as a permanent project rule.

### Project-specific artifact labels

A project-specific research-operations protocol may define internal `A#`, `B#`, and `D#` artifacts alongside external `R#` research runs.

- R-runs retain the stable external title format defined above and are used for externally launched research.
- A/B/D artifacts are normally internal records and do not require external research chats.
- This does not alter the existing role boundaries: research direction stays with ResearchOrch, prompt drafting and returned-result auditing stay with TaskRunners, and execution agents remain execution-only.

---

## Completion, handoff, and closure

Completion is not the same as closure. A named orchestration chat does not reach closeout merely by stating that the chat is done. It reaches closeout only when its original task is complete, it is materially blocked outside its scope, or MainOrch explicitly transfers or ends the task.

At real closeout, the chat provides what was completed and the supporting result or evidence; unresolved items or blockers; the recommended next step; and the recommended owner. When the result affects project direction, sequencing, or another lane, it also provides a concise MainOrch handoff with recommended next steps. For a fully self-contained result with no MainOrch relevance, it explicitly states why a MainOrch handoff is unnecessary. The chat may state that it is ready for closure, but Jonathan or MainOrch decides whether it is actually closed.

---

## How a task flows

1. Orient and begin. A fresh chat reads the project files to confirm where the project is, then begins collaborative work with Jonathan. State lives in files; the chat is today's working memory.
2. MainOrch decides whether work is direction (stays here) or production (goes down).
3. MainOrch breaks down a production task and decides whether it stays flat or needs a SubOrch.
4. SubOrch (only if needed) works one focused problem with Jonathan and hands back up only when a genuine decision-ready, execution-ready, final, or materially blocked result is ready.
5. TaskOrch (only if needed) manages runners under it.
6. TaskRunner writes a self-contained prompt, sends it to an execution agent, and continues through the original task until it is complete, materially blocked, or explicitly transferred or re-scoped by MainOrch. It then provides the required closeout.
7. Execution agent executes and returns the result.
8. Results flow back up when a real decision, blocker, or completed handoff is ready. The orchestrator checks returned work against project direction. Approval is the signal for the human to authorize any repository or deployment actions.

---

## Failure mode this prevents

Collapsing the lanes. An orchestrator chat writing a prompt as if it is the execution agent. An execution agent handed the orchestration brain files and told to figure out the mission. Each layer hands down a distilled instruction and hands up a result. Context is not inherited wholesale across layers.
