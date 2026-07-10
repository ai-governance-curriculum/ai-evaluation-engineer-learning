# exercise-01: Release-Gate Design for a Real Product

**Estimated effort:** 3 hours

## Objective

Design a **release-gate** for a stated AI product surface. The gate must have explicit hard-vs-soft criteria, pre-registered pass thresholds, rollback and rollforward hooks, and *at least three deployment-surface-specific variants* (e.g., T0 pilot, T1 canary, T2 staged production — or the tiering used by your program). This is the applied output of chapter `01`, and it is the input the rest of the module builds on.

## Prerequisites

- Chapter `01-release-gate-architecture-in-one-view.md` (this module).
- Mod-101 chapter `06` (deferral contract) and mod-102 chapter `06` (evidence-contract producer side).
- A concrete product to design against. Options:
  - An AI system your organisation actually operates. Strong preference — the design is more instructive when the deployment surface is real.
  - A public-domain reference system (an internal LLM assistant, a customer-intent classifier, a RAG-based question-answering surface, or a code-completion service). Whichever you pick, name it, name the deployment surface, and name the tier taxonomy explicitly.

## Problem statement

Pick a system and design the standing release-gate for it. Write down the six components chapter `01` calls out — scope, pre-registered criterion set, evidence bundle, decision record, rollback / rollforward contract, post-market handoff — and produce a working criterion set for one release cycle. Then produce the *delta* between three deployment-surface variants, criterion by criterion.

The design is defensible if a peer reading it can (a) tell what makes a criterion hard vs. soft, (b) reconstruct what the on-call assurance engineer does at approval, and (c) tell what happens on rollback.

## Requirements

Produce four artefacts.

### 1. `system-scope.md`

- System-in-scope: name, brief description, intended use, out-of-scope uses.
- Deployment-surface taxonomy for the system: at least three tiers (name them per your program, e.g., T0 / T1 / T2, or "pilot / canary / prod"). For each tier, name the user population, reversibility profile, and monitoring-baseline expectations.
- The regulatory and framework surface applicable to the system: NIST AI RMF (always), ISO/IEC 42001 (always in this program), EU AI Act (only if in-scope by jurisdiction and use), sector rule (if applicable), values baseline (mod-101 chapter `05`).

### 2. `gate-criteria-v1.md` (or CSV / spreadsheet)

The pre-registered criterion set for one release cycle. Use the schema from chapter `01`:

| Field                 | Content                                                                                       |
| --------------------- | --------------------------------------------------------------------------------------------- |
| Criterion identifier  | Stable ID (`GATE-…`).                                                                          |
| Threshold             | The pass level as a number *and* the estimator.                                               |
| Hard / soft           | With a one-line justification (statute-tied, harm-tied, internal-goal).                        |
| Evidence pointer      | Owner peer track and the artefact ID the gate walker resolves.                                 |
| Framework citation    | ISO/IEC 25059 dimension (foreshadow chapter `02`), NIST AI RMF MEASURE sub-category, EU AI Act article, ISO/IEC 42001 clause. |

Coverage minima:

- **At least 8 criteria** total. If you have fewer than 8, the gate is under-covering; if you have more than about 20, you are probably duplicating rubric rows.
- At least **2 hard criteria** and **2 soft criteria** — the taxonomy has to be non-trivial.
- At least **one criterion tied to a statute obligation** (EU AI Act, sector rule, or FDA GMLP) — the hard/soft justification for this criterion has to cite the statute.
- At least **one criterion whose justification is "internal goal above the hard-floor"** — a soft criterion that improves quality but does not by itself discharge a statute.
- The criterion set version is tagged.

### 3. `gate-variants.md`

For each tier in your taxonomy, describe the *delta* against the previous tier's criterion set:

- Which criteria are added or removed at this tier.
- Which criteria change threshold (with a written justification tying the change to the tier's reversibility profile or user-population).
- Which soft criteria are promoted to hard (or vice-versa).
- What the tier-specific rollback profile looks like (RTO, authorisation, reverse-drill cadence).

At least three tiers. Delta is *explicit* — a table, not prose. Skipping a tier requires an exception (foreshadow chapter `05`); the variant document names this.

### 4. `rollback-rollforward-contract.md`

The reversal contract for the highest tier your design covers. Sections:

- Rollback triggers, with the specific metric, threshold, persistence window, observer, and authoriser (foreshadow chapter `05`'s runbook).
- Rollback procedure (config swap / model swap / feature-flag / traffic-shift), the tested RTO, and the reverse-drill cadence.
- Rollforward triggers and procedure, with the safeguards (rollforward test-set, wall-clock ceiling, disqualifying trigger classes — supply-chain, cybersecurity, serious-incident).
- Signer and RACI. Where does authorisation escalate?

## Starter guidance

- **Start from the deployment surface, not from the framework.** The framework columns fill in *after* the criteria are stated; if you start from the framework, you will write generic criteria and lose specificity to the product.
- **The hard/soft justification is not "important vs. nice-to-have."** It is *statute-tied and non-negotiable* vs. *quality-improving and dispositioned but non-blocking*. Ambiguous justifications become audit findings.
- **Threshold *and* estimator.** A threshold without an estimator (e.g., "F1 ≥ 0.85" with no interval or set specified) is not a criterion. It is a wish.
- **Pre-registration means before the run.** If you find yourself tuning the threshold after seeing the release candidate's numbers, you are not designing a gate — you are writing a post-hoc rationalisation.
- **Do not sneak the rubric here.** This exercise stops at the criterion set. Chapter `02`'s rubric extends the criteria into the columnar view.
- **Reverse-drill.** Even in an academic exercise, sketch what a reverse-drill would look like: which team runs it, on what schedule, against what surface.

## Acceptance criteria

You have succeeded if:

- `system-scope.md` names the system, tier taxonomy, and applicable framework surface with no hand-waving.
- `gate-criteria-v1.md` contains at least 8 criteria, with the coverage minima above, each with a threshold *and* estimator *and* hard/soft justification.
- The framework citations use exact identifiers (e.g., `NIST AI RMF MEASURE-2.5`, `EU AI Act Article 15(1)(a)`, `ISO/IEC 42001 clause 8.1`), not topical shorthand.
- `gate-variants.md` presents the deltas between at least three tiers in table form; each delta has a justification.
- `rollback-rollforward-contract.md` names triggers, procedures, RTO, reverse-drill cadence, and RACI for the highest tier covered.
- A peer reading the four artefacts can tell what the on-call assurance engineer does at approval, and what happens if a hard criterion fails after promotion.

## Stretch goals

- Extend the criterion set to cover **all six ISO/IEC 25059 dimensions** (functional adequacy, robustness, transparency, controllability, adaptability, appropriate use of data), previewing chapter `02`. Balance criteria per dimension.
- Add a **fifth tier** for a regulated-sector deployment (SR 11-7 model-risk, FDA GMLP, DORA) previewing mod-107. Justify the new criteria that appear only at that tier.
- Draft the **decision record template** the gate walker will populate: sections, required fields, signer list, and how the record cites the criterion set version.
- Draft a **reverse-drill runbook** you would use to actually test the rollback procedure against a stubbed production surface. Include success criteria for the drill itself.
- Prepare a **defence memo** — one page — arguing why one contested hard-criterion (fairness, judge quality, threshold) is where you drew the line, previewing mod-102 chapter `06`'s contested-routing rules.
