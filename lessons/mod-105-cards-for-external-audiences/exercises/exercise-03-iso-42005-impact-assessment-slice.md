# exercise-03: ISO/IEC 42005 Impact Assessment Slice

**Estimated effort:** 3 hours

## Objective

Author the **ISO/IEC 42005 impact-assessment section** of your system card (from exercise `02`) as a compact, machine-referenceable projection of an underlying impact-assessment artefact. Every finding on the section must be traceable — by content-address — to (a) a substructure digest of the impact-assessment document, (b) at least one supporting evidence node, and (c) an assurance-case goal.

## Prerequisites

- Chapter [`04-iso-iec-42005-impact-assessment-section.md`](../04-iso-iec-42005-impact-assessment-section.md).
- Exercises [`exercise-01`](exercise-01-model-card-for-a-regulated-product.md) and [`exercise-02`](exercise-02-system-card-composition-from-evidence-tree.md) — this exercise adds to the same system card.
- Skim access to [ISO/IEC 42005:2025](https://www.iso.org/standard/42005) (the abstract on the ISO page is the required reading; the standard itself is authoritative). For the EU AI Act Article 27 stretch, the [EU AI Act text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) Article 27.

## Problem statement

Produce the ISO/IEC 42005 impact-assessment section of the system card. Do this as *two* linked artefacts: (a) a `impact-assessment-document.md` that is the underlying artefact the section is a projection of (imagine it as the output of a workshop your program actually ran), and (b) the `impact-assessment-section.md` and `head-impact-block.yaml` that appear in the card body and head.

You are *not* running a real ISO/IEC 42005 process. You are producing the output shape a real process would produce. Use your chosen scenario (from exercise `01`) as the system in scope.

## Requirements

Produce five artefacts.

### 1. `impact-assessment-document.md`

The full underlying artefact. Structure to the five ISO/IEC 42005 sections chapter `04` names:

- **§Scope.** System scope, intended use (extended and constrained), deployment context, affected stakeholders (users, decision subjects, third parties), temporal frame, jurisdictions in scope, review cadence.
- **§Methodology.** The methodology the assessment used (harms-and-benefits HAZOP, structured brainstorming with facilitator, scenario analysis — pick one and document); who participated (roles, not names); the evidence sources drawn on (red-team reports, harm inventory, historical incidents, stakeholder engagement); the scoring rubric with a bounded severity × likelihood matrix.
- **§Findings.** At least **eight findings**, each with:
  - `finding_id` (stable, e.g., `imp:IAI-2026-05-07:F-014`).
  - Impact class (positive / adverse; individual / group / societal; direct / indirect).
  - Affected stakeholder category.
  - Severity classification with the rubric row cited.
  - Likelihood classification with the rubric row cited.
  - Composite risk position and rationale.
  - Evidence pointers (placeholder digests are acceptable if marked).
  - `sacm_artifact_id` (matches head entry).
- **§Treatments.** For each finding, one of: mitigation (with cited control ID and eval-evidence digest), monitoring (with signal + threshold + escalation contact), acceptance (with named accountable role and rationale), or elimination-by-scope (with scope-restriction reference). Every finding with severity above `minor` has a treatment.
- **§Residual position.** Aggregate residual-risk position (a narrative bounded by the scoring frame), accountable role, review triggers, next scheduled review.

Length: 15–30 pages equivalent. This is the source-of-truth document; the section on the card is a projection.

### 2. `impact-assessment-section.md`

The section as it appears in the system card body. Compact — 2–4 pages. Every finding named on the section maps by ID to a finding in `impact-assessment-document.md`. Every finding cites its severity, its likelihood, its treatment status, and — for the *public variant* — the stakeholder category rather than the specific stakeholder identity.

Cross-reference §2 (foreseeable misuse) and §4 (quality attributes) of the system card body from exercise `02`; explicit `misuse-M-… ↔ imp:IAI-F-…` and `quality-attribute:{characteristic}.{metric} → imp:IAI-F-…` links.

### 3. `head-impact-block.yaml`

The `impact_assessment` block for the system card's head. Follows chapter `04`'s shape:

```yaml
impact_assessment:
  document_id: "iai:internal-assistant/rc-2026-05-07"
  document_content_address: "sha256:..."
  standard: "iso-iec-42005:2025"
  standard_clauses:
    scope: "sha256:.../scope"
    methodology: "sha256:.../methodology"
    findings: "sha256:.../findings"
    treatments: "sha256:.../treatments"
    residual: "sha256:.../residual"
    monitoring: "sha256:.../monitoring"
  methodology: { ... }
  findings: [ ... ]
  treatments: [ ... ]
  residual: { ... }
```

At least eight findings, at least eight treatments, and a complete residual position. Every `finding_id` on the card and in the document is present in `findings[]` here.

### 4. `traceability-matrix.md`

A matrix that shows, for each finding, the three-way binding chapter `04` requires:

| finding_id                | document substructure digest       | evidence pointers                  | case node                                        |
|---------------------------|------------------------------------|------------------------------------|--------------------------------------------------|
| imp:IAI-2026-05-07:F-014  | sha256:88af.../findings/F-014       | sha256:4a1c…, sha256:9df1…         | goal:G1.S4.G-impact-F-014-evaluated              |
| imp:IAI-2026-05-07:F-014  | sha256:88af.../treatments/F-014     | sha256:c33d…                        | goal:G1.S4.G-impact-F-014-treated                |
| imp:IAI-2026-05-07:F-021  | sha256:88af.../findings/F-021       | sha256:ec1d…                        | goal:G1.S4.G-impact-F-021-evaluated              |
| ...                       | ...                                 | ...                                 | ...                                              |

Every row is a walkable path chapter `04`'s six-step audit walk would traverse.

### 5. `rubric-v1.md`

The severity × likelihood scoring rubric as its own signed, content-addressed artefact. Bounded ordinal scales (e.g., `minor / moderate / major / catastrophic`; `unlikely / possible / likely / near-certain`) with anchored descriptions for each row. The rubric is what the findings' severity and likelihood classifications cite. Version it (`rubric-v1`); if you change it in a future release, the version bumps.

## Starter guidance

- **Write the underlying document first, then the section.** The section is a projection; you cannot project what you have not authored.
- **Anchor severity and likelihood rows.** "Moderate severity — impact on 100–10,000 individuals; recovery-with-effort" is anchored; "moderate — you know it when you see it" is not. Anchored rows are what let two releases stay comparable.
- **A finding is not a fear.** A finding cites evidence — a subgroup metric, a red-team result, an external report, a stakeholder interview. A finding that cites only "we discussed it" is a hypothesis; upgrade it to a finding by citing evidence or downgrade it out of the section.
- **Treatments name specific controls.** "Add a guardrail" is not a treatment; "control-id `ctrl:guardrail:multilingual-response-quality-v3` with eval evidence at `sha256:c33d…` showing threshold met at 4.1% ± 0.3%" is a treatment.
- **Monitoring names signals with thresholds.** "We will monitor" is not monitoring; "signal `creator-attribution-refusal-rate` breaching `> 4% weekly` escalates to `content-policy-lead@example.corp`" is.
- **The residual position aggregates over treated findings.** If any finding is above the acceptance floor with no named escalation, the residual position is not `acceptable`. Do not fudge this.
- **Use the same finding IDs everywhere.** `finding_id = imp:IAI-2026-05-07:F-014` on the section, in the head, in `traceability-matrix.md`, and in the case. A single mismatched ID means the walk fails.

## Acceptance criteria

You have succeeded if:

- `impact-assessment-document.md` covers all five ISO/IEC 42005 sections; §Findings has at least eight findings with the required per-finding fields; §Treatments carries a treatment for every finding above the acceptance floor.
- `impact-assessment-section.md` compresses the document into 2–4 pages while preserving every finding ID and treatment status; cross-references to §2 and §4 of the system card body are present.
- `head-impact-block.yaml` conforms to chapter `04`'s shape; `document_content_address` and every substructure digest are populated (placeholders acceptable if marked); every finding on the card is in `findings[]`.
- `traceability-matrix.md` walks every finding to (a) a document substructure digest, (b) at least one evidence pointer, (c) a case node. No finding is missing any of the three columns.
- `rubric-v1.md` is versioned and content-addressed; every severity and likelihood classification in the findings cites a specific rubric row.
- A peer reviewer can pick any finding on `impact-assessment-section.md`, walk to the substructure digest, find the evidence pointers, and reach a case node — chapter `04`'s six-step walk succeeds.

## Stretch goals

- **Author the Article 27 FRIA specialisation.** For a scenario in scope for EU AI Act Article 27 (deployers of high-risk systems), produce a `fria.md` document and a `fria_content_address` field on the head that specialises the base impact assessment with the Article 27 required fields (categories of natural persons affected; specific risks of harm; human-oversight measures; measures to take if the risk materialises; internal governance and complaints arrangements). Cite each Article 27 sub-paragraph.
- **Diff two impact-assessment releases.** Produce a hypothetical `rc-2026-08-14` release of the impact assessment (a version later than the exercise's `rc-2026-05-07`). Diff finding-by-finding: which findings are unchanged, which have re-scored severity or likelihood, which are new, which are retired-with-rationale. This is the shape of the ISO/IEC 42001 clause 8.1 re-assessment output.
- **Bind the impact assessment to a stakeholder-engagement report.** Author a short `stakeholder-engagement-report.md` (2–4 pages) that documents an engagement session (real or fictitious-but-plausible), and cite it as an evidence pointer for at least two findings. Stakeholder engagement is one of the harder parts of a defensible ISO/IEC 42005 methodology.
- **Publish the aggregate rate but redact the raw findings.** For the *public* variant of the card, produce a `redacted-impact-section.md` that shows only the aggregate residual position and the count of findings per severity class — no per-finding IDs or stakeholder-category detail — with a `redaction_manifest` row explaining why. This foreshadows exercise `05`.
- **Cross-reference `harm-inventory` from the risk-engineering peer.** Chapter `06` of mod-102 named the risk-engineering peer's harm inventory as an evidence source. Cite the harm inventory as a `harm-id` → `finding-id` mapping in the traceability matrix.
