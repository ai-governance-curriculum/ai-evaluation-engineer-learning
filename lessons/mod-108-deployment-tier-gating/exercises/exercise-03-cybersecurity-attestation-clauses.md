# exercise-03: Cybersecurity Attestation Clauses for the Tier Gate

**Estimated effort:** 2 hours

## Objective

Author the **cybersecurity-attestation section** of the tier-decision artefact for one product's tier landing, composing the four reference frameworks from chapter `03`: Google SAIF as enterprise-security frame, NCSC / CISA Guidelines for Secure AI System Development as lifecycle attestation, OWASP Top 10 for LLM Applications as coverage certification, and MITRE ATLAS as attack taxonomy. Every framework is discharged by a named clause with a named signer; every clause is a peer-produced evidence pointer, not a paragraph the methodology owner wrote.

The exercise is authoring the *methodology-owner side* of the boundary from chapter `03`: cite the frameworks, name the peer signers, compose the section, and do not backfill threat-model authorship or mitigation-effectiveness certification. Those are `ai-infra-security` peer work.

## Prerequisites

- Chapter [`03-cybersecurity-attestation-clauses-for-the-tier-gate.md`](../03-cybersecurity-attestation-clauses-for-the-tier-gate.md) — the four frameworks, how they compose, the peer-role boundaries.
- Exercise [`exercise-01-enterprise-tier-scheme-in-rsp-shape.md`](exercise-01-enterprise-tier-scheme-in-rsp-shape.md) — the tier scheme and the product's tier landing you will discharge.
- Exercise [`exercise-02-capability-evidence-thresholds.md`](exercise-02-capability-evidence-thresholds.md) — the safety-side evidence (AgentDojo, InjecAgent) that this exercise's OWASP LLM01 coverage cites.
- Skim access to the four framework primary sources:
  - [NCSC / CISA Guidelines for Secure AI System Development](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development) — read the four lifecycle sections.
  - [Google Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) — read the six core elements.
  - [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — read the current published list.
  - [MITRE ATLAS](https://atlas.mitre.org/) — read the tactics-and-techniques matrix.
- Familiarity with the peer-role registry — the `ai-infra-security` peer owns the substantive attestation authoring; the methodology owner cites and composes.

## Problem statement

Continue from exercise `01`'s product portfolio. Pick the product whose deployment surface exposes the *most* cybersecurity attack surface (typically the external-facing product with `tools:High`-or-above and `reach:High`-or-above). Author the cybersecurity-attestation section for that product's tier-decision artefact.

Two failure modes to design against, from chapter `03`:

- **Backfilling threat-model authorship.** The methodology owner is not a security engineer. If your exercise output *is* a threat model, you have crossed the boundary. The exercise output *cites* the threat model as a peer artefact.
- **Uncredited mitigations.** A guardrail with an unmeasured block rate does not discharge a mitigation obligation. If your OWASP LLM01 row cites "prompt-injection guardrail in place" without evidence pointer to a measured block rate, you have declared a mitigation without discharging its evidence requirement.

## Requirements

Produce six artefacts in a single directory.

### 1. `product-scoping-brief.md`

A short brief that names:

- **Product and tier landing.** Named product from exercise `01`; the tier landing; pointer back to the tier scheme.
- **Deployment surface.** The concrete surface — API-gateway boundary, hosted inference layer, tool-execution runtime, retrieval-corpus store, front-end integration.
- **Threat-actor context.** For this product, the plausible threat actors — external attackers, malicious insiders, curious authenticated users, indirect-injection sources (untrusted tool responses), model-side supply-chain (foundation-model provider compromise).
- **Peer-track partners.** For each of the four frameworks, the peer-track lead that owns the substantive attestation content. Typical: `ai-infra-security` for all four; `ai-infra-mlops` for the secure-development NCSC sub-section; `head-of-ai-infrastructure` for the SAIF frame; `head-of-ai-governance` for the escalation contract.
- **Prior threat-model reference.** Pointer to the `ai-infra-security` peer's existing threat model for the product (or a placeholder if the exercise scenario is fresh). The methodology owner *cites* the threat model but does not author it.

### 2. `saif-frame-section.md`

The SAIF frame section — one to two paragraphs, not more. SAIF is the *outer envelope*, not the gate criterion set. The section states:

- **Enterprise SAIF posture.** How the enterprise's overall AI-security programme is designed to SAIF. This is typically written *once* at the programme level and referenced from every tier-decision artefact.
- **Product-specific SAIF anchors.** For each of SAIF's six core elements, name the product-specific anchor — what the product's deployment does that instantiates the element. Do not restate the element; state the instantiation.
- **Owner signature.** `head-of-ai-infrastructure` (or the enterprise's equivalent) signs the SAIF frame section as authoritative for this product.

The section does *not* enumerate SAIF as a compliance checklist; SAIF is not that kind of framework. If your section reads as a compliance checklist, rewrite it as an enterprise-posture paragraph.

### 3. `ncsc-lifecycle-attestation.md`

The NCSC / CISA lifecycle attestation. Structured as four sub-sections, one per lifecycle stage. For each sub-section, produce a short table with:

| Guideline reference | Local implementation | Owner | Evidence pointer |

The guideline reference is the NCSC document's own paragraph or sub-item; the local implementation is what the enterprise actually does; the owner is the peer role that authored the substantive artefact; the evidence pointer is the concrete artefact (with `<placeholder>` or `<!-- needs-research: … -->` where a specific artefact would need to be named in the real programme).

Sub-sections:

- **Secure design.** Threat modelling, model-and-environment security design, security trade-offs in model selection. Owner: `ai-infra-security`.
- **Secure development.** Supply-chain security, asset identification and protection, data / model / prompt documentation, technical-debt management. Owner: `ai-infra-mlops` + `ai-infra-security`.
- **Secure deployment.** Infrastructure hardening, model protection in operation, incident-management procedure integration, responsible release. Owner: `ai-infra-security` + `head-of-ai-governance` (release-authority sign-off).
- **Secure operation and maintenance.** Behaviour and input monitoring, secure-by-design updates, lessons-learned loop. Owner: `ai-infra-security` + `ai-infra-mlops`.

Each sub-section closes with the peer-role signature line.

### 4. `owasp-llm-top-10-coverage-table.md`

The OWASP LLM Top 10 coverage table. One row per current OWASP LLM Top 10 risk item (use the current published version — see the OWASP landing page). For each row:

| Risk ID | Risk title | Local threat model instance | Mitigation(s) | Evidence pointer | Peer-track owner | Residual risk |

Where the mitigation has a *measurable* effectiveness metric (a guardrail block rate, a prompt-injection detection accuracy), the evidence pointer must reference the measurement — typically the evidence artefacts from exercise `02` (AgentDojo, InjecAgent for LLM01; HarmBench for the harm-category coverage; PII-leak eval for LLM06).

Explicitly discharge, at minimum, the following risks with an evidence pointer (not just a mitigation name):

- **Prompt injection** — cite AgentDojo / InjecAgent evidence from exercise `02` plus red-team results specific to the deployment surface.
- **Insecure output handling** — code-review attestation from `ai-infra-security` covering the downstream handling of model outputs (HTML escaping, structured-data validation, no-eval).
- **Training-data poisoning** — provider attestations for the base model; supply-chain evidence for any fine-tuning data.
- **Supply-chain vulnerabilities** — SBOM (software bill of materials) and MBOM (model bill of materials) evidence.
- **Sensitive information disclosure** — PII-leak evaluations and RAG-context-leakage tests.
- **Excessive agency** — evidence tied to the tool-invocation-autonomy axis from exercise `01`, plus the human-oversight design.
- **Overreliance** — human-oversight design evidence (EU AI Act Article 14).

For any risk where the current release cannot fully discharge the row, use a `<residual-risk>` marker and describe the compensating control or the deferred-criterion timeline.

Where the current OWASP identifiers have shifted from the v1.x list (e.g., a 2025 revision renumbered or restructured), cite the current identifiers and mark `<!-- needs-research: verify current OWASP LLM Top 10 identifiers -->` where the identifier mapping would need re-verification.

### 5. `mitre-atlas-adversarial-eval-index.md`

The MITRE ATLAS index for the adversarial-eval report. The methodology owner does *not* author the adversarial-eval report; the `ai-risk-engineer` or `ai-infra-security` peer does. This artefact is the *index* — the mapping from the report's scenarios to ATLAS techniques — that the methodology owner reads and cites.

Structure:

- **Report reference.** Pointer to the underlying adversarial-eval report (with `<placeholder>` or `<!-- needs-research: … -->` where the report would be a real peer artefact).
- **ATLAS-technique index table.** One row per ATLAS technique the report addresses. Columns:

| ATLAS tactic column | ATLAS technique ID | Report scenario | Coverage disposition |

The `coverage disposition` is one of: `covered` (the report demonstrates a mitigation exists and is measured), `partial` (the report covers the technique but the mitigation is not fully evaluated), `residual` (the report acknowledges the technique but no mitigation is currently in place — a residual risk with named compensating controls), or `not applicable` (the technique's threat model does not apply to this deployment surface — with a one-line justification).

- **Coverage-and-gap summary.** For each ATLAS tactic column, a one-line summary of the coverage disposition across the tactic's techniques. Where a tactic column has significant residuals, name the escalation to the head of AI governance.
- **Owner signature.** `ai-risk-engineer` or `ai-infra-security` peer signs the underlying report; the methodology owner signs the index as *consumed*.

For the exercise, cover at least four ATLAS tactic columns (typically Reconnaissance, ML Model Access, Defence Evasion, and Exfiltration — but pick the columns that most match your product's deployment surface).

### 6. `boundary-and-backfill-log.md`

The self-check log. In half a page:

- **Where the exercise would have crossed the boundary.** List two places where the temptation to backfill peer work (author the threat model; certify a mitigation as effective without measurement; write the ATLAS scenario descriptions) was resisted, and how.
- **Where a `<!-- needs-research: … -->` marker was used and why.** List the markers by artefact and note what the real programme would need to verify (current OWASP version, current NCSC signatory count, specific vendor attestation content).
- **Escalation triggers into `head-of-ai-governance`.** Note the specific attestation-section conditions that would escalate — an unresolved OWASP row with material residual risk; an ATLAS tactic column with a coverage gap and no compensating control; a threat-model change since the last tier-decision artefact that the current attestation does not reflect.
- **Foreshadowing chapter `04` and exercise `04`.** Note the cybersecurity-integrity conditions that would trigger a kill-switch (compromise of weights, prompts, judge configuration, or serving infrastructure), rather than a rollback or downgrade.

## Starter guidance

- **Cite the frameworks; do not restate them.** Your SAIF section is not the SAIF landing page paraphrased. Your NCSC section is not the NCSC document rewritten. The frameworks are the *reference*; your attestation is the *evidence pointer set*.
- **The methodology owner does not author the threat model.** If a section reads as if it is the threat model, the exercise has drifted. The threat model is a peer artefact the section *cites*. Same for the mitigation-effectiveness evaluation.
- **Every mitigation cited must have measured effectiveness.** If OWASP LLM01 says "prompt-injection guardrail," the evidence pointer must reference a measurement — AgentDojo attack-success rate, InjecAgent scenario coverage, red-team probe result. A guardrail with an unmeasured block rate does not discharge a mitigation obligation.
- **Owner signatures are separate.** SAIF frame is signed by `head-of-ai-infrastructure`. NCSC sub-sections are signed by `ai-infra-security` (and `ai-infra-mlops` for secure development). OWASP coverage table is signed by `ai-infra-security`. ATLAS index is signed by `ai-risk-engineer` or `ai-infra-security` for the report, and by the methodology owner for the index consumption.
- **Placeholder evidence pointers are legitimate.** Do not fabricate specific artefact IDs, cryptographic digests, or vendor attestation contents. Use `<placeholder>` or `<!-- needs-research: … -->` markers and note what the real programme would populate.
- **Residual risks are declared, not hidden.** An OWASP row that cannot be fully discharged today is a `<residual-risk>` row with a compensating-control and expiry note — not a row that quietly claims discharge. An ATLAS technique with no mitigation is `residual`, not `covered`.
- **The current OWASP LLM Top 10 identifiers may have shifted from the v1.x list.** Use the current published version's identifiers and cite the version. Where you are unsure, mark `<!-- needs-research: … -->`.
- **The current NCSC partner count may have grown since 2023-11.** Use the current signatory list from the NCSC page. Where you are unsure, mark `<!-- needs-research: … -->`.

## Acceptance criteria

You have succeeded if:

- `product-scoping-brief.md` names the product, deployment surface, threat-actor context, peer-track partners, and prior threat-model reference.
- `saif-frame-section.md` reads as an enterprise-posture paragraph (not a compliance checklist), names the six core elements' product-specific anchors, and carries the `head-of-ai-infrastructure` signature line.
- `ncsc-lifecycle-attestation.md` covers all four lifecycle stages, each with a per-guideline table. Owner and evidence pointer are named per row. Peer-role signature closes each sub-section.
- `owasp-llm-top-10-coverage-table.md` covers every current OWASP LLM Top 10 risk item. Prompt injection, insecure output handling, training-data poisoning, supply-chain, sensitive-information disclosure, excessive agency, and overreliance carry concrete evidence pointers (not just mitigation names). Where a row has residual risk, the residual is declared.
- `mitre-atlas-adversarial-eval-index.md` covers at least four ATLAS tactic columns; each technique row carries a coverage disposition; each disposition of `residual` carries a compensating control or an escalation trigger. Peer-role and methodology-owner signatures are separate.
- `boundary-and-backfill-log.md` names two backfill temptations resisted, the `<!-- needs-research: … -->` markers used, the escalation triggers into head of AI governance, and the cybersecurity-integrity conditions that foreshadow the kill-switch trigger from chapter `04`.
- No section reads as *the frameworks themselves*. Every section reads as *the enterprise's evidence pointer set citing the frameworks*.
- No mitigation is cited without a measurement or an explicit residual-risk declaration.
- Every place a fact would need to be verified against the current framework version or the peer track's own current artefact is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Draft the cyber-tabletop scenario the attestation section anticipates.** In `cyber-tabletop-scenario.md`, sketch a tabletop scenario — an indirect prompt injection reaches the agent via a returned document, triggers a write-tool invocation, and exfiltrates a customer record. Walk the four dispositions (kill-switch, rollback, downgrade, do-not-deploy — foreshadowing chapter `04`) and name which is the correct disposition per stage of the scenario.
- **Author the MBOM (Model Bill of Materials) row for the supply-chain OWASP risk.** In `mbom-row.md`, sketch what the MBOM entry for this product would contain — base model + version, fine-tune + version, embedding model + version, judge model + version, guardrail classifier + version, retrieval corpus + refresh date. Cross-reference the `mod-104` MBOM discipline (foreshadow if needed).
- **Cross-reference the DORA / SR-11-7 sector overlays.** For a product that deploys into a DORA-scoped or SR-11-7-scoped context, in `sector-cyber-overlay.md`, walk which sector-rule articles impose *additional* cybersecurity clauses on top of the four-framework attestation (DORA Articles 5–16 and 30(3); SR 11-7's information-security expectations).
- **Author the incident-response bridge to the enterprise SOC.** In `soc-bridge.md`, sketch how the AI-specific incident-response procedure integrates with the enterprise SOC's runbook — the detection paths, the escalation paths, the tabletop cadence, the role that owns the bridge.
- **Draft the Coalition for Secure AI (CoSAI) publication reading list.** SAIF's programme has an associated Coalition for Secure AI (CoSAI). In `cosai-reading-list.md`, list two to three CoSAI publications you would open when the attestation section is next reviewed, and note which framework's discharge each publication is likely to inform. This is the shared-vocabulary library the enterprise reads alongside SAIF itself.
