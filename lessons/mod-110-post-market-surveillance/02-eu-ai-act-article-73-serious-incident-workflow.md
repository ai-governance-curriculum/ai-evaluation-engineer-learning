# EU AI Act Article 73 — The Serious-Incident Workflow

## Motivation

Chapter `01` designed the *steady-state* half of post-market surveillance — the Article 72 loop that ingests, analyses, and re-reviews. This chapter designs the *exceptional* half: what happens when a monitored signal, a deployer escalation, or a public event indicates that the deployed system has caused, or is implicated in, a **serious incident** — and how the assurance programme meets the notification obligation the Regulation places on the provider under **Article 73 — Reporting of serious incidents**.

Article 73 is where the release-assurance programme has to be *fast*. Article 72 works on weekly and monthly cadences; Article 73 works on hours and days. A programme that has never rehearsed the Article 73 procedure under time pressure has a hypothesis, not a control (`mod-103` chapter `05`). Two failure modes motivate the shape of this chapter: the *slow-notification* failure, where the notification is compliant in content but late; and the *content-thin* failure, where the notification is on time but does not carry enough substance for the market-surveillance authority to act on.

## What counts as a "serious incident"

**What Article 3(49) says.** <!-- needs-research: reconfirm the exact wording of Article 3 point 49 in the consolidated 2024/1689 text as of 2026-07 --> "Serious incident" means an incident or malfunctioning of an AI system that directly or indirectly leads to any of the following:

- the death of a person, or serious harm to a person's health;
- a serious and irreversible disruption of the management or operation of critical infrastructure;
- the infringement of obligations under Union law intended to protect fundamental rights;
- serious harm to property or the environment.

**Release-assurance implication.** The four disjuncts are *broad*. A regression in a hiring-support system that discriminates against a protected group is a fundamental-rights infringement under the third disjunct. A misconfiguration in an energy-grid optimisation model that causes cascading outages is a critical-infrastructure disruption. A hallucination in a clinical-decision-support system that leads a clinician to omit a life-saving intervention is a health-harm case. The assurance programme's triage procedure has to be pattern-literate enough to recognise each disjunct without waiting for a fatality to make the categorisation obvious.

## What Article 73 requires

**What it says (paragraph 1).** Providers of high-risk AI systems placed on the Union market shall report any serious incident to the market-surveillance authorities of the Member States where that incident occurred.

**Release-assurance implication.** The *jurisdictional* dimension is real. A system deployed across multiple Member States can produce concurrent notifications to multiple authorities. The programme's incident procedure names, per Member State, the competent authority contact, the notification channel, and the language obligations.

**What it says (paragraph 2).** The report shall be made immediately after the provider has established a causal link between the AI system and the serious incident or the reasonable likelihood of such a link, and, in any event, not later than 15 days after the provider or, where applicable, the deployer becomes aware of the serious incident.

**Release-assurance implication.** 15 days is the *outer* wall-clock. It is not the operating cadence — the operating cadence is *immediately* on causal-link establishment. The procedure has to be able to produce a substantive initial report within hours if the link is clear on triage.

**What it says (paragraph 3).** <!-- needs-research: reconfirm exact windows against current EUR-Lex text of Article 73(3) — the widely-cited windows are (a) 2 days for a widespread infringement or a serious and irreversible disruption of critical infrastructure, and (b) 10 days for death, but the 15-day outer bound and the shorter inner bounds have been subject to editorial refinement; verify against the consolidated text as of 2026-07 --> The period for reporting is shortened in certain cases:

- Not later than **2 days** after the provider or the deployer becomes aware of the serious incident in the case of a widespread infringement or a serious and irreversible disruption of critical infrastructure.
- Not later than **10 days** after the date on which the provider or, where applicable, the deployer becomes aware of the serious incident in the case of the death of a person.

**Release-assurance implication.** The workflow must run three concurrent clocks — 2-day, 10-day, 15-day — and pick the shortest that applies. Triage cannot afford to wait for full root-cause; the initial report is *incremental* (paragraph 5) and updated as investigation proceeds.

**What it says (paragraph 5).** Following the reporting of a serious incident pursuant to paragraph 1, the provider shall, without delay, perform the necessary investigations in relation to the serious incident and the AI system concerned. This shall include a risk assessment of the incident, and corrective action.

**Release-assurance implication.** Article 73 investigation feeds Article 20 corrective action (chapter `01`) which feeds an update to the Article 72 monitoring plan and, when needed, a re-opening of the release-gate decision (`mod-103` chapter `05`).

**What it says (paragraph 6).** The provider shall cooperate with the competent authorities and, where relevant, with the notified body concerned.

**Release-assurance implication.** The notified-body interface (`mod-109`) is *live* during a serious incident; the assurance programme's third-party-interface contract carries the notification, the investigation updates, and the corrective-action evidence.

## The actor map

- **Provider** — reports to the market-surveillance authority of the Member State where the incident occurred, and cooperates with the notified body (Article 43 pathway) if any.
- **Deployer** — under Article 26(5), when a deployer identifies a serious incident, they inform the provider *immediately* (and, where applicable, the importer / distributor). The deployer is not the primary reporter to the authority for high-risk AI systems, but they are the reporter for their own sector-regulated obligations that may run in parallel (medical-device MDR reporting, financial-services incident notifications, DORA under `mod-107`).
- **Provider's authorised representative** — where the provider is established outside the Union, the authorised representative under Article 22 carries the reporting duty.
- **Market-surveillance authority** — receives the report, may open a market-surveillance procedure under Article 79, communicates with peer authorities in other Member States.
- **AI Office** — for GPAI models with systemic risk, the reporting channel is different (Article 55 under `mod-111`), but the incident may still meet Article 73 for a downstream high-risk deployment.

## Interaction with GDPR Article 33 (data-breach reporting)

Many serious incidents under Article 73 will *also* be personal-data breaches under Article 33 of the General Data Protection Regulation (Regulation (EU) 2016/679). Article 33 imposes a **72-hour** notification obligation on the controller to the supervisory authority. The two regimes run in parallel — the Data Protection Officer notifies under GDPR, the assurance programme notifies under the AI Act, and the two notifications must be *consistent*.

The assurance programme's incident procedure names the DPO contact and the joint-drafting protocol so that both notifications reference the same incident identifier, the same technical facts, and the same mitigation timeline. Divergent notifications to different authorities on the same event are an audit finding.

## The internal shape of the incident-response runbook

The programme owns the *release-assurance* half of the response — the incident-response methodology depth is owned by the peer `ai-risk-engineer` (level 25). What the assurance owner authors is the *integration surface*: how the peer's incident procedure carries release-attribution, evidence preservation, and notification content.

### Triage

- **Detection.** Signal enters from the Article 72 monitoring plan (chapter `01`), from a deployer escalation under Article 26(5), from an end-user report, from an external incident-registry match (chapter `05`), or from a market-surveillance-authority notice.
- **Classification.** Triage classifies the incident against Article 3(49)'s four disjuncts and assigns the applicable wall-clock (2 / 10 / 15 days).
- **Release-attribution.** Triage identifies the release candidate implicated and the specific assurance-case claim potentially defeated (`mod-102` chapter `05`).
- **Escalation.** The incident commander is paged; the release-assurance on-call is a support role (`mod-103` chapter `05`).

### Evidence preservation

- **Legal hold.** A legal-hold flag is applied to every evidence artefact tied to the implicated release candidate (`mod-104` chapter `01`). Nothing expires while the incident is open.
- **Trace pinning.** The relevant production traces are pinned into the assurance store by digest.
- **Reproducibility bundle refresh.** The reproducibility bundle for the implicated release is verified to still resolve; if any digest has drifted (it should not, in an immutable store), that itself is an incident.

### Root-cause conservatism

The default working assumption is that the release *caused* the incident until evidence disproves the link. This is the same conservatism the runbook applies to rollback triggers (`mod-103` chapter `05`). It is defensible because it aligns with the "reasonable likelihood" language in Article 73(2) — the reporting obligation triggers on likelihood, not on confirmed causation.

### Notification drafting

The initial notification carries: incident identifier, incident date and place, affected AI system (product, release candidate, Article 49 registration reference), the classification against Article 3(49), the known facts, the preliminary causal hypothesis, the immediate mitigations already in place, the wall-clock the report is filed under, and the expected update cadence.

The notification is signed by an authorised signer (the release-owner or a designated regulatory-affairs signer) and lodged with the competent authority through the authority's designated channel. A copy lands in the assurance store as a signed artefact under retention.

### Corrective action (Article 20)

The corrective action decides among: (a) leave-in-service with elevated monitoring, (b) forced downgrade of deployment tier (`mod-108`), (c) rollback to the previous release candidate, (d) withdraw the system, (e) recall the system. The decision is co-signed by the release-owner and the second-line effective-challenge signer (`mod-103` chapter `05`).

### Learning capture

Every serious incident produces a post-incident review whose output is a corrective-action record under ISO/IEC 42001 clause 10.2 (nonconformity and corrective action). The review updates the harm inventory (owner: `ai-risk-engineer`), the release-gate rubric (`mod-103` chapter `02`), and the Article 72 monitoring plan (chapter `01`).

## The three concurrent clocks in more detail

Wall-clocks in Article 73 are counted from *awareness* — the moment the provider or the deployer becomes aware of the incident. Establishing "awareness" is itself part of the workflow: an ambiguous signal is not awareness, but *reasonable-likelihood* is. The programme's triage procedure has to be honest about when awareness landed and record it as a timestamp, because that timestamp starts the shortest applicable clock.

- **The 2-day clock** applies to (a) widespread infringement of Union-law obligations, and (b) serious and irreversible disruption of critical infrastructure. Both are the "systemic" end of the disjuncts — an incident that affects many people at once, or an incident that takes down infrastructure society depends on. Widespread-infringement triage typically requires legal-counsel input to establish; the programme's incident-response runbook names the counsel-on-call.
- **The 10-day clock** applies to death. The runbook has to be able to file substantive initial content within 10 days even where root-cause is still under investigation; the notification is *incremental* (Article 73(5) authorises further reports as investigation continues).
- **The 15-day outer bound** applies to all other serious incidents.

Concurrent applicability is possible — an incident may combine widespread infringement (2 days) with serious harm to health (15 days). The programme files under the shortest applicable clock and updates with the same identifier as more facts land.

## Notification content — the substantive checklist

The initial notification, at minimum, carries:

- Incident identifier — the internal identifier the programme uses to link all downstream evidence to this incident.
- Incident date, place, and Member State(s) affected.
- Affected AI system — product identifier, release candidate, Article 49 registration reference, notified-body identifier if applicable.
- Classification against Article 3(49) — which disjunct(s), with rationale.
- Known facts — timeline of the event, observed harm, affected population where knowable.
- Preliminary causal hypothesis — the programme's current best read of the causal chain, marked as *preliminary*.
- Immediate mitigations already in place — what the programme has already done to prevent recurrence pending investigation.
- Wall-clock the report is filed under — the shortest applicable, with rationale for the choice.
- Expected update cadence — when the next update will land.
- Contact for the competent authority — a named individual with authority to answer questions on the record.

Updates carry the same incident identifier and either confirm or revise the causal hypothesis, name new mitigations, and record the closure state.

## Where this shows up in the rest of the track

## Worked timeline — a healthcare triage AI system

A hospital network deploys a triage-support AI that ranks emergency-department presentations by urgency. The system is Annex III high-risk. The provider is a MedTech company; the deployer is the hospital network.

- **Day 0, 08:15.** A patient triaged as "low urgency" by the AI-assisted queue is later re-evaluated by a physician as suffering an acute cardiac event; the patient survives after a 3-hour delay in cardiology consultation. The hospital's clinical safety team is notified.
- **Day 0, 11:30.** The hospital's safety team escalates internally and notifies the AI provider under Article 26(5). This starts the *deployer becomes aware* clock.
- **Day 0, 13:00.** The provider's release-assurance on-call is paged. Triage begins. Classification: "serious harm to health" (Article 3(49) disjunct 1) — 15-day outer bound; the case does not meet the "death" 10-day inner bound (patient survived) nor the "critical-infrastructure disruption" 2-day bound.
- **Day 0, 14:30.** Release-attribution completed: the current production release is `rc-2026-07-03`; the assurance-case claim potentially defeated is `Article-15-accuracy` on the "high-acuity cardiac-presentation" subgroup. Legal hold applied to the release's assurance bundle.
- **Day 0, 15:00.** The runbook decision: leave-in-service with elevated monitoring + forced-downgrade of the cardiac-presentation subgroup (all cardiac-symptom presentations bypass the AI ranking and route directly to physician review). Downgrade deployed by 15:45 (`mod-108`).
- **Day 1.** Root-cause investigation. Preliminary hypothesis: the production distribution of ECG-relevant features shifted after a hospital-network EHR upgrade three weeks earlier; the Article 72 plan's drift monitor should have caught it but the KL-divergence threshold was set too loose. The finding is *provisional*.
- **Day 2, 10:00.** Initial notification to the competent authority in the Member State where the incident occurred. Content: incident identifier, date and place, product identifiers, Article 3(49) classification, provisional causal hypothesis, mitigations already in place (subgroup downgrade), planned investigation steps, update cadence (every 5 business days).
- **Day 2, 12:00.** GDPR Article 33 notification lodged in parallel by the DPO — the incident involved processing of health data and meets the "risk to rights and freedoms" threshold. The notifications reference the same incident identifier.
- **Days 3–9.** Investigation. The provisional hypothesis is confirmed: the drift monitor's threshold was too loose. Corrective action drafted.
- **Day 10.** Update to the competent authority: causal link confirmed, corrective action agreed. Corrective action per Article 20 is to (a) retrain with the shifted distribution, (b) tighten the Article 72 drift monitor threshold, (c) add an ECG-feature-specific subgroup metric to the monitoring plan, (d) require a signed re-review of the assurance-case `Article-15-accuracy` claim before the subgroup is re-routed through the AI.
- **Day 14.** Final update to the competent authority: retraining complete, re-review signed, corrective action implemented. Post-incident review scheduled with the deployer.
- **Day 21.** Post-incident review at the hospital, joint with the deployer. Learning capture: the Article 72 plan is amended to include EHR-upgrade-triggered drift re-baselining; the release-gate rubric adds a cardiac-subgroup accuracy criterion at T2 and above. Both changes land in the assurance store as new versioned artefacts.

The whole workflow — from awareness to closed corrective action — is 21 days, well inside the 15-day outer notification bound but *only* because the runbook was rehearsed and the wall-clocks were pre-committed.

## Where this shows up in the rest of the track

- `mod-101` chapter `04` — Article 73 named in the article set that shapes the release-gate.
- `mod-102` chapter `05` — the assurance case's defeaters shape the triage's release-attribution.
- `mod-103` chapter `05` — the runbook's incident-cutover and rollback triggers are the mechanism the workflow drives.
- `mod-104` chapter `06` — the signed assurance bundle is the reference against which the incident is investigated; legal-hold operates on its digests.
- `mod-107` — sector-parallel reporting regimes (FDA MDR, DORA, MiFID II) run alongside Article 73.
- `mod-109` — the notified-body interface is live during an Article 73 event.
- `mod-111` — GPAI systemic-risk incidents reported to the AI Office run in parallel or in lieu of Article 73 depending on the deployment.

## Summary

- Article 73 requires providers of high-risk AI systems to report serious incidents to the Member State market-surveillance authority, on wall-clocks that range from 2 days (widespread infringement / critical-infrastructure disruption) through 10 days (death) to a 15-day outer bound.
- "Serious incident" (Article 3(49)) covers death, serious harm to health, serious and irreversible critical-infrastructure disruption, infringement of Union-law fundamental-rights obligations, and serious harm to property or environment.
- The assurance programme's incident-response runbook integrates the peer `ai-risk-engineer`'s incident methodology with release-attribution, evidence preservation, notification drafting, and Article 20 corrective action.
- GDPR Article 33's 72-hour data-breach notification runs in parallel where personal data is involved; joint drafting keeps the two notifications consistent.
- A rehearsed procedure with pre-committed wall-clocks turns the outer 15-day bound into headroom rather than a target.
- Exercise 02 has you write the Article 73 serious-incident workflow for a named in-scope high-risk system, with triage rules, notification templates, and a worked timeline against pre-committed wall-clocks.
