# exercise-04: Build-vs-Buy Governance Platform Fit-vs-Gap Analysis

**Estimated effort:** 3 hours

## Objective

Author the **build-vs-buy fit-vs-gap analysis** for the assurance programme's tooling substrate, against the vendor landscape and against the operating model pinned in exercises `01`–`03`. Produce a scored capability × vendor matrix with per-cell rationales; write the build-side decision (what the programme authors internally versus what it buys); own the evidence-schema story to avoid the single most expensive migration hazard in this space (vendor lock-in on the assurance-bundle serialisation); and defend the choice against a plausible procurement counterparty.

This exercise is design and authoring, not solving. `<!-- needs-research: … -->` markers are legitimate answers where a vendor's current product surface would need verification against the vendor's own site or a hands-on trial, or where a standards-body publication would need verification against the current release.

## Prerequisites

- Chapter [`04-build-vs-buy-governance-platform-fit-vs-gap.md`](../04-build-vs-buy-governance-platform-fit-vs-gap.md) — the ten capabilities of the tooling substrate; the seven vendors in scope; the pass / partial / fail scoring shape; the trial-not-brochure discipline; the evidence-schema-ownership rule; the three enterprise-responsible-AI standards as shape references.
- Exercise [`exercise-01`](exercise-01-operating-model-and-effective-challenge-convention.md) — the operating model the fit-vs-gap analysis is scored against. Score against your operating model, not against a generic concept of governance.
- Exercise [`exercise-02`](exercise-02-peer-track-contract-matrix.md) — the peer-contract matrix implies which vendor surfaces the programme integrates with which peer teams (some vendors bring their own peer-integration story; some do not).
- Familiarity with [`mod-104-evaluation-evidence-pipeline`](../../mod-104-evaluation-evidence-pipeline/) chapters `01` (the content-addressed store), `03` (the reproducibility bundle), `04` (supply-chain provenance — CycloneDX, SPDX, SLSA, Sigstore), `05` (eval-set security), `06` (the signed assurance bundle).
- Skim access to each vendor's public product surface:
  - [Credo AI](https://www.credo.ai/)
  - [Holistic AI](https://www.holisticai.com/)
  - [ModelOp Center](https://www.modelop.com/)
  - [ServiceNow AI Control Tower](https://www.servicenow.com/) (verify current product name against the current site — `<!-- needs-research: verify product name -->`)
  - [IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance)
  - [Fiddler AI](https://www.fiddler.ai/)
  - [Monitaur](https://www.monitaur.ai/)
- Skim access to the three enterprise responsible-AI reference standards:
  - [Microsoft Responsible AI Standard](https://www.microsoft.com/en-us/ai/principles-and-approach) (verify the current version — `<!-- needs-research: verify current version and canonical URL -->`).
  - [Google Responsible AI practices](https://ai.google/responsibility/) (verify the current documentation surface).
  - [AWS Responsible AI overview](https://aws.amazon.com/ai/responsible-ai/) (verify the current overview surface and the AWS AI Service Cards convention).

## Problem statement

Carry the pinned organisation from exercises `01`–`03`. The fit-vs-gap analysis must score vendors against *your* operating model — the six-stage cycle, the three registers, the effective-challenge convention, the peer-contract matrix, the reporting-line contract, the external-supervisor interfaces. Two programmes with different operating models can score the same vendor differently and both be right; the analysis is a *defence* of your operating model's needs, not a rating of vendors in the abstract.

Three complications when drafting:

- **The evidence-schema-ownership rule is non-negotiable.** Every vendor row must state whether the vendor commits to importing from and exporting to standard formats (CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore / Rekor, RO-Crate or BagIt at the bundle boundary) at high fidelity. Vendors that will not commit fail the analysis on that ground alone, regardless of the rest of their capability scoring. State the rule and its consequences in the analysis explicitly.
- **The trial-not-brochure discipline is a hard constraint.** Every cell in the matrix must rest on a hands-on trial observation, or be marked `<!-- needs-research: score against a hands-on trial -->` where a trial has not been run. Cells scored on marketing pages are not defensible against procurement; the exercise treats brochure-scored cells as an unfilled cell.
- **The build-side authoring load has to be small enough to actually deliver.** The exercise asks for a *committable* build-side plan — one the pinned organisation's programme-team size can complete in a bounded number of FTE-weeks. Ambitious build-sides that require more capacity than the team has are not defensible.

## Requirements

Produce five artefacts in a single `build-vs-buy/` directory.

### 1. `build-vs-buy/capability-list.md`

The ten capability rows the operating model needs, per chapter `04`. For each capability, state:

- **What the capability is,** in one sentence, against the pinned operating model.
- **The load-bearing operating-model stage it serves** (intake, scope assessment, evidence provisioning, assurance-case draft, release-gate review, decision + post-market; see exercise `01` for the six stages).
- **The differentiation class:** *shared substrate* (rows 1–3: intake, inventory, risk register), *differentiated core* (rows 4–5: evidence store, assurance-case authoring), or *composed on top* (rows 6–10: release-gate workflow, dashboard, post-market runbook, incident workflow, third-party-audit envelope).
- **The freshness / latency / integrity requirement** the capability must meet at the pinned organisation's scale.
- **The interoperability boundary** — the standard format the capability must import from and export to. Rows 4 (evidence store) and 10 (third-party-audit envelope) carry the strictest requirements (CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore, RO-Crate / BagIt).

### 2. `build-vs-buy/fit-vs-gap-matrix.md`

The scored matrix, capability rows × vendor columns, with a one-line rationale per cell.

- **Columns.** The seven vendors from chapter `04` (Credo AI, Holistic AI, ModelOp Center, ServiceNow AI Control Tower, IBM watsonx.governance, Fiddler AI, Monitaur), plus an optional eighth *internal / open-source* column for the current state of the programme's own tooling and any open-source products the analysis considered.
- **Cells.** *Pass* (fits the operating model), *partial* (covers the capability but requires meaningful adaptation, name the adaptation), *fail* (does not cover, or covers in a way that would force the operating model to distort, name the distortion). Every cell has a one-line rationale grounded in a specific claim on the vendor's site or a specific finding from a hands-on trial. Where a hands-on trial was not run, mark the cell `<!-- needs-research: score against a hands-on trial -->` explicitly.
- **The evidence-schema-ownership row.** Add an eleventh row (below the ten capabilities) for *standards-based schema interoperability*. Cells: *committed* (the vendor commits to importing and exporting the standard formats at high fidelity), *partial* (the vendor supports the standards but with known lossy conversions or unpublished serialisation extensions), *no-commit* (the vendor does not commit; the vendor's evidence store is a lock-in hazard). This row is a *hard gate*: a *no-commit* cell disqualifies the vendor for the evidence-store row (row 4) and the third-party-audit-envelope row (row 10) regardless of the rest of the scoring.
- **A summary block below the matrix.** Which vendors covered which contiguous slices of the operating model well; which vendors were disqualified on the schema-interoperability row; which vendors would require the operating model to distort in order to be adopted (name the distortion).

### 3. `build-vs-buy/build-side-decision.md`

The committable plan for what the programme authors internally.

- **Buy-side rows.** For each capability the analysis buys, name the vendor selected (or, if the analysis is inconclusive without a trial, mark `<!-- needs-research: trial to select between vendor X and vendor Y for capability Z -->` and name the trial's success criteria). State the integration boundary — what data flows in, what data flows out, what standard format the boundary crosses.
- **Author-side rows.** For each capability the analysis authors internally, state the *scope* (the operating-model surface that lives in the internal tool), the *FTE-week estimate*, the *ship-by date*, and the *maintenance owner role*. Explicitly commit to the evidence store (row 4) and the assurance-case authoring surface (row 5) as author-side rows — these are the differentiated core per chapter `04`.
- **Hybrid rows.** For each capability where the analysis buys the observability primitives and authors the operating-model glue (row 8 — post-market monitoring — is the canonical case), state the split: which vendor primitives are consumed, which internal glue is authored.
- **Standards-interoperability commitment.** Restate the interoperability boundary the analysis enforces — CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore / Rekor, RO-Crate or BagIt. State that this is a *purchase precondition* for every buy-side vendor, and that a vendor that refuses to commit is dropped from the analysis regardless of feature richness.
- **Total effort budget.** Sum the FTE-week estimates for the author-side rows. State whether the total fits the pinned organisation's programme-team capacity (from exercise `01`) and, if not, which author-side rows defer to the next planning cycle.

### 4. `build-vs-buy/reference-standard-read.md`

The reference read of the three enterprise responsible-AI standards, as shape prior art for the internal standard the assurance programme authors and enforces. For each standard:

- **Bibliographic reference.** Standard name, publisher, current version (mark `<!-- needs-research: verify current version -->` where the version is not stable), canonical URL, publication date, licence.
- **Shape summary.** What the standard covers, at the top level — principles statement, operationalising standard, templates, enforcement points. Not the specifics; the *shape*.
- **What shape transfers to your internal standard.** For each of the top-level sections of the standard, state whether the shape transfers to the pinned organisation's internal standard (the operating-model handbook plus the assurance-case authoring surface plus the effective-challenge convention plus the peer contracts) — *transfers directly*, *transfers with adaptation*, or *does not transfer* (with a one-line reason).
- **What specifics do NOT transfer.** State explicitly that the internal standard the pinned organisation authors will look nothing like the reference standards in specifics — because your organisation is not Microsoft, Google, or AWS. This is a warning against the failure mode of copying specifics as if they were transferable.
- **Adjacent references.** Where the reference standard has a live adjacent artefact the pinned organisation could consume directly (a template, a checklist, a public tool), name it as an adjacent reference rather than as prior art.

### 5. `build-vs-buy/procurement-defence.md`

The one-pager the programme lead uses to defend the build-side decision against a procurement counterparty (a chief procurement officer, a finance-partner reviewing the annual planning cycle, a CIO / CTO evaluating the total-cost-of-ownership).

- **The question the counterparty will ask.** *Why are we not just buying a full-stack governance platform and getting on with it?*
- **The answer, in one paragraph.** The consolidated rule from chapter `04`: buy the plumbing; author the evidence conventions and the reasoning. Vendor plumbing accelerates the operating model; vendor evidence conventions constrain it. The rule is defensible because the evidence store and the assurance-case authoring surface carry the organisation's specific evidence conventions and reasoning, which cannot be off-the-shelf without also off-the-shelving the audit-defensibility.
- **The migration-risk paragraph.** Vendor lock-in on the evidence schema is the single most expensive migration hazard. Enumerate the three exit conditions from chapter `04` (switching vendors, bringing the store in-house, discharging Article 74 requests in a form the authority can verify independently) and state the mitigation (own the schema; require standards-based interoperability from every vendor).
- **The trial-not-brochure discipline.** State the analysis was scored on hands-on trials for cells where the score was decision-relevant, and marked `needs-research` for cells where the trial was not yet run. Explain why the trial discipline is a hard constraint.
- **The total-cost-of-ownership table.** A compact table with columns *capability*, *buy cost* (annual subscription plus integration FTE), *build cost* (initial FTE-weeks plus per-year maintenance FTE), *migration cost* (if switching vendors becomes necessary in year N — the schema-lock-in premium). The table's job is not to be arithmetically precise (it usually cannot be at this stage) but to make the TCO shape visible.
- **The reversibility argument.** State which decisions are reversible cheaply (a vendor for intake / dashboard is easy to swap out) and which are expensive (a proprietary evidence-schema commitment is a decade-long liability). The build-side decision follows the reversibility gradient.

## Starter guidance

- **Score against your operating model, not against a general concept of governance.** A vendor whose model matches a policy-attestation shape and whose intake queue is *pass* against an inventory-first programme may be *fail* against your evidence-first programme, and vice versa.
- **The differentiated core is short.** Only two rows (evidence store, assurance-case authoring) are the differentiated core; the other eight rows are cheaper to buy at a reasonable price. Do not talk yourself into authoring the intake queue when the current internal ticket system is doing the job well enough.
- **Brochures over-promise, uniformly.** Assume every vendor's marketing surface over-promises on the differentiated core (evidence store, assurance-case authoring) and under-promises on the composed layer (dashboards, workflows). Trials realign both.
- **The trial does not have to be exhaustive.** A two-week trial with one representative case per capability that matters for the decision is enough. The point is to score against observation, not against a demo. Representative cases are drawn from the current inventory, not from synthetic vendor pre-loads.
- **The build-side load has to be small enough to actually ship.** If the plan requires four FTE-quarters of build-side authoring and the team has two FTE-quarters of capacity, the plan is a fantasy. Cut the author-side rows to fit — or reallocate capacity, but state the reallocation explicitly.
- **The evidence-schema-ownership rule is non-negotiable.** A vendor that refuses to commit to CycloneDX / SPDX / SLSA / DSSE / Sigstore / RO-Crate interoperability is off the shortlist. This is not a preference; it is a fit-vs-gap failure on the migration-risk axis.
- **The reference standards read is *shape*, not *specifics*.** Microsoft's, Google's, and AWS's public responsible-AI standards are read to see how a large organisation structures a principles-plus-standard-plus-templates-plus-enforcement stack — not to be copied. The internal standard your pinned organisation authors will look nothing like theirs in specifics.
- **`<!-- needs-research: … -->` is a legitimate answer** for every vendor feature claim (verify against a hands-on trial), every standards clause number, every URL that has moved, and every date that has drifted.

## Acceptance criteria

You have succeeded if:

- `build-vs-buy/capability-list.md` covers the ten capability rows from chapter `04`, each with what-it-is, load-bearing operating-model stage, differentiation class, freshness / latency / integrity requirement, and interoperability boundary.
- `build-vs-buy/fit-vs-gap-matrix.md` scores the seven vendors from chapter `04` (plus an optional internal / open-source column) against the ten capability rows plus the eleventh standards-based-schema-interoperability row. Every cell has a one-line rationale grounded in a hands-on-trial observation, a specific claim on the vendor's site, or an explicit `needs-research` marker. The summary block names which vendors covered which slices well, which were disqualified on the schema row, and which would force distortion.
- `build-vs-buy/build-side-decision.md` names the buy-side vendors per capability (or the trial to select between candidates), the author-side capabilities with scope, FTE-week estimate, ship-by date, and maintenance owner. The evidence store (row 4) and the assurance-case authoring (row 5) are author-side rows. The standards-interoperability commitment is stated as a purchase precondition. The total FTE-week budget fits the pinned organisation's programme-team capacity.
- `build-vs-buy/reference-standard-read.md` reads Microsoft's, Google's, and AWS's public responsible-AI standards with bibliographic reference, shape summary, transfers / does-not-transfer analysis, an explicit warning against copying specifics, and any adjacent references worth consuming directly.
- `build-vs-buy/procurement-defence.md` states the question, the one-paragraph answer, the migration-risk paragraph (with the three exit conditions and the mitigation), the trial-not-brochure discipline, a compact TCO table, and the reversibility argument.
- Every vendor row in the matrix carries an evidence-schema-ownership cell (committed / partial / no-commit). No-commit disqualifies the vendor for rows 4 and 10.
- Every author-side row has a named maintenance owner role (not a person's name) and a ship-by date that fits the pinned organisation's planning cycle.
- Every URL, version, and article number is either verified against the current source or marked `<!-- needs-research: … -->`.

## Stretch goals

- **Run one trial and report against it.** In `trial-report-<vendor-slug>.md`, execute a two-week hands-on trial with one representative case per capability that matters for the decision, and produce the report — cases run, findings per cell, matrix cells this trial resolved, matrix cells still `needs-research`. This turns the exercise's `needs-research` markers into resolved cells for one vendor.
- **Draft the vendor-questionnaire template.** In `vendor-questionnaire.md`, produce the questionnaire the procurement function sends to shortlisted vendors covering the ten capability rows, the schema-interoperability commitment (including the specific formats — CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore / Rekor, RO-Crate / BagIt), the peer-integration story, and the migration-cost commitment.
- **Author the total-cost-of-ownership model.** In `tco-model.md`, extend the TCO table from artefact 5 into a full model — per-year subscription plus integration FTE for the buy-side, initial-plus-maintenance FTE for the author-side, migration-cost premium for the schema-lock-in scenario, over a five-year horizon.
- **Draft the internal responsible-AI standard's outline.** In `internal-standard-outline.md`, produce the outline the pinned organisation's internal standard would take — principles statement, operationalising standard, templates, enforcement points — using the three reference standards as shape prior art but populated with the pinned organisation's specifics.
- **Draft the vendor-decision-record.** In `decision-record.md`, formalise the architectural-decision-record (ADR) template the programme uses to record every build-vs-buy decision — the decision, the alternatives considered, the rationale, the reversal-cost estimate, the review trigger.
