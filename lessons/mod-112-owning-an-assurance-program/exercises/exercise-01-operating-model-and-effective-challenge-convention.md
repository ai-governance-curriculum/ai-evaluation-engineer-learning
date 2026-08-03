# exercise-01: Operating Model and Effective-Challenge Convention

**Estimated effort:** 3 hours

## Objective

Author the **operating-model handbook** for a self-scoped AI-evaluation-assurance programme. The handbook is the single artefact a new joiner reads to learn how the programme runs, an auditor reads to walk the AIMS operating record, and the head of AI governance reads to confirm the reporting-line contract. It fixes the six-stage intake-to-decision cycle, the evidence-package versioning convention, the decision / exception / deferred-approval registers, the effective-challenge rotation borrowed from [Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm), and the escalation classes with the head of AI governance.

This exercise is design and authoring, not solving. Placeholder role-name fields and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the current [ISO/IEC 42001](https://www.iso.org/standard/81230.html) clause text, the current EU AI Act consolidated text, or organisation-specific data the exercise scope does not fix.

## Prerequisites

- Chapter [`01-operating-model-and-the-effective-challenge-convention.md`](../01-operating-model-and-the-effective-challenge-convention.md) — the six-stage cycle; MAJOR / MINOR / PATCH versioning; the three registers; the effective-challenge convention; the reporting-line contract with `head-of-ai-governance` (level 60); the classes of decision the programme may not decide alone.
- Familiarity with [`mod-101-release-assurance-position`](../../mod-101-release-assurance-position/) chapters `05` (the peer / prerequisite tracks) and `06` (the deferral contract).
- Familiarity with [`mod-103-release-gate-architecture`](../../mod-103-release-gate-architecture/) chapters `05` (the walker) and `06` (the on-call dashboard).
- Familiarity with [`mod-104-evaluation-evidence-pipeline`](../../mod-104-evaluation-evidence-pipeline/) chapter `06` (the signed assurance bundle the operating loop emits).
- Skim access to Federal Reserve [SR 11-7 on model risk management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and to [ISO/IEC 42001](https://www.iso.org/standard/81230.html) clauses 5 (leadership) and 9.3 (management review).

## Problem statement

Pin one worked organisation to draft against. The organisation must:

- **Have a specific AI-inventory count and tier distribution.** How many systems are in the inventory, how many sit at each deployment tier (T0 / T1 / T2 / T3 per `mod-108`), and roughly how many release-gate cycles the programme runs per month at steady state. The scope changes the operating model — a programme running two cycles per month cannot run the same rotation as one running twenty.
- **Have a specific programme-team size.** Number of assurance engineers, whether there is a dedicated on-call rotation coordinator, whether there is a dedicated assurance-programme analyst who liaises with the analyst function, and where the programme sits in the reporting line (typically reporting to the head of AI governance at level 60).
- **Have a specific jurisdictional and sector posture.** Which markets the organisation places systems on, whether any of them are EU markets (bringing EU AI Act obligations in scope per `mod-106`), and whether the organisation operates in a sector-regulated domain (bringing sector-supervisor overlay in scope per `mod-107`).
- **Have at least one T2+ system in the inventory.** The operating model at T0 / T1 only is a subset of the operating model this exercise draws; the T2+ posture forces the effective-challenge rotation, the deferral log, and the escalation classes to be real.

Common shapes worth considering (pick one, or invent your own):

- **The mid-size B2B SaaS provider.** ~30 systems in the inventory, most at T1, three at T2 (a customer-facing chatbot, a document-summarisation feature, a search-ranking model), no T3; six-person programme; three EU deployments; no sector overlay.
- **The regulated financial-services institution.** ~40 systems in the inventory, roughly evenly split T1 / T2, one T3 (a credit-decisioning model); eight-person programme; EU and US deployments; SR 11-7-shape sector overlay from `mod-107` in the US, ECB / EBA overlay in the EU.
- **The healthcare-AI provider.** ~15 systems in the inventory, most at T2, two at T3 (a diagnostic-assist system and a workflow-triage system); five-person programme; US and EU deployments; FDA GMLP + PCCP overlay in the US, MDR + AI Act overlay in the EU.
- **The frontier-model developer.** ~10 systems in the inventory, one T3 GPAI-systemic-risk model plus several derivative deployments at T2; seven-person programme; EU + US + UK exposure; Article 55 GPAI overlay from `mod-111` in scope.

Pin the organisation, the inventory count, the programme size, and the jurisdictional / sector posture before drafting.

## Requirements

Produce five artefacts in a single `operating-model/` directory.

### 1. `operating-model-handbook.md`

The handbook proper. Structured as follows.

- **Scope.** The organisation pinned above, in one paragraph, with the inventory count, tier distribution, programme-team size, and jurisdictional / sector posture.
- **The six-stage intake-to-decision cycle.** For each stage — intake queue, scope assessment, evidence-pipeline provisioning, assurance-case draft, release-gate review, decision plus post-market cadence — state the *owner role* (not a person's name), the *service-time expectation* (in working days), the *stage output artefact*, and the *escalation path* if the stage exceeds its service time or lacks an owner comment. Cite chapter `01` for the shape.
- **Cadences.** State the per-cycle, per-release-candidate, and per-quarter cadences the programme runs against. Name the specific meetings (weekly intake triage, daily on-call standup, weekly effective-challenge assignment, monthly release-decision summary, quarterly management-review contribution) with owners and time budgets.
- **Intake worksheet reference.** State that the submitter fills in the analyst-owned intake worksheet, not an assurance case; cite the analyst-track schema by pointer (or mark `<!-- needs-research: … -->` if the schema is not yet pinned in the analyst-track repository). State the discipline: **consume the worksheet or reject it back with a specific request; do not silently redo it.**
- **Common failure modes.** Enumerate at least the six failure modes chapter `01` names — stage-two absorption, stage-four drift, decision-log gaps, silent exception expiry, deferral loops, effective-challenge decay — and for each, state the observable signal (which log or dashboard would reveal it) and the fix.

The handbook is the *reference document* for the running loop. A new joiner should be able to run their first cycle after reading it.

### 2. `evidence-versioning-convention.md`

The evidence-package versioning convention.

- **Shape.** Semantic MAJOR.MINOR.PATCH with the definitions from chapter `01` — MAJOR for criterion-set / deployment-tier / intended-use change, MINOR for evidence extension against the same release-in-scope, PATCH for corrections that do not change the decision.
- **Supersession log.** How MAJOR bumps carry a signed supersession pointer from old to new bundle-id; how the AIMS controlled-document register (per `mod-104` chapter `06`) walks from any bundle-id forward to the current active bundle for that system.
- **Amendment record.** How MINOR bumps carry an amendment record that names what evidence was added, by whom, and why.
- **Patch rationale.** How PATCH bumps carry a `patch_rationale` stanza that explains what was corrected without changing the decision.
- **Failure modes.** Enumerate the four failure modes chapter `01` names — overwriting in place, silent MAJOR bump without supersession pointer, MINOR that should have been a re-decision, silent PATCH — and for each, name the pipeline check that would prevent it.
- **Worked example.** One worked bundle lineage across a release-candidate's lifecycle: initial 1.0.0 bundle at first release, one MINOR bump on a late-arriving third-party evaluator report (1.1.0), one PATCH on a redaction pass (1.1.1), one MAJOR bump on a re-tier decision at the next release (2.0.0), with the supersession pointer from 1.1.1 to 2.0.0.

### 3. `three-registers.md`

The decision log, exception log, and deferred-approval log.

For each register:

- **Row schema.** The columns each row carries. Decision log at minimum: bundle-id, signers, timestamp, disposition (pass / delayed / refused / promoted-at-lower-tier). Exception log at minimum: criterion-id, exception rationale, corrective action, expiry date, revisit trigger, exception approver. Deferred-approval log at minimum: case-id, deferral reason, escalation counterparty, resolution timestamp, resolution disposition (closed-into-decision, closed-into-refusal, or still-open).
- **Append-only invariant.** State that the log is append-only; corrections issue a new row that supersedes the old, with a signed rationale. Reference the pipeline check that enforces the invariant.
- **Read cadence.** Who reads the register, on what cadence, and for what signal. Auditors read the decision log first, the exception log second, the deferred-approval log third; the head of AI governance reads the exception-log summary quarterly; the on-call reads the exception log daily for near-expiry rows.
- **Programme-signal detection.** For each register, at least one *programme-level* signal the register surfaces (not per-case anomalies). Examples: more exceptions than pass-clean decisions signals a criterion-set out of alignment with reality; deferral loops signal a peer-contract broken or a capacity blocker; an exception expiring without a revisit signals a governance defect.

### 4. `effective-challenge-convention.md`

The convention borrowed from [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm).

- **Rule.** For every release-gate decision, an effective-challenger who did not draft the assurance case attempts to refute it before signing; the challenge attempt is recorded whether or not the disposition changes. Cite chapter `01` and the SR 11-7 second-line-of-defence pattern.
- **Rotation.** For the pinned organisation, draft the rotation: which roles rotate, how a challenger is selected per case (previous-week on-call, cross-team lead, a named separate role — pick and defend), how the rotation is audited so no team member is the perpetual challenger or the perpetual challengee.
- **Brief for the challenger.** The short list of things the challenger tries to break: unstated assumptions (per `mod-102` chapter `05` pass 2), serious defeaters (pass 3), diversity of evidence (pass 4). State the challenger's output artefact — a signed challenge report attached to the assurance bundle at layer 4 (per `mod-104` chapter `06`).
- **Failure modes.** Enumerate the four failure modes chapter `01` names — proposer's line manager as challenger, post-signing challenge, silent-fold-back, peer-review-in-name-only — and for each, name the observable signal and the fix.
- **Health signals.** State the health metrics the programme tracks against the convention: rate of surfaced unstated assumptions per challenge (should be non-zero and trending steady), rate of surfaced defeaters that change the disposition (should be small but non-zero), rate of challenges that log a documented disagreement (should be small; if zero, the challenger is deferential; if large, the case-quality is upstream-broken).
- **Pipeline invariant.** State the invariant the pipeline enforces: no bundle is signed at layer 4 unless the challenge review is complete and its output attached (per chapter `01`).

### 5. `reporting-line-contract.md`

The reporting-line contract with `head-of-ai-governance` (level 60).

- **What the programme escalates upward.** The four categories from chapter `01`: monthly release-decision summary, quarterly exception-log summary and corrective-action closure, on-event serious-incident reports (EU AI Act Article 73 where applicable — cite by article number), annual methodology review. For each, state the pack shape, the signer, and the transmission channel.
- **What the programme disposes at team level.** Routine release-gate decisions at previously-approved tier, exception approvals below the escalation bar, deferrals with internal-programme resolution paths, peer-contract renegotiation triggers within the four production peer tracks.
- **What the programme may not decide alone.** The four categories from chapter `01`: EU AI Act Article 55 GPAI systemic-risk classification decisions (cross-reference `mod-111`), prohibited-practice edge cases (Article 5), cross-institution reputational-risk cases, sector-supervisor communications above the routine cadence. For each, state the escalation route and the signer.
- **What the head owes the programme.** The institutional risk-appetite statement, board-level constraints, reputational-risk overrides, resource allocation and top-management commitment (ISO/IEC 42001 clauses 5.1 and 7.1 — cite by clause number).
- **Cadence table.** A compact table with columns *artefact*, *cadence*, *signer*, *transmission channel* for every artefact the contract carries.
- **Escalation-decision log stub.** A stub for the append-only log that records every escalation the programme has made upward, whether the head disposed the case at institution scope or referred it back, and the resolution timestamp. This is the audit-side view of the reporting-line contract.

## Starter guidance

- **Author the handbook against the pinned organisation, not against a generic mid-size company.** A programme running two cycles per month cannot run the same rotation as one running twenty; the cadences, service-time expectations, and rotation shape all change with the inventory count and the programme-team size.
- **Roles, not people.** The handbook names *role slots* (assurance engineer, on-call, effective challenger, programme lead, analyst-team lead, head of AI governance). It does not name people. People change; role slots do not.
- **The pipeline enforces the invariants; the handbook does not just state them.** Every invariant the handbook names (append-only decision log, no bundle signed at layer 4 without an effective-challenge output, exception-expiry sweep) should have a pipeline check that enforces it. Where the pipeline check does not exist yet, mark `<!-- needs-research: pipeline check to be authored -->` rather than gloss over the gap.
- **The effective-challenge convention is quality assurance for the *argument*, not adversarial theatre.** A programme where every case survives challenge cleanly is a programme with too weak a challenger or too shallow a case; a programme where challenges break down into political disputes has lost the second-line pattern's meaning. The health metrics should show a steady rate of surfaced assumptions and a small rate of surfaced defeaters.
- **The reporting-line contract is bidirectional.** The programme owes the head legible reporting on a fixed cadence and escalation on the named classes; the head owes the programme the risk-appetite statement, board-level constraints, and authorisation. If the head's side of the contract is empty, the programme cannot defend its authority against internal challenge.
- **`<!-- needs-research: … -->` is a legitimate answer.** The specific ISO/IEC 42001 clause numbers, the specific EU AI Act article numbers (for Article 55, 73, 74 — verify against the current consolidated text), the current internal schema pointers, and organisation-specific role-name conventions should all be marked rather than guessed where the drafting date is not clean.

## Acceptance criteria

You have succeeded if:

- `operating-model-handbook.md` fixes the pinned organisation's scope; describes each of the six intake-to-decision stages with owner, service time, output, and escalation path; states the per-cycle, per-release-candidate, and per-quarter cadences with specific meetings and owners; references the analyst-owned intake worksheet with the consume-or-reject discipline; enumerates at least six named failure modes with the observable signal and fix for each.
- `evidence-versioning-convention.md` defines MAJOR / MINOR / PATCH per chapter `01`; specifies the supersession log, amendment record, and patch-rationale stanza; enumerates the four failure modes with the pipeline check that prevents each; walks one worked bundle lineage across a release-candidate's lifecycle.
- `three-registers.md` gives the row schema, append-only invariant, read cadence, and at least one programme-level signal for each of the decision log, exception log, and deferred-approval log.
- `effective-challenge-convention.md` states the rule, the rotation for the pinned organisation, the challenger's brief and output artefact, the four failure modes with signals and fixes, the health metrics, and the pipeline invariant.
- `reporting-line-contract.md` covers what the programme escalates upward (four classes), what it disposes at team level, what it may not decide alone (four classes), what the head owes the programme, and a compact cadence table with signer and transmission channel per artefact. An escalation-decision log stub is included.
- Every role is a role slot, not a person's name.
- Every invariant has a named pipeline check (or a `needs-research` marker if the check is not yet authored).
- Every citation to SR 11-7, ISO/IEC 42001 clause number, or EU AI Act article number is either verified against the current text or marked `<!-- needs-research: … -->`.

## Stretch goals

- **Draft the on-call dashboard specification.** In `on-call-dashboard-spec.md`, extend `mod-103` chapter `06` to the programme's actual dashboard: the release-owner board, the on-call board, the programme-owner board, and the audit board, with the specific rows each carries against the pinned organisation.
- **Draft the quarterly management-review pack template.** In `management-review-pack-template.md`, produce the template the programme lead uses to prepare the quarterly ISO/IEC 42001 clause 9.3 management-review contribution — sections, owners, and data sources.
- **Author the exception-log sweep runbook.** In `exception-log-sweep-runbook.md`, produce the runbook the on-call executes each cycle to sweep the exception log for near-expiry rows, missing revisit triggers, and closure-rate outliers.
- **Cross-map to `mod-101/06`.** In `deferral-contract-crosswalk.md`, walk each row of the deferral contract from `mod-101` chapter `06` and pin which register / cadence / handbook stage in this exercise's artefacts discharges it.
- **Draft a mock quarterly review packet.** In `mock-q1-review-pack.md`, produce a mock pack for one hypothetical quarter's operation of the pinned organisation — twelve gate cycles, ten open exceptions with revisit triggers, two escalations upward, one incident, one corrective-action closure — and rehearse the reading of it with a peer standing in for the head of AI governance.
