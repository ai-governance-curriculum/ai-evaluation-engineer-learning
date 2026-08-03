# exercise-03: ISO/IEC Clauses Crosswalk

**Estimated effort:** 3 hours

## Objective

Extend the map from exercises `01` and `02` with the **ISO/IEC clause cross-tag** — for every row (anchor rows and GenAI-Profile rows alike), name the ISO/IEC 42001 clauses (and Annex A controls) an auditor would inspect the deliverable under, plus the method-guidance references from ISO/IEC 23894 (risk), ISO/IEC 42005 (impact assessment), ISO/IEC 25059 (quality attributes), and ISO/IEC 24029-2 (robustness). Then draft the Statement of Applicability (SoA) fragment that declares which Annex A controls the programme is applying.

The output is what an ISO/IEC 42001 internal auditor (or, once you certify, an ISO/IEC 42006-accredited external auditor) picks up. From a single row they can walk to the clause, the control, the method reference, and the deliverable.

## Prerequisites

- Chapter [`04-iso-clauses-crosswalk.md`](../04-iso-clauses-crosswalk.md).
- Exercises [`exercise-01`](exercise-01-eu-ai-act-obligation-to-deliverable-map.md) and [`exercise-02`](exercise-02-nist-rmf-genai-profile-crosswalk.md) — this exercise extends the map they produced.
- Skim access to the current published texts of ISO/IEC 42001:2023, ISO/IEC 23894:2023, ISO/IEC 42005:2025, ISO/IEC 25059:2023, and ISO/IEC 24029-2:2023. If the standard text is not available in your environment, work from the ISO abstract pages (linked in `resources.md`) and mark specific clause numbers `<!-- needs-research: … -->`.
- Familiarity with the Harmonised Structure (HS) that ISO management-system standards use — clauses 4 (context), 5 (leadership), 6 (planning), 7 (support), 8 (operation), 9 (performance evaluation), 10 (improvement).

## Problem statement

Take the map from exercise `02` and extend every row with the ISO clause cross-tag columns. Then produce a Statement of Applicability fragment that declares, per Annex A control, whether the programme applies it (`in-scope`), excludes it with justification (`out-of-scope`), or defers it (`deferred`). The SoA fragment is the artefact the auditor holds you to: any cross-tag onto an Annex A control the SoA excludes is a gap.

You may (and should) also draft the **method-of-record declaration** for the four method-standards: for each of 23894, 42005, 25059, and 24029-2, state which specific method your programme uses on which specific deliverable. This is what makes the cross-tag *walkable* — a reader can pick 24029-2 clause 7 and see that it corresponds to your robustness report's `adversarial-testing.md` methodology, produced by `model-evaluation-engineer`.

## Requirements

Produce four artefacts.

### 1. `iso-extended-map.yaml`

The exercise-`02` map, extended with the ISO cross-tag columns for every row. New / updated fields per row:

- `sibling_iso_clauses` — list of clause references in the shape `<standard>:<year> <clause>`. Examples: `"ISO/IEC 42001:2023 8.2"`, `"ISO/IEC 42001:2023 A.6.2.4"`, `"ISO/IEC 23894:2023 6.5"`, `"ISO/IEC 42005:2025 clause 7"`, `"ISO/IEC 25059:2023 5.6"`, `"ISO/IEC 24029-2:2023 clause 7"`.
- `iso_soa_status` — map of Annex A control ID → `in-scope | out-of-scope | deferred`, for every Annex A control tagged on the row. The value on the row must match the SoA (§3 below).
- `iso_method_pin` — where the row cross-tags to a method standard (23894, 42005, 25059, 24029-2), the specific programme-side method reference the ISO standard is providing method-of-record for. Example: `iso_method_pin: { "ISO/IEC 24029-2:2023 clause 7": "methods/robustness-perturbation.md" }`.
- `iso_rationale` — a one-sentence rationale for the primary clause tag (why is 8.2 on this row?), analogous to `rmf_rationale` from exercise `02`.

The map header gains `frameworks_pinned.iso-iec-42001`, `.iso-iec-23894`, `.iso-iec-42005`, `.iso-iec-25059`, and `.iso-iec-24029-2` — each with the year of the version-of-record.

### 2. `iso-cross-tag-rationales.md`

Analogous to `nist-rmf-cross-tag-rationales.md` from exercise `02`: a one-line rationale per row for its primary ISO clause tag.

| obligation_id | primary sibling_iso_clauses | rationale |
| --- | --- | --- |
| `eu-ai-act.art9.plan` | `ISO/IEC 42001:2023 6.1.2, 6.1.3` | Risk-management planning under AIMS clause 6 |
| `eu-ai-act.art10.governance-plan` | `ISO/IEC 42001:2023 6.1.2, 7.5, A.7` | Data governance planning + documented information + A.7 data controls |
| `eu-ai-act.art15.robustness-report` | `ISO/IEC 42001:2023 8.2, 9.1; ISO/IEC 24029-2:2023 clause 7` | Operational execution + performance evaluation, with 24029-2 method of record |
| … | … | … |

Every row must appear. Where a row tags to Annex A controls, the rationale states which SoA status applies.

### 3. `statement-of-applicability.yaml`

A Statement of Applicability fragment covering every Annex A control your map cross-tags. For each control:

- `control_id` — the Annex A identifier (e.g., `A.5.4`, `A.6.2.4`, `A.7.3`, `A.8.2`, `A.9.3`, `A.10.1` — check identifiers against the current ISO/IEC 42001:2023 text and mark `<!-- needs-research: … -->` where the exact identifier is not verified).
- `control_title` — the short name from Annex A.
- `status` — `in-scope | out-of-scope | deferred`.
- `justification` — one to three sentences explaining the status. For `out-of-scope`, this must be substantive (Annex B implementation guidance uses "sourced not developed AI systems" as an example of an exclusion; your programme will have its own analogues).
- `deliverable_refs` — list of `obligation_id`s whose deliverables demonstrate the control. Empty for excluded controls.
- `owner_role` — the programme role responsible for maintaining the control's implementation.

The SoA is the artefact the auditor consults before opening the map. It must be internally consistent: no map row can cross-tag an `out-of-scope` control.

### 4. `method-of-record.md`

For each of the four method standards, a short (half-page each) declaration of the programme's method-of-record:

- **ISO/IEC 23894 — AI risk management.** Which specific 23894 clauses does the harm-inventory / risk-management activity follow? Which deliverable is the output? What is the cadence of re-execution?
- **ISO/IEC 42005 — AI system impact assessment.** Which 42005 clauses shape the impact-assessment section structure? What is the relationship to Article 27 FRIA (if in scope)? Which deliverable is the output?
- **ISO/IEC 25059 — SQuaRE quality attributes.** Which 25059 characteristics does the programme measure against? Which deliverables carry the quality-attribute-side of the evaluation (cross-reference the card-side in `mod-105`)?
- **ISO/IEC 24029-2 — Neural-network robustness.** Which 24029-2 clauses does the robustness evaluation methodology follow (formal vs. empirical)? Which perturbation classes are covered? Which deliverable is the report?

For each, note where you are unable to pin exact clause identifiers (`<!-- needs-research: … -->`).

## Starter guidance

- **Clause 6 (planning) ≠ clause 8 (operation).** A row that only cites 6.1.x has not shown its evaluation happened. Every evaluated deliverable needs at least one clause 8 or clause 9 tag.
- **Clause 7.5 is a catch-all.** Almost every deliverable is documented information. That is fine, but you must *also* cite the specific substantive clause (6, 8, 9, or 10). A row tagged only 7.5 has hidden the substantive obligation.
- **Annex A control IDs move.** The exact identifiers in the published ISO/IEC 42001:2023 Annex A are stable, but the *grouping* names sometimes differ between the standard text and secondary literature. Cite the ID; mark `<!-- needs-research: … -->` if the exact identifier is not verified against the standard text.
- **Method standards are guidance, not certifiable.** 23894, 42005, 25059, 24029-2 do not carry SoA controls — they are referenced by 42001 clauses. Their cross-tag on a row is about *methodology traceability*, not *audit scope*.
- **25059 characteristics are attributes, not metrics.** The characteristic is `reliability`; the metric is (say) `p99 latency` or `error rate on X`. Do not conflate.
- **24029-2 splits formal / empirical.** Empirical robustness (adversarial testing under perturbation classes) is the usual case; formal robustness (interval-bound propagation, certification) is less common. State which your row is doing.
- **SoA is small.** A first-cut SoA might have 10–20 controls declared `in-scope`, a handful `deferred`, and a few `out-of-scope`. You are not annotating every possible control in the catalogue — only the ones your map touches.
- **Cross-reference to `mod-105` chapter `04` for 42005.** The impact-assessment card section is the *output* the 42005 method produces. Your `iso-extended-map.yaml`'s 42005 tags should point at whatever impact-assessment deliverable filename you named in exercise `01`.

## Acceptance criteria

You have succeeded if:

- `iso-extended-map.yaml` retains every row from exercise `02` unchanged in its anchor / NIST fields, with the new `sibling_iso_clauses`, `iso_soa_status`, `iso_method_pin`, and `iso_rationale` fields populated.
- Every row has at least one ISO/IEC 42001 clause tag. Rows that evaluate (Article 12 completeness, Article 14 usability, Article 15 accuracy / robustness / cybersecurity, Article 72 post-market review) all carry a clause 8 or 9 tag, not just 6.1 or 7.5.
- Every method-standard-relevant row (risk-management, impact-assessment, quality-attribute, robustness) tags the corresponding method standard and populates `iso_method_pin` with the programme's method reference.
- The map header pins all five ISO standards.
- `iso-cross-tag-rationales.md` covers every row with a one-line rationale — no row is unexplained.
- `statement-of-applicability.yaml` declares every Annex A control tagged on the map, with `in-scope | out-of-scope | deferred` status and substantive justification. No map row cross-tags an `out-of-scope` control (or, if it does, the reviewer sees the gap and the SoA has to be updated or the row's tag removed).
- `method-of-record.md` names the programme's specific method per method standard, cross-referenced to a deliverable filename.
- Every place you could not verify an exact clause identifier or Annex A ID is marked `<!-- needs-research: … -->` rather than guessed.
- A reviewer walking the map row-by-row can walk from any row into: the ISO/IEC 42001 clause number, the applicable Annex A control (with SoA status), the method-of-record standard (if applicable), and the deliverable filename — a complete audit trail from obligation to artefact.

## Stretch goals

- **Author the 42001 gap register.** Where the map has rows that do *not* cross-tag to any 42001 clause (they should be few — Article 49 registration is a candidate), record them in `42001-gap-register.md` with a note on why they sit outside the AIMS scope. This is what a 42001 certification prep exercise produces.
- **Draft the internal-audit programme.** In `internal-audit-programme.md`, sketch what a 42001 clause 9.2 internal audit would cover across your map: which rows, in what order, on what cadence, by whom. This is a genuine 9.2 deliverable a programme running toward certification needs.
- **Cross-reference ISO/IEC 27001 controls.** For Article 15 cybersecurity rows, add a `sibling_iso_27001` sub-field pointing at the 27001:2022 Annex A controls the row also touches. 42001 does not include a full cybersecurity control catalogue; 27001 is the reference for that layer.
- **Cross-reference the ISO/IEC 5259 data-quality series.** For Article 10 dataset-facing rows, add tags to 5259 clauses where they apply. Programmes with mature data-quality programmes have a distinct 5259 audit path.
- **Draft the management-review agenda (clause 9.3).** In `management-review-agenda.md`, produce the standing agenda for the 42001 clause 9.3 management review, cross-referenced to specific map rows and their status. This is what the annual management review consumes.
- **Cross-reference the 42006 accreditation angle.** In `certification-readiness-note.md`, note which of your SoA controls would be inspected by an ISO/IEC 42006-accredited certification body during a stage-1 vs. stage-2 audit, and what evidence they would expect to see. This anticipates the certification hand-off `mod-112` sets up.
