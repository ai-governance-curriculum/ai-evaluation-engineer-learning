# Build vs Buy: Governance-Platform Fit-vs-Gap Analysis

## Motivation

The operating model (chapter `01`), the peer contracts (chapter `02`), and the upward interfaces (chapter `03`) all sit on top of a *tooling substrate*: the intake queue, the inventory, the risk register, the evidence store, the assurance-case authoring surface, the release-gate workflow, the dashboard, the post-market-monitoring runbook, the incident workflow, the third-party-audit envelope. The programme has to decide, per surface, whether to buy a commercial product, adopt an open-source project, or author internally.

Two failure modes motivate a deliberate fit-vs-gap analysis rather than an ad-hoc procurement.

The first is **buying the wrong shape**. A vendor's product looks like a governance platform in the demo but is optimised for a different operating model (institution-scope reporting rather than team-scope release-gate operation; policy-attestation workflow rather than assurance-case authoring; inventory-first rather than evidence-first). The programme buys it, moulds the operating model to fit the tool, and loses the altitude from chapter `01`.

The second is **building what is already commodity**. The programme authors a bespoke intake queue, a bespoke inventory, and a bespoke workflow tool when a competent commercial or open-source product already covers those surfaces cheaply. Capacity is burned on undifferentiated plumbing rather than the differentiated work (assurance-case reasoning, evidence-pipeline conventions, cross-jurisdiction reconciliation) the programme's altitude actually requires.

The rule this chapter draws: **intake and workflow are cheap to buy; the evidence pipeline and the assurance-case reasoning are worth authoring internally because they carry the organisation's specific evidence conventions.** The analysis below shows how to justify that rule against a live vendor landscape.

## The capability list

Before scoring any vendor, list the capabilities the operating model needs. Ten capabilities cover the surface:

1. **Intake queue** — structured submission of new systems, model versions, and material changes.
2. **Inventory** — the AI inventory the analyst maintains; the programme's read surface for scope assessment.
3. **Risk register** — the harm inventory and residual-risk log, versioned and tied to systems.
4. **Evidence store** — immutable, content-addressed, retention-classed storage for evaluation artefacts (`mod-104/01`).
5. **Assurance-case authoring** — GSN / CAE / SACM authoring surface with diff-and-review (`mod-102/04`).
6. **Release-gate workflow** — the walker, the decision record, the signing chain (`mod-103`).
7. **Dashboard** — the on-call board, plus the release-owner, programme-owner, and audit boards (`mod-103/06`).
8. **Post-market-monitoring and Article 72 runbook** — the ongoing-assurance surface (`mod-110`).
9. **Incident workflow** — Article 73 notification path, root-cause tracking, corrective-action closure.
10. **Third-party-audit envelope** — the packet the independent evaluator or notified body walks (`mod-109`, `mod-104/06`).

The intake, inventory, and risk-register capabilities (1–3) are the *shared substrate* — used by every downstream stage but not the load-bearing differentiator. The evidence store and assurance-case authoring (4–5) are the *differentiated core* — the shape of these determines the whole programme's altitude. The release-gate workflow, dashboard, post-market runbook, incident workflow, and audit envelope (6–10) are *composed* on top and can be either bought or authored depending on how deeply the vendor's model matches yours.

## The vendor landscape as of 2026-07

Seven vendors are worth reading against the capability list. Mark all specific feature claims with `<!-- needs-research: verify current feature set for vendor X in release Y -->` — vendor product surfaces change faster than curriculum text.

- **[Credo AI](https://www.credo.ai/)** — a governance platform positioning itself around policy attestation, use-case intake, and multi-framework crosswalking. <!-- needs-research: verify current Credo AI product surface as of 2026-07 -->
- **[Holistic AI](https://www.holisticai.com/)** — a governance platform with bias-and-explainability tooling, inventory, and audit-preparation features. <!-- needs-research: verify current Holistic AI product surface as of 2026-07 -->
- **[ModelOp Center](https://www.modelop.com/)** — a model-operations platform with governance overlays, positioned around model inventory, lifecycle workflow, and SR 11-7-shape model-risk management. <!-- needs-research: verify current ModelOp Center product surface as of 2026-07 -->
- **[ServiceNow AI Control Tower](https://www.servicenow.com/)** — a Now-Platform-native governance surface for AI inventory, risk assessment, and workflow, positioned around integration with existing IT-service-management and GRC. <!-- needs-research: verify current ServiceNow AI Control Tower feature set and its exact product name as of 2026-07 -->
- **[IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance)** — an IBM-stack governance product tied into watsonx for lifecycle governance, model-risk workflow, and factsheet generation. <!-- needs-research: verify current watsonx.governance product surface as of 2026-07 -->
- **[Fiddler AI](https://www.fiddler.ai/)** — an AI observability platform with governance-adjacent features around monitoring, explainability, and evaluation. <!-- needs-research: verify Fiddler AI's current positioning between observability and governance as of 2026-07 -->
- **[Monitaur Governance OS](https://www.monitaur.ai/)** — a governance product positioned around model-risk workflow and evidence capture. <!-- needs-research: verify Monitaur Governance OS product surface as of 2026-07 -->

The list is not exhaustive; other vendors (hyperscaler-native tools from AWS SageMaker / Azure ML / GCP Vertex, open-source products, boutique consultancies with tooling) are worth reading against the same matrix. What follows is a shape you can extend, not a finished procurement recommendation.

## The fit-vs-gap analysis shape

Score each vendor on each of the ten capabilities, on a three-band scale: **pass** (fits the operating model), **partial** (covers the capability but requires meaningful adaptation), **fail** (does not cover, or covers in a way that would force the operating model to distort).

The scoring is *against your operating model*, not against a general concept of governance. Two programmes with different operating models can score the same vendor differently and both be right.

**Shape.** A matrix of vendor × capability, cells carry pass / partial / fail plus a one-line rationale. The rationale is what a procurement decision defends against; the score without a rationale is decorative.

**Failure modes.** Scoring on brochure claims rather than a proof-of-concept (a partial passes as pass because the demo covers the happy path); scoring against an idealised operating model rather than the actual one; scoring based on the loudest voice in the procurement meeting rather than the release-gate on-call's experience.

**What good looks like.** Every cell's rationale points to a specific claim on the vendor's site or a specific finding from a hands-on trial; every partial names the adaptation required and the party responsible for authoring it; every fail names what the operating model would have to distort to accept it, and why that distortion is unacceptable.

A worked example matrix — for the six-person team from earlier chapters, with a bank-sector product line and one T3 system — might look like:

| Capability | Credo AI | Holistic AI | ModelOp Center | ServiceNow AI Control Tower | IBM watsonx.governance | Fiddler AI | Monitaur |
| ---------- | -------- | ----------- | -------------- | --------------------------- | ---------------------- | ---------- | -------- |
| Intake queue | pass | pass | pass | pass (native to Now) | pass | partial | pass |
| Inventory | pass | pass | pass | pass | pass | partial | pass |
| Risk register | pass | pass | partial | pass | pass | fail | pass |
| Evidence store | partial | partial | partial | partial | partial | partial | partial |
| Assurance-case authoring | fail | fail | fail | fail | fail | fail | partial |
| Release-gate workflow | partial | partial | partial | pass | partial | fail | partial |
| Dashboard | pass | pass | pass | pass | pass | pass | pass |
| Post-market-monitoring / Article 72 | partial | partial | partial | partial | partial | pass | partial |
| Incident workflow | partial | partial | pass | pass | partial | fail | pass |
| Third-party-audit envelope | partial | partial | partial | partial | partial | fail | partial |

The cell values above are illustrative — for a real procurement, run a hands-on trial and mark every cell against a rationale you can defend. <!-- needs-research: replace all cells with rationale-backed scoring after a hands-on trial -->

What the shape reveals across vendors: intake, inventory, and dashboard are near-universally passable (row 1, 2, 7). The evidence store and assurance-case authoring are near-universally partial or fail (rows 4, 5). Release-gate workflow, post-market runbook, incident workflow, and third-party-audit envelope split across the vendors depending on whose model the vendor originated from.

## The build-side decision

Given the matrix shape, the build-side decision falls out:

- **Intake, inventory, dashboard (rows 1, 2, 7).** Buy. These are cheap and undifferentiated. A commercial product carries them faster than internal engineering can, and the switching cost is low because the data models are simple.
- **Risk register, release-gate workflow, incident workflow (rows 3, 6, 9).** Buy at pass or partial; author internally at fail. Where a vendor covers the shape, integrate; where the vendor's model would force distortion, author.
- **Evidence store (row 4).** *Author internally.* The content-addressed store, the retention classes, the RO-Crate / BagIt / OCI serialisation choice, the Fulcio-plus-Rekor signing chain (`mod-104`) — these carry the organisation's specific evidence conventions. Every vendor's evidence store is *a store*; none is *your store*. Buying it means adopting the vendor's serialisation, the vendor's retention model, and the vendor's key-management story, which are near-impossible to unwind later.
- **Assurance-case authoring (row 5).** *Author internally.* SACM authoring, GSN / CAE representations, defeater and diversity-of-evidence audit (`mod-102`) are the differentiated core of the programme's methodology. A vendor's assurance-case authoring surface, where it exists at all, is typically a template-based factsheet — an artefact class, not an authoring surface for the reasoning. The reasoning is the programme's actual product.
- **Post-market-monitoring / Article 72 runbook (row 8).** *Author internally with vendor-supplied observability primitives.* The runbook shape (`mod-110`) is programme-specific; the underlying observability signals (drift detection, coverage measurement, incident detection) can come from a vendor.
- **Third-party-audit envelope (row 10).** *Author internally.* The bundle shape (`mod-104/06`), the signing story, the verification instructions, and the trust-root artefacts are programme-specific. Vendor-generated PDFs do not survive a mechanical verification walk.

The consolidated rule: **buy the plumbing; author the evidence conventions and the reasoning.** Vendor plumbing accelerates the operating model; vendor evidence conventions constrain it.

## Migration risk

The single most expensive migration hazard in this space is **vendor lock-in on the evidence schema**. If the assurance bundles, reproducibility bundles, and evidence-store artefacts are serialised in a vendor's proprietary schema, three exit conditions become expensive:

- **Switching vendors** requires reserialising every historical bundle; every bundle-id changes; the AIMS controlled-document register loses continuity.
- **Bringing the store in-house** requires re-signing every historical artefact under the internal key infrastructure; provenance chains break at the migration boundary.
- **Discharging Article 74 market-surveillance requests** in a form the authority can verify independently requires exporting to a standard format anyway — and if the vendor's schema is not exportable at high fidelity, the export loses evidence.

The mitigation is to *own the evidence schema* — CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore/Rekor, RO-Crate or BagIt at the bundle boundary — and to require every vendor product used in the pipeline to consume and emit these standard formats without re-serialisation. Vendors that will not commit to standard-format interoperability fail the fit-vs-gap analysis on that ground alone, regardless of the rest of their capability scoring.

## The trial-not-brochure discipline

Every score in the fit-vs-gap matrix must rest on a trial or a hands-on observation, not on a vendor demo or a marketing page. The trial does not have to be exhaustive; it has to be *targeted* — a small number of representative cases that stress the operating model where the programme actually spends time.

**Shape.** For each vendor in scope, run a two-week trial with one representative case per capability that matters for the decision. A representative case is one drawn from the current inventory (not a synthetic demo) and walked end-to-end with the vendor's product substituted for the current tool. Score each cell of the matrix against the trial's findings; write the rationale in one line.

**Failure modes.** The trial is executed by the vendor's implementation engineer rather than by the programme (findings are optimistic); the trial uses synthetic cases the vendor pre-loads (edge cases are hidden); the trial period is too short to reveal steady-state failures (the freshness enforcement, the audit-walk performance, the rebuild-on-schema-change behaviour); the trial is scored against a wish-list rather than against the operating model.

**What good looks like.** The trial is run by the on-call engineer who would use the tool; cases are drawn from the current queue; the trial period covers at least one full release-cycle for at least one system in the inventory; the scoring rationale is grounded in specific observations ("the walker output can be exported as DSSE-envelope-signed JSON per our schema"; "the assurance-case template cannot express the diversity-of-evidence pattern from `mod-102/05` without a workaround").

## Enterprise responsible-AI standards as reference-worked-examples

The internal standard the assurance programme authors and enforces is a reference-worked-example artefact. Three publicly available enterprise standards are worth reading as prior art:

- **[Microsoft Responsible AI Standard v2](https://www.microsoft.com/en-us/ai/principles-and-approach)** — the public documentation of Microsoft's internal responsible-AI standard, with impact-assessment templates, fit-for-purpose evaluation, and deployment-readiness checkpoints. <!-- needs-research: verify current Microsoft Responsible AI Standard version and canonical URL as of 2026-07 -->
- **[Google Responsible AI practices](https://ai.google/responsibility/)** — Google's public documentation of responsible-AI practices, including the model card and dataset card conventions, evaluation frameworks, and safety-review processes. <!-- needs-research: verify current Google responsible-AI documentation surface and canonical URL as of 2026-07 -->
- **[AWS Responsible AI overview](https://aws.amazon.com/ai/responsible-ai/)** — AWS's public documentation of responsible-AI practices, including the service-card convention and Bedrock-tied evaluation surfaces. <!-- needs-research: verify current AWS Responsible AI overview surface and canonical URL as of 2026-07 -->

Read them as *shape references* — the internal standard the programme authors will look nothing like these in specifics because your organisation is not Microsoft, Google, or AWS. It will look like them in shape: a principles statement, an operationalising standard, a set of templates, and a set of enforcement points across the release lifecycle.

## Worked example — the six-person team makes a build-vs-buy call

The six-person team's current stack (before this analysis) is: internal issue-tracker for intake, internal wiki for inventory, internal Git for the assurance case and criterion sets, an internal evidence store on top of an object-storage bucket with object-lock, custom scripts for the walker, and a home-built dashboard.

The team runs the fit-vs-gap analysis this quarter with two goals: unload the intake and dashboard (buy them; free 0.3 FTE); commit to authoring the evidence store and the assurance-case surface internally (invest 0.5 FTE for a full lifecycle release of both).

The team selects a vendor for intake and inventory after a hands-on trial (one of the seven above; the specific choice depends on the trial outcomes and the fit-vs-gap matrix). The team commits to a standards-based evidence schema (CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore/Rekor, RO-Crate bundle serialisation) and requires the vendor to import from and export to that schema at high fidelity as a purchase precondition.

The team defers the release-gate workflow, incident workflow, and post-market-monitoring runbook decisions to the next planning cycle; the current internal surfaces are working, and the fit-vs-gap analysis did not surface a vendor whose model matches the operating model closely enough to justify the migration.

The build-side authoring load is scoped to: (1) the assurance-case authoring surface (SACM plus GSN/CAE representation, defeater and diversity-of-evidence audit UI); (2) the evidence-store maintenance work (retention-class enforcement, canonicalisation, signing chain). The reasoning surface is the programme's differentiator; the storage plumbing is the substrate that supports it.

The decision is recorded in the operating-model documentation with a review trigger at the next planning cycle.

## Where this shows up in the rest of the track

- `mod-101/06` — the deferral contract is the programme's authoritative statement of what it owns; the build-vs-buy analysis follows the deferral contract's grain.
- `mod-104` — the evidence pipeline is the "author internally" side of the analysis; every chapter of `mod-104` is what would be lost if the evidence store were bought at low fidelity.
- `mod-105` — cards are card-shaped views over the evidence pipeline; vendor factsheet generators are lossy versions of what `mod-105` authors.
- `mod-107` — sector-regulated shape determines whether a vendor's sector-overlay coverage (SR 11-7 shape, FDA GMLP shape) is a real fit or a marketing claim; the sector overlay is part of the fit-vs-gap matrix.
- `mod-109` — third-party-audit envelope is one of the ten capabilities; vendor scoring on this row is directly tied to whether the vendor's export survives an auditor's mechanical walk.
- Chapter `01` — the operating model is the yardstick the analysis measures against.
- Chapter `05` — the incident-driven roadmap prioritisation is where the deferred surfaces (release-gate workflow, incident workflow, post-market runbook) get revisited when incident signal justifies the investment.

## Summary

- The programme's tooling substrate has ten capabilities: intake, inventory, risk register, evidence store, assurance-case authoring, release-gate workflow, dashboard, post-market-monitoring runbook, incident workflow, third-party-audit envelope.
- Vendors in scope (Credo AI, Holistic AI, ModelOp Center, ServiceNow AI Control Tower, IBM watsonx.governance, Fiddler AI, Monitaur) each cover a slice of the ten; score each cell pass / partial / fail against your operating model with a written rationale.
- The consolidated rule: buy intake, inventory, and dashboard (undifferentiated plumbing); author the evidence store and assurance-case authoring internally (the differentiated core); buy or author the middle rows depending on whether the vendor's shape matches.
- Vendor lock-in on the evidence schema is the most expensive migration hazard; own the schema (CycloneDX ML-BOM, SPDX-AI, SLSA, DSSE, Sigstore/Rekor, RO-Crate / BagIt) and require standards-based interoperability from every vendor.
- Read Microsoft's Responsible AI Standard v2, Google's Responsible AI practices, and AWS's Responsible AI overview as shape references for the internal standard the programme authors and enforces; the shape transfers, the specifics do not.
- Mark every uncertain vendor-feature claim with `needs-research`; run a hands-on trial before scoring.
- Exercise-04 asks you to draft the fit-vs-gap matrix for your organisation's real vendor landscape and defend the build / buy split against a procurement counterparty.
