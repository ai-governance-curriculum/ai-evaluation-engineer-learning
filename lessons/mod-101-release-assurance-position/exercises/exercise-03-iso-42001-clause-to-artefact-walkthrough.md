# exercise-03: ISO/IEC 42001 Clause-to-Artefact Walkthrough

**Estimated effort:** 2 hours

## Objective

Walk a **single AI system's release** end-to-end across ISO/IEC 42001:2023 clauses 4–10 and, for each clause, name (a) the documented information the AIMS certification auditor would ask for and (b) the specific release-assurance artefact that discharges it. Then pick one Annex A control and trace it into the release-gate.

This exercise operationalises chapter `03` and prepares you for `mod-102`'s assurance-case work and `mod-106`'s crosswalk.

## Prerequisites

- Chapter `03-iso-iec-42001-clause-structure.md`.
- Chapter `02-nist-ai-rmf-and-playbook.md` (for the sibling-framework citations).
- Chapter `06-deferral-contract.md` (for the peer-owner column).
- Reference open in browser: ISO/IEC 42001:2023 clause list (via ISO catalogue), and ideally an internal or vendor summary of Annex A controls.

## Problem statement

Choose one AI system already deployed at (or realistically deployable at) an organisation you know — internal or public. It must:

- Be non-trivial (i.e. it has interested parties beyond the engineering team; someone outside the engineering team could be affected by its behaviour).
- Have at least one specific release event that has happened or is planned (not just "we run this all the time").
- Have documentation you can reason about (public model / system card, released blog post, or a similar record).

Sample choices, if none of the above is available: a hypothetical GenAI feature in an existing productivity SaaS, a hypothetical AI-assisted underwriting model at a mid-sized insurer, a hypothetical medical-imaging screening classifier at a hospital network. If you use a hypothetical, note it explicitly and flesh out the interested parties.

For the chosen system's release, produce the walkthrough described below.

## Requirements

Produce `iso-42001-walkthrough.md` containing:

1. **System and release header.** Two or three paragraphs — the system, the specific release, in-scope interested parties, in-scope jurisdictions.
2. **Clause-by-clause table** for clauses 4 through 10:

   | Clause | Sub-clauses touched | Documented information the auditor would ask for | Release-assurance artefact that discharges it | Peer role owing evidence | Sibling NIST AI RMF sub-category | Notes |
   | ------ | ------------------- | ----------------------------------------------- | --------------------------------------------- | ------------------------ | ------------------------------- | ----- |

   Each clause row must name at least one specific artefact. If a clause has no artefact yet, mark it as a **program gap** and note who owns closing the gap.
3. **Annex A trace.** Pick **one** Annex A control category (e.g. "assessing impacts of AI systems," "data for AI systems," "third-party and customer relationships"). For that category:
   - Summarise the control statements in your own words (2–3 sentences).
   - Cite the corresponding EU AI Act article(s) and NIST AI RMF sub-category(ies).
   - Name the release-gate evidence that discharges the control for your chosen system.
   - Name any adjacent ISO standard that supplies the method (e.g. ISO/IEC 23894 for risk method, ISO/IEC 42005 for impact assessment, ISO/IEC 24029-2 for robustness, ISO/IEC 5259 series or ISO/IEC 8183 for data).
4. **Certification-readiness call.** In one page, judge whether the release you chose would survive a Stage 2 AIMS certification audit today. Name three specific gaps that would come up in the certificate report and the corrective action for each.

## Starter guidance

- **Use ISO's own vocabulary** where possible: "documented information," "leadership commitment," "risk assessment," "risk treatment," "management review," "internal audit," "nonconformity," "corrective action."
- **Documented information means artefacts you can *point at*.** Not "we have a policy" but "*AI Policy v3.2, approved by top management on YYYY-MM-DD*." If you can't name the version, treat it as a gap.
- **Adjacent standards belong in the Notes column.** ISO/IEC 42001 is deliberately terse on method; the adjacent standards supply the method.
- **Do not skip clause 4 or clause 10.** Programs often over-invest in clause 8 (Operation) and under-invest in clause 4 (Context) and clause 10 (Improvement). Both are auditable.
- **The certification-readiness call should be brutally honest.** If the release you chose has no documented internal audit (clause 9.2) or no management review record (clause 9.3), that is Stage-2 failure material and the exercise expects you to flag it.

## Acceptance criteria

You have succeeded if:

- Every clause row (4 through 10) has at least one named artefact or an explicitly flagged program gap.
- Each artefact is cross-cited to the sibling NIST AI RMF sub-category.
- The Annex A trace cites the correct EU AI Act article(s) and lists the adjacent-standard method.
- The certification-readiness call is specific — no "we have work to do" language; instead, "clause 9.2 has no internal-audit programme; corrective action: schedule internal audit before next Stage-2 review, per ISO/IEC 42001 clause 9.2."
- The table would be usable inside a real audit-preparation pack.

## Stretch goals

- Extend the table to clauses 1–3 for completeness (scope, normative references, terms and definitions — these are not audited but shape the audit).
- Add a *risk-of-non-conformity* score (low / medium / high) to each clause row.
- Trace a *second* Annex A control category so the exercise touches two different concerns (e.g. data governance *and* third-party relationships).
- Draft the one-page management-review input (clause 9.3) the release-assurance program would produce for this system's release.
