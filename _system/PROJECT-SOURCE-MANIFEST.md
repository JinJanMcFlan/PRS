# PRS Project Source Manifest

This manifest is the exact manual upload list for ChatGPT project sources.

## Default read order

1. `PRS-ALIGNMENT.md`
2. `CURRENT-STATE.md`
3. `DECISIONS.md`
4. `WORKFLOW-ROLES.md`
5. `GIT-WORKFLOW.md`
6. `OCC-CURRENT-STATE.md`
7. `TRC-CURRENT-STATE.md`
8. `PROJECT-SOURCE-MANIFEST.md`

## Source policy

The `_system/` folder is intentionally minimal. It should contain only the stable PRS context a fresh orchestration chat needs.

Task-specific files outside `_system/` are added only when relevant to the task.

Do not upload these by default:
- `Human/`
- `archive/`
- Raw research files
- Historical pitch materials
- Working deliverables
- Website screenshots
- Partnership drafts

## Active `_system` files

| File | Purpose |
|---|---|
| `PRS-ALIGNMENT.md` | Defines PRS scope, boundaries, and cross-project role. |
| `CURRENT-STATE.md` | Live PRS operating state, active priorities, historical material, and missing information. |
| `DECISIONS.md` | Durable launch decisions and open decisions. |
| `WORKFLOW-ROLES.md` | Role definitions, lanes, handoff protocol, and execution-agent boundaries. |
| `GIT-WORKFLOW.md` | Safe git workflow for this PRS repository. |
| `OCC-CURRENT-STATE.md` | PRS-facing OCC context snapshot. |
| `TRC-CURRENT-STATE.md` | PRS-facing TRC context snapshot. |
| `PROJECT-SOURCE-MANIFEST.md` | This upload list and source policy. |
