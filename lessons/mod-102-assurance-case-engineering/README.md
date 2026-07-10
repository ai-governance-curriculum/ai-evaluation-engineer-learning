# mod-102-assurance-case-engineering: Assurance-Case Engineering for AI Evaluation Evidence

Installs the assurance-case discipline for the AI Evaluation Engineer track: **GSN**, **CAE**, and **SACM** as the notations, defeater / mitigation and diversity-of-evidence as the audit shape, and evidence contracts as the interface into the peer tracks that produce each leaf's evidence.

**Estimated effort:** 14 hours

## Learning objectives

- Author a Goal Structuring Notation (GSN) assurance case for a concrete AI release decision: top-level goal, strategies, sub-goals, solutions (evidence nodes), context, assumptions, and away-goals.
- Author the same case in Claim-Argument-Evidence (CAE) form and reason about when GSN, CAE, or a hybrid pattern is the right shape.
- Persist an assurance case in the OMG Structured Assurance Case Metamodel (SACM) so it can be versioned and diffed across release cycles.
- Audit a submitted assurance case for undermining evidence, unstated assumptions, insufficient diversity of evidence, and defeater-and-mitigation patterns.
- Route each claim-branch to the owner peer track and record the evidence contract (what artefact, at what version, with what statistical warrant).

## Lecture chapters

1. [`01-why-assurance-cases.md`](01-why-assurance-cases.md) — Why an assurance case is the shape a release-gate decision needs; how it differs from a report, checklist, or story; the three notations (GSN, CAE, SACM) at a glance; the standard top-level shape of an AI-release case.
2. [`02-gsn-for-ai-release-decisions.md`](02-gsn-for-ai-release-decisions.md) — The seven GSN node types and two link types (per the GSN Community Standard v3), a worked release-case walkthrough, and the failure modes an experienced reviewer catches at draft.
3. [`03-cae-and-shape-choice.md`](03-cae-and-shape-choice.md) — CAE's three primitives, five argument building blocks, and side-warrants; the same worked release-case in CAE; the CAE Blocks + Defeaters pattern; criteria for choosing GSN, CAE, or a hybrid.
4. [`04-sacm-persistence-and-diff.md`](04-sacm-persistence-and-diff.md) — OMG SACM 2.2 packages and the classes you actually use; persisting a GSN or CAE case as SACM; versioning `ArtifactAsset` / `Artifact` / `ArgumentPackage`; diffing between release cycles; queries that fall out of SACM.
5. [`05-auditing-an-assurance-case.md`](05-auditing-an-assurance-case.md) — Five audit passes (structural well-formedness → unstated assumptions → defeaters → diversity of evidence → residual-risk / confidence-in-argument). Rushby's confidence-in-argument framing. Audit-ledger schema and common findings.
6. [`06-evidence-contracts-and-routing.md`](06-evidence-contracts-and-routing.md) — Evidence-contract row schema; routing by owner peer track (analyst L15, risk engineer L25, AI-eval L30, model-eval L30, MLSec L35, third-party); contested branches (fairness, judge quality, threshold); freshness, cadence, escalation; contract as a governed artefact.

## Structure

- `01-…md` … `06-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapter `01`** — read once, then keep as the motivation and vocabulary anchor for the module.
- **Chapters `02` + `03`** — read together and translate the worked release-case between GSN and CAE by hand before doing exercises `01` and `02`. The point is to feel the two notations as one underlying graph.
- **Chapter `04`** — read after you have a GSN or CAE case drafted; SACM persistence is easier to internalise when you have a specific case to persist. Exercise `03` is the applied output.
- **Chapter `05`** — read after `04`; the audit is easier when the target is persisted and diff-able. Exercise `04` runs the five-pass audit against a case you audit rather than authored.
- **Chapter `06`** — read alongside mod-101's deferral contract; the evidence contract is a specialisation of that contract to the leaves of an assurance case. Exercise `05` produces the contract set for the case authored in exercises `01`–`03`.

## Dependencies

- Requires mod-101 (release-assurance position, framework overview, deferral contract).
- Consumed by mod-103 (release-gate architecture), mod-104 (evidence pipeline), mod-105 (cards), mod-109 (third-party evaluator interface), and the project-101 capstone.
