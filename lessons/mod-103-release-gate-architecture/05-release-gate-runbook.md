# The Release-Gate Runbook and the SR 11-7 Effective-Challenge Convention

## Motivation

Chapter `01` said every release-gate carries a rollback and rollforward contract. Chapters `02`–`04` designed the rubric, the AIMS mapping, and the peer-track contracts. This chapter writes the *runbook* — the standing document the on-call assurance engineer keeps at hand on the day of the release and during the post-release watch. Without a runbook, the design in the previous chapters lives in slide decks; with a runbook, the design binds to a set of *dispositions* the on-call executes without improvisation.

The runbook has to answer six kinds of question:

1. **Rollback triggers.** What signals, at what thresholds, trigger a rollback? Who authorises the invocation? What is the RTO?
2. **Rollforward triggers.** What signals admit a fix-forward instead of a rollback? What are the safeguards?
3. **Incident cutover.** When a release causes an incident (in the mod-110 sense), how does the gate hand off to incident-response, and at what point does the release-owner reclaim authority?
4. **Deferred approvals.** When a criterion cannot be evaluated at gate time (an artefact is missing but expected to arrive within days), what is the *deferred-approval* disposition, and how is it tracked?
5. **Exception approvals.** When a criterion fails but the release-owner argues for promotion regardless (residual risk accepted), what is the process, who signs, what is the residual expiry?
6. **Second-line effective challenge.** How does the assurance function (second line) challenge the release decision without owning the release decision — the shape SR 11-7 fixes.

Each of the six has a documented procedure below.

## Rollback triggers

**Design principle.** Every trigger is pre-committed, measurable at runtime, and observed by the dashboard (chapter `06`). Triggers do not require judgement to fire; judgement enters at *disposition after fire*.

**Trigger classes.**

- **Safety-metric trigger.** Any safety-benchmark metric (from the `ai-risk-engineer` peer contract) that exceeded the pre-registered threshold at gate is re-measured on production traffic. If the production measurement exceeds the threshold by more than a pre-registered `epsilon`, rollback fires.
- **Guardrail-effectiveness trigger.** Guardrail block-rate falls below a floor (guardrail is failing to block adversarial input) *or* rises above a ceiling (guardrail is over-blocking benign input). Both are pre-registered.
- **Statistical-warrant trigger.** The primary functional-adequacy metric on the production distribution slips below the CI lower-bound accepted at gate (with a pre-registered wall-clock persistence window to avoid single-batch noise).
- **Drift trigger.** Distributional drift on named input features exceeds the pre-registered drift-magnitude, per the `ai-eval-engineer` peer contract's online-eval slice.
- **Cybersecurity / integrity trigger.** A supply-chain integrity check (BOM digest, judge digest, model digest) fails post-promotion. Fires immediately regardless of user impact.
- **Regulatory-trigger.** A regulator or an equivalent authority issues a notice that changes the deployment's compliance status. Fires immediately.
- **Serious-incident trigger.** A serious incident under EU AI Act Article 73 (or the equivalent obligation in scope — sector rule, DoRA, FDA MDR) occurs and is attributable to the release. Fires immediately.

Every trigger names: the metric, the threshold, the persistence window (single-batch vs. sustained), the observer (the dashboard signal or the incident source), and the authoriser (the on-call for measurement-based triggers; the release-owner or the head of AI governance for regulatory / serious-incident triggers).

**Authorisation.** The on-call has *pre-authorised* rollback authority for measurement-based triggers, up to the T-tier they are on-call for. Higher-tier rollback (typically T3+ for a deployment that affects many users, notified-body-involved deployments, or on-prem deployer sites) escalates to the release-owner. All rollback invocations are logged.

**RTO.** Recovery-time objective per tier. Values are program-specific; what matters is that (a) the RTO is written down per tier in the runbook, (b) the reverse-drill (chapter `01`) is tested against the RTO at least quarterly, and (c) the actual rollback time from an incident is recorded post-hoc and compared to the RTO.

**Post-rollback disposition.** Every rollback fires a *post-rollback review* within a documented window. The review's output feeds a corrective action into ISO/IEC 42001 clause 10.1 (improvement) and either updates the harm inventory (mod-102 chapter `06`'s risk-engineer contract row), updates the rubric (chapter `02`), or updates the runbook itself.

## Rollforward triggers

**Design principle.** Rollforward is a *narrower* option than rollback. It is available only when (a) the trigger is scoped to a small, patchable component and (b) reverting the entire promotion would itself be more disruptive than the trigger.

**Trigger classes admitting rollforward.**

- **Prompt / config-only regression.** A change in the prompt or a config file causes the regression; reverting *just* the prompt / config is well-tested.
- **Guardrail-config regression.** A guardrail change is under-blocking or over-blocking; the guardrail-config is versioned separately from the model and can be reverted independently.
- **Judge-prompt regression.** The judge is producing skewed scores because of a judge-prompt change; the judge prompt reverts independently.

Rollforward is *never* available for supply-chain-integrity, cybersecurity, or serious-incident triggers. Those roll back.

**Safeguards.**

- The rollforward patch is exercised against the pre-registered rollforward test-set (small, per-tier, kept fresh by the peer track owning the affected component) before deployment.
- The rollforward records itself as a *change* in the change-log (ISO/IEC 42001 clause 8.2), including a *delta risk-assessment* the risk-engineer peer signs off on.
- The rollforward wall-clock is bounded — if the patch cannot be deployed within a pre-registered window, the trigger escalates to rollback.

## Incident cutover

**Design principle.** When a release causes an incident, the release-gate hands off to incident-response, and clarity of hand-off is what prevents the release-gate from being *both* the trigger source *and* the incident owner (a conflict that produces slow response).

**Cutover procedure.**

1. On-call assurance engineer detects the trigger (dashboard signal, incident-source page, regulator notice). The on-call *pages* the incident commander per the incident-response process the organisation runs.
2. On-call assurance engineer records the *release-attribution* — this release, this rubric criterion, this rollback trigger — in the incident-response system.
3. Incident commander owns the incident; on-call assurance engineer is a support role. The on-call *executes* the pre-authorised rollback if their authorisation covers the tier, or *requests* the release-owner's authorisation if not.
4. Once the incident is stabilised (rollback executed, or rollforward patch deployed, or explicit "hold with elevated monitoring" agreed), the incident commander hands back to the release-owner for post-incident review.
5. Post-incident review runs the corrective-action loop: rubric change, runbook change, contract change, harm-inventory change.

**Interface to mod-110.** The incident-detection signal comes out of post-market surveillance. The runbook cites the specific dashboards and detectors mod-110 owns; the mod-110 loop cites the release-gate as the corrective-action target. Feed both directions.

**Interface to EU AI Act Article 73.** Where the incident meets the "serious incident" threshold (as scoped in the applicable jurisdictional obligation), the runbook includes the *notification* procedure: whom to notify, in what wall-clock, with what content. The AIMS's incident-notification obligation is separate from — but must not lag — the internal rollback.

## Deferred approvals

**Design principle.** A criterion may have all the shape right (metric, threshold, evidence pointer) but the *artefact* has not arrived at the gate window. Two dispositions are possible: defer the release, or defer the criterion evaluation with a bounded expiry.

**Deferred-criterion approval** is the second option. It is *not* an exception; it is a *time-boxed acceptance of a gap*.

**Procedure.**

1. On-call verifies the criterion is *deferrable* — the criterion is soft, or the criterion is hard but the tier-specific rubric row permits deferral (typically only at T0 / T1; higher tiers are stricter).
2. On-call names the *deferral window* — a wall-clock or a milestone at which the artefact must arrive. Windows are pre-registered per rubric row; ad-hoc windows are exception approvals, not deferred approvals.
3. On-call names the *contingent action* if the artefact does not arrive by expiry (rollback, tier downgrade, exception approval reconsideration).
4. Deferral is logged in the decision record with an *expiry timestamp* and an *owner peer track* obligation to close the gap.

**Escalation.** If a deferral expires without closure, the runbook escalates to the release-owner (T0 / T1) or the head of AI governance (T2 and above). Repeated deferrals against the same rubric row are a signal that the contract with the peer track needs renegotiation (chapter `04`).

**Reporting.** Deferred approvals are a *tracked metric* on the dashboard (chapter `06`) and a standing management-review input (ISO/IEC 42001 clause 9.3). An accumulation of deferrals against a peer track is a governance signal.

## Exception approvals

**Design principle.** An exception is a *knowing* acceptance of a criterion failure. It is rare, tracked, defensible, and time-bounded.

**Procedure.**

1. Release-owner submits a written *exception request* naming the criterion, the failure, the residual risk being accepted, the mitigation in place, the expiry, and the framework citations (EU AI Act article, ISO 42001 clause, sector rule).
2. Head of AI governance (or their delegated signer per the RACI) reviews. For T2 and above, the review includes a *second-line effective challenge* (see the next section).
3. Exception is either granted or denied. A grant is *conditional* — with the mitigation, the expiry, and a *revisit trigger* named.
4. Exception is recorded in the residual-risk register (ISO 42001 clause 8.3 output). The register is a program-level artefact reviewed by internal audit and management review.
5. At expiry, the exception is either re-granted (with a fresh review), closed (the mitigation now brings the criterion into pass), or the release is rolled back.

**What makes an exception defensible.** Three things: the residual risk is *quantified* (a widened CI, a coverage gap of X%, a known false-negative-rate elevation), the mitigation is *specific and testable* (a monitoring detector fires at Y threshold), and the expiry is *near-term* (typically weeks to a small number of months, not "next major release").

**What makes an exception undefensible.** "The release-owner argued the criterion is not applicable." "The threshold was too tight to begin with." "The residual is *some* risk, mitigated by *various* controls." Any of these are audit findings.

**What exceptions are *not* used for.** Statute obligations. If a criterion discharges EU AI Act Article 15 accuracy, sector-rule independent validation, or a similar hard-floor requirement, the exception path is *not available* — the release either passes or is deferred until the criterion is closed. The runbook names the "no-exception" criteria explicitly per tier.

## Second-line effective challenge — the SR 11-7 shape

**Motivation.** Federal Reserve SR 11-7 (Guidance on Model Risk Management), together with OCC 2011-12, is the source of the *three lines of defence* framing that most model-risk regimes now use: the first line owns and uses the model, the second line independently validates and challenges the model, the third line audits both lines. For the release-assurance program, the relevant convention is the second-line *effective challenge* — the ability of an independent function to push back on the release with authority.

The release-assurance program *is* second-line for the AI release decision. The runbook has to describe what "effective challenge" looks like in that role. SR 11-7 gives the shape; this section adapts it.

**What "effective challenge" means.**

- **Independence from the release-owner.** The assurance function does not report through the release-owner. Reporting-line separation is set at the RACI level (mod-101 chapter `03`, clause 5) and cannot be side-stepped.
- **Sufficient competence.** The challenger has the technical competence to interrogate the evidence — not to re-do the model-eval, but to *read* the peer track's warrant and identify defeaters (mod-102 chapter `05`).
- **Sufficient authority.** The challenger can block a release. In the release-gate model, "block" is either: (a) refusing to sign the decision record, which prevents T2+ promotion; or (b) requiring an exception-approval path with head-of-AI-governance review.
- **Documented.** Every challenge and its disposition is documented in the decision record.

**Effective challenge in the release-gate procedure.**

1. The assurance function reads the assurance case, the evidence bundle, and the drafted decision record before signing.
2. The assurance function documents challenges — questions raised, defeaters identified, contract clauses cited — in the decision record's challenge log.
3. The release-owner responds to each challenge on the record (mitigation, revised residual, revised rubric, additional evidence).
4. Where the response is inadequate, the challenge escalates to an *exception-approval request* (previous section) or a *deferral* (two sections back).
5. Where the challenge is a *methodology* concern about a peer track's contract, the challenge triggers a contract renegotiation (chapter `04`).

**Anti-patterns.**

- **Rubber-stamp.** Assurance signs without documented challenge. This is a governance defect; internal audit catches it by sampling decision records and looking for the challenge log.
- **Adversarial gridlock.** Every release is challenged with the same set of unresolved concerns; the assurance function becomes an obstacle rather than a challenge function. Fix by *closing* challenges — either the peer track closes the concern or the challenge is retired with a documented reason.
- **Second-line does first-line work.** The assurance function re-runs the eval, builds the harm inventory, or writes the rubric criteria (rather than reviewing them). This is the mod-101 backfill trap.

**Interface into sector-regulated regimes.** For banks and other sector-regulated deployers, SR 11-7's independent-validation expectation is often satisfied *at the deployer's site* by their model-risk-management function. The release-gate's second-line and the deployer's second-line are distinct; mod-107 walks the interface.

## The runbook as a document

**Format.** Markdown or a structured document format (per the AIMS's documented-information convention, ISO 42001 clause 7.5). Versioned in Git, tagged, cited by decision records.

**Sections.**

1. Scope (which release-gates the runbook applies to; where variants live).
2. RACI (roles, authorisers, escalations).
3. Rollback triggers, procedures, RTOs, reverse-drill cadence.
4. Rollforward triggers, procedures, safeguards.
5. Incident-cutover procedure and Article 73 notification interface.
6. Deferred-approval procedure and windows per rubric row.
7. Exception-approval procedure, signers, non-exceptionable criteria.
8. Second-line effective-challenge convention.
9. Post-market handoff to mod-110.
10. Change log for the runbook itself.

**Review cadence.** At minimum annually; on framework change (EU AI Act updates, sector rule updates); after every incident that surfaces a runbook gap; after every reverse-drill that surfaces a procedural gap.

**Testing.** Reverse-drills are the runbook's primary test. Rollback and rollforward procedures are exercised against the actual production surface at the tested cadence. A runbook procedure that has never been executed under time pressure is a hypothesis, not a control.

## Worked example — one trigger, one disposition

A T2 gate promotes a customer-intent classifier with a `GATE-FA-01` hard criterion (per-class F1 ≥ 0.85, CI lower-bound ≥ 0.83, from chapter `02`'s worked row) and a `GATE-ROB-03` hard criterion (adversarial-attack-success ≤ 5% on threat-model T with a stated CI).

Twelve hours after promotion, the online-eval slice reports the per-class F1 CI lower-bound has slipped below 0.80 for two consecutive 30-minute batches. That is the `GATE-FA-01` runtime trigger for a statistical-warrant rollback.

**Disposition.**

1. Dashboard signal fires. On-call is paged.
2. On-call verifies the trigger against the runbook: `GATE-FA-01` statistical-warrant trigger fires when the online CI lower-bound < 0.80 for ≥ 2 consecutive 30-minute batches. Confirmed.
3. On-call executes the T2 rollback: traffic-shift back to the previous known-good version, per the pre-tested procedure. RTO for T2 is 15 minutes; measured wall-clock is recorded.
4. On-call pages the incident commander and records the release-attribution.
5. Post-rollback, on-call verifies the previous version's F1 is at expected level.
6. Within a documented window, the release-owner and the assurance owner review: was the rollback caused by a drift the rubric did not cover (adaptability gap), or by a model-side regression that the model-eval peer's benchmark did not surface?
7. Corrective action: either the rubric adds an adaptability criterion at gate time, or the model-eval peer's benchmark is extended to cover the failure mode. The action lands in ISO 42001 clause 10.1 with an owner and an expiry.

The whole flow — from signal to corrective action — is documented in the decision record and in the incident record; both link to each other.

## Common failure modes

- **Runbook procedures never tested.** Reverse-drill has not fired in a year. Rollback works "in principle."
- **Triggers depend on a signal the dashboard does not surface.** The runbook cannot be executed because the observer is missing.
- **Deferred and exception approvals blur.** The two dispositions look similar; neither has a defensible track. Fix by keeping the two lanes strictly separate in the runbook.
- **Second-line signs the decision record without a challenge log.** The effective-challenge convention is not observed; internal audit escalates.
- **Runbook does not name the wall-clock for Article 73 notification.** A serious incident happens; notification is late; the AIMS has a compliance breach on top of the release incident.

## Where this feeds

- Chapter `06` — the dashboard's signal lanes are exactly the triggers the runbook consumes.
- mod-104 — the immutable evidence pipeline is what the decision record's challenge log and rollback log land in.
- mod-107 — sector-regulated regimes (SR 11-7, OCC 2011-12, FDA GMLP, DORA) may add per-sector runbook clauses.
- mod-110 — the post-market loop is the source of the ongoing signal set the runbook triggers on.
- mod-111 — GPAI systemic-risk deployments add serious-incident notification obligations (EU AI Act Article 55 and the Code of Practice) that the runbook mirrors.

## Summary

- The runbook is the standing document the on-call reads. Its six sections cover rollback triggers, rollforward triggers, incident cutover, deferred approvals, exception approvals, and second-line effective challenge.
- Rollback triggers are pre-committed and observed by the dashboard. On-call has pre-authorised rollback for measurement-based triggers up to their tier; higher-tier and non-measurement triggers escalate.
- Rollforward is a narrower option, safeguarded by a rollforward test-set and a wall-clock ceiling. Never available for supply-chain, cybersecurity, or serious-incident triggers.
- Deferred approvals time-box a criterion evaluation with a bounded expiry and a contingent action; exception approvals accept a known failure with a quantified residual, a specific mitigation, and a near-term expiry.
- Statute-tied criteria are non-exceptionable; the runbook names them per tier.
- Second-line effective challenge (SR 11-7 shape) is documented in the decision record's challenge log. Independence, competence, authority, and documentation are the four properties.
- Reverse-drills, incident cutover exercises, and challenge-log audits keep the runbook a *tested* control, not a document.
- The next chapter draws the dashboard the on-call reads to execute this runbook.
