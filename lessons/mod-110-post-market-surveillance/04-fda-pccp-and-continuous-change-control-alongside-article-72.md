# FDA PCCP and Continuous Change Control Alongside Article 72

## Motivation

For medical-device deployments, the release-assurance programme does not choose between EU AI Act Article 72 and the FDA regime — it runs both, concurrently, against the same deployed system. An AI-enabled device that is CE-marked as high-risk AI under the AI Act and is also cleared by the U.S. FDA carries two post-market monitoring obligations, two corrective-action regimes, and two authority-facing evidence trails.

The design job is *unification*. Both regimes look similar in aim (keep monitoring, act on drift, notify authorities), but they diverge in scope, in change-control philosophy, and in evidence expectations. This chapter walks the FDA **Predetermined Change Control Plan** (PCCP) — the mechanism the FDA has introduced for AI-enabled device software functions — and shows how the assurance programme integrates it with the Article 72 plan (chapter `01`) into a single monitoring runbook and a single evidence store.

The chapter is scoped to medical devices — this is where PCCP applies. The pattern (a pre-authorised change envelope, tagged observations, jurisdiction-tagged corrective actions) generalises to other sectors, and `mod-107` walks the wider sector-overlay pattern.

## PCCP in one page

**What it is.** A Predetermined Change Control Plan is a written plan, submitted by a device manufacturer as part of a marketing submission (510(k), De Novo, PMA), that describes specific modifications the manufacturer intends to make to a locked machine-learning-enabled or AI-enabled device software function post-clearance without triggering a new marketing submission. The FDA issued its finalised guidance on PCCPs in 2024 — see the [FDA guidance: Predetermined Change Control Plans for Artificial Intelligence-Enabled Device Software Functions](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions).

**What is in a PCCP.** The FDA guidance calls for three components:

- **Description of modifications** — the specific, planned changes the manufacturer intends to make to the AI/ML function within a bounded envelope. Examples: retraining on refreshed data on a stated cadence, expansion of the intended patient population within pre-specified bounds, adjustment of decision thresholds within pre-specified bounds.
- **Modification protocol** — the methodology by which each planned change is developed, validated, and implemented. Covers data-management practices, model-development and re-training procedures, verification and validation activities, model-update-procedures (including labelling updates), and cybersecurity considerations.
- **Impact assessment** — the risk-based analysis of the modifications, comparing the AI-enabled device with the changes to the version without. Assesses benefits and risks of the modifications, addresses risks of implementing them, and identifies mitigations.

<!-- needs-research: reconfirm the exact three-component naming and any 2025-2026 refinements to the FDA guidance as of 2026-07 -->

**Why it matters.** Without a PCCP, every substantive change to a cleared AI/ML function typically requires a new marketing submission — a wall-clock the pace of AI iteration cannot afford. With a PCCP, the manufacturer executes changes *within the envelope* without new submissions, and the FDA has an assurance path built on the pre-authorised plan.

## Where PCCP and Article 72 overlap

Both regimes require *ongoing performance monitoring* and both drive *corrective action* on drift. The overlaps are substantial:

- **Monitoring** — PCCP's modification protocol includes verification activities that in practice look very like Article 72's monitored characteristics. Both regimes monitor accuracy, robustness, subgroup performance, and drift.
- **Corrective action** — PCCP-cleared modifications are one class of "corrective action" the manufacturer executes on monitoring signal. Article 72 signal that indicates loss of declared accuracy triggers Article 20 corrective action; that corrective action may take the form of a modification the PCCP already authorises.
- **Evidence pipeline** — both regimes require immutable, versioned evidence tying changes to their validation records. The content-addressed evidence store (`mod-104` chapter `01`) discharges both.
- **Labelling** — PCCP anticipates labelling updates that reflect the modifications (device labelling under 21 CFR Part 801). Article 13's instructions for use and the Article 72 plan's declared levels are the AI Act counterparts.

## Where they diverge

The two are *not* substitutable. Four divergences shape the unification.

### Envelope vs. open-scope monitoring

PCCP is built around a *pre-authorised change envelope*. The manufacturer names, in advance, the modifications that will be made and the bounds within which each will be made. A modification outside the envelope requires a new marketing submission. Article 72 is broader — it monitors for *any* material change in performance, including changes that no envelope anticipated. In practice, the assurance programme's monitoring runbook covers both: within the envelope, monitoring signals feed the PCCP modification protocol; outside the envelope, monitoring signals feed the Article 20 corrective-action route which may — depending on the change class — trigger a new FDA submission alongside the AI-Act notification.

### Deployer-channel signal

Article 72 explicitly names *deployer channels* — signal from users of the system (clinicians, healthcare organisations) as a first-class input. PCCP focuses on the manufacturer's own monitoring and modification methodology; deployer-facing feedback loops are less prescriptive. The unified runbook explicitly routes deployer feedback into both regimes, tagging the observation with the applicable authority.

### Fundamental-rights signal

The AI Act's high-risk regime treats infringement of Union-law fundamental-rights obligations as a distinct signal class (chapter `02`, Article 3(49) disjunct 3). FDA's PCCP is not framed around fundamental-rights language; it is framed around clinical safety and effectiveness. A performance regression that disproportionately affects a protected subgroup is *both* a clinical-effectiveness signal (FDA route) *and* a fundamental-rights signal (AI Act route); the unified runbook must recognise both.

### Serious-incident reporting

FDA's Medical Device Reporting (MDR) under 21 CFR Part 803 imposes its own serious-incident reporting obligations to the FDA, with its own wall-clocks (typically 30 days for reportable events; 5 working days for events requiring remedial action to prevent unreasonable risk). The AI Act's Article 73 (chapter `02`) runs on 2 / 10 / 15-day windows. The unified runbook triages each incident once and files each applicable notification on its own clock. <!-- needs-research: reconfirm 21 CFR Part 803 wall-clocks and any 2025-2026 refinements as of 2026-07 -->

## The unification pattern

The assurance programme runs *one* monitoring runbook and *one* evidence store. Each observation is *tagged* with the applicable authority (or authorities). Each corrective action names the regime(s) it discharges. Each notification is filed on its own regime's wall-clock.

### One monitoring runbook, tagged

The Article 72 plan (chapter `01`, section 3) becomes the top-level monitoring specification. Each monitored characteristic is annotated with the regime(s) it discharges:

| Monitored characteristic | Metric | AI Act obligation | FDA / PCCP obligation |
| --- | --- | --- | --- |
| Per-class sensitivity on triage subgroups | 95% CI lower bound | Article 15 (accuracy) | PCCP modification protocol: performance verification |
| Distribution drift on ECG-feature inputs | KL-divergence | Article 10 / Article 15 | PCCP modification protocol: data-management |
| Subgroup performance parity | Δ across pre-specified subgroups | Article 10 / Article 9 / fundamental rights | PCCP impact assessment; 21 CFR Part 820 QSR |
| Cybersecurity supply-chain integrity | BOM digest match | Article 15 (cybersecurity) | FDA cybersecurity guidance |
| Adverse event rate | events per 10⁶ uses | Article 9 / potential Article 73 | 21 CFR Part 803 MDR |

Each row's dispositions include: (a) is this within a PCCP-authorised modification envelope? (b) does this defeat an assurance-case claim? (c) does this meet any serious-incident threshold in either regime?

### One evidence store, tagged

Every evidence artefact in the content-addressed store (`mod-104`) carries a `retention_class` and a `regulatory_scope` field. For a dual-regulated medical device, the artefact carries both `retention_class: eu-ai-act-10y` and `retention_class: fda-device-life-plus-2y`, and `regulatory_scope: ["eu-ai-act-article-72", "fda-pccp", "fda-mdr", "iso-42001", "iso-13485"]`. The store applies the *maximum* retention across scopes. The audit views are separable: an FDA inspector's walk pulls artefacts tagged with FDA scope; a market-surveillance-authority walk pulls artefacts tagged with AI-Act scope; the underlying artefacts are the same bytes.

### One corrective-action register, dual-signed

A corrective action produced by monitoring signal is recorded once, with its impact scope evaluated against both regimes. Concretely, a corrective action carries: the change proposed, the PCCP-envelope determination (in-envelope, out-of-envelope, or new-envelope-required), the Article 20 disposition (bring into conformity, withdraw, disable, recall), and the sign-off route for each regime.

### One incident triage, two clocks

A serious incident triage is single-source (chapter `02`'s procedure), but produces multiple notifications on their own wall-clocks: AI-Act Article 73 to the Member State market-surveillance authority, FDA MDR to the FDA under 21 CFR Part 803, GDPR Article 33 if personal-data breach, and internal notifications to hospital deployers under the manufacturer's clinical-safety procedures.

## Worked shape — medical-imaging triage AI cleared by FDA and placed on the EU market

An AI-enabled device software function analyses chest X-rays and triages images for the presence of urgent findings (pneumothorax, large pleural effusion). The provider is a MedTech company. The device is cleared by the FDA with a PCCP that authorises: (a) quarterly retraining on refreshed data within a specified population, (b) tightening of decision thresholds within pre-specified bounds, and (c) expansion to additional imaging-device manufacturers within a pre-specified compatibility protocol. The device is also CE-marked and placed on the EU market as a high-risk AI system (Annex III use-case: medical device).

**The unified monitoring plan.** Sections 1–4 of the Article 72 plan (chapter `01`) are authored to include the PCCP's modification-protocol verification activities. Section 3's monitored-characteristics table is annotated as above; several rows discharge both regimes. Section 6 (review cadence) is annotated with the PCCP's own quarterly retraining cycle — the retraining triggers a modification-protocol run, which produces evidence that discharges both the FDA verification and the Article 72 monitored-characteristics table.

**A signal example.** Six months after clearance, the online-eval slice shows the pneumothorax-detection sensitivity has drifted from a declared 0.94 (CI lower bound 0.92) at gate to 0.90 (CI lower bound 0.87) on production traffic. The drift is confirmed with three consecutive weekly observations at CI lower bound below 0.90.

- **Article 72 disposition.** Trigger fires; assurance case's `Article-15-accuracy` claim reopened; re-review scoped (chapter `03`).
- **PCCP disposition.** The drift meets the PCCP's pre-specified verification bound — the modification protocol authorises a retraining. Retraining executed within the modification protocol; new model version validated; verification evidence signed and lodged in the store; labelling updated per the PCCP.
- **Post-corrective-action.** The signed retraining evidence discharges both the Article 20 corrective action (bringing the AI Act declared accuracy back into conformity) and the PCCP verification obligation. One evidence artefact; two authority scopes.

**An out-of-envelope signal example.** A subsequent signal shows that the drift is not fixed by retraining — a subgroup (paediatric imaging) is systematically under-served. The proposed corrective action is to expand the intended population to explicitly exclude paediatric use, adjust the labelling, and add subgroup-specific monitoring. This modification is *not* in the PCCP envelope (the PCCP anticipated retraining, not intended-population changes) — a new FDA marketing submission is required. Concurrently, the Article 72 plan is amended to reflect the narrower intended purpose, and the Article 13 instructions for use are updated. The corrective-action register records both routes with distinct wall-clocks.

## What the assurance programme owns

The programme's role in this dual regime is *unification and disposition*, not sector-specific methodology. Concretely:

- The programme *does not author* the PCCP itself — the manufacturer's regulatory-affairs function drafts and submits the PCCP; the peer risk-engineer contributes the impact assessment; the peer AI-eval engineer contributes the modification-protocol verification activities.
- The programme *does own* the unified monitoring runbook, the corrective-action register, and the incident triage — the surface where both regimes' signals converge.
- The programme *does own* the tagging discipline in the evidence store — every artefact carries its regulatory scopes; the audit views are separable.

`mod-107` (sector-regulated assurance) covers SR 11-7, FDA GMLP, DORA, and the wider sector-overlay pattern. This chapter is the specific PCCP-Article-72 unification within that pattern.

## Anti-patterns

- **Two runbooks, two stores.** The programme runs a PCCP monitoring runbook and an Article 72 monitoring runbook side by side, with different observability infrastructures and different evidence stores. Signal that should have crossed the two regimes is siloed; corrective actions that should have discharged both discharge only one. Fix: one runbook, one store, tagged.
- **PCCP treated as a shield against Article 72.** The programme reads Article 72(3)'s equivalence clause as permission to substitute the PCCP for an Article 72 plan without argument. The equivalence has to be *demonstrated*, per obligation, and the plan (or the integrated document that plays the plan's role) has to be inspectable by a market-surveillance authority. Fix: an explicit crosswalk maps each Article 72 obligation to the PCCP section(s) that discharge it and names any gap.
- **Deployer-channel signal lost in translation.** Signal from hospital deployers reaches the manufacturer's medical-safety function but never reaches the assurance programme's monitoring runbook. Fix: the runbook explicitly ingests medical-safety-function reports on a stated cadence.
- **Retention mismatch.** The store carries only the FDA-required retention (device-life plus two years) but the AI Act requires ten years of technical-documentation retention (Article 18). Artefacts expire before the AI-Act obligation lapses. Fix: retention class is the maximum across all applicable regimes plus a margin.
- **Envelope inflation.** The manufacturer treats every new signal as within the PCCP envelope to avoid new-submission overhead. Envelope determinations become optimistic; regulators eventually catch a modification that materially expanded intended use without a submission. Fix: envelope determination is a co-signed decision with the manufacturer's regulatory-affairs function; borderline cases escalate to a formal FDA pre-submission discussion.

## The unified crosswalk as a controlled document

Where the programme runs the dual regime, the *crosswalk* — the document mapping AI Act obligations to PCCP sections and identifying gaps — is itself a controlled document under ISO/IEC 42001 clause 7.5. It carries a version, a signer, a review cadence, and a diff history. Auditors from either regime read the crosswalk to understand what the programme has committed to.

A defensible crosswalk has one row per obligation-and-regime combination, with the following columns: obligation identifier (Article 72 monitored-characteristic, PCCP modification-protocol activity, sector-rule clause), the evidence artefact class that discharges it, the owner peer track, the cadence, the applicable-authority tag, and any gap or equivalence argument. The crosswalk is stored alongside the plan in the assurance store; the assurance bundle references its digest.

## The PCCP's own change-control loop feeds Article 20

An underappreciated interaction is that a PCCP-authorised modification, executed within the envelope, is *itself* an Article 20 corrective action from the AI Act's perspective — the modification brings the system into (or maintains its) conformity with the declared Article 15 levels. The evidence produced by executing the PCCP modification protocol (validation reports, updated labelling, updated risk assessment) discharges the Article 20 evidence obligation without a separate corrective-action workflow.

This is a substantial efficiency for programmes running the dual regime well. It also imposes a discipline: the PCCP modification-protocol evidence has to *actually* reach the assurance store under the tagging that lets a market-surveillance authority walking the AI-Act view find it. A PCCP verification report that lives only in the manufacturer's regulatory-affairs filing system, unindexed by the assurance store, does not discharge the AI-Act obligation even though it discharges the FDA obligation.

## Communication with the two authorities

The programme's authority-facing communication runs in two directions:

- **Routine communications** — PCCP status updates to the FDA (typically at pre-specified intervals or on modification execution) and Article 72 plan updates lodged with the notified body (Article 43 pathway) or otherwise available on Article 74 market-surveillance request. Routine communications are scheduled, batched, and cited in the assurance store.
- **Incident communications** — chapter `02`'s Article 73 notification and the FDA MDR notification under 21 CFR Part 803 run on independent wall-clocks; the programme's incident procedure named a single triage that produces both notifications with a single incident identifier.

Where the notified body under CE-marking and the FDA both request information on the same incident, the programme's response is coordinated but jurisdiction-specific — each authority receives content shaped for its own regulatory framework, and the two responses are linked by the incident identifier and are consistent on facts. Divergent responses to different authorities on the same facts are an audit finding in both regimes.

## Where this shows up in the rest of the track

## Where this shows up in the rest of the track

## Where this shows up in the rest of the track

- `mod-101` chapter `04` — Article 72 named as the AI-Act anchor; sector-rule overlay named as adjacent obligation.
- `mod-102` chapter `06` — the risk-engineer contract row carries the PCCP impact-assessment ownership.
- `mod-104` chapter `01` — the store's `retention_class` and `regulatory_scope` fields carry the tagging.
- `mod-107` — sector overlays; PCCP is one specific case within the pattern.
- `mod-108` — a forced downgrade under one regime may exceed a PCCP-envelope bound and require a new submission under the other.
- `mod-109` — the notified-body interface (CE-marking pathway) runs alongside the FDA quality-system inspection interface.

## Summary

- FDA PCCP is a pre-authorised change envelope for AI/ML-enabled device software functions; three components — description of modifications, modification protocol, impact assessment.
- PCCP and Article 72 overlap on monitoring, corrective action, evidence pipeline, and labelling; they diverge on envelope vs. open-scope, deployer-channel breadth, fundamental-rights framing, and serious-incident wall-clocks.
- The unification pattern is one monitoring runbook tagged with applicable regimes, one evidence store tagged with regulatory scopes and maximum-across-regimes retention, one corrective-action register with dual sign-off routes, and one incident triage producing multiple notifications on independent wall-clocks.
- The assurance programme owns the unification and disposition surface; the PCCP itself is authored by regulatory-affairs with peer contributions from risk-engineer and AI-eval-engineer.
- Exercise 04 has you author the unified monitoring runbook and evidence-tagging discipline for a specific device that is both FDA-cleared under a PCCP and EU-placed as an Annex III high-risk AI system.
