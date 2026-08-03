# exercise-01: Article 55 and GPAI Code of Practice Obligation Map

**Estimated effort:** 3 hours

## Objective

Author the **EU AI Act Article 55 obligation map** for one worked GPAI-systemic-risk release, obligation by obligation, discharged via signatory adherence to the [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice). The map is the artefact a reviewer at the European AI Office reads first when they attach to the assurance bundle for a systemic-risk GPAI. It resolves — in one hop per row — from statute (an Article 55 sub-obligation and the Code commitment operationalising it), through the enterprise's discharge instrument (a frontier framework, an evaluation report, an incident procedure, a cybersecurity attestation), to a specific evidence artefact in the store (`mod-104` chapter `02`).

The exercise is design and authoring, not solving. Placeholder evidence pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the current EUR-Lex text, the current published version of the Code of Practice, the enterprise's own frontier framework, or a specific benchmark version.

## Prerequisites

- Chapter [`01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md`](../01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md) — Article 3(65) / 51 / 52 classification path; Article 55's four sub-obligations; the Code of Practice's three chapters and the presumption of conformity for signatories.
- Skim access to Regulation (EU) 2024/1689 Articles 3(65), 51, 52, 53, 55, and 56, plus Annex XIII, in the consolidated text at [eur-lex.europa.eu/eli/reg/2024/1689/oj](https://eur-lex.europa.eu/eli/reg/2024/1689/oj).
- Skim access to the current [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the safety-and-security, transparency, and copyright chapters.
- Familiarity with `mod-102` (the assurance case's claim structure — the Article 55 obligations become top-level claims), `mod-104` chapter `06` (the signed assurance bundle the map cites into), and `mod-105` (the Model Documentation Form the transparency chapter operationalises).
- Foreshadow of chapters `02` (frontier-framework citation), `03` (AI 600-1 crosswalk and TEVV envelope), `04` (safety-benchmark citation pack), and `05` (C2PA / NTIA overlay) — this exercise's rows point *forward* to the artefacts subsequent exercises construct.

## Problem statement

Pin one worked GPAI-systemic-risk release. The release must:

- **Be classifiable as a GPAI with systemic risk** under Article 3(65). Either the training-compute presumption of Article 51(2) applies (cumulative training compute crosses the 10^25-FLOP presumption threshold — `<!-- needs-research: reconfirm 10^25 in the current consolidated text and any delegated-act updates -->`), or the Annex XIII equivalent-capability path applies. State which and why.
- **Be placed on the market inside the Union** (or intended to be). Article 55 applies to providers placing GPAI-systemic-risk models on the Union market; a release with no Union exposure has a different discharge path.
- **Have a named modality set** — text-only LLM, multimodal (text + image), text + image + audio, text-to-video, and so on. The modality set affects Article 50(2) machine-readable-marking obligations and the safety-benchmark citation pack later in the module.
- **Have a named openness position** — closed-weight via API, gated-open with structured access, or open-weight. The openness position shapes the mitigation set available at Article 55(1)(b) discharge (chapter `05`).

Common shapes worth considering (pick one, or invent your own):

- **Closed-weight frontier LLM** — a text-only or multimodal LLM at or above the training-compute presumption, deployed via API only, with a signatory position on the Code of Practice. Discharge relies on the signatory's own published frontier framework (chapter `02`).
- **Multimodal reasoning model with tool use** — a text + image model that natively invokes tools inside an agent scaffold. Discharge extends the safety-benchmark citation pack (chapter `04`) with agentic-safety evidence from `agentic-safety-engineer`.
- **Open-weight foundation model above the presumption** — weights published under an open licence with the training compute crossing the presumption threshold. Discharge extends chapter `05`'s NTIA-framing citation and the Article 55(1)(b) Union-level mitigation set.
- **Fine-tuned derivative of a base GPAI-systemic-risk model** — the derivative may or may not itself cross the presumption; the discharge either passes through the upstream provider's Article 55 artefacts or independently discharges (with the delta explicitly named).

Pin the release, its Article 51 classification path, the modality set, and the openness position before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `release-classification-brief.md`

A one-to-two-page brief that pins the classification and the scope the map covers:

- **Provider identity.** The provider organisation (single legal entity), authorised-representative reference under Article 22 if the provider is established outside the Union (with placeholder `<!-- needs-research: … -->` where applicable), and the intended interface with the European AI Office (chapter `01`).
- **Model identity.** The model name, version, and content-addressed digest the release resolves to; the training-run identifier; and the artefact-set the assurance bundle wraps around (foreshadow `mod-104` chapter `06`).
- **Article 3(65) definition path.** The specific classification path — Article 51(2) FLOP presumption crossing, or Annex XIII equivalent-capability designation. State the training-compute estimate (with basis for the estimate — training FLOPS aggregated from the training log, or a placeholder with `<!-- needs-research: … -->`), the parameter count, the training-dataset size, the input / output modalities, and the reach / registered-end-users the model is expected to have. These are the classification-relevant facts.
- **Article 52 notification reference.** The notification the provider filed (or plans to file) — date, template used, and the AI Office's classification decision (or a placeholder). If the provider is presenting a rebuttal under Article 52, cite the rebuttal reference and its rationale.
- **Openness position.** Closed-weight / gated-open / open-weight, with a one-sentence justification.
- **Code of Practice position.** Signatory (with the signing date and the Code version signed), non-signatory with an alternative discharge path (with a one-paragraph justification of the alternative), or pending. Where the Code of Practice's current version is unclear as of the drafting date, mark `<!-- needs-research: verify current Code of Practice version at the drafting date -->`.
- **Counterparty set.** Which external bodies the assurance bundle is written for — European AI Office (mandatory for Article 55), UK AISI, US AISI, other notified bodies, sector-specific supervisors where applicable. Cross-reference `mod-109`.

The brief is the *setup*. Reviewers of the obligation map read this first.

### 2. `article-55-obligation-map.md`

The Article 55 obligation map itself. Structured as a table with the following columns.

| Column | Content |
| --- | --- |
| Article 55 sub-obligation | The specific Article 55(1)(a) / (b) / (c) / (d) obligation, with the relevant sub-paragraph text paraphrased. |
| Code of Practice commitment | The specific safety-and-security-chapter commitment that operationalises the sub-obligation for signatories (mark `<!-- needs-research: verify current numbering / naming of the commitment in the current Code version -->` where necessary). |
| Discharge instrument | The internal artefact that discharges the commitment — the enterprise's frontier framework (foreshadow chapter `02`), the evaluation report set (foreshadow chapters `03` and `04`), the incident procedure, the cybersecurity attestation. |
| Evidence artefact class | The specific evidence-artefact class in the store (`mod-104` chapter `02`) — reproducibility bundles for benchmark runs, red-team reports, guardrail-evaluation reports, signed attestations. |
| Peer-role owner | Which peer track produces the underlying methodology / evidence — `model-evaluation-engineer`, `ai-risk-engineer`, `agentic-safety-engineer` (level 40) for agentic capabilities, `ai-infra-security` for the cybersecurity attestation. |
| Store landing | The content-addressed store artefact-class name and the tags (`obligation:eu-ai-act-art-55-1-a`, `regulatory_scope:eu`, `code_of_practice:v1.x`) it carries. |
| Assurance-case anchor | The claim node in the assurance case (`mod-102`) the row's evidence discharges. |

At minimum, the map covers:

- **Article 55(1)(a)** — state-of-the-art model evaluation, including adversarial testing. Cross-reference the state-of-the-art justification (chapter `01`) that names the benchmarks and red-team methodology cited as state-of-the-art at release date. Foreshadow the specific safety-benchmark citation pack in chapter `04`.
- **Article 55(1)(b)** — assessment and mitigation of possible systemic risks at Union level. Note that the Union-level assessment is a distinct artefact from the product-level risk register carried in `mod-102`. Cross-reference the NTIA-framing citation for the openness-position reasoning (chapter `05`) and the AI 600-1 risk categories the assessment is structured against (chapter `03`).
- **Article 55(1)(c)** — serious-incident tracking and reporting to the AI Office. Cross-reference `mod-110`'s Article 73 workflow, with the AI Office as an additional counterparty for GPAI-systemic-risk providers.
- **Article 55(1)(d)** — adequate cybersecurity of the model and infrastructure. Cross-reference `mod-104` chapter `04` (supply-chain provenance), chapter `05` (eval-set-security), and the peer `ai-infra-security` role. The threat model at Article 55(1)(d) explicitly includes state-level model-exfiltration actors.

Include, alongside the four Article 55 sub-obligations, at least the following *baseline* Article 53 rows the systemic-risk provider still owes:

- **Article 53(1)(a) — technical documentation for the model itself.** Discharged via the Code of Practice's Model Documentation Form (chapter `01`, transparency chapter). Cross-reference `mod-105`.
- **Article 53(1)(b) — information for downstream providers.** Discharged via the same Model Documentation Form, subset appropriate to downstream integration.
- **Article 53(1)(c) — copyright policy.** Discharged via the Code's copyright chapter and the internal copyright-compliance procedure.
- **Article 53(1)(d) — training-content summary.** Discharged via the Code's training-content-summary template.

Every row states its counterparty (the AI Office is the primary counterparty for Article 55; other counterparties per the map from artefact 1).

### 3. `code-of-practice-signatory-position.md`

A brief that fixes the enterprise's position on the Code of Practice and captures the discharge choice as an assurance-case-visible decision:

- **Signatory / non-signatory / pending.** State the position with the signing date and the Code version signed (with placeholder if not signed).
- **Chapter-by-chapter discharge shape.** For each of the safety-and-security, transparency, and copyright chapters, state at *chapter* level whether discharge is via Code adherence (presumption of conformity) or via alternative means. Where via alternative means, cite the alternative and its justification.
- **Frontier-framework citation stub.** A placeholder pointer to the frontier framework the enterprise carries (chapter `02` / exercise `02`) — the specific version, the tier the release sits at, and the pre-commitments the framework carries at that tier.
- **Code revision procedure.** How the enterprise tracks Code revisions after signing — the review cadence, the responsible role, and the process for re-signing on a Code version change without invalidating prior discharge.
- **Non-signatory equivalence argument (only if applicable).** If the enterprise is not a signatory, the paragraph-length argument that the alternative discharge equals or exceeds the Code's shape, with citations to the alternative artefacts and to any independent audit or third-party evaluation that supports the claim.
- **Third-country provider considerations.** If the provider is established outside the Union, name the authorised representative under Article 22, the Article 22 mandate reference, and the communication path with the AI Office. Third-country signatories on the Code face additional coordination — mark `<!-- needs-research: verify the Article 22 mandate template and any specific coordination guidance the AI Office has issued -->` where the current guidance is not stable.

### 4. `article-52-classification-workflow.md`

The workflow for the Article 52 notification and, if applicable, the Article 52(2) rebuttal. This is a *release-gate-adjacent* obligation — the release-assurance programme cannot ship a candidate that crosses the presumption threshold without confirming the notification is filed (or the rebuttal is submitted), so the workflow attaches to the intake gate (`mod-102`).

- **Threshold monitoring.** How the enterprise tracks its cumulative training compute against the Article 51(2) threshold, and who is accountable for notifying at the two-week window. Include the internal data source (training-cluster telemetry, aggregated FLOPS meter, or similar) and the notification-owner role.
- **Notification content.** The information the notification carries (as specified in Article 52 and any Commission template — mark `<!-- needs-research: verify current notification template on the AI Office site -->` where the template is not stable). Include cross-references to the release-classification brief (artefact 1) for the classification-relevant facts.
- **Notification wall-clock.** The two-week window (state the wall-clock start — meeting the requirement, or becoming known — and the internal notification sign-off route).
- **Rebuttal path (if applicable).** The path under Article 52(2)–(3) for presenting arguments that the model does not present systemic risks despite meeting the threshold. Include the evidence set the rebuttal cites (typically capability-evaluation results that fall well below the frontier framework's tier-elevation triggers), the counterfactual argument, and the person accountable for signing.
- **AI Office response handling.** How the enterprise handles the AI Office's classification decision — acceptance, rejection of a rebuttal, ex-officio designation of a below-threshold model on Annex XIII grounds. Include the escalation path where the decision changes the release plan.
- **Assurance-bundle integration.** The Article 52 notification reference (and the AI Office decision, once received) lands as a discrete evidence node in the assurance bundle (`mod-104` chapter `06`), cited from the assurance case as a discharged intake obligation before any Article 55 evidence is even collected.

### 5. `discharge-verification-walkthrough.md`

A one-page walkthrough of what a reviewer at the European AI Office would walk when they attach to the obligation map. Structured as a numbered sequence:

1. Reviewer receives the assurance bundle handle and reads `release-classification-brief.md` to fix the classification path and the release scope.
2. Reviewer opens `code-of-practice-signatory-position.md` to fix the discharge shape (signatory presumption or alternative-means argument).
3. Reviewer opens `article-52-classification-workflow.md` to confirm the notification is filed and the AI Office decision is on record.
4. Reviewer opens `article-55-obligation-map.md` and, per row, walks the discharge chain — Article 55 sub-obligation → Code commitment → discharge instrument → evidence-artefact class → store landing → assurance-case anchor.
5. Reviewer resolves any one row end-to-end, from the map row to the specific evidence artefact in the store, verifying digest and signature (per `mod-104` chapter `06`).

For each step, name the artefact and any specific field or section the reviewer would look at. This walkthrough is the *acceptance test* for the map: if a reviewer cannot walk it in this order, the map is not doing its job.

## Starter guidance

- **The classification path is a live obligation, not a formality.** Article 52's two-week notification window makes the classification the *first* release-gate check on a candidate that plausibly crosses the presumption. If the training-compute number is uncertain, the intake gate (`mod-102`) does not clear until the notification-decision path is known.
- **Sign the Code or defend the alternative — do not straddle.** The map's rows must state, per row, whether discharge is via the Code's presumption of conformity or via an alternative-means argument. Rows that gesture at "consistent with the Code" without either signing or defending an alternative are not walkable by an AI Office reviewer.
- **The Union-level assessment is not the product-level risk register.** Chapter `01` names this explicitly. If the map's Article 55(1)(b) row cites the same risk register carried in `mod-102`, the row is under-serving the obligation. A distinct Union-level assessment is required — with cross-border cascade reasoning, information-integrity effects on Union-wide discourse, and cross-sector uplift reasoning.
- **The safety-benchmark citation pack is not this exercise's job.** Exercise `04` builds the citation pack in detail. This exercise's Article 55(1)(a) row cites the pack's artefact class and its store landing without enumerating specific benchmarks.
- **The frontier-framework citation is not this exercise's job either.** Exercise `02` builds the comparative-read table. This exercise's rows cite the framework's artefact and version without re-executing the comparative read.
- **The AI 600-1 crosswalk and the TEVV envelope are not this exercise's job.** Exercise `03` builds them. This exercise's rows cite the crosswalk artefact and the evaluator envelope as references without duplicating the content.
- **`<!-- needs-research: … -->` is a legitimate answer.** The Code of Practice's version, the exact Article 51(2) threshold under any delegated act, the Model Documentation Form's current template, the AI Office's current notification form — all of these should be marked rather than guessed if the drafting date is not clean against the current text.
- **The AI Office is the primary counterparty.** Every row's counterparty column states this explicitly, plus any additional counterparty (UK AISI, US AISI, notified body, sector supervisor) that also consumes the row's evidence.
- **The map is a controlled document.** It is versioned, signed, and superseded (not edited in place) alongside the assurance bundle it accompanies. Foreshadow — the map's version is pinned into the manifest field of the assurance bundle (`mod-104` chapter `06`), with the release candidate's identifier.

## Acceptance criteria

You have succeeded if:

- `release-classification-brief.md` fixes provider identity, model identity, the Article 3(65) definition path with the classification-relevant facts (compute, parameters, dataset size, modalities, reach), the Article 52 notification reference, the openness position, the Code-of-Practice position, and the counterparty set. A reviewer can decide from the brief alone which release is in scope and which classification path applies.
- `article-55-obligation-map.md` has one row per sub-obligation of Article 55(1)(a), (b), (c), (d), plus at least the four baseline Article 53(1)(a)–(d) rows. Every row states the Article 55 (or 53) sub-obligation, the Code commitment, the discharge instrument, the evidence-artefact class, the peer-role owner, the store landing, and the assurance-case anchor. The AI Office is named as the primary counterparty for the Article 55 rows.
- `code-of-practice-signatory-position.md` states the signatory / non-signatory / pending position with the signing date and the Code version signed. Each of the three Code chapters (safety-and-security, transparency, copyright) has a chapter-level discharge shape stated. If the position is non-signatory, the alternative-means argument is present with cited artefacts.
- `article-52-classification-workflow.md` covers threshold monitoring, notification content, notification wall-clock (two weeks), rebuttal path (if applicable), AI Office response handling, and assurance-bundle integration.
- `discharge-verification-walkthrough.md` walks a reviewer end-to-end in five numbered steps, resolving at least one map row from statute to a specific evidence artefact in the store.
- Every place a fact would need to be verified against the current EUR-Lex text, the current Code of Practice version, the current AI Office notification template, or the enterprise's own frontier framework is marked `<!-- needs-research: … -->` rather than guessed.
- Every artefact's owner is a single named individual with a named backup, not a team.
- The map does not duplicate content that exercises `02`–`05` produce; it cites forward to those artefacts by class and store landing.

## Stretch goals

- **Cross-map to Article 53 baseline in detail.** In `article-53-baseline-map.md`, extend the Article 53 rows into a full baseline map with the same seven-column shape. This captures the full GPAI provider obligation set (baseline plus systemic-risk overlay) that the assurance bundle must discharge.
- **Draft the AI Office correspondence stub.** In `ai-office-correspondence-stub.md`, sketch the cover letter that accompanies the Article 52 notification and the initial Article 55(1)(c) serious-incident point-of-contact designation. Include the placeholder headings for the AI Office's expected acknowledgement fields.
- **Author the Code-revision-tracking log.** In `code-revision-tracking.md`, formalise the enterprise's process for tracking Code of Practice revisions after signing — the review cadence, the responsible role, the decision routine for re-signing on a version change, and the change-log format the assurance bundle carries.
- **Cross-reference the assurance case.** In `assurance-case-integration.md`, sketch how each map row lands in the assurance case (`mod-102`) — the sub-obligation as a top-level claim, the Code commitment as the supporting context, the discharge instrument as a sub-claim, and the evidence artefact as the leaf. Include the defeater vocabulary the map row supports for post-market re-review (`mod-110`).
- **Design the multi-jurisdiction overlay.** In `multi-jurisdiction-overlay.md`, extend the map with the UK AISI and US AISI counterparty rows — how the same underlying evidence discharges obligations in adjacent regimes, and where the jurisdictions diverge (evidence access terms, reporting timelines, publication conventions). Cross-reference `mod-106`.
