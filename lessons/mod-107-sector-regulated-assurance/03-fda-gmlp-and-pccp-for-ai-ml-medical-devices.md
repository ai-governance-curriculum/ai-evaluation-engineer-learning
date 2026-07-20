# FDA GMLP and PCCP for AI/ML Medical Devices

## Motivation

Chapters `01` and `02` gave the U.S. banking sector shape. Move the release-assurance methodology owner into a medical-device manufacturer — for example, a company shipping a Software-as-a-Medical-Device (SaMD) triage assistant used by clinicians in an emergency-department workflow — and the ground under the release-gate changes again. The anchor is neither NIST AI RMF nor SR 11-7. It is the **U.S. Food and Drug Administration's** regulatory shape for AI/ML-enabled device software functions, articulated across three connected instruments.

The first is the [**Good Machine Learning Practice for Medical Device Development: Guiding Principles**](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles), a set of 10 principles jointly published in October 2021 by FDA, Health Canada, and the UK Medicines and Healthcare products Regulatory Agency (MHRA). GMLP is not a regulation. It is a *baseline of good practice* the three regulators agree on, and it functions as the quality shape a submission is expected to demonstrate against — the way ISO/IEC 42001 functions as a management-system shape for enterprise AI governance.

The second is the [**Predetermined Change Control Plans (PCCP) for Artificial Intelligence-Enabled Device Software Functions**](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions) final guidance, issued by FDA in December 2024. PCCP is a mechanism — authorised in statute by the FD&C Act §515C added by the Food and Drug Omnibus Reform Act of 2022 — that lets a manufacturer *pre-authorise* specified post-market modifications to an AI/ML-enabled device at the time of initial marketing authorisation, so that those modifications can be implemented without a new premarket submission.

The third is the older device-specific literature (510(k), De Novo, PMA pathways; the [SaMD framework](https://www.fda.gov/medical-devices/software-medical-device-samd) developed originally by IMDRF) that GMLP and PCCP sit inside. This chapter does not re-cover those pathways — the release-assurance owner joining a medical-device team is expected to have that literature from the regulatory-affairs colleagues. It focuses on the two AI/ML-specific instruments: what they say, how they wire into a release-gate, and how PCCP interacts with the assurance loop over the device's lifecycle. Exercise-02 asks you to draft a GMLP-plus-PCCP-shaped submission for one SaMD scenario.

## The 10 GMLP guiding principles

The 10 principles are short — a title and a paragraph each on the FDA page. They are worth reading in their canonical form; here they are paraphrased in the shape the release-assurance owner uses them, grouped by lifecycle phase.

### Multidisciplinary expertise and design (principles 1, 2, 3)

**Principle 1 — Multi-disciplinary expertise is leveraged throughout the total product life cycle.** The team combines domain (clinical), data, engineering, and post-market-surveillance expertise, and the interfaces between them are documented.

**Principle 2 — Good software engineering and security practices are implemented.** Standard software-engineering discipline (requirements, design, verification, cybersecurity) applies without exception; the ML content does not lower the software-engineering bar.

**Principle 3 — Clinical study participants and data sets are representative of the intended patient population.** Data sourcing, sampling, and representativeness are documented, and coverage of subgroups relevant to the intended use is evaluated. Non-representative data is a design defect, not a downstream fairness footnote.

**Release-assurance implication.** These three principles set the *conceptual soundness* of the submission and map cleanly to EU AI Act Article 10 (data governance) and NIST AI RMF MAP-4 (risks and benefits mapped across components). The release-package carries the multidisciplinary-team roster, the software-engineering and cybersecurity plan (with references to [IEC 62304](https://www.iec.ch/) and [IEC 81001-5-1](https://www.iec.ch/) where relevant), and the intended-population and dataset-representativeness memo.

### Development discipline (principles 4, 5, 6, 7)

**Principle 4 — Training data sets are independent of test sets.** Training / validation / test disjointness is verified and documented, including for any subsequent retraining. This is the classical ML-hygiene principle, restated as a submission expectation.

**Principle 5 — Selected reference datasets are based upon best available methods.** Where reference sets exist for the clinical task, they are used and named. Where none exists, the manufacturer documents how their reference set was constructed and why.

**Principle 6 — Model design is tailored to the available data and reflects the intended use of the device.** The model architecture and complexity match the data volume and the clinical decision the device supports. Over-parameterised models on thin data are called out.

**Principle 7 — Focus is placed on the performance of the human-AI team.** The performance metric that matters is the clinician-plus-device performance, not the device's stand-alone accuracy. Usability, automation bias, and workflow effects are evaluated.

**Release-assurance implication.** These four principles are the development-and-testing evidence set. Principle 4 anchors the evaluation-set-integrity discipline (chapter `01` stress point) in submission language. Principle 7 anchors human-oversight evidence in a *joint-performance* metric that maps to EU AI Act Article 14 (human oversight) and to the release-gate's usability criteria.

### Validation and monitoring (principles 8, 9, 10)

**Principle 8 — Testing demonstrates device performance during clinically relevant conditions.** Validation is designed to reflect the environment of use, not just the training environment; edge cases, hardware variability, and workflow variability are exercised.

**Principle 9 — Users are provided clear, essential information.** Labelling and instructions-for-use are precise about intended use, contraindications, performance characteristics on the intended population and on relevant subgroups, and known limitations. This is the FDA-specific sibling of EU AI Act Article 13 (transparency).

**Principle 10 — Deployed models are monitored for performance and re-training risks are managed.** Post-market monitoring is designed, documented, and executed; retraining — if it happens — is managed under a change-control plan. Principle 10 is what PCCP operationalises.

**Release-assurance implication.** Principles 8–10 map onto the validation report, the labelling and instructions-for-use draft, and the post-market plan — all first-class artefacts in the release-package. Principle 10 is the joint into the PCCP guidance below.

## What PCCP is, and why it matters

Before PCCP, an AI/ML-enabled device that a manufacturer wanted to update after market authorisation typically had to submit a new 510(k) (or comparable) whenever the update crossed the FDA's *significant change* threshold. For a locked model, updates were infrequent enough that this was tolerable. For an AI/ML-enabled device whose value proposition includes iterative improvement — retraining on new data, adapting to shifting clinical patterns, adding new operating points — the classical submission cycle was a persistent friction.

PCCP addresses this by letting the manufacturer *pre-specify* the modifications the device will undergo, *pre-specify* the process for making them safely, and get all of it authorised at the time of the initial marketing submission. Once authorised, modifications that fit within the PCCP can be implemented without a new premarket submission — the device is still considered to be operating within its authorised state.

Three ideas anchor PCCP:

- **The device remains "locked" in the FDA sense.** PCCP is not a mechanism for continuous learning or on-device adaptation. The device version deployed to a patient is a specific, identifiable version; updates happen through a controlled release process the manufacturer runs. What PCCP changes is the *administrative* process for authorising updates, not the *technical* nature of the device.
- **PCCP has three required components.** A **Description of Modifications** (what changes are pre-authorised, precisely enumerated), a **Modification Protocol** (the methods used to develop, validate, and implement each modification, with the verification-and-validation activities and the labelling updates specified), and an **Impact Assessment** (analysis of how the pre-authorised modifications, individually and jointly, may affect the device's safety and effectiveness, and the mitigations in place). All three are reviewed as part of the initial marketing authorisation.
- **PCCP is scoped and specific.** A PCCP covers *specific* modification types (for example: retraining the model on additional data from the same population; adding a new operating point on a specified curve; updating a specific input-preprocessing step). Modifications outside the PCCP scope still require a new submission. The bounding of scope is what makes PCCP tractable for the reviewer and defensible for the manufacturer.

### The three components in the release-package

For the release-assurance owner, PCCP shows up as three concrete artefacts in the release-package, each with its own release-gate criteria.

- **Description of Modifications.** A tabulated set of pre-authorised change types, with the *triggers* under which each may be exercised (e.g. "retraining is triggered when the monitoring plan detects performance drift exceeding threshold X on the intended population"), the *bounds* on each (e.g. "retraining uses only data from sites of type Y, restricted to the intended population, and produces a model whose evaluation on the reference set does not fall below threshold Z"), and the *notification* the manufacturer commits to make when the modification is exercised.
- **Modification Protocol.** The end-to-end method for each pre-authorised change: data-management plan (sourcing, quality checks, disjointness with the reference test set), retraining or update procedure, verification-and-validation activities (with acceptance criteria), labelling-and-instructions-for-use updates, and change-control governance. This is the artefact the release-gate consumes whenever a PCCP-covered modification is exercised — the change is only in-scope if the Modification Protocol was followed.
- **Impact Assessment.** The analysis showing the modifications, individually and jointly, do not adversely affect the safety and effectiveness of the device beyond what has been authorised. This includes the *envelope* of behaviours the modifications may produce and the mitigations that keep the device inside that envelope.

### The interaction between PCCP and continuous learning

A common misunderstanding is that PCCP authorises continuously-learning models. It does not. The FDA's position is that continuously-learning models — where the model updates itself in the field, from field data, without a controlled release event — remain outside PCCP's scope. PCCP authorises **controlled retraining and update events** that the manufacturer runs on its own release cadence, with the Modification Protocol applied to each event, and with the Impact Assessment establishing that the envelope of authorised behaviours is not exceeded.

The release-assurance methodology owner uses this distinction to draw a hard boundary in the release-gate: an AI system whose developers want it to learn continuously in the field is not a PCCP candidate and must be evaluated under a different pathway (or restructured to introduce controlled release events). The distinction matters commercially — many AI-native product teams *want* continuous learning, and the release-gate is where the regulatory boundary is enforced.

### PCCP versus a new premarket submission — when the boundary is crossed

The Modification Protocol enumerates the classes of change PCCP authorises; the Description of Modifications sets their bounds. When a proposed modification does not fit inside the Description of Modifications (for example, retraining on a population outside the specified sites; adding an operating point outside the specified curve; changing the model architecture) it is *outside PCCP scope* and requires a new premarket submission. The release-assurance methodology owner is the function that makes this call and — where necessary — refuses the change under PCCP.

Where the call is not clear-cut (a modification that arguably fits the Description of Modifications but tests its bounds), the release-assurance owner works with the regulatory-affairs function to file a Q-submission with FDA before the change is exercised. The Q-submission gets an FDA reading on whether the modification fits inside the authorised PCCP, and provides a paper trail if the FDA later inspects the manufacturer's PCCP execution. The release-gate does not approve modifications whose PCCP fit is contested but unresolved.

## Worked shape — an ED triage SaMD with a PCCP-covered retraining

Take a concrete SaMD: an **emergency-department triage assistant** that ingests structured triage data plus a short free-text presenting-complaint and outputs a triage-priority recommendation for the clinician. The intended use is *decision support*, not autonomous triage. The device is locked at initial marketing authorisation, and the manufacturer wants to pre-authorise annual retraining on data from the sites that deploy the device, plus quarterly updates to a specific preprocessing rule for free-text input.

Plugged into GMLP and PCCP:

- **GMLP submission evidence set:** multidisciplinary-team roster (principle 1); software-engineering and cybersecurity plan citing IEC 62304 (principle 2); intended-population memo and dataset-representativeness analysis across the sites in scope (principle 3); train/validation/test disjointness verification (principle 4); reference-set justification (principle 5); model-design rationale keyed to available data volume (principle 6); joint clinician-plus-device performance study on a representative site (principle 7); clinical-conditions validation exercising overnight vs day shift, EHR-schema variants across sites (principle 8); labelling and instructions-for-use covering contraindications and subgroup performance (principle 9); post-market monitoring plan (principle 10).
- **PCCP Description of Modifications:** two entries — annual site-data retraining and quarterly preprocessing-rule update, each with triggers, bounds, and notifications specified.
- **PCCP Modification Protocol:** end-to-end retraining SOP including data-quality gates, disjointness re-verification, revalidation against the reference set with pre-registered acceptance criteria, and labelling-update procedure; preprocessing-update SOP with narrower V&V scope.
- **PCCP Impact Assessment:** envelope analysis showing that retraining within the specified bounds cannot degrade sensitivity on high-acuity classes below authorised thresholds, and that preprocessing updates cannot silently change the model's decision boundaries; mitigation: automatic revalidation gate before any modification is released to sites.
- **Release-gate criteria for each retraining event:** disjointness re-verification passed; reference-set performance within envelope; joint clinician-plus-device performance re-measured on a representative site; labelling updates drafted; on-going monitoring plan refreshed. The gate is the *same* gate the initial release passed; PCCP does not create a lighter gate, it removes the FDA-submission requirement for changes that stay inside the pre-authorised envelope.

That is a PCCP-covered SaMD as the release-assurance owner sees it. Exercise-02 asks you to develop the Description, Modification Protocol, and Impact Assessment for an SaMD scenario of your own choosing, with the release-gate criteria for each pre-authorised modification enumerated.

## Related instruments the release-assurance owner tracks

The GMLP-plus-PCCP shape sits inside a broader FDA and international regulatory landscape that the release-assurance owner reads in the background even when the anchor obligation is GMLP:

- **The FDA Digital Health Center of Excellence** ([DHCoE](https://www.fda.gov/medical-devices/digital-health-center-excellence)) is the FDA's coordinating body for digital-health regulatory work; its publications track the direction of FDA thinking on AI/ML devices, including on transparency for AI/ML-enabled device software functions.
- **The IMDRF (International Medical Device Regulators Forum) AI Medical Devices working group** publishes documents on AI-specific device concepts (definitions, risk categorisation, quality-management adaptations). Where a manufacturer ships internationally, the IMDRF documents are the cross-jurisdictional shape.
- **ISO 14971** — the medical-device risk-management standard — applies to any medical device including AI/ML-enabled ones. The GMLP principles do not replace ISO 14971; they layer on top.
- **IEC 62304** — the medical-device software lifecycle standard — is the standard GMLP principle 2 typically references for software-engineering discipline.
- **EU Medical Device Regulation (MDR, Regulation (EU) 2017/745)** and **In-Vitro Diagnostic Regulation (IVDR, Regulation (EU) 2017/746)** are the EU statutory counterparts to the FDA pathways; manufacturers shipping into the EU carry MDR/IVDR obligations that braid with EU AI Act obligations for high-risk medical-device AI. This is a rich interaction covered in `mod-106` at cross-jurisdictional altitude.

The release-package for a globally-shipped SaMD carries the GMLP-plus-PCCP artefacts for the U.S. pathway and the MDR/IVDR technical-documentation artefacts for the EU pathway, with a crosswalk that shows which pieces of evidence discharge which obligations in each jurisdiction. The release-assurance methodology owner authors and maintains the crosswalk; `mod-106` teaches the crosswalk shape.

## Where this shows up in the rest of the track

- `mod-101` — GMLP principles 3, 7, 8, 9, 10 sit inside MAP and MEASURE of NIST AI RMF; a manufacturer running under both cross-references them in the assurance case.
- `mod-102` — the assurance case for a SaMD carries a GMLP-principle branch alongside its NIST AI RMF and EU AI Act (where applicable) branches; PCCP-covered modifications land as sub-cases citing the Modification Protocol.
- `mod-103` — the release-gate variant for a PCCP-covered modification is a *smaller* gate than the initial release-gate but not a *soft* gate; the reversal contract includes a rollback path if the revalidation gate fails.
- `mod-105` — the labelling and instructions-for-use are the SaMD sibling of the system card; principle 9 is the driver.
- `mod-108` — deployment-tier gating for medical devices maps to the SaMD framework's risk categorisation (I–IV) rather than to a bank's MRM tier.
- `mod-109` — the third-party interface for medical devices includes clinical evaluators and, where a notified body is involved (EU MDR route), the notified body itself.
- `mod-110` — GMLP principle 10 is the direct sibling of the post-market surveillance loop `mod-110` teaches; PCCP-covered retraining triggers are one type of surveillance-driven action.

## Summary

- FDA's shape for AI/ML medical devices sits in three connected instruments: the 10 GMLP guiding principles (2021, joint with Health Canada and MHRA); the PCCP final guidance (December 2024, statutory basis FD&C Act §515C); and the older device-specific pathways (510(k), De Novo, PMA; SaMD framework).
- GMLP is a quality baseline: 10 principles covering multidisciplinary expertise, software-engineering discipline, representative data, train/test disjointness, reference-set selection, model-design fit, human-AI team performance, clinically-relevant testing, labelling clarity, and post-market monitoring.
- PCCP is a mechanism to pre-authorise specified post-market modifications at initial marketing authorisation, with three components: Description of Modifications, Modification Protocol, and Impact Assessment. Pre-authorised modifications can be implemented without a new premarket submission.
- PCCP does *not* authorise continuously-learning models; it authorises controlled retraining and update events the manufacturer runs on a release cadence, with the release-gate consuming the Modification Protocol at each event.
- The release-package for a PCCP-covered SaMD carries the GMLP evidence set at initial authorisation and the three PCCP components; each pre-authorised modification is a release-gate event with the same rigour as the initial release, minus the FDA-submission requirement.
- Exercise-02 asks you to develop the GMLP-plus-PCCP submission shape for an SaMD scenario of your own choosing.
