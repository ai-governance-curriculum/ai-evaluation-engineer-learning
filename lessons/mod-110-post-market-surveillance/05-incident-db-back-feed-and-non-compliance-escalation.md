# Incident-Database Back-Feed and Non-Compliance Escalation

## Motivation

Chapter `03` wired *internal* peer signal into the re-review cycle. This chapter wires *external* signal — the public record of AI incidents the wider ecosystem has already surfaced — into the same cycle, and then walks the non-compliance escalation path when signal (internal or external) indicates that a deployed system has drifted out of the release-gate's premise.

Two closely related failure modes motivate the chapter. The first is *external-signal blindness*: an incident lands in the public record involving a capability, deployment context, or supply-chain component the programme's inventory covers, and the programme does not notice. Six months later a regulator asks whether the programme considered the incident; the answer is no, not because the incident was irrelevant but because the programme had no ingest for the registry. The second is *unilateral reversal*: a signal (internal or external) drives the release-assurance owner to reverse a release decision, alone, without the co-sign of the head of AI governance — the second-line-of-defence pattern breaks; the reversal is not defensible; internal audit escalates.

The chapter fixes both. First half: back-feeding public incident evidence into the trigger register. Second half: the escalation contract with the `head-of-ai-governance` (level 60) that governs how a release-gate decision is reversed.

## The external incident registries

Three registries are the reference set for release-assurance programmes as of 2026:

- **AI Incident Database (AIID)** — the Responsible AI Collaborative's registry of AI incidents. Each incident carries reports, taxonomy tags, and severity assessments. Data are queryable via the site and via API. See [incidentdatabase.ai](https://incidentdatabase.ai/). AIID is the longest-running open registry and the most cited.
- **OECD.AI Incidents Monitor (AIM)** — the OECD's monitor of AI incidents and hazards drawn from global news sources, updated on a rolling basis. Aligns with the OECD Framework for the Classification of AI Systems. See [oecd.ai/en/incidents](https://oecd.ai/en/incidents).
- **MIT AI Risk Repository** — a categorised database of AI risks drawn from a systematic review of the literature. Less incident-report-shaped than AIID and AIM; more risk-taxonomy-shaped. See [airisk.mit.edu](https://airisk.mit.edu/). Useful for cross-referencing an internal harm inventory against a well-curated public taxonomy.

Other registries and initiatives exist and continue to emerge (national AI-safety-institute incident databases, the OECD AI Policy Observatory's periodic reports, sectoral registries in aviation and health). <!-- needs-research: check whether new national or sectoral incident registries have launched by 2026-07 that a release-assurance programme should ingest --> The pattern below generalises to any well-formed registry.

## The "match a public incident to your inventory" procedure

The peer `ai-risk-engineer` owns depth in incident-response methodology. What the assurance programme owns is the *matching discipline* that turns a public incident into a re-review trigger against a specific claim in a specific assurance case.

### Ingest cadence

- **Weekly scan** — the programme scans AIID and AIM for new incidents since the previous scan. Scan artefacts (the query, the returned incident IDs, the scan timestamp) are content-addressed and lodged in the store as evidence that the scan happened.
- **Event-triggered scan** — on any internal signal that a specific incident class may apply (a deployer escalation matching a known pattern), an ad-hoc scan is executed against the registries.
- **Annual comprehensive review** — the MIT AI Risk Repository is walked in full annually to cross-check the harm inventory against the taxonomy.

### Matching axes

For each candidate incident, the programme evaluates a *match score* against the inventory along three axes:

- **Capability match** — does the incident involve a capability class (image classification, text generation, decision recommendation, autonomous action) present in the inventory?
- **Deployment-context match** — does the incident involve a deployment context (healthcare triage, hiring support, credit decisioning, content moderation) present in the inventory?
- **Evidence-gap match** — does the incident implicate a failure mode the assurance case does *not* have a discharging evidence artefact for? (This is the most valuable match — the incident points at a specific gap.)

A match on any axis is *worth reading*; a match on all three is *usually* a re-review trigger. The match score, the reviewer, and the decision are recorded per incident.

### Disposition

For each incident that clears the match threshold, one of four dispositions is signed:

- **No action** — the incident is not applicable (different capability, different deployment context, different threat model). Recorded with rationale.
- **Read-only awareness** — the incident is applicable in principle but the programme's current evidence already discharges the risk. Recorded, filed under the applicable assurance-case claim as adjacent context.
- **Re-review trigger** — the incident indicates an evidence gap or an evidence staleness. A trigger fires against the specific claim; chapter `03`'s five-step re-review procedure runs.
- **Escalation** — the incident is severe enough that the programme's read is insufficient; the case is escalated to the head of AI governance and to the peer risk-engineer for deeper analysis.

## The outcome states of a re-review

Chapter `03` named three outcome states of a re-review: *reaffirm*, *downgrade*, *defeat*. This chapter adds the fifth outcome — *withdrawal* — and gives all five as the disposition vocabulary the programme uses for external and internal signal alike.

### Reaffirm

The refreshed or challenged evidence still discharges the claim at the declared threshold. The release-gate decision stands. The re-review is a signed artefact in the store; the assurance case's evidence pointer is updated to point at the refreshed artefact (the claim now discharges against a fresher artefact of the same class).

### Forced retest

The evidence pointer is *stale* (methodology has moved on, the peer track has released a newer version of its harness, an intervening framework update has changed the discharging shape). The claim is not defeated, but the current evidence is insufficient to reaffirm. A forced retest is signed with a wall-clock (retest within N days — N is pre-registered per criterion class). If the retest does not land by the wall-clock, the disposition escalates automatically to downgrade.

### Forced downgrade

The evidence does not discharge the claim at the declared level, but does discharge at a lower level. The deployment tier drops per `mod-108` — a T2 deployment reverts to T1, a T1 deployment reverts to T0 or to human-only-supervision, and so on. The downgrade holds until fresh evidence supports the higher tier again. Downgrade is co-signed by release-owner and second-line signer (`mod-103` chapter `05`).

### Do-not-deploy / withdrawal

The evidence defeats the claim outright, or the incident is severe enough (Article 3(49) serious-incident territory — chapter `02`) that the deployment cannot continue while investigation proceeds. The release-gate decision is *reversed*: the deployment stops. Article 20 corrective action begins. The withdrawal is co-signed by release-owner, second-line signer, and head of AI governance (see the escalation contract below).

### Standing-review update only

Sometimes the incident does not defeat a claim but *does* change the risk framing — a new harm is now known, and the assurance case should carry it explicitly. The disposition adds a new claim (or amends an existing claim's scope) without changing the disposition of the current release-gate decision. This is the most common disposition for external-registry matches.

## The non-compliance escalation contract

The assurance owner does *not* unilaterally reverse a release-gate decision. This is the second-line-of-defence pattern (`mod-103` chapter `05`) applied to reversal. The reversal is a *co-signed* decision with a documented rationale and a documented dissent process.

### Who signs

- **Release-owner** — the first-line owner of the deployment. Signs the disposition (or dissents on the record).
- **Second-line effective-challenge signer** — the release-assurance function's independent challenger. Signs the disposition (or dissents on the record).
- **Head of AI governance** (level 60) — for withdrawal and for forced-downgrade at T3 and above, the head of AI governance is a required co-signer.

For lower dispositions (reaffirm, forced retest, standing-review update), the release-owner and second-line signer are sufficient; the head of AI governance is briefed on a cadence but not required per disposition.

### What is recorded

The escalation record carries: the trigger (the internal peer signal or the external incident reference), the affected claim(s), the evidence walked in the re-review, the disposition proposed, the rationales of each signer, and any dissent. Dissent is *documented*, not suppressed — the release-owner may sign under protest, the second-line signer may sign under protest, and the head of AI governance may impose a disposition over one or both objections. The dissent record is part of the audit trail; internal audit reads dissent as a signal about programme health.

### Wall-clocks on escalation

Escalation is *fast*. Standing dispositions (reaffirm, standing-review update) land within one business week. Forced retest and forced downgrade land within two business days. Withdrawal, where a serious-incident wall-clock is also running (chapter `02`), lands inside the tightest applicable notification window — typically within 48 hours of the triggering signal.

### Interface to Article 20 corrective action

Every forced-downgrade and withdrawal decision drives an Article 20 corrective action (EU AI Act — bring into conformity, withdraw, disable, recall). The corrective action is co-signed as above, notified to the market-surveillance authority as required, and recorded in the assurance store as a signed, superseding artefact against the assurance bundle of the release under investigation (`mod-104` chapter `06`).

## Depth is owned by `ai-risk-engineer`

A recurring reminder: the assurance owner *integrates* rather than *authors* the incident-response methodology. The `ai-risk-engineer` peer (level 25) owns:

- The taxonomy of failure modes and the harm inventory.
- The red-team engagement design and adversarial-eval methodology.
- The incident-response triage methodology (severity scales, blast-radius estimation, root-cause analysis).
- The methodology for turning an incident into a signed learning-capture record that lands in the store.

The assurance owner consumes those artefacts and turns them into re-review triggers, dispositions, and escalation records. Where the assurance owner needs deeper analysis than they can perform themselves, the escalation contract routes the question back to the peer.

## Worked shape — public incident matched, escalation walked

A financial-services deployer of a customer-service assistant (chapter `01`'s worked example) runs the weekly external-registry scan. The scan surfaces an AIID incident describing a customer-service chatbot at another company that produced *unauthorised financial advice* to a customer, on the basis of an out-of-scope query that bypassed the assistant's refusal policy. The other company's assistant was built on a different foundation model but used a similar retrieval-augmented pattern.

- **Match assessment.** Capability match (text generation + retrieval-augmented), deployment-context match (customer service in financial services), evidence-gap match (the assurance case's `Article-9-misuse` claim discharges against a red-team engagement report from six months ago; the specific query pattern in the incident was not in the threat model).
- **Disposition — re-review trigger.** Signed as a re-review of the `Article-9-misuse` claim. Scope: the misuse-resistance evidence only.
- **Evidence walked.** The peer `ai-risk-engineer` executes a targeted red-team run against the specific pattern class. The refresh takes three business days. Finding: the assistant's refusal policy does refuse the direct query pattern but partially responds to a paraphrased variant.
- **Outcome.** Forced downgrade proposed: unauthorised-financial-advice-adjacent intents are removed from the assistant's answerable set until the refusal policy is hardened; the assistant continues to serve other intents.
- **Escalation.** Because the deployment is T2 and the finding is a fresh-adversarial-severity S2 (below S1 but above the reporting floor), the release-owner and the second-line signer co-sign. The head of AI governance is briefed but does not co-sign the disposition itself (this is not a T3 deployment and not a withdrawal).
- **Corrective action.** Article 20 corrective action is initiated: the refusal policy is hardened; new red-team engagements are commissioned against the paraphrase pattern class; the Article 72 plan is amended to add a paraphrase-adversarial monitor.
- **Record.** The whole flow is signed and lodged: the scan, the match assessment, the disposition, the re-review record, the peer refresh report, the downgrade signature, the corrective action, and the plan amendment. Six months later, an auditor asking whether the programme considered the AIID incident sees the trail end to end.

If the incident had been more severe — for example, a similar pattern had produced actual customer financial loss at scale, meeting the Article 3(49) "serious harm to property" threshold — the disposition would have escalated to withdrawal with head-of-AI-governance co-sign, and the Article 73 notification workflow (chapter `02`) would have run in parallel.

## Anti-patterns

- **No registry ingest.** The programme has no scheduled scan against AIID, AIM, or the MIT AI Risk Repository. External incidents in the programme's own capability and deployment space are surfaced only when they reach mainstream news, which is late.
- **Match-without-record.** The scan happens but no artefact records that it happened. Six months later there is no audit trail. Fix: every scan, every match assessment, every disposition is a signed artefact.
- **Unilateral reversal.** The assurance owner reverses a release decision alone. The second-line-of-defence pattern breaks; audit escalates. Fix: co-signing contract is non-optional.
- **Silent dissent.** A signer disagrees with a disposition but signs anyway with no documented objection. The audit trail loses the dispute; the programme cannot learn from it. Fix: dissent is a first-class field in the escalation record.
- **Escalation-as-signal-loss.** A disposition is escalated to the head of AI governance and never returns; the release-owner never learns what was decided. Fix: escalation returns a signed disposition to the release-owner within the wall-clock.

## Building the match discipline into a review cadence

External-registry ingest is a *discipline*, not a one-off exercise. A defensible programme runs three cadences against the registries:

- **Weekly scan** — the assurance on-call runs a scripted query against AIID and AIM new-incidents-since-last-scan. Scans that return no matches are still recorded as signed artefacts — the null result is evidence that the scan happened.
- **Monthly triage review** — every match assessment produced by the weekly scan is reviewed in a monthly session with the peer `ai-risk-engineer`. Borderline matches are surfaced for a second opinion; escalations are queued.
- **Annual taxonomy walk** — the MIT AI Risk Repository (or the equivalent well-curated taxonomy) is walked end to end against the harm inventory. Every taxonomy entry that is not covered by the inventory is a discussion point; the walk's output is an amended harm inventory and, where applicable, amended monitoring characteristics in the Article 72 plan.

The three cadences produce a *steady state* in which external-registry evidence flows into the programme at a rate the programme can absorb. The alternative — episodic scans triggered by news cycles — is unpredictable and leaves gaps.

## The escalation record schema

An escalation record is a signed artefact in the assurance store with the following fields:

- Trigger reference — the peer artefact or external-incident reference that initiated the re-review.
- Affected release-candidate — the assurance bundle identifier.
- Affected claim(s) — the assurance-case claim(s) the trigger defeats or challenges.
- Evidence walked — the artefact digests reviewed in the re-review, with reviewer and review-date per artefact.
- Disposition proposed — one of the five outcome states (reaffirm, forced retest, forced downgrade, withdrawal, standing-review update).
- Rationale — the argument for the disposition, referencing evidence, defeaters, and any framework citation.
- Signers — release-owner, second-line effective-challenge signer, head of AI governance where required.
- Dissent — any signer's documented objection, with rationale.
- Wall-clock — the wall-clock the disposition landed on, and the wall-clock the corrective action (Article 20, or sector-rule counterpart) is scheduled to complete on.
- Supersession pointer — a link to the superseded assurance-bundle reference the disposition amends.

Every escalation record is DSSE-signed by every signer, Rekor-logged, and lodged in the store under the same retention class as the underlying assurance bundle (`mod-104` chapter `06`). The audit walks the record end-to-end without trusting any signer — signatures verify against Fulcio-issued certs; log inclusion verifies against Rekor.

## Where this shows up in the rest of the track

## Where this shows up in the rest of the track

- `mod-102` chapter `05` — external-registry incidents are one class of defeater the case has to be able to absorb.
- `mod-103` chapter `05` — the runbook's rollback-authorisation and second-line effective-challenge convention shape the escalation contract.
- `mod-104` chapter `01` / `06` — scans, match assessments, dispositions, and escalation records all land as signed artefacts in the store; supersession discipline is applied to reversed release-gate decisions.
- `mod-108` — forced downgrade lands on the tier architecture.
- `mod-111` — for GPAI systemic-risk deployments, the incident-registry set and the escalation contract extend to the AI Office notification channel.
- `mod-112` — running the escalation contract across a portfolio is a top-management review input under ISO/IEC 42001 clause 9.3.

## Summary

- Three external registries anchor the programme's back-feed of public evidence: the AI Incident Database, OECD.AI Incidents Monitor, and MIT AI Risk Repository.
- The matching discipline evaluates each candidate incident along capability, deployment-context, and evidence-gap axes; a well-formed match becomes a re-review trigger against a specific claim.
- Five re-review outcome states cover the disposition space: reaffirm, forced retest, forced downgrade, withdrawal, and standing-review update.
- The non-compliance escalation contract binds the assurance owner to co-signing with the release-owner and the second-line signer; withdrawals and T3+ downgrades require the head-of-AI-governance co-sign.
- Dissent is documented, not suppressed; every disposition and every objection lands in the audit trail.
- Depth in incident-response methodology is owned by `ai-risk-engineer` (level 25); the assurance owner integrates and dispositions rather than authors.
- Exercise 05 has you author the external-registry ingest procedure, a match assessment for a named public incident against a named in-scope system, and a walked escalation to a co-signed disposition with a documented dissent process.
