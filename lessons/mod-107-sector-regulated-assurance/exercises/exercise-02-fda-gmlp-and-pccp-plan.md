# exercise-02: FDA GMLP Evidence Set and PCCP Plan for a SaMD Scenario

**Estimated effort:** 3 hours

## Objective

For one AI/ML-enabled Software-as-a-Medical-Device (SaMD) scenario, author the **FDA GMLP-shaped evidence set for the initial marketing authorisation** and the **PCCP (Predetermined Change Control Plan) content set** for a small number of pre-authorised post-market modifications. The 10 GMLP principles from chapter `03` must each be discharged by a named artefact; the three PCCP components (Description of Modifications, Modification Protocol, Impact Assessment) must be complete; the release-gate criteria that fire on every pre-authorised modification event must be enumerated with the same rigour as the initial-release criteria.

The exercise is authoring, not solving. Where a factual determination would depend on FDA policy at time of submission, on the specific SaMD's regulatory pathway (510(k), De Novo, PMA), or on clinical-study design choices that would happen in a real programme, mark `<!-- needs-research: … -->` rather than guessing.

## Prerequisites

- Chapter [`03-fda-gmlp-and-pccp-for-ai-ml-medical-devices.md`](../03-fda-gmlp-and-pccp-for-ai-ml-medical-devices.md) — the 10 GMLP principles by lifecycle phase, the three PCCP components, the boundary between PCCP-covered and continuously-learning models, and the release-gate criteria for each pre-authorised modification.
- Skim access to [FDA — *Good Machine Learning Practice for Medical Device Development: Guiding Principles*](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the 10 principles in their canonical form.
- Skim access to [FDA — *Predetermined Change Control Plans for Artificial Intelligence-Enabled Device Software Functions*](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions) — the December 2024 final guidance. The three-components framing is the reference point.
- Familiarity with the SaMD framework (IMDRF's risk categorisation I–IV, or the pathway-specific reasoning your scenario uses).
- Familiarity with the peer-role registry — the release-assurance owner works alongside regulatory affairs, quality-management-system leads, clinical evaluation, cybersecurity, human-factors engineering, and post-market surveillance.

## Problem statement

Invent one specific SaMD your team is preparing for initial FDA marketing authorisation. The scenario must be *AI/ML-enabled* (the "AI/ML" is what makes GMLP and PCCP the operative shape) and must have a clinical decision surface (advisory or non-advisory) that a release-gate would meaningfully evaluate. Common patterns worth considering (pick one, or invent your own):

- **Emergency-department triage-support SaMD** — clinical-decision-support tool that ingests structured triage data plus short free-text presenting-complaint, recommending a triage-priority. Decision support, not autonomous triage.
- **Retinal-imaging screening SaMD** — computer-vision-based screening tool that reads fundus photographs and flags images for referable disease. High sensitivity requirement; specific reference-standard reasoning.
- **Cardiac-arrhythmia detection on wearable ECG** — signal-processing plus ML classifier detecting a small number of arrhythmia classes on wearable-device ECG; notification to the user and/or a clinician.
- **Radiology-triage prioritisation SaMD** — worklist reordering tool that reads imaging studies and boosts the priority of studies where a specific finding is likely. Advisory only; does not override.
- **Insulin-dosing decision-support SaMD** — closed-loop or open-loop dosing recommender for insulin-dependent diabetes. High-risk category; likely PMA pathway.
- **Digital-pathology assistant** — assistant that annotates whole-slide-imaging tiles for a pathologist review workflow.

Pick concretely and pin the scenario before you begin the artefact set. State the intended-use population, the clinical decision the SaMD supports, whether the deployment is autonomous or human-in-the-loop, the IMDRF SaMD risk category, and the FDA regulatory pathway you assume for initial authorisation.

## Requirements

Produce seven artefacts in a single directory.

### 1. `scenario-scoping-brief.md`

A one-page brief that fixes:

- **Product name and one-sentence intended purpose.** Named product; specific clinical decision informed; explicit statement of decision-support vs autonomous decisioning.
- **Intended-use population.** Who the device is for. Care setting. Exclusions.
- **SaMD risk category (IMDRF I–IV).** The category you assume, with reasoning.
- **FDA regulatory pathway.** 510(k), De Novo, or PMA — the assumption you make and the reasoning. `<!-- needs-research: … -->` is acceptable where the pathway would be determined through a Q-submission process in the real programme.
- **PCCP intent.** Explicit statement that the scenario intends to include a PCCP at initial marketing authorisation, and the classes of change PCCP will pre-authorise. Two to three pre-authorised change types is a good number for this exercise.
- **What the scenario is *not*.** Explicit exclusion of continuously-learning modes. Explicit exclusion of any change type that will not be pre-authorised (i.e., changes outside the PCCP that will require a new premarket submission if made).
- **Cross-jurisdictional reach.** Whether the SaMD will also be marketed in the EU (MDR / IVDR obligations attach) and in the UK / Canada / Japan (each with its own regulator). For this exercise, focus the artefact set on the FDA pathway and reference the EU MDR / IVDR crosswalk in a section rather than authoring parallel EU artefacts.

### 2. `gmlp-evidence-set.md`

The GMLP evidence set is the *quality-baseline* set for the initial marketing authorisation. Author it as a table with one row per GMLP principle and, for each row:

- **Principle identifier and title.** From the FDA GMLP page.
- **Evidence artefact(s).** Specific artefact filenames the release-package would carry — e.g. `multidisciplinary-team-roster.md` for principle 1, `dataset-representativeness-analysis.md` for principle 3, `train-validation-test-disjointness-verification.md` for principle 4, `joint-clinician-plus-device-performance-study.md` for principle 7, `labelling-and-instructions-for-use.md` for principle 9, `post-market-monitoring-plan.md` for principle 10.
- **Owner role.** The peer role that produces the substantive content.
- **Signing role.** The role whose signature closes the artefact.
- **Standards cross-reference.** Where the principle interacts with a formal standard (IEC 62304, IEC 81001-5-1, ISO 14971, ISO 13485), name it. Principle 2 is where the software-engineering and cybersecurity standards land explicitly.
- **Content sketch.** A short bulleted description of what the artefact would actually contain for the invented scenario — not full prose, but enough that a reviewer can see the artefact is plausible.

Then, in a separate short section, write two paragraphs on:

- **Human-AI team performance (principle 7).** How joint performance is measured for the specific scenario — the metric, the study design, the reference standard, the acceptance criterion. This is often the section a reviewer probes hardest.
- **Post-market monitoring (principle 10).** The high-level monitoring plan the initial-authorisation submission commits to. The full monitoring plan can be an artefact reference; this section states the *commitment*.

### 3. `pccp-01-description-of-modifications.md`

The PCCP Description of Modifications enumerates the pre-authorised change types precisely. For each pre-authorised change:

- **Change type name.** A concise, unambiguous name (e.g. "annual site-data retraining," "quarterly free-text-preprocessing-rule update," "operating-point addition on the pre-specified ROC curve").
- **Trigger.** The condition under which the change may be exercised (e.g. "when post-market monitoring detects a drift in sensitivity on the intended-use population exceeding threshold X on the reference set," "on a fixed calendar cadence").
- **Scope and bounds.** What the change may and may not do. For a retraining change, the data sources that may be used, the population restrictions, the model-architecture invariants, and the performance envelope the retrained model must remain within.
- **Notification.** What the manufacturer commits to notify — FDA, customers, users, clinicians — when the change is exercised, on what timing, in what medium.
- **Exclusions.** Explicit exclusions — change types that look similar but are *outside* the PCCP scope and would require a new premarket submission.

Two to three change types is a good exercise number. One change type should be a *retraining* event; another should be an *update to a supporting component* (preprocessing, guardrail, feature computation); a third, if included, is manufacturer's choice. Choose changes that produce a meaningful release-gate event, not trivial ones.

### 4. `pccp-02-modification-protocol.md`

The PCCP Modification Protocol is the end-to-end method for each pre-authorised change. Author, per change type from artefact 3:

- **Data-management plan.** For retraining changes, data sourcing rules, quality gates, disjointness re-verification with the reference test set, labelling rules, provenance tracking, and any data-governance oversight (e.g. ethics or IRB oversight if applicable).
- **Retraining or update procedure.** The technical procedure — model architecture invariants, hyperparameters that may / may not change, training environment reproducibility, artefact-version pinning.
- **Verification and validation activities.** The V&V activities for the change — offline evaluation against the reference set with pre-registered acceptance criteria, on-device or on-integration testing, human-factors re-evaluation where applicable, cybersecurity re-verification per IEC 81001-5-1 where applicable.
- **Labelling-and-instructions-for-use updates.** How labelling and IFU are updated to reflect the change, who reviews and approves the update, and how users are informed.
- **Change-control governance.** Who reviews the change proposal, who approves the change, and how the change decision is recorded. Cross-reference to the manufacturer's 21 CFR Part 820 quality-system change-control procedures.
- **Rollback plan.** If the change is exercised and post-release monitoring detects an unacceptable deviation, how the change is rolled back and how affected sites are informed.

### 5. `pccp-03-impact-assessment.md`

The PCCP Impact Assessment analyses how the pre-authorised modifications, individually and jointly, may affect safety and effectiveness. Cover:

- **Envelope analysis.** For each change type, the envelope of behaviours the change may produce and the mitigations that keep the device inside the authorised envelope. Cite the reference-set acceptance criteria as the numerical envelope where applicable.
- **Individual-change impact.** For each change type, the safety and effectiveness impact if the change is exercised within its bounds. Address any risk that the change could shift performance on a specific subgroup even while overall performance is preserved.
- **Cumulative-change impact.** The impact of the changes exercised in combination over the device's lifecycle. Are there interaction effects (a retraining after a preprocessing update may amplify subgroup shifts, for example)?
- **Mitigations.** The mitigations that keep the device safe and effective — pre-release revalidation, post-release monitoring, rollback readiness, cadence limits.
- **Residual risk.** Any residual risk the mitigations do not fully cover, and the risk-acceptance rationale (referencing the manufacturer's ISO 14971 risk-management file).

### 6. `release-gate-criteria-per-modification.md`

For each pre-authorised change type from artefact 3, enumerate the release-gate criteria the change must satisfy before it is released to the field. The gate has the *same rigour* as the initial release-gate; PCCP does not create a lighter gate. It removes the FDA-submission requirement for changes that stay inside the pre-authorised envelope; it does not remove the manufacturer's own release-gate.

For each criterion, name:

- **Criterion.** What is checked (e.g. "reference-set sensitivity within envelope").
- **Discharging artefact.** The artefact that provides the evidence.
- **Signer.** The role whose signature confirms discharge.
- **Currency window.** How recent the evidence must be for the gate to close.
- **Hard vs soft gate.** Whether failure blocks release (hard) or triggers dispositions (soft).
- **Rollback trigger.** What post-release signal would fire a rollback of the change (cross-reference the rollback plan in artefact 4).

### 7. `mdr-ivdr-crosswalk.md`

A short crosswalk from the FDA-shaped artefact set to what an EU MDR / IVDR submission would require. The exercise does not develop the EU artefact set; it names the crosswalk so the release-package can be assembled for a globally-shipped SaMD:

- **GMLP principle to MDR / IVDR technical-documentation section.** Where the GMLP evidence set discharges the same requirement as an MDR / IVDR General Safety and Performance Requirement (GSPR) or technical-documentation section, note the mapping.
- **PCCP to MDR / IVDR *change-substantial* discipline.** MDR / IVDR do not have a PCCP mechanism as such; changes deemed *substantial* trigger notified-body re-review. The crosswalk notes which PCCP-covered changes would likely trigger MDR / IVDR substantial-change review, so the release-package can plan accordingly.
- **Cross-references to `mod-106` for cross-jurisdictional obligation mapping.** For a globally-shipped SaMD, `mod-106` teaches the full cross-jurisdictional map; this crosswalk is a light sketch.

Where a jurisdictional fact would need to be verified against the current state of the relevant regulator's guidance, mark `<!-- needs-research: … -->`.

## Starter guidance

- **Fix the scenario before you author.** SaMD risk category and regulatory pathway drive every artefact. Getting them wrong means restructuring the release-gate criteria. Getting them right saves the exercise.
- **PCCP is not a mechanism for continuously-learning models.** If your scenario needs the model to update itself in the field from field data without a controlled release event, restructure — introduce controlled release events, or accept that PCCP is not the right pathway. The release-gate is where the boundary is enforced.
- **Two to three pre-authorised change types is enough.** More than five and the Modification Protocol becomes unwieldy. Pick change types that produce meaningful release-gate events. A trivial preprocessing tweak is a bad choice; a retraining event on new site data is a good one.
- **Principle 7 is where a reviewer probes.** GMLP principle 7 (human-AI team performance) is easy to gloss and hard to do well. Name the joint-performance metric, the study design, and the acceptance criterion explicitly. Automation bias is a real effect the study design should address.
- **Principle 3 dataset representativeness is not one row.** For a real SaMD, principle 3 typically involves several artefacts — data sourcing and lineage, demographic representativeness analysis, subgroup performance evaluation, gap-and-limitation documentation. For this exercise, one artefact is enough as long as the content sketch is honest about the underlying breadth.
- **The release-gate criteria for a PCCP-covered modification are as rigorous as the initial gate.** Do not soften them because the FDA does not require a new submission. The rigour protects patients; the FDA submission is an administrative step.
- **Rollback readiness is part of the plan.** A PCCP-covered change that cannot be rolled back if a post-release signal fires is a design defect. The rollback plan in artefact 4 is not decorative.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need FDA policy specifics, standards references not yet consolidated, or clinical-evaluation details that would depend on the specific device, mark it rather than guessing.
- **Do not fabricate clinical performance numbers.** Placeholders (`<placeholder>` or `<target-sensitivity>`) are fine. Fabricated sensitivities or effect sizes read as fake to a reviewer and are worse than an honest placeholder.

## Acceptance criteria

You have succeeded if:

- `scenario-scoping-brief.md` fixes the seven scoping decisions with reasoning. A reviewer can decide, from the brief alone, the intended use, the SaMD risk category, the regulatory pathway, the PCCP intent, and the pre-authorised change types.
- `gmlp-evidence-set.md` has one row per GMLP principle. Each row names concrete artefact filenames, owner and signing roles, standards cross-references where applicable, and a plausible content sketch for the invented scenario. Principle 7 (human-AI team performance) is treated in a separate paragraph and names the joint-performance metric, study design, and acceptance criterion. Principle 10 (post-market monitoring) is treated in a separate paragraph and names the initial-authorisation commitment.
- `pccp-01-description-of-modifications.md` covers two to three pre-authorised change types, each with a name, trigger, scope and bounds, notification, and exclusions. At least one change type is a retraining event.
- `pccp-02-modification-protocol.md` covers, per change type from artefact 3, the data-management plan, retraining/update procedure, V&V activities, labelling/IFU updates, change-control governance, and rollback plan.
- `pccp-03-impact-assessment.md` covers envelope analysis, individual-change impact, cumulative-change impact, mitigations, and residual risk.
- `release-gate-criteria-per-modification.md` enumerates, per change type, the release-gate criteria including hard vs soft classification, discharging artefact, signer, currency window, and rollback trigger.
- `mdr-ivdr-crosswalk.md` provides the crosswalk from the FDA-shaped artefact set to what the EU MDR / IVDR path would require. Cross-references to `mod-106` are named where the cross-jurisdictional map extends.
- Every one of the 10 GMLP principles is discharged by at least one named artefact.
- Every place a fact would need to be verified against FDA policy, standards, or scenario-specific clinical details is marked `<!-- needs-research: … -->` rather than guessed.
- The artefact set is *consistent* — the PCCP change types on the Description are the same set the Modification Protocol elaborates, the Impact Assessment analyses, and the release-gate criteria enumerate. A reviewer diffing across the set finds no drift.

## Stretch goals

- **Draft the Q-submission memo.** For one pre-authorised change type whose PCCP fit is not clean-cut, draft the Q-submission-like memo the manufacturer would file with FDA to confirm the change fits within the authorised PCCP. In `q-submission-memo.md`, include the manufacturer's own analysis, the specific question, and the change description.
- **Author the clinical-evaluation report shape.** In `clinical-evaluation-report-shape.md`, sketch the clinical-evaluation report the initial marketing submission carries — study design, endpoints, statistical treatment, results template, safety analysis, discussion. The full study report is out of scope; the shape is not.
- **Draft the cybersecurity plan.** In `cybersecurity-plan.md`, sketch the IEC 81001-5-1-shaped cybersecurity plan for the SaMD — threat model, mitigations, verification activities, incident response, updateability. Cross-reference the U.S. FDA cybersecurity guidance and, if the SaMD ships in the EU, the MDR Annex I §17 requirements.
- **Author the human-factors evaluation plan.** In `human-factors-evaluation-plan.md`, sketch the FDA-shaped human-factors evaluation for the SaMD — user profile, use scenarios, use-related risks, evaluation methodology (formative and summative), acceptance criteria. Human factors is often what catches issues the technical validation misses.
- **Add the post-market surveillance plan (foreshadowing `mod-110`).** In `post-market-surveillance-plan.md`, sketch the full post-market surveillance plan for the SaMD — active surveillance, passive surveillance (complaints, MDRs), performance-monitoring cadence, corrective and preventive action pathway, PCCP-modification triggers. This is `mod-110`'s territory but the linkage back to PCCP is worth practising here.
- **Draft the transparency-for-users artefact.** In `transparency-for-users-artefact.md`, sketch the labelling / IFU content that satisfies the joint FDA / Health Canada / MHRA transparency-for-ML-enabled-devices principles. Users include clinicians and, for direct-to-consumer devices, patients. Note the reading-level and audience-variant discipline (foreshadowing `mod-105`).
