# exercise-01: SR-11-7-Shaped Document Set for One AI Model

**Estimated effort:** 3 hours

## Objective

Author the **SR-11-7-shaped model-risk-management document set** for one AI system deployed by a U.S. banking organisation. Produce the six load-bearing artefacts a U.S. bank's Model Risk Management (MRM) function would open at inspection — Model Description Document, development-test report, implementation-test report, model-use section, independent-validation report, and on-going-monitoring plan — plus a first Model Performance Report entry and a set of SR-23-4 crosswalk artefacts for the foundation-model dependency where one applies. The four SR-11-7 stress points chapter `01` names (foundation-model reuse, prompt-based / agentic surfaces, evaluation-set contamination, moving-upstream monitoring) must each be explicitly addressed.

The exercise is authoring, not solving. Placeholder evidence pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified with the bank's own MRM policy or with the vendor's own documentation.

## Prerequisites

- Chapter [`01-sr-11-7-and-model-risk-management-adapted-to-ai.md`](../01-sr-11-7-and-model-risk-management-adapted-to-ai.md) — the six-element paraphrase, the three lines of defence, the four stress points, the Model Performance Report standing artefact.
- Chapter [`02-sr-23-4-third-party-relationships-and-foundation-models.md`](../02-sr-23-4-third-party-relationships-and-foundation-models.md) — the SR 23-4 lifecycle and the seven-item contract-clause fight list; prerequisite background because most AI systems in a U.S. bank now carry a foundation-model dependency the SR-11-7 documents cross-reference.
- Skim access to [Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html). The guidance is short by regulatory standards (~21 pages); read the model-definition, effective-challenge, development-and-implementation, and validation-and-monitoring paragraphs directly.
- Familiarity with the peer-role registry for the AI Evaluation Engineer track (`ai-risk-engineer`, `model-evaluation-engineer`, `ai-governance-analyst`, `ai-infra-security`, platform-eng, product, legal, MRM validation lead, Internal Audit — plus your own role, `ai-evaluation-engineer`).

## Problem statement

Invent one specific AI system your U.S. bank plans to promote to a T3 or T4 deployment surface. Common patterns worth considering (pick one, or invent your own):

- **Credit-decisioning assistant** — an LLM-based summariser plus anomaly-surfacer that supports adjudicators reviewing consumer-credit or small-business-credit files. Human-in-the-loop; adverse-action-notice-relevant (chapter `06` overlay applies).
- **KYC / AML alert-triage assistant** — an LLM-based summariser of AML alert context plus a scoring re-ranker that orders the alert queue for investigators. Sits inside the bank's BSA / AML programme; regulator-visible.
- **Client-relationship-manager brief generator** — an LLM-based brief generator that summarises client documentation for relationship managers ahead of client meetings. Lower stakes per interaction but high-scale and consumer-adjacent.
- **Model-development co-pilot for the risk-modelling team** — an internal-facing LLM assistant helping quantitative modellers write and test SR-11-7-inventoried models. Second-order: the co-pilot's outputs land in *other* models' inventories.
- **Contact-centre agent-assist** — a real-time transcription + suggestion tool for contact-centre agents handling consumer inquiries. High volume, low latency, direct customer effect.

Fix the scoping first (see below), then author the artefact set. The system-invention step is not decorative — the MRM tier, the third-party arrangement classification, the evidence contracts, and every artefact signer depend on it.

## Requirements

Produce nine artefacts in a single directory, keyed to the SR-11-7 element they discharge.

### 1. `system-scoping-brief.md`

A one-to-two page brief that fixes:

- **Product name and one-sentence intended purpose.** Named product; specific decision the system informs; explicit statement of whether it makes any decision autonomously or supports a human decision-maker.
- **Composition.** Enumerate every *model* in SR-11-7's sense participating in the system. A RAG assistant is at least three models (foundation model, embedding / retrieval, re-ranker). A fine-tuned foundation model plus a guardrail classifier is at least two. Each becomes its own inventory row.
- **MRM tier.** Cite the bank's own MRM tiering methodology (if the bank has one; otherwise use the three-tier scheme from chapter `01`), state the tier, and give the reasoning against materiality of decisions, complexity, and exposure to model error. Where AI-specific factors (reversibility, scale, composability) matter for the tier, name them.
- **Deployment tier.** State the assurance-side deployment tier (T0–T4 per `mod-108`'s planned scheme, or your own labels) and the mapping to the MRM tier. Cite the mapping table your programme uses.
- **Third-party dependency classification.** For each third-party model or hosted-inference provider in the composition, name the provider and state whether the arrangement is *critical* under SR 23-4 (chapter `02`). If the system uses no third-party model, say so explicitly.
- **Business owner and MRM validation lead.** Named roles (or placeholder names) — the first-line business owner and the second-line MRM validation lead who will sign the validation report. Note the reporting-line independence.
- **Substantial-change rule.** Under what changes to the system (composition change, foundation-model version change, retrieval-corpus refresh, prompt-template major revision, MRM tier change) do you re-open the SR-11-7 document set? This is your revalidation-trigger definition.

The brief is the *setup* for the artefact set. Reviewers of the artefact set will read this first.

### 2. `01-model-description-document.md`

The Model Description Document (MDD) is the SR-11-7 sibling of EU AI Act Article 11 technical documentation. Author one MDD per model in the composition (three MDDs if you have three models — use `01a-…`, `01b-…`, `01c-…` where helpful). Each MDD covers:

- **Purpose and intended use.** What the model does inside the composition. What decision it participates in. What decisions it does *not* participate in.
- **Theory, methodology, and design.** For a classical model, the mathematical or statistical basis. For a foundation model, the family and version, the pretraining architecture (paraphrased from the vendor's system card), and any bank-side fine-tuning or adaptation.
- **Data.** Training data description; for a foundation model, a card-derived paraphrase citing the vendor system card, plus the bank-side data used for fine-tuning or retrieval. Data lineage, provenance, and known limitations.
- **Assumptions.** What the model design assumes about its inputs, its operating environment, and its intended population.
- **Implementation.** Where the model runs, how it is invoked, what pins its version, and how a version bump is detected.
- **Limitations.** Known failure modes, out-of-scope uses, and — for foundation-model-backed components — vendor-published limitations.

Where the MDD is *card-derived* (as it must be for a hosted foundation model), state so explicitly and cite the specific vendor card and version. Do not paraphrase vendor content beyond what a supervisor could verify against the vendor's own current documentation.

### 3. `02-development-testing-report.md`

The Model Development Testing report covers outcomes analysis, benchmarking, and sensitivity analysis for the composition. It must include:

- **Test design.** The test plan — datasets used, hold-out discipline, evaluation metrics, thresholds, statistical treatment (confidence intervals, group differences).
- **Evaluation-set integrity.** Explicit treatment of the SR-11-7 stress point on evaluation-set contamination. Where evaluation data may overlap with a foundation model's training corpus, name the mitigation (canary strings, private evaluation set, benchmark-refresh cadence). Where the evaluation set has been used publicly, note the exposure risk to the reported metric.
- **Outcomes analysis.** Reported metrics against the thresholds with confidence intervals; disaggregation by subgroup where the intended-use population supports it.
- **Benchmarking.** Comparison against a stated baseline (a prior model, a rules-based baseline, a human baseline, a competing model). For a foundation-model-backed component, benchmarking includes performance on the bank's own held-out evaluation set, not vendor-published benchmarks alone.
- **Sensitivity analysis.** Response of the reported metrics to perturbations of inputs, thresholds, or configuration. For prompt-based systems, sensitivity to prompt-template variation is part of the analysis.
- **Composition testing.** The critical addition SR 11-7's drafters did not name — end-to-end evaluation of the *composition* (all models together in the deployed configuration), not only per-model evaluation. Emergent failure modes only the composition surfaces are called out here.

### 4. `03-implementation-testing-report.md`

The Implementation Testing report covers change management, environment reproducibility, and controls. It must include:

- **Change management.** How versions are cut, promoted, rolled back. Version-control locations for model artefacts, prompt templates, retrieval indices, and configuration.
- **Environment reproducibility.** Container / runtime pinning; dependency pinning; secrets management; how a deployed environment is diffed against the intended state.
- **Access control.** Who can invoke the model, who can change the configuration, who can read the logs. RACI to the peer-role registry.
- **Operational monitoring.** What runs in production for observability (latency, error rate, throughput) as distinct from model performance (accuracy, calibration, drift — those live in the on-going-monitoring plan).
- **Foundation-model-version pinning discipline.** For any third-party model in the composition, how the pin is enforced, how a silent update would be detected, and what fires when a detection occurs. This addresses the SR-11-7 stress point on moving upstream.

### 5. `04-model-use-section.md`

The Model Use section documents the intended business use, the human oversight design, and any overrides. Cover:

- **Intended business use.** What decision the model informs; who consumes its output; the workflow the output enters.
- **Human oversight design.** For a decision-support system, how the human decision-maker is expected to weigh the model's output. Instructions provided to the human. Training the human receives. Cross-reference to EU AI Act Article 14 (human oversight) where applicable and to `mod-105`'s system-card human-oversight section.
- **Override design.** How a human can override, ignore, or escalate above a model output. How overrides are logged. Whether override patterns are analysed as a signal.
- **Consumer-facing effects.** Whether the output ever reaches a consumer directly (in a notice, a decision letter, a chat message). For consumer-credit systems, cross-reference the CFPB adverse-action-notice discipline from chapter `06`.
- **Out-of-scope uses.** Explicitly disclaimed uses the release-gate has not authorised; how the programme will detect and shut down attempted out-of-scope use.

### 6. `05-independent-validation-report.md`

The Independent Validation report is the second-line effective-challenge artefact — authored by MRM Validation, not by the model developer. For this exercise, author it as if you were the MRM Validation lead reviewing your own developer artefacts. It must cover:

- **Conceptual soundness assessment.** Does the model design fit the problem? Does the data support the design? Do the assumptions hold in the intended-use environment? The reviewer's own reasoned view, not a re-statement of the developer's own claims.
- **Process verification.** Verification that development discipline was followed — test/train disjointness, evaluation-set integrity, benchmarking rigour, sensitivity analysis coverage.
- **Outcomes analysis.** The reviewer's own reading of the reported metrics against the thresholds. Where the reviewer disagrees with the developer's interpretation, that disagreement is on the record here.
- **Composition validation.** Second-line validation of the composition, not only of the individual models. Where composition testing surfaces issues per-model testing missed, note them.
- **Deficiencies and remediation.** A tracked list of deficiencies with owners, due dates, and closure criteria. The release-gate does not close on unresolved material deficiencies.
- **Validation decision and scope.** The validator's stated decision — validated, validated with conditions, or not validated — and the scope over which the decision applies. The validity window (when re-validation is required) is stated here.
- **Independence statement.** The validator's own statement that they are independent of the model developer (no reporting line, no compensation link, no involvement in development). If the exercise scenario means the same person authored the developer artefacts and the validation report, note that as a *simulation artefact*, name what the real programme would require, and mark `<!-- needs-research: … -->` where the real independence chain would be established.

### 7. `06-ongoing-monitoring-plan.md`

The On-going Monitoring plan is what makes SR 11-7 a lifecycle regime rather than a point-in-time authorisation. It must cover:

- **Monitoring metrics.** What is measured continuously, at what cadence, with what thresholds. Per-model metrics *and* composition-level metrics.
- **Semantic and behavioural drift.** For prompt-based / generative components, drift measurement that captures behaviour changes not visible in scalar outcome metrics. Address the SR-11-7 stress point on prompt-based / agentic surfaces explicitly.
- **Outcomes analysis cadence.** How model outputs are compared against actual outcomes over time. For decision-support systems where the ground truth arrives with a lag, the cadence acknowledges the lag.
- **Vendor-side signal collection.** Provider status pages, published model updates, provider incident disclosures, safety-report updates, deprecation announcements — the SR-11-7 stress point on moving upstream. The plan names who monitors what, on what cadence, and with what escalation path.
- **Escalation and revalidation triggers.** What signals fire what actions (developer notification, MRM notification, MRC escalation, release-gate re-opening). Cross-reference the substantial-change rule from the scoping brief.
- **Reporting cadence.** How monitoring findings roll up into the Model Performance Report (below) and into the annual MRM inventory reconciliation.

### 8. `07-model-performance-report-template-and-first-entry.md`

The MPR is the standing artefact SR 11-7 introduces implicitly through its on-going-monitoring paragraphs and that most banks build explicitly. Produce two things:

- **The template.** What every MPR for this system will contain — sections, cadence, signer. For a Tier-1 model the cadence is typically monthly; for Tier-2, quarterly; for Tier-3, annually. State the cadence the scoping brief's MRM tier implies.
- **A first entry.** A worked entry as if the system had been in production for one reporting period. Populate the entry with representative metrics (placeholders are fine — do not fabricate specific numbers as if they were measured; use `<placeholder>` markers and note what the real programme would report).

The MPR entry names any vendor-side signals in the period, any material events (revalidations, exceptions, incidents), and the disposition for the coming period. It is signed by MRM Validation, reviewed by the model-risk committee, and referenced in the next release-gate cycle.

### 9. `sr-23-4-crosswalk.md`

For every third-party arrangement in the composition (foundation-model provider, hosted-inference vendor, judge-model provider, evaluation-platform vendor), a short crosswalk table matching the SR-23-4 lifecycle stages (planning, due diligence, contract, on-going monitoring, termination) against:

- The artefact the release-package carries for that stage.
- The SR-11-7 document (from above) that cross-references the SR-23-4 artefact.
- The seven contract-clause items from chapter `02` — for each, whether it is executed, executed-with-gaps, or missing. Where missing, the release-gate disposition for the gap.
- The concentration and sub-outsourcing note — for the provider, its own upstream dependencies where known, and what happens if the concentration or sub-outsourcing hazard materialises.

If the system uses no third-party model, write a two-line `sr-23-4-not-applicable.md` explaining why, and skip artefact 9.

## Starter guidance

- **Fix scoping first, then author.** The MRM tier, the deployment tier, the third-party classification, and the substantial-change rule all cascade through every artefact. Getting them wrong on the scoping brief means rewriting five artefacts. Getting them right saves the exercise.
- **Every model in the composition is a model in SR-11-7's sense.** A RAG assistant is not one model. Do not fold the retriever, the re-ranker, and the LLM into a single MDD; they are three MDDs. The composition's emergent behaviour is a fourth artefact section, not the whole set.
- **Foundation-model MDDs are card-derived. Say so.** A supervisor who reads a paragraph paraphrasing a vendor's system card without a citation will assume you invented it. Cite the exact vendor card and version and mark any claim you cannot verify with `<!-- needs-research: … -->`.
- **Effective challenge is a role, not a paragraph.** The Independent Validation report reads as authored by the second-line function, not as authored by the developer with a rubber-stamp. The reviewer's own view is on the record, including where they disagree with the developer. If you are simulating both, name that.
- **Composition testing catches what per-model testing does not.** Emergent failure modes — retrieval misfires that the LLM confidently paraphrases; guardrail regressions that only surface under long prompts; ranker-plus-generator interactions — are only visible at the composition level. Section 6 of the Development Testing report is often the section a supervisor probes.
- **Evaluation-set integrity is a first-class artefact, not a footnote.** SR 11-7's development-testing paragraph did not name evaluation-set contamination, but the release-package for a foundation-model-backed system must address it. Canary strings, private evaluation sets, benchmark-refresh cadence — each is a specific artefact the release-gate consumes.
- **Vendor-side signals belong on the monitoring plan.** The most common release-gate oversight in AI-in-bank practice is a monitoring plan written as if only the *world* drifts. Foundation-model providers push silent updates, deprecations, and safety-classifier changes. The monitoring plan says who watches, at what cadence, with what escalation.
- **Independence is a signer question.** The Model Description Document, the Development Testing report, and the Implementation Testing report are developer-side artefacts. The Independent Validation report is second-line. The signer of the release decision is not the model developer, does not report to the model developer, and does not have a compensation link to the model's business outcomes. Name the signers.
- **The MPR is the recurring artefact the release-gate re-opens against.** The release-gate does not close on ship; it hands off to a monitoring cadence, and every MPR is a re-opening. Design the MPR template with that recurrence in mind.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the bank's own MRM policy, the vendor's own current documentation, or a specific supervisor's expectation for the sector, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `system-scoping-brief.md` fixes the seven scoping decisions with reasoning. A reviewer can decide, from the brief alone, the composition, the MRM tier, the deployment tier, the third-party classification, and the substantial-change rule.
- Every model in the composition has its own `01-model-description-document.md` (or `01a-…`, `01b-…`, `01c-…`). Foundation-model MDDs are labelled as card-derived and cite the vendor card and version.
- `02-development-testing-report.md` covers all six sections including the composition-testing section. Evaluation-set-integrity treatment is explicit and names concrete mitigations.
- `03-implementation-testing-report.md` covers change management, environment reproducibility, access control, operational monitoring, and foundation-model pinning discipline. The silent-update detection procedure is described.
- `04-model-use-section.md` describes intended use, human oversight, override design, consumer-facing effects, and out-of-scope uses. Consumer-facing effects cross-reference the CFPB overlay where applicable.
- `05-independent-validation-report.md` is authored in the voice of an independent second-line validator. Deficiencies (if any) are tracked. The independence statement is present, even if it is a simulation-artefact caveat.
- `06-ongoing-monitoring-plan.md` covers per-model and composition-level metrics, semantic / behavioural drift, outcomes analysis, vendor-side signals, and escalation / revalidation triggers. The MRM tier's cadence is applied.
- `07-model-performance-report-template-and-first-entry.md` provides both a reusable template and a worked first entry. Placeholders are marked; no numbers are fabricated as if measured.
- `sr-23-4-crosswalk.md` covers every third-party arrangement in the composition and populates all five SR-23-4 lifecycle stages against the SR-11-7 artefacts and the seven contract-clause items.
- Every one of the four SR-11-7 stress points from chapter `01` is *explicitly* addressed somewhere in the set: foundation-model reuse (in the MDD and SR-23-4 crosswalk), prompt-based / agentic surfaces (in the Development Testing and On-going Monitoring reports), evaluation-set contamination (in the Development Testing report), and moving-upstream monitoring (in the Implementation Testing and On-going Monitoring reports).
- Every place a fact would need to be verified against the bank's own MRM policy or the vendor's current documentation is marked `<!-- needs-research: … -->` rather than guessed.
- The document set is *consistent* — the composition on the scoping brief matches the composition in the MDDs, the substantial-change rule matches the revalidation triggers in the monitoring plan, the MRM tier matches the MPR cadence. A reviewer diffing across the set finds no drift.

## Stretch goals

- **Author the model-risk-committee memo.** The committee that approves the release for T3/T4 promotion typically reads a two-to-three page memo synthesising the artefact set. In `08-mrc-memo.md`, draft that memo — decision requested, one-paragraph model description, key MRM Validation findings, deficiencies (open and closed), vendor-side signals, recommended decision. This is what senior management actually reads.
- **Draft the release-gate criterion set derived from the artefact set.** In `release-gate-criteria.md`, extract the hard-gate and soft-gate criteria the release-gate enforces derived from the sector obligations. For each criterion, name the artefact that discharges it, the signer, the currency window, and the disposition for failure.
- **Add a Q-submission for a contested change.** Where the substantial-change rule contemplates a change whose SR-11-7 classification is not clean-cut (e.g., a foundation-model minor-version bump the vendor calls compatible but which the bank's evaluation may not confirm), draft the Q-submission-like memo to MRM that asks for a reading. Note that in real practice this is a memo to MRM Validation, not a filing with a supervisor; the shape is worth practising.
- **Draft the Internal Audit workpaper shell.** In `internal-audit-workpaper.md`, sketch what an Internal Audit reviewer would read across the artefact set — the second-line's own coverage of the six SR-11-7 elements, the effective-challenge trail, the deficiencies pipeline, the MPR chain. This is the third-line loop.
- **Author the retirement plan.** SR 11-7 covers models to be retired as well as models in use. In `retirement-plan.md`, sketch the retirement pathway — the substitution or graceful degradation, the customer-facing communication if any, the record-retention obligations, the SR-23-4 termination-triggering elements if the retirement involves ending a vendor arrangement.
- **Add the OCC 2011-12 mapping.** In `occ-2011-12-mapping.md`, walk paragraph by paragraph through OCC Bulletin 2011-12 and note where the exercise's artefact set differs — if at all — from what OCC's text specifically calls for. OCC and Fed are aligned in substance; the exercise is in the small deltas that occasionally matter for OCC-supervised institutions.
