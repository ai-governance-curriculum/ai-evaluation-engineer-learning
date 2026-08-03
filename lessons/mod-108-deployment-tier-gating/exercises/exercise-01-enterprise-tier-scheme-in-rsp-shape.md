# exercise-01: Enterprise Tier Scheme in the RSP / Preparedness / FSF Shape

**Estimated effort:** 3 hours

## Objective

Author the **enterprise tier-gating scheme** for one enterprise deployment programme, adapted from the shape shared by Anthropic RSP, OpenAI Preparedness, and Google DeepMind FSF. Produce a small, defensible tier scheme — the axes, the bandings, the permission envelopes at each band, the mitigation-obligation set at each band, and the *tier landing* for at least two concrete deployment products the programme carries.

The exercise is design and authoring, not solving. Placeholder evidence pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the enterprise's own policy, its foundation-model provider's own documentation, or a specific standard's current wording.

## Prerequisites

- Chapter [`01-deployment-tier-gating-shape-across-frontier-labs.md`](../01-deployment-tier-gating-shape-across-frontier-labs.md) — the frontier-lab pattern, the three source frameworks, and the shape-versus-labels distinction.
- Skim access to at least one of the three source frameworks end-to-end:
  - [Anthropic Responsible Scaling Policy](https://www.anthropic.com/rsp).
  - [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/).
  - [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/).
- Familiarity with `mod-103`'s surface-specific gate variants (T0..T4) — this exercise's capability-envelope tier vector composes *with* that surface tier, not *instead of* it.
- Familiarity with the peer-role registry — the tier scheme's mitigation obligations name the peer role that produces the evidence (`ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`, `ai-infra-security`, `ai-infra-mlops`).

## Problem statement

Invent one enterprise deployment programme that carries at least two distinct AI products on shared foundation-model infrastructure. The tier scheme you author must be able to *land* both products at meaningfully different points in the scheme — otherwise the scheme is not exercising its axes. Common pairings worth considering (pick one, or invent your own):

- **Professional-services firm** deploying (a) an internal-facing coding-assistant integrated with the developer IDEs and repositories, and (b) an external customer-support agent with tool-use into the CRM and ticketing systems.
- **Consumer software company** deploying (a) an internal analyst-assistant that summarises product-usage telemetry, and (b) an in-product AI feature that authors user-facing content from a natural-language prompt.
- **Healthcare provider group** deploying (a) an internal clinician-note summarisation tool with human review, and (b) a patient-facing symptom-triage assistant that recommends next-step care (advisory only; hand-off to a clinician).
- **Financial-services firm** deploying (a) an internal middle-office assistant that reconciles trade breaks, and (b) a client-facing wealth-management chat assistant that answers portfolio questions inside a strictly scoped envelope.
- **Government agency** deploying (a) an internal caseworker-assistant that drafts case summaries, and (b) a public-facing benefits-eligibility screening assistant.

Pin the enterprise and both products before you begin the artefact set. The enterprise's regulatory context (EU / US / sector-regulated / consumer-facing) and the two products' contrasting risk profiles are the material the tier scheme exercises.

## Requirements

Produce five artefacts in a single directory.

### 1. `enterprise-context-brief.md`

A one-page brief that fixes:

- **Enterprise name and one-sentence position.** Named enterprise; the AI deployment programme's stated mission; the release-assurance methodology owner's role within it.
- **Foundation-model provider(s).** Which provider(s) the enterprise sources from; whether the enterprise is a single-provider or multi-provider shop; whether any first-party fine-tuning is in scope.
- **Product portfolio.** The two (or more) products the tier scheme will serve, each with a one-line description and its intended user population.
- **Regulatory reach.** Jurisdictions the enterprise ships into (EU / UK / US / other), sector rules that attach (SR 11-7, DORA, FDA GMLP, CFPB, EEOC — cross-reference `mod-107` where a sector rule applies), and whether any of the products falls under EU AI Act Annex III high-risk categories.
- **Provider-side tier context.** For each foundation-model provider, name the tier assessment the provider currently publishes for the model(s) the enterprise consumes (Anthropic ASL, OpenAI Preparedness levels, Google DeepMind FSF CCLs). This is the *floor* the enterprise's tier scheme sits above.
- **Escalation contract sketch.** Named `head-of-ai-governance` role (or a stand-in name for the exercise), reporting-line note, and one-sentence description of the escalation contract for tier-boundary crossings.

The brief is the *setup* for the tier scheme. Reviewers of the tier scheme will read this first.

### 2. `tier-scheme.md`

The tier scheme itself. Structured as follows.

**Shape choice.** Explicit statement of whether the enterprise scheme is:

- **Single-ladder** (Anthropic RSP style — one linear tier ladder, e.g. `T1`..`T4`+), or
- **Vector** (OpenAI Preparedness / Google DeepMind FSF style — a vector of axes × bandings), or
- **Hybrid** (a small vector of axes, with a *summary* tier level as a communication convenience).

Whichever you choose, justify it against the enterprise's product portfolio. A single-ladder scheme is easier to communicate but forces the highest-risk axis to dominate; a vector is more honest but requires more discipline. State which trade-off applies to your enterprise and why.

**Axes** (if vector or hybrid). Two to five axes is the useful range. For each axis:

- **Axis name and one-line definition.** Concrete, enterprise-specific — not "cyber-offensive uplift on the open internet" (a frontier-lab category) but something like "cross-tenant data exfiltration blast-radius via tool-use" (the enterprise adaptation). Examples from chapter `01`: `data-access blast-radius`, `tool-invocation autonomy`, `external-user reach`, `regulated-sector exposure`. Feel free to invent axes that fit your portfolio (`autonomy-of-consequential-action`, `retention-of-user-content`, `judgement-authority-over-clinical-decision`, etc.).
- **Bandings.** For each axis, name three to four bandings (typically `Low / Med / High / Critical`, adapted from Preparedness). For each banding, state:
  - **Permission envelope.** What the banding *admits* — concrete permissions expressed in the language of the deployment surface (which tools, which populations, which data, which retention, which autonomy).
  - **Mitigation obligations.** What must be true at the deployment surface for the tier to sit at this banding — guardrail set, monitoring detectors, human-oversight design, cybersecurity-attestation depth (foreshadow chapter `03`), kill-switch design (foreshadow chapter `04`), capability-evidence threshold (foreshadow chapter `02`).
  - **Peer-track evidence.** Which peer track owns the evidence that discharges the mitigation obligations at this banding.

**Tier landings.** For each product in the portfolio, name the *tier landing* — the point in the scheme (single-ladder tier level, or the vector across the axes) the product currently occupies — with a one-paragraph justification. The two products should land at meaningfully different points; if they do not, the scheme's axes are not doing their work.

### 3. `provider-floor-map.md`

The provider-tier-as-a-floor map. For each foundation-model provider the enterprise consumes:

- **Provider tier assessment.** The provider's own tier assessment for the model in use (link to the provider's own published policy).
- **Provider deployment standard.** What the provider commits to (or requires of deployers) at that tier — data-handling obligations, misuse-hardening obligations, kill-switch commitments, safety-testing obligations, incident-reporting obligations. Cite the provider's terms of service, use policy, and safety framework directly.
- **Enterprise delta.** For each product landing on this provider, name the *delta* — where the enterprise's deployment context imposes *stricter* obligations than the provider's floor, and where it does *not*. Deltas typically arise because the enterprise's population, tool-set, or data-access is more restrictive (or less restrictive) than the provider's baseline envisages.
- **Contract touchpoints.** Where the provider's terms of service, enterprise agreement, or DPA carries an obligation that lands in the tier scheme's mitigation set (data-processing terms, model-usage restrictions, prohibited use cases, sub-processor rules).

If the enterprise sources from multiple providers, produce one section per provider. If the enterprise uses a first-party fine-tuned derivative, note that the derivative may sit at a *different* provider-tier assessment than the base model, and the enterprise carries a *heavier* attestation burden as a consequence.

### 4. `frontier-lab-shape-crosswalk.md`

A crosswalk table showing how the enterprise scheme in `tier-scheme.md` maps to each of the three source frameworks. The crosswalk demonstrates that the enterprise adopted *the shape*, not the labels — and it gives an external reviewer a bridge from their own familiar framework into the enterprise's scheme.

Columns:

| Enterprise scheme element | Anthropic RSP counterpart | OpenAI Preparedness counterpart | Google DeepMind FSF counterpart | Notes |
| --- | --- | --- | --- | --- |
| Single-ladder vs vector shape | | | | |
| Each axis (rows per axis) | | | | |
| Each banding within each axis | | | | |
| Escalation trigger | | | | |
| Mitigation coupling | | | | |
| Periodic re-evaluation channel | | | | |
| Mitigation-effectiveness measurement | | | | |

The crosswalk is *approximate* — the frontier-lab categories are calibrated to model-producing organisations, and the enterprise's categories are calibrated to a downstream deployer. Where the mapping is not clean, note that and defend the enterprise's substitution.

### 5. `axis-drift-and-review-plan.md`

The scheme is not fixed for all time. Frontier-lab publications, provider policies, sector rules, and the enterprise's own product portfolio all change. Author a short plan for keeping the scheme current:

- **Review cadence.** How often the scheme is opened for review (e.g., quarterly for provider-side changes, annually for scheme-shape changes, ad-hoc on a triggering event).
- **Triggering events.** Specific events that force an ad-hoc review — a provider updates its RSP / Preparedness / FSF equivalent; a new EU AI Act delegated act attaches; a Frontier Model Forum publication introduces a new evaluation category; a serious incident at the enterprise or at a peer.
- **Signers.** Who signs the scheme at each review. Head of AI governance signs at scheme-shape changes; the methodology owner signs at within-shape banding refinements.
- **Versioning.** How the scheme's version is pinned into each tier-decision artefact (foreshadow chapter `05`) — new artefacts cite the current scheme version, prior artefacts remain valid against the scheme version they were authored under.
- **Deprecation.** How an axis or a banding is deprecated (e.g., a banding that no product has occupied in two review cycles). Deprecation is not silent — it lands in a change-log the release-package can cite.

## Starter guidance

- **Fix scoping first, then design.** The enterprise's regulatory context, foundation-model providers, and the two products' contrasting risk profiles cascade through the axes and bandings. Getting them wrong on the context brief means restructuring the scheme.
- **Two products, meaningfully different landings.** If both products land at `(Low, Low, Low, Low)`, the scheme is not exercising its axes and the exercise's discipline is lost. If both land at `(Critical, Critical, Critical, Critical)`, the scheme is not distinguishing between them either. Push at least one axis into contrast between the two products.
- **The enterprise adopts the shape, not the labels.** Do not import the Anthropic ASL labels (`ASL-2`, `ASL-3`, `ASL-4`) directly; the labels are calibrated to frontier-lab capability categories, not to enterprise deployment contexts. Use your own axis names and your own bandings.
- **Two to five axes is the useful range.** One axis is a single ladder in disguise. Six or more axes become an unweighted checklist and the tier landing is illegible. Preparedness's original four categories (Cyber, CBRN, Persuasion, Model Autonomy) is a good landmark; adapt it to your enterprise.
- **Enterprise-specific axes only.** "Cyber-offensive uplift on the open internet" is a frontier-lab category. The enterprise adaptation is "cross-tenant data exfiltration via tool-use in the customer-support workflow" or "prompt-injection-triggered write-tool invocation." Frame the axis at the level where the enterprise's mitigations can meaningfully attach.
- **The provider tier is a floor, not a ceiling.** The enterprise cannot deploy at a *lower* mitigation level than the provider requires. But the enterprise's deployment context may impose *higher* mitigations than the provider's baseline envisages. Both cases show up in the provider-floor map.
- **Periodic re-evaluation and mitigation-effectiveness measurement are non-negotiable.** The FSF's contributions to the pattern are the pair of primitives — the enterprise scheme should adopt them explicitly. Note in the axis-drift-and-review-plan how the periodic re-evaluation cadence attaches; note in the tier scheme how mitigation-effectiveness measurement discharges a mitigation obligation.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the enterprise's own policy, the provider's current published tier, or a specific sector-rule wording, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `enterprise-context-brief.md` fixes the six scoping decisions with reasoning. A reviewer can decide, from the brief alone, the enterprise, the two products, the providers, the regulatory reach, and the escalation contract.
- `tier-scheme.md` states the shape choice (single-ladder / vector / hybrid) and justifies it; enumerates two to five axes each with three to four bandings; each banding names its permission envelope and mitigation obligations; the two products land at *meaningfully different* points in the scheme with a paragraph of justification each.
- `provider-floor-map.md` covers every foundation-model provider the enterprise consumes; for each provider, the provider tier, the provider deployment standard, the enterprise delta, and the contract touchpoints are named. Multi-provider deployments have one section per provider.
- `frontier-lab-shape-crosswalk.md` maps the enterprise scheme to each of the three source frameworks in a table. Where the mapping is not clean, the substitution is noted and defended.
- `axis-drift-and-review-plan.md` covers the review cadence, triggering events, signers, versioning, and deprecation. Head of AI governance's signing role is named for scheme-shape changes.
- The two products' tier landings are *internally consistent* — the mitigation obligations at each landing match the peer-track evidence the enterprise can plausibly produce.
- Every place a fact would need to be verified against the enterprise's own policy, a provider's current published tier, or a specific sector rule is marked `<!-- needs-research: … -->` rather than guessed.
- No axis is a frontier-lab category imported without adaptation. Every axis names its enterprise-specific formulation.

## Stretch goals

- **Add a third product with a contested tier landing.** In `tier-landings-extended.md`, add a product whose tier landing is genuinely arguable (a customer-facing analytics assistant that is *not quite* a decision-support system; an internal tool whose users occasionally hand its outputs to customers). Author the two-column landing-decision memo: business-owner's proposed landing, methodology-owner's proposed landing, disposition and rationale.
- **Author the mitigation-effectiveness measurement plan for one axis.** In `mitigation-effectiveness-plan.md`, pick the axis whose mitigations most matter (typically `tools:High`-and-above or `sector:regulated-decision-support`), and sketch how each mitigation's effectiveness is measured — the peer track, the measurement cadence, the metric, the failure trigger.
- **Draft the escalation-contract narrative.** In `escalation-contract-narrative.md`, write the two-paragraph description of the escalation contract with head of AI governance: which tier-boundary crossings escalate, on what timing, with what evidence set, into what decision. This foreshadows chapter `04`'s reversal-side pathways.
- **Cross-reference the assurance case.** In `assurance-case-integration.md`, sketch how the tier scheme lands in the assurance case (`mod-102`) — the tier claim as a top-level context node; each axis as a sub-claim; each banding's mitigation obligations as sub-sub-claims discharged by peer-produced evidence.
- **Author the Frontier Model Forum reading list.** In `fmf-reading-list.md`, pull two to three Frontier Model Forum publications you would open when the scheme is reviewed, and note which axis or banding each publication is likely to inform. This is the public library the enterprise reads to keep the shape current.
