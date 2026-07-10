# The ISO/IEC 42005 Impact-Assessment Section

## Motivation

An assurance card can carry a beautifully-written safety-evidence summary and still leave a regulator or notified body without the artefact they legally need. Under the EU AI Act Article 27 (Fundamental Rights Impact Assessment for deployers of high-risk systems), under ISO/IEC 42001 clause 6.1.4 (AI system impact assessment), and under many sectoral rules that treat impact analysis as a first-class obligation, the reviewer expects a *structured* impact assessment they can walk — not a paraphrase inside the safety section.

[ISO/IEC 42005:2025 — *Information technology — Artificial intelligence — AI system impact assessment*](https://www.iso.org/standard/42005) is the international standard that operationalises what that structured impact assessment has to look like. This chapter shows how to produce an ISO/IEC 42005 impact-assessment output section inside a system card such that every finding is traceable — by content-address — to a concrete evidence node in the underlying GSN case (mod-102) and to a digest in the evidence store (mod-104).

The section is *not* a summary. It is a compact, machine-referenceable projection of the underlying impact-assessment artefact. Chapter `03`'s six sections carried claims; this chapter's section carries impacts, with the same audit-walk discipline.

## What ISO/IEC 42005 fixes

ISO/IEC 42005 (published 2025) treats the AI system impact assessment as a documented process producing a documented output. It is a *sibling* to ISO/IEC 42001 (the management-system standard, mod-101 chapter `03`), a *specialisation* of ISO/IEC 42006 conformance assessments, and a *complement* to ISO/IEC 23894 (AI risk management guidance). ISO/IEC 42001 clause 6.1.4 requires an AI-system impact assessment; ISO/IEC 42005 tells you how to do it.

Three shapes ISO/IEC 42005 fixes are worth knowing before you can write the card section:

- **Scope and boundaries.** The impact assessment starts by fixing the system's scope (what the system is), the intended use (extended and constrained), the deployment context, the affected stakeholders (users, subjects of decisions, third parties), and the temporal frame (initial deployment, updates, decommissioning).
- **Process activities.** The standard's clauses walk the assessor through activities: identifying potential impacts (both benefits and harms), analysing them, evaluating severity and likelihood, treating them (mitigations, monitoring, acceptance), and documenting decisions.
- **Output shape.** The impact assessment output is a documented artefact with named sections — scope, methodology, findings, treatments, residual position, monitoring, review-cycle — that the AI management system (ISO/IEC 42001 clause 7.5) retains and reviews.

The full impact assessment can be dozens to hundreds of pages. What lives on the card is a *section* whose job is to give the reviewer enough structure to (a) understand the impact assessment's shape, (b) reach the specific findings that are load-bearing for this release, and (c) verify those findings against the evidence store.

<!-- needs-research: verify the exact numbered clause structure of ISO/IEC 42005:2025 (published version) and cite specific clauses for scope, methodology, findings, and output; the current draft references clause-level activities generically. -->

## The card section, structured

The impact-assessment section of the system card carries five sub-sections. Each maps to a part of the underlying ISO/IEC 42005 output artefact by content-address.

### §Impact-01 — Scope, stakeholders, and temporal frame

**Discharges:** the case node `goal:G1.S1.G-42005-scope`.

**Body content:** the system's impact-assessment scope (mirrors the system card's §1 identity but adds *impacted parties* — users, decision subjects, third parties, non-users affected by outputs); the temporal frame the assessment covers (initial release, planned updates, decommissioning horizon); the jurisdictions in scope for the assessment (mod-106); the review cadence.

**Head binding:**
```yaml
impact_assessment:
  document_id: "iai:internal-assistant/rc-2026-05-07"
  document_content_address: "sha256:88af..."
  standard: "iso-iec-42005:2025"
  standard_clauses:
    scope: "sha256:88af.../scope"                # substructure digest of the scope section
    methodology: "sha256:88af.../methodology"
    findings: "sha256:88af.../findings"
    treatments: "sha256:88af.../treatments"
    residual: "sha256:88af.../residual"
    monitoring: "sha256:88af.../monitoring"
```

Two invariants for the scope section:

- Every stakeholder category named in the card is present in the underlying impact-assessment artefact. Adding a category on the card that the artefact does not carry is broken.
- The temporal frame on the card matches the artefact. A card that claims to cover "12 months" while the artefact covers "6 months" is broken.

### §Impact-02 — Methodology and provenance of findings

**Discharges:** the case node `goal:G1.S3.G-42005-methodology-sound`.

**Body content:** the methodology the impact assessment used (structured-brainstorming with a facilitator, hazard-and-operability-style HAZOP walk, harms-and-benefits inventory, scenario analysis, external stakeholder engagement); who participated (roles, not names — see chapter `07` on redaction); what evidence sources the assessment drew on (existing red-team findings, historical incidents, external threat intelligence, stakeholder interviews); the decision rule the assessment applied (severity × likelihood rubric, ordinal scoring, or a scored rubric the program has written down); the confidence-level frame used to report findings.

**Head binding:**
```yaml
impact_assessment:
  methodology:
    approach: "harms-and-benefits-hazop"      # program choice; write it down
    scoring_rubric_content_address: "sha256:5a11..."
    facilitator: "iso-42005-lead@example.corp"
    participant_role_list_content_address: "sha256:2b3c..."
    evidence_sources:
      - kind: "red-team-report"
        content_address: "sha256:c33d..."
      - kind: "harm-inventory"
        content_address: "sha256:e01d..."
      - kind: "historical-incident-log"
        content_address: "sha256:1234..."
      - kind: "stakeholder-engagement-report"
        content_address: "sha256:9abc..."
```

The methodology sub-section is what a third-party evaluator uses to decide whether the impact assessment's findings are worth trusting. A card that omits methodology and jumps straight to findings is asking the reader to trust the process without evidence. Chapter `07` shows how to redact participant identities without redacting the methodology.

### §Impact-03 — Findings — impacts identified and evaluated

**Discharges:** the per-impact case nodes `goal:G1.S4.G-impact-{id}-evaluated`.

**Body content:** a structured list of findings. Each finding carries:

- A finding identifier (`imp:IAI-2026-05-07:F-014` — stable across variants).
- The impact class (positive / adverse; individual / group / societal; direct / indirect).
- The affected stakeholder category.
- The severity classification (per the program's rubric — e.g., minor / moderate / major / catastrophic) with the rubric row cited.
- The likelihood classification, similarly.
- The composite risk position and the rationale.
- The evidence pointers that support the classification (a red-team report, a stakeholder interview, an eval result showing the mitigation works).

The card renders this as a table (or a bulleted list). What matters is that every finding has both an ID and a pointer.

**Head binding:**
```yaml
impact_assessment:
  findings:
    - finding_id: "imp:IAI-2026-05-07:F-014"
      class: "adverse-individual-direct"
      stakeholder: "end-user-with-limited-english-proficiency"
      severity: "moderate"
      severity_rubric_row: "iai-rubric-v2:severity:row-3"
      likelihood: "likely"
      likelihood_rubric_row: "iai-rubric-v2:likelihood:row-2"
      composite: "elevated"
      evidence_pointers:
        - eval_report_content_address: "sha256:4a1c..."     # subgroup-metric report
        - stakeholder_interview_content_address: "sha256:9df1..."
      sacm_artifact_id: "art:iai-finding:rc-2026-05-07:F-014"
    - finding_id: "imp:IAI-2026-05-07:F-021"
      class: "adverse-group-indirect"
      stakeholder: "content-creator"
      severity: "moderate"
      severity_rubric_row: "iai-rubric-v2:severity:row-3"
      likelihood: "possible"
      likelihood_rubric_row: "iai-rubric-v2:likelihood:row-3"
      composite: "medium"
      evidence_pointers:
        - external_report_content_address: "sha256:ec1d..."
      sacm_artifact_id: "art:iai-finding:rc-2026-05-07:F-021"
    # ...
```

Three invariants over findings:

- Every finding on the card is a finding in the underlying ISO/IEC 42005 artefact by ID. Adding a finding on the card that the artefact does not carry is broken.
- Every finding's severity and likelihood cite a rubric row that the rubric-content-address itself carries. Ad-hoc classifications are broken.
- Every finding's evidence pointers resolve in the store. A finding without evidence is a claim, not a finding.

### §Impact-04 — Treatments — mitigations, monitoring, or acceptance

**Discharges:** the per-impact treatment case nodes `goal:G1.S4.G-impact-{id}-treated`.

**Body content:** for each finding, one of four treatment decisions:

- **Mitigation** — a specific control shipped (guardrail, sampling constraint, refusal policy, deployer contract clause), with the evidence-pointer showing the control works.
- **Monitoring** — the finding is not eliminated at release but the post-market plan monitors for it, with a named signal and threshold (mod-110).
- **Acceptance** — the residual position is accepted with sign-off from a named accountable role; the acceptance rationale is cited.
- **Elimination-by-scope** — the risk is eliminated by restricting the deployment scope (the deployer contract prohibits a use case, the tier restricts the deployment mode); the scope restriction is cited.

**Head binding:**
```yaml
impact_assessment:
  treatments:
    - finding_id: "imp:IAI-2026-05-07:F-014"
      treatment: "mitigation"
      controls:
        - control_id: "ctrl:guardrail:multilingual-response-quality-v3"
          eval_evidence_content_address: "sha256:c33d..."
      after_treatment_composite: "medium"
    - finding_id: "imp:IAI-2026-05-07:F-021"
      treatment: "monitoring"
      monitoring_plan:
        signal: "creator-attribution-refusal-rate"
        threshold: "> 4% weekly"
        escalation: "content-policy-lead@example.corp"
      after_treatment_composite: "medium"
    # ...
```

Two invariants over treatments:

- Every finding that carries any severity above `minor` has a treatment. A finding with no treatment and a severity above the acceptance floor is a broken decision (the card cannot ship until this is resolved).
- Every mitigation cites an eval-evidence content-address that demonstrates the mitigation works. An unproven mitigation is a claim, not a mitigation.

### §Impact-05 — Residual position and review

**Discharges:** the case node `goal:G1.S4.G-residual-acceptable`.

**Body content:** the aggregate residual-risk position (a narrative — not a single number — but with a bounded scoring frame the reader can walk), the accountable roles for residual acceptance, the review triggers (post-market signals that would re-open the assessment; mod-110), and the scheduled review cadence.

**Head binding:**
```yaml
impact_assessment:
  residual:
    aggregate_position: "acceptable-with-monitoring"
    accountable_role: "chief-risk-officer"
    review_triggers:
      - signal: "adverse-safety-incident"
        threshold: "1 confirmed per quarter"
      - signal: "post-market-drift"
        threshold: "> 3% delta on primary-quality-attribute"
    next_scheduled_review: "2026-10-11"
```

Two invariants:

- The residual position aggregates over the treated findings; if any finding has an `after_treatment_composite` above the acceptance floor without a named escalation, the residual position is not `acceptable`.
- The review triggers name post-market signals (mod-110); a residual position with no review triggers is broken.

## Traceability walk end-to-end

A reviewer opening the impact-assessment section and following a single finding (`F-014`) walks:

1. **Read the finding on the card body** — severity `moderate`, likelihood `likely`, composite `elevated`, mitigation shipped.
2. **Follow the head pointer** — `impact_assessment.findings[finding_id=F-014].evidence_pointers`.
3. **Resolve the finding in the impact-assessment artefact** — `impact_assessment.document_content_address` at `sha256:88af…` carries the full finding text under section `findings.F-014`; substructure digest (`sha256:88af…/findings/F-014`) proves the card's paraphrase matches.
4. **Resolve the supporting evidence** — the subgroup-metric report at `sha256:4a1c…` and the stakeholder interview at `sha256:9df1…` are fetched and re-hashed against the recorded digests.
5. **Resolve the mitigation** — the guardrail-eval report at `sha256:c33d…` is fetched and confirms the guardrail meets its threshold.
6. **Reach the assurance case** — the `sacm_artifact_id = art:iai-finding:rc-2026-05-07:F-014` maps into the case at `goal:G1.S4.G-impact-F-014-evaluated` and its `G-impact-F-014-treated` sibling.

The section is defensible only if the walk succeeds for *every* finding on the card. A card that names ten findings but only three walk to the case has seven undischarged claims.

## Interaction with other card sections

The impact-assessment section does not stand alone. It sits inside the system card and shares content with three other sections; the boundaries matter.

- **vs §2 (intended purpose / foreseeable misuse).** The intended-purpose section names use categories; the impact-assessment section names *impacts* on stakeholders. A misuse pathway in §2 may be the *cause* of a finding in §Impact-03; the two sections cross-reference by ID (`misuse-M-018 → imp:IAI:F-014`).
- **vs §4 (quality attributes).** A quality attribute is a *property* of the system; an impact is a *consequence* on a stakeholder. A quality-attribute finding (per-subgroup accuracy is 12 points below top-line) is the *evidence* for an impact finding (adverse impact on limited-English-proficiency users). Chapter `05` returns to the linkage.
- **vs §5 (safety-evidence summary).** A safety evaluation is *what was done*; an impact finding is *what was found*. The safety-evidence summary carries the red-team methodology; the impact-assessment findings section carries the specific harms identified. The two sections share content-addresses for the underlying reports.

Keeping these boundaries clean prevents the card from double-counting evidence and lets the reviewer walk without confusion.

## Interaction with EU AI Act Article 27 FRIA

For deployers of high-risk systems in scope for the EU AI Act, Article 27 requires a Fundamental Rights Impact Assessment (FRIA). ISO/IEC 42005 is the international-standard scaffolding on which many providers and deployers align their internal impact-assessment process; the FRIA is the specific *Article 27 output artefact* the deployer submits or holds available.

The card treats the FRIA as a *specialisation* of the ISO/IEC 42005 output — same structure, additional fields the Article 27 text requires (categories of natural persons likely to be affected; specific risks of harm; human-oversight measures; measures to take if the risk materialises; internal governance and complaints arrangements). A card that supports Article 27 deployers carries the FRIA as an optional `impact_assessment.fria_content_address` pointing at the specialised artefact.

<!-- needs-research: confirm whether the FRIA output has a formal template published by the Commission or by a designated body (as of 2026-Q3), and cite the reference. AI Act Article 27 fixes contents but the template itself may be under development. -->

## Anti-patterns

- **Findings without evidence.** A finding whose only support is "we thought about it in a workshop" fails the trace walk. Every finding cites at least one evidence-content-address.
- **Rubric drift.** Using an ad-hoc severity classification instead of the program's written rubric row breaks between releases; two releases become non-comparable.
- **Aggregate-only residual position.** An impact-assessment section that reports only "residual risk: acceptable" without carrying per-finding treatments is not walkable. The residual position aggregates *over* the findings; it does not replace them.
- **Missing temporal frame.** An impact assessment that does not name its temporal scope (initial release / planned updates / decommissioning) will not survive a mid-cycle re-review. Chapter `06` of mod-110 (post-market) returns to this.
- **FRIA collapsed into the base impact assessment.** If the release is in scope for Article 27, the FRIA carries fields the base impact assessment does not require. Merging them silently means the FRIA becomes ambiguous. Keep them as two artefacts, the FRIA specialising the base.

## Summary

- The ISO/IEC 42005 impact-assessment section is a compact, machine-referenceable projection of the underlying impact-assessment artefact, structured in five sub-sections: scope, methodology, findings, treatments, residual position.
- Every finding is bound by ID to the underlying artefact by content-address, and every finding cites at least one evidence pointer that resolves in the store.
- The section sits alongside §2 (intended purpose / foreseeable misuse), §4 (quality attributes), and §5 (safety-evidence summary); cross-references keep the boundaries clean.
- For EU AI Act Article 27 deployers, the section carries an optional FRIA specialisation content-address; the FRIA specialises the base impact assessment with the Article 27 required fields.
- A reviewer walks any finding from the card body to the artefact substructure digest to the supporting evidence to the case node in six steps.
- Chapter `05` picks up the quality-attribute spine that the findings' supporting evidence often rests on.
