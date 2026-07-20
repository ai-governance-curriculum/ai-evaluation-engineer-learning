# Kill-Switch, Rollback, Downgrade, and Do-Not-Deploy Pathways

## Motivation

Chapters `01`–`03` designed the positive side of the tier gate: what a tier is, what capability evidence supports it, and what mitigation obligations stack onto it. This chapter is the negative side — what happens when the tier is *exceeded* by observed capability, when the evidence *expires*, when a mitigation *fails*, or when the release simply *should not have been made*.

The release-gate runbook in `mod-103` chapter `05` gave the runtime-triggered reversal shape — rollback triggers, rollforward triggers, exception approvals. This chapter widens the frame to the *tier-boundary* reversal shape, which is the shape frontier labs pre-commit to in their responsible-scaling policies: kill-switch, rollback, downgrade, do-not-deploy. Each is a distinct disposition with distinct authorising conditions, distinct signers, and distinct trail obligations.

The methodology owner's job is to design each pathway *before* the release, name it in the tier-decision artefact (`05`), test it on a cadence, and *carry the escalation contract* with the head of AI governance (level 60) when a tier-boundary reversal is on the table. Without those pathways, the tier gate is a one-way door: the release goes out, and the enterprise carries whatever consequences ensue.

## The four dispositions

The four dispositions form a spectrum from most disruptive (immediate stop) to most subtle (permanent refusal to deploy):

- **Kill-switch.** An immediate stop to inference, at platform level, invoked when the deployment is causing (or is judged to be causing) unacceptable harm right now. The kill-switch does not restore a prior state — it *terminates* the current state.
- **Rollback.** A return to a prior *model version* or a prior *deployment-tier configuration*. Rollback restores a state the enterprise previously ran and previously certified.
- **Downgrade.** Movement of the deployment to a *lower tier* without full withdrawal — the tool set is restricted, the population is narrowed, an autonomous action is put behind a human-in-the-loop step. Downgrade preserves the deployment but shrinks its permission envelope.
- **Do-not-deploy.** The terminal decision — the release is *not* promoted, or the deployment is withdrawn permanently. The decision carries an artefact trail so that a later attempt to reverse it silently is visible.

The four are not substitutes for each other. Each is appropriate in different conditions; the tier-decision artefact (`05`) names which conditions trigger which disposition, and the escalation contract names which signer authorises each.

## Kill-switch design

**What it is.** A technical control at the platform layer — usually at the inference-serving layer or the API-gateway layer — that stops the model from being invoked at all. The kill-switch is *not* the same as a feature flag on the client side; a client-side flag can be bypassed by a client that has cached the endpoint. A kill-switch is enforced *server-side* and, ideally, at the point closest to the model.

**Design principles.**

- **One switch, one action.** The switch has one job — stop inference. Not "stop inference and email a report and file a ticket." One authorised person hits it, and inference stops.
- **Enforced at the platform layer.** Not in application code, not in a client library. The layer that owns model invocation owns the switch.
- **Tested on a cadence.** A kill-switch that has never been fired is a hypothesis. Reverse-drill it on the same cadence as rollback (mod-103 chapter `05`; typically quarterly against the production surface).
- **Auditable.** Every invocation records: who invoked, when, what tier, what trigger, what wall-clock. The audit trail lands in the immutable evidence pipeline (`mod-104`).
- **Failure-safe.** Under a control-plane outage, the switch's *default state* has to be documented. Some deployments prefer "on if unreachable" (fail-safe closed); others prefer "on if unreachable" would cause secondary harm and prefer the opposite. The choice is a design decision, defended in the artefact.

**When to design it.** The kill-switch is designed at tier-scheme authoring time (`01`), *not* at release time. Every tier admits a kill-switch appropriate to its blast-radius — a T0 pilot's kill-switch can be simple; a T-CS-style external-facing deployment's kill-switch has to handle stateful in-flight sessions gracefully. The methodology owner does not design the mechanism; the `ai-infra-mlops` and `ai-infra-security` peers do. The methodology owner *requires* it, *cites* it in the tier-decision artefact, and *reviews* its test evidence.

**When to invoke it.** Kill-switch invocation is the appropriate disposition when:

- A serious-incident trigger fires (EU AI Act Article 73 threshold, sector-rule equivalent, or an internal serious-incident definition) and continued operation would compound the harm.
- A cybersecurity-integrity trigger fires (a compromise of weights, prompts, judge configuration, or serving infrastructure — mod-103 chapter `05`).
- A regulator or authority issues a notice that the deployment must cease.
- A downstream tool-invocation is causing measurable, unacceptable side effects and rollback cannot be executed fast enough.

Kill-switch invocation is *not* the appropriate disposition when rollback or downgrade would restore an acceptable state in comparable time — the more surgical option is preferred. The trade-off is judgement, documented in the runbook.

## Rollback

**What it is.** Return to a prior model version or a prior deployment-tier configuration. Rollback is *reversible* — it puts the deployment back into a state the enterprise previously ran, previously certified with an assurance case, and previously monitored.

Two flavours matter for the tier gate:

- **Model-version rollback.** Serve the prior model version (or prior fine-tune, or prior system-prompt version) instead of the current one. The prior version's assurance case, cards, and post-market monitoring plan are re-activated.
- **Tier-configuration rollback.** Move the deployment back to the prior *tier* — the prior permission envelope, the prior mitigation set, the prior evidence set. The model may not change; only the tier does.

Rollback is the operations-primary disposition — most reversals in a mature programme are rollbacks. The runbook (mod-103 chapter `05`) already carries the trigger set, the RTO expectations, the post-rollback review procedure, and the authorising conditions. This chapter adds the *tier-boundary* nuance: a rollback that crosses a tier boundary (from T2 back to T1, from `tools:High` back to `tools:Med`) is *itself* a tier-boundary crossing, and triggers the escalation contract below.

## Downgrade

**What it is.** Movement of the deployment to a lower tier without full withdrawal. The deployment continues; its permission envelope shrinks. Common downgrade moves:

- **Tool-set restriction.** Remove writes from the tool set (agent can read the CRM but not update it); remove long-horizon planning; require human confirmation before tool invocations.
- **Population narrowing.** Move the deployment from unauthenticated external users back to authenticated users only; move from paying customers to internal beta; move from full population to opt-in subset.
- **Autonomy reduction.** Insert a human-in-the-loop step at a decision the deployment previously made autonomously; require dual-confirm for high-blast-radius actions.
- **Data-access restriction.** Narrow the data the deployment may access (from cross-tenant to per-tenant, from historical to recent, from writable to read-only).

Downgrade is the *precise* disposition — it preserves the value the deployment delivers while retracting the specific permission surface that caused the tier boundary to be exceeded. It is often the right answer when a capability-evidence spec (`02`) shows the model is measurably more capable than the previous release, but the mitigation set has not yet been updated to match: downgrade first (constrain the permission envelope), and re-uplift once the mitigation set at the higher tier is demonstrably in place.

**Design principles.**

- **Downgrade paths are pre-designed per axis.** For every axis in the tier scheme (`01`), the tier-decision artefact names the downgrade increments — "from `tools:High` to `tools:Med` means removing the write-tools and the long-horizon planner"; "from `reach:High` to `reach:Med` means requiring authentication."
- **Downgrade is tested.** Like the kill-switch and rollback, downgrade paths are exercised on a cadence — a downgrade that has never been exercised may have unexpected side effects.
- **Downgrade is not a discount.** A downgraded deployment carries the mitigation obligations of *its new tier*, not a subset of them. The methodology owner re-runs the tier gate at the lower tier before certifying the downgrade complete.

## Do-not-deploy

**What it is.** The terminal decision: the release is *not* promoted, or an already-deployed system is withdrawn permanently. Do-not-deploy is the highest-stakes decision in the tier gate, because it is *not reversible* by rollback — reversal requires a *new* release-gate exercise with fresh evidence.

**When to design it.** The do-not-deploy pathway is designed at tier-scheme authoring time. The tier-decision artefact names the conditions under which do-not-deploy is the mandatory disposition:

- A capability threshold is crossed at a level the enterprise's mitigation set does not have credible evidence for (RSP-style "we cannot deploy at this ASL because our standards are not yet published").
- A cybersecurity attestation cannot be discharged (`03`) and no compensating control is available.
- A regulator prohibits the deployment under a specific statutory ground (EU AI Act Article 5 prohibited practices; sector rule prohibitions; deployer contract prohibitions).
- A residual-risk register accumulation reaches a level the head of AI governance has pre-committed to as a non-deploy threshold.

**Trail obligations.** Do-not-deploy decisions have to *survive* — the failure mode is silent reversal, where the deployment is quietly attempted again months later by a different team, with the original decision's rationale lost. The trail includes:

- The tier-decision artefact recording the do-not-deploy disposition, its rationale, its signers, and its expiry (do-not-deploy is often *time-bounded* — the decision may be revisited when specified evidence becomes available).
- A record in the residual-risk register.
- A record in the assurance-programme's decision log (mod-112).
- A watch item in the intake process (mod-101, mod-103) so that a *new* release of the same or a substantially similar system is flagged against the prior decision.

Do-not-deploy without a trail is not a decision; it is a delay. The distinction matters because a delay can be quietly reversed; a decision-with-trail cannot.

## The escalation contract with head of AI governance

For the higher-tier dispositions — kill-switch at a T-CS-style external deployment, rollback that crosses a tier boundary, downgrade that materially changes the deployment's value proposition, or do-not-deploy — the release-assurance methodology owner does *not* sign alone. The tier-decision artefact names the *escalation contract* with the head of AI governance (level 60 in the curriculum).

**Who reviews.** The head of AI governance chairs the review; the methodology owner presents the evidence; the release-owner presents the business context; the peer specialists (as required) attend to defend evidence. For sector-regulated deployments, sector-specific signers attend (`mod-107`).

**Who signs.** For a tier-boundary crossing:

- *Kill-switch.* Pre-authorised at the operational level for measurement-based triggers up to the release-owner's tier; escalates to head of AI governance for regulatory / serious-incident triggers and for on-prem deployer sites. (Mirrors mod-103 chapter `05` runbook authorising conditions.)
- *Rollback across a tier boundary.* Methodology owner + release-owner signature at T-CS-and-below; head of AI governance signature at the highest tiers (T3+, notified-body-involved, sector-regulated).
- *Downgrade.* Methodology owner + release-owner signature; head of AI governance countersign if the downgrade materially changes the deployment's contractual commitments.
- *Do-not-deploy.* Head of AI governance signature is mandatory. The methodology owner cannot make a do-not-deploy decision unilaterally.

**Failure modes to design against.**

- **Silent tier drift.** The deployment's actual permission envelope grows past the tier's declared envelope without a tier-decision artefact update. Symptoms: new tools added to the tool set without a re-gate; new populations opened up without a re-gate; new data sources connected without a re-gate. Countermeasure: the tier-decision artefact is the *source of truth* for the permission envelope, and platform-level enforcement points (feature-flags, API-gateway rules) are configured *from* the artefact rather than by hand.
- **Tier "shopping" between products.** Two products in the same enterprise fine-tune the same base model and take advantage of *the more permissive tier* one product certified for the *other* product's use. Symptoms: cross-product citation of tier decisions without independent evidence for each product's context. Countermeasure: tier decisions are *per deployment*, not per model; the tier-decision artefact identifies the deployment system and does not transfer.
- **Deferred approvals that become de facto approvals.** A tier gate closes with a deferred criterion (mod-103 chapter `05`), the deferral expires without closure, but the deployment continues serving traffic. Symptoms: expired deferrals in the tracker; no rollback fired. Countermeasure: the deferral expiry is a pre-registered rollback trigger (`04` of this module) that fires if the expiry lapses without closure.
- **Kill-switch that no one is authorised to fire.** Authorising role is vacant, or the role's incumbent is unavailable, or the incumbent has not been trained to invoke the switch. Symptoms: the switch is written into the runbook but never tested. Countermeasure: the reverse-drill cadence includes explicit authorisation-chain testing, with a documented alternate authoriser for every primary authoriser.
- **Do-not-deploy without a trail.** A decision to not deploy is communicated verbally and never written down; six months later, a different team retries the deployment with no knowledge of the prior decision. Symptoms: no artefact in the residual-risk register; no watch item in the intake process. Countermeasure: do-not-deploy decisions have mandatory trail artefacts (see below), and the intake process is required to check the register at every candidate release.
- **Downgrade without re-gate.** The deployment is downgraded from `tools:High` to `tools:Med` operationally (the write-tools are removed from the configuration) but the tier-decision artefact is not re-authored, the assurance case is not updated, and the release-package's tier declaration continues to read `tools:High`. Symptoms: divergence between operational configuration and governance artefacts. Countermeasure: downgrade is not certified complete until the tier-decision artefact (`05`) is re-authored at the new tier and re-signed.

## Worked example — a T-CS incident and the four dispositions

Twenty-four hours after promoting the T-CS agent to `(data:Med, tools:High, reach:High, sector:none)`, post-market surveillance (`mod-110`) detects that the guardrail block-rate has fallen below its floor and that a small number of tool-call sequences produced customer-visible responses that leaked partial internal-system information. Depending on the severity of the assessment, each of the four dispositions is on the table:

- **Kill-switch.** If the leakage is judged severe (regulated data disclosed, cross-tenant leakage confirmed, or the enterprise has a contractual notification obligation triggered), the on-call invokes the T-CS kill-switch. Inference stops. Incident-response takes over. Head of AI governance is notified. The tier-decision artefact records the invocation, the trigger, and the signer.
- **Rollback.** If the leakage traces to the *current* guardrail-config change from the last release (i.e., the prior guardrail-config would have blocked), the on-call rollbacks the guardrail-config to the prior known-good state. The model version does not change; the tier does not change; the mitigation set reverts.
- **Downgrade.** If the leakage traces to the *tool-set change* — the new release added a tool whose response format the guardrail does not adequately parse — the on-call downgrades from `tools:High` to `tools:Med` by removing the new tool from the agent's tool set. The deployment continues serving customers, with the reduced tool set, until the mitigation set at `tools:High` is demonstrably improved and the tier is re-uplifted.
- **Do-not-deploy.** If the leakage traces to a *capability of the new model* that the tier mitigation set structurally cannot address (e.g., the new model has demonstrably better exfiltration capabilities than the guardrail was designed to catch), the head of AI governance issues a do-not-deploy for T-CS at the new model version. The T-CS product either continues on the prior model version indefinitely, or a new mitigation set is designed and re-gated before the new model can be tried again.

The methodology owner does not pick one disposition and defend it after the fact. The tier-decision artefact names, *ahead of time*, which trigger classes admit which dispositions and who signs each.

## Why the methodology owner does not choose the mechanism

Two boundaries worth naming, mirroring the boundaries in `03`.

**The methodology owner does not design the kill-switch mechanism.** The `ai-infra-mlops` and `ai-infra-security` peers own the mechanism — where in the stack it sits, how it enforces, what its default state is under control-plane outage, how it interacts with in-flight sessions. The methodology owner *requires* a kill-switch, *reviews* the test evidence, and *cites* the mechanism in the tier-decision artefact (`05`). Designing the mechanism is peer work.

**The methodology owner does not decide the disposition unilaterally on the day.** The tier-decision artefact names *ahead of time* which triggers admit which dispositions. On the day of an incident, the on-call executes the pre-committed pathway; if none of the pre-committed pathways fits, that itself is an incident-response escalation, not a live judgement call. The methodology owner's job is to make sure the disposition-matrix in the artefact is *complete enough* that live judgement is rarely required — and, when required, is escalated to the head of AI governance without hesitation.

## Where this shows up in the rest of the track

- `01` — the tier scheme this chapter's dispositions unwind. Every axis in the scheme has a downgrade increment defined.
- `02` — capability-evidence expiry is a rollback / downgrade / do-not-deploy trigger.
- `03` — cybersecurity-integrity failure is a kill-switch trigger; a mitigation deficiency is a downgrade trigger.
- `05` — the tier-decision artefact composes the four disposition pathways into the release-package.
- `mod-103` chapter `05` — the runtime rollback / rollforward runbook this chapter widens.
- `mod-104` — the immutable audit trail for kill-switch invocations, rollback executions, downgrade decisions, and do-not-deploy records.
- `mod-110` — the post-market surveillance signals that fire each disposition's triggers.
- `mod-112` — the operating-model interfaces that make the escalation contract with head of AI governance operable across products.

## Summary

- The tier gate has four reversal dispositions: kill-switch (immediate stop), rollback (return to prior known-good state), downgrade (constrain the permission envelope without withdrawal), do-not-deploy (terminal, trail-preserved).
- Kill-switch design: one switch, one action, platform-layer enforcement, tested on cadence, auditable, failure-safe with a defended default state. Owned by `ai-infra-mlops` and `ai-infra-security`; required and cited by the methodology owner.
- Rollback is the operations-primary reversal; a rollback that crosses a tier boundary triggers the tier-boundary escalation contract.
- Downgrade is the precise reversal — pre-designed per tier axis, tested on cadence, re-gated at the new lower tier before the downgrade is certified complete.
- Do-not-deploy is terminal, trail-preserved, and often time-bounded. Silent reversal is the primary failure mode; the trail across artefact, register, decision log, and intake watchlist is the countermeasure.
- Escalation contract: kill-switch, rollback across a tier boundary, downgrade with material contract change, and do-not-deploy escalate to the head of AI governance. Silent tier drift, tier shopping, deferred approvals as de facto approvals, and untrained authorisation chains are the failure modes to design against.
- Exercise 04 has you design each of the four pathways for a worked deployment tier, name the triggers, and specify the escalation contract per pathway.
