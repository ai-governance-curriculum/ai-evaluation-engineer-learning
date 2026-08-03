# exercise-01: Article 72 Post-Market Monitoring Plan

**Estimated effort:** 3 hours

## Objective

Author the complete **EU AI Act Article 72 post-market monitoring plan** for one in-scope Annex III high-risk AI system, matching the nine-section structure chapter `01` defines (system identification, monitoring objectives, monitored characteristics, data-collection methods, analysis methodology, review cadence and triggers, Article 20 integration, Article 73 integration, change control on the plan). Produce the plan as five artefacts that together satisfy the Article's "actively and systematically" language and that ship inside the Annex IV technical documentation at gate time.

The exercise is design and authoring, not solving. Placeholder pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the current Regulation text, the Commission's implementing act (once published), or the enterprise's own policy.

## Prerequisites

- Chapter [`01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md`](../01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md) — the nine-section plan, the proportionality argument, the three deployer-channel shapes.
- Chapter [`03-peer-eval-and-risk-signal-into-the-re-review-cycle.md`](../03-peer-eval-and-risk-signal-into-the-re-review-cycle.md) — the five-part trigger design that populates the plan's section 6.
- Familiarity with `mod-102` chapter `06` (harm inventory as the source of monitored characteristics) and `mod-104` chapter `06` (assurance bundle where the plan is manifest-referenced under `post_market_handoff_digest`).
- Familiarity with `mod-108` (deployment-tier framework — the tier the plan's proportionality argument scales against).
- Skim access to Regulation (EU) 2024/1689 Articles 9, 10, 11, 12, 13, 14, 15, 20, 26, and 72 in the consolidated text at [eur-lex.europa.eu/eli/reg/2024/1689/oj](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), plus Annex III and Annex IV.

## Problem statement

Pin one in-scope Annex III high-risk deployment. The choice must:

- **Fall inside Annex III.** The deployment maps to one of Annex III's eight use-case categories (biometrics; critical infrastructure; education and vocational training; employment, workers management and access to self-employment; access to and enjoyment of essential private services and essential public services; law enforcement; migration, asylum and border-control; administration of justice and democratic processes).
- **Have declared Article 15 levels.** The release-gate at time `T` discharged accuracy, robustness, and cybersecurity thresholds — the plan verifies those declarations remain true.
- **Have named deployers.** A concrete deployer set (a specific hospital network, a specific bank, a specific municipal government) grounds the deployer-channel design.

Common shapes worth considering (pick one, or invent your own):

- **Healthcare triage or clinical-decision-support AI** deployed by a hospital network to rank emergency-department presentations or to flag high-risk clinical presentations — Annex III point 5(a) (access to and enjoyment of essential public services) or point 6 (law enforcement) depending on the specific use.
- **Hiring or promotion decision-support AI** deployed by an employer or employment agency to score resumes, rank candidates, or recommend promotions — Annex III point 4 (employment, workers management, and access to self-employment).
- **Credit or insurance decisioning AI** deployed by a financial institution to score creditworthiness or to trigger fraud-review workflows — Annex III point 5(b) (essential private services — creditworthiness assessment).
- **Public-services eligibility AI** deployed by a government agency to score benefit eligibility, screen social-services referrals, or triage administrative-appeal queues — Annex III point 5(a).
- **Educational-outcomes AI** deployed by an educational institution to score assessments or to allocate learning resources — Annex III point 3.

Pin the deployment shape, the Annex III use-case classification, the declared Article 15 levels (accuracy metric + threshold; robustness metric + threshold; cybersecurity assurance basis), and the deployment-tier landing (from `mod-108`) before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `system-identification-brief.md`

A two-page brief that pins section 1 of the plan (System identification) plus the parts of section 2 (Monitoring objectives) that follow from identification:

- **Provider identity and Article 49 registration reference.** The provider organisation (single legal entity), the authorised-representative reference under Article 22 if the provider is established outside the Union, and the Article 49 EU-database entry identifier for the registered high-risk AI system (placeholder — mark `<!-- needs-research: verify the current Article 49 registration workflow and the identifier format the EU database issues -->`).
- **Product and release-candidate identifiers.** The `system_under_release` identifier from the assurance bundle, the current release candidate (e.g., `rc-2026-05-07`), and the pinned model digest the release candidate resolves to.
- **Intended purpose statement.** The Article 13 instructions-for-use statement, verbatim (or with pinned placeholder). This is the boundary Article 72 monitors against — a deployer using the system outside the intended purpose is itself a monitored signal.
- **Annex III classification and Article 6 high-risk determination.** The specific Annex III point (with sub-point where applicable) and the Article 6 determination that produced the high-risk classification. Where the classification is contested or borderline, cite the reasoning.
- **Notified body.** If the deployment falls under Article 43's Annex VII pathway, the notified body's name and Article 43 identification number (placeholder). If the deployment falls under Article 43's Annex VI internal-control pathway, note that explicitly.
- **Declared Article 15 levels.** Accuracy metric and threshold (with statistical basis — CI lower bound, subgroup breakdown, etc.); robustness metric and threshold (adversarial-attack-success rate, distribution-shift tolerance, etc.); cybersecurity assurance basis (BOM digest pinning, SLSA level, supply-chain integrity attestation).
- **Deployment-tier landing.** The tier from the enterprise's `mod-108` scheme (T1 / T2 / T3, or the enterprise's own naming) with the axis-by-axis rationale. The tier is the axis the plan's proportionality argument scales against.
- **Monitoring objectives.** Continuous compliance with Chapter III Section 2 (Articles 9-15); drift detection classes (input, output, harm-signal, fairness); detection of previously unforeseen risks; verification of the Article 9 risk-management system loop; feed of learnings into the next release cycle (`mod-103` chapter `01`).

### 2. `monitored-characteristics-table.md`

The section-3 table from chapter `01`, populated for this system. At least eight rows. Columns:

- **Obligation** — the specific Chapter III Section 2 Article (Article 9 risk management, Article 10 data governance, Article 12 record-keeping, Article 13 transparency, Article 14 human oversight, Article 15 accuracy / robustness / cybersecurity).
- **Monitored characteristic** — the concrete characteristic being observed (per-class accuracy on a named slice, retrieval-relevance drift on named features, override rate by human overseer, complaint rate against transparency, etc.).
- **Metric** — the specific measurable quantity (95% bootstrap CI lower bound of F1, KL-divergence against a release-time baseline, override deviations per session, complaints per 10⁶ interactions).
- **Threshold** — the pre-registered value the metric must respect. Where a threshold cannot be pinned without further work, use `<!-- needs-research: … -->` rather than a placeholder number.
- **Cadence** — how often the characteristic is measured (continuous, weekly, monthly, quarterly, per-deployment).
- **Source peer** — which peer track owns the methodology (`ai-eval-engineer` at level 30 for online-eval and trace signal, `ai-risk-engineer` at level 25 for adversarial and guardrail refresh, `ai-infra-mlops` for supply-chain integrity).
- **Store landing** — where the evidence artefact lands in the content-addressed store (per `mod-104` chapter `02`); the artefact-class name.

Include at least one Article 15 accuracy row that ties directly to the declared level from artefact 1 (the Article 72 monitor is what verifies the Article 15 declaration remains true — see chapter `01`'s section on how Article 72 binds to Article 15). Include at least one row for each of Articles 9, 10, 13, 14, and 15.

### 3. `data-collection-and-analysis-methods.md`

Sections 4 (Data-collection methods) and 5 (Analysis methodology) of the plan.

**Data-collection methods** — for each of the seven sources chapter `01` enumerates:

- **Telemetry from the deployed system.** Which production traces (OpenTelemetry Gen-AI, OpenInference, internal substrate), what sampling rate, what fields, what retention, and how they flow into the store. Owner: `ai-eval-engineer`.
- **Deployer channels.** The three shapes (contractual, platform, human) from chapter `01`, populated for this deployment — the contractual reporting schedule and format, the platform "report an issue" affordance and its schema, the human point-of-contact.
- **End-user feedback.** How thumbs-down / complaint / appeal / opt-out signal is collected under Article 13's transparency obligation and how it enters the store.
- **Internal red-team refresh.** Cadence (typically quarterly), scope (threat-model classes covered), owner (`ai-risk-engineer`).
- **External incident registries.** The three from chapter `05` (AI Incident Database, OECD.AI Incidents Monitor, MIT AI Risk Repository) — the ingest cadence and store landing.
- **Notified-body inspection findings.** How findings from an Article 43 pathway inspection or an Article 74 market-surveillance visit enter the plan.
- **Market-surveillance authority communications.** The channel for Article 74 / 79 notices, including per-Member-State authority contact (mark `<!-- needs-research: … -->` per Member State).

Each source names an ingest cadence, an owner peer track (with backup owner), a store landing, and a format specification.

**Analysis methodology** — for each measured characteristic in artefact 2, the plan names:

- **Statistical procedure** — bootstrap CI, drift test (KL-divergence / Kolmogorov-Smirnov / population-stability index), run-length control chart, or similar. Versioned.
- **Signal-aggregation rule** — how many independent sources must agree before a trigger fires. Chapter `01`'s worked example uses a two-source agreement rule; alternatives are possible.
- **Root-cause conservatism stance** — the default assumption when signal is ambiguous. Chapter `01`'s default is *treat as regression until disproven*, aligning with Article 73(2)'s "reasonable likelihood" language.
- **Human-triage cutoff** — which signals require human triage vs. automated disposition, with the specific rule (e.g., "any signal at severity S1 or above escalates to on-call human triage regardless of statistical significance").

### 4. `review-cadence-and-triggers-register.md`

Section 6 of the plan (Review cadence and triggers) plus the trigger register that operationalises chapter `03`.

**Standing cadence** — per monitored characteristic from artefact 2, the standing review cycle (weekly / monthly / quarterly) and the review-output artefact class.

**Event-triggered review rules** — the conditions under which an out-of-cadence review fires: threshold breach on a monitored characteristic, an external-incident-registry match (chapter `05`), a deployer escalation, a notified-body finding, or a serious incident (chapter `02`).

**Annual comprehensive review** — the annual calendar entry that re-visits the whole plan; the review record's landing in ISO/IEC 42001 clause 9.3 (management review).

**Trigger register** — at least five pre-registered triggers, one per row, with the five fields chapter `03` defines:

- Trigger identifier (e.g., `TRG-ART-15-ACC-01`).
- Source — the specific peer artefact class the trigger reads.
- Metric — the exact metric name (matches what the peer emits).
- Threshold — the pre-committed threshold, with the threshold-class (statistical significance / risk-tier promotion / adversarial-severity floor).
- Persistence window — how many observation windows the signal must persist across before firing.
- Authoriser — which role dispositions the re-review (on-call assurance engineer for statistical-warrant triggers at the tier the trigger covers; release-owner for risk-tier promotion; head-of-AI-governance for adversarial S1 or T3+ dispositions).
- Affected assurance-case claim — the specific claim the trigger defeats.
- Disposition wall-clock — how quickly the disposition must land (per chapter `03`'s wall-clock discipline).

**Article 20 integration** — the decision procedure that carries a monitoring finding into an Article 20 corrective action; the sign-off route; the corrective-action-record artefact class.

**Article 73 integration** — cross-reference to chapter `02`: which monitored characteristics can escalate into a serious incident, what triage carries the escalation, what the notification wall-clock is per Article 3(49) disjunct.

### 5. `change-control-and-annex-iv-integration.md`

Section 9 of the plan (Change control on the plan itself) plus the plan's integration with the Annex IV technical documentation and the assurance bundle.

- **Change-control discipline.** The plan is a controlled document under ISO/IEC 42001 clause 7.5. Every amendment carries a version identifier (semantic or content-addressed), a signer, a rationale, a diff against the superseded version, and a review-cadence commitment (annual + framework-update-triggered).
- **Supersession discipline.** The plan is *superseded*, not edited in place — the store carries every historical version by digest. `postmarket-plan/<system-slug>/v1` supersedes to `v2`; the assurance bundle for the current release candidate references the current version's digest under `post_market_handoff_digest`.
- **Annex IV integration.** The plan is part of the technical documentation referred to in Annex IV. Cite the Annex IV section under which the plan sits (or mark `<!-- needs-research: verify which Annex IV section the Commission has designated for the post-market monitoring plan -->`). The plan's inclusion is one of the manifest fields the release-gate walker checks at gate time.
- **Proportionality defence.** Chapter `01`'s heuristic — "the monitored characteristics are `{X, Y, Z}` because the harm inventory identifies `{H1, H2}` as material; the cadence is `{C}` because signal-to-noise resolves at that timescale; the analysis methodology is `{M}` because it detects the failure modes at the pre-registered significance in the pre-registered wall-clock" — applied concretely to this system, with citations back to the harm inventory (`mod-102` chapter `06`), the intended-purpose statement (from artefact 1), and the tier landing (from artefact 1).
- **Framework-update triggers.** The events that force a plan re-visit even outside the annual cadence: publication of an Article 96 delegated act, adoption of a harmonised standard, publication of a Commission implementing act laying down the plan template (chapter `01` flags this as pending), publication of updated NIST AI RMF or ISO/IEC 42001 guidance.
- **Framework citations.** The specific ISO/IEC 42001 clauses the plan discharges (7.5 documented information; 9.3 management review; 10.2 nonconformity and corrective action) and the NIST AI RMF functions the plan operationalises (`MEASURE` for the monitored-characteristics table, `MANAGE` for the trigger register).

## Starter guidance

- **Proportionality is not a get-out.** Chapter `01` is emphatic — proportionality means the monitoring effort scales with the risk profile, but the structural obligations (documented plan, actively and systematically operated, feeding Article 20 corrective action, integrating Article 73 incident reporting) are non-negotiable regardless of scale. A plan that reads "the system is low-risk, so we do less" collapses under adversarial reading.
- **Pre-register thresholds before signal appears.** A threshold set after the signal has been observed is a rationalisation, not a threshold. Every threshold in the monitored-characteristics table and the trigger register is pinned to the release-gate declaration or to the harm inventory *before* the plan is signed.
- **Specific metric names beat "quality" wishes.** Chapter `03` is emphatic — vague triggers ("if quality drops") are wishes, not triggers. Every metric name in the plan matches what the source peer emits.
- **Every characteristic gets a named peer owner with a backup.** "The MLOps team" or "the eval team" is not a named owner. "Alice Chen (backup: Bob Kim)" is. This is the same discipline `mod-109` chapter `06` applies to third-party engagement components.
- **The plan is a controlled document under ISO/IEC 42001 clause 7.5.** Versioned, signed, superseded (not edited in place), reviewed on a stated cadence. The change-control artefact is not an afterthought; it is what makes the plan defensible after two years of amendments.
- **The plan ships inside the Annex IV bundle at gate time.** Not months later, not "when the deployer complains". The `post_market_handoff_digest` manifest field in the assurance bundle (`mod-104` chapter `06`) is the release-gate's check that the plan is authored, signed, and content-addressed before the system is placed on the market.
- **The deployer channel is a coordination problem.** Deployers are separate legal entities (hospitals, banks, agencies) using the system under their own authority. Design all three channel shapes (contractual, platform, human) — the tiering (platform for standing signal, contractual for periodic reports, human for incidents) is chapter `01`'s recommendation.
- **`<!-- needs-research: … -->` markers are legitimate.** The Commission's implementing act on the plan template is pending; some Member State authority contacts are still being populated; some ISO clause numberings may drift. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `system-identification-brief.md` fixes provider identity + Article 49 registration reference + product/RC identifiers + intended-purpose statement + Annex III classification + notified body + declared Article 15 levels + tier landing + monitoring objectives. A reviewer can decide from the brief alone which system is in scope and what the plan is verifying.
- `monitored-characteristics-table.md` has at least eight rows covering at minimum Articles 9, 10, 13, 14, and 15; every row names obligation, characteristic, metric, threshold, cadence, source peer, and store landing. At least one Article 15 accuracy row is directly tied to the declared level in artefact 1.
- `data-collection-and-analysis-methods.md` covers all seven data sources chapter `01` enumerates, each with a named owner, ingest cadence, store landing, and format. The analysis-methodology section names a statistical procedure, signal-aggregation rule, root-cause-conservatism stance, and human-triage cutoff.
- `review-cadence-and-triggers-register.md` covers standing cadence, event-triggered rules, annual comprehensive review, and a trigger register with at least five triggers each with all fields from the chapter `03` five-part structure (plus affected claim and disposition wall-clock). Article 20 and Article 73 integration are explicit.
- `change-control-and-annex-iv-integration.md` covers change-control discipline, supersession, Annex IV integration, proportionality defence (with citations back to the harm inventory / intended purpose / tier), framework-update triggers, and framework citations. The proportionality defence follows chapter `01`'s heuristic rather than reading as "we do less because we are small".
- Every artefact's owner is a single named individual with a named backup, not a team.
- Every threshold in artefact 2 and artefact 4 is either pre-committed with a rationale or flagged `<!-- needs-research: … -->`. No made-up numbers.
- Every place a fact would need to be verified against the current Regulation text, a pending Commission implementing act, a specific Member State authority contact, or the enterprise's own policy is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Add a cross-jurisdictional overlay.** In `cross-jurisdictional-overlay.md`, extend the monitored-characteristics table with sector-regime tags (SR 11-7, FDA GMLP, DORA) per chapter `04`'s pattern, so a single row can discharge multiple regimes' obligations. Cross-reference `mod-107`.
- **Draft the Article 71 deployer-registration excerpt.** In `article-71-deployer-registration.md`, sketch the fields the deployer registration in the EU database carries (Article 49 for providers; deployer-side registration where required for public-authority deployers under Article 49(3)). Include the coordination workflow with Member State deployer registries where required.
- **Design the deployer-channel intake schema.** In `deployer-channel-schema.md`, formalise the platform-channel schema — the structured report format deployers submit, the field validation, the ingestion into the observability substrate, and the flow into the monitored-characteristics table.
- **Walk one worked signal end-to-end.** In `worked-signal-walkthrough.md`, pick one trigger from artefact 4, invent a plausible firing, and walk through the five-step re-review procedure from chapter `03` to a co-signed disposition and an Article 20 corrective action, landing as a superseding assurance-bundle record.
- **Author the plan-template crosswalk to Annex IV.** In `plan-annex-iv-crosswalk.md`, map every section of the plan (1-9) to the specific Annex IV subsection it satisfies. Where the mapping is uncertain pending the Commission's implementing act, mark `<!-- needs-research: … -->` explicitly.
