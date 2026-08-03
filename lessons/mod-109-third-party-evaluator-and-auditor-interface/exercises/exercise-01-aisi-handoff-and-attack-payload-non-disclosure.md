# exercise-01: AISI Handoff and Attack-Payload Non-Disclosure

**Estimated effort:** 3 hours

## Objective

Design the **AISI-shape handoff envelope** for one frontier-tier deployment and defend the **attack-payload non-disclosure discipline** against the three specific leakage failure modes chapter `01` names (training-corpus contamination, peer-provider leakage, public-web scrape). Produce the six-component envelope, the engagement charter, and the three-pipe non-disclosure control set the programme will operate for the engagement's duration.

The exercise is design and authoring, not solving. Placeholder pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against a specific institute's current published methodology, a specific frontier-lab framework's current version, or the enterprise's own policy.

## Prerequisites

- Chapter [`01-aisi-shape-third-party-evaluators-and-attack-payload-non-disclosure.md`](../01-aisi-shape-third-party-evaluators-and-attack-payload-non-disclosure.md) — the AISI category, the six-component envelope, the three-pipe non-disclosure discipline, and the worked customer-support-agent example.
- Chapter [`06-delivery-timing-envelope-and-evidence-hardening-playbook.md`](../06-delivery-timing-envelope-and-evidence-hardening-playbook.md) — the engagement-charter template, the seven-component envelope structure, and the twenty-one-item intake checklist the playbook applies uniformly across engagement types.
- Familiarity with `mod-104` chapter `03` (reproducibility bundles) and `mod-104` chapter `06` (assurance bundle) — the primary sources for envelope assembly.
- Skim access to the UK AI Security Institute `Inspect` framework landing page ([inspect.aisi.org.uk](https://inspect.aisi.org.uk/)) and the US AI Safety Institute home page ([nist.gov/aisi](https://www.nist.gov/aisi)).

## Problem statement

Invent one enterprise frontier-tier deployment being handed to an AISI-shape evaluator. Two dimensions must be pinned before you begin the artefact set:

- **Deployment shape.** A frontier-tier deployment whose surface, tool-use envelope, and user population justify an AISI-shape engagement at the highest deployment tier. Common shapes worth considering (pick one, or invent your own):
  - **Internal-facing coding-and-agent assistant** with tool use over the repository, the CI system, and the deploy pipeline; used by engineers on production code.
  - **External customer-support agent** with tool use into the CRM, ticketing, and knowledge-base systems; used by customer-service staff and, for some interactions, directly by end-customers.
  - **Analyst-copilot** for regulated-industry decision support with tool use into internal decision-support datasets; used by internal analysts whose outputs go to external clients.
  - **Long-horizon research agent** with browser-use, code-execution, and file-system access; used by researchers for autonomous multi-step tasks.
- **Evaluator identity.** One AISI-shape evaluator (UK AI Security Institute, US AI Safety Institute, Singapore AI Verify Foundation, METR, Apollo Research, or an MLCommons AI Safety Working Group submission). The evaluator's own home-page and methodology-shape documentation is the reference for what they typically ask for.

Both choices cascade through the envelope's contents (different evaluators ask for different specific items) and through the non-disclosure discipline (different evaluators have different confidentiality profiles). Pin them before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `deployment-context-brief.md`

A two-page brief that fixes:

- **Enterprise and deployment identity.** Named enterprise, named product, one-sentence position; the release candidate's identifier (e.g., `rc-2026-05-07`); the model digest the release candidate resolves to.
- **Deployment surface.** The specific surface (chat interface, API, agentic loop), the tool-use envelope (named tools with their parameter shapes), the data-access envelope (which datasets, what retention), the user population, and the guardrail set that sits around the surface in production.
- **Deployment-tier landing.** The enterprise's tier scheme (from `mod-108`) applied to the release candidate; the axis-by-axis landing; the tier-decision artefact identifier the AISI evaluator will read to understand the release's context.
- **Frontier-lab framework alignment.** Where the foundation-model provider's own framework (Anthropic RSP / OpenAI Preparedness / Google DeepMind FSF) has a tier assessment for the underlying model, name it. The provider's tier is the *floor* for the enterprise's own tier landing (per `mod-108` chapter `01`).
- **Peer-role dependencies.** Which peer roles (`ai-risk-engineer`, `ai-eval-engineer`, `model-evaluation-engineer`, `agentic-safety-engineer` where applicable) own the evidence that will be handed over, per the `mod-101` deferral contract.
- **Prior-engagement history.** If the evaluator has previously engaged with the enterprise on a prior release, name the prior engagement and its report identifier so the new engagement can build on it (versus starting from a bespoke first-time engagement).

The brief is the *setup* the AISI evaluator reads first. Reviewers of the envelope will read it before opening any of the other four artefacts.

### 2. `handoff-envelope.md`

The six-component envelope from chapter `01`, specialised to the chosen deployment and evaluator. For each of the six components:

- **Contents.** The specific artefact(s) that satisfy the component for this engagement. Concrete — not "the deployment-tier framework document" but the specific tier-decision artefact identifier and the specific redaction pass applied to it for this evaluator's audience.
- **Owner.** The single named owner (per the seven-component owner-assignment rows in chapter `06`), with a named backup owner for continuity.
- **Digest or provenance pin.** The specific digest, commit hash, or pipeline-run identifier the artefact resolves to. Where the artefact is a redacted view of an underlying artefact, cite both the redacted-view digest and the underlying-artefact digest so the evaluator can see that the underlying evidence exists.
- **Delivery mechanism.** How the artefact is handed over (shared secure workspace, credential-scoped API endpoint, controlled-document register export).

The six components (from chapter `01`, aligned with chapter `06`'s uniform seven-component structure — the AISI shape typically leaves the QMS/AIMS component empty and marks it "not applicable" rather than omitting it):

- **Read-only credentialed access.** Credentials scoped to the pinned model digest, bounded evaluation window, rate limits, and log-store segregation. Owned jointly with `ai-infra-security` (level 35).
- **Dedicated evaluation environment.** Sandboxed instance or evaluator's own infrastructure; how evaluator traffic is segregated from production telemetry and from the training-data pipeline's ingestion allowlist.
- **Reproducibility-bundle exchange, one-way.** The `mod-104` chapter `03` bundles for the release candidate's provider-side evaluations already run — model digest, harness code, eval-set descriptors, statistical warrant.
- **Mutual non-disclosure agreement.** Bilateral NDA structure covering (a) the evaluator's attack payloads and methodology, (b) the provider's internal safety case, unpublished harm-inventory rows, and commercially-sensitive deployment context. The specific derivative-artefacts clause.
- **Provenance-preserving return channel.** Signed-artefact expectation, digest-pinning against the model version tested, transparency-log entry (Rekor or equivalent) if the evaluator publishes to one, ingestion path into the `mod-104` chapter `06` assurance bundle.
- **Post-engagement dispositions.** Written procedure for the case where the evaluator finds a capability that shifts the release's deployment tier — pause, mitigate, re-evaluate, or refuse the release. Cross-reference to the `mod-103` release-gate hook that honours the hard-fail.

### 3. `non-disclosure-control-set.md`

The three-pipe non-disclosure control set the programme operates for the engagement's duration. Chapter `01` names the three pipes explicitly: the training-data pipeline, the online-eval telemetry (`mod-104`), and the reproducibility-bundle exchange. For each pipe:

- **Failure mode being addressed.** Which of the three leakage failure modes (training-corpus contamination, peer-provider leakage, public-web scrape) the pipe's control set addresses.
- **Control mechanism.** The specific mechanism that blocks the pipe — the ingestion allowlist exclusion, the drift-detector filter, the reproducibility-bundle scope constraint. Concrete — the config setting, the IAM rule, the pipeline stage, and where the control is verified.
- **Owner.** The peer role that operates the control (`ai-infra-mlops`, `ai-eval-engineer`, `ai-infra-security`, this programme) with the backup owner.
- **Verification cadence.** How often the control is verified during the engagement window (weekly / daily / continuous) and how the verification result is recorded.
- **Post-engagement teardown.** What happens to the control after the engagement window closes — some controls remain in place (the training-data pipeline's exclusion remains as a policy); others are relaxed (the online-eval slice's filter can drop the engagement's credential identifier from its watchlist once the window closes).

Add a fourth section on **incident-tracking flagging**: how the enterprise's own incident-tracking system flags any ticket that quotes evaluator-supplied prompt content for legal review before it can be forwarded to peer teams or vendors. This is the fourth control chapter `01`'s worked example describes.

### 4. `engagement-charter.md`

The engagement charter from chapter `06`, specialised to this engagement. Sections:

- **Engagement identity.** Engagement identifier, evaluator organisation, evaluator engagement-team lead (name or role placeholder), contract reference, engagement type (`AISI-shape`), and the release candidate the engagement covers.
- **Calendar.** Report-delivery date, envelope-ready date, kick-off date, mid-engagement checkpoint date, draft-review window opening date, with the slack budget on each milestone (chapter `06`'s discipline). Cross-references to the `mod-103` release-gate cadence and any external-disclosure deadlines.
- **Six-component owner assignments.** Primary and backup owner for each of the six envelope components from artefact `2`.
- **Hardening declarations.** The specific attestation formats the envelope will carry (DSSE, in-toto, Rekor); the redaction targets applied per-leaf and calibrated to this evaluator's audience; the sampling channels the pipeline will expose.
- **Intake-checklist state.** The twenty-one-item checklist state at envelope-ready (chapter `06`). Sign-off from the release-assurance on-call and the methodology owner.
- **Return-artefact disposition.** How the evaluator's return artefact will be ingested (external-evaluator leaf in the assurance case per `mod-102` chapter `06`; validity window; re-engagement reminder date).
- **Peer-role acknowledgements.** Signed acknowledgements from each peer role whose evidence is being handed over.

### 5. `worked-defence-against-failure-modes.md`

A defence, written as an internal review memo, that walks each of chapter `01`'s four common failure modes and shows how the envelope and control set defend against it:

- **Evaluator traffic contaminates the training pipeline.** How the credentialed-access channel and the training-data pipeline's ingestion allowlist together prevent this. Cite the specific configuration and the verification cadence.
- **Safety-case draft over-redacted.** How the assurance-case-excerpt component preserves the harm-inventory shape and the deployment-tier framework's substantive criteria while redacting commercially-sensitive specifics. Cite the redact-to-audience heuristic from chapter `06`.
- **Reproducibility bundle inadequate.** How the reproducibility-bundle exchange delivers the `mod-104` chapter `03` bundle shape end-to-end (harness code, eval-set descriptors, statistical warrant) so the evaluator can distinguish new findings from re-discovery of what the programme already knew.
- **Return channel has no provenance.** How the return-channel-and-provenance-manifest component requires the evaluator to sign the report (DSSE envelope or equivalent) and to cite the model digest in the report's header. Where the evaluator publishes to a transparency log, how the log entry is recorded in the assurance bundle.

Add a fifth section on **on-call operating discipline**: what the release-assurance on-call does during the engagement window — the routine control-verification checks, the escalation path for any non-disclosure suspected breach, the responsibility for producing supplementary evidence in response to evaluator clarification requests.

## Starter guidance

- **Pin the evaluator before drafting the envelope.** Different AISI-shape evaluators ask for meaningfully different specific items even where the envelope's shape is uniform. A METR engagement's elicitation-compute footprint differs from an Apollo Research deception-evaluation setup, and both differ from a UK AI Security Institute `Inspect`-based engagement. The envelope's contents follow.
- **Frontier-tier means top of the enterprise's own tier scheme.** If the deployment lands at the enterprise's low or medium tier, an AISI-shape engagement is disproportionate and the exercise's discipline is diluted. Pick a deployment surface, tool-use envelope, and user population whose tier landing genuinely justifies the AISI-shape interface.
- **The three-pipe non-disclosure discipline is the load-bearing artefact.** The exercise's core is not the envelope's contents (which are largely mechanical); it is the discipline the programme operates to keep the payloads from leaking. Spend proportional effort on `non-disclosure-control-set.md`.
- **Ownership is single-named, not team-named.** Chapter `06` is explicit — every component and every control has a single named owner with a named backup. "The MLOps team" is not a named owner. "Alice Chen (backup: Bob Kim)" is.
- **Digest-pin every leaf.** Where you cite an artefact by digest, use a plausible placeholder digest (e.g., `sha256:a1b2c3…` or a `<!-- needs-research: … -->` marker if the actual digest scheme is unspecified). The point is the discipline of citing digests, not the specific digest values.
- **The evaluator is a peer, not an adversary.** The non-disclosure discipline is *methodology-preserving*, not *methodology-defensive*. Draft the envelope and the control set as if the goal were to help the evaluator produce the most useful possible report while preserving the payloads' evaluation utility — because that is the goal.
- **`<!-- needs-research: … -->` markers are legitimate.** Where you would need the evaluator's current published methodology, a specific frontier-lab framework's current version, or the enterprise's own policy detail, mark it rather than guessing. The AISI landscape is moving; marking is honest.

## Acceptance criteria

You have succeeded if:

- `deployment-context-brief.md` fixes the six scoping decisions (identity, surface, tier landing, framework alignment, peer-role dependencies, prior-engagement history). A reviewer can decide, from the brief alone, which evaluator has been chosen, which deployment surface is in scope, and which peer roles will be handing over evidence.
- `handoff-envelope.md` covers all six components; each component names its contents, owner (with backup), digest or provenance pin, and delivery mechanism. The QMS/AIMS component from chapter `06`'s uniform seven-component structure is either present or explicitly marked "not applicable to this engagement type."
- `non-disclosure-control-set.md` covers the three pipes (training-data pipeline, online-eval telemetry, reproducibility-bundle exchange) and the fourth incident-tracking flagging control, each with its failure-mode addressed, control mechanism, owner, verification cadence, and post-engagement teardown.
- `engagement-charter.md` is populated per chapter `06`'s template with a plausible calendar (report-delivery date, envelope-ready date back-planned, slack budgets named), the six-component owner assignments, hardening declarations, intake-checklist state, and return-artefact disposition.
- `worked-defence-against-failure-modes.md` walks each of chapter `01`'s four failure modes and cites the specific envelope component or control-set item that defends against it. The fifth on-call operating-discipline section names the escalation path and the routine control-verification checks.
- Every artefact is redacted to the *audience* — an AISI-shape evaluator gets more assurance-case shape than a Big-Four attest firm's engagement partner would; but nothing in the envelope is legally sensitive detail the evaluator's NDA is not covering.
- No component's owner is a team or role; each is a single named individual with a named backup.
- Every place a fact would need to be verified against the evaluator's current published methodology, a frontier-lab framework's current version, or the enterprise's own policy is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Add a mid-engagement clarification-response worked exchange.** In `mid-engagement-clarification.md`, author a plausible evaluator clarification request (missing evidence on a specific eval-set descriptor's coverage) and the programme's response — including the sampling query executed against the `mod-104` evidence pipeline and the supplementary evidence returned. This foreshadows chapter `06`'s mid-engagement checkpoint discipline.
- **Design the cross-institute portfolio adapter.** In `cross-institute-adapter.md`, sketch how the same envelope structure accommodates a parallel engagement with a *second* AISI-shape evaluator (the same release candidate handed to both UK AI Security Institute and METR simultaneously). Cite chapter `05`'s portfolio-adapter shape lesson.
- **Draft the post-engagement disposition runbook.** In `post-engagement-runbook.md`, walk the specific case where the evaluator's report identifies a capability that shifts the release's tier landing. What the release-gate does (`mod-103` hook); who the escalation goes to (`head-of-ai-governance`, level 60, per `mod-108` chapter `04`); what the programme's on-call does in the first twenty-four hours after receipt.
- **Cross-reference the systemic-risk overlay.** In `systemic-risk-overlay.md`, sketch how the envelope changes for a provider that is *also* an EU AI Act Article 55 systemic-risk provider (per `mod-111`). The AI Office's own supervision runs alongside the AISI-shape engagement; the envelope's provenance manifest may need to accommodate both audiences.
- **Author the `Inspect`-framework adapter note.** In `inspect-adapter-note.md`, describe how the UK AI Security Institute's `Inspect` framework is used as the shared substrate for the engagement — what task suites the enterprise's own internal AI-eval engineer runs to prepare for the evaluator's engagement, and how the resulting eval logs are shared under the reproducibility-bundle exchange.
