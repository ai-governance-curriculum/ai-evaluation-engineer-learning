# exercise-05: C2PA-Provenance and NTIA-Openness Overlay

**Estimated effort:** 2 hours

## Objective

Overlay the **content-provenance section** (C2PA producer credentials, trust-list position, chained-manifest discipline, watermarking complement) and the **openness-position section** (NTIA marginal-risk framing, mitigation set per openness position, interlock with Article 55(1)(b) Union-level assessment) onto the GPAI-systemic-risk assurance package from exercises `01`–`04`. The overlay carries the Article 50 machine-readable-marking and deep-fake-disclosure discharge, the trust-list governance decision the assurance case makes visible, and the openness reasoning that Article 55(1)(b) requires. This exercise is the final piece — chapters `01`–`04`'s discharge stops at the *evaluation and mitigation* surface; the C2PA + NTIA overlay closes the *disclosure and openness* surface.

The exercise is overlay authoring, not solving. Placeholder producer credentials, trust-list membership positions, and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the current C2PA specification version, the current NTIA report status, or an equivalent EU-side analysis.

## Prerequisites

- Chapter [`05-c2pa-provenance-and-ntia-obligations-for-genai.md`](../05-c2pa-provenance-and-ntia-obligations-for-genai.md) — the C2PA reading from the GPAI-assurance angle (manifest as evidence, trust-list as governance surface, chained manifests, redaction-aware discipline); the NTIA marginal-risk framing; the three openness positions and their mitigation sets; the interaction with Article 55(1)(b); the anti-patterns.
- Chapter [`01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md`](../01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md) — Article 55(1)(b) Union-level systemic-risk assessment; Article 50 in outline.
- Chapter [`04-safety-benchmark-evidence-citation-pack.md`](../04-safety-benchmark-evidence-citation-pack.md) — the safety-benchmark evidence the openness-position mitigation set consumes when arguing residual-risk discharge.
- Skim access to:
  - [C2PA technical specification](https://c2pa.org/specifications/specifications/) — the manifest structure, assertions, hard binding, trust list, redaction.
  - [NTIA Report on Dual-Use Foundation Models with Widely Available Model Weights](https://www.ntia.gov/programs-and-initiatives/artificial-intelligence/report-on-dual-use-foundation-models) (2024-07).
  - Regulation (EU) 2024/1689 Article 50 in the [consolidated text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj).
- Familiarity with `mod-105` chapter `06` (the deep C2PA teaching from the card-authoring side — this exercise cites into that block but does not re-teach the depth), `mod-104` chapter `04` (supply-chain provenance — the same Sigstore / Fulcio / Rekor trust ecosystem the C2PA producer credential lives inside), and `mod-110` (post-market surveillance — the openness-position re-assessment cadence).

## Problem statement

Continue from the release pinned in exercise `01`. The overlay must:

- **Match the release's modality set.** A text-only release does not carry a C2PA manifest for image / video / audio outputs; the overlay states so and cites the adjacent text-provenance mechanism (per `mod-105` chapter `06`). A multimodal release carries C2PA manifests for image / video / audio outputs and needs the trust-list-membership decision.
- **Match the release's openness position.** Closed-weight, gated-open, or open-weight — the overlay's Article 55(1)(b) mitigation set differs materially per position. State which and design the overlay accordingly.
- **Cite `mod-105` chapter `06`, not duplicate it.** The depth of the C2PA `provenance.c2pa` block on the assurance card, plus the redaction-manifest discipline, live in `mod-105` chapter `06`. This overlay cites into that block from the GPAI-assurance angle.
- **Cite the NTIA report by version and date.** The 2024-07 publication is the reference; note if any subsequent NTIA output has updated the framing.

## Requirements

Produce five artefacts in a single directory.

### 1. `provenance-and-openness-scoping-brief.md`

A one-page brief that pins the overlay's scope:

- **Release modality set.** From exercise `01` — text-only, text + image, text + image + audio, text-to-video, and so on. Each modality carries a distinct provenance mechanism; the brief names the mechanism per modality (C2PA for image / video / audio; complementary mechanism for text per `mod-105` chapter `06`).
- **Openness position.** From exercise `01` — closed-weight via API, gated-open, or open-weight. State the position and its justification (one sentence).
- **Downstream deployment shape.** Whether the release is deployed directly to end users, integrated into downstream deployer products, or made available for research access. This shape drives the chain-preservation contract.
- **In-scope Article 50 clauses.** Article 50(2) (machine-readable marking for synthetic content) applies to all output-producing GenAI systems. Article 50(4) (deep-fake disclosure) applies where the output includes image / audio / video content constituting a deep fake — cross-reference the modality set.
- **Article 55(1)(b) tie-in.** Which Union-level systemic risks the openness-position reasoning is discharging — cross-reference exercise `01`'s obligation map and exercise `03`'s AI 600-1 crosswalk.
- **Card cross-reference.** The specific `provenance.c2pa` block on the assurance card (per `mod-105` chapter `06`) the overlay cites into. Placeholder card identifier is legitimate.

### 2. `c2pa-provenance-section.md`

The content-provenance section of the assurance package. Structured as follows.

**Producer credential infrastructure.**

- The signing service that produces C2PA manifests at generation time — service name, deployment location, ownership, and the operational-security stance (weight-storage security cross-reference to Article 55(1)(d) and `mod-104` chapter `04`).
- The signing key(s) — where they live, who has access, the rotation cadence, and the audit-log format for signing events.
- The credential chain — the certificate authority whose root the producer credential chains to; whether the chain uses Sigstore / Fulcio (per `mod-104` chapter `04`) or a bespoke CA; the credential's validity period and renewal cadence.
- The audit-log ingestion — how signing events land in the store (`mod-104` chapter `01`) as content-addressed evidence.

**Manifest structure per modality.**

- For each in-scope modality, the specific C2PA assertions the manifest carries — `c2pa.ai-generated`, `c2pa.actions`, `c2pa.training-mining-and-generative-ai-use`, and any custom assertions the enterprise defines. `<!-- needs-research: verify current C2PA assertion names in the specification version -->` where uncertain.
- The hard binding (hash) algorithm and its version.
- The redaction position per audience — which assertions are visible to the public audience, which are visible to the regulator audience only, which are visible to the third-party evaluator audience under the evaluation agreement. Cross-reference `mod-105` chapter `06`'s redaction-manifest discipline.

**Trust-list membership and governance.**

- The trust list(s) the producer credential is registered under — Content Authenticity Initiative, C2PA's own, an industry-specific list, or an enterprise-internal list with a defensible root-of-trust argument.
- The trust list(s) the enterprise's own verification service consults when checking upstream manifests (for content the release ingests) — the same list, a superset, a subset with a stated reason.
- The revocation procedure — how the enterprise handles a trust-list member whose credential is revoked (upstream), and how downstream consumers handle revocation of the enterprise's own credential.
- The escalation procedure — who at the enterprise is authorised to *change* the trust-list position (add a new list, treat a specific member as untrusted following an incident). Placeholder role name is legitimate.

**Verification endpoint.**

- Where consumers verify the manifest chain for an asset produced by the release. URL placeholder acceptable.
- What the verification endpoint returns — the manifest content, the chain of signatures, the trust-list check result, and the redaction position for the requesting audience.
- The endpoint's operational-security stance — rate limiting, authentication (if any), and interlock with `mod-104` chapter `04`'s supply-chain integrity.

**Chain-preservation contract.**

- The terms in the downstream-provider integration documentation (from exercise `01`'s Model Documentation Form) that require or recommend chain preservation across downstream edits.
- The specific contract clause language (placeholder acceptable).
- The enforcement mechanism — audit rights, contractual remedies, or a *cooperative* stance (chapter `05`'s chain-preservation-without-contract anti-pattern names this).

**Article 50 discharge.**

- The specific citation into the assurance case for how the C2PA manifest infrastructure discharges Article 50(2) machine-readable-marking.
- The specific citation for how deployer contracts pass through the Article 50(4) deep-fake-disclosure obligation.
- The tool-UI disclosure design for direct deployments where the enterprise is both provider and deployer.

**Watermarking complement.**

- Where the release also carries a statistical watermarking mechanism (SynthID for text, an image-side watermark, an audio-side watermark), name it, cite `mod-105` chapter `06` for the depth, and note the detection endpoint. Chapter `05`'s watermarking-without-detector anti-pattern is what this row guards against.
- Where the release does *not* carry a watermarking mechanism for a modality, state the reason (technical impossibility, no reliable scheme for the modality, decision-in-progress) and mark `<!-- needs-research: … -->` if the reason is unstable.

### 3. `openness-position-section.md`

The openness-position section of the assurance package. Structured as follows.

**Openness position statement.**

- The specific position (closed-weight, gated-open, open-weight) with a one-paragraph justification anchored in the NTIA marginal-risk framing.
- The position's *change history* — if the release's openness position differs from a prior version, name the change, the release-triggering event that authorised it, and the re-assessment that supports it. Chapter `05`'s silent-openness-change anti-pattern names the discipline this row enforces.

**NTIA framing citation.**

- The citation of the [NTIA Report on Dual-Use Foundation Models with Widely Available Model Weights](https://www.ntia.gov/programs-and-initiatives/artificial-intelligence/report-on-dual-use-foundation-models) — publication date, version, current-status note (mark `<!-- needs-research: verify current status and any successor documents -->`).
- A one-paragraph summary of the marginal-risk framing as it applies to *this* release — not a restatement of the report, but a specific reasoning for the position.
- Any equivalent EU-side analysis cited alongside NTIA — mark `<!-- needs-research: check for AI Office / AI Board publications on the open-weights foundation-model trade-off at drafting date -->` where such an analysis may or may not exist.

**Mitigation set per position.**

For the specific openness position, enumerate the mitigation set that Article 55(1)(b) discharge relies on. Chapter `05` names three shapes:

- **For closed-weight.** Access-control mitigations — API authentication, rate limiting, TOS-based use-case restrictions, monitoring for prohibited use, kill-switch. Per mitigation: the mechanism, the owner peer role, the evidence artefact class, and the store landing.
- **For open-weight.** Intrinsic mitigations — unlearning of hazardous knowledge (cite the WMDP evidence from exercise `04`), refusal training, capability-limitation choices at training time. Plus ecosystem-level mitigations — developer-community coordination, incident-reporting channel with downstream integrators, threat-monitoring for misuse.
- **For gated-open.** A blend — some access controls (research-access gating, application-based release, staged geographic release), some intrinsic mitigations. Per mitigation: the mechanism, the owner peer role, the evidence artefact class, and the store landing.

**Interlock with Article 55(1)(b) Union-level assessment.**

- The pointer into the Union-level systemic-risk assessment artefact (from exercise `01`, `article-55-obligation-map.md`'s Article 55(1)(b) row) where the openness reasoning lives.
- The specific risk categories from the AI 600-1 crosswalk (exercise `03`) the openness position materially affects — Information Security, CBRN Information or Capabilities, Value Chain and Component Integration, and Information Integrity are the most common.
- The residual-risk narrative — what risk remains after the mitigation set is applied, and how the assurance case handles it.

**Post-market re-assessment cadence.**

- The cadence at which the openness position is re-assessed — aligned with the frontier framework's re-evaluation cadence (exercise `02`) and `mod-110`'s post-market surveillance loop.
- The signals that trigger an ad-hoc re-assessment — a serious incident in a peer release, a new capability elicitation surfacing hazardous knowledge, a legal or regulatory change, a Frontier Model Forum brief on the openness trade-off.
- The responsible role and the sign-off route.

### 4. `article-55-integration-note.md`

The overlay's tie-in to the exercise `01` obligation map. For each affected Article 55 sub-obligation, state:

- **Article 55(1)(a).** How the C2PA infrastructure attestation contributes to the state-of-the-art evaluation set (cybersecurity of the signing infrastructure is one dimension); how the watermarking-and-detector position is state-of-the-art at release date.
- **Article 55(1)(b).** How the openness-position reasoning is a first-class component of the Union-level systemic-risk assessment. The pointer at the Union-level assessment artefact, the risk categories affected, the mitigation set cited.
- **Article 55(1)(c).** How incidents in the provenance layer (a producer credential compromise; a trust-list member revocation) or in the openness layer (misuse-at-scale of an open-weight release) trigger the serious-incident procedure. Cross-reference `mod-110`.
- **Article 55(1)(d).** How the signing-service operational-security stance contributes to the cybersecurity attestation. Cross-reference exercise `01`'s Article 55(1)(d) row.

Plus, at least the following Article 53 baseline tie-ins:

- **Article 53(1)(a)–(b).** How the Model Documentation Form (from exercise `01`, transparency chapter) includes the openness-position statement and the C2PA infrastructure summary, so downstream providers know both.

### 5. `anti-pattern-audit.md`

A short audit of the overlay against chapter `05`'s named anti-patterns. For each anti-pattern, state — one sentence per — whether the overlay avoids it, and how.

Anti-patterns to audit:

- **C2PA-without-a-trust-list-position.** Where in `c2pa-provenance-section.md` the trust-list membership is named and the revocation procedure is documented.
- **Openness-as-a-checkbox.** Where in `openness-position-section.md` the NTIA framing is cited and the mitigation set is enumerated.
- **Manifest-in-transit-only.** Where the audit-log ingestion into the store is described.
- **Chain-preservation-without-contract.** Where the downstream-provider contract clause is stated.
- **NTIA-report-as-permission-slip.** Where the NTIA framing citation is *specifically* reasoned against this release, not restated as a general permission.
- **Watermarking-without-detector.** Where the detector endpoint is named per watermarking mechanism.
- **Openness-decision-without-post-market-loop.** Where the post-market re-assessment cadence is defined and the interlock with `mod-110` is stated.
- **Silent openness change.** Where the openness-position change history discipline is named.

Any anti-pattern the overlay does *not* fully avoid must be marked `<!-- needs-research: … -->` with a rationale, or documented as an intentional trade-off with a defence.

## Starter guidance

- **The overlay cites `mod-105` chapter `06`, not duplicates it.** The deep C2PA teaching lives there. This overlay reads C2PA from the *GPAI-assurance* angle: the manifest is *evidence the assurance case cites*, the trust-list is *itself a governance decision*. If the overlay carries assertion-name lists at the specification depth, the boundary has slipped.
- **The openness position drives the mitigation set.** Chapter `05` calls this out — the mitigation sets are *materially different* across the three positions. A closed-weight overlay that cites unlearning as a primary mitigation, or an open-weight overlay that cites API kill-switch as a primary mitigation, is designing the wrong overlay for the position.
- **The NTIA framing is not a permission slip.** Chapter `05`'s NTIA-report-as-permission-slip anti-pattern is easy to reintroduce. The overlay's NTIA citation *does* the marginal-risk analysis for this release; it does not merely repeat the report's headline recommendation.
- **The chain-preservation contract is *cooperative*.** Chapter `05` names this — chain preservation across downstream edits is enforced through the downstream-provider contract, not through technical mechanism alone. The overlay's contract clause is what makes chain preservation actionable.
- **The trust-list position is a first-class governance decision.** Which lists the enterprise is on, which lists it consults, and who has authority to change the position — all are visible in the assurance case. Chapter `05`'s C2PA-without-trust-list anti-pattern is what this discipline guards against.
- **Watermarking and C2PA are complements, not substitutes.** For text outputs (and for many other modalities), statistical watermarking survives transformations that strip C2PA manifests, and C2PA survives content transformations that watermarking cannot. The overlay carries both where the modality supports both.
- **The post-market re-assessment cadence is release-triggering-adjacent.** A change in the openness position triggers a new release; a serious incident in a peer's release may trigger a re-assessment even without a new release. Cross-reference `mod-110`.
- **`<!-- needs-research: … -->` is a legitimate answer.** The current C2PA specification version, the current status of the NTIA report and its successor documents, current AI Office publications on open-weights foundation models, and the current watermarking mechanisms available per modality all drift. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `provenance-and-openness-scoping-brief.md` fixes the modality set, the openness position, the downstream deployment shape, the in-scope Article 50 clauses, the Article 55(1)(b) tie-in, and the card cross-reference.
- `c2pa-provenance-section.md` covers producer-credential infrastructure, manifest structure per modality, trust-list membership and governance, verification endpoint, chain-preservation contract, Article 50 discharge, and watermarking complement. Every sub-section carries a specific position or a `<!-- needs-research: … -->` marker; no sub-section is elided.
- `openness-position-section.md` covers the openness position statement (with change history), NTIA framing citation, mitigation set per position (matching the position from artefact 1), interlock with Article 55(1)(b), and the post-market re-assessment cadence.
- `article-55-integration-note.md` names the tie-in for each of Article 55(1)(a)–(d) plus Article 53(1)(a)–(b). Cross-references to exercise `01`'s obligation map are explicit.
- `anti-pattern-audit.md` audits every anti-pattern from chapter `05`, one sentence per, with either an avoidance explanation or a `<!-- needs-research: … -->` marker with rationale.
- The overlay cites `mod-105` chapter `06` for the depth of C2PA card content, not duplicates it.
- The mitigation set matches the openness position — closed-weight overlays cite access controls; open-weight overlays cite intrinsic and ecosystem mitigations; gated-open overlays blend both.
- Every place a fact would need to be verified against the current C2PA specification, current NTIA output, or an equivalent EU-side analysis is marked `<!-- needs-research: … -->` rather than guessed.
- The chain-preservation contract clause is present and enforcement is stated.
- The post-market re-assessment cadence is aligned with the frontier-framework cadence from exercise `02`.

## Stretch goals

- **Draft the trust-list-membership charter.** In `trust-list-membership-charter.md`, sketch the enterprise's charter for trust-list membership decisions — the criteria for adding a list, the criteria for consulting a list, the review cadence, the escalation route on incidents, the interlock with `mod-104` chapter `04`. This is the governance artefact behind the trust-list position from `c2pa-provenance-section.md`.
- **Author the Article 50 pass-through language.** In `article-50-pass-through-clause.md`, write the specific contract clause language the enterprise uses in downstream-provider integration to pass through the Article 50(4) deep-fake-disclosure obligation. Include the exception language for the Article 50(4) narrow exceptions.
- **Design the openness-position change-log.** In `openness-position-change-log.md`, define the format of the change-log the assurance bundle carries — one entry per openness-position change, with the trigger, the re-assessment reference, and the signer. Cross-reference `mod-110`.
- **Cross-reference `mod-105`.** In `mod-105-alignment-note.md`, describe how the `c2pa-provenance-section.md` cites into the assurance card's `provenance.c2pa` block (per `mod-105` chapter `06`) and how the two artefacts stay in sync across releases.
- **Draft the incident-in-provenance-layer procedure.** In `provenance-incident-procedure.md`, define the specific serious-incident procedure for a producer credential compromise or a trust-list-member revocation — the wall-clock, the notification counterparty (AI Office under Article 55(1)(c); Content Authenticity Initiative or C2PA's trust-list steward), and the interlock with `mod-110`'s Article 73 workflow.
