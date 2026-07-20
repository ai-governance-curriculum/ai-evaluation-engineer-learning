# Cybersecurity Attestation Clauses for the Tier Gate

## Motivation

Chapter `02` gave the capability-evidence side of the tier gate — the measured floor and transition thresholds tied to peer benchmarks. This chapter gives the mitigation-obligation side: the *cybersecurity attestation clauses* that stack onto the tier gate and become non-negotiable at higher tiers.

The methodology owner cares about cybersecurity for two reasons. First, an AI system whose weights, training data, prompts, or judge configuration can be tampered with is not an AI system whose evaluation evidence is trustworthy — every claim in the assurance case (`mod-102`) rests on the integrity of the artefacts the claim cites. Second, from the deployment side, an AI system is now a *cyber-attack surface* in its own right: prompt-injection is not a hypothesis, adversarial input to a tool-calling agent is a live threat, and cross-tenant data exfiltration through a coding-assistant is a well-documented incident class.

The release-assurance methodology owner is not a security engineer. The `ai-infra-security` peer (level 35 in the curriculum) owns cybersecurity engineering; the methodology owner *cites* the peer's attestation clauses in the release-gate. The four reference frameworks in this chapter are the vocabulary the two roles share.

## The four reference frameworks

Four bodies of guidance sit at the centre of AI cybersecurity practice:

- **NCSC (UK) and international-partner Guidelines for Secure AI System Development** — a secure-by-design guideline document jointly issued in 2023-11 by the UK's National Cyber Security Centre together with CISA (US) and 21 international partners. <!-- needs-research: verify the exact current partner count — initial publication cited "23 international partners" (24 signatory agencies including CISA and NCSC), and additional partners have been added since; confirm current signatory list. -->
- **Google's Secure AI Framework (SAIF)** — a conceptual framework Google published in 2023-06 that adapts secure-development practice to AI systems, structured around six core elements.
- **OWASP Top 10 for LLM Applications** — an enumeration of the top ten security risks specific to LLM-integrated applications, first published in 2023-08 (v1.0) with subsequent revisions. <!-- needs-research: verify the current published version of the OWASP Top 10 for LLM Applications (v1.1 was released 2023-10; a 2025 revision may have shifted the risk categories) and the current numeric identifiers of each risk. -->
- **MITRE ATLAS (Adversarial Threat Landscape for AI Systems)** — the reference taxonomy of adversarial-ML tactics, techniques, and mitigations, modelled on the MITRE ATT&CK structure.

The tier gate cites each in a specific place. NCSC is cited as an *attestation section* in the release package. OWASP LLM Top 10 is cited as an *enumeration the release-gate certifies coverage against*. MITRE ATLAS is cited as *the taxonomy an adversarial-eval report cross-references*. SAIF sits above all three as a conceptual anchor for the enterprise's AI-security posture. The rest of this chapter walks each in turn.

## NCSC Guidelines for Secure AI System Development

**What it is.** The Guidelines for Secure AI System Development ([NCSC](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development)) is a lifecycle-oriented set of secure-development principles for AI systems, jointly issued by NCSC and CISA in November 2023 and co-sealed by 21 further international-partner agencies. The document organises its guidance under four stages of the AI system lifecycle:

- **Secure design** — understanding risks and threat modelling; designing the system, model, and environment for security; considering security benefits and trade-offs when selecting the AI model.
- **Secure development** — supply-chain security; identifying, tracking, and protecting assets; documenting data, models, and prompts; managing technical debt.
- **Secure deployment** — securing infrastructure; continuously protecting the model; developing incident-management procedures; releasing AI responsibly.
- **Secure operation and maintenance** — monitoring system behaviour; monitoring inputs; following secure-by-design principles for updates; collecting and sharing lessons learned.

Under each stage the document lists specific practices — not audit criteria in the ISO sense, but *guidelines* the deployer is expected to have addressed and to be able to defend.

**How the release-gate cites it.** The release-package (`mod-104`) carries an **NCSC attestation section**: a per-stage table with each guideline referenced, the local implementation named, the owner named, and the evidence pointer given. The tier gate reads the attestation section as an obligation set: at low tiers, the attestation may cite compensating controls; at higher tiers, missing evidence for a guideline stage is a gating defect.

**Adaptation-to-enterprise implication.** The four stages align neatly with the release-gate's lifecycle framing (mod-103) — design-time, development-time, deployment-time, operation-time. The methodology owner can slot each guideline into the assurance case (`mod-102`) as a sub-claim, discharged by the `ai-infra-security` peer's attestation.

## Google Secure AI Framework (SAIF)

**What it is.** SAIF ([safety.google/cybersecurity-advancements/saif](https://safety.google/cybersecurity-advancements/saif/)) is a conceptual framework Google published in 2023-06, structured around six core elements:

1. Expand strong security foundations to the AI ecosystem.
2. Extend detection and response to bring AI into an organisation's threat universe.
3. Automate defences to keep pace with existing and new threats.
4. Harmonise platform-level controls to ensure consistent security across the organisation.
5. Adapt controls to adjust mitigations and create faster feedback loops for AI deployment.
6. Contextualise AI-system risks in surrounding business processes.

<!-- needs-research: verify the exact wording of the six core elements as currently published on safety.google/cybersecurity-advancements/saif; SAIF has been extended over time with additional maps, risk taxonomies, and a Coalition for Secure AI (CoSAI) programme — confirm current material. -->

SAIF is *conceptual* — it does not enumerate specific risks like the OWASP list, nor does it provide lifecycle guidelines like the NCSC document. Its role is to name six *dispositions* the enterprise's AI-security posture must exhibit, and to serve as an outer envelope for more concrete practices.

**How the release-gate cites it.** The release-gate does not cite SAIF criterion-by-criterion; it cites SAIF as the *frame* within which the more concrete attestations (NCSC, OWASP, ATLAS) sit. In the assurance case, SAIF appears as a top-level context node ("the enterprise's AI-security programme is designed to SAIF, with the specific attestations below discharging the required elements").

**Adaptation-to-enterprise implication.** SAIF is often the frame the enterprise-security team already uses (independent of the release-assurance programme), because it is compatible with the enterprise's broader security dispositions. The methodology owner should read SAIF as *shared vocabulary* with the enterprise-security team — cite it in briefings and in cross-team requirements, but rely on the concrete attestations (NCSC, OWASP, ATLAS) for gate-level evidence.

## OWASP Top 10 for LLM Applications

**What it is.** The OWASP Top 10 for LLM Applications ([owasp.org/www-project-top-10-for-large-language-model-applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)) is an enumeration of the ten most critical security risks specific to LLM-integrated applications. It follows the same shape as the classic OWASP Top 10 for web applications — a short list, updated on a cadence, with each risk item carrying a description, common examples, prevention guidance, and reference material.

The v1.x list included: prompt injection, insecure output handling, training-data poisoning, model denial-of-service, supply-chain vulnerabilities, sensitive information disclosure, insecure plugin design, excessive agency, overreliance, and model theft. <!-- needs-research: verify the current published version (2025 revisions restructured several categories, e.g., renaming some items and adding categories such as "vector and embedding weaknesses" or "system-prompt leakage"). Confirm the current v1.x or 2025 canonical enumeration. -->

**How the release-gate cites it.** The release-gate carries an **OWASP LLM Top 10 coverage table**: per risk, the local threat model instance, the mitigation in place, the peer track producing the evidence, and the residual risk. The tier gate reads the table as an *enumeration to certify coverage against*. A tier at `tools:High` or above with an uncovered OWASP risk is a gating defect.

The specific coverage-tests differ per risk. For example:

- **Prompt injection (v1.x LLM01).** Evidence from AgentDojo, InjecAgent (`02`), plus red-team results specific to the deployment surface.
- **Insecure output handling (LLM02).** Evidence that model outputs are safely handled downstream (escaped in HTML contexts, validated as structured data, not passed to eval, and so on) — typically a code-review attestation from `ai-infra-security`.
- **Training-data poisoning (LLM03).** Provider attestations for the base model; supply-chain evidence for any fine-tuning data.
- **Supply-chain vulnerabilities (LLM05).** SBOM (software bill of materials) and, increasingly, MBOM (model bill of materials) evidence.
- **Sensitive information disclosure (LLM06).** Evidence from PII-leak evaluations and RAG-context-leakage tests.
- **Excessive agency (LLM08).** Evidence tied to the tool-invocation-autonomy axis from `01`.
- **Overreliance (LLM09).** Human-oversight design evidence (EU AI Act Article 14; `mod-101` chapter `04`).

**Adaptation-to-enterprise implication.** The OWASP list is not exhaustive, and its shape (a Top 10) is a heuristic rather than a taxonomy. Use it as a *starting enumeration* — every tier gate certifies coverage against the list — but *do not* treat coverage of the list as sufficient. The MITRE ATLAS taxonomy below provides the more exhaustive catalogue.

## MITRE ATLAS

**What it is.** MITRE ATLAS (Adversarial Threat Landscape for AI Systems) ([atlas.mitre.org](https://atlas.mitre.org/)) is the reference taxonomy of adversarial-ML tactics, techniques, and mitigations. It is modelled on the MITRE ATT&CK structure — tactics along the top (Reconnaissance, Resource Development, Initial Access, ML Model Access, Execution, Persistence, Privilege Escalation, Defence Evasion, Credential Access, Discovery, Collection, ML Attack Staging, Exfiltration, Impact) — and techniques and sub-techniques underneath, each with a stable identifier, a description, a set of documented case studies, and a set of mitigations.

<!-- needs-research: verify the exact current set of ATLAS tactics; ATLAS has been extended over time and specific tactic-column labels or additions may differ. -->

Because ATLAS shares the ATT&CK shape, security teams that already run ATT&CK-based threat modelling can adapt their practice to AI systems without inventing a new vocabulary. This is the practical reason the enterprise programme cites ATLAS: it *maps* into the security team's existing work.

**How the release-gate cites it.** The release-gate's **adversarial-eval report** — produced by the `ai-risk-engineer` or `ai-infra-security` peer — cross-references each attack scenario tested to its ATLAS technique identifier. The tier gate reads the report as *taxonomically indexed evidence*, not as narrative. The methodology owner can then ask, and defend, "which ATLAS techniques does this deployment's evidence cover, and which does it not?" That question is answerable if the report is indexed to ATLAS; it is not answerable if the report is prose.

**Adaptation-to-enterprise implication.** ATLAS provides the *shared taxonomy* the methodology owner uses to communicate with the enterprise-security team, the incident-response team, and (increasingly) external auditors. When the assurance case (`mod-102`) claims "the deployment discharges Article 15(4) cybersecurity", the leaf evidence is an ATLAS-indexed adversarial-eval report, not a prose paragraph.

## How the four compose

The four frameworks are not competing — they cover different levels of abstraction:

| Layer | Framework | Role in the tier gate |
| --- | --- | --- |
| Enterprise posture | Google SAIF | Framing context; shared vocabulary with the enterprise-security team. |
| Lifecycle guidance | NCSC Guidelines | Per-stage attestation section in the release package. |
| Risk enumeration | OWASP LLM Top 10 | Coverage table the tier gate certifies against. |
| Attack taxonomy | MITRE ATLAS | Index the adversarial-eval report is cross-referenced to. |

Every tier gate above the lowest tier cites *all four* — SAIF as frame, NCSC as attestation, OWASP as coverage, ATLAS as taxonomy. At the lowest tier (internal-only, minimal tool use), a subset may be defensible; the methodology owner has to *argue* the subset, not assume it.

## Worked example — cybersecurity attestation for the customer-support agent

Continuing the T-CS product from chapters `01` and `02`. The cybersecurity attestation section of the tier-decision artefact (`05`) reads:

**Frame (SAIF).** The T-CS deployment sits within the enterprise's SAIF-aligned programme; detection-and-response for T-CS extends the enterprise SOC's threat universe (element 2); T-CS-specific controls are harmonised with the enterprise's platform controls (element 4). Owner: `head-of-ai-infrastructure`.

**Lifecycle attestation (NCSC).** Four sub-sections, one per lifecycle stage:

- *Secure design.* Threat model documented; foundation-model provider selection justified with security trade-off analysis; tool-set scope justified with excessive-agency avoidance analysis. Owner: `ai-infra-security`.
- *Secure development.* SBOM and MBOM produced; prompts and system prompts versioned in the same repository as code; training / fine-tuning data lineage documented. Owner: `ai-infra-mlops`.
- *Secure deployment.* Inference infrastructure hardened per enterprise baseline; kill-switch and rollback tested (`04`); incident-management procedure integrated with the enterprise IR runbook. Owner: `ai-infra-security` + `head-of-ai-governance`.
- *Secure operation and maintenance.* Runtime input / output monitoring in place; guardrail block-rate and over-block-rate tracked on the dashboard (mod-103 chapter `06`); lessons-learned loop integrated with `mod-110`. Owner: `ai-infra-security`.

**Coverage certification (OWASP LLM Top 10).** A table with per-risk mitigation and evidence pointers. For T-CS specifically, LLM01 (prompt injection) cites AgentDojo and InjecAgent evidence from chapter `02`; LLM06 (sensitive information disclosure) cites PII-leak eval results; LLM08 (excessive agency) cites tool-set scope justification and monitoring detectors. <!-- needs-research: confirm current LLM01/LLM06/LLM08 identifiers under the currently-published version of the OWASP LLM Top 10; earlier v1.x used LLM01 for prompt injection, but the 2025 revision may re-number. -->

**Adversarial-eval report (ATLAS-indexed).** The `ai-risk-engineer` peer's red-team report on T-CS is indexed to ATLAS techniques: the prompt-injection scenarios map to relevant ATLAS techniques for prompt manipulation and adversarial input; the exfiltration scenarios map to the ATLAS Exfiltration tactic; the guardrail-evasion scenarios map to Defence Evasion techniques. Coverage is defended per tactic column; uncovered techniques are declared as residual with a rationale.

Each of the four sub-sections is signed by the named owner; the release-gate cannot pass without all four attached.

## What the methodology owner does *not* do

Two boundaries are worth naming.

**The methodology owner does not author the threat model.** Threat modelling for the AI system is the `ai-infra-security` peer's work. The methodology owner *requires* a threat model of a specified shape, *cites* it in the assurance case, and *reviews* it for coverage of the deployment tier — but does not draft it.

**The methodology owner does not certify the mitigation as effective.** A guardrail with an unmeasured block rate does not discharge a mitigation obligation (chapter `01`'s FSF-derived point about mitigation-effectiveness evaluation). The peer specialist produces the measurement; the methodology owner reads it.

Both boundaries are backfill traps: the methodology owner is *tempted* to write the threat model or to certify effectiveness when the peer track is slow. Resisting the temptation is what keeps the tier gate's evidence independent.

## Where this shows up in the rest of the track

- `01` — the tier axes this chapter's attestations discharge (`data`, `tools`, `reach`, `sector`).
- `02` — the capability-evidence side; safety-side benchmarks (AgentDojo, InjecAgent) also serve as OWASP LLM01 evidence.
- `04` — the kill-switch and rollback design that NCSC secure-deployment guidance mandates.
- `05` — the composition of the tier-decision artefact, where the cybersecurity attestation is one of the mandatory sections.
- `mod-101` chapter `04` — EU AI Act Article 15(4) cybersecurity is the statutory obligation this chapter's attestations discharge.
- `mod-104` — SBOM / MBOM evidence and provenance for artefact integrity.
- `mod-107` — sector-regulated regimes (DORA, SR 11-7) add sector-specific security clauses on top.
- `mod-109` — third-party evaluators may audit the cybersecurity attestation independently.
- `mod-110` — the operations-side monitoring detectors that keep the attestation live.

## Summary

- Four frameworks compose in the tier gate: Google SAIF (frame), NCSC Guidelines for Secure AI System Development (lifecycle attestation), OWASP LLM Top 10 (coverage certification), MITRE ATLAS (attack taxonomy).
- NCSC (co-issued 2023-11 by NCSC + CISA + international partners) organises secure-by-design guidance under four lifecycle stages — design, development, deployment, operation and maintenance.
- SAIF (2023-06) sits above the concrete attestations as shared enterprise-security vocabulary, not gate criteria in itself.
- OWASP LLM Top 10 is an enumeration the release-gate certifies coverage against; use it as a starting list, not as a sufficient set.
- MITRE ATLAS is the reference adversarial-ML taxonomy; the release-gate's adversarial-eval report is indexed to it.
- The methodology owner cites the frameworks and consumes the peer evidence; does not author threat models, does not certify mitigation effectiveness. The `ai-infra-security` peer owns both.
- Exercise 03 has you author cybersecurity-attestation clauses for a worked deployment tier, one clause per framework, with the peer-track owner named.
