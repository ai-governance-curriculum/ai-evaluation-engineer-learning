# Singapore AI Verify as an Interoperability Reference

## Motivation

Chapters `02`–`06` layered jurisdiction after jurisdiction onto the map. Each layer added rows; each row added a *shared or new deliverable*; each deliverable ultimately points at a *test* — an evaluation run, a bias audit, a robustness measurement, a red-team report. Left unmanaged, the map's evaluation surface expands linearly with the jurisdiction count and the release-gate begins to run the same evaluation three or five times in slightly different shapes to satisfy overlapping obligations.

Singapore's [AI Verify](https://aiverifyfoundation.sg/) is the interoperability reference this chapter adopts to keep that expansion under control. AI Verify is a testing framework and open-source toolkit developed by the Infocomm Media Development Authority (IMDA) and hosted by the AI Verify Foundation. Its central proposition is that a common technical-test-and-process-check battery, mapped onto a well-known set of governance principles, can be *shared* across jurisdictions — one battery run, many obligations discharged.

The value on this map is not that AI Verify is itself a statute the release-gate must satisfy (it is not). The value is that AI Verify's principle set is deliberately aligned with the OECD AI Principles, the NIST AI RMF characteristics, ISO/IEC 42001, the EU AI Act's substantive obligations, and (increasingly) the Hiroshima Code of Conduct. If the release-gate names AI Verify as its evaluation-battery interface, the same battery output can attach to many map rows across jurisdictions without duplication.

This chapter walks:

1. The AI Verify Foundation, its instruments, and their legal status.
2. The AI Verify Framework's eleven principles and how they cross-tag onto the anchor.
3. The AI Verify Toolkit — technical tests, process checks, and how it emits an assessment report.
4. Where AI Verify's Model AI Governance Framework (MGF) sits and how it composes with the Framework.
5. How to use AI Verify as the *evaluation-battery interface* on the map, so one battery run discharges rows across jurisdictions.
6. The specific compose points with the EU AI Act, NIST AI RMF, ISO/IEC 42001, PDPA, and the [Model AI Governance Framework for Generative AI](https://aiverifyfoundation.sg/) (MGF-GenAI).

## The AI Verify ecosystem in one paragraph

The IMDA and Personal Data Protection Commission (PDPC) issued the first *Model AI Governance Framework* (Model AI GF) in 2019 and updated it in 2020. In 2022 the IMDA released **AI Verify**, an open-source AI governance testing framework and toolkit, and in 2023 established the [AI Verify Foundation](https://aiverifyfoundation.sg/) — a not-for-profit hosted at the Linux Foundation — to steward the framework and toolkit as open-source community projects. In 2024 the Foundation and IMDA published the [Model AI Governance Framework for Generative AI](https://aiverifyfoundation.sg/wp-content/uploads/Model-AI-Governance-Framework-for-Generative-AI-May-2024-1-1.pdf), extending the framework to generative-AI-specific concerns. The [PDPA](https://www.pdpc.gov.sg/) supplies Singapore's data-protection floor, and the PDPC's [Advisory Guidelines on the Use of Personal Data in AI Recommendation and Decision Systems](https://www.pdpc.gov.sg/Guidelines-and-Consultation) supply the AI-specific personal-data guidance.

**Legal status.** AI Verify itself is voluntary. It is *not* a certification regime, and no statute mandates its use. It is used as a market-and-procurement interoperability layer: enterprises adopt it, tender processes reference it, and multinational programmes use it as evidence of testing rigour. The PDPA is statutory; Singapore's [Cybersecurity Act 2018](https://sso.agc.gov.sg/Act/CA2018) applies for critical information infrastructure. Sectoral guidance (MAS Fairness / Ethics / Accountability / Transparency — the FEAT principles — for financial services) is regulator-issued supervisory expectation.

## The AI Verify Framework — eleven principles

The AI Verify Framework organises AI governance testing around eleven principles the Foundation groups into five categories. The exact grouping and principle names should be verified against the current Framework version, but the shape below is stable enough to build the map around.

- **Transparency of AI to individuals**
  - Transparency
- **Understanding how the AI model reaches decisions**
  - Explainability
  - Repeatability / Reproducibility
- **Ensuring safety and resilience**
  - Safety
  - Security
  - Robustness
- **Ensuring fairness / no unintended discrimination**
  - Fairness
  - Data governance
- **Ensuring proper management and oversight**
  - Accountability
  - Human agency and oversight
  - Inclusive growth, societal and environmental well-being

`<!-- needs-research: reconcile the exact eleven-principle list and grouping against the current AI Verify Framework version — the AI Verify Foundation refined the taxonomy between the 2022 MVP and later releases -->`

Every principle in the Framework carries a *testable component* (a set of technical tests the toolkit runs against the model) and a *process check component* (a set of documentation / process attestations the organisation records). The Framework's design is that the *combination* of the two is what satisfies the principle — a test alone is not enough, and a process attestation alone is not enough.

## The AI Verify Toolkit — technical tests and process checks

The [AI Verify Toolkit](https://github.com/aiverify-foundation/aiverify) is an open-source Python-based tool that:

- Runs a battery of technical tests against a supplied model + dataset (fairness metrics per group; robustness against perturbation; explainability via SHAP / LIME / equivalent; performance metrics; adversarial-example tests).
- Prompts the operator through a set of process checks (documented governance policies, data-lineage records, human-oversight design, incident-response plan, retention policy — the process side of each principle).
- Emits a **testing report** in a defined format that combines the technical results and the process attestations.
- Supports containerised deployment for reproducibility.

The MGF-GenAI added complementary artefacts for generative-AI systems — the [AI Verify GenAI Sandbox / MLC AILuminate](https://aiverifyfoundation.sg/project-moonshot/) project and the [Project Moonshot](https://aiverifyfoundation.sg/project-moonshot/) LLM evaluation toolkit are the current evaluation-battery references for LLMs.

Deliverables the toolkit emits that land on the map:

- `ai-verify-report-v<N>.pdf` — the human-readable report from the toolkit
- `ai-verify-report-v<N>.json` — the machine-readable results
- `ai-verify-config-v<N>.yaml` — the toolkit configuration (which tests were run, at what thresholds)
- `ai-verify-container-digest.txt` — the container digest for the toolkit run, for reproducibility
- `project-moonshot-report-v<N>.json` — where applicable, the Moonshot LLM evaluation results

## The Model AI Governance Framework — process spine

The Model AI Governance Framework (Model AI GF) is the process-side companion. Where AI Verify is *test-heavy*, the Model AI GF is *policy-heavy* — an implementation guide covering internal governance, decision framework for AI use, operations management, and stakeholder communication.

The Model AI GF's four building blocks map onto the map thus:

- **Internal governance structures and measures.** Maps onto EU AI Act Article 17 QMS rows and ISO/IEC 42001 clauses 4–5.
- **Determining the level of human involvement in AI-augmented decision-making.** Maps onto Article 14 rows and MAP-3 / MEASURE-2.9 sub-categories.
- **Operations management.** Maps onto Article 9 rows and Article 15 rows.
- **Stakeholder interaction and communication.** Maps onto Article 13 rows and the card-side output from `mod-105`.

The MGF-GenAI adds nine dimensions specific to generative AI: accountability, data, trusted development and deployment, incident reporting, testing and assurance, security, content provenance, safety and alignment R&D, and AI for public good. Each dimension composes onto the AI Verify Framework and onto the map's existing rows.

## Cross-tag row extension

Every existing row on the map (from chapters `02`–`06`) picks up an interoperability column:

| Field | Content |
| --- | --- |
| `interop_ai_verify_principles` | The AI Verify principles the row's deliverable contributes to (e.g., `[fairness, data_governance, transparency]`) |
| `interop_ai_verify_test_ids` | The specific toolkit test IDs whose output attaches to this row (e.g., `[t.fair.001, t.robust.003]`) |
| `interop_mgf_building_block` | Which Model AI GF building block or MGF-GenAI dimension the row contributes to |
| `interop_ai_verify_report_ptr` | Content-address pointer into the report / json artefact where the row's evidence appears |

The pointer is what makes AI Verify a genuine interoperability layer: many rows across jurisdictions can point at the same report content-address for the fairness or robustness evidence — one battery run, many rows discharged. Where a row cannot point at a shared report, either the shared battery does not yet cover it (feature gap) or the obligation is genuinely jurisdiction-specific (correct).

## Compose points with the anchor and other frames

### AI Verify ↔ EU AI Act

AI Verify was explicitly designed to be *EU AI Act-compatible*. The [AI Verify Foundation's mapping documentation](https://aiverifyfoundation.sg/) publishes crosswalks that name which principles and which tests contribute to which EU AI Act articles. The recurring pattern on the map:

| AI Verify principle | Contributes to (EU AI Act rows) |
| --- | --- |
| Transparency | `eu-ai-act.art13.instructions-for-use`, `eu-ai-act.art13.deployer-card`, `eu-ai-act.art50.*` |
| Explainability | `eu-ai-act.art13.deployer-card`, `eu-ai-act.art14.oversight-design` |
| Repeatability / reproducibility | `eu-ai-act.art11.annex-iv.2`, `eu-ai-act.art15.accuracy-declaration` |
| Safety | `eu-ai-act.art9.harms`, `eu-ai-act.art15.robustness-report` |
| Security | `eu-ai-act.art15.cybersecurity-report`, `eu-ai-act.art12.integrity-plan` |
| Robustness | `eu-ai-act.art15.robustness-report` |
| Fairness | `eu-ai-act.art10.bias-report`, `eu-ai-act.art10.governance-plan` |
| Data governance | `eu-ai-act.art10.governance-plan`, `eu-ai-act.art10.dataset-cards`, `eu-ai-act.art10.lineage-manifest` |
| Accountability | `eu-ai-act.art17.qms`, `eu-ai-act.art47.declaration` |
| Human agency and oversight | `eu-ai-act.art14.oversight-design`, `eu-ai-act.art14.usability-report`, `eu-ai-act.art26.*` |
| Inclusive growth, societal and environmental well-being | broader impact-assessment rows; card-side from `mod-105` |

`<!-- needs-research: attach the specific AI Verify Foundation crosswalk document version to this table; the mapping evolves as the Framework releases new versions -->`

### AI Verify ↔ NIST AI RMF

The AI Verify principles map cleanly onto the RMF characteristics (valid and reliable; safe; secure and resilient; accountable and transparent; explainable and interpretable; privacy-enhanced; fair with harmful bias managed). The map's `sibling_nist_rmf` field is unaffected; the toolkit's test IDs *add* an interoperability pointer to that field's evidence.

### AI Verify ↔ ISO/IEC 42001

Where the map has ISO 42001 clause tags on a row (chapter `04`), the AI Verify process-check attestations for that principle can be listed as documented information under clause 7.5.3, and the technical-test outputs can be listed as monitoring under clause 9.1. This makes the AI Verify toolkit's report an *acceptable evidence artefact* for an ISO 42001 internal audit.

### AI Verify ↔ Singapore statute / PDPA / MAS FEAT

Rows in the map that already carry Singapore-specific obligations pick up direct AI Verify tags:

| Row | AI Verify tag |
| --- | --- |
| `sg-pdpa.consent` | Data governance |
| `sg-pdpa.notification-obligation` | Transparency |
| `sg-pdpa.protection-obligation` | Security |
| `sg-pdpa.access-and-correction` | Explainability |
| `sg-pdpa.data-protection-impact-assessment` | Accountability + Data governance |
| `sg-mas-feat.fairness` (finance-sector) | Fairness |
| `sg-mas-feat.ethics-accountability-transparency` (finance-sector) | Transparency + Accountability |

### AI Verify ↔ non-EU overlays

The interoperability value shows most clearly here — a single AI Verify fairness test can attach to:

- `eu-ai-act.art10.bias-report` (EU baseline)
- `co-sb24-205.deployer.impact-assessment` (Colorado)
- `nyc-ll-144.bias-audit` (with caveats — see below)
- `eeoc.title-vii.adverse-impact` (with caveats — UGESP methodology)
- `au-vaiss.g3.data-governance` (Australia)
- `br-pl-2338.high-risk.aia` (Brazil, if enacted)
- `kr-ai-framework.high-impact.risk-management` (Korea)

**Caveat: NYC LL 144.** The LL 144 bias audit has a *fixed methodology* (impact ratios per specified category), and it must be conducted by an *independent* auditor. An AI Verify test result cannot substitute for the LL 144 audit — but it can be *input* to the auditor's work and contribute to the map row's evidence, provided the audit itself is done by the qualified independent party.

**Caveat: UGESP four-fifths.** EEOC UGESP methodology specifies particular group definitions and analysis paths. AI Verify's fairness tests need to be configured to match UGESP conventions to attach to that row.

**Caveat: reason-code fidelity (CFPB).** CFPB adverse-action reason-code fidelity is a bespoke evaluation. AI Verify explainability tests contribute but do not by themselves meet the "specific and accurate" standard.

## The one-run-many-rows discipline

The interoperability discipline is a discipline on the *evaluation battery*, not on the map. It works only if the toolkit configuration (`ai-verify-config-v<N>.yaml`) is authored to *cover* the union of tests the map rows call for, not merely to hit AI Verify's defaults. The failure mode is a report that looks complete but that a Colorado impact-assessment row cannot attach to because the fairness test was run only against sex, not against age, or that a robustness row cannot attach to because the perturbation classes did not cover the ones ISO/IEC 24029-2 requires.

Two disciplines make the interoperability real:

1. **Requirements-first configuration.** The map is walked *before* the toolkit is configured. Every row that is a candidate for shared evidence lists the tests it needs. The configuration is then the union.
2. **Post-run coverage audit.** After the toolkit runs, every row that was expected to attach is checked: does the report actually cover it? Gaps get either a follow-up run or a row-specific supplementary evaluation.

Chapter `08` bakes both disciplines into the schema and the review workflow.

## Worked example — one fairness test attaching to five jurisdictional rows

A programme ships a hiring-tool product to EU, US (NY / national), Colorado, Australia, and Brazil. It runs the AI Verify fairness test suite with a configuration covering sex, race/ethnicity, age, and disability status against a representative test set.

The report emits:

- `ai-verify-report-v3.json`, content-addressed `sha256:be71…`
- Fairness sub-section content-addressed `sha256:be71…#/results/fairness`

Rows on the map:

```yaml
- obligation_id: eu-ai-act.art10.bias-report
  interop_ai_verify_principles: [fairness, data_governance]
  interop_ai_verify_test_ids: [fair.disparate_impact, fair.equal_opportunity]
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness

- obligation_id: co-sb24-205.deployer.impact-assessment
  interop_ai_verify_principles: [fairness, data_governance, accountability]
  interop_ai_verify_test_ids: [fair.disparate_impact, fair.equal_opportunity]
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness

- obligation_id: nyc-ll-144.bias-audit
  interop_ai_verify_principles: [fairness]
  interop_ai_verify_test_ids: [fair.disparate_impact]     # feeds independent auditor
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness
  notes: "Feeds LL 144 independent audit; does not substitute for it"

- obligation_id: eeoc.title-vii.adverse-impact
  interop_ai_verify_principles: [fairness]
  interop_ai_verify_test_ids: [fair.disparate_impact]     # configured for UGESP groups
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness

- obligation_id: au-vaiss.g3.data-governance
  interop_ai_verify_principles: [fairness, data_governance]
  interop_ai_verify_test_ids: [fair.disparate_impact, fair.equal_opportunity]
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness

- obligation_id: br-pl-2338.high-risk.aia
  interop_ai_verify_principles: [fairness, data_governance, accountability]
  interop_ai_verify_test_ids: [fair.disparate_impact, fair.equal_opportunity]
  interop_ai_verify_report_ptr: sha256:be71…#/results/fairness
```

One report; six rows attached; two overlays satisfied fully by the report (`au-vaiss.g3`, `eu-ai-act.art10.bias-report`); one overlay served by the report but with the independent-audit caveat (`nyc-ll-144.bias-audit`); one requires additional UGESP-specific interpretation (`eeoc.title-vii.adverse-impact`); one waits on legislation (`br-pl-2338.high-risk.aia`) but is pre-populated.

## MGF-GenAI — the generative-AI additions

For generative-AI systems, the AI Verify Foundation's MGF-GenAI adds nine dimensions the map should cross-tag:

- Accountability
- Data
- Trusted development and deployment
- Incident reporting
- Testing and assurance
- Security
- Content provenance
- Safety and alignment R&D
- AI for public good

The interoperability column extends with `interop_mgf_genai_dimension`. The dimension mostly overlaps with existing rows — but a few generate new evaluation obligations that the Framework's default toolkit does not yet cover, chiefly:

- **Content-provenance testing** — cross-references C2PA / SynthID work from `mod-105` chapter `06`.
- **Incident-reporting readiness testing** — cross-references EU AI Act Article 61 rows and the drill report from chapter `02`.
- **Safety and alignment R&D disclosure** — for frontier-model providers, cross-references the Hiroshima Code of Conduct commitments and `mod-111`'s GPAI systemic-risk rows.

Project Moonshot is the current evaluation-battery reference for LLM-specific tests (adversarial red-teaming, prompt-injection resilience, harmful-content classification, jailbreak resistance). Where the system includes an LLM, the map's Article 15 cybersecurity sub-rows should carry a `project_moonshot_ptr` in addition to the general AI Verify report pointer.

## When AI Verify is not enough

The interoperability discipline has limits:

- **The toolkit's test surface is finite.** Tests not in the toolkit are not in the report; the row cannot attach. Programme-specific evaluations must be added as separate artefacts.
- **Prescribed-methodology obligations do not substitute.** LL 144 independent audit, CFPB reason-code fidelity, UGESP four-fifths analysis with prescribed group definitions — these have specified methodologies the toolkit does not implement out-of-the-box.
- **Certified-body audits are not covered.** ISO/IEC 42001 certification requires an accredited body under 42006; AI Verify does not accredit auditors.
- **Substantive content obligations are jurisdiction-specific.** PRC CAC content-policy compliance is not testable via a generic toolkit — a jurisdiction-specific content-policy layer is required and evaluated separately.
- **Legal counsel signs the applicability calls.** An AI Verify report can attach to a row, but the *classification* of whether a jurisdictional obligation applies is a legal call.

The map records these limits with an `interop_gap` sub-field on the row where the toolkit does not cover the obligation.

## Where this shows up in the rest of the track

- `mod-104` (evidence pipeline) — the AI Verify report artefacts are pushed into the evidence pipeline like any other artefact, and content-addressed there.
- `mod-105` (cards for external audiences) — the deployer-facing card can include a "tested with AI Verify vX.Y" statement and cite the report content-address.
- `mod-108` (deployment-tier gating) — tier criteria may require that specific AI Verify tests pass at specific thresholds; the tier decision is authored against the report.
- `mod-109` (third-party evaluator interface) — an AISI evaluation, a Big Four audit, or a notified-body assessment often uses the AI Verify report as input evidence; the interoperability layer is the hand-off shape.
- `mod-110` (post-market surveillance) — a periodic re-run of the AI Verify battery is one shape of post-market check.
- `mod-111` (GPAI systemic-risk assurance) — Project Moonshot is a candidate red-team battery for GPAI systemic-risk evaluations; the interoperability column carries the Moonshot report pointer.

## Summary

- Singapore's AI Verify Foundation publishes an interoperability testing framework (AI Verify) and companion policy frameworks (Model AI GF, MGF-GenAI) that are voluntary but widely used.
- The Framework's eleven principles cross-tag cleanly onto the anchor (EU AI Act), NIST AI RMF, ISO/IEC 42001, PDPA, and non-EU overlays.
- The map's row schema picks up an interoperability column: `interop_ai_verify_principles`, `interop_ai_verify_test_ids`, `interop_mgf_building_block` or `interop_mgf_genai_dimension`, and `interop_ai_verify_report_ptr`.
- The one-run-many-rows discipline requires the toolkit configuration be authored *from* the map's evaluation demand and the coverage be audited *against* the map's rows.
- Prescribed-methodology obligations (LL 144, CFPB, UGESP), certified audits (42001), and substantive content obligations (PRC) do not substitute — they layer.
- Project Moonshot is the LLM-specific evaluation-battery reference; MGF-GenAI adds nine generative-AI dimensions to cross-tag against.
- Exercise 06 walks a shared-battery scenario across jurisdictional rows; chapter `08` closes the module with the machine-readable schema and the review workflow that hands the map to the L50 architect.
