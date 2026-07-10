# ISO/IEC Clauses Crosswalk — 42001, 23894, 42005, 25059, 24029-2

## Motivation

Where NIST AI RMF gives the map an *analytical* cross-tag (which sub-category a deliverable plugs into), the ISO/IEC standards give the map an *audit* cross-tag (which management-system clause an auditor will inspect the deliverable under). ISO/IEC 42001 in particular is the only certifiable AI management-system standard — an ISO/IEC 42006-accredited body can issue a certificate against it, and once an organisation is certified, every deliverable on the release-gate map has to be locatable inside a clause that certificate covers.

This chapter walks the five ISO/IEC standards that carry the release-gate's obligations:

- **ISO/IEC 42001:2023** — the AI management system (AIMS), clauses 4–10 and Annex A controls
- **ISO/IEC 23894:2023** — AI risk-management *guidance* (method behind AIMS clause 6 risk activities)
- **ISO/IEC 42005:2025** — AI system impact assessment (method behind AIMS clause 6 impact activities)
- **ISO/IEC 25059:2023** — SQuaRE for AI systems (the quality-attribute vocabulary that carries accuracy / robustness / usability into cards)
- **ISO/IEC 24029-2:2023** — Robustness of neural networks (method for Article 15 robustness evidence)

Adjacent standards (ISO/IEC 5259 data-quality series, ISO/IEC 8183 data lifecycle, ISO/IEC 42006 accreditation, ISO/IEC 27001 for cybersecurity) are noted where they intersect but not deeply crosswalked here.

## The cross-tag row extension

Every row on the map picks up a `sibling_iso_clauses` field carrying one or more clause references. Clause references use the `<standard> <clause-number>` shape:

- `ISO/IEC 42001 6.1.4` — a specific 42001 clause
- `ISO/IEC 42001 A.6.2.4` — a specific 42001 Annex A control
- `ISO/IEC 23894 6.5` — a specific 23894 clause
- `ISO/IEC 42005 8.3` — a specific 42005 clause
- `ISO/IEC 25059 5.2` — a specific 25059 quality sub-characteristic
- `ISO/IEC 24029-2 7.3` — a specific 24029-2 method clause

## ISO/IEC 42001 — the AIMS clause spine

ISO/IEC 42001 follows the **Harmonised Structure** (HS) common to ISO management-system standards. Clauses 1–3 are scope, references, and terms. Clauses 4–10 are the auditable requirements. Annex A is the AI-specific control catalogue, and Annex B provides implementation guidance for those controls.

The clause structure and how the release-gate deliverables plug in:

- **Clause 4 — Context of the organisation.** Understand internal and external issues, interested parties, and scope of the AIMS. Deliverables: `aims-scope-statement.md`, `interested-parties-register.yaml`. Not release-gate rows per se — organisational context underlies the whole map. `<!-- needs-research: confirm 42001 clause 4 sub-clauses land as 4.1 / 4.2 / 4.3 / 4.4 in the published text and adjust references accordingly -->`
- **Clause 5 — Leadership.** AI policy, roles, responsibilities. Deliverables: `ai-policy.md`, `roles-and-responsibilities.yaml`. Ties to Article 17 QMS.
- **Clause 6 — Planning.** Risks and opportunities, AI risk assessment, AI risk treatment, AI system impact assessment, objectives. This is where the risk-management-plan and impact-assessment deliverables from chapter `02` land. ISO/IEC 23894 is the method reference for the risk activities; ISO/IEC 42005 is the method reference for the impact activities.
- **Clause 7 — Support.** Resources, competence, awareness, communication, documented information. Deliverables: `competence-register.yaml`, `documented-information-index.yaml`. Clause 7.5 (documented information) is where the Article 12 record-keeping row picks up its ISO tag.
- **Clause 8 — Operation.** Operational planning and control, AI risk assessment (application), AI system impact assessment (application), lifecycle. This is where accuracy, robustness, cybersecurity evaluation deliverables land; where the release-gate is *operated*.
- **Clause 9 — Performance evaluation.** Monitoring, measurement, analysis, evaluation, internal audit, management review. Where post-market monitoring plans and post-market review reports land.
- **Clause 10 — Improvement.** Nonconformity and corrective action, continual improvement. Where serious-incident deliverables land.

**Annex A controls.** Annex A of 42001 is the AI-specific control catalogue an auditor may inspect. The catalogue is grouped (roughly) into policies for AI, internal organisation, resources for AI systems, assessing impacts, AI system life-cycle, data for AI systems, information for interested parties, use of AI systems, and third-party relationships. Every Annex A control declared applicable in the Statement of Applicability (SoA) becomes a candidate cross-tag on the map. `<!-- needs-research: cross-check the exact Annex A grouping in the published ISO/IEC 42001:2023 text and adjust names -->`

## EU AI Act row → 42001 clause mapping

| EU AI Act row (from chapter 02) | 42001 clause | 42001 Annex A control (candidate) | Rationale |
| --- | --- | --- | --- |
| `eu-ai-act.art9.plan` | 6.1.2, 6.1.3, 6.1.4 | A.6 (impact assessment), A.5.4 (risk assessment) — check current SoA IDs | Risk-management planning and impact assessment |
| `eu-ai-act.art9.harms` | 6.1.2, 8.2 | A.5.4 | AI risk assessment, application |
| `eu-ai-act.art9.residuals` | 6.1.3, 10.1 | A.5.5 (risk treatment) | Risk treatment and nonconformity |
| `eu-ai-act.art10.governance-plan` | 6.1.2, 7.5 | A.7 (data for AI systems) | Data governance sits under clause 6.1 planning and A.7 controls |
| `eu-ai-act.art10.bias-report` | 6.1.4, 8.3 | A.6 | Impact assessment for bias; operational execution |
| `eu-ai-act.art10.dataset-cards` | 7.5.3 | A.7 | Documented information for datasets |
| `eu-ai-act.art11.annex-iv.*` | 7.5, 8.2 | A.8 (information for interested parties) | Technical documentation as documented information |
| `eu-ai-act.art12.logging-design` | 7.5.3, 8.1 | A.8 | Documented information with retention |
| `eu-ai-act.art12.completeness-report` | 9.1 | A.8 | Monitoring and measurement of the AIMS |
| `eu-ai-act.art13.instructions-for-use` | 7.4, 7.5 | A.8 | Communication and documented information for external parties |
| `eu-ai-act.art14.oversight-design` | 8.1, 8.4 | A.9 (use of AI systems) | Operational planning; human oversight sits under A.9 |
| `eu-ai-act.art14.usability-report` | 9.1 | A.9 | Performance evaluation |
| `eu-ai-act.art15.accuracy-declaration` | 8.2, 9.1 | A.6 | Operation and performance evaluation |
| `eu-ai-act.art15.robustness-report` | 8.2, 9.1 | A.6 | Uses ISO/IEC 24029-2 method |
| `eu-ai-act.art15.cybersecurity-report` | 8.2, 9.1 | A.6 | Cross-references ISO/IEC 27001 controls |
| `eu-ai-act.art17.qms` | Clauses 4–10 as a set | (entire SoA) | 42001 is the QMS |
| `eu-ai-act.art26.deployer-tom-plan` | 8.1, 8.4 | A.9, A.10 (third-party) | Deployer is a third-party consumer of a provider's system |
| `eu-ai-act.art43.decision-record` | 5.3, 10.1 | A.5 | Leadership + accountability |
| `eu-ai-act.art47.declaration` | 7.5.3 | A.8 | Documented information for external parties |
| `eu-ai-act.art49.registration` | 5.3, 7.5 | A.8 | Filing action documented |
| `eu-ai-act.art61.incident-plan` | 10.1, 10.2 | A.9 | Nonconformity, corrective action |
| `eu-ai-act.art72.post-market-plan` | 9.1, 10.2 | A.9 | Monitoring, measurement, continual improvement |

`<!-- needs-research: the Annex A control identifiers above (A.5, A.6, A.7, A.8, A.9, A.10) are the standard groupings; confirm the current SoA identifiers against the published ISO/IEC 42001:2023 text and update -->`

Where a row hits multiple clauses (as most do), the `sibling_iso_clauses` field carries the list. Clause 8 rows are the busy ones: every operational deliverable lands there.

## ISO/IEC 23894 — AI risk-management method

23894 is *guidance* — it is not certifiable. It adapts ISO 31000 to AI-specific risk sources. The AIMS clause 6.1.2 (AI risk assessment) and clause 6.1.3 (AI risk treatment) *specify what the AIMS requires*; 23894 *specifies how you do it*.

The release-gate does not produce a separate 23894 deliverable — the harm inventory, residual-risk register, and risk-management plan under Article 9 are already the outputs. The map cross-tags them with 23894 clauses to make the method visible.

Typical cross-tag for the risk-management row:

```yaml
obligation_id: eu-ai-act.art9.harms
sibling_iso_clauses:
  - ISO/IEC 42001 6.1.2
  - ISO/IEC 42001 8.2
  - ISO/IEC 23894 6.4    # risk identification
  - ISO/IEC 23894 6.5    # risk analysis
  - ISO/IEC 23894 6.6    # risk evaluation
```

`<!-- needs-research: 23894 clause 6 sub-clauses in the published 2023 text — confirm identifier numbers 6.4 / 6.5 / 6.6 vs. 6.4.2 / 6.4.3 etc. and update -->`

23894 also carries a helpful appendix listing AI-specific risk sources (complexity of environment, degree of automation, lack of transparency, opacity, malicious use, etc.). The harm-inventory `applies_when` conditions should draw from this list rather than an ad-hoc taxonomy — it makes the deliverable audit-defensible.

## ISO/IEC 42005 — AI system impact assessment

42005 is the impact-assessment *method* the AIMS clause 6.1.4 (AI system impact assessment) and clause 8.3 (operational impact-assessment execution) refer out to. It intersects heavily with the EU AI Act's Article 27 fundamental-rights impact assessment (FRIA) — where the deployer is a public authority or otherwise triggered under Article 27, the FRIA can often be executed as a specialisation of a 42005 impact assessment.

Deliverables under 42005 on the map:

- `impact-assessment-report-v<N>.md` — the report itself, whose sections follow 42005's structure (scope, methodology, findings, treatments, residual position). `mod-105` chapter `04` walks the card-side of this artefact.
- `impact-assessment-review-log-v<N>.md` — cadence of review as the system evolves.

Typical cross-tag for the impact-assessment row:

```yaml
obligation_id: eu-ai-act.art9.impact-assessment
sibling_iso_clauses:
  - ISO/IEC 42001 6.1.4
  - ISO/IEC 42001 8.3
  - ISO/IEC 42005 clause 6   # scope and boundary
  - ISO/IEC 42005 clause 7   # method
  - ISO/IEC 42005 clause 8   # findings and treatments
```

`<!-- needs-research: 42005 was published in 2025; confirm clause identifiers 6 / 7 / 8 shape once the published text is on hand -->`

## ISO/IEC 25059 — SQuaRE quality-attribute vocabulary

25059 extends the SQuaRE quality model to AI systems. Its quality characteristics and sub-characteristics are the vocabulary the deliverables under Article 15 (accuracy, robustness, cybersecurity) and Article 13 (usability) are written in.

The typical characteristic set includes:

- Functional suitability (functional correctness, functional completeness, functional appropriateness) — under Article 15 accuracy
- Performance efficiency — for compute-cost / latency
- Compatibility — for GPAI models integrated into deployer systems
- Interaction capability (user assistance, user error protection, appropriate recognisability) — under Article 13 transparency and Article 14 human oversight
- Reliability (maturity, availability, fault tolerance, recoverability) — under Article 15 accuracy / robustness
- Security (confidentiality, integrity, non-repudiation, accountability, authenticity, resistance) — under Article 15 cybersecurity
- Maintainability — for lifecycle deliverables
- Portability
- AI-specific: functional adaptability, robustness (as a top-level characteristic), transparency, user controllability, intervenability

`<!-- needs-research: the AI-specific SQuaRE additions in 25059 differ subtly between draft and published text — confirm the current characteristic and sub-characteristic list -->`

The map uses 25059 characteristics as the *column labels* on the quality-attribute row block on the card (`mod-105`). Cross-tags:

- `eu-ai-act.art15.accuracy-declaration` → `ISO/IEC 25059 5.1 functional suitability`, `ISO/IEC 25059 5.5 reliability`
- `eu-ai-act.art15.robustness-report` → `ISO/IEC 25059 5.x AI robustness`
- `eu-ai-act.art15.cybersecurity-report` → `ISO/IEC 25059 5.6 security`
- `eu-ai-act.art13.instructions-for-use` → `ISO/IEC 25059 5.4 interaction capability`
- `eu-ai-act.art14.oversight-design` → `ISO/IEC 25059 5.x user controllability / intervenability`

## ISO/IEC 24029-2 — Robustness of neural networks (method)

24029-2 is the *method* the Article 15 robustness-report deliverable calls out to. Where 42001 clause 8.2 requires a robustness evaluation and 25059 names "robustness" as a quality characteristic, 24029-2 is the method-of-record for how you *measure* it.

24029-2 covers formal-method approaches (e.g., interval-bound propagation for robustness verification), statistical / empirical approaches (adversarial testing under specified perturbation classes), and their combination. It is method-heavy, and the specific measurement design will typically be owned by `model-evaluation-engineer`.

Cross-tag:

```yaml
obligation_id: eu-ai-act.art15.robustness-report
sibling_iso_clauses:
  - ISO/IEC 42001 8.2
  - ISO/IEC 42001 9.1
  - ISO/IEC 25059 5.x robustness
  - ISO/IEC 24029-2 clause 6   # methodology overview
  - ISO/IEC 24029-2 clause 7   # empirical methods
  - ISO/IEC 24029-2 clause 8   # formal methods (where applicable)
```

`<!-- needs-research: confirm 24029-2 top-level clauses (6, 7, 8) once the published 2023 text is on hand -->`

The 24029-2 tag is the release-gate's answer to "what does your robustness evaluation *mean*?" — the auditor pulls the tag, opens 24029-2, and reads the method.

## Adjacent standards worth naming (light cross-tags only)

- **ISO/IEC 5259 series** — data quality for analytics and ML. Cross-tagged onto `eu-ai-act.art10.governance-plan` and dataset-card rows.
- **ISO/IEC 8183** — data lifecycle framework. Cross-tagged onto dataset-card rows and lineage manifests.
- **ISO/IEC 42006** — accreditation requirements for AIMS certification bodies. Not on the map — it constrains who can *audit* the map, not the map's rows.
- **ISO/IEC 27001** — the cybersecurity management-system reference. Article 15 cybersecurity rows cross-tag to 42001 clause 8 and 25059 5.6, and also to 27001 controls where applicable — but 27001 is out of scope for the AIMS certificate and is owned by `ai-infra-security`.

## Worked example — Article 15 robustness end-to-end

```yaml
obligation_id: eu-ai-act.art15.robustness-report
instrument: eu-ai-act-2024-1689
article_or_clause: Article 15(1)(4)(5)
obligation_summary: Robustness of the AI system, including resilience against adversarial attempts
applies_when: high-risk provider
deliverable: robustness-evaluation-report-v3.md
deliverable_kind: report
owner_role: model-evaluation-engineer
signing_role: ai-evaluation-engineer
sibling_nist_rmf: [MEASURE-2.6]
sibling_nist_ai_600_1:
  - risk: information security (prompt-injection resilience)
sibling_iso_clauses:
  - ISO/IEC 42001 8.2
  - ISO/IEC 42001 9.1
  - ISO/IEC 25059 5.x robustness
  - ISO/IEC 24029-2 clause 7
tier_applicability: [tier-1, tier-2, tier-3]
status: covered
evidence_pointer: sha256:1a2b3c…
```

A reader can now walk from this single row into the EU AI Act text (Article 15), the NIST Playbook (MEASURE-2.6), the ISO/IEC 42001 clause 8.2 audit path, the ISO/IEC 25059 quality vocabulary, and the ISO/IEC 24029-2 robustness methodology — without opening any other artefact.

## Traps in the ISO crosswalk

- **Clause 6.1 activities are *planning*, not *execution*.** The plan lives under 6.1.2 / 6.1.3 / 6.1.4; the execution lives under 8.2 / 8.3. A row that only tags 6.1 has not actually shown its evaluation happened.
- **Documented information (clause 7.5) is a catch-all.** Nearly every deliverable can be tagged 7.5. That is fine — but the *specific* clause carrying the substantive obligation (6, 8, 9, 10) has to be tagged too, or the auditor cannot find the requirement.
- **Annex A is *selectable*.** An organisation's Statement of Applicability picks the Annex A controls it applies. A cross-tag onto an Annex A control the SoA excludes is a gap; the map should carry an `soa_status` sub-field on Annex A tags.
- **23894 clause numbers change between draft and published.** Pin the standard version year on every tag: `ISO/IEC 23894:2023 6.5`.
- **42005 is 2025.** For older programs the impact-assessment method may pre-date 42005 and use a bespoke or GDPR-DPIA-derived method. The map should record `impact_assessment_method` explicitly.
- **25059 characteristics are not metrics.** They are quality *attributes* the metrics measure against. Confusing them with metrics is the fastest way to make the quality section of a card look wrong.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — argument nodes cite ISO clauses.
- `mod-103` (release-gate architecture) — the gate schema carries `iso_clauses` per obligation, matching the `sibling_iso_clauses` field here.
- `mod-104` (evidence pipeline) — evidence artefacts carry ISO clause tags for retrieval.
- `mod-105` (cards for external audiences) — the card's quality-attribute row block uses 25059 vocabulary; the impact-assessment section uses 42005 structure.
- `mod-107` (sector-regulated assurance) — sector standards cross-reference 42001 where applicable.
- `mod-109` (third-party evaluator interface) — a notified body under Article 43 will typically be accredited against 42006 to audit 42001 conformity; the map's ISO tags make the audit walkable.
- `mod-112` (owning an assurance program) — 42001 certification is one of the program-level milestones.

## Summary

- Each EU AI Act row on the map picks up a `sibling_iso_clauses` field carrying one or more clause references from 42001, 23894, 42005, 25059, 24029-2.
- 42001 clauses 4–10 are the audit spine; Annex A controls attach where the SoA declares them applicable.
- 23894 is the method reference for AI risk activities; 42005 is the method reference for AI impact activities; both are guidance, not certifiable.
- 25059 provides the quality-attribute vocabulary (functional suitability, reliability, security, interaction capability, robustness, user controllability, intervenability) that Article 13, 14, and 15 rows are labelled with.
- 24029-2 is the method-of-record for the Article 15 robustness deliverable.
- Version and SoA status must be pinned per tag — clause identifiers evolve, and Annex A control applicability is per-organisation.
- Exercise 03 walks the ISO crosswalk against the scenario from exercises 01–02.
