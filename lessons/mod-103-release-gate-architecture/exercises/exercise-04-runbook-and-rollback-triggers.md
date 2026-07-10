# exercise-04: Runbook and Rollback Triggers

**Estimated effort:** 2 hours

## Objective

Author the **release-gate runbook** for the design produced in exercises `01`–`03`. The runbook covers rollback triggers, rollforward triggers, incident cutover, deferred approvals, exception approvals, and the second-line effective-challenge convention (SR 11-7 shape). Then run one *table-top reverse-drill* on paper — walk a hypothetical trigger firing and record what the on-call would do, minute-by-minute, through the corrective-action closure.

## Prerequisites

- Chapter `05-release-gate-runbook.md` (this module).
- Chapters `01`–`04` (this module), and their applied outputs in exercises `01`–`03`.
- Familiarity with SR 11-7 (mod-101 resources link) — the three-lines-of-defence framing.

## Problem statement

The design so far produces a gate that *can be signed*. This exercise produces the document the on-call actually uses when a signal fires. The runbook has to be executable under time pressure by someone who did not author the design — that is the test of a runbook.

The exercise has three parts: (1) write the runbook sections named in chapter `05`, (2) draft the second-line effective-challenge convention specific to your program, (3) run one table-top reverse-drill and record the trace.

## Requirements

Produce three artefacts.

### 1. `runbook-v1.md`

The runbook, with the sections named in chapter `05`:

- **Scope.** Which gate(s) this runbook applies to; where variant sections live.
- **RACI.** Roles for signer, on-call, release-owner, head of AI governance, incident commander, third-party evaluator interface (where mod-109 applies). Authorisers per tier. Escalation paths.
- **Rollback triggers.** Per-trigger: metric, threshold, persistence window, observer (the dashboard field from chapter `06`), authoriser, RTO. Cover at least: safety-metric, guardrail-effectiveness, statistical-warrant, drift, cybersecurity / integrity, regulatory, and serious-incident triggers.
- **Rollback procedure.** The pre-tested steps per tier. Reverse-drill cadence and reverse-drill success criteria.
- **Rollforward triggers.** Per-trigger: what qualifies for rollforward, the wall-clock ceiling, and the rollforward test-set the patch is exercised against. Explicitly name the trigger classes that are *not* eligible (supply-chain, cybersecurity, serious-incident).
- **Incident cutover.** Procedure for handing off to incident-response. Interface into mod-110. Article 73 (or the applicable serious-incident notification) wall-clock and content requirements.
- **Deferred approvals.** Procedure, per-tier eligibility, expiry, contingent action if expiry lapses.
- **Exception approvals.** Procedure, signers, defensibility criteria (quantified residual, specific mitigation, near-term expiry), and the list of **non-exceptionable criteria** — statute-tied hard-gate criteria that cannot be exceptioned.
- **Post-market handoff.** Which rubric rows continue as ongoing signals in mod-110, where the dashboards live, and the review cadence.
- **Change log.** The runbook's own version history.

### 2. `effective-challenge-convention.md`

A short (1-page) document specifying how second-line effective challenge (SR 11-7 shape) works in your program:

- Reporting-line independence: how the assurance function is independent of the release-owner. If it is not (e.g., a small organisation where the same person owns release and assurance), name the *compensating control* — a second-line reviewer external to the team, a rotating challenge role, an internal-audit sample of decision records.
- Competence: how the challenger's technical competence is demonstrated (training records, per-domain proficiency check, standing peer network).
- Authority: how the challenger blocks. What documents record the block, what override paths exist, and how the override is audited.
- Documentation: the decision-record challenge-log template — sections, mandatory fields, where the log persists, how internal-audit samples it.
- Anti-patterns: the specific rubber-stamp / adversarial-gridlock / first-line-work traps you commit not to repeat, and how the runbook or dashboard would surface each.

### 3. `reverse-drill-tabletop.md`

A table-top exercise. Pick one rollback trigger from `runbook-v1.md` — a statistical-warrant slippage on the primary functional-adequacy metric is a good default — and walk the disposition minute-by-minute:

- T+0: signal source (the dashboard field or the peer-track observer).
- T+0 → T+RTO: on-call actions, wall-clock, hand-offs.
- T+RTO+ε: incident-commander involvement, release-owner notification, release-attribution recording.
- Notification (if the incident meets the serious-incident threshold): who is notified, in what wall-clock, with what content.
- Post-stabilisation review: participants, agenda, outputs.
- Corrective-action closure: what lands in ISO/IEC 42001 clause 10.1, what lands as a rubric-change (chapter `02`), what lands as a contract-renegotiation (chapter `04`), what lands as a runbook change.

The trace should show what the runbook is *actually* good for — not that the events happen, but that no step depends on improvisation.

## Starter guidance

- **Assume the reader is not you.** The runbook must be executable by an on-call who did not participate in the design. If a step requires context that lives only in your head, the step is not written.
- **Wall-clock RTOs are not aspirational.** If the rollback procedure has never been executed under time pressure, the RTO is a hypothesis. State it as such and set the reverse-drill cadence to test it.
- **Do not merge deferred and exception approvals.** They look similar and get conflated in practice; the whole point of writing them down is to keep them separate.
- **Non-exceptionable criteria are the shortest section but the most important.** If you cannot name any, the runbook is under-designed — every statute-tied hard-gate criterion should appear.
- **Effective challenge is not a paragraph in the runbook.** It is a standing convention. If your program does not have organisational independence between the release-owner and the assurance owner, name the compensating control explicitly rather than glossing.
- **The table-top drill is a *paper* exercise.** You do not need to actually execute the rollback. What you need is a minute-by-minute trace that would survive review by a colleague who did not co-author the runbook.

## Acceptance criteria

You have succeeded if:

- `runbook-v1.md` covers every section named in chapter `05` and is executable without external context (a colleague could sign the on-call rotation).
- Rollback triggers are pre-committed with metric / threshold / persistence-window / observer / authoriser / RTO.
- Rollforward triggers are narrow, safeguarded, and explicitly exclude supply-chain, cybersecurity, and serious-incident classes.
- Deferred and exception approvals are strictly separated with their own procedures and defensibility criteria.
- Non-exceptionable criteria are named.
- The Article 73 (or applicable serious-incident) notification interface names the wall-clock and the content requirements.
- `effective-challenge-convention.md` names independence, competence, authority, and documentation and, if independence is imperfect, names the compensating control.
- The reverse-drill trace shows a minute-by-minute path that does not depend on improvisation.
- The runbook and the dashboard (chapter `06`) are consistent — every runbook trigger has a dashboard observer.

## Stretch goals

- Extend the runbook with a **sector-specific overlay** (mod-107 preview): the additional clauses that apply under SR 11-7, FDA GMLP, or DORA. Name the additional signers and the additional notification obligations.
- Extend the runbook with a **GPAI systemic-risk overlay** (mod-111 preview): the additional Article 55 / GPAI Code of Practice obligations, and the additional third-party notifications.
- Author a **runbook-audit check-list** — the sample the internal-audit function uses to walk a decision record against the runbook. This will surface any runbook step that depends on side-channel context.
- Draft the **incident post-mortem template** the runbook cites — sections, required fields, and the loop from post-mortem into rubric / contract / runbook change.
- Run a **red-team on the runbook**: hand the document to a colleague and ask them to identify at least three gaps or ambiguities. Capture their findings and revise. This is the only cheap way to test the runbook's readability.
