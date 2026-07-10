# US State and City Overlay — Colorado, NYC, CFPB, EEOC

## Motivation

The United States has no horizontal federal AI regulation in 2026. What it has instead is a patchwork of state-level statutes, city-level rules, and sector-specific federal agency guidance, layered on top of long-standing anti-discrimination and consumer-protection law. For a release-assurance program, this means: even a US-only system without EU exposure faces a *stack* of obligations that the release-gate has to enumerate.

This chapter overlays four US-side instruments onto the anchor map:

- **Colorado Artificial Intelligence Act (SB24-205)** — the first US comprehensive AI statute imposing obligations on developers and deployers of "high-risk" AI systems. Signed 2024; effective 2026.
- **New York City Local Law 144 (AEDT)** — the automated employment-decision-tool rule requiring an independent bias audit before use.
- **CFPB adverse-action-notice circulars** — the Consumer Financial Protection Bureau's guidance that ECOA / Regulation B adverse-action-notice obligations apply to credit decisions made with AI, no "black box" exception.
- **EEOC AI / ADA guidance** — the Equal Employment Opportunity Commission's guidance on AI selection tools under Title VII and on AI accommodation under the ADA.

Sector-specific US federal instruments (SR 11-7 / OCC 2011-12 / SR 23-4 for banking, FDA GMLP / PCCP for medical devices) are covered in `mod-107` (sector-regulated assurance), not here. This chapter is the "civil-rights and consumer-protection" overlay.

## The instruments in one paragraph each

### Colorado AI Act — SB24-205 (Consumer Protections for Artificial Intelligence)

Colorado SB24-205 was signed by Governor Polis in May 2024 and, as enacted, takes effect on 2026-02-01. `<!-- needs-research: confirm the effective date has not been amended by a subsequent Colorado session -->`. It imposes obligations on both *developers* (who develop or intentionally and substantially modify a "high-risk artificial intelligence system") and *deployers* (who deploy one) of high-risk AI systems, where "high-risk" is defined (broadly) as any AI system that makes, or is a substantial factor in making, a *consequential decision* — education, employment, financial or lending services, essential government services, healthcare, housing, insurance, or legal services.

Key obligation shapes:

- Developer duty of reasonable care to protect consumers from known or reasonably foreseeable risks of algorithmic discrimination.
- Statement disclosing high-risk purpose, foreseeable uses, known limitations, discrimination-risk mitigation measures, data used to train, evaluation done, and post-deployment monitoring — provided to deployers.
- Deployer duty of reasonable care to protect consumers from algorithmic discrimination, including a risk-management policy and program, an impact assessment (annual and after intentional and substantial modification), and consumer notice.
- Consumer notice before a high-risk system is used to make (or is a substantial factor in making) a consequential decision that is adverse to the consumer, and an opportunity to appeal / seek human review.
- Discovery-and-disclosure obligation to the Colorado Attorney General for algorithmic discrimination detected via post-deployment monitoring.
- Attorney General enforcement; no private right of action.

### NYC Local Law 144 — Automated Employment Decision Tools (AEDT)

NYC Local Law 144 (effective 2023-07-05 with enforcement) prohibits use of an automated employment decision tool (AEDT) unless (a) a **bias audit** has been conducted by an independent auditor within one year prior to use, (b) a summary of the results has been publicly published, and (c) candidates and employees receive notice at least 10 business days before use.

The bias audit computes selection-rate impact ratios per category (sex; race/ethnicity; and intersectional sex × race/ethnicity groupings) against historical or test data, and reports them.

Owner: the *employer* using the tool bears the audit obligation. A vendor providing the tool may commission the audit and republish it, but it does not by itself absolve the employer.

Enforcement: NYC Department of Consumer and Worker Protection (DCWP), with civil penalties per violation.

### CFPB adverse-action-notice circulars

The CFPB has issued circulars — notably **2022-03** (adverse action notification requirements in connection with credit decisions based on complex algorithms) and **2023-03** (adverse-action-notice requirements when relying on AI or complex predictive models) — clarifying that ECOA (Equal Credit Opportunity Act) and Regulation B require **specific and accurate** reasons for adverse credit action, and that a lender cannot avoid these obligations by using a model too complex to explain. The specific reasons must be substantive; canned language ("credit score too low") is inadequate.

Owner: the *creditor* making the adverse decision; the model provider is a supplier under third-party risk-management (SR 23-4).

`<!-- needs-research: confirm current CFPB circular numbers; CFPB has issued additional related guidance since 2023 — refresh the citations to whatever is current at authoring time -->`

### EEOC AI / ADA guidance

The EEOC has issued two principal AI-adjacent guidance documents:

- **Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence Used in Employment Selection Procedures Under Title VII of the Civil Rights Act of 1964** (May 2023) — clarifying that AI-based selection procedures are subject to the Uniform Guidelines on Employee Selection Procedures four-fifths rule adverse-impact analysis, and that vendor conduct does not immunise the employer.
- **The Americans with Disabilities Act and the Use of Software, Algorithms, and AI to Assess Job Applicants and Employees** (May 2022) — clarifying that AI selection tools may violate the ADA if they screen out disabled candidates who could perform the essential functions with reasonable accommodation, or if they are administered without offering reasonable accommodation.

Owner: the *employer*.

`<!-- needs-research: EEOC may have issued additional Technical Assistance Documents since 2023 — refresh with current listing on eeoc.gov -->`

## Adding US-side rows to the map

Each of these instruments generates its own rows on the map. Where an obligation is *also* covered by an EU AI Act row (many are — Colorado's risk-management program obligation echoes EU AI Act Article 9), the US row cross-references the EU row rather than duplicating the deliverable.

### Colorado SB24-205 rows

| Row | Obligation summary | Applies to | Deliverable | Owner |
| --- | --- | --- | --- | --- |
| `co-sb24-205.developer.reasonable-care` | Developer reasonable care against algorithmic discrimination | developer of high-risk AI | cross-ref to `eu-ai-act.art9.plan` + `co-developer-care-statement.md` | this role |
| `co-sb24-205.developer.disclosure-statement` | Statement to deployer (purpose, uses, limits, discrimination-risk mitigations, data, evaluation, monitoring) | developer of high-risk AI | `co-developer-statement-to-deployer-v<N>.md` | this role |
| `co-sb24-205.deployer.risk-management-program` | Deployer risk-management policy and program | deployer of high-risk AI | cross-ref to `eu-ai-act.art9.plan` + `co-deployer-rm-program.md` | this role |
| `co-sb24-205.deployer.impact-assessment` | Annual + on-substantial-modification impact assessment | deployer of high-risk AI | `co-deployer-impact-assessment-v<N>.md` (cross-ref to `iso/42005` shape) | this role |
| `co-sb24-205.deployer.consumer-notice` | Notice to consumer before an adverse consequential decision | deployer of high-risk AI | `co-consumer-notice-template.md`, `co-appeal-mechanism-spec.md` | this role + product + legal |
| `co-sb24-205.deployer.consumer-appeal` | Opportunity for human review of adverse decision | deployer of high-risk AI | `co-appeal-mechanism-spec.md` | product + this role |
| `co-sb24-205.deployer.ag-disclosure` | Disclosure to Colorado AG on detected algorithmic discrimination | deployer of high-risk AI | `co-ag-disclosure-procedure.md` | legal + this role |

**Trap: "consequential decision" ≠ EU AI Act "high-risk."** The lists overlap heavily (employment, housing, financial, healthcare, essential government services) but not perfectly. A system may be in-scope of one and not the other. The map records the classification per instrument.

**Trap: developer *and* deployer.** Where the organisation both develops and deploys, both row sets apply. The developer-facing disclosure statement is delivered to the deployer's release-gate (even if internal) — the audit trail must show the handoff.

**Trap: "substantial factor."** Colorado's definition of what counts as an AI system being a "substantial factor" in a consequential decision is legal-interpretive. Legal counsel signs off on the applicability determination.

### NYC Local Law 144 rows

| Row | Obligation summary | Applies to | Deliverable | Owner |
| --- | --- | --- | --- | --- |
| `nyc-ll-144.bias-audit` | Independent bias audit within one year prior to use | employer using AEDT for hiring / promotion decisions of NYC-based employees / candidates | `nyc-ll-144-bias-audit-report-<audit-date>.pdf` (from independent auditor) | independent auditor; this role coordinates |
| `nyc-ll-144.bias-audit-summary` | Publicly published summary of audit results | employer | `nyc-ll-144-public-summary.md` (posted at deployer URL) | this role + comms |
| `nyc-ll-144.notice` | ≥10 business day notice to candidates and employees | employer | `nyc-ll-144-notice-template.md` (integrated into ATS / HR system) | HR + this role |
| `nyc-ll-144.reasonable-accommodation-notice` | Notice of alternative selection process or reasonable accommodation | employer | `nyc-ll-144-accommodation-notice.md` | HR + legal |
| `nyc-ll-144.retention` | Retention of audit and notice records | employer | `nyc-ll-144-record-retention-policy.yaml` | HR + this role |

**Trap: independence.** The auditor "shall not have been involved in using, developing, or distributing the AEDT" and must have no financial interest in the tool. If the organisation attempts to satisfy the audit with an in-house team, the audit is not compliant. The map's `owner_role` for the audit report is *external* — this role coordinates the engagement (`mod-109` third-party interface) but does not produce the audit.

**Trap: employment scope.** LL 144 covers hiring and promotion of candidates or employees within NYC (or where the employment position is located in NYC, or in some interpretations where a candidate resides in NYC). A US-national deployment triggers LL 144 rows for the NYC subset.

**Trap: coverage vs. category.** The audit reports impact ratios per specified category. Categories are drawn from EEO-1 reporting. The map should carry a sub-row per category to make coverage explicit.

### CFPB adverse-action-notice rows

Applies when the system contributes to a credit decision under ECOA / Regulation B.

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `cfpb-adverse-action.specific-reasons` | Adverse-action notices state specific and accurate reasons | `cfpb-adverse-action-notice-template.md`, `reason-code-catalogue.yaml` | product + legal + this role |
| `cfpb-adverse-action.reason-code-derivation` | Reason codes derived from the model's actual decision drivers, not proxies | `reason-code-derivation-methodology.md`, evaluated evidence of fidelity | `model-evaluation-engineer` + this role |
| `cfpb-adverse-action.reason-code-fidelity-report` | Evidence the reason codes match model behaviour | `reason-code-fidelity-report-v<N>.md` | `model-evaluation-engineer` |
| `cfpb-adverse-action.no-black-box-defence` | Programme stance that model complexity does not excuse the obligation | `credit-decision-explainability-policy.md` | legal + this role |

**Trap: "specific and accurate."** Reason codes drawn from a fixed vendor list that do not correspond to the model's actual decision drivers are inadequate. The map's `reason-code-fidelity-report` is not decorative — it is the evidence that keeps the row green.

**Trap: cross-tag to EU AI Act.** ECOA-shape adverse-action-notice obligations are *not* mirrored in the EU AI Act (which does not have a US-federal-analog credit statute); the row is US-side only. It does, however, cross-tag to NIST AI RMF MEASURE-2.8 (transparency and accountability) and to ISO/IEC 42001 clause 7.4 (communication) — those siblings hold.

### EEOC AI / ADA rows

Applies when the system is used for employment selection or accommodation-relevant employment decisions.

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `eeoc.title-vii.adverse-impact` | Four-fifths rule adverse-impact analysis under UGESP | `eeoc-adverse-impact-report-v<N>.md` (from `ai-risk-engineer` + `model-evaluation-engineer`) | `ai-risk-engineer` |
| `eeoc.title-vii.validation` | Job-relatedness / business-necessity validation | `eeoc-validation-study-v<N>.md` | I/O psychologist (external or internal) + this role |
| `eeoc.ada.screen-out-analysis` | Analysis of whether tool screens out disabled candidates | `eeoc-ada-screen-out-analysis-v<N>.md` | `ai-risk-engineer` + accessibility specialist |
| `eeoc.ada.accommodation-procedure` | Procedure to offer reasonable accommodation | `eeoc-ada-accommodation-procedure.md` | HR + legal |
| `eeoc.vendor-immunity-stance` | Position that vendor conduct does not immunise employer | `eeoc-vendor-immunity-policy.md` | legal + this role |

**Trap: UGESP is federal.** EEOC guidance sits under the Uniform Guidelines on Employee Selection Procedures (1978). The four-fifths rule is one heuristic, not the only inference; the map should carry the actual selection-rate ratios and the validation study, not just a pass/fail on the ratio.

**Trap: ADA screen-out is about capability, not about disability status.** The analysis is whether a disabled person capable of performing essential functions with reasonable accommodation is screened out — not whether disability is inferred by the model.

## Cross-references back to the EU AI Act anchor

The overlay is not additive independently: many US rows share deliverables with EU AI Act rows, and the map should show the shared deliverable, not two copies. The frequent cross-references:

- Colorado SB24-205 developer/deployer risk-management → shares `eu-ai-act.art9.plan` and `eu-ai-act.art9.harms`
- Colorado SB24-205 deployer impact assessment → shares the ISO/IEC 42005 impact-assessment deliverable (cross-ref to `eu-ai-act.art9.impact-assessment`)
- Colorado SB24-205 developer disclosure statement → shares the deployer-facing card (cross-ref to `eu-ai-act.art13.deployer-card`), but Colorado's specific-content list (data used, evaluation done, discrimination-risk mitigations) needs to be verified against Article 13's content list
- NYC LL 144 bias audit → *does not* share with the EU AI Act Article 10 bias-and-shortcoming report. The LL 144 audit has a fixed methodology (impact ratios per category); the EU report is broader. Both are required.
- CFPB adverse-action notices → *do not* share with any EU AI Act row. Article 13 instructions-for-use go to the *deployer*, not the consumer; CFPB notices go to the *consumer*.
- EEOC adverse-impact → partially shares with EU AI Act Article 10 bias-and-shortcoming report (methodology), but the categories are different (EEO-1 vs. Article 10's less-prescribed list). The map should carry both.

## Where the overlay adds genuinely new obligations

Rows the EU AI Act does not cover and that must be added independently:

- **Consumer-facing notice and appeal (Colorado SB24-205, Article 27 of the EU Act *partially* mirrors this for public-authority deployers under FRIA — check applicability).** The consumer-facing route in the EU is closer to GDPR Article 22 automated-decision rights than to a specific AI Act obligation.
- **AG disclosure of detected algorithmic discrimination (Colorado SB24-205).** No EU AI Act equivalent — Article 61 covers *serious incidents* but not routine discrimination disclosure.
- **NYC bias audit's fixed impact-ratio methodology.** The EU AI Act does not specify a categorical impact-ratio audit; Article 10 bias review is method-flexible.
- **CFPB specific-reason adverse-action notice.** Fully US-side.
- **UGESP four-fifths adverse-impact.** Partially overlaps EU AI Act Article 10 but the methodology is specific to UGESP.
- **EEOC ADA reasonable-accommodation procedure.** No EU AI Act analogue; the closest is Article 14 human-oversight-as-mitigation.

## Enforcement mismatches worth flagging

- **Colorado** — enforced by the AG only, no private right of action. Damages accumulate but do not go to the plaintiff.
- **NYC LL 144** — DCWP with civil penalties per violation; each candidate an employer used an AEDT on without audit is a separate violation.
- **CFPB** — the CFPB acts under ECOA; state attorneys general and private plaintiffs also have ECOA authority. A CFPB circular is not itself binding — but the underlying ECOA / Regulation B *is*.
- **EEOC** — Title VII / ADA private rights of action; EEOC enforcement typically under a Notice of Right to Sue.

Enforcement asymmetry matters because the *residual-risk register* posture per row differs: a Colorado residual is a regulator-facing exposure; an EEOC residual is a private-litigation exposure. Legal counsel will read these rows differently and sign accordingly.

## Where this shows up in the rest of the track

- `mod-105` (cards for external audiences) — the Colorado disclosure statement is a specific card variant; the NYC public bias-audit summary is a distinct publication.
- `mod-107` (sector-regulated assurance) — CFPB rows compose with SR 11-7 model-risk rows for a bank running a credit model.
- `mod-108` (deployment-tier gating) — a US-only deployment tier may drop the EU AI Act rows and elevate the Colorado / NYC / CFPB / EEOC rows.
- `mod-109` (third-party evaluator interface) — the NYC LL 144 independent auditor is one shape of third-party evaluator, distinct from an EU notified body.
- `mod-110` (post-market surveillance) — Colorado's AG-disclosure procedure is a specific post-market artefact.

## Summary

- The US-side overlay adds four instruments to the map: Colorado SB24-205 (comprehensive state statute), NYC Local Law 144 (city-level bias-audit rule for hiring), CFPB adverse-action-notice circulars (federal credit adverse-action clarification), and EEOC AI / ADA guidance (federal employment civil-rights guidance).
- Many rows share deliverables with EU AI Act rows and are recorded as cross-references, not duplicates.
- Genuinely new rows: consumer notice + appeal (Colorado), AG disclosure (Colorado), fixed-methodology bias audit (NYC), specific-reason adverse-action notice (CFPB), UGESP four-fifths analysis (EEOC), ADA screen-out and reasonable-accommodation procedure (EEOC).
- Enforcement asymmetries change how residual-risk posture is written per row: AG-only enforcement (Colorado), city civil penalty (NYC), private litigation risk (EEOC / ECOA).
- Sector-specific US federal instruments (SR 11-7, FDA GMLP) are covered in `mod-107`, not here.
- Exercise 04 walks a US-scoped scenario through the overlay row-by-row.
