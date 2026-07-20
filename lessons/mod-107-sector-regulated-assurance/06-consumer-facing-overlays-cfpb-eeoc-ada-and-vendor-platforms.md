# Consumer-Facing Overlays: CFPB, EEOC / ADA, and Vendor Platforms

## Motivation

Chapters `01`–`05` covered the sector-regulated shape from the perspective of financial supervision (SR 11-7, SR 23-4, DORA, ECB / EIOPA / ESMA) and medical-device regulation (FDA GMLP + PCCP). Two further overlays matter for a release-assurance methodology owner whenever an AI system touches U.S. consumers, and one further piece of terrain matters whenever the release-assurance function has to decide what to *build* and what to *buy*. This chapter covers all three.

The first overlay is the [**Consumer Financial Protection Bureau's Circulars series**](https://www.consumerfinance.gov/compliance/circulars/), which the CFPB uses to state its enforcement interpretations of the consumer-financial-protection statutes it administers. Circulars are not regulations, but they announce how the CFPB reads statute for supervised institutions, and they carry enforcement weight. Two circulars in particular are load-bearing for AI systems used in credit decisions: **Circular 2022-03** on adverse-action-notice requirements when creditors use complex algorithms, and **Circular 2023-03** on adverse-action-notice requirements regarding negative decisions based on inaccurate reasons. Both restate that Equal Credit Opportunity Act (ECOA, 15 U.S.C. §1691 et seq.) and Regulation B (12 CFR Part 1002) requirements to provide specific and accurate reasons for adverse action apply unchanged when the creditor uses AI/ML. <!-- needs-research: verify the current CFPB circular numbering and any subsequent circulars on AI/chatbots in consumer finance published since 2023, and confirm both circulars are still active enforcement guidance -->

The second overlay is [**Equal Employment Opportunity Commission (EEOC) guidance on AI in employment**](https://www.eeoc.gov/ai), most prominently the 2022 technical assistance document *The Americans with Disabilities Act and the Use of Software, Algorithms, and Artificial Intelligence to Assess Job Applicants and Employees* and the 2023 technical assistance document on Title VII implications of employer use of AI in selection procedures. Together they restate that ADA and Title VII apply to employer use of AI in hiring and evaluation, and that employers remain liable for discriminatory outcomes produced by AI tools they use — including tools supplied by third-party vendors. <!-- needs-research: verify current EEOC technical assistance inventory; subsequent EEOC statements on generative AI in employment may exist beyond the 2023 document -->

The third piece of terrain is the **vendor platform** landscape. The release-assurance methodology owner does not build every part of the release-gate from scratch. Vendors offering **model-risk-management platforms** (ModelOp Center), **AI governance operating systems** (Monitaur Governance OS), **model-observability and validation platforms** (Fiddler AI), and others cover parts of the SR-11-7-shaped programme. This chapter names which parts they typically cover — with vendor claims explicitly marked for verification — and where the release-assurance owner still has to author manually.

Exercise-05 asks you to draft the consumer-facing-overlay row for a release-package and map the vendor coverage against your own programme.

## The CFPB circulars — ECOA, Regulation B, and adverse-action reasons

**What the circulars say.** ECOA and Regulation B require creditors to provide applicants with statements of specific reasons for adverse action taken against them. Circular 2022-03 states that a creditor using a complex algorithm — including AI/ML — cannot rely on generic reasons; the creditor must identify the specific reasons that actually explain the adverse action for the specific applicant. Circular 2023-03 restates the accuracy requirement: reasons stated in the adverse-action notice must accurately reflect the actual reasons for the decision, and stated reasons that do not accurately reflect the decision violate ECOA and Regulation B.

Together the circulars close two loopholes creditors sometimes reach for with AI/ML models: pointing at model complexity as a reason not to give specific reasons, and giving reasons that are technically listed by the model but do not actually correspond to the adverse decision.

**Release-assurance implication.** For any consumer-credit AI system, the release-package carries an **adverse-action-reason-generation** artefact that shows *how* the system generates the reasons that will be provided to applicants, *how* those reasons are validated to accurately reflect the model's actual decision, and *how* the validation is monitored post-release. The release-gate cannot approve a T3/T4 promotion whose reason-generation validation has not been signed by the compliance function. For a system using an LLM to *narrate* reasons on top of an underlying scoring model, the release-package additionally addresses whether the LLM's narration can misrepresent the scoring model's actual reasons — an LLM-hallucination-in-adverse-action-notice risk that is directly a Circular 2023-03 concern.

The credit-decisioning assistant from chapter `01` inherits this overlay: even though it does not make the credit decision, its outputs shape the adjudicator's attention and — through the adjudicator — the eventual adverse-action reasoning. The release-assurance owner has to work with the compliance function to decide whether the assistant's outputs are themselves subject to CFPB-facing reason-generation discipline, or whether the adjudicator's own reasoning provides an independent layer that discharges ECOA on its own. That decision belongs in the release-package.

## The EEOC guidance — ADA and Title VII in AI-enabled employment decisions

**What the guidance says.** The EEOC's 2022 ADA technical assistance addresses whether employers' use of AI tools to assess job applicants and employees may violate the Americans with Disabilities Act. Three risks are foregrounded: **screening out** individuals with disabilities (the tool disqualifies applicants because of characteristics correlated with a disability), **inaccessibility** (the tool cannot be used by an applicant with a disability), and **unlawful disability-related inquiries and medical examinations** (the tool asks disability-related questions or elicits medical information without justification). Employers are responsible for these outcomes regardless of whether they built the tool themselves or bought it from a vendor.

The 2023 Title VII technical assistance addresses **disparate impact** in AI-enabled selection procedures. It restates that the Uniform Guidelines on Employee Selection Procedures apply to AI/ML-based selection tools and that employers should assess whether their tools produce a disparate impact on protected classes. Where a tool does produce a disparate impact, the employer must be prepared to show job-relatedness and business necessity.

**Release-assurance implication.** For an employment-facing AI system, the release-package carries an **ADA analysis** covering the three screening-out / inaccessibility / medical-inquiry vectors, an **adverse-impact analysis** covering the protected classes reachable in the intended-use population, and a **job-relatedness and business-necessity** justification for the residual impact where it exists. The release-gate cannot approve a T3/T4 promotion of an employment-facing AI system whose ADA and adverse-impact artefacts have not been signed by the compliance function.

The overlay applies whether or not the employer built the tool. That has direct implications for third-party arrangements: a vendor supplying an AI hiring tool cannot indemnify its customer against EEOC liability, and the release-assurance owner running the programme for the employer *deployer* has to author the overlay artefacts even for a wholly-vendored system. `mod-102`'s away-claim mechanism is one way to structure this: the deployer's assurance case has a claim about ADA compliance whose evidence includes an away-claim into the vendor's documentation, but the deployer's case is where the release-gate closes.

### Reasonable accommodations and the human-in-the-loop question

The ADA imposes a duty to provide reasonable accommodations to qualified individuals with disabilities. For AI-enabled hiring tools, the release-assurance owner has to think through the reasonable-accommodation loop concretely: what does the applicant see if they request an accommodation? Is there an alternative assessment pathway that does not use the AI tool? Who reviews the request? How does the applicant know the option exists? These are not questions the AI tool answers on its own; they are questions the *deployment* around the tool has to answer, and the release-package documents the answers.

Similarly, the Title VII adverse-impact analysis is not a one-time exercise. Where the AI tool's inputs, deployment population, or upstream data changes, the adverse-impact analysis must be re-run, and the release-gate's revalidation cadence has to acknowledge this. The post-market surveillance loop (`mod-110`) carries the periodic re-evaluation as a scheduled activity.

## Related consumer-facing overlays worth naming

Two further overlays that show up in adjacent contexts and that the release-assurance owner has to track when applicable:

- **CFPB Circular 2022-06** on unfair and deceptive acts or practices (UDAAP) in connection with the use of consumer data. Applies broadly, including to AI systems that use consumer data.
- **HUD Fair Housing Act guidance** on the use of algorithmic tools in housing decisions. Applies to housing-facing AI systems. <!-- needs-research: verify current HUD guidance on algorithmic tools in tenant screening and housing decisions, particularly since 2023 -->
- **State-level laws** on AI in employment (New York City Local Law 144 on automated employment decision tools; Illinois Artificial Intelligence Video Interview Act; Colorado SB 24-205 on high-risk AI). State laws are moving fast; the release-assurance owner tracks them via the same watch-list process from chapter `05`. <!-- needs-research: verify current inventory and effective dates of U.S. state-level AI-in-employment and AI-in-consumer laws; the landscape at time of writing includes NYC LL 144, IL AIVIA, and CO SB 24-205 but is expanding -->

Consumer-facing overlays are one of the areas where the *watch-list process* (chapter `05`) most directly interfaces with release-package templates: new circulars and new state laws land often, and each one is a candidate template update.

## Vendor platforms and where they cover the sector-regulated shape

The release-assurance methodology owner does not build every part of the release-gate from scratch. Several vendors offer platforms that cover parts of the SR-11-7-shaped programme. This section names three commonly-cited ones with the caveat that vendor features change often — every claim here is marked for verification against the vendor's own current documentation before being cited in a release-package.

### ModelOp Center

[**ModelOp Center**](https://www.modelop.com/) is a model operations and governance platform positioned as a solution for enterprise MRM programmes. Its typical coverage claims include a **model inventory** with lineage; **workflow orchestration** for model-onboarding, validation, and monitoring; **documentation generation** aligned with SR 11-7 expectations; and integrations with third-party model registries and monitoring tools. <!-- needs-research: verify current feature coverage in ModelOp Center's latest release, particularly the AI/ML-specific features (foundation-model tracking, prompt-versioning, judge-model management) and the SR-11-7-templated document generation -->

**Where the release-assurance owner still authors manually.** The release-gate *criteria* — the hard/soft classification, the framework citations, the sector-rule pointers — remain the release-assurance owner's authorship. Vendor workflow orchestration executes the criteria; it does not decide them. Effective-challenge decisions (approvals of MRM validation, dispositions of soft-gate failures) remain human decisions the platform records but does not replace. Foundation-model-specific evidence (vendor-side signals, silent-update detection, PCCP-style change-control for AI-only components) may or may not fit the platform's native workflow; where it does not, the release-assurance owner authors external evidence collection and threads it into the platform's inventory.

### Monitaur Governance OS

[**Monitaur**](https://www.monitaur.ai/) positions its Governance OS as an AI-specific governance platform, with coverage claims including a **governance workflow** with sign-offs, an **evidence repository** with an audit trail, **model / dataset / system documentation** templates, and **cross-framework mapping** onto NIST AI RMF, ISO/IEC 42001, and EU AI Act clauses. <!-- needs-research: verify current Monitaur Governance OS features, especially the sector-specific extensions (SR 11-7 / DORA / FDA GMLP templates) and the release-gate orchestration surface -->

**Where the release-assurance owner still authors manually.** The template shapes the platform ships with — for cards, for policies, for cross-framework maps — need to be *tailored* to the entity's own regulatory footprint and the release-assurance methodology's own vocabulary. Sector-specific extensions (SR 11-7 tiering matched to the entity's MRM policy; DORA register-of-information entries aligned with the entity's own register-of-information; PCCP components for a medical-device entity) require the release-assurance owner to author the entity-specific content that the templates hold.

### Fiddler AI

[**Fiddler AI**](https://www.fiddler.ai/) positions its platform as **model observability and monitoring**, with coverage claims including **drift monitoring**, **explainability** (attribution methods for tabular and text models), **performance monitoring** in production, and **fairness monitoring** across subgroups. <!-- needs-research: verify current Fiddler AI feature coverage, particularly for LLM-specific monitoring surfaces (hallucination detection, prompt-injection detection, judge-model integration) and for the sector-regulated documentation expectations (SR 11-7 on-going-monitoring report generation) -->

**Where the release-assurance owner still authors manually.** Observability platforms produce *data* the release-gate consumes; they do not produce the *disposition* of that data. The release-assurance owner authors: the monitoring plan (what is monitored, how often, at what thresholds, with what escalation), the on-going-monitoring report template, the connection between monitoring signals and the release-gate reversal contract, and — most importantly — the interpretation that a monitoring anomaly is or is not a release-gate concern. Vendor dashboards are inputs into that authorship, not substitutes for it.

### The general shape of vendor coverage

A useful way to think about all three platforms — and any others in the same space — is that they typically cover the **operational layer** of the sector-regulated programme (inventory, workflow, evidence storage, monitoring signals, cross-framework mapping) and leave the **authorship layer** to the release-assurance methodology owner (criterion selection, disposition, sector-rule interpretation, effective-challenge decisions). A vendor that promises to cover the authorship layer is either overselling or asking to become the accountable second-line function, neither of which is what the release-assurance owner should agree to.

The evaluation shape for any such platform is:

- What does the vendor claim to cover, verified against the vendor's own current documentation?
- What is *load-bearing* in a release-package that the platform would need to hold, and what is left over that the release-assurance owner still authors?
- What are the platform's own third-party arrangements (chapters `02`, `04`), and how does the release-assurance programme's use of the platform fit into SR 23-4 / DORA due-diligence for the entity?
- What is the platform's exit-and-portability story, and how does the release-package's evidence integrity survive a platform switch?

That evaluation shape is the assurance-programme sibling of the SR-23-4 due-diligence package from chapter `02` — the release-assurance owner runs it on the vendors that support the release-assurance programme itself.

## Worked shape — a hiring-decision AI at a mid-sized U.S. employer

Take a concrete system: a **hiring-decision AI** at a mid-sized U.S. employer, used to screen applicant CVs and generate a shortlist for human recruiters to review. It uses a vendor-supplied resume-screening model plus an in-house re-ranker tuned to the employer's own hiring history. It touches all three overlays covered in this chapter.

Plugged into the consumer-facing overlays and the vendor landscape:

- **EEOC / ADA overlay**: ADA analysis covering the three vectors (screening-out, inaccessibility, medical-inquiry) at the applicant-experience level and at the model-behaviour level; adverse-impact analysis across race, sex, age, disability, and national origin (as reasonably practicable given data availability); job-relatedness and business-necessity justification for the residual impact; connection to the employer's own EEO-1 reporting.
- **State-law overlay**: NYC Local Law 144 bias-audit and applicant-notice compliance for any NYC applicant; similar tracking for other applicable state laws via the watch-list.
- **Vendor overlay**: the vendor-supplied resume-screening model treated under SR-23-4-shaped due diligence (chapter `02`), even though the entity is not a bank — the shape works for any critical third-party AI arrangement; the vendor's own bias-audit and technical documentation collected as part of the release-package.
- **Vendor platform**: the entity uses ModelOp Center (or a similar platform) for inventory and workflow; the release-assurance owner authored the sector-specific templates that the platform holds; observability monitoring feeds from the platform's monitoring integrations into the release-gate reversal contract.
- **Release-gate criteria**: EEOC and ADA artefacts signed; state-law-compliance memo current; vendor-package current; adverse-impact analysis within currency window; job-relatedness and business-necessity justification signed by counsel.

That is a consumer-facing-overlay release-package for a hiring-decision AI. Exercise-05 asks you to author the consumer-facing-overlay row for a system of your own choosing and to map the vendor-platform coverage against your programme.

## The build-versus-buy decision as a programme-level artefact

Every release-assurance programme sooner or later confronts the build-versus-buy question at platform altitude: build our own inventory-and-workflow layer, or buy one; build our own evidence-repository layer, or buy one; build our own monitoring layer, or buy one. The decision is not purely economic. It is also a *supervisory-defensibility* decision: a vendor platform whose feature-set aligns to SR 11-7 (or DORA, or FDA GMLP) lowers the burden of demonstrating that the programme is systematic; a bespoke implementation lowers the risk of vendor lock-in and gives the release-assurance owner precise control over every criterion, but requires the owner to author every template from scratch.

The build-versus-buy decision itself is a programme-level artefact. The release-assurance methodology owner authors a **platform strategy** document that captures the current state of the buy versus build split, the rationale for each choice, the exit plan for each vendored component, and the review cadence. The document is a management-review agenda item (`mod-112`) and is refreshed on the same annual cadence as the release-assurance methodology itself.

The one thing to avoid: outsourcing the *methodology* itself to a vendor. A vendor platform can carry the operational layer; it cannot carry the accountable-second-line function's authorship. Where a vendor pitch offers to relieve the release-assurance function of authorship, the release-assurance owner refuses politely — the vendor is asking to become an unregulated intermediary between the entity and its supervisor, and no supervisor will accept that arrangement at inspection.

## Where this shows up in the rest of the track

- `mod-101` — the consumer-facing overlays sit inside GOVERN-1 (organisational policies) and MEASURE-2.11 (fairness with harmful bias managed) of NIST AI RMF; the vendor-platform terrain sits inside GOVERN-6 (third-party governance).
- `mod-102` — the assurance case for a consumer-facing AI system carries a consumer-overlay branch alongside its other framework branches; away-claims to vendor documentation are the standard mechanism for the vendor-supplied components.
- `mod-104` — the evidence pipeline carries adverse-action reason-generation artefacts, ADA analyses, adverse-impact analyses, and vendor bias-audit outputs as first-class artefact types.
- `mod-105` — the applicant-facing and consumer-facing transparency artefacts (adverse-action notices, applicant notices under state law) are cards of a specific kind.
- `mod-108` — deployment-tier gating for consumer-facing systems uses the applicable-consumer-overlay set as one of its tier inputs.
- `mod-109` — third-party auditors performing bias audits (e.g. under NYC LL 144) interface through `mod-109`.
- `mod-110` — post-market surveillance for consumer-facing systems includes complaint-monitoring and adverse-impact-drift monitoring; the CFPB accuracy circular fires on any evidence that stated adverse-action reasons drift from the model's actual reasoning.
- `mod-112` — the choice of vendor platform is itself a release-assurance-programme decision that management review revisits on a stated cadence.

## Summary

- CFPB Circulars 2022-03 and 2023-03 restate that ECOA and Regulation B adverse-action-notice requirements apply unchanged to creditors using AI/ML: specific reasons are required, and stated reasons must accurately reflect the actual reasons for the decision.
- EEOC 2022 (ADA) and 2023 (Title VII) technical-assistance documents restate that employer use of AI in hiring and evaluation is subject to ADA and Title VII, with three screening-out / inaccessibility / medical-inquiry vectors and a disparate-impact analysis expected.
- Related U.S. state-level laws (NYC LL 144, IL AIVIA, CO SB 24-205 and others) add further consumer-facing requirements; the release-assurance owner tracks them via the watch-list process from chapter `05`.
- Vendor platforms (ModelOp Center, Monitaur Governance OS, Fiddler AI, and others) cover the **operational layer** of the sector-regulated programme (inventory, workflow, evidence storage, monitoring, cross-framework mapping) and leave the **authorship layer** (criterion selection, disposition, sector-rule interpretation, effective-challenge decisions) to the release-assurance owner.
- Vendor feature claims are marked `<!-- needs-research: ... -->` and verified against the vendor's own current documentation before being cited in a release-package; the vendor itself is evaluated under SR-23-4-shaped due diligence for its role in supporting the assurance programme.
- Exercise-05 asks you to author the consumer-facing-overlay row for a release-package and to map vendor-platform coverage against your programme.
