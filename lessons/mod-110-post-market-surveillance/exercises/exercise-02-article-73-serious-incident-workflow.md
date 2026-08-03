# exercise-02: Article 73 Serious-Incident Workflow

**Estimated effort:** 3 hours

## Objective

Author the **EU AI Act Article 73 serious-incident workflow** for one named in-scope high-risk deployment: the triage decision-tree that classifies observed facts against the four Article 3(49) disjuncts, the three concurrent wall-clocks (2-day / 10-day / 15-day outer bound), the notification-content templates that survive filing under time pressure, the parallel GDPR Article 33 coordination for personal-data breaches, the actor-and-authority map per Member State the system is on the market in, and a rehearsed worked timeline that walks from awareness through corrective action to closure.

The exercise is design and authoring, not solving. The workflow's core is *rehearsable procedure* — a runbook that a first-time responder can execute under time pressure without needing to re-derive Article 3(49)'s disjuncts or Article 73's clocks. `<!-- needs-research: … -->` markers are legitimate where a specific Member State's competent-authority contact would need to be verified.

## Prerequisites

- Chapter [`02-eu-ai-act-article-73-serious-incident-workflow.md`](../02-eu-ai-act-article-73-serious-incident-workflow.md) — Article 3(49)'s four disjuncts, Article 73's three clocks, the internal runbook shape (triage, evidence preservation, root-cause conservatism, notification drafting, corrective action, learning capture), the substantive notification-content checklist, and the worked healthcare-triage 21-day timeline.
- Chapter [`01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md`](../01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md) — the plan's section 8 (Article 73 integration) cross-reference and the trigger sources that feed into incident triage.
- Chapter [`05-incident-db-back-feed-and-non-compliance-escalation.md`](../05-incident-db-back-feed-and-non-compliance-escalation.md) — the co-signing contract that binds withdrawal to head-of-AI-governance sign-off.
- Familiarity with `mod-103` chapter `05` (rollback runbook / incident-cutover), `mod-104` chapter `01` (legal-hold on evidence artefacts), `mod-104` chapter `06` (assurance bundle whose superseded record captures the incident).
- Regulation (EU) 2024/1689 Articles 3(49), 20, 22, 26(5), 43, 55, 73, 74, and 79 in the consolidated text at [eur-lex.europa.eu/eli/reg/2024/1689/oj](https://eur-lex.europa.eu/eli/reg/2024/1689/oj).
- GDPR (Regulation (EU) 2016/679) Article 33 for the parallel 72-hour data-breach notification.

## Problem statement

Pin one in-scope Annex III high-risk deployment where at least one of Article 3(49)'s four disjuncts is *plausibly foreseeable* — a system whose failure modes could reasonably produce a serious incident under the statute. The choice must:

- **Have a plausible incident vector.** The intended purpose and the harm inventory make one of the four disjuncts (death, serious health harm, serious and irreversible critical-infrastructure disruption, infringement of Union-law fundamental-rights obligations, serious harm to property or environment) foreseeable. A system where every disjunct is implausible dilutes the exercise.
- **Be on the market in more than one Member State.** The workflow's jurisdictional dimension is real — a system on the market in three Member States can produce concurrent notifications to three authorities. Even if the exercise's incident touches only one Member State, the actor-and-authority map has to cover all of them.
- **Have a named notified body if applicable.** Where the deployment falls under Article 43's Annex VII pathway, the notified-body interface is live during a Article 73 event.

Common shapes worth considering:

- **Clinical-decision-support AI** deployed by a hospital network across three Member States, ranking patient presentations by urgency — the *health-harm* disjunct is foreseeable if the AI under-triages an acute presentation.
- **Hiring or promotion decision-support AI** deployed by a multinational employer — the *fundamental-rights infringement* disjunct is foreseeable if the AI produces a disparate-impact regression on a protected group at scale.
- **Critical-infrastructure model** (grid dispatch, water-treatment control, transportation-signal optimisation) deployed across multiple Member States by a utility or public authority — the *critical-infrastructure-disruption* disjunct is foreseeable if the model recommends a control action that cascades.
- **Content-moderation AI** deployed by a platform across the EU — the *fundamental-rights infringement* disjunct is foreseeable via speech, access, or non-discrimination angles.
- **Financial-services fraud-triage AI** deployed by a bank across the EU — the *serious harm to property* disjunct is foreseeable if the AI freezes accounts erroneously at scale.

Pin the deployment shape, the deployer(s), the Member States on the market, the notified body (if applicable), and one foreseeable incident-vector before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `incident-classification-and-clock-rules.md`

The decision-tree that maps observed facts to Article 3(49) disjuncts and to the applicable wall-clock. Sections:

- **Article 3(49) disjunct rules.** For each of the four disjuncts (death; serious harm to health; serious and irreversible disruption of critical infrastructure; infringement of Union-law fundamental-rights obligations; serious harm to property or environment — chapter `02` splits the last into two for readability), the observable signals that indicate the disjunct applies, and the evidence a first-responder collects to defend the classification. Example: for the fundamental-rights disjunct, a disparate-impact regression against a protected group observed across a sufficient sample size.
- **Wall-clock assignment rules.** Which disjunct maps to which of the three clocks (2 / 10 / 15 days). Include the concurrent-clock rule chapter `02` gives — where multiple disjuncts apply, the workflow files under the shortest applicable clock and uses the same incident identifier for the whole notification chain.
- **Awareness-timestamp discipline.** The specific procedure for recording the "awareness" timestamp that starts the clock, with the ambiguous-signal-vs-reasonable-likelihood distinction chapter `02` names. Include the *provider becomes aware* clock (from own monitoring or from a peer's report) and the *deployer becomes aware* clock (Article 26(5) obligates the deployer to inform the provider immediately) — the provider's clock starts when the provider becomes aware, but Article 73(2)'s language accepts "reasonable likelihood".
- **Reasonable-likelihood escalation rule.** Where the causal link is not yet established but *reasonable likelihood* exists (Article 73(2)'s explicit language), the clock starts and the notification is filed as *preliminary*. The procedure resists the temptation to wait for full causal certainty.
- **GDPR Article 33 parallel-trigger rule.** Where personal data is processed by the affected system, GDPR Article 33's 72-hour clock runs in parallel to the AI Act's clock. The rule fires a joint-drafting protocol with the DPO (see artefact 3).
- **Sector-parallel clock check.** Cross-reference to `mod-107` — if the deployment is sector-regulated (medical-device MDR under 21 CFR Part 803, DORA, MiFID incident-reporting), the sector-parallel clock runs independently. The workflow files each notification on its own clock and uses one shared incident identifier.

### 2. `triage-runbook.md`

The triage runbook the on-call executes from detection through classification through release-attribution to escalation. Sections:

- **Detection sources.** The signal sources chapter `02` enumerates: internal Article 72 monitoring signal (chapter `01`); deployer escalation under Article 26(5); end-user report; external incident-registry match (chapter `05`); market-surveillance-authority notice; media/public report. Each source has a page-out rule and an intake-artefact class.
- **Named on-call roles.** The incident-commander role (owned by `ai-risk-engineer` peer at level 25 per chapter `02`); the release-assurance on-call (owned by this role); the legal-counsel on-call; the DPO on-call; the regulatory-affairs on-call. Each is a single named individual with a named backup and a page-out channel.
- **Classification workflow.** Applies the decision-tree from artefact 1 to the observed facts, producing a classification against Article 3(49) with rationale and an assigned wall-clock. Where the classification is ambiguous, the runbook escalates to legal counsel before committing.
- **Release-attribution workflow.** Identifies the release candidate implicated, the specific assurance-case claim potentially defeated (`mod-102` chapter `05`), and the model/harness/eval-set digests from the assurance bundle. Cross-reference to `mod-104` chapter `06`.
- **Evidence-preservation steps.**
  - **Legal hold.** Apply a legal-hold flag to every artefact tied to the implicated release candidate (`mod-104` chapter `01`) so nothing expires while the incident is open.
  - **Trace pinning.** Pin the relevant production traces into the assurance store by digest.
  - **Reproducibility-bundle verification.** Verify the reproducibility bundle for the implicated release still resolves; if any digest has drifted, that itself is an incident.
- **Root-cause-conservatism stance.** The default is that the release *caused* the incident until evidence disproves the link. Chapter `02` defends this as consistent with Article 73(2)'s "reasonable likelihood" language.
- **Escalation rules.** For which classifications the incident commander pages the head-of-AI-governance (level 60) immediately, for which classifications the second-line effective-challenge signer (`mod-103` chapter `05`) is a required co-signer, and for which classifications routine release-owner co-sign is sufficient.

### 3. `notification-templates.md`

Three notification templates the on-call fills against pre-committed fields.

**Initial-notification template.** Covers every field from chapter `02`'s substantive checklist:

- Incident identifier — the internal identifier the workflow uses to link all downstream evidence.
- Incident date, place, and Member State(s) affected.
- Affected AI system — product identifier, release candidate, Article 49 registration reference (placeholder), notified-body identifier if applicable.
- Classification against Article 3(49) — which disjunct(s), with rationale.
- Known facts — timeline, observed harm, affected population where knowable.
- Preliminary causal hypothesis — the current best read, marked *preliminary*.
- Immediate mitigations already in place.
- Wall-clock the report is filed under — the shortest applicable, with rationale.
- Expected update cadence.
- Contact for the competent authority — a named individual (placeholder) with authority to answer questions on the record.

**Update-notification template.** Carries the same incident identifier plus: what has changed since the previous update (confirmed or revised causal hypothesis; new mitigations; investigation status); the next-update date.

**Closure-notification template.** Carries the incident identifier plus: final causal analysis; corrective actions implemented (with Article 20 references); learning-capture artefact references (`mod-102` chapter `06` harm inventory amendments, `mod-103` rubric amendments, chapter `01` plan amendments); the release-attribution decision (leave in service / downgrade / withdraw / recall).

**Per-Member-State authority routing.** For each Member State the deployment is on the market in, name the market-surveillance authority contact and channel. Mark `<!-- needs-research: verify the current Member State market-surveillance authority contact and notification channel for [Member State] under Article 70 as of 2026-07 -->` per Member State whose authority is not verified.

**GDPR Article 33 joint-drafting protocol.** Where personal data is involved, the DPO's notification under GDPR Article 33 (72-hour clock) and the assurance owner's Article 73 notification reference the same incident identifier, cite the same technical facts, and coordinate on mitigation timeline. Divergent notifications on the same event are an audit finding.

### 4. `actor-and-authority-map.md`

The actor map from chapter `02`, populated for this deployment. Sections:

- **Provider role.** The provider organisation with the named regulatory-affairs signer.
- **Authorised representative under Article 22.** If the provider is established outside the Union, the authorised representative and their reporting duty.
- **Deployer(s).** The named deployer(s) and their Article 26(5) obligation to inform the provider immediately when a serious incident is identified.
- **Market-surveillance authority per Member State.** For each Member State the system is on the market in, the designated Article 70 authority, the notification channel, the language obligations, and the escalation contact. Mark `<!-- needs-research: … -->` per Member State whose designation cannot be verified.
- **AI Office.** The AI Office contact for GPAI systemic-risk incidents (cross-reference to `mod-111`) or for cross-Member-State coordination.
- **Notified body under Article 43.** If applicable, the notified body's contact and the routing for incident communications during the Article 73 event. Cross-reference to `mod-109` chapter `02` for the notified-body interface pattern.
- **DPO.** The Data Protection Officer contact for the GDPR Article 33 joint-drafting protocol.
- **Sector-regulator contacts.** Where sector-regulated (FDA for medical devices, financial-services regulator for DORA-scoped systems), the sector-regulator contact. Cross-reference to `mod-107`.

### 5. `worked-timeline.md`

A rehearsed timeline showing the workflow end-to-end from Day 0 awareness to closure, at the granularity of chapter `02`'s worked healthcare-triage example. The timeline is *invented content* pinned to the picked deployment — but it must be internally consistent with the classification rules (artefact 1), triage runbook (artefact 2), notification templates (artefact 3), and actor map (artefact 4).

Structure:

- **Day 0 (hour by hour).** Awareness landed; incident-commander paged; triage classified against Article 3(49); wall-clock assigned; release-attribution completed; legal hold applied; initial mitigations deployed.
- **Days 1–N (day by day).** Root-cause investigation; provisional-hypothesis update; DPO parallel-drafting where personal data involved; sector-parallel-clock actions where sector-regulated.
- **Wall-clock hits.** The exact hour the initial notification is filed (relative to the applicable clock); the exact hour each update lands; the exact hour the closure notification lands.
- **Signatures and artefact digests.** Every notification carries a signer name (or role placeholder), a DSSE signature placeholder, a Rekor log-entry placeholder, and an assurance-store digest.
- **Article 20 corrective action.** The corrective-action route (bring into conformity / withdraw / disable / recall) initiated within the timeline, with the co-sign route from artefact 2.
- **Learning-capture updates.** The harm-inventory amendment (`mod-102` chapter `06`), the rubric amendment (`mod-103` chapter `02`), and the Article 72 plan amendment (chapter `01`) that the incident produces.
- **Post-incident review.** The joint review with the deployer (and, where applicable, the notified body) that closes the incident record.

The timeline is a rehearsal artefact — a first-time responder should be able to walk it and understand the ordered actions the workflow demands.

## Starter guidance

- **15 days is the outer bound, not the operating cadence.** Chapter `02` is emphatic — the operating cadence is *immediately upon causal-link establishment* per Article 73(2). A programme that treats 15 days as the target is under-rehearsed and will miss the shorter inner bounds when they apply.
- **Awareness starts the clock.** Establishing awareness is part of the workflow — an ambiguous signal is not awareness, but reasonable-likelihood *is*. Record the awareness timestamp honestly; it starts the shortest applicable clock.
- **The initial report is incremental.** Article 73(5) authorises further reports as investigation continues. The initial notification does not require full root-cause; it requires substantive content under the applicable clock and a commitment to an update cadence.
- **Three concurrent clocks — pick the shortest.** Chapter `02`'s clock-assignment rules make this explicit. An incident that combines widespread infringement (2 days) with serious harm to health (15 days) files under the 2-day clock and updates the notification chain with the same incident identifier as more facts land.
- **Parallel-regime reporting must be consistent.** Article 73 + GDPR Article 33 + sector-rule reporting (FDA MDR, DORA) run in parallel; the notifications share an incident identifier, share the underlying facts, and coordinate on mitigation. Divergent notifications on the same event are an audit finding in every regime.
- **Dissent in triage is legitimate.** Where the classification is ambiguous and different actors disagree, the record captures the dissent. Chapter `05`'s dissent-is-a-first-class-field discipline applies to triage as well as to escalation.
- **Rehearse before you rely.** A programme that has never run the workflow under time pressure has a hypothesis, not a control (chapter `02`'s framing). The worked timeline (artefact 5) is a rehearsal artefact — treat it as the reference for a tabletop exercise.
- **`<!-- needs-research: … -->` markers are legitimate.** Member State authority contacts are being populated on a rolling basis; the exact wall-clock numbering in Article 73(3) has been subject to editorial refinement. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `incident-classification-and-clock-rules.md` covers all four Article 3(49) disjuncts with observable-signal rules and evidence-collection guidance; the three concurrent clocks are assigned; the awareness-timestamp discipline is explicit; the reasonable-likelihood escalation rule is stated; the GDPR Article 33 and sector-parallel clock triggers are explicit.
- `triage-runbook.md` covers all six detection sources chapter `02` enumerates; every on-call role is a single named individual with a backup and a page-out channel; the classification, release-attribution, and evidence-preservation workflows are step-by-step; the root-cause-conservatism stance is explicitly stated; escalation rules are clear per classification.
- `notification-templates.md` has three templates (initial, update, closure); the initial template carries every field from chapter `02`'s substantive checklist; per-Member-State authority routing is present with `<!-- needs-research: … -->` markers where authorities are unverified; the GDPR Article 33 joint-drafting protocol is present.
- `actor-and-authority-map.md` covers provider, authorised representative (or explicit note that none required), deployers, Member State market-surveillance authorities (all Member States on the market), AI Office, notified body (where applicable), DPO, and sector-regulator contacts (where applicable). Every actor has a named contact or role placeholder plus channel.
- `worked-timeline.md` walks the workflow from Day 0 awareness to closure at hour-by-hour granularity for Day 0 and day-by-day granularity thereafter; every wall-clock hit is timestamped; every notification carries a signer, signature placeholder, and artefact digest; the Article 20 corrective-action route is initiated with the correct co-sign route; the learning-capture updates are all named.
- Every artefact is internally consistent with the others — the classification rules cover the disjunct(s) in the worked timeline; the runbook's roles are named in the actor map; the notification templates' contacts are named in the actor map.
- Every place a fact would need to be verified against the consolidated Regulation text, a specific Member State's authority designation, a specific notified body's contact, or the enterprise's own policy is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Coordinate with sector-rule serious-incident reporting.** In `sector-parallel-reporting.md`, add the sector-parallel notification templates (FDA MDR under 21 CFR Part 803 for medical devices; DORA ICT-incident notifications for financial services; MiFID or PSD2 reporting where applicable) with their independent clocks and the shared-incident-identifier discipline. Cross-reference `mod-107` and `mod-110` chapter `04`.
- **Multi-jurisdiction notification-coordination matrix.** In `multi-jurisdiction-matrix.md`, design the matrix for a system on the market in five Member States plus the UK plus the US — one row per jurisdiction, columns for authority, channel, clock, language obligations, escalation contact. Include the coordination protocol when two Member States' authorities open concurrent Article 79 procedures on the same incident.
- **Tabletop rehearsal script.** In `tabletop-rehearsal-script.md`, author a tabletop-exercise script the release-assurance function runs quarterly — the scenario prompt, the escalation prompts at each turn, the observer's checklist, and the after-action-review template. Cite the worked timeline (artefact 5) as the target reference.
- **Integrate with the mod-103 rollback runbook.** In `rollback-integration.md`, walk how the same signal that triggers Article 73 triage triggers the `mod-103` chapter `05` rollback runbook — the shared decision points, the shared authorisation, and the differences (rollback focuses on service continuity; Article 73 focuses on authority notification).
- **Draft the post-incident-review template.** In `post-incident-review-template.md`, structure the joint review with the deployer per ISO/IEC 42001 clause 10.2 (nonconformity and corrective action) — participants, agenda, evidence review, corrective-action verification, learning-capture disposition.
