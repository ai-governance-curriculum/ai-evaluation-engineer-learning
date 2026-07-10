# Mapping Release-Gate Outputs into ISO/IEC 42001 Clauses 8 and 9

## Motivation

Mod-101 chapter `03` walked all of ISO/IEC 42001's clauses 4–10 and named which pieces of the release-assurance program feed each clause. This chapter narrows to the two clauses the release-gate itself lives most tightly under — **clause 8 (Operation)** and **clause 9 (Performance evaluation)** — and answers a specific question: *when the gate produces its decision record, what documented information is created, and how does it stream into the AIMS in a form an auditor recognises without translation?*

Two clauses matter because 42001 draws a clean line between *doing the thing* and *watching how the thing performs*. Clause 8 is the operation of the AIMS — plan the operation, control the changes, run the risk assessment and treatment during operation, run the impact assessment during operation. Clause 9 is monitoring, measurement, analysis, evaluation, internal audit, and management review. The release-gate is a clause-8 activity that *generates evidence for clause 9*. If the gate does not stream into clause 9, the AIMS has a monitoring hole.

If the mapping is done sloppily, three failure modes appear at audit time:

1. **Un-cited operational control.** The release-gate SOP exists but does not identify itself as the operational control under 8.1; the auditor asks "how do you control operation of AI systems in scope?" and the answer wanders through peer-track methodology.
2. **Missing change-control trail.** A model is retrained and re-deployed but the change-control trail under 8.2 does not link to a fresh gate outcome. The auditor cannot tell whether the change was gated.
3. **Un-cited performance-evaluation loop.** Post-market signals are collected (mod-110) but not linked to specific release-gate outputs under clause 9. The AIMS looks like it monitors but cannot show how the monitoring changes future gates.

This chapter walks the clause-by-clause hooks the gate has to satisfy.

## Clause 8 — Operation: the four sub-clauses that matter

The 42001 clause 8 structure (at time of writing) has:

- **8.1 — Operational planning and control.** The clause that requires the organisation to *plan, implement, and control the processes needed to meet AIMS requirements and to implement the risk-treatment plan.*
- **8.2 — AI risk assessment (during operation).** Or, more precisely, *AI risk assessment* as an operational activity — the standard requires the assessment to be updated during operation, not only at planning time.
- **8.3 — AI risk treatment (during operation).** The corresponding operational treatment.
- **8.4 — AI system impact assessment (during operation).** The clause that ties operational activity to the ISO/IEC 42005-shaped impact assessment.

(Sub-clause numbering can vary as the standard evolves; cite the version of 42001 in force in the AIMS scope document. The mapping below is stable in shape even when the sub-clause numbering shifts.)

### 8.1 hooks — operational planning and control

**What the standard asks.** Documented procedures for the operation of the AIMS, including operational controls that ensure planned outcomes.

**What the release-gate contributes.**

- **The release-gate SOP.** The standing procedure from chapter `01` is the operational control the standard asks for. It cites its own version, references the criterion-set version, and points to the assurance-case template (mod-102).
- **The change-control SOP.** The procedure that determines whether a proposed change requires a fresh gate, a delta gate, or no gate. This is what an auditor will ask for under 8.1, and — depending on the standard's structure — under a change-control-focused sub-clause.
- **The per-release decision record.** Each pass through the gate produces a decision record naming the model version, the deployment surface, the criteria evaluated, the signers, the disposition, the residuals, and the rollback contract. This record is the operational-control output the auditor traces.

**Documented information.** The auditor's trace: from the SOP (a controlled document under 7.5) → to the criterion set (versioned under configuration control) → to the decision record (per-release, immutable in the evidence pipeline) → to the assurance case (mod-102, versioned in SACM) → to the artefact bundle (mod-104).

### 8.2 hooks — AI risk assessment during operation

**What the standard asks.** The AI risk assessment (originally performed under clause 6.1) is *reviewed and updated* during operation, particularly when the deployment context, use case, or system changes.

**What the release-gate contributes.**

- **Delta risk-assessment on change.** Every time the change-control SOP determines a fresh gate is required (retraining, judge change, guardrail change, deployment-surface expansion, new jurisdiction), the gate's intake includes a *delta risk-assessment record* — what changed, which risk categories are affected, whether the harm inventory (mod-102 leaves at the risk-engineer L25) needs revision.
- **Interfaces into ISO/IEC 23894 methodology.** The risk-assessment update itself follows 23894 (mod-101 chapter `03`); the release-gate's contribution is to *close the loop* — capture the update, tie it to the specific release, cite it in the decision record.

**Documented information.** The delta risk-assessment record referenced from the decision record, tied to the harm-inventory version, tied to the SACM `Claim` nodes affected.

### 8.3 hooks — AI risk treatment during operation

**What the standard asks.** The risk-treatment plan (originally in 6.1) is operationalised, its effectiveness is monitored, and treatments are revised where needed.

**What the release-gate contributes.**

- **Treatment-effectiveness measurement at each gate.** For each risk that had a mitigation stated at 6.1 planning, the release-gate re-verifies effectiveness on the current release candidate. This is the direct hook for guardrail-eval, red-team retest, and the risk-engineer L25 evidence contract (chapter `04`).
- **Residual-risk disposition on each release.** The decision record explicitly names residuals — a mitigation that came in below threshold, a defeater that lacks a mitigation and is being accepted, a treatment that was deferred. Residuals get an owner and an expiry.

**Documented information.** The residual-risk register per release, cross-linked to the assurance-case defeater/mitigation pass (mod-102 chapter `05`).

### 8.4 hooks — AI system impact assessment during operation

**What the standard asks.** The AI system impact assessment (originally under 6.1, and using ISO/IEC 42005 as the method) is reviewed and updated during operation.

**What the release-gate contributes.**

- **Impact-assessment refresh on change.** Every retrain, judge change, deployment-surface expansion, or jurisdiction addition triggers a review of the impact assessment. The gate refuses to run without a stated impact-assessment version, and the decision record cites it.
- **Cross-link to EU AI Act FRIA / SIA obligations.** Where the deployer (Article 26) or the provider (Article 27, if applicable) has a Fundamental-Rights Impact Assessment obligation, the 42001 impact-assessment refresh is the AIMS-side counterpart. Cross-mapping is owned in mod-106; the gate produces the trigger.

**Documented information.** The impact-assessment version cited in each decision record, and the change-log of the impact assessment itself.

## Clause 9 — Performance evaluation: three sub-clauses that matter

Clause 9 in the Harmonised Structure typically has:

- **9.1 — Monitoring, measurement, analysis, evaluation.**
- **9.2 — Internal audit.**
- **9.3 — Management review.**

Each of the three is fed by the release-gate.

### 9.1 hooks — monitoring, measurement, analysis, evaluation

**What the standard asks.** Determine what needs to be monitored and measured; determine methods; determine when; determine when the results are analysed and evaluated. Retain documented information as evidence of results.

**What the release-gate contributes.**

- **The rubric (chapter `02`) is the determined "what is measured."** Each rubric row is a monitored characteristic. The 25059 dimension is the *what*, the MEASURE sub-category is the *why (framework)*, the metric is the *how*.
- **The gate walker (chapter `01`) is the "how methods are applied."** The pre-registered thresholds are the "when — pass or defer." The decision record is the "results and analysis."
- **Streaming into post-market.** The rubric rows tagged for continuous monitoring feed mod-110's ongoing signals. The gate's output is not just a snapshot decision; it is a *baseline* that mod-110's online-eval slice measures against.

**Documented information.** The rubric (versioned), the decision records (immutable), the post-market monitoring plan tied to the rubric, and the mod-110 dashboards showing the ongoing state.

### 9.2 hooks — internal audit

**What the standard asks.** Conduct internal audits at planned intervals to determine whether the AIMS conforms to the organisation's requirements and to the standard's requirements, and is effectively implemented and maintained.

**What the release-gate contributes.**

- **A gate-audit input.** Internal audit walks a sample of decision records against the SOP, the rubric, and the evidence bundle. The release-gate's design must make that walk feasible: the decision record is a *linkable* artefact (mod-104's evidence pipeline pins it), and the record's citations resolve.
- **A gate-audit output.** The internal-audit finding either lands as a corrective action against the gate SOP (chapter `05`'s runbook), the rubric (chapter `02`), the criterion set, or an evidence contract (chapter `04`). Findings feed clause 10 (improvement).

**Documented information.** Internal-audit findings tied to the gate SOP version, corrective-action records, and the closure trace.

### 9.3 hooks — management review

**What the standard asks.** Top management reviews the AIMS at planned intervals to ensure continuing suitability, adequacy, and effectiveness.

**What the release-gate contributes.**

- **Standing management-review inputs.** Each management-review cycle receives release-gate metrics (throughput, decisions, exception approvals granted, rollbacks executed), open residuals, corrective-action status, and framework-change impact (e.g. what an EU AI Act GPAI-Code-of-Practice update means for the rubric).
- **Standing management-review outputs.** Direction to tighten thresholds, expand rubric coverage, adjust exception-approval delegation, extend third-party evaluator interfaces (mod-109) — all of which land as work back on the assurance program.

**Documented information.** The standing management-review agenda (a controlled document under 7.5), the review minutes, and the actions arising.

## What the release-gate's outputs look like on the AIMS side

The mapping above, rearranged so the *left column* is a gate output and the *right column* is the clause hook:

| Release-gate output               | 42001 clause hook                                                       |
| --------------------------------- | ----------------------------------------------------------------------- |
| Release-gate SOP (version-controlled) | Clause 7.5 (documented information) + Clause 8.1 (operational control) |
| Rubric (version-controlled)       | Clause 8.1 + Clause 9.1                                                 |
| Criterion set for release rc-*    | Clause 8.1                                                              |
| Decision record for rc-*          | Clause 8.1 + Clause 9.1 + (feeds 9.2, 9.3, 10.1)                        |
| Delta risk-assessment record      | Clause 8.2 (with reference back to 6.1)                                 |
| Treatment-effectiveness measurement | Clause 8.3                                                             |
| Residual-risk register            | Clause 8.3 + Clause 10.1                                                |
| Impact-assessment refresh         | Clause 8.4 (with reference to ISO/IEC 42005 method)                     |
| Rollback / rollforward contract   | Clause 8.1                                                              |
| Reverse-drill test record         | Clause 8.1 + Clause 9.1                                                 |
| Post-market handoff (rubric → mod-110) | Clause 9.1                                                          |
| Internal-audit findings (gate-scoped) | Clause 9.2                                                          |
| Management-review inputs          | Clause 9.3                                                              |
| Corrective actions from gate-scoped audit findings | Clause 10.1                                             |

This one table is what the AIMS auditor uses to plan the audit path. Handing it over at audit intake shortens the audit substantially.

## Worked example — one clause, one gate

Take a T2 gate that promotes an updated customer-intent classifier. The auditor walks 9.1 first.

1. The rubric (v3) lists the six 25059 dimensions with per-dimension criteria.
2. The criterion set (`gate-criteria-rc-2026-07-<hash>-v1`) is derived from rubric v3, with per-criterion thresholds and pre-registered hard / soft labels.
3. The decision record (`decision-rc-2026-07-<hash>`) resolves each criterion against the evidence bundle and gives the disposition.
4. The rubric rows tagged `continuous` (drift, calibration, guardrail-effectiveness) point at mod-110 dashboards.

The 8.1 walk is similar but starts from the SOP, then criterion set, then decision record. The 8.2 walk starts from the delta risk-assessment record, references the change-control SOP entry that triggered it, and terminates in the decision record. The 8.3 walk starts from the treatment-effectiveness measurement rows in the rubric and terminates in the residual-risk register.

At no point does the auditor need to translate — every artefact carries the version, the clause citation, and the peer track that produced it.

## Annex A cross-linkage, briefly

Beyond clauses 4–10, ISO/IEC 42001 Annex A lists AI-specific controls. Two Annex A categories are directly touched by the gate:

- **AI system life cycle** controls — planning, requirements, design, verification and validation, deployment, operation, retirement. The gate is the *deployment* control and the *operation* control's chief operational surface.
- **Assessing impacts of AI systems** controls — the gate refuses to run without a stated impact assessment; the impact assessment discharges these controls.

Annex A cross-linkage in the rubric is optional at this altitude but useful for the AIMS certification body's evidence walk; mod-106 owns the full obligation crosswalk.

## Common failure modes at audit

- **The SOP exists but the decision records do not cite it by version.** The auditor cannot bind operation to the control document.
- **Change-control SOP separates from the gate SOP with no cross-reference.** Retrains happen; some are gated, some are not; the auditor cannot verify coverage.
- **Rubric versions and criterion-set versions are not aligned.** A criterion in a decision record does not resolve to a rubric row.
- **Residuals are recorded but have no expiry.** Under clause 10, that reads as an open non-conformity.
- **Reverse-drill records are absent.** The rollback contract exists but has never been tested; the auditor treats the rollback as unfired.
- **Post-market signals are recorded but not tied back to a specific gate output.** Clause 9.1's *analysis* and *evaluation* look absent even though the raw signals are collected.

## What the assurance owner does on the day-of-audit

The AIMS auditor asks for four folders:

1. The gate SOP + rubric + criterion set (7.5, 8.1, 9.1).
2. A sample of decision records (the auditor chooses; the owner produces).
3. The residual-risk register and change-log (8.3, 10.1).
4. The post-market monitoring linkage and the internal-audit findings on gate-scope (9.1, 9.2, 9.3).

If each folder has version numbers on the cover and citations that resolve, the audit is short. If the auditor has to hunt across systems, the audit is long. The design guidance in this chapter is optimised for the short audit.

## Where this feeds

- Chapter `04` — the evidence-contract clause identifiers cited above are the *consumer contracts* the gate signs with each peer.
- Chapter `05` — the runbook operationalises the clause-8 controls (rollback triggers, deferred approvals, exception approvals) as procedures under 8.1.
- Chapter `06` — the dashboard is the reader's view of the clause-9.1 monitoring layer.
- mod-104 — the evidence pipeline is the 7.5 documented-information substrate that all of the above lives in.

## Summary

- The release-gate is a clause-8.1 operational control. It also feeds 8.2 (delta risk-assessment on change), 8.3 (residual-risk register), and 8.4 (impact-assessment refresh).
- The rubric + decision record + post-market handoff is the clause-9.1 monitoring, measurement, analysis, and evaluation loop.
- Gate-scoped internal-audit findings and gate-metrics feed 9.2 and 9.3, and corrective actions land under 10.1.
- Each gate output carries version numbers and clause citations so the AIMS auditor can walk it without translation.
- Annex A life-cycle and impact-assessment controls are discharged by the gate's existence + reverse-drill + impact-assessment refresh.
- Common failure modes are un-cited SOPs, mis-aligned versions, un-tested rollbacks, un-expiring residuals, and un-tied post-market signals — the design in this module removes each.
- The next chapter turns to the *consumer contracts* the gate signs with the four peer tracks whose evidence it depends on.
