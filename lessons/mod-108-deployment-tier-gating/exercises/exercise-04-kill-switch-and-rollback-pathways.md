# exercise-04: Kill-Switch, Rollback, Downgrade, and Do-Not-Deploy Pathways

**Estimated effort:** 3 hours

## Objective

Design the **four reversal-side dispositions** — kill-switch, rollback, downgrade, do-not-deploy — for one product's tier landing from exercise `01`, and the **escalation contract** with the head of AI governance that each disposition triggers. Every disposition is designed *ahead* of the release, not chosen on the day of the incident. Every disposition names its authorising conditions, its signer, its reverse-drill cadence, and its trail obligations.

The exercise is authoring the *methodology-owner side* of the reversal pathways from chapter `04`. You do not design the kill-switch mechanism; you do not certify the rollback's technical feasibility; you do not build the operational runbook. Those are `ai-infra-mlops`, `ai-infra-security`, and operations peer work. You *require* the pathways, *name* their triggers and signers, and *cite* their test evidence in the tier-decision artefact.

## Prerequisites

- Chapter [`04-kill-switch-rollback-downgrade-and-do-not-deploy-pathways.md`](../04-kill-switch-rollback-downgrade-and-do-not-deploy-pathways.md) — the four dispositions, their design principles, and the escalation contract with head of AI governance.
- Chapter [`01-deployment-tier-gating-shape-across-frontier-labs.md`](../01-deployment-tier-gating-shape-across-frontier-labs.md) — the tier scheme whose axes downgrade paths are pre-designed against.
- Chapter [`03-cybersecurity-attestation-clauses-for-the-tier-gate.md`](../03-cybersecurity-attestation-clauses-for-the-tier-gate.md) — the cybersecurity-integrity conditions that trigger the kill-switch rather than a softer disposition.
- Exercise [`exercise-01-enterprise-tier-scheme-in-rsp-shape.md`](exercise-01-enterprise-tier-scheme-in-rsp-shape.md) — the tier scheme and the product's tier landing.
- Familiarity with `mod-103` chapter `05` (release-gate runbook) — the runtime rollback / rollforward triggers this exercise widens with tier-boundary crossings.

## Problem statement

Continue with the same product you scoped in exercise `01`. Design the reversal pathways for its current tier landing (and for the adjacent lower tier the downgrade path targets). Where the product lands high on the scheme (external-facing, `tools:High`-or-above, sector-regulated, or Annex III), the exercise is more demanding — the disposition matrix has to handle more failure modes and the escalation contract carries more weight. That is intentional.

Two failure modes to design against, both from chapter `04`:

- **Live-judgement dispositions.** The methodology owner is not making disposition calls on the day of the incident. The disposition matrix is pre-committed in the tier-decision artefact; the on-call executes the pre-committed pathway. If your exercise output leaves the choice of disposition to the on-call, the design is incomplete.
- **Mechanism design.** The methodology owner does not design the kill-switch mechanism, the rollback control-plane, or the downgrade tooling. Those are peer work. If your exercise output specifies the mechanism (which HTTP endpoint, which Envoy filter, which feature-flag path), you have crossed the boundary.

## Requirements

Produce six artefacts in a single directory.

### 1. `product-scoping-brief.md`

A short brief that names:

- **Product and tier landing.** Named product from exercise `01`; the current tier landing; the adjacent lower tier the downgrade path targets.
- **Deployment surface.** The concrete surface (API gateway, hosted inference, tool-execution runtime).
- **Peer-track partners.** The `ai-infra-mlops` peer lead (kill-switch mechanism, rollback control-plane), the `ai-infra-security` peer lead (kill-switch enforcement layer, integrity-trigger detection), the `head-of-ai-governance` role incumbent (escalation-contract counterparty), the on-call assurance engineer role (first-responder on the operational side).
- **Prior reversal history.** If any prior release of this product has fired a reversal disposition (kill-switch, rollback, downgrade), note the incident and the disposition chosen. If not, note that this is the first-release design.

### 2. `kill-switch-design.md`

The kill-switch design, at the level a tier-decision artefact reads it (not the mechanism-implementation level). Cover:

- **Named mechanism (peer-produced).** Pointer to the `ai-infra-mlops` / `ai-infra-security` peer's mechanism specification. The methodology owner does not restate the mechanism; the pointer suffices. Use a `<placeholder>` if the exercise scenario has no real mechanism to point at.
- **Enforcement layer.** State the enforcement layer at the level a reviewer needs — platform-layer (API gateway, inference-serving layer), not application-layer or client-layer. Cite chapter `04`'s "one switch, one action" and "enforced at the platform layer" principles as the design commitments.
- **Authorising conditions.** For each of the four kill-switch trigger classes below, name the authoriser:
  - Cybersecurity-integrity trigger (weights, prompts, judge configuration, or serving infrastructure compromise).
  - Serious-incident trigger (EU AI Act Article 73 threshold, sector-rule equivalent, or internal serious-incident definition).
  - Regulator or authority notice.
  - Downstream tool-invocation harm where rollback cannot restore an acceptable state in comparable time.
- **Failure-safe default.** Explicit statement of the switch's default state under control-plane outage. Defend the choice (fail-safe closed / fail-safe open) with reference to the deployment's blast radius and any secondary-harm considerations.
- **In-flight session handling.** How the switch interacts with stateful in-flight sessions — abrupt termination vs graceful drain vs deferred termination. This is *especially* important for an agent with tool-invocation sequences in flight.
- **Reverse-drill cadence.** How often the switch is fired against a non-production surface (typically monthly against staging, quarterly against production with pre-notification). Reference `mod-103` chapter `05`'s reverse-drill discipline.
- **Audit trail.** Every invocation records: who invoked, when, what tier, what trigger class, what wall-clock duration to full effect. The audit trail lands in the immutable evidence pipeline (`mod-104`).
- **Signer.** The methodology owner *requires* the kill-switch and *cites* the mechanism; the `ai-infra-mlops` peer *signs* the mechanism specification; the `head-of-ai-governance` *countersigns* for higher-tier products.

### 3. `rollback-design.md`

The rollback design. Distinguish and cover both flavours from chapter `04`:

- **Model-version rollback.** Serve the prior model version (or prior fine-tune, or prior system-prompt version) instead of the current one. Name the specific prior version the rollback targets, the RTO expectation, the prior version's re-activated assurance case and cards, and the trigger classes that admit this rollback.
- **Tier-configuration rollback.** Move the deployment back to the prior tier — prior permission envelope, prior mitigation set, prior evidence set. The model version does not change; only the tier does. Name the prior tier landing, the RTO, and the trigger classes that admit this rollback.

For each flavour:

- **Trigger classes.** Which trigger classes admit this rollback (typically a subset of chapter `mod-103` chapter `05`'s rollback triggers, cross-referenced).
- **RTO expectation.** How fast the rollback executes end-to-end (typically minutes to low tens of minutes for platform-side rollbacks; longer for tier-configuration rollbacks that touch contract commitments).
- **Reverse-drill cadence.** How often the rollback is exercised against a non-production surface.
- **Tier-boundary crossing check.** For each rollback flavour, whether the rollback itself crosses a tier boundary (from T2 back to T1, or from `tools:High` back to `tools:Med`). Cross-boundary rollbacks trigger the escalation contract (see artefact 6).
- **Signer.** Methodology owner + release-owner for within-tier rollbacks; head of AI governance for cross-tier rollbacks at high tiers.

### 4. `downgrade-paths-per-axis.md`

The downgrade paths, pre-designed per tier axis. For every axis in the product's tier landing, name the downgrade increment(s) — how the deployment moves one banding down on that axis without full withdrawal.

Structure as a table:

| Axis (from exercise `01`) | Current banding | Adjacent lower banding | Downgrade increment (concrete tool / population / autonomy change) | Trigger classes | Signer | Re-gate discipline |

For each row, be concrete:

- **Downgrade increment.** Not "restrict the tool set" (too vague) but "remove the write-tools from the agent's toolbox: CRM writes, ticketing writes, calendar creates" (concrete). Not "narrow the population" but "move from unauthenticated external users to authenticated users only; require MFA for authentication."
- **Trigger classes.** Which conditions admit downgrade on this axis specifically. Typical triggers: a capability-evidence spec (`02`) shows the model is measurably more capable than the tier assumed and the mitigation set at the current banding is not sufficient; a monitoring detector (`mod-110`) fires above threshold; a residual OWASP or ATLAS coverage gap becomes material.
- **Re-gate discipline.** A downgrade is not certified complete until the tier-decision artefact is re-authored at the new lower banding and re-signed. State the re-gate steps and the signer.

Then, in a closing paragraph, cover the *downgrade-without-re-gate* failure mode from chapter `04`: how the exercise's design prevents operational configuration and governance artefacts from diverging (the tier-decision artefact must be re-authored at the new banding).

### 5. `do-not-deploy-trail.md`

The do-not-deploy pathway. Cover:

- **Conditions.** The specific conditions under which do-not-deploy is the *mandatory* disposition:
  - A capability threshold is crossed at a level the enterprise's mitigation set does not have credible evidence for (RSP-style commitment).
  - A cybersecurity attestation cannot be discharged (`03`) and no compensating control is available.
  - A regulator prohibits the deployment under a specific statutory ground (EU AI Act Article 5 prohibited practices; sector rule prohibitions; deployer contract prohibitions).
  - A residual-risk register accumulation reaches a pre-committed non-deploy threshold.
- **Trail artefacts.** Every do-not-deploy decision has to *survive* — the failure mode is silent reversal. Name each trail artefact:
  - The tier-decision artefact recording the do-not-deploy disposition, rationale, signers, and expiry (do-not-deploy is often time-bounded).
  - The record in the residual-risk register.
  - The record in the assurance-programme's decision log (`mod-112`).
  - The watch item in the intake process (`mod-101`, `mod-103`) so that a *new* release of the same or a substantially similar system is flagged against the prior decision.
- **Expiry.** Do-not-deploy decisions are typically time-bounded — the decision may be revisited when specified evidence becomes available. State the expiry conditions (e.g., "the decision may be revisited once the AgentDojo v-next benchmark is available and re-run against the model"; "the decision may be revisited when the notified body's opinion on the specific Annex III sub-category is available").
- **Signer.** `head-of-ai-governance` signature is mandatory. The methodology owner cannot make a do-not-deploy decision unilaterally. Name the counterparty and the escalation timing.
- **Silent-reversal countermeasure.** Explicit statement of how the intake process at each future release checks the residual-risk register and the decision log for a prior do-not-deploy that would apply.

### 6. `escalation-contract-with-head-of-ai-governance.md`

The escalation contract with the head of AI governance, at the disposition level. For each of the four dispositions, cover:

- **Escalation trigger.** The specific condition (or trigger class) that escalates to the head of AI governance.
- **Escalation timing.** How fast the escalation happens (immediate for kill-switch on regulator notice; within 24h for cross-boundary rollback; on the next review cycle for downgrade with material contract change; before any deployment attempt for do-not-deploy).
- **Evidence set delivered.** What the methodology owner delivers into the escalation — the tier-decision artefact, the capability-evidence set, the cybersecurity attestation, the reversal-design section, the residual-risk register position.
- **Decision.** What the head of AI governance decides (approve, condition, escalate further, reject). For each disposition, name the decision types available.
- **Trail obligation.** What is recorded and where — decision log, tier-decision artefact update, communications to peer tracks and to contracted counterparties.

Then, in a table, cover the failure modes from chapter `04` — for each failure mode, the countermeasure the exercise's design applies:

| Failure mode | Countermeasure in the exercise's design |
| --- | --- |
| Silent tier drift | |
| Tier shopping between products | |
| Deferred approvals as de facto approvals | |
| Kill-switch that no one is authorised to fire | |
| Do-not-deploy without a trail | |
| Downgrade without re-gate | |

Each countermeasure is a specific pointer into one of artefacts 2–5 (the design *is* the countermeasure).

## Starter guidance

- **Fix scoping first, then design.** The product's tier landing and the adjacent lower tier drive the downgrade paths. Getting the landing wrong means restructuring the disposition matrix.
- **Every disposition is pre-committed.** The disposition matrix in the tier-decision artefact names, *ahead of time*, which triggers admit which dispositions and who signs each. If your artefacts leave the disposition to the on-call's judgement on the day, the exercise has left the discipline off.
- **Do not design the mechanism.** The methodology owner requires the kill-switch and cites the mechanism specification. Where in the stack the switch sits, how it enforces, what its default state is under control-plane outage — those are `ai-infra-mlops` and `ai-infra-security` peer work. Your kill-switch design artefact reads at the tier-decision-artefact level, not the mechanism-implementation level.
- **Kill-switch is the ratchet, not the default.** Kill-switch invocation is *not* the appropriate disposition when rollback or downgrade would restore an acceptable state in comparable time. The more surgical option is preferred. The trade-off is judgement, documented in the runbook — but the *conditions* are pre-committed, not judged on the day.
- **Downgrade is not a discount.** A downgraded deployment carries the mitigation obligations of *its new tier*, not a subset of them. The re-gate discipline in artefact 4 is what enforces this.
- **Do-not-deploy is not a delay.** A do-not-deploy decision without a trail can be silently reversed months later. The trail across artefact, register, decision log, and intake watchlist is the countermeasure. Design it in.
- **The escalation contract is bidirectional.** The head of AI governance is not just a signer; the contract also names what the methodology owner *delivers* into the escalation (evidence set) and what the decision types available *are*.
- **Reverse-drill cadence is not decorative.** A kill-switch that has never been fired is a hypothesis. A rollback that has never been exercised is an assumption. State the cadence and cross-reference `mod-103` chapter `05`.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the enterprise's own operational runbook, the peer track's mechanism specification, or the head-of-AI-governance role's own policy, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `product-scoping-brief.md` names the product, the tier landing and adjacent lower tier, the peer-track partners, and any prior reversal history.
- `kill-switch-design.md` names the peer-produced mechanism pointer, the enforcement layer, the four trigger-class authorisers, the failure-safe default, the in-flight session handling, the reverse-drill cadence, and the audit trail. The methodology-owner + peer-signer split is preserved.
- `rollback-design.md` covers both model-version and tier-configuration rollback flavours; each with trigger classes, RTO expectation, reverse-drill cadence, tier-boundary crossing check, and signer.
- `downgrade-paths-per-axis.md` provides one downgrade row per axis in the product's tier landing; each row is *concrete* (named tool changes, named population changes, named autonomy changes); the re-gate discipline is stated. The closing paragraph addresses the downgrade-without-re-gate failure mode.
- `do-not-deploy-trail.md` names the mandatory conditions, the four trail artefacts, the expiry conditions, the head-of-AI-governance signer, and the silent-reversal countermeasure.
- `escalation-contract-with-head-of-ai-governance.md` covers, for each of the four dispositions, the escalation trigger, timing, evidence set delivered, decision, and trail obligation. The failure-mode countermeasure table has one countermeasure per failure mode, each pointing into a specific design artefact.
- No artefact leaves the choice of disposition to the on-call's live judgement. Every disposition is pre-committed with a named trigger and signer.
- No artefact designs the kill-switch mechanism, the rollback control-plane, or the downgrade tooling. Every mechanism reference is a pointer to peer work.
- Every place a fact would need to be verified against the enterprise's operational runbook or the peer track's own current specification is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Author the reverse-drill test plan for the kill-switch.** In `reverse-drill-plan.md`, sketch a quarterly kill-switch drill against production — pre-notification to affected counterparties, drill scope (fire the switch, verify inference stops, verify audit trail, restore inference), success criteria, failure protocol, sign-off. Cross-reference `mod-103` chapter `05`'s reverse-drill discipline.
- **Draft the cross-jurisdictional do-not-deploy variant.** In `cross-jurisdictional-do-not-deploy.md`, sketch how a do-not-deploy for one jurisdiction (say, EU) composes with continued deployment in others (US, UK). The trail artefacts must accommodate the per-jurisdiction disposition (foreshadow `mod-106`).
- **Sketch the M&A / re-org resilience of the do-not-deploy trail.** In `do-not-deploy-trail-resilience.md`, walk what happens to the do-not-deploy trail when the enterprise reorganises, spins off a business unit, or acquires another AI programme. The trail must survive; sketch how.
- **Author the incident-post-mortem template.** In `incident-post-mortem-template.md`, sketch the template the assurance programme uses after any disposition-firing incident — timeline, trigger, disposition chosen, disposition executed, deviations from the pre-committed pathway, lessons learned, tier-decision-artefact updates required.
- **Draft the operational runbook joint sign-off.** The disposition matrix in the tier-decision artefact and the operational runbook in `mod-103` chapter `05` must remain coherent. In `joint-sign-off-memo.md`, sketch the memo that keeps the two coherent at every release — the methodology owner and the operations lead both sign that the disposition matrix and the runbook match.
- **Extend the downgrade table with a "downgrade-locked" state.** In `downgrade-locked-state.md`, sketch how a downgrade that is *not admissible* on some axis (a sector-regulated axis where the tier cannot descend below a certain floor without withdrawal) is expressed. The design must handle the case where downgrade is not an option and do-not-deploy is the only remaining lever.
