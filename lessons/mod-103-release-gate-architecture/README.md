# mod-103-release-gate-architecture: Release-Gate Architecture for AI Products and Platforms

Builds the release-gate the AI Evaluation Engineer owns: **hard vs. soft criteria** with pre-registered pass thresholds and rollback / rollforward hooks; a rubric structured around **ISO/IEC 25059** quality dimensions and cross-mapped to **NIST AI RMF MEASURE**; outputs mapped into **ISO/IEC 42001** clauses 8 (operation) and 9 (performance evaluation); consumer contracts with the four peer tracks that produce the evidence; a runbook shaped by **SR 11-7** second-line effective challenge; and the dashboard the on-call assurance engineer reads at approval.

**Estimated effort:** 15 hours

## Learning objectives

- Design a release-gate for a stated AI product surface with explicit hard vs. soft gates, pre-registered pass criteria, rollback and rollforward hooks, and deployment-surface-specific gate variants.
- Structure gate rubrics around ISO/IEC 25059 quality dimensions (functional adequacy, robustness, transparency, controllability, adaptability, appropriate-use-of-data) and cross-map to NIST AI RMF MEASURE sub-categories.
- Map release-gate outputs to ISO/IEC 42001 clauses 8 (operation) and 9 (performance evaluation) so the assurance program's evidence flows into the AIMS.
- Delegate branch-level ownership: consumer contract with `ai-eval-engineer` (trace / trajectory / RAG / judge / online-eval evidence), with `model-evaluation-engineer` (statistical warrant, benchmark evidence, calibration), with `ai-risk-engineer` (safety-benchmark and red-team evidence), and with `ai-infra-security` (supply-chain / eval-set-security evidence).
- Author a release-gate runbook: incident-cutover, rollback triggers, deferred approvals, exception approvals, and the second-line effective-challenge convention (SR 11-7 shape).
- Author the release-gate dashboard the on-call assurance engineer reads before approving a release.

## Lecture chapters

1. [`01-release-gate-architecture-in-one-view.md`](01-release-gate-architecture-in-one-view.md) — The six-part standing procedure (scope, criterion set, evidence bundle, decision record, rollback/rollforward contract, post-market handoff); hard vs. soft gates; pre-registration; deployment-surface variants (T0 → T4).
2. [`02-iso-25059-quality-rubric.md`](02-iso-25059-quality-rubric.md) — The columnar rubric structured around ISO/IEC 25059's AI-adapted quality dimensions and cross-mapped to specific NIST AI RMF MEASURE sub-category identifiers; balance and coverage rules.
3. [`03-mapping-into-iso-42001-clauses-8-and-9.md`](03-mapping-into-iso-42001-clauses-8-and-9.md) — How the gate's outputs stream into ISO/IEC 42001 clause 8 (operation: 8.1–8.4) and clause 9 (performance evaluation: 9.1–9.3), so the AIMS auditor can walk the trail end-to-end.
4. [`04-consumer-contracts-with-peer-tracks.md`](04-consumer-contracts-with-peer-tracks.md) — The consumer-side evidence-contract row (extending mod-102 chapter `06`'s producer-side row) for the four peer tracks that feed the gate: `ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`, `ai-infra-security`.
5. [`05-release-gate-runbook.md`](05-release-gate-runbook.md) — Rollback triggers, rollforward triggers, incident cutover, deferred approvals, exception approvals, and the SR 11-7-shaped second-line effective-challenge convention.
6. [`06-release-gate-dashboard.md`](06-release-gate-dashboard.md) — The on-call assurance engineer's dashboard: five lanes (Scope, Evidence freshness, Pass criteria grouped by ISO/IEC 25059 dimension, Peer-track health, Runbook readiness), fail-states, silent-failure protection, and audience separation.

## Structure

- `01-…md` … `06-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapters `01` + `02`** — read together. `01` sets the six components of the gate; `02` writes the rubric that produces the criterion set. Do exercise `01` after `01` and exercise `02` after `02`.
- **Chapter `03`** — read after the rubric is drafted. The AIMS mapping is easier to internalise when you have a specific rubric to map. No exercise is dedicated to `03` on its own — it feeds every later exercise's framework-citation columns.
- **Chapter `04`** — read alongside mod-102 chapter `06`. The consumer-side row extends the producer-side row; the two together are what a peer signs. Exercise `03` produces the four consumer contracts.
- **Chapter `05`** — read after `04`. Contracts feed triggers; triggers feed the runbook. Exercise `04` produces the runbook and one table-top reverse-drill.
- **Chapter `06`** — read after `05`. The dashboard is the runbook made readable at a glance. Exercise `05` is the module capstone and stitches the four earlier exercises together.

## Dependencies

- Requires mod-101 (release-assurance position, framework overview, deferral contract) and mod-102 (assurance-case engineering).
- Consumed by mod-104 (evidence pipeline — the immutable substrate the gate reads), mod-105 (cards — a gate output), mod-106 (cross-jurisdictional mapping — the framework-citation columns are shared), mod-107 (sector-regulated overlays), mod-108 (deployment-tier gating), mod-109 (third-party evaluator interface — layered on top of the four peer contracts), mod-110 (post-market surveillance — the handoff target), mod-111 (GPAI systemic risk — additional runbook obligations), and mod-112 (program ownership). All three capstone projects consume this module.
