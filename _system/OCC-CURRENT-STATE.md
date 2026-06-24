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

## Commercial and trust direction

OCC's internal alpha quality bar is sellable: a user should be able to request a bounded build, such as a creatively distinct simple game based on a reference, and OCC should materially progress or complete it autonomously while the user is away.

This is an internal quality direction, not a finalized v1 specification or public capability claim.

Preferred commercial direction:

- One OCC account and one setup.
- Managed multi-provider access.
- Clear user-controlled budget.
- Optional customer API keys and local AI.
- Customer-provided API/local capacity should reduce OCC's fee/take for that usage and may receive user-selected routing preference.
- Routing must optimize for customer budget, quality, outcome, and stated preferences rather than undisclosed OCC-margin optimization.

Launch-critical controls:

- Visible spend.
- Forecasts and explanations.
- User-set limits.
- Project, task, and workspace budgets.
- Approval gates for costly work.
- Alerts, hard stops, and kill-switch behavior.

There is no unlimited managed frontier-model promise.

Security needs costed later phases: founder/alpha baseline, launch hardening, then high-security local/infrastructure operations. Current baseline gaps include password management and broader operational security maturity.

All OCC pricing, integrations, implementation, public packaging, and external security language remain unfinalized unless the OCC repository records a later authoritative decision.

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
- PRS may discuss the sellable-alpha internal bar, managed-usage direction, optional customer-owned capacity, customer-first routing, budget controls, and security phases as current direction, but must not present them as implemented capability, finalized pricing, or external assurance.

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
- Verified model/provider pricing, infrastructure costs, support costs, legal/tax/accounting/security estimates, customer-acquisition assumptions, and margin cases.
- Launch criteria and near-term business milestone language.
- Costed budget-control requirements and costed security phases.
- Which OCC visuals or screenshots are approved for external website/fundraising use.
