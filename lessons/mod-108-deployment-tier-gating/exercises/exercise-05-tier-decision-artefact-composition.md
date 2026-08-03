# exercise-05: The Tier-Decision Artefact — Composition End-to-End

**Estimated effort:** 3 hours

## Objective

Compose the **full tier-decision artefact** for one candidate release of the product you scoped in exercises `01`–`04`, walking each of the eight sections from chapter `05`. The artefact is *the* output of the tier gate — a single, versioned, digest-pinned, signed document that the release-gate walker reads and that hangs off the assurance case as the concentrated discharge of the tier claim.

The exercise is composition, not authoring from scratch. The prior four exercises produced the *substantive content*; this exercise composes them into the artefact shape, adds the sections that live only at the composition layer (system identity, deployment context, decision-with-reviewers-and-expiry, assurance-case join, multilateral context), and delivers the artefact into the release package.

Two prior-exercise dependencies are load-bearing: without them, this exercise has nothing to compose. If you have not completed exercises `01`–`04` you can substitute short placeholder content for each section, but the composition-layer discipline is where the exercise sits.

## Prerequisites

- Chapter [`05-tier-decision-artefact-and-multilateral-context.md`](../05-tier-decision-artefact-and-multilateral-context.md) — the eight-section schema, the composition with the assurance case and the release package, and the multilateral context.
- Chapters `01`–`04` — the substantive content composed into sections 2–5.
- Exercises `01`–`04` — the artefacts composed into the tier-decision artefact.
- Skim access to the multilateral-context references:
  - [Bletchley Declaration](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration) — 2023-11.
  - [Seoul Declaration and Frontier AI Safety Commitments](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — 2024-05.
  - [Paris AI Action Summit](https://www.elysee.fr/en/sommet-pour-l-action-sur-l-ia) — 2025-02. <!-- needs-research: confirm the current Elysée URL for the summit outcome documents; the URL structure may have shifted. -->
  - [Frontier Model Forum](https://www.frontiermodelforum.org/) — pick one recent publication to cite in the artefact.
- Familiarity with `mod-102` (assurance-case engineering) — the artefact hangs off the assurance case as a concentrated discharge of the tier claim.
- Familiarity with `mod-104` (evaluation evidence pipeline) — the artefact slots as an immutable file in the release package with a cryptographic digest.

## Problem statement

Produce the complete tier-decision artefact for the current release candidate of your product. The artefact is a *single file* with eight sections; each section carries an owner and, where applicable, a signer.

Two failure modes to design against, both from chapter `05`:

- **Restating the assurance case.** The tier-decision artefact should not read as a mini-assurance-case; it should *concentrate* the case's leaves at the tier boundary. If your artefact restates the case's argument, delete the restatement and cite the case.
- **Mutability.** The tier-decision artefact is a governance artefact. Once signed, it is immutable. Updates are *new* artefacts referencing prior ones, never rewrites. The exercise's artefact is authored under this assumption — versioning and prior-artefact references are explicit.

## Requirements

Produce three artefacts in a single directory.

### 1. `tier-decision-artefact.md` (or `.yaml`, or `.json` — see below)

The artefact itself. You may author it as Markdown (most legible), YAML / JSON (most machine-consumable), or a hybrid (Markdown with structured front-matter). The choice is yours; state and justify it in one sentence at the top.

The artefact has eight required sections. Each section is *explicit* in the artefact — even short sections should carry the section heading and owner line.

#### Section 1 — System identity

Fields:

- **System name and version.** The release-candidate identifier, resolvable back to a specific model version, prompt version, tool-set version, guardrail configuration, and infrastructure baseline.
- **Deployment identifier.** The product surface the tier decision applies to.
- **Assurance-case reference.** Pointer into `mod-102`'s assurance case for this deployment. Placeholder or `<!-- needs-research: … -->` where the case ID would exist in the real programme.
- **Prior tier-decision reference.** Pointer to the previous artefact this release supersedes; `<none>` if this is the first tier decision.
- **Framework version references.** Which version of the internal tier scheme (exercise `01`), threshold-spec catalogue (exercise `02`), cybersecurity-attestation template (exercise `03`), reversal-runbook (exercise `04`).

#### Section 2 — Deployment context

Fields:

- **Tier landing.** The vector across the tier scheme's axes (or the single-ladder tier), from exercise `01`.
- **Population served.** Who is on the receiving end.
- **Tool set.** Named tools and their invocation modes (read-only, write, autonomous-chain).
- **Data access.** Which data sources, at what granularity, under what tenancy constraints.
- **Jurisdictions.** The jurisdictions in scope; sector-rule map (`mod-107`) if applicable.
- **Contracted counterparties.** Any deployer whose contract commits the enterprise to specific tier configurations.

#### Section 3 — Capability-evidence set

Pull from exercise `02`. Per threshold spec:

- **Threshold-spec identifier.** From the exercise `02` catalogue.
- **Evidence artefact reference.** Pointer into the evidence pipeline (`mod-104`), with the artefact's cryptographic digest (use `<digest-placeholder>` where a real digest would exist).
- **Measurement summary.** Point estimate, confidence interval, estimator, pass / fail decision under the spec's decision rule. Use placeholders for numerical values, not fabricated numbers.
- **Peer-track owner signature.** Named peer-role signature confirming the artefact.

#### Section 4 — Cybersecurity-attestation section

Pull from exercise `03`. Sub-sections:

- **SAIF frame.** One paragraph referencing the enterprise SAIF posture; `head-of-ai-infrastructure` signature.
- **NCSC lifecycle attestation.** Per lifecycle stage, per-guideline table with evidence pointers; `ai-infra-security` (+ `ai-infra-mlops` for secure development) signature.
- **OWASP LLM Top 10 coverage table.** Per risk, mitigation and evidence pointer; `ai-infra-security` signature.
- **MITRE ATLAS adversarial-eval index.** ATLAS-technique table with coverage disposition; peer signature for the report, methodology-owner consumption signature for the index.

The full sub-content need not be reproduced verbatim from exercise `03`; a pointer with a short summary is legitimate as long as the substantive artefact from exercise `03` is referenced.

#### Section 5 — Kill-switch, rollback, downgrade, do-not-deploy design

Pull from exercise `04`. Fields:

- **Kill-switch.** Named mechanism pointer, authoriser per trigger class, tested-cadence evidence, default-state under control-plane outage.
- **Rollback.** Named prior state(s), RTO, tested-cadence evidence, authoriser per trigger class.
- **Downgrade paths.** Per axis, the downgrade increment(s) and their triggers.
- **Do-not-deploy conditions.** The mandatory conditions and the escalation-contract signer.

#### Section 6 — Decision, rationale, reviewers, expiry

The methodology-owner half of the release-decision. Fields:

- **Disposition.** One of: `promote at tier T`; `promote at tier T with deferred criterion X (expiry Y)`; `do not promote`; `downgrade to tier T'`; `do-not-deploy`.
- **Rationale.** Prose citing the capability-evidence set (section 3), the cybersecurity attestation (section 4), and the residual-risk register position. Two to four paragraphs.
- **Reviewers.** Named methodology owner, release-owner, peer-specialist signers (as required per the disposition), `head-of-ai-governance` countersign (as required for tier-boundary crossings).
- **Expiry.** Wall-clock or milestone at which the tier decision must be re-evaluated. Typical drivers: capability-evidence expiry (from exercise `02`'s threshold-drift plan), post-market-surveillance triggers (`mod-110`), framework-version changes (any of the four preceding chapters' frameworks).

#### Section 7 — Assurance-case join

A short section pointing into the assurance case (`mod-102`) where the tier decision lands. Fields:

- **Case reference and claim ID.** The specific claim (in GSN or CAE terms) this artefact discharges.
- **Sub-claims discharged.** The set of sub-claims (capability evidence, mitigation obligations, reversal design) this artefact's leaves aggregate.
- **What the artefact does *not* discharge.** Sub-claims of the case that live outside the tier gate (e.g., the operating-model-level claims in `mod-112`; the post-market-surveillance claims in `mod-110`).

If your reader cannot walk from the assurance-case claim to this artefact and back to the evidence in one hop, the join is not doing its work.

#### Section 8 — Multilateral-context citation

One to three paragraphs positioning the artefact in the multilateral context. Cover:

- **Which frameworks the artefact's *shape* mirrors.** Cite the Seoul Frontier AI Safety Commitments and one of the three source frameworks (Anthropic RSP / OpenAI Preparedness / Google DeepMind FSF) as the shape reference.
- **Which multilateral commitments the artefact's *substance* aligns with.** Where applicable, cite the Bletchley Declaration (as origin), the Seoul Declaration (as multilateral commitment), and the Paris AI Action Summit (as extended agenda).
- **Which Frontier Model Forum publication the artefact's specific design choices *reference*.** Pick one recent Frontier Model Forum publication and cite it in the context section. State how the publication informed the section's design (e.g., statistical framing of evidence; reversal-design pattern; evaluation methodology).

Keep the section short. It is a citation section, not an argument section.

### 2. `composition-checklist.md`

A short checklist that a reviewer runs against the tier-decision artefact before it is admitted to the release package. Cover:

- **Every section is present and non-empty.** No section is `TBD`.
- **Every section has an owner line and (where applicable) a signer line.**
- **Every evidence pointer resolves.** Not just "there is a pointer" — the pointer resolves to an artefact in the evidence pipeline. Placeholders (`<digest-placeholder>`) are acceptable for the exercise; in real practice, unresolved pointers are gate defects.
- **Every threshold-spec measurement has a statistical framing.** No point estimate without a confidence interval.
- **Every OWASP LLM Top 10 row is either discharged (with evidence pointer) or declared residual (with compensating control and expiry).** No row is silently blank.
- **Every ATLAS technique in the index has a coverage disposition.** No technique is silently uncovered.
- **Every kill-switch / rollback / downgrade path has a signer.** No pathway is designed without a named authoriser.
- **The disposition is one of the pre-declared values.** No freeform disposition.
- **The expiry is named.** No "TBD" or "on request."
- **The assurance-case join names a specific claim.** No handwaving pointer.
- **The multilateral-context section cites at least one framework, at least one summit, and at least one Frontier Model Forum publication.** No missing citations.
- **The artefact's version and prior-artefact reference are explicit.** The immutability discipline is respected.

The checklist is a *gate*, not a soft guideline. State the disposition for a checklist failure: rework of the artefact by the methodology owner, or (if the failure is a peer-track evidence deficit) a deferred criterion with expiry.

### 3. `release-package-manifest-slot.md`

A short artefact that specifies where the tier-decision artefact slots in the release package (`mod-104`). Cover:

- **File location.** The path or manifest entry the tier-decision artefact lives at inside the release package.
- **Cryptographic digest.** How the artefact is digest-pinned (algorithm, content-addressing scheme). Use `<placeholder>` where a real digest would exist.
- **Signer keys.** The public keys or signature-verification chain for each signer named in the artefact (methodology owner, peer signers, head of AI governance). Placeholders acceptable.
- **Immutability discipline.** The rule that a *new* tier-decision artefact is authored (rather than the existing one edited) when an update is required. The rule references chapter `05`.
- **Supersession semantics.** How the release-gate walker knows which tier-decision artefact is current — the manifest entry, the supersedes-reference, and the audit-trail rule that the *prior* artefact remains readable (marked superseded, not deleted).
- **External-consumer paths.** How the artefact is surfaced (or excluded) for external consumers:
  - Notified body dossier (`mod-109`) — full artefact included.
  - Sector-regulated evidence set (`mod-107`) — full artefact included; sector-specific sub-sections attached.
  - External-audience system card (`mod-105`) — a *derived* paragraph is included in the card; the artefact itself is not.
  - Public statement (if any) — the multilateral-context section may be echoed; the substantive evidence set is not.

## Starter guidance

- **Compose, do not re-author.** The artefacts you produced in exercises `01`–`04` are the substantive content. This exercise is the composition layer — the artefact schema, the section boundaries, the section owners and signers, the section-to-section coherence.
- **The tier-decision artefact is not a mini-assurance-case.** If your section 3 restates the assurance case's argument, delete the restatement and cite the case. The tier-decision artefact *concentrates* the case's leaves at the tier boundary; it does not *duplicate* the case.
- **Immutability is a design commitment, not a technical one.** Even in Markdown, the artefact carries a version, a supersedes-reference, and a signed timestamp — because updates are *new* artefacts, not rewrites. State the versioning discipline explicitly.
- **Every signer is named.** Section owners are always named; where a signer is required (peer sign-off, methodology-owner sign-off, head-of-AI-governance countersign), the signer is named. `<placeholder>` is fine; `TBD` is not.
- **Placeholder numbers, not fabricated numbers.** For confidence intervals, digests, timestamps, and cryptographic signatures, use `<placeholder>` markers. Do not fabricate measured values.
- **The multilateral-context section is short.** One to three paragraphs. It is a citation section, not an argument section.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the current Seoul signatory list, the current Frontier Model Forum publication set, the enterprise's specific assurance-case claim IDs, or the release-package manifest schema, mark it rather than guessing.
- **The composition checklist is the gate.** Run it against your artefact before you submit the exercise. If a row fails, fix the artefact.

## Acceptance criteria

You have succeeded if:

- `tier-decision-artefact.md` (or `.yaml` / `.json`) is a single file with all eight sections present and non-empty. Each section has an owner line and (where applicable) a signer line. The artefact's format choice is stated and justified.
- Section 1 (system identity) names the system, version, deployment identifier, assurance-case reference, prior tier-decision reference (or `<none>`), and framework version references.
- Section 2 (deployment context) names the tier landing, population, tool set, data access, jurisdictions, and contracted counterparties.
- Section 3 (capability-evidence set) has one entry per threshold spec from exercise `02`. Each entry has a spec identifier, evidence artefact reference with digest placeholder, measurement summary with statistical framing (placeholders for numbers), and peer signature line.
- Section 4 (cybersecurity attestation) references or reproduces the SAIF frame, NCSC lifecycle attestation, OWASP LLM Top 10 coverage table, and MITRE ATLAS index from exercise `03`. Peer signatures are named.
- Section 5 (reversal design) references the kill-switch, rollback, downgrade, and do-not-deploy pathways from exercise `04`. Signers are named per pathway.
- Section 6 (decision) names one of the pre-declared dispositions, a two-to-four-paragraph rationale citing sections 3 and 4, named reviewers, and a specific expiry.
- Section 7 (assurance-case join) names a specific claim in the assurance case and lists the sub-claims this artefact discharges (and does not discharge).
- Section 8 (multilateral context) cites at least one source framework (RSP / Preparedness / FSF), at least one summit (Bletchley / Seoul / Paris), and at least one Frontier Model Forum publication.
- `composition-checklist.md` covers every checklist row from the requirements. The disposition for a checklist failure is stated.
- `release-package-manifest-slot.md` names the file location, digest, signer keys, immutability discipline, supersession semantics, and external-consumer paths.
- The artefact is *internally consistent* — the tier landing in section 2 matches the tier discharged in section 3, the mitigation obligations at the tier match the cybersecurity attestation in section 4, the reversal design in section 5 matches the tier's blast-radius, the disposition in section 6 is consistent with the evidence in sections 3–5, the assurance-case claim in section 7 matches the disposition.
- No section reads as a mini-assurance-case. Every section reads as a *concentrated* discharge of the case's argument at the tier boundary.
- Every place a fact would need to be verified against the enterprise's own artefacts, the assurance case, the release-package manifest schema, or a current multilateral publication is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Author two consecutive tier-decision artefacts to demonstrate supersession.** In addition to the current artefact, author a prior-release artefact (`td-<product>-v0.md`) and the current artefact (`td-<product>-v1.md`). Explicitly wire the supersedes-reference. Note the deltas between the two.
- **Draft the external-card paragraph derived from the artefact.** In `external-card-tier-paragraph.md`, sketch the paragraph in `mod-105`'s external-audience system card that is *derived* from this artefact's section 2 and section 4. The external-card paragraph is stripped of internal identifiers and evidence pointers; it retains the tier landing, the mitigation posture, and the reversal-design commitment.
- **Draft the notified-body dossier cover page.** For a product that falls under Annex III high-risk, in `notified-body-cover-page.md`, sketch the cover page a notified body (`mod-109`) would see when opening the tier-decision artefact as part of the conformity assessment.
- **Compose the sector-overlay sub-section.** For a product in a sector-regulated context (DORA, SR 11-7, FDA GMLP), in `sector-overlay-sub-section.md`, sketch the sector-specific sub-section that attaches to the tier-decision artefact — the sector-rule article citations, the additional signers, the additional evidence pointers.
- **Author the "artefact is stale" trigger memo.** In `staleness-trigger-memo.md`, sketch the memo the release-gate walker fires when the tier-decision artefact's expiry (section 6) arrives without re-authoring. The memo goes to the methodology owner, the release-owner, and the head of AI governance; it names the operational disposition (continue with a deferred criterion; downgrade; kill-switch; do-not-deploy).
- **Cross-map the artefact to `mod-111`'s GPAI systemic-risk obligations.** For a GPAI systemic-risk deployment, in `gpai-crossmap.md`, sketch how the tier-decision artefact aligns with EU AI Act Article 55 obligations — the capability-evaluation, systemic-risk-mitigation, cybersecurity, and incident-reporting rows. The tier-decision artefact composes with the Article 55 obligation set; sketch the mapping.
- **Author the Frontier Model Forum publication-reading log.** In `fmf-publication-log.md`, list the two or three Frontier Model Forum publications you actually opened while composing this artefact, and note which section each publication informed. This is the reading log an external auditor might ask for.
