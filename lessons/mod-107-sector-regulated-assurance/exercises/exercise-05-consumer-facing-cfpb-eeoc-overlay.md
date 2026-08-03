# exercise-05: Consumer-Facing Overlay Row and Vendor-Coverage Map

**Estimated effort:** 2 hours

## Objective

For one consumer-facing AI system deployed by a U.S. organisation, produce the **consumer-facing-overlay row of the release-package** — the CFPB adverse-action-reason artefact and reasoning-fidelity plan (for credit-adjacent systems), the EEOC ADA and Title VII analysis artefact set (for employment systems), an adjacent-overlay note (HUD Fair Housing, state-law overlays), and a **vendor-platform coverage map** that shows what a candidate vendor platform (ModelOp Center, Monitaur Governance OS, Fiddler AI, or a comparable) covers of the sector-regulated-programme surface and where the release-assurance owner still authors manually.

The exercise is authoring, not solving. Every vendor claim is provisional; the coverage map is the exercise of *evaluating* the vendor's claims against a programme, not of trusting them. Every consumer-facing overlay is subject to shift in guidance; the exercise emphasises citing primary sources and marking `<!-- needs-research: … -->` where facts would need to be verified.

## Prerequisites

- Chapter [`06-consumer-facing-overlays-cfpb-eeoc-ada-and-vendor-platforms.md`](../06-consumer-facing-overlays-cfpb-eeoc-ada-and-vendor-platforms.md) — the CFPB circulars, the EEOC guidance, the adjacent overlays, the vendor platform landscape, and the *operational layer* / *authorship layer* distinction that governs the vendor evaluation.
- Chapter [`02-sr-23-4-third-party-relationships-and-foundation-models.md`](../02-sr-23-4-third-party-relationships-and-foundation-models.md) — the SR-23-4-shaped due-diligence shape the vendor-coverage map reads to for the platform vendor itself.
- Skim access to:
  - [CFPB Circular 2022-03](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) and [CFPB Circular 2023-03](https://www.consumerfinance.gov/compliance/circulars/circular-2023-03/).
  - [EEOC — *The Americans with Disabilities Act and the Use of Software, Algorithms, and AI to Assess Job Applicants and Employees* (2022)](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence).
  - [EEOC — *Assessing Adverse Impact in Software, Algorithms, and AI Used in Employment Selection Procedures* (2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial).
- Familiarity with the peer-role registry — the release-assurance owner works alongside compliance, legal, HR (for employment systems), and the platform vendor's account team (for vendor-coverage evaluation).

## Problem statement

Invent the consumer-facing AI system and the deploying organisation. The scenario must trigger at least one of the two consumer-facing overlays (CFPB or EEOC). If the credit-decisioning assistant from exercise `01` is a natural fit, reuse it and add the CFPB overlay layer; if not, invent afresh.

Common patterns worth considering (pick one, or invent your own):

- **Credit-decisioning assistant at a U.S. bank** — the chapter `01` worked shape. CFPB Circulars 2022-03 and 2023-03 attach; EEOC does not; state overlays may attach (e.g., Colorado SB 24-205 for a consequential-decision determination).
- **Hiring-decision AI at a mid-sized U.S. employer** — the chapter `06` worked shape. EEOC ADA and Title VII overlays attach; NYC LL 144 attaches for NYC-located applicants; CFPB does not; Colorado SB 24-205 may attach.
- **Consumer-credit adjudication AI at a fintech lender** — CFPB Circulars attach fully; EEOC does not; HUD Fair Housing may attach if the lender's products include housing-adjacent lending.
- **Tenant-screening AI at a property-management firm** — HUD Fair Housing overlay is central; CFPB is out of scope; state overlays vary.
- **AI-based debt-collection assistant** — CFPB UDAAP considerations attach; adverse-action does not (debt-collection is downstream); FDCPA overlay may apply.
- **Employer benefits-eligibility screening AI** — EEOC ADA attaches (benefits-decision related); ERISA overlays may attach; state overlays may attach.

Pin the scenario before authoring:

- The AI system's intended purpose and the specific consumer-facing decision it participates in.
- The regulatory footprint — CFPB, EEOC, HUD, state authorities.
- The composition of the AI system (vendor-supplied components, in-house components, foundation-model dependency).
- The candidate vendor platform (or platforms) evaluated in the coverage map. Pick one to concentrate on — ModelOp Center, Monitaur Governance OS, or Fiddler AI is fine; a comparable platform is fine; a "no platform, all in-house" is also a valid choice as long as the coverage map addresses what the release-assurance owner would build.

## Requirements

Produce five artefacts in a single directory.

### 1. `scenario-scoping-brief.md`

A one-page brief that fixes:

- **Product name and one-sentence intended purpose.** Named product; specific consumer-facing decision informed; whether the AI decides autonomously or supports a human decision-maker.
- **Overlay scope.** Which consumer-facing overlays attach and which do not, with reasoning. Explicit not-applicable determinations for every overlay in the chapter (CFPB, EEOC ADA, EEOC Title VII, HUD, state-law overlays).
- **Composition.** What runs in-house, what runs at a vendor, and what runs at a foundation-model provider (if any).
- **Candidate platform.** The vendor platform (or "no platform") the coverage map evaluates.
- **Legal-counsel countersign.** Which determinations require legal-counsel countersign (typically all applicability determinations) and what the current sign-off state is (or a simulation-artefact caveat).

### 2. `consumer-facing-overlay-row.md`

The overlay row itself — a YAML entry (or a well-structured table) with one row per applicable consumer-facing obligation. For each row:

- **Obligation identifier.** Unique within the release-package (e.g. `cfpb.circular-2022-03.specific-reasons`, `cfpb.circular-2023-03.accuracy`, `eeoc.ada.screening-out`, `eeoc.ada.inaccessibility`, `eeoc.ada.medical-inquiry`, `eeoc.title-vii.adverse-impact`, `hud.fair-housing.tenant-screening`, `co.sb-24-205.deployer-notice`, `nyc.ll-144.bias-audit`).
- **Primary source citation.** URL and specific paragraph or section.
- **Obligation summary.** One-sentence paraphrase.
- **Applies-when condition.** The scoping determination that puts the obligation in scope for the system, with `determined_by: legal-counsel` and a determination date.
- **Deliverable.** The specific artefact (filename) that discharges the obligation.
- **Owner role.** Which peer role produces the substantive content.
- **Signing role.** Which role's signature closes the deliverable — for consumer-facing overlays, typically compliance / legal.
- **Cross-reference to anchor artefacts.** If the deliverable is shared with an artefact produced under SR 11-7 (chapter `01`), DORA (chapter `04`), EU AI Act (from `mod-106`), or another framework, name the cross-reference.
- **Post-market monitoring hook.** Which post-market signal (from `mod-110`) would fire a re-evaluation of the row. For CFPB accuracy, drift between stated adverse-action reasons and the model's actual decision drivers; for EEOC adverse impact, drift in subgroup impact ratios over time.
- **Notes.** Any specific trap or nuance for the row.

### 3. `adverse-action-reason-artefact.md` *(only if CFPB is in scope)*

The load-bearing artefact for a CFPB-in-scope system. Cover:

- **Reason-code catalogue.** The specific reason codes the system uses, each keyed to a model decision driver rather than to a vendor-list proxy. If the system uses vendor-list proxies out of necessity, name the reason and the plan to move to substantive codes.
- **Derivation method.** How reason codes are derived from the model — SHAP, LIME, counterfactual explanations, or another method. Cite the specific method. Note the method's fidelity limitations.
- **Fidelity evaluation.** How the programme measures whether reason codes accurately reflect the model's actual decision drivers (as CFPB Circular 2023-03 requires). What is measured. What threshold is acceptable. What the release-gate consumes as evidence of fidelity.
- **Notice template.** How the reason code lands in the adverse-action notice the consumer receives. The ECOA / Regulation B "specific and accurate" standard is what the notice discharges.
- **LLM-narration risk.** If an LLM is used to *narrate* reasons on top of the underlying scoring model, the risk that the LLM's narration misrepresents the scoring model's actual reasons. The mitigation — LLM-narration fidelity evaluation, human review, restrictions on generative content in adverse-action notices.
- **Cross-reference to the credit-decision explainability policy.** The standing programme document the artefact discharges into.

If CFPB is out of scope, produce a two-line `cfpb-not-in-scope.md` recording the determination and skip this artefact.

### 4. `eeoc-analysis-set.md` *(only if EEOC is in scope)*

For an EEOC-in-scope employment system, three sub-artefacts (as sections of one file or three files):

- **`ada-analysis.md`** — covering the three vectors from the EEOC 2022 ADA guidance: screening-out (does the tool disqualify applicants because of characteristics correlated with a disability?), inaccessibility (can applicants with disabilities use the tool at all?), and medical-inquiry / disability-related-inquiry (does the tool ask disability-related questions or elicit medical information without justification?). For each vector, the analysis, the mitigations, and the residual risk. Plus the **reasonable-accommodation procedure** — how an applicant requests an alternative assessment, who reviews it, who decides, and how the applicant is informed the option exists.
- **`adverse-impact-analysis.md`** — the UGESP-shaped four-fifths analysis (or a more-appropriate statistical approach where the population supports one) across protected classes reachable in the intended-use population. Where a disparate impact is present, the **job-relatedness and business-necessity** justification. Where a disparate impact is not present, the analysis and the currency window before re-analysis is required. Note that "we have no data on protected classes" is not a defence; the analysis must be run on the data reasonably available under applicable law.
- **`vendor-immunity-note.md`** — the programme's position that the deployer's liability is not extinguished by vendor conduct. Where the AI tool is vendor-supplied, the deployer's assurance case has a claim about EEOC compliance whose evidence includes an *away-claim* into the vendor's documentation (cross-reference `mod-102`), but the deployer's case is where the release-gate closes.

If EEOC is out of scope, produce a two-line `eeoc-not-in-scope.md` recording the determination and skip this artefact.

### 5. `vendor-platform-coverage-map.md`

The coverage map for the candidate vendor platform (or the "no platform" analysis). Two sections:

**Section A — Coverage claims and evidence.** A table with one row per major coverage claim the vendor makes (or per major coverage the release-assurance owner would need). For each row:

- **Coverage area.** Model inventory, workflow orchestration, evidence storage, monitoring signals, cross-framework mapping, sector-template shipping, third-party arrangement tracking, etc.
- **Vendor claim.** The vendor's own stated coverage, marked `<!-- needs-research: … -->` for any claim that would need verification against the vendor's current documentation.
- **Verification approach.** How the release-assurance owner would confirm the claim — vendor demo, product documentation, reference customer, POC.
- **Fit for this programme.** Whether the coverage fits the specific programme's shape. A ModelOp Center inventory row may be a great fit for a bank's MRM inventory but require tailoring for an insurer's DORA register.
- **Gaps.** Where the coverage is partial or absent, what the release-assurance owner still authors manually or acquires from a second vendor.

**Section B — Authorship-layer boundary.** A short section naming the parts of the release-assurance programme that the vendor platform *cannot* cover:

- **Criterion selection.** The release-gate criteria remain the release-assurance owner's authorship.
- **Sector-rule interpretation.** SR 11-7 / DORA / GMLP interpretation remains the second-line function's judgment.
- **Effective-challenge decisions.** MRM validation approvals, soft-gate dispositions, waiver dispositions remain human judgment on the record; the platform records but does not replace them.
- **Concentration and residual dispositions.** CRO-level judgments on third-party concentration hazards and residual risk acceptance.
- **The build-versus-buy decision itself.** The platform strategy document is a programme-level artefact the release-assurance owner authors.

Plus a **SR-23-4-shaped due-diligence note** for the platform vendor itself — the release-assurance programme's use of the platform is itself an SR-23-4 arrangement for a U.S. bank (or a DORA arrangement for an EU entity). The note names the arrangement, the criticality classification, the due-diligence package the programme collects, and the exit-and-portability story for the platform.

If the coverage map concludes "no platform, all in-house," Section A is replaced with a build inventory — what the release-assurance owner would need to build to cover the same surface, with an effort estimate — and Section B remains unchanged.

## Starter guidance

- **Fix the scoping first.** Which consumer-facing overlays attach is a legal call. Get the scoping right before authoring artefact content. `not-in-scope` with reasoning is legitimate; silence on an applicable overlay is a defect.
- **CFPB circulars are enforcement interpretations.** They are not regulations, but they announce how CFPB reads statute for supervised institutions. Cite the specific circular; do not paraphrase into a hard rule.
- **EEOC vendor immunity does not exist.** Employer liability under Title VII and ADA is not extinguished by vendor conduct. The `vendor-immunity-note.md` states this position and the release-package treats vendor-supplied components under the same overlay as in-house components.
- **Reasonable accommodations are workflow, not model.** The ADA reasonable-accommodation duty is discharged in the *deployment workflow around the tool*, not in the tool itself. The release-package artefact describes the workflow — who reviews requests, what alternative pathway exists, how the applicant is informed the option exists.
- **Adverse-impact analysis is not a one-time exercise.** UGESP four-fifths or a more-appropriate statistical approach must be re-run when the tool's inputs, deployment population, or upstream data changes. Note the currency window and the re-analysis trigger. Cross-reference the post-market surveillance loop.
- **Reason-code fidelity is a substantive artefact.** A reason-code catalogue plus a fidelity-evaluation deliverable is what CFPB 2023-03 asks for; a template alone is not enough. Name the derivation method (SHAP, LIME, counterfactuals), the fidelity metric, and the threshold.
- **Vendor claims are provisional.** Every vendor claim in the coverage map is `<!-- needs-research: … -->` until confirmed against the vendor's own current documentation and — ideally — against a POC or a reference customer. Do not carry vendor claims into the release-package unverified.
- **The authorship layer is non-negotiable.** A vendor platform that offers to relieve the release-assurance function of authorship is asking to become an unregulated second-line function. Refuse politely. The platform can carry the operational layer.
- **The platform vendor itself is a third-party arrangement.** The release-assurance programme's use of the platform is an SR-23-4 arrangement (or a DORA arrangement in the EU) and the release-assurance owner runs the same due-diligence shape on the platform vendor as they would run on any other critical vendor.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Consumer-facing overlays shift; vendor feature-sets shift. Marking-for-verification is the discipline.

## Acceptance criteria

You have succeeded if:

- `scenario-scoping-brief.md` fixes the AI system, the consumer-facing decision, the overlay scope (with explicit in-scope / not-in-scope determinations), the composition, the candidate platform, and the legal-counsel countersign state.
- `consumer-facing-overlay-row.md` has one row per applicable obligation, each with obligation identifier, primary source citation, obligation summary, applies-when condition (`determined_by: legal-counsel`), deliverable filename, owner role, signing role, cross-reference to anchor artefacts, post-market monitoring hook, and notes.
- Where CFPB is in scope, `adverse-action-reason-artefact.md` addresses reason-code catalogue, derivation method, fidelity evaluation, notice template, LLM-narration risk (if applicable), and cross-reference to the credit-decision explainability policy. Where out of scope, `cfpb-not-in-scope.md` records the determination.
- Where EEOC is in scope, `eeoc-analysis-set.md` (or the three sub-files) addresses ADA (three vectors), adverse-impact analysis (UGESP-shape), and vendor-immunity position. Where out of scope, `eeoc-not-in-scope.md` records the determination.
- `vendor-platform-coverage-map.md` covers Section A (coverage claims and evidence, per row) and Section B (authorship-layer boundary), plus the SR-23-4-shaped due-diligence note for the platform vendor.
- Every vendor claim is marked `<!-- needs-research: … -->` unless the exercise scenario states an explicit verification pathway.
- Every applicability determination on the overlay row is `determined_by: legal-counsel` (or a simulation-artefact caveat) with a determination date.
- Every place a fact would need to be verified against a supervisor's current guidance or a vendor's current documentation is marked `<!-- needs-research: … -->`.
- The artefact set is *consistent* — the overlay scope on the scoping brief matches which artefacts exist and which are not-in-scope files; the vendor-coverage map's authorship-layer boundary is compatible with the overlay row's owner/signing roles.
- A reviewer walking the set can see, for the system, which consumer-facing overlays attach, what the release-package discharges each with, which parts a platform vendor covers, and what the release-assurance owner still authors manually.

## Stretch goals

- **Author a HUD Fair Housing overlay artefact.** For a housing-adjacent system, sketch in `hud-fair-housing-overlay.md` the HUD-shaped analysis — disparate-impact concerns in tenant-screening or lending decisions, the deployer's affirmative-fair-housing considerations, cross-reference to the EEOC-style analysis where applicable.
- **Draft the state-law overlay stack.** For a system with multi-state exposure, produce `state-law-overlay-stack.md` — a table of applicable state laws (NYC LL 144, CO SB 24-205, IL AIVIA, CA CPRA rulemaking where applicable, others), the trigger for each, the artefact each requires, and the multi-jurisdictional posture. Cross-reference `mod-106` exercise `04`.
- **Author the vendor-selection RFP shape.** In `vendor-selection-rfp-shape.md`, sketch the RFP the release-assurance owner would issue to evaluate two or three candidate platforms — the coverage criteria, the vendor-immunity clause, the exit-and-portability requirements, the sector-template shipping list. This is what the programme's platform-strategy document is authored against.
- **Draft the platform-exit runbook.** In `platform-exit-runbook.md`, sketch the exit runbook for the candidate platform — how the release-assurance programme migrates its inventory, its evidence store, its workflow definitions, and its integration points off the platform. Untested exit runbooks are the weakest link in the SR-23-4 / DORA due-diligence chain for the platform vendor.
- **Add the LLM-narration fidelity test suite design.** For a CFPB-in-scope system that uses an LLM to narrate adverse-action reasons, sketch in `llm-narration-fidelity-suite.md` the test-suite design — how the programme validates that LLM narration does not misrepresent the underlying scoring model, the acceptance thresholds, the monitoring cadence. This is where the CFPB 2023-03 accuracy requirement meets the operational reality of generative-AI features on top of classical scoring.
- **Draft the applicant-facing accommodation notice.** For an EEOC-in-scope employment system, draft in `applicant-accommodation-notice.md` the applicant-facing text that informs applicants of the reasonable-accommodation option, the mechanism to request one, and the expected response time. The notice is a real customer-facing artefact; getting the language right is where the ADA overlay's rubber meets the road.
