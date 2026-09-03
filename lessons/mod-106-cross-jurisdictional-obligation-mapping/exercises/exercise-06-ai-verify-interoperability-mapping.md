# exercise-06: AI Verify Interoperability Mapping

**Estimated effort:** 2 hours

## Objective

Close the map by adding the **Singapore AI Verify interoperability layer** — the one-run-many-rows discipline chapter `07` names. For every row on the extended map (from exercises `01`–`05`), decide which AI Verify Framework principles the row's deliverable contributes to, which specific toolkit test IDs would satisfy the row's evaluation demand, and which single evaluation-report content-address a downstream reader would resolve to see the evidence. Then author the toolkit configuration that would *produce* that report and the coverage audit that confirms every row that expected to attach actually did.

The output is the interoperability contract the release-gate holds itself to: many rows across many jurisdictions attach to a single AI Verify report, and the gaps (LL 144 independent-audit, CFPB reason-code fidelity, UGESP-specific methodology, PRC substantive content) are recorded explicitly so nobody quietly assumes the shared report discharges them.

## Prerequisites

- Chapter [`07-singapore-ai-verify-interoperability.md`](../07-singapore-ai-verify-interoperability.md) — the eleven principles, the toolkit, the Model AI Governance Framework, and the MGF-GenAI additions.
- Chapter [`08-map-schema-and-emission.md`](../08-map-schema-and-emission.md) — the interoperability columns (`interop_ai_verify_principles`, `interop_ai_verify_test_ids`, `interop_mgf_building_block`, `interop_ai_verify_report_ptr`, `interop_gap`) and the map header shape.
- Exercises [`exercise-01`](exercise-01-eu-ai-act-obligation-to-deliverable-map.md) through [`exercise-05`](exercise-05-non-eu-overlay-uk-au-ca-jp-kr-cn-br.md) — the map they produced is the input.
- Skim access to the [AI Verify Foundation site](https://aiverifyfoundation.sg/), the [AI Verify Toolkit repository](https://github.com/aiverify-foundation/aiverify) (look at the technical-test catalogue and the process-check list), the [Model AI Governance Framework (2020 second edition)](https://www.pdpc.gov.sg/-/media/files/pdpc/pdf-files/resource-for-organisation/ai/sgmodelaigovframework2.pdf), and the [Model AI Governance Framework for Generative AI (2024)](https://aiverifyfoundation.sg/wp-content/uploads/Model-AI-Governance-Framework-for-Generative-AI-May-2024-1-1.pdf).
- If your system includes an LLM, familiarity with the [Project Moonshot](https://aiverifyfoundation.sg/project-moonshot/) LLM evaluation toolkit and its test taxonomy.

## Problem statement

Take the map from exercise `05` and add the interoperability layer to *every* row. Before you author the row-level fields, do the requirements-first configuration walk chapter `07` names: walk the map row-by-row and list the tests each row would need to see in the shared report, so that the toolkit configuration is authored *from the map's evaluation demand* rather than *from AI Verify's defaults*.

Then run (or simulate — this is a paper exercise, you do not need to execute the toolkit) the configured AI Verify battery, and produce the post-run coverage audit: for every row that was expected to attach, did the report actually cover it? Where it did not, is the gap a *configuration miss* (fix it and re-run) or an *interoperability gap* (record `interop_gap` with a follow-up)?

Finally, be honest about the four categories of obligation that AI Verify **cannot** satisfy — prescribed-methodology audits (LL 144 independent bias audit), certified-body audits (ISO/IEC 42001 by an ISO/IEC 42006-accredited body), substantive-content obligations (PRC CAC content policy), and bespoke fidelity evaluations (CFPB reason-code fidelity). Their rows carry `interop_gap` with a reason and a pointer to the parallel artefact that actually discharges them.

## Requirements

Produce five artefacts.

### 1. `interop-extended-map.yaml`

The exercise-`05` map, extended with the interoperability columns for every row. New / updated fields per row:

- `interop_ai_verify_principles` — list drawn from the eleven principles (transparency, explainability, repeatability, safety, security, robustness, fairness, data governance, accountability, human agency and oversight, inclusive growth). May be empty for rows that are purely filing / registration actions (Article 49, Korean in-country representative appointment) — record `[]` explicitly rather than omitting the field.
- `interop_ai_verify_test_ids` — list of specific toolkit test identifiers (or a placeholder marker where the test exists conceptually but the exact identifier needs verification against the current toolkit version — mark `<!-- needs-research: … -->`).
- `interop_mgf_building_block` — one of `internal-governance | human-involvement | operations-management | stakeholder-communication`, or an MGF-GenAI dimension identifier for GenAI-relevant rows (`accountability | data | trusted-development-and-deployment | incident-reporting | testing-and-assurance | security | content-provenance | safety-and-alignment-rd | ai-for-public-good`).
- `interop_ai_verify_report_ptr` — a content-address pointer of the shape `sha256:<digest>#/<json-pointer>` into the shared report, keyed to the row's evidence. Where the row attaches to a fairness sub-section, the pointer is `sha256:<digest>#/results/fairness/<group>`; where it attaches to a robustness sub-section, `sha256:<digest>#/results/robustness/<class>`. Use placeholder digests (`sha256:0000…placeholder`) for this exercise.
- `interop_gap` — `null` where the shared report fully discharges the row; a short string (`"prescribed-methodology"`, `"certified-body-audit"`, `"substantive-content-policy"`, `"bespoke-fidelity-evaluation"`, `"jurisdictional-registration"`, `"toolkit-does-not-cover"`) plus a `interop_gap_follow_up` pointer where it does not.
- `project_moonshot_ptr` — for rows that touch LLM-specific evaluations (Article 15 cybersecurity sub-rows for jailbreak / prompt-injection, GenAI-Profile information-security rows), add a Moonshot report pointer alongside the general AI Verify pointer.

The map header gains `frameworks_pinned.ai-verify-framework`, `.ai-verify-toolkit`, `.model-ai-governance-framework`, `.mgf-genai`, and (where applicable) `.project-moonshot`. Each carries the version-of-record you cross-tagged against.

### 2. `ai-verify-config.yaml`

The toolkit configuration authored *from the map's evaluation demand*. Sections required:

- `system_under_test` — model artefact reference, dataset references, task type, and (for GenAI) prompt-set references.
- `technical_tests` — enumerated per AI Verify principle. Each test entry names the test, its parameters (group definitions for fairness, perturbation classes for robustness, adversarial-example generation method for security, sampling strategy for repeatability), the acceptance threshold, and the *map rows* it is authored to serve. Use the map's `obligation_id`s as the linkage.
- `process_checks` — the process attestations to record per principle. Each entry names the attestation, the source deliverable (a path into your programme's evidence store from exercise `01`), and the map rows served.
- `output_format` — the report format the toolkit emits (`ai-verify-report-v<N>.json` for machine, `ai-verify-report-v<N>.pdf` for human), the `ai-verify-container-digest.txt` reproducibility marker, and the storage location (a content-addressed pipeline pointer per `mod-104`).
- `moonshot_addendum` — for LLM systems, the Moonshot test suite configuration (adversarial red-team suite, prompt-injection resilience, jailbreak resistance, harmful-content classification), each entry linked to the map rows it serves.

The important discipline: every technical test and every process check names the map rows it is meant to attach to. A test with no rows served is a candidate for removal; a row with no tests serving it is a coverage gap the map should not silently absorb.

### 3. `coverage-audit.md`

The post-run coverage audit. A table with one row per map row expected to attach to the shared report:

| obligation_id | expected principles | tests configured | tests actually run | report pointer | attached? | notes |
| --- | --- | --- | --- | --- | --- | --- |
| `eu-ai-act.art10.bias-report` | fairness, data governance | `fair.disparate_impact`, `fair.equal_opportunity` | `fair.disparate_impact`, `fair.equal_opportunity` | `sha256:…#/results/fairness` | yes | full coverage |
| `co-sb24-205.deployer.impact-assessment` | fairness, data governance, accountability | `fair.disparate_impact` | `fair.disparate_impact` | `sha256:…#/results/fairness` | partial | accountability process-check pending; follow-up recorded |
| `nyc-ll-144.bias-audit` | fairness | `fair.disparate_impact` (feeds auditor) | `fair.disparate_impact` | `sha256:…#/results/fairness` | attached-as-input | independent audit still required — `interop_gap: prescribed-methodology` |
| … | … | … | … | … | … | … |

The audit is the honest reckoning: does every expected attachment actually resolve, and where it does not, is the gap in the *configuration* (fixable) or in the *interoperability layer* (correctly annotated on the row)?

### 4. `interop-gap-register.md`

A per-row register of the interoperability gaps that AI Verify does not cover. For each gap, one entry:

- `obligation_id` — the map row.
- `gap_category` — one of the enum values above (`prescribed-methodology`, `certified-body-audit`, `substantive-content-policy`, `bespoke-fidelity-evaluation`, `jurisdictional-registration`, `toolkit-does-not-cover`).
- `reason` — one to three sentences on *why* the shared report cannot discharge this row.
- `parallel_artefact` — the deliverable that actually discharges the row (the LL 144 independent-audit report, the CFPB reason-code fidelity report, the PRC content-policy record, the ISO/IEC 42001 certificate, the algorithm-filing receipt).
- `parallel_owner` — the role or external party producing the parallel artefact.
- `review_by` — the date the gap posture is re-verified (e.g., when a Moonshot release covers a previously uncovered test class).

The register makes it explicit that AI Verify is an interoperability *layer*, not a substitute. A programme without this register tends to overstate what the shared report discharges.

### 5. `handoff-note-to-l50-architect.md`

A one-page hand-off note the release-assurance methodology owner writes to the L50 `senior-ai-governance-architect`. It summarises the map's interoperability posture: how many rows attached to the shared report, how many are covered by parallel artefacts, how many gaps remain, and what the architect should know about aggregation across systems. This is what closes chapter `08`'s L50 aggregate-handoff step.

The note is short. It should include:

- **Interoperability coverage summary.** Rows attached to shared report vs. rows discharged by parallel artefacts vs. rows still `open`.
- **Aggregation candidates.** Rows whose `deliverable` names a template a common enterprise control would likely subsume (a shared risk-management plan across many systems, a shared QMS, a shared data-lineage manifest schema).
- **Framework-refresh calendar.** Which framework pins on this map (AI Verify, Playbook, ISO revisions, CAC / Korea / Brazil / Canada instrument updates) are due for re-verification in the next six months, based on the version pins in the header.
- **Interop-gap patterns.** Which gap categories appear repeatedly on this map; where the L50 might reasonably invest in an enterprise-wide parallel-artefact capability (a shared independent-audit vendor relationship, a shared reason-code-fidelity toolchain, a shared substantive-content-policy authoring service).
- **Unresolved determinations.** Any `applies_when` or `not-applicable` classification the L50 should re-verify at the institution scope (particularly where two of your maps might disagree with each other).

## Starter guidance

- **Requirements-first, not toolkit-first.** The failure mode chapter `07` warns about is: run the toolkit's defaults, then map the report backwards to rows. That produces a report that looks complete but does not cover Colorado's age-group fairness ratios or ISO/IEC 24029-2's specific perturbation classes. Walk the map first; list the tests the map's rows *need*; then configure.
- **Every test names a row; every row names its tests.** If a test does not serve at least one row, ask whether it belongs in the configuration. If a row does not have at least one test (or a process-check) serving it, either it is a gap or the row belongs on the interop-gap register.
- **One content-address, many pointers.** The shared report is one JSON document with a single top-level content-address. Rows point at *sub-sections* of that document via JSON-pointer (`sha256:<digest>#/results/fairness/age`). Multiple rows can point at the same sub-section — that is the whole point of interoperability.
- **The MGF building block is not a decoration.** For GenAI rows, choosing the MGF-GenAI dimension (content-provenance, incident-reporting, testing-and-assurance) helps the L50 architect see the aggregation pattern. Choosing "operations-management" for everything defeats the purpose.
- **LL 144 attaches as input, not as substitute.** An AI Verify fairness test *feeds* the independent auditor. The map row should reflect that: `interop_gap: prescribed-methodology`, with the LL 144 auditor's report as the `parallel_artefact` in the gap register. Do not mark the row `attached` and call it done.
- **CFPB reason-code fidelity is a bespoke evaluation.** AI Verify explainability tests contribute but do not on their own demonstrate "specific and accurate" reason codes. The row's gap category is `bespoke-fidelity-evaluation`; the parallel artefact is `cfpb-reason-code-fidelity-report-v<N>.md` from exercise `04`.
- **PRC content-policy is content-policy.** No generic toolkit measures conformance to PRC substantive content requirements. The row's gap is `substantive-content-policy`; the parallel artefact is the content-policy evaluation and the CAC filing record.
- **ISO/IEC 42001 certification is a certified-body audit.** The AI Verify report is *input* to an internal audit under clause 9.2, but the certificate under 42006 accreditation comes from the certification body. Do not mark 42001-scoped rows `attached` to the AI Verify report and forget the certification path.
- **Non-GenAI systems still touch some Moonshot territory.** If your product has any LLM component (a small summarisation layer, a chatbot support surface) the Moonshot subset for that component's tests belongs on the map.
- **Pinning matters.** AI Verify's principle list has been refined between the 2022 MVP and the current release; toolkit test IDs move. Pin the framework version, the toolkit version, the Model AI GF version, and (where relevant) Moonshot version in the map header. Use `<!-- needs-research: … -->` where you are unsure of the exact pin.
- **The audit is the honest reckoning.** If the coverage audit is 100 % attachments with zero gaps, either you have a genuinely well-configured battery or you have quietly under-scoped the rows. Assume the latter and re-check.

## Acceptance criteria

You have succeeded if:

- `interop-extended-map.yaml` retains every row from exercise `05` unchanged in its anchor / NIST / ISO / US-side / non-EU fields and adds the interoperability columns to every row.
- Every row's `interop_ai_verify_principles` field is populated (possibly empty, but present) and `interop_ai_verify_test_ids` names the tests the row expects (or is annotated `interop_gap` where no toolkit test attaches).
- Every row's `interop_ai_verify_report_ptr` is either a plausible content-address pointer with a JSON-pointer path or `null` with an `interop_gap` reason.
- Every row's `interop_mgf_building_block` (or MGF-GenAI dimension for GenAI rows) is set.
- Rows that touch LLM-specific evaluation surface carry `project_moonshot_ptr` alongside the general AI Verify pointer.
- The map header pins AI Verify Framework, AI Verify Toolkit, Model AI Governance Framework, MGF-GenAI, and (where applicable) Project Moonshot with version-of-record.
- `ai-verify-config.yaml` is authored from the map's demand — every technical test and process check names the map rows it serves; no unassigned tests, no unserved rows without an interop-gap entry.
- `coverage-audit.md` covers every row expected to attach to the shared report, honestly recording attachments, partials, and gaps. No row is silently absent.
- `interop-gap-register.md` covers every row whose `interop_gap` is non-null. Each entry names the parallel artefact and the parallel owner.
- Prescribed-methodology rows (LL 144 bias audit), certified-body-audit rows (ISO/IEC 42001), substantive-content-policy rows (PRC CAC), bespoke-fidelity-evaluation rows (CFPB reason-code fidelity), and jurisdictional-registration rows (EU Article 49, PRC algorithm filing, Korean in-country representative) all appear in the gap register with correct categorisation.
- `handoff-note-to-l50-architect.md` summarises the map's interoperability posture and gives the L50 architect a starting point for aggregate queries across systems.
- Every place you could not verify an exact toolkit test ID, Moonshot suite name, or framework version pin is marked `<!-- needs-research: … -->` rather than guessed.
- A reviewer walking the final map cold can see, for any obligation, which shared-report evidence attaches to it, which parallel artefact discharges it if the shared report cannot, and where the residual gaps sit.

## Stretch goals

- **Simulate the one-run-many-rows discipline end-to-end.** Even without executing the real toolkit, produce a stub `ai-verify-report-v1.json` with the JSON shape that would satisfy every attached row (a fairness sub-section keyed by group, a robustness sub-section keyed by perturbation class, an explainability sub-section, etc.). Compute the report's SHA-256 and populate the map's `interop_ai_verify_report_ptr` fields with a real digest. This makes the map machine-verifiable — a tool can now confirm every attached row's JSON-pointer resolves.
- **Cross-tag onto the Hiroshima AI Process Code of Conduct.** For frontier-model / GPAI rows (from `mod-111`), add a `sibling_hiroshima_code_commitment` sub-field naming the Code of Conduct commitment each row contributes to. Use the eleven commitments as the enumeration.
- **Build a rows-per-principle report.** Author a small analysis (`rows-per-principle.md`) that inverts the map: for each AI Verify principle, list every row that tags to it. This is what a reviewer answering "show me every deliverable contributing to `fairness`" reads. It also flags principles that are under-populated — a signal the map may under-tag them.
- **Rows-per-gap-category report.** Similarly, invert the interop-gap register: for each gap category, list the rows in it. A category with many rows (e.g., many `prescribed-methodology` gaps) is a signal that the L50 architect could invest in an enterprise-wide capability to close that gap uniformly.
- **Author the coverage-audit script sketch.** In `coverage-audit-script.md`, sketch the automation that would run the coverage audit at each release: for each row with a non-null `interop_ai_verify_report_ptr`, resolve the pointer against the actual report and check that the JSON-pointer path exists and carries a non-empty result. This is what closes the discipline into the release-gate.
- **Compose with the MAS FEAT principles for a finance-sector system.** If your system has financial-services exposure, add a `sg-mas-feat` overlay row set with the MAS Fairness / Ethics / Accountability / Transparency principles and cross-tag them onto the AI Verify principles. This anticipates sector-regulated composition from `mod-107`.
- **Draft the Project Moonshot suite selection.** In `moonshot-suite-selection.md`, list the Moonshot test suites your programme would run on the LLM component, why each suite is in scope, and which map rows each suite serves. This makes the Moonshot addendum explicit rather than embedded in the toolkit config.
- **Draft the toolkit-container reproducibility protocol.** In `toolkit-reproducibility.md`, sketch how you would archive the toolkit container digest and the exact configuration to permit re-execution of the shared report a year later during a post-market review or an audit. Cross-reference the evidence-pipeline reproducibility discipline from `mod-104`.
