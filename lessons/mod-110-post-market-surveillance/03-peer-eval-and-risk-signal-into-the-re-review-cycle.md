# Peer-Eval and Risk Signal into the Re-Review Cycle

## Motivation

Chapters `01` and `02` fixed the statutory backbone — the Article 72 plan and the Article 73 workflow. The plan says *what* is monitored; the workflow says what happens when a monitored signal is severe enough to be an incident. This chapter connects the two to the *ordinary* signal — the online-eval regressions, the trace-based anomalies, the harm-model updates, the adversarial-eval refresh findings — and shows how that signal drives the *re-review cycle* that keeps the assurance case (`mod-102`) and the release-gate decision (`mod-103`) alive.

The pivotal design decision is the *deferral contract*: the release-assurance owner does **not** author the online-eval and does **not** author the adversarial refresh. Those methodologies are owned by two peer tracks — the AI Evaluation Engineer at level 30 for online-eval and trace-based signal, and the AI Risk Engineer at level 25 for harm inventory and adversarial-eval refresh. What this role owns is the *trigger contract*: given a signal from a peer, what re-review does the assurance case demand, and what evidence must be refreshed before the release decision is reaffirmed, downgraded, or reversed.

Without a signal-to-trigger contract, one of two things fails. Either the peer's signal is *rich* but the assurance programme does not act on it (regression fires; the case is never reopened; the release decision decays silently). Or the assurance programme *over-acts* on every signal, triggering re-reviews so frequently that the peer's signal becomes noise the programme learns to ignore. The contract in this chapter is what gets both wrong-modes out of the way.

## What signal is consumed, from where

The assurance programme consumes signal from three peer sources. Each source has an owner peer track, an ingest cadence, a store landing, and a defined *type* of re-review it can trigger.

### From `ai-eval-engineer` (level 30, AI Engineering track)

- **Online-eval regression signal.** The AI-eval peer runs online-eval on a sampled slice of production traffic (Phoenix, Langfuse, Weave, or an internal substrate — `mod-104` chapter `02`). Each eval record lands as a content-addressed artefact with the seven lineage dimensions (`mod-104` chapter `01`). The peer emits a *regression alert* when a pre-registered metric on the online slice drops below a pre-registered threshold with pre-registered statistical significance.
- **Trace-based anomaly signal.** The peer's trace substrate detects anomalies in per-turn latency, per-tool-call rate, hallucination-indicator rate, refusal rate, or novel-output-pattern rate. Each anomaly emits a bundle of pinned traces plus a signature-of-the-anomaly summary.
- **Judge-agreement drift.** For LLM-as-judge eval pipelines, the peer monitors judge-vs-human agreement on a held-out slice; drift there indicates that the judge itself has moved, and every metric downstream of the judge is suspect.

### From `ai-risk-engineer` (level 25, ML Engineering track)

- **Harm inventory update.** The risk-engineer peer maintains the harm inventory (`mod-102` chapter `06`). When a new harm is added (a new failure mode observed in the wild, a new stakeholder group identified, a new deployment context), the inventory revision lands in the store with a signed diff.
- **Adversarial-eval refresh.** On a stated cadence (quarterly, typically) the risk-engineer refreshes the red-team engagement against the current threat model, produces a signed engagement report, and re-derives the adversarial-eval score.
- **Guardrail-eval refresh.** The risk-engineer refreshes the guardrail evaluation (block-rate, over-block-rate, adversarial bypass rate) and emits a refresh report.
- **Incident-derived learnings.** Every serious incident (chapter `02`) produces a learning-capture record owned by the risk-engineer; the record enters the assurance store as a fresh harm-inventory row or a rubric-amendment recommendation.

### From external sources (chapter `05` covers in depth)

- Public incident registries (AI Incident Database, OECD.AI Incidents Monitor, MIT AI Risk Repository) — matched to the inventory on a stated cadence.
- Notified-body inspection findings.
- Market-surveillance-authority notices.
- Deployer channel escalations.

## The deferral contract in one paragraph

The release-assurance programme does not build online-eval, does not build the harm inventory, and does not build the adversarial-eval refresh. It **specifies the re-review triggers** the peers' signal fires, and **consumes** the peers' signed artefacts as evidence in the re-opened assurance case. The peer owns the *methodology*; the assurance owner owns the *disposition*.

This contract keeps the peer tracks accountable for the depth and rigor of their methodology (they own it, they are audited on it) and keeps the assurance owner accountable for the release-decision integrity (they own the trigger contract, they are audited on it). Both accountabilities are documented in the RACI (`mod-101` chapter `03`).

## Trigger design

A trigger has five parts: *source*, *metric*, *threshold*, *persistence window*, *authoriser*. Each is pre-registered in the Article 72 plan (chapter `01`) and referenced from the assurance case's claim it defeats.

### Source and metric

Every trigger names a *specific* peer artefact class and a *specific* metric within it. Vague triggers ("if quality drops") are not triggers — they are wishes. A well-formed trigger reads: "if the AI-eval peer's online-eval `per-class-F1` metric on the `harm-eval-set/v3.2` slice reports a 95% bootstrap CI lower bound below 0.80…". The metric name matches exactly what the peer emits; the slice name is one the peer maintains.

### Threshold

Thresholds are pre-committed *before* the peer produces the signal, so that the threshold reflects the release-gate declaration rather than a post-hoc rationalisation. Three threshold classes recur:

- **Statistical significance** — the drop must be statistically significant at a pre-registered `alpha` (typically 0.05, sometimes 0.01 for high-tier deployments). This defeats the "single-batch noise" false trigger.
- **Risk-tier promotion** — a new harm added to the inventory promotes to a re-review trigger only if it exceeds a pre-registered severity band (typically S3 and above on the risk-engineer's severity scale, or a "reasonably foreseeable and likely" combination on the likelihood-severity matrix).
- **Adversarial-severity floor** — an adversarial-eval fresh finding triggers re-review at severity S or higher on the risk-engineer's adversarial scale (the scale is the peer's; the floor is the assurance owner's contract).

### Persistence window

Some triggers require signal to *persist* across multiple observation windows to fire. This defeats single-batch noise, and it also defeats the fire-and-recover pattern where a metric dips briefly and recovers unassisted. Typical persistence windows: two consecutive 30-minute batches for high-frequency metrics, three consecutive daily observations for moderate-frequency, four consecutive weekly observations for slow-moving metrics. Persistence windows are pre-registered per metric.

### Authoriser

Every trigger names *who* dispositions the re-review. Statistical-warrant triggers on measurement-based signal are pre-authorised to the on-call assurance engineer at the tier they cover. Risk-tier promotion triggers escalate to the release-owner. Adversarial-severity triggers at severity S or above escalate to the head of AI governance and, for T3-or-above deployments, to the second-line effective-challenge signer (`mod-103` chapter `05`).

## The "keep the release-gate decision alive" pattern

A passed release-gate at time `T` is valid only so long as its premise evidence is still fresh. When a trigger fires, the release-assurance programme executes a *re-review* of the assurance case, at the matching claim, in five steps:

1. **Identify the defeated claim.** The trigger names the specific assurance-case claim it defeats (for example, an online-eval regression on `per-class-F1` defeats the `Article-15-accuracy` claim discharged at gate). The re-review is *scoped* to that claim; the rest of the case is not reopened. This is important: an unscoped re-review is unaffordable in practice, and it dilutes the programme's ability to say what is being challenged.
2. **Pull the discharging evidence.** From the assurance bundle for the release under investigation (`mod-104` chapter `06`), retrieve the evidence artefact whose digest discharged the claim at gate. Verify the digest still resolves; verify the producer signature.
3. **Refresh or challenge the evidence.** Two paths — refresh (re-run the peer's methodology to produce a new signed artefact; compare) or challenge (identify a defeater in the existing evidence in light of the new signal; document it). The refresh path is preferred where the methodology admits a re-run at wall-clock affordable to the release; the challenge path is used where the re-run is prohibitively slow.
4. **Update the case.** The case's claim is either *reaffirmed* (refreshed evidence discharges it at the same threshold), *downgraded* (evidence supports a lower threshold; the release-tier drops per `mod-108`), or *defeated* (evidence does not discharge; the release decision reverses per chapter `05`).
5. **Update the store.** The re-review is a signed artefact in the assurance store, referenced from the assurance bundle by supersession (`mod-104` chapter `06`). The reader six months later can see (a) what the case said at gate, (b) what triggered the re-review, (c) what the re-review concluded, and (d) what disposition was signed.

Every step is documented; every signature is Rekor-logged; the trail is what makes the "kept alive" claim defensible under EU AI Act Article 72 paragraph 1's "actively and systematically" language.

## NIST AI RMF as the framework backing

NIST AI RMF's `MANAGE` function frames the same pattern. `MANAGE-4.1` reads (paraphrased from the NIST AI RMF 1.0 Playbook): AI risks and benefits from third-party resources are regularly monitored, and risk controls are applied and documented. The Playbook (see the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook)) elaborates on the post-deployment monitoring cadence, the tie-in to `MEASURE` (the evidence that establishes the risk in the first place), and the documentation obligations.

The release-assurance programme's re-review cycle is the operational shape of `MANAGE-4.1` applied to the release-gate decision. Programmes running under both NIST AI RMF and EU AI Act cite the two side-by-side — the framework citation gives the *why*, the Regulation citation gives the *must*.

## Worked shape — one trigger, one re-review

A T2 customer-service RAG assistant (chapter `01`'s worked example) is at release candidate `rc-2026-07-03`, promoted five weeks ago. The assurance case's `Article-15-accuracy` claim was discharged at gate by an eval record with digest `sha256:74a1…` on the `financial-services-intent/v3.2` slice, showing per-intent F1 = 0.87 (CI lower bound = 0.84) against the declared threshold of 0.85 (lower bound ≥ 0.83).

**Day 35, 09:00.** The AI-eval peer's online-eval reports per-intent F1 on the production slice at 0.82 (CI lower bound = 0.78) — below the declared threshold. The peer's regression alert fires. Signature: peer's key. Persistence: three consecutive daily observations at CI lower bound below 0.80. Statistical significance: p < 0.01.

**Day 35, 09:15.** The assurance programme's on-call receives the alert. Trigger classification: `TRG-ART-15-ACC-01` — an online-eval regression trigger on the `Article-15-accuracy` claim. Pre-registered disposition: on-call authorised to initiate re-review at T2.

**Day 35, 10:00.** Re-review opened. Scope: `Article-15-accuracy` claim only. Legal hold applied to the current-release assurance bundle so no evidence expires during investigation.

**Day 35, 11:00.** The AI-eval peer runs a refresh on a stratified sample of production traces. New eval record produced, signed, and lodged in the store as `sha256:c2fb…`. Refreshed measurement: per-intent F1 = 0.81 (CI lower bound = 0.77).

**Day 35, 13:00.** The refreshed evidence does not discharge the claim at the declared threshold. Two dispositions on the table: downgrade the release tier (deployment scope shrinks until the peer produces evidence at the higher threshold — `mod-108`), or defeat the claim and reverse the release-gate decision.

**Day 35, 15:00.** Release-owner and second-line signer co-sign a *forced downgrade*: the assistant continues to run but only for a subset of intents where the per-intent F1 refresh remained at or above 0.85. All other intents route to human-only handling. Disposition is a fresh signed artefact in the store, referenced from a superseded assurance bundle `rc-2026-07-03/superseded-by/downgrade-2026-08-08`.

**Day 35, 16:00.** The Article 72 plan is amended: the KL-divergence threshold on the retrieval-relevance drift monitor is tightened, and a per-intent F1 alarm is added at a lower persistence window (two daily observations, not three). Amendment lands as `postmarket-plan/customer-triage-assistant/v2` in the store.

**Day 42.** A retraining candidate is prepared and enters the release-gate cycle for evaluation as a candidate for lifting the downgrade. The re-review record is one of the inputs to the next release-gate walk.

At no point in this walk did the assurance owner *do* the online-eval or the retraining — the AI-eval peer and the ML-engineering team did. The assurance owner *triaged the signal against the contract*, *dispositioned the re-review*, *co-signed the downgrade*, and *amended the plan*. That is the role.

## Anti-patterns

- **Signal-consumer becomes signal-producer.** The assurance programme starts running its own online-eval because the peer's cadence is too slow. This is the `mod-101` backfill trap: the second line is doing first-line work; the accountability blurs; the audit finds it.
- **Every signal triggers a full re-review.** Re-reviews become weekly, ceremonial, non-substantive. Fix: scoped re-reviews, pre-registered thresholds, persistence windows.
- **No signal ever triggers a re-review.** The peer emits alerts; the assurance programme logs them; nothing happens. Fix: trigger contract binds signal to disposition; the audit reads the trigger register against the alert register and flags gaps.
- **The re-review is not recorded.** The re-review runs informally, no signed artefact lands in the store, the release decision is quietly downgraded without an audit trail. Fix: every re-review is a signed artefact; supersession is explicit.
- **The peer's methodology is not read.** The assurance owner triggers a re-review on signal whose statistical basis they do not understand. Fix: the trigger contract includes a *methodology-read* attestation — the assurance owner has read the peer's evidence-contract row (`mod-102` chapter `06`) and can articulate what the metric measures.

## The trigger register as a first-class artefact

A programme running the pattern well maintains a *trigger register* — an append-only list of every trigger the programme has defined, with the source, metric, threshold, persistence window, and authoriser fields spelled out; and a *fire register* — an append-only list of every trigger that has fired, with the timestamp, the peer artefact that raised it, the disposition, and the wall-clock the disposition landed on.

Reading the two registers side by side gives the audit the *health check* on the pattern:

- Triggers defined but never fired over long periods may be either over-strict (the threshold is unreachable) or over-scoped (the metric never approaches the threshold in practice). Either is an argument for tightening.
- Triggers that fire often and always disposition to "reaffirm" may be over-loose (the threshold is too generous) or the persistence window may be too short. Either is an argument for widening.
- Triggers that fire and disposition to "downgrade" or "defeat" repeatedly against the same claim indicate a *systemic* issue — the underlying evidence at release time was probably weaker than the case argued. Feed back into `mod-103`'s rubric design.

Under ISO/IEC 42001 clause 9.3 (management review), the trigger register and the fire register are standing inputs to the periodic review. Under NIST AI RMF `MANAGE-4.3` (continuous improvement), the same registers are the input to the improvement loop.

## Timing and the wall-clock discipline

A trigger contract that does not name wall-clocks is not enforceable. Every disposition class carries a pre-registered wall-clock:

- **Reaffirm** — inside one review cycle (typically one business week for standing metrics; faster for continuous metrics).
- **Forced retest** — the retest itself must complete within `N` days (pre-registered per criterion class, typically 5-15 business days depending on peer methodology).
- **Forced downgrade** — the downgrade must be deployed within one business day of the co-sign, per the tier architecture in `mod-108`.
- **Defeat / withdrawal** — deployment stops within the shortest applicable notification wall-clock (typically inside 24 hours), with formal Article 20 corrective action scheduled to begin within the next business day.

Wall-clocks apply to the assurance programme's own dispositions. They do *not* substitute for statutory wall-clocks (chapter `02`'s Article 73 clocks, GDPR's 72 hours, sector-rule clocks) — the two run in parallel and the shortest applicable governs the notification path.

## Where this shows up in the rest of the track

## Where this shows up in the rest of the track

- `mod-102` chapter `05` — defeaters framing gives the vocabulary for what a re-review is challenging.
- `mod-102` chapter `06` — the evidence-contract row per peer track names the artefact classes the trigger contract consumes.
- `mod-103` chapter `05` — rollback triggers are one class of re-review disposition; the runbook and the re-review cycle share vocabulary.
- `mod-103` chapter `06` — the dashboard reads the trigger register and displays live signal.
- `mod-104` chapter `06` — the re-review supersedes the assurance bundle by adding a new signed artefact.
- `mod-108` — forced downgrade is a re-review disposition landing on the tier architecture.
- `mod-112` — running the trigger contract across a portfolio is a management-review input under ISO/IEC 42001 clause 9.3.

## Summary

- The assurance programme consumes signal from `ai-eval-engineer` (level 30, online-eval regression, trace anomaly, judge-agreement drift) and from `ai-risk-engineer` (level 25, harm inventory update, adversarial refresh, guardrail refresh, incident learnings).
- The deferral contract keeps the assurance owner out of building methodology — the peer owns depth; the assurance owner owns disposition.
- A trigger has five parts: source, metric, threshold, persistence window, authoriser. All pre-registered in the Article 72 plan.
- The "keep the release-gate decision alive" pattern re-opens the specific defeated claim, refreshes or challenges the discharging evidence, and reaffirms, downgrades, or defeats the claim.
- NIST AI RMF `MANAGE-4.1` and the RMF Playbook are the framework backing; EU AI Act Article 72 is the statutory obligation.
- Every re-review is a signed, superseding artefact in the assurance store — the trail is what makes the "actively and systematically" language of Article 72(1) defensible.
- Exercise 03 has you write the trigger contract for a named in-scope high-risk system, mapping peer artefacts to claims to dispositions to authorisers.
