# exercise-03: Peer-Eval Signal to Re-Review Triggers

**Estimated effort:** 3 hours

## Objective

Author the **trigger contract** for one in-scope high-risk release: for each peer-signal class chapter `03` enumerates — from `ai-eval-engineer` at level 30 (online-eval regression, trace-based anomaly, judge-agreement drift); from `ai-risk-engineer` at level 25 (harm-inventory update, adversarial-eval refresh, guardrail refresh, incident-derived learnings) — write triggers with all five parts (source, metric, threshold, persistence window, authoriser), map each trigger to the specific assurance-case claim it defeats, and specify the disposition wall-clock. Then author the trigger-register and fire-register schemas that operationalise the contract, rewrite the `mod-101` chapter `03` deferral-contract rows for the two peer tracks, and walk one worked signal end-to-end from peer artefact through re-review to a co-signed disposition and a superseding assurance-bundle record.

The exercise is design and authoring. The load-bearing artefact is the trigger contract itself — vague triggers ("if quality drops") are wishes, not triggers.

## Prerequisites

- Chapter [`03-peer-eval-and-risk-signal-into-the-re-review-cycle.md`](../03-peer-eval-and-risk-signal-into-the-re-review-cycle.md) — the deferral contract; the five-part trigger; the five-step re-review procedure; NIST AI RMF `MANAGE-4.1`; the trigger register and fire register; five anti-patterns.
- Chapter [`01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md`](../01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md) — the plan section 6 is where triggers are pre-registered.
- Chapter [`05-incident-db-back-feed-and-non-compliance-escalation.md`](../05-incident-db-back-feed-and-non-compliance-escalation.md) — the five outcome states (reaffirm / forced retest / forced downgrade / defeat / standing-review update) extend chapter `03`'s three, and the co-signing contract applies to every disposition.
- Familiarity with `mod-101` chapter `03` (RACI / deferral contract), `mod-102` chapter `05` (defeaters vocabulary), `mod-102` chapter `06` (evidence-contract row per peer track), `mod-103` chapter `05` (second-line effective-challenge signer), and `mod-104` chapter `06` (superseding-assurance-bundle discipline).
- NIST AI RMF Playbook (`MANAGE-4.1` and `MANAGE-4.3`) at [airc.nist.gov/AI_RMF_Knowledge_Base/Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook).

## Problem statement

Pick one in-scope high-risk system already through release-gate — the exercise requires an existing assurance case with claims a trigger can defeat. The choice must:

- **Have an existing assurance case.** A current release candidate (`rc-YYYY-MM-DD` or equivalent identifier) with a signed assurance bundle whose claims are the anchors the re-review reopens.
- **Have at least four assurance-case claims worth defeating.** As a floor: Article 9 misuse-resistance, Article 10 data-quality / drift, Article 13 transparency-and-user-instruction, Article 15 accuracy. Systems with additional claims (Article 14 human oversight, Article 15 robustness, Article 15 cybersecurity) yield richer triggers.
- **Have peer-track owners for both `ai-eval-engineer` and `ai-risk-engineer` signal.** Named individuals (with backup) for each peer track — the deferral contract's coordination has real names or role placeholders.
- **Have a current deployment tier from `mod-108`.** The tier scales the trigger contract's escalation rules — statistical-warrant triggers pre-authorise to on-call at T1/T2 but escalate at T3+.

Common shapes worth considering (reuse from exercise-01 for module coherence, or pick a new one):

- **Customer-service RAG assistant** deployed by a bank or a large B2C platform — the chapter `03` worked-example shape.
- **Agentic coding assistant** deployed by an engineering organisation — signal classes span accuracy on generated code, refusal on unsafe operations, tool-use anomaly.
- **Medical-imaging classifier** — signal classes span sensitivity/specificity drift, subgroup regression, adversarial-perturbation robustness.
- **Fraud-detection scoring model** deployed by a payments processor — signal classes span precision/recall drift, adversarial-evasion refresh, base-rate drift.
- **Content-moderation classifier** deployed by a platform — signal classes span block-rate, over-block-rate, adversarial-bypass rate, judge-agreement drift on LLM-as-judge pipelines.

Pin the release-candidate identifier, the four claims (or more), the peer-track owners with named individuals plus backup, and the current tier before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `trigger-catalogue.md`

At least ten pre-registered triggers, one per row, covering all three `ai-eval-engineer` signal classes and all four `ai-risk-engineer` signal classes. Columns per trigger:

- **Trigger identifier** — a stable slug (e.g., `TRG-ART-15-ACC-01`, `TRG-ART-9-MISUSE-02`).
- **Source** — the specific peer artefact class the trigger reads (e.g., "AI-eval peer's online-eval regression alert on the `financial-services-intent/v3.2` slice"; "risk-engineer peer's quarterly adversarial-eval refresh report").
- **Metric** — the exact metric name (matches what the peer emits) with the slice / population / harness identifier.
- **Threshold** — the pre-committed threshold with the threshold-class explicit (statistical significance at pre-registered `alpha` / risk-tier promotion at severity S3+ / adversarial-severity floor at S1+).
- **Persistence window** — how many observation windows the signal must persist across before firing (chapter `03`'s worked defaults: two consecutive 30-minute batches for high-frequency; three consecutive daily for moderate-frequency; four consecutive weekly for slow-moving).
- **Authoriser** — the role authorised to disposition the re-review at this trigger's class and tier.
- **Affected claim** — the specific assurance-case claim the trigger defeats (from the picked release's case).
- **Disposition wall-clock** — how quickly the disposition must land per chapter `03`'s wall-clock discipline (reaffirm within one business week; forced retest within N days pre-registered per criterion class; forced downgrade within one business day of co-sign; defeat / withdrawal within 24 hours).

Coverage requirements:

- At least three triggers on `ai-eval-engineer` signal (one per signal class).
- At least four triggers on `ai-risk-engineer` signal (one per signal class).
- At least one trigger per threshold-class (statistical significance, risk-tier promotion, adversarial-severity floor).
- At least one trigger tied to each of the four claims from the problem statement.
- At least one trigger that reads *judge-agreement drift* (if the deployment uses LLM-as-judge in its evaluation pipeline — otherwise mark the row `<!-- not applicable — deployment does not use LLM-as-judge -->` with rationale).

### 2. `disposition-decision-tree.md`

The decision tree from trigger-fired through the five-step re-review procedure to one of the five outcome states.

**Five-step re-review procedure** (from chapter `03`, spelled out for this deployment):

1. Identify the defeated claim — the trigger names the specific assurance-case claim; the re-review is scoped to that claim.
2. Pull the discharging evidence — from the assurance bundle (`mod-104` chapter `06`), retrieve the artefact whose digest discharged the claim at gate; verify the digest still resolves; verify the producer signature.
3. Refresh or challenge — refresh is preferred (re-run the peer's methodology; produce a new signed artefact; compare); challenge is used where re-run is prohibitively slow (identify a defeater in existing evidence in light of the new signal; document it).
4. Update the case — reaffirm / forced retest / forced downgrade / defeat / standing-review update.
5. Update the store — the re-review is a signed artefact; the assurance bundle is superseded by adding a new record.

**Outcome states** — the five states from chapter `05` mapped to this deployment:

- **Reaffirm** — refreshed evidence discharges the claim at the declared threshold; the release-gate decision stands.
- **Forced retest** — evidence pointer is stale but not defeated; retest within N days per criterion class or auto-escalate to downgrade.
- **Forced downgrade** — evidence does not discharge at the declared level but discharges at a lower level; deployment tier drops per `mod-108`.
- **Defeat / withdrawal** — evidence defeats the claim outright, or the incident is severe enough (Article 3(49) territory) that deployment stops.
- **Standing-review update** — the incident does not defeat a claim but *does* change the risk framing; a new claim is added or an existing claim's scope is amended.

**Authoriser routing per disposition class per tier** — a matrix showing which role signs which disposition at which tier:

- Statistical-warrant triggers → pre-authorised to on-call assurance engineer at T1/T2; release-owner co-sign at T3+.
- Risk-tier-promotion triggers → release-owner + second-line signer at all tiers.
- Adversarial-severity S1 triggers → release-owner + second-line signer + head-of-AI-governance at all tiers.
- Forced downgrade at T3+ → release-owner + second-line signer + head-of-AI-governance (chapter `05`'s escalation contract).
- Defeat / withdrawal → release-owner + second-line signer + head-of-AI-governance (chapter `05`'s escalation contract).

### 3. `trigger-and-fire-register-schemas.md`

The schema (in YAML-like or JSON-like pseudocode) for the two registers plus the auditor-facing health-check queries.

**Trigger register** — append-only, one entry per trigger definition. Fields:

- `trigger_id` — the stable slug.
- `defined_at` — timestamp (placeholder — no need for real time).
- `defined_by` — signer of the trigger definition.
- `source_artefact_class` — the peer artefact class the trigger reads.
- `metric_name` — the exact metric name.
- `threshold` — the pre-committed threshold with class.
- `persistence_window` — observation-window count.
- `authoriser_role` — the disposition role at this trigger's class.
- `affected_claim` — the assurance-case claim reference.
- `disposition_wall_clock` — the wall-clock for disposition.
- `superseded_by` — pointer to the trigger version that replaces this one (null while current).
- `plan_reference` — the Article 72 plan version this trigger is registered in.

**Fire register** — append-only, one entry per trigger firing. Fields:

- `fire_id` — a stable identifier for this firing.
- `trigger_id` — the trigger definition that fired.
- `fired_at` — timestamp.
- `raising_artefact_digest` — the peer artefact that raised the signal.
- `raising_artefact_signature` — the peer's signature.
- `re_review_id` — the re-review the firing opened (or `null` if no re-review triggered — with rationale).
- `disposition` — one of the five outcome states.
- `disposition_signers` — list of signer roles with signatures.
- `disposition_landed_at` — timestamp the disposition was signed.
- `wall_clock_hit` — the wall-clock this disposition landed under.
- `supersession_pointer` — the superseded assurance-bundle reference the disposition amends.
- `article_20_reference` — the corrective-action record the disposition drives (or `null` for reaffirm / standing-review update).
- `plan_amendment` — the Article 72 plan-amendment reference the firing produces (or `null` if no amendment).

**Auditor health-check queries**:

- **Silent triggers** — triggers defined but never fired over a stated window (e.g., 90 days). Argues either over-strict threshold or over-scoped metric.
- **Perpetually-reaffirming triggers** — triggers that fire often and always disposition to reaffirm. Argues either over-loose threshold or too-short persistence window.
- **Repeatedly-downgraded claims** — triggers that fire and disposition to downgrade or defeat repeatedly against the same claim. Argues systemic issue with the underlying evidence at release time; feed back into `mod-103` rubric design.
- **Missing supersession** — fire register entries whose supersession pointer is `null` when the disposition class requires one (any downgrade / defeat).
- **Unauthorised authoriser** — fire register entries whose signer role does not match the trigger definition's authoriser role.

### 4. `deferral-contract-rewrite.md`

A one-page rewrite of the `mod-101` chapter `03` deferral-contract entries for the `ai-eval-engineer` and `ai-risk-engineer` rows. For each peer row:

- **What the peer owns.** The methodology depth — the online-eval harness / the trace substrate / the judge design / the harm-inventory taxonomy / the red-team engagement design / the adversarial-eval scale. The peer is audited on the depth and rigor of the methodology.
- **What this programme owns.** The trigger contract (which peer signals fire which triggers), the disposition (which outcome state each firing produces), the supersession (the superseding assurance-bundle record). The programme is audited on the trigger-contract integrity and on the disposition trail.
- **Signed-artefact classes exchanged.** The specific artefact classes the peer produces and the programme consumes, with digest-pinning and signature discipline (`mod-104` chapter `01`).
- **Audit-question that verifies the contract has not blurred.** The specific question that surfaces the `mod-101` backfill trap ("is the programme running the peer's methodology because the peer's cadence is too slow?"). Chapter `03`'s anti-patterns section names the two most common blurring modes:
  - **Signal-consumer becomes signal-producer** — the programme starts running its own online-eval. Fix: the programme's re-reviews *consume* peer artefacts; they do not *produce* peer artefact classes.
  - **The peer's methodology is not read** — the programme triggers a re-review on signal whose statistical basis it does not understand. Fix: the trigger contract includes a methodology-read attestation — the assurance owner has read the peer's evidence-contract row (`mod-102` chapter `06`) and can articulate what the metric measures.

The rewrite is a controlled document — signer, version, review cadence. Both peer roles counter-sign to acknowledge the contract.

### 5. `worked-signal-walkthrough.md`

An end-to-end walk of one signal firing on the picked deployment, at the granularity of chapter `03`'s Day-35 worked example (hours, timestamps, digests). Structure:

- **Trigger firing.** Day-X hour-Y: the peer artefact raises the signal; peer's key signs the alert; persistence check passes; trigger `TRG-…-…` fires per the catalogue (artefact 1).
- **Programme intake.** Day-X hour-Y+15min: the on-call assurance engineer receives the alert; trigger classification confirmed; pre-registered disposition looked up (from artefact 2's decision tree).
- **Re-review opening.** Day-X hour-Y+1: re-review opened, scoped to the affected claim; legal hold applied to the current-release assurance bundle so nothing expires during investigation.
- **Refresh or challenge.** Day-X hour-Y+N: the peer runs a refresh (or the programme documents a challenge); new eval-record / new engagement report / new judge-agreement snapshot produced, signed, and lodged in the store as `sha256:xxxx…` (placeholder digest).
- **Disposition.** Day-X hour-Y+M: the refreshed evidence produces one of the five outcome states; release-owner + second-line signer (+ head-of-AI-governance where required by artefact 2's routing matrix) co-sign; disposition is a fresh signed artefact in the store.
- **Supersession.** Day-X hour-Y+M+30min: the assurance bundle is superseded — the store records `rc-…/superseded-by/downgrade-YYYY-MM-DD` or the equivalent supersession pointer.
- **Article 72 plan amendment.** Day-X+1: the plan is amended to tighten the trigger threshold or add an adjacent monitor (chapter `03`'s worked example does this); plan lands as `postmarket-plan/<system-slug>/vN+1`.
- **Article 20 corrective action** (where the disposition is downgrade or worse): the corrective-action record is signed and lodged, notified to the market-surveillance authority as required.
- **Fire-register entry.** Every field from artefact 3's fire-register schema is populated for this firing.

The walkthrough is invented content pinned to the picked deployment, but every field and every timestamp must be internally consistent — the trigger identifier matches the catalogue; the affected claim matches the case; the authoriser matches the routing matrix; the supersession pointer references the correct assurance-bundle version.

## Starter guidance

- **Source and metric names must match exactly what the peer emits.** The trigger contract is not aspirational — if the peer emits `per_class_f1` on `financial-services-intent/v3.2` and the trigger reads `per-class-F1` on `financial-services-intent/v3`, the contract is broken. Read the peer's evidence-contract row (`mod-102` chapter `06`) before authoring.
- **Thresholds pre-committed before signal appears.** A threshold set after the signal has been observed is a rationalisation, not a threshold. Every threshold is pinned to the release-gate declaration or to the harm inventory *before* the trigger is registered.
- **Persistence window defeats single-batch noise.** Chapter `03`'s worked defaults are a starting point — pre-register per metric based on the metric's frequency and noise floor.
- **Wall-clocks make the contract enforceable.** A trigger contract without wall-clocks is not a contract; it is aspiration.
- **Ownership single-named with backup, never "the team".** "The MLOps team" is not a named owner. "Alice Chen (backup: Bob Kim)" is.
- **Every re-review is a signed superseding artefact.** No informal downgrades. Chapter `03`'s anti-pattern *the re-review is not recorded* is the audit-trail-losing failure mode.
- **The peer is not the programme, and the programme is not the peer.** The deferral contract keeps both accountabilities crisp — peer owns methodology, programme owns disposition. Blurring collapses second-line-of-defence.
- **`<!-- needs-research: … -->` markers are legitimate.** Where a specific peer harness's metric name or a specific vendor's judge-model version would need verification, mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `trigger-catalogue.md` has at least 10 triggers covering all three `ai-eval-engineer` signal classes and all four `ai-risk-engineer` signal classes; every trigger has all five fields plus affected claim and disposition wall-clock; at least one trigger per threshold class; every claim from the problem statement has at least one trigger.
- `disposition-decision-tree.md` covers the five-step re-review procedure spelled out for this deployment, the five outcome states, and the authoriser-routing matrix per disposition class per tier. The head-of-AI-governance co-sign requirement for adversarial-S1 / T3+ downgrade / withdrawal is explicit.
- `trigger-and-fire-register-schemas.md` has both register schemas with every field enumerated; the five auditor health-check queries are all present and defensibly named.
- `deferral-contract-rewrite.md` covers both peer rows (`ai-eval-engineer` and `ai-risk-engineer`) with what-peer-owns / what-programme-owns / signed-artefact-classes / audit-question sections. Both anti-patterns (`signal-consumer becomes signal-producer` and `the peer's methodology is not read`) are explicitly addressed. Both peer roles counter-sign.
- `worked-signal-walkthrough.md` is internally consistent with the catalogue, decision tree, and register schemas; every timestamp is coherent; every signature is routed correctly; a superseding assurance-bundle record lands; the fire-register entry is populated per artefact 3's schema.
- Every owner is a single named individual with a named backup, not a team.
- Every place a fact would need to be verified against a specific peer harness's metric name, a specific vendor's judge-model, or the enterprise's own tier-scheme values is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Design the trigger-register audit query set.** In `audit-query-set.md`, expand the five health-check queries into a full auditor-facing report — for each query, the SQL / query-language expression, the expected pass rate over a stated window, and the escalation rule when a query returns findings. Cite ISO/IEC 42001 clause 9.3.
- **Sketch the dashboard live-signal view.** In `dashboard-live-signal-view.md`, describe the `mod-103` chapter `06` dashboard tile that reads the trigger register and the fire register in real time — the columns, the alert conditions, the drill-through to individual re-review records.
- **Accommodate an external-registry match.** In `external-registry-adapter.md`, sketch how the trigger contract accommodates a match from an external incident registry (chapter `05`) — the additional "source" enumeration value, the ingest cadence, and the disposition routing (chapter `05`'s three-axis match discipline plus the four disposition classes).
- **Add a vendor-model-refresh trigger class.** In `vendor-refresh-trigger.md`, extend the catalogue with triggers that fire when the underlying foundation-model provider silently refreshes the model version (a pattern chapter `01` flags as a drift source). The source is the platform-team's model-registry event; the metric is the model-digest inequality; the disposition is a forced retest at minimum.
- **Draft the `mod-101` deferral-contract diff.** In `mod-101-contract-diff.md`, produce the specific diff (as markdown-diff-style) against the existing `mod-101` chapter `03` deferral-contract text — the exact lines added / removed / modified. Signal that the rewrite is a controlled amendment.
