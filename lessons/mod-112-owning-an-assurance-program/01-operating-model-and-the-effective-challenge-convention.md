# The Operating Model and the Effective-Challenge Convention

## Motivation

The preceding eleven modules gave you the *methodology*: how the release-gate is architected, how evidence is packaged, how cards are produced, how obligations map across jurisdictions, how post-market surveillance closes the loop. This chapter turns the methodology into a *running function* — a team-scope operating model with an intake queue, a decision log, an exception log, a deferred-approval log, a standing effective-challenge convention, and a reporting-line contract with the head of AI governance.

Two failure modes motivate the exercise.

The first is **the invisible programme**. The methodology exists on paper; each release is worked ad hoc by whoever has time; there is no queue, no cadence, no versioned decision log, and no way for the head of governance to see throughput. Under ISO/IEC 42001 clause 5 (leadership) and clause 9.3 (management review) this posture fails an audit before the auditor has read the technical documentation, because the AIMS itself has no operating record. Under SR 11-7's second-line-of-defence pattern the programme also has no *challenge* record; every decision looks like a solo call.

The second is **the overweight programme**. The assurance team has an intake queue, a decision log, and a full RACI, but it has silently absorbed peer-track work — running its own risk assessments, hand-tuning its own eval harnesses, drafting its own harm inventories. Altitude is lost (per `mod-101`), the deferral contract (per `mod-101/06`) is violated, and the team burns capacity on work its peers already own.

The operating model this chapter draws is the equilibrium between the two: enough procedure to be auditable, few enough responsibilities to stay at altitude.

## The intake-to-decision cycle

The programme's core loop has six stages. Every release-in-scope traverses the same six.

1. **Intake queue.** A change (new system, new model version, new deployment tier, material config change, a jurisdictional trigger, a post-market signal from `mod-110`) enters the queue with a submitter, a proposed effective date, and a pointer to the analyst-owned intake worksheet.
2. **Scope assessment.** The assurance owner classifies the change against the deployment-tier map (`mod-108`), the jurisdictional scope (`mod-106`), and the sector overlay (`mod-107`). Output: a scope statement pinning the criterion set version, the peer contracts in force, and the deferral contract rows that apply.
3. **Evidence-pipeline provisioning.** The assurance owner opens the evidence-pipeline slot (`mod-104`), notifies each peer of what artefacts are owed with what freshness, and posts a target gate date. The pipeline provisions the store paths, the retention class, and the SACM stub.
4. **Assurance-case draft.** The assurance owner drafts the case (`mod-102`) against the criterion set, threading the incoming peer evidence into the argument as it lands. The case is a live document until freeze.
5. **Release-gate review.** The walker runs (`mod-103`); the on-call reads the dashboard (`mod-103/06`); the effective-challenge review is executed (see the convention below); the decision record is signed; the assurance bundle is emitted (`mod-104/06`).
6. **Decision + post-market cadence.** The bundle is persisted into the AIMS register (ISO/IEC 42001 clause 7.5); the online-eval slice, the drift detectors, and the review cadence are handed to `mod-110`; the exception and deferral registers are updated; the retrospective enters the next management-review pack.

Each stage has an owner, a service-time expectation, and an escalation path. A change that dwells more than one cadence in any stage without an owner comment is a *programme signal* — the queue is either under-staffed or the contract with a peer is broken.

### The intake worksheet

The submitter does not fill in an assurance case; they fill in a short intake worksheet the analyst owns (`mod-101/06`). The worksheet carries: the system-under-change identity, the proposed change class, the intended-use delta, the deployment-tier delta, the jurisdictional-scope delta, the last approved release candidate, and the submitter's proposed effective date. The assurance owner *does not* re-elicit these fields; they consume the analyst's worksheet.

### Cadences per stage

The loop has three natural cadences that a running programme visibly runs against:

- **Per-cycle.** Intake queue and scope assessment run continuously; every incoming change is triaged within one working day. Cases with a proposed effective date more than four weeks out enter *planned* status; cases closer in enter *active* status.
- **Per-release-candidate.** Evidence-pipeline provisioning through decision-and-post-market runs per candidate; the target service-time (submission to signed decision) is negotiated against the deployment tier and the release-cadence of the peer engineering teams. A steady-state programme carries a target of two weeks at T2 and four weeks at T3.
- **Per-quarter.** Retrospective across all cycles; the operating model itself is audited against its running record; the criterion set, peer contracts, matrix, and runbook are refreshed on triggers.

Cadences that slip more than one cycle without a documented reason are a *programme signal* (per chapter `05` — the queue-dwell signal is one of the incident-driven-roadmap inputs).

## Evidence-package versioning

Assurance bundles are versioned; decision records are appended, never overwritten; corrections issue new versions with a rationale.

**Shape.** Every assurance bundle carries a semantic version — `MAJOR.MINOR.PATCH` — with the following convention:

- **MAJOR** — the criterion set, the deployment tier, or the intended-use scope changed. A MAJOR bump means the release under review is a materially different release; a new bundle stands beside the old one, both remain retrievable, and the supersession log records the pointer from old to new.
- **MINOR** — an additional piece of evidence has been folded in for the same release-in-scope (a late-arriving third-party evaluator report, an incident-derived corrective action from `mod-110`, a jurisdictional-mapping refresh). The decision is not re-opened; the bundle is extended with an amendment record.
- **PATCH** — a correction that does not change the decision (a redaction pass owned by the peer, a typo in a card, a broken cross-reference fix). The bundle carries the corrected artefact plus a `patch_rationale` stanza.

**Failure modes.** Overwriting a bundle in place (the audit trail vanishes); issuing a MAJOR bump without a supersession pointer (the AIMS register loses the lineage); using MINOR for what should have been a re-decision (the decision log stops matching the deployed reality); silent PATCH (auditors cannot reconstruct what changed).

**What good looks like.** Every bundle-id is immutable and points at exactly one manifest; every supersession is a signed record; the AIMS controlled-document register (`mod-104/06`) can be walked from any bundle-id forward to the current active bundle for that system.

## The decision log, exception log, and deferred-approval log

Three registers sit next to the AIMS records and are inspected in every audit.

**The decision log.** Append-only. Every release-gate decision (pass, delayed, refused, promoted-at-lower-tier) is a row with the bundle-id, the signers, the timestamp, and the disposition. The log is the top-level index the auditor walks; every ISO/IEC 42001 clause 9.1 record threads through it.

**The exception log.** Every release-gate decision that passed with a documented exception (a criterion the walker resolved as `soft-fail` and the on-call dispositioned to accept with a corrective action, or a `hard-fail` overridden by escalation) is a row with a rationale, an expiry date, a revisit trigger, and the exception approver. Exceptions carry an expiry by convention; an exception without a revisit trigger is a governance defect.

**The deferred-approval log.** Every release-gate decision that was *not made* — the release delayed, the evidence pipeline paused, the decision passed to a later cycle — is a row with the deferral reason, the party the deferral escalates to, and the resolution timestamp. Deferrals close either into a decision (the release-gate re-runs with the missing evidence) or into a refusal (the release is withdrawn).

Two of the three logs sit *behind* the decision log in the audit walk. The exception log is the second-most-scrutinised artefact in the programme after the decision log itself — auditors read exceptions to test whether the criterion set is being *enforced* or *negotiated*. A programme with more exceptions than pass-clean decisions is a programme whose criterion set is out of alignment with reality (`mod-101/03`).

## The effective-challenge convention

The single most important cultural practice in the operating model is the effective-challenge convention, borrowed directly from the second-line-of-defence pattern in [Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) on model risk management. The pattern is simple: **someone other than the release proposer must attempt to refute the assurance case, and the refutation attempt must be recorded**.

**Shape.** For every release-gate decision, the assurance case is reviewed by an effective-challenger who did *not* draft it. The challenger's brief is to try to break the case: surface unstated assumptions (per `mod-102/05` pass 2), name serious defeaters (pass 3), test the diversity of evidence (pass 4), and either concur with the disposition or log a documented disagreement. Their signature lands in the assurance bundle alongside the on-call signature (`mod-104/06` layer 4).

**Failure modes.** The challenger is the proposer's line manager (not adversarial in shape, deferential in practice); the challenge is performed *after* the decision is signed (a rubber-stamp); the challenger's disagreement is quietly folded back into the case without a record (the audit trail loses the challenge); the challenger has no methodology of their own (a peer-review-in-name-only). Any of these turns effective challenge into a compliance artefact rather than a quality-assurance practice.

**What good looks like.** The challenger is drawn from the assurance team but from a different case; the challenge is executed *before* the signing, with the assurance case in its live state; the challenger's findings are attached to the bundle whether or not the disposition changed; a documented disagreement is a bundle-level record, not a private note. The rotation is transparent — every team member is challenger for roughly half of their case count and challengee for the other half.

The point is quality assurance for the *argument*, not adversarial theatre. A programme where every case survives challenge cleanly is a programme with too weak a challenger or too shallow a case; a programme where challenges break down into political disputes has lost the second-line pattern's meaning. The healthy signal is a steady rate of surfaced unstated assumptions that improve the case without changing the disposition, plus a small rate of surfaced defeaters that do change the disposition.

## The reporting-line contract with `head-of-ai-governance`

The team-scope programme reports upward to the head of AI governance (level 60), whose remit is institution-scope. The contract governing that reporting line is what keeps the programme's authority defensible without dragging institution-scope decisions down to team scope.

**What the programme escalates upward.**

- Monthly: a release-decision summary (throughput, disposition mix, exception counts, deferral counts, rollback events).
- Quarterly: an exception-log summary and a corrective-action closure report (feeds ISO/IEC 42001 clause 9.3 management review, per [ISO/IEC 42001](https://www.iso.org/standard/81230.html)).
- On-event: serious-incident reports (EU AI Act Article 73), material changes to the risk landscape, any release-gate decision the programme *could not* dispose alone (see below).
- Annually: the programme's own methodology review — what changed in the criterion set, the peer contracts, the runbook, the dashboard.

**What the programme disposes at team level.**

- Routine release-gate decisions for systems already in the AI inventory at their previously approved tier.
- Exception approvals that meet the programme-set threshold (severity below the escalation bar, corrective action within one cycle, no cross-jurisdiction implication).
- Deferrals whose resolution path is internal to the programme.
- Peer-contract renegotiation triggers that stay within the four production peer tracks (`mod-103/04`).

**What the programme may not decide alone.**

- **EU AI Act Article 55 GPAI systemic-risk classification decisions.** These are institution-scope; the programme's role is to assemble the evidence, but the classification decision rests with the head of AI governance or higher (`mod-111`).
- **Prohibited-practice edge cases (Article 5).** Any case where a proposed deployment sits close to a prohibited practice escalates before the release-gate runs.
- **Cross-institution reputational-risk cases.** A release that could affect the institution's public posture across the board (a first-of-its-kind agentic deployment, a novel modality, a case where the harm inventory has a societal-scale entry) escalates. The programme's authority is *team scope*; institution-scope reputational calls are the head's.
- **Sector-supervisor communications above the routine reporting cadence.** A first-time contact with a competent authority, a serious-incident notification under Article 73, or a market-surveillance response under Article 74 goes upward before it goes outward (`mod-107`, `mod-109`).

The contract is bidirectional. The head owes the programme: an institution-level risk-appetite statement (referenced by every criterion set), the programme's authorisation and resourcing (ISO/IEC 42001 clause 5.1, clause 7.1), and any board-level constraints that shape what the programme can approve. The programme owes the head: legible reporting on a fixed cadence, escalation on the classes above, and a signed methodology review annually.

## Common failure modes in the operating model

The operating model fails in patterns that show up across programmes. Naming them makes them detectable:

- **Stage-two absorption.** Scope assessment inflates from a one-hour classification into a multi-day analysis session; the assurance owner starts re-eliciting the analyst's worksheet fields. The fix is a discipline: consume the worksheet or reject it back to the analyst with a specific request; do not silently redo it.
- **Stage-four drift.** Assurance-case drafting slips beyond the target service time; peer evidence lands but is not threaded in on time. The fix is per-cycle owner accountability: the case has a named drafter per cycle; the case's state is visible on the on-call dashboard (`mod-103/06`).
- **Decision-log gaps.** A gate cycle finishes but the row is entered later, or entered without one of the required fields (bundle-id, signer, timestamp). The fix is a pipeline check: no bundle is emitted (`mod-104/06`) unless the decision-log row is present and complete; the pipeline enforces the invariant.
- **Silent exception expiry.** An exception's expiry date passes without a revisit; the deployed system is now operating outside the criterion set. The fix is a per-cycle sweep of the exception log with an automated alert on any row within its expiry window.
- **Deferral loops.** A case defers, then defers again next cycle, then again; the queue accumulates cases that no one has forced to a decision. The fix is a maximum-deferral count (typically two) after which the case is escalated to the head of AI governance for a forcing disposition (proceed with exceptions, refuse, or reassign).
- **Effective-challenge decay.** The challenge review slips off the schedule; challenges arrive after the decision is signed; the log accumulates rubber-stamped concurrences. The fix is a schedule invariant: no bundle is signed at layer 4 unless the challenge review is complete and its output attached; the pipeline enforces this too.

Every failure mode above is *observable* — either from the decision log, the exception log, the deferral log, or the on-call dashboard. Detection is not the hard part; the hard part is treating the pattern as a programme-level defect rather than a per-case anomaly.

## Worked example — a six-person assurance team inside a four-hundred-person AI engineering organisation

Consider a provider with roughly 400 AI engineers across a dozen product lines, forty AI systems in the inventory (of which six sit at deployment tier T2 and one at T3), and a governance function led by a head of AI governance at level 60. The assurance programme is a team of six: one lead (level 35), three assurance engineers (level 35 or growing into it), one on-call rotation coordinator, and one assurance-programme analyst who liaises with the eleven analysts across the product lines.

**Intake queue.** Roughly two release-gate decisions per week across the inventory, plus one MAJOR-bump reassessment per month, plus one incident-derived re-run per quarter — call it twelve gate cycles per month at steady state. The queue is tracked in the programme's own ticket system; each ticket carries a pointer to the analyst worksheet, the scope statement, and a target gate date.

**Cadence.** Weekly intake triage (one hour); daily on-call standup (fifteen minutes); weekly effective-challenge assignment (thirty minutes); monthly release-decision summary to the head (thirty minutes with a written pack); quarterly management-review contribution (a written pack, no meeting owned by the programme).

**Effective-challenge rotation.** Three assurance engineers rotate on-call, one week at a time. The on-call engineer is the release proposer for their week; the previous week's on-call is the effective challenger for the current week's cases. The lead reviews any challenge that logs a disagreement and countersigns the disposition either way.

**Deferral posture.** The programme escalates two cases upward last quarter: a T3 case where the harm inventory had a new societal-scale entry (escalated to the head; approved with a board-level constraint attached) and a cross-jurisdictional case where the EU deployment triggered an Article 55 assessment (escalated to the senior architect and the head; classification not made at team level).

**Exception posture.** Ten open exceptions across the inventory, all with revisit triggers and expiry dates within one quarter. Two exceptions closed into decisions this quarter; one converted into a refusal after the corrective action could not close.

The programme is small; the operating model does not require it to be large. What it requires is that every stage has an owner and every log is append-only.

## Where this shows up in the rest of the track

- Chapter `02` — the peer-track contract matrix specifies exactly what each of the six inputs owes the intake stage and what the release-gate stage owes back.
- Chapter `03` — the reporting-line contract with the head of AI governance is drawn in full, alongside the interfaces with the senior architect and external supervisory bodies.
- Chapter `04` — the build-vs-buy decision names which stages of the intake-to-decision cycle are cheap to buy and which are worth authoring internally.
- Chapter `05` — the incident-driven roadmap prioritisation ritual reads from the exception log, the deferral log, and the decision log to rank the next quarter's investment.
- `mod-101/06` — the deferral contract is the input; the operating model is the running function that discharges it.
- `mod-104/06` — the assurance bundle is the artefact each cycle emits; the operating model is what produces and persists it.

## Summary

- The programme is a running function with a six-stage intake-to-decision cycle: intake queue, scope assessment, evidence-pipeline provisioning, assurance-case draft, release-gate review, decision plus post-market cadence.
- Assurance bundles are semantically versioned (MAJOR / MINOR / PATCH); the decision log is append-only; corrections issue new versions with a rationale rather than overwriting.
- Three registers sit next to the decision log: the decision log itself, the exception log (the second-most-scrutinised artefact in the programme), and the deferred-approval log.
- The effective-challenge convention (borrowed from SR 11-7) requires a challenger who is not the proposer to attempt to refute the case before signing; the challenge attempt is recorded whether or not it changes the disposition.
- The reporting-line contract with `head-of-ai-governance` fixes what the programme escalates, what it disposes at team level, and what it may not decide alone (Article 55 classification, prohibited-practice edge cases, cross-institution reputational-risk cases, first-time supervisor communications).
- The worked six-person team inside a four-hundred-person organisation shows that the operating model does not require scale — it requires stage ownership and append-only logs.
- Exercise-01 asks you to draft the operating model for a realistic organisation, name the effective-challenge rotation, and defend the escalation classes with your head-of-governance.
