# exercise-03: NYC AEDT Independent Bias Audit Envelope

**Estimated effort:** 2 hours

## Objective

Prepare the **AEDT independent bias audit envelope** for one worked in-scope hiring or promotion product and defend the four dataset-preparation dimensions against the DCWP independence line. Produce the auditor-selection memo, the input dataset specification, the category-tagging attestation, the historical-data option memo, and the candidate-notice pointer that the employer's HR or talent function will consume.

The exercise is design and authoring, not solving. The audit is prescribed by DCWP rule — the exercise's discipline is on the *input side* the programme controls, not on the auditor's methodology.

## Prerequisites

- Chapter [`03-nyc-local-law-144-aedt-independent-bias-audit.md`](../03-nyc-local-law-144-aedt-independent-bias-audit.md) — the DCWP definition of an AEDT, the independent-auditor independence tests, the prescribed statistical output, the four dataset-preparation dimensions, the candidate-notice obligation, and the four-axis contrast with AISI-shape evaluation.
- Chapter [`06-delivery-timing-envelope-and-evidence-hardening-playbook.md`](../06-delivery-timing-envelope-and-evidence-hardening-playbook.md) — the engagement-charter template applied to the AEDT engagement type, with the credentialed-access channel typically marked "not applicable" and the input dataset substituting for reproducibility bundles.
- Familiarity with `mod-104` chapter `05` (MLSec attestations — eval-set-integrity and exfiltration control) and `mod-104` chapter `01` (evidence pipeline — the online-eval slice as the source for the input dataset).
- Familiarity with `mod-106` (cross-jurisdictional mapping) where the same product may face parallel obligations under Colorado SB 24-205, Illinois, or EU AI Act Annex III point 4.
- Skim access to the DCWP AEDT hub at [nyc.gov/site/dca/about/automated-employment-decision-tools.page](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) and the rule text at [rules.cityofnewyork.us/rule/automated-employment-decision-tools-updated/](https://rules.cityofnewyork.us/rule/automated-employment-decision-tools-updated/) <!-- needs-research: verify current published rule URL and any DCWP amendments -->.

## Problem statement

Pick one in-scope AEDT deployment. The choice must:

- **Sit in scope of DCWP's definition.** The tool's output must *substantially assist or replace* discretionary decision-making on hiring or promotion decisions for candidates residing in New York City.
- **Have a plausible historical operating window.** The audit requires a dataset representative of the tool's operation across a defined historical window — the tool must have been operating long enough for a meaningful window, or the exercise has to invoke the historical-data option explicitly.

Common shapes worth considering:

- **Resume-screening ATS scoring model.** A model that ranks incoming resumes for a specific job-family; the ranking is used by recruiters to shortlist candidates.
- **Video-interview scoring model.** A model that scores recorded candidate interviews on a set of dimensions; the score is used to advance or reject the candidate.
- **Assessment-scoring model.** A model that grades candidate performance on a structured skills assessment; the grade contributes to the hire/no-hire decision.
- **Promotion-recommendation model.** A model that flags employees for promotion consideration based on tenure, performance, and role-fit features.

Pin the product, the employer, and the historical window before you begin the artefact set.

## Requirements

Produce five artefacts in a single directory.

### 1. `deployment-and-scope-memo.md`

A one-page memo that fixes:

- **Employer and product identity.** Named employer or employment agency, named AEDT product, the product's version identifier(s) that will be covered by the audit, one-sentence position of the tool in the hiring or promotion workflow.
- **Substantially-assist-or-replace justification.** A short paragraph explaining why the tool's output substantially assists or replaces the human decision-maker's discretion (per DCWP's definition). This is the in-scope determination.
- **Geographic-scope note.** How the employer identifies candidates residing in New York City in the operational dataset. Candidate self-declaration, address on the application form, or an inferred determination — with the source system and the reliability caveat named.
- **Historical window.** The specific twelve-month (or shorter, if the tool has been in use less than twelve months) window the audit will cover. The window's end date is within one year prior to the audit's target use — DCWP requires the audit be completed within one year prior to use, per chapter `03`.
- **Prior-audit history.** If the tool has previously been audited (annual re-audit obligation), the prior audit's identifier and the delta since the prior audit. The delta is what the current audit's summary will describe as *material changes since the last audit*.
- **Peer-role dependencies.** Which peer roles will contribute — typically `ai-eval-engineer` (online-eval slice access for dataset assembly), `ai-risk-engineer` (fairness-metric methodology), and `ai-infra-security` (integrity attestation on the delivered dataset).

### 2. `auditor-selection-memo.md`

A short memo (two to three pages) that documents the auditor selection. Sections:

- **Independence tests.** The DCWP's independence criteria applied to each shortlisted auditor — no employment relationship with the employer, employment agency, or AEDT provider; no involvement in the tool's design, development, or implementation; no direct financial interest in the outcome; no reasonable question of independence.
- **Shortlist.** Three plausible auditors (specialist HR-analytics consulting firm, employment-law-adjacent quant shop, Big-Four-shape firm with a Local Law 144 practice). For each, cite a plausible auditor profile — the firm's publicly-stated Local Law 144 practice, references from prior engagements, published methodology briefs.
- **Comparison table.** Columns: independence attestation depth, Local Law 144 methodology familiarity, references from prior engagements, indicative timeline, fees.
- **Selection.** The selected auditor and the reason. Chapter `03` is emphatic — auditor selection favours documented independence and methodology familiarity over price.
- **Engagement scope.** The version(s) of the tool covered, the historical window, the auditor's right to describe the audit methodology in the summary (per DCWP publication requirements), and the deliverable — the summary of results and any supplementary methodology annex.
- **Confidentiality boundaries.** What the auditor sees (the audit dataset, the tool's methodology memo, the data-dictionary), what the auditor does *not* see (candidate PII beyond what the DCWP methodology requires, commercially-sensitive product roadmaps, non-Local-Law-144 evaluation results).

### 3. `input-dataset-specification.md`

The input dataset specification the auditor consumes. This artefact is the *core* of the exercise — chapter `03` is emphatic that the programme's leverage on the audit is on the input side, not on the methodology side. Sections:

- **Row-level schema.** Every column of the delivered dataset, with source system, transformation applied (if any), and the peer-role owner. Columns include the AEDT's inputs (features the model consumes), the AEDT's output (score, classification, or recommendation), the downstream hiring or promotion outcome tied to the candidate (shortlisted / interviewed / offered / hired / promoted, as applicable), and the candidate's self-identified category tags (race / ethnicity / sex, and their intersections).
- **Representative-sample attestation.** The four dataset-preparation dimensions from chapter `03` applied concretely to this dataset:
  - **Representative sample.** How the dataset covers the AEDT's operation across the historical window — the sampling strategy, coverage attestation from `ai-eval-engineer`, and the reasoning against sampling artefacts (mid-window behaviour shifts, one-pipeline-among-several coverage).
  - **Category tagging.** How the category tags were sourced from candidate self-identification or EEO data collection. Explicit attestation that no category tag was *inferred* from other features (name, ZIP code, photo).
  - **Statistical sufficiency.** Sample-size analysis by intersectional category against the auditor's expected minimum-sample-size threshold. Where a category is under-sampled, the reason (small applicant-pool, role-class scoping) and the disposition (exclude from ratio calculation with disclosure, invoke historical-data option).
  - **Data lineage and integrity.** The lineage trace from each row back to the AEDT operation and the candidate record. MLSec integrity attestation confirming no rows were dropped or reweighted before delivery. Cross-reference `mod-104` chapter `05` MLSec attestations.
- **Delivery mechanism.** How the dataset is delivered to the auditor — secure workspace, encryption in transit and at rest, access-log capture. What the auditor is contractually obliged to do with the dataset after audit completion (destroy, return, retain under NDA per an agreed retention window).

### 4. `historical-data-option-memo.md`

Where the tool has been in use for less than the audit's target window, or where sample-size on any category is insufficient for the impact-ratio calculation, the DCWP rules allow a *historical-data option* — the employer may use test data or historical data from a similar AEDT for the audit's ratio calculations <!-- needs-research: verify the historical-data option is still available under the current DCWP rule and its exact wording -->.

If the audit's dataset requires the historical-data option (or if you want to exercise the memo even where it does not), author:

- **Trigger.** The specific condition invoking the option (insufficient in-scope operational data, under-sampled intersectional category, tool freshly deployed).
- **Data source.** Where the historical or test data comes from — a prior version of the same tool, a similar tool from the same vendor, a controlled test dataset with synthetic candidates. The source is disclosed to the auditor.
- **Comparability defence.** Why the historical or test data is a defensible substitute for operational data — feature-set overlap, decision-mechanism similarity, demographic-composition similarity.
- **Auditor's disclosure disposition.** How the auditor will describe the option's invocation in the summary of results the employer will publish. The disclosure is required by DCWP rule; the memo pre-empts the disclosure's shape so the summary does not surprise.

Where the option is not invoked, this memo is a *not-invoked* memo — a short attestation that the operational-data path is sufficient and the option was considered but declined, with the coverage numbers supporting the decision.

### 5. `candidate-notice-and-publication-plan.md`

The plan for the DCWP's candidate-notice and publication obligations. The release-assurance programme's role here is *supporting*, not *owning* — the notice is typically owned by HR or talent — but the programme has to produce the audit-summary URL and the underlying-data descriptions the notice cites, on the timing the notice requires. Sections:

- **Notice content.** What the advance notice tells candidates: the tool's use, the job qualifications and characteristics the tool will assess, the type of data collected (on request), the source of the data (on request), the employer's data-retention policy (on request), and the audit-summary URL.
- **Notice timing.** The DCWP-required lead time (at least ten business days before use) and how the timing is enforced in the applicant-tracking workflow. Where a candidate is added to the pipeline within the ten-day window, the disposition — defer AEDT scoring, use a non-AEDT screening path, delay pipeline entry.
- **Publication location.** Where the audit summary is posted on the employer's or employment agency's website — the URL, the accessibility test (candidates with assistive-technology access), and the retention period during which the summary remains posted.
- **Distribution to candidates.** How the summary is distributed to candidates as part of the notice — inline in the notice text, linked from the notice, or attached separately.
- **Annual re-audit calendar.** The re-audit trigger date (twelve months from the current audit's completion date), the envelope-ready lead time (per chapter `06` calibration for the AEDT engagement type), and the release-gate criterion that flags any AEDT operation lacking a current audit.
- **Escalation on audit lapse.** What happens if the audit is not current at the notice-issue date — the AEDT cannot be used, the applicant pipeline routes through a non-AEDT path, and the escalation to `head-of-ai-governance` (level 60) for the audit gap.

## Starter guidance

- **The programme's leverage is on the input, not on the methodology.** DCWP prescribes the auditor's methodology; the programme's discipline is on the dataset that feeds the methodology. `input-dataset-specification.md` is the load-bearing artefact.
- **Inferred category tags invalidate the audit.** Chapter `03` is emphatic — tags from names, ZIP codes, or photos are not acceptable evidence. If the applicant tracking system does not collect self-identified tags, the audit cannot run as designed and the historical-data option or a data-collection uplift is the disposition.
- **The auditor's independence line is not negotiable.** The programme's role is to prepare the input well, not to influence the auditor's methodology or the summary's numbers. Author the artefacts as if you were preparing evidence for a judge, not for a business partner.
- **The summary of results will be published.** Every number the auditor produces will be publicly posted. The `input-dataset-specification.md` and the `historical-data-option-memo.md` are what the summary's methodology annex will reference — draft them assuming external scrutiny.
- **The candidate-notice obligation is a hard-gate for release.** Chapter `03` frames this — the AEDT cannot lawfully be used without a current audit. The release-gate criterion foreshadowed in `candidate-notice-and-publication-plan.md` is the enforcement point.
- **Cross-jurisdiction is coming.** Colorado SB 24-205, Illinois, EU AI Act Annex III point 4 — the AEDT-shape audit is likely to appear in multiple jurisdictions the same product ships into. Note in the memo where the input-dataset specification is designed for reuse across jurisdictions rather than bespoke to Local Law 144.
- **`<!-- needs-research: … -->` markers are legitimate.** The DCWP rule has been amended since initial publication; verify the current published rule URL and any specific threshold values before citing them.

## Acceptance criteria

You have succeeded if:

- `deployment-and-scope-memo.md` fixes the six scoping decisions (identity, in-scope justification, geographic-scope, historical window, prior-audit history, peer-role dependencies). A reviewer can decide, from the memo alone, whether the AEDT falls in DCWP's scope and what the audit's historical window covers.
- `auditor-selection-memo.md` presents three plausible auditors, applies the DCWP independence tests to each, selects one, and documents contract touchpoints and confidentiality boundaries.
- `input-dataset-specification.md` covers the row-level schema, the four dataset-preparation dimensions (representative sample, category tagging, statistical sufficiency, data lineage and integrity), and the delivery mechanism. Every column names its source system, transformation, and peer-role owner. No category tag is inferred.
- `historical-data-option-memo.md` is either an invocation memo (trigger, source, comparability defence, disclosure disposition) or a not-invoked memo (coverage numbers supporting the decision). The option's status is explicit.
- `candidate-notice-and-publication-plan.md` covers notice content, notice timing, publication location, distribution to candidates, annual re-audit calendar, and escalation on audit lapse. The release-gate criterion for missing-audit is foreshadowed.
- The four dataset-preparation dimensions are traceable — the representative-sample attestation names the sampling strategy, the category-tagging attestation names the source, the statistical-sufficiency analysis names the under-sampled categories, and the lineage-and-integrity attestation cites `mod-104` chapter `05`.
- The auditor's independence line is respected — nothing in the envelope reads as pressure on the auditor's methodology or the summary's numbers.
- Every place a fact would need to be verified against the current DCWP rule text, a specific auditor's public methodology, or the employer's own applicant-tracking configuration is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Cross-jurisdictional adapter.** In `cross-jurisdictional-input-adapter.md`, describe how the input-dataset specification designed for Local Law 144 is adapted for Colorado SB 24-205 and for EU AI Act Annex III point 4 hiring systems. Cross-reference `mod-106` where the crosswalk lives.
- **Draft the audit-summary review protocol.** In `summary-review-protocol.md`, author the internal review the programme runs on the auditor's draft summary — the factual-accuracy checks, the consistency-with-dataset checks, and the strict prohibition against methodology negotiation or number adjustment. Cite chapter `03`'s worked-example step 7.
- **Author the release-gate substantial-modification test for AEDTs.** In `aedt-substantial-modification-test.md`, express the AEDT-specific substantial-modification test — material change to input features, to output-thresholding, to workflow position — as a release-gate criterion in the `mod-103` chapter `02` format. Any material change invalidates the current audit's coverage.
- **Draft the incident-response playbook for an unfavourable audit.** In `unfavourable-audit-response.md`, walk what the programme does if the audit surfaces an impact ratio below 0.8 for one or more intersectional categories — the tool-remediation options (feature removal, threshold adjustment, hybrid human-review path), the release-gate hold pending remediation, the escalation to `head-of-ai-governance`, and the candidate-notice implications during the remediation window.
- **Compose the ML-BOM for the AEDT.** In `aedt-mlbom.md`, sketch the `mod-104` chapter `04` ML-BOM for the AEDT — the training-data provenance, the model architecture, the deployment surface, the guardrails — that the auditor sees as an appended methodology reference where the auditor requests it.
