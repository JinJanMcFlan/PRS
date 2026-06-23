# OCC Current State - PRS Snapshot

**Snapshot type:** PRS business-context summary, not the authoritative OCC project state.
**Source location audited:** `D:\studio-tools\OCC\_system`
**Audit date:** 2026-06-23

For authoritative OCC state, return to the OCC repository.

## Source files present

- `APP-VISUAL-DIRECTION.md`
- `CURRENT-STATE.md`
- `DECISIONS.md`
- `GIT-WORKFLOW.md`
- `MAINORCH-HANDOFF.md`
- `OCC-ALIGNMENT.md`
- `PROJECT-SOURCE-MANIFEST.md`
- `RESEARCH-DIRECTION.md`
- `RESEARCH-OPERATIONS.md`
- `WORKFLOW-ROLES.md`

## Current purpose

OCC means Overseer Command Center. It is a standalone, IDE-scale AI orchestration app. It does not live inside VS Code, though it may ship a VS Code connector plugin. The app is the brain; models are swappable drivers.

OCC is intended to be provider-agnostic, local-first where useful, and driven by deterministic routing over capability, cost, urgency, user presence, and output-quality factors.

## Active workstreams

- Router reconciliation is complete, but core router implementation remains blocked until a MainOrch-approved Router Build Package exists.
- Wave 1 external research is complete and audited.
- Base UX desktop shell exists in `apps\occ-desktop\`.
- Base UX Command Thread is complete and mounted in the shell, with one manual keyboard acceptance check still remaining.
- Founder Research Briefings are authorized to discuss completed research findings.
- Further research runs R10-R21 are conditional and not approved/launched.

## PRS implications

- PRS may position OCC as the active product direction, but should avoid claiming a finished product, active users, finalized pricing, or launched provider integrations.
- PRS language should emphasize the stable direction: standalone orchestration app, provider-agnostic routing, local-first folder awareness where useful, and a survival layer over changing AI tools.
- Website and founder materials should not make AGI claims, provider-specific commitments, or implementation promises unsupported by OCC source material.
- HKB should be treated as terminated as the active project direction and as a possible OCC parts donor only where OCC source material supports that framing.

## Major constraints

- No OCC v1 scope is defined.
- No real provider, model, cost, API, persistence, database, filesystem binding, VS Code connector, or router-core implementation is live.
- Model/provider registry information is stale and must be refreshed at build time.
- No timelines and no "MVP" language unless the founder explicitly authorizes it.
- Split-gate interpretation and semantic-feedback governance remain pending decisions.

## Missing Information

- Founder-approved OCC v1 product scope.
- Public-facing pricing and packaging.
- Current market evidence for competitor pricing and model/provider cost claims.
- Launch criteria and near-term business milestone language.
- Which OCC visuals or screenshots are approved for external website/fundraising use.
