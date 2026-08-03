# mod-108-deployment-tier-gating: Deployment-Tier Gating: RSP / Preparedness / DeepMind FSF Adapted to Enterprise

Walks the release-assurance methodology owner from the coarse *deployment-surface* tier taxonomy of `mod-103` into the *capability-envelope* tier gate the frontier labs adopted for the same problem. Anthropic Responsible Scaling Policy (RSP), OpenAI Preparedness Framework, and Google DeepMind Frontier Safety Framework (FSF) are read as three variants of a single pattern — capability evidence → tier → mitigation obligation — and the enterprise programme adopts *the shape*, not the labels. The chapters then work through the capability-evidence side (thresholds tied to peer-produced benchmarks), the mitigation-obligation side (cybersecurity attestation clauses from NCSC, SAIF, OWASP LLM Top 10, MITRE ATLAS), the reversal-side dispositions (kill-switch, rollback, downgrade, do-not-deploy) with the escalation contract to the head of AI governance, and close by composing a single **tier-decision artefact** per candidate release set in its multilateral context (Bletchley, Seoul, Paris, Frontier Model Forum).

**Estimated effort:** 14 hours

## Learning objectives

- Design a deployment-tier-gating scheme in the Anthropic RSP, OpenAI Preparedness, and Google DeepMind Frontier Safety Framework shape adapted to enterprise deployment surfaces.
- Author tier-transition thresholds tied to concrete capability-evidence artefacts consumed from peer specialists — safety benchmark evidence (HarmBench / AIR-Bench 2024 / SafetyBench / AgentDojo) from `ai-risk-engineer` and `ai-eval-engineer`, and coding / agent capability evidence (SWE-bench Verified / τ-bench / GAIA) from `ai-eval-engineer` and `model-evaluation-engineer`.
- Author cybersecurity-attestation clauses aligned with UK NCSC and international-partner Secure AI System Development guidelines, Google SAIF, OWASP Top 10 for LLM Applications, MITRE ATLAS.
- Design kill-switch, rollback, downgrade, and 'do not deploy' pathways for each tier, and the escalation contract with `head-of-ai-governance` (level 60) when a tier-boundary crossing is proposed.
- Reference multilateral commitments (Bletchley / Seoul / Paris summits, Frontier Model Forum publications) as the industry-context reference for the tier gate.
- Consume the mod-108 evidence emitted by the peer level-30 tracks and produce a single tier-decision artefact per candidate release.

## Lecture chapters

1. [`01-deployment-tier-gating-shape-across-frontier-labs.md`](01-deployment-tier-gating-shape-across-frontier-labs.md) — the shape (capability evidence → tier → mitigation obligation, pre-committed and publishable) read across Anthropic RSP (AI Safety Levels), OpenAI Preparedness (tracked risk categories × Low / Med / High / Critical), and Google DeepMind FSF (Critical Capability Levels with periodic re-evaluation and mitigation-effectiveness measurement). Why the enterprise adopts the shape, not the labels; the provider's tier as a floor for the enterprise's tier; a worked bounded enterprise tier scheme across a two-product deployment.
2. [`02-capability-evidence-thresholds-tied-to-peer-benchmarks.md`](02-capability-evidence-thresholds-tied-to-peer-benchmarks.md) — the capability-evidence side of the tier gate. The deferral contract that keeps the methodology owner out of eval-authoring; safety-side evidence (HarmBench, AIR-Bench 2024, SafetyBench, AgentDojo, InjecAgent); capability-side evidence (SWE-bench Verified, τ-bench, GAIA, CyBench); the shape of a threshold spec and why reproducibility is a precondition, not a footnote.
3. [`03-cybersecurity-attestation-clauses-for-the-tier-gate.md`](03-cybersecurity-attestation-clauses-for-the-tier-gate.md) — the mitigation-obligation side. Four frameworks compose: Google SAIF as enterprise-security frame, NCSC / CISA Guidelines for Secure AI System Development as lifecycle attestation, OWASP LLM Top 10 as coverage certification, MITRE ATLAS as attack taxonomy. What the methodology owner cites versus what the `ai-infra-security` peer authors.
4. [`04-kill-switch-rollback-downgrade-and-do-not-deploy-pathways.md`](04-kill-switch-rollback-downgrade-and-do-not-deploy-pathways.md) — the reversal side. Four dispositions (kill-switch, rollback, downgrade, do-not-deploy), each with design principles, invocation conditions, and trail obligations. The escalation contract with `head-of-ai-governance` and the failure modes to design against (silent tier drift, tier shopping, deferred approvals becoming de facto approvals, untrained authorisation chains, do-not-deploy without a trail, downgrade without re-gate).
5. [`05-tier-decision-artefact-and-multilateral-context.md`](05-tier-decision-artefact-and-multilateral-context.md) — the single-output composition. The eight sections of a tier-decision artefact (system identity, deployment context, capability evidence, cybersecurity attestation, reversal design, decision with reviewers and expiry, assurance-case join, multilateral context); how the artefact composes with the assurance case and slots into the release package; the multilateral context (Bletchley Declaration 2023-11, Seoul Declaration and Frontier AI Safety Commitments 2024-05, Paris AI Action Summit 2025-02, Frontier Model Forum) that positions the artefact in a recognised shape.

## Structure

- `01-…md` … `05-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapter `01`** — read once, then read at least one of the three source frameworks end-to-end (the RSP is shortest; the FSF and Preparedness are next). Draft your own enterprise tier axes on paper before opening exercise `01`.
- **Chapter `02`** — read after `01`. Skim at least one benchmark paper per family (HarmBench for safety, SWE-bench Verified for capability, AgentDojo for tool-use robustness) so you can distinguish what the peer track produces from what the methodology owner reads. Exercise `02` authors a threshold-spec set.
- **Chapter `03`** — read alongside the NCSC / CISA Guidelines, the OWASP LLM Top 10 landing page, and MITRE ATLAS. SAIF is short and conceptual; the other three carry the concrete weight. Exercise `03` produces the four-framework attestation section.
- **Chapter `04`** — read after `03`. Skim `mod-103` chapter `05` (runbook) if you have not recently. Exercise `04` designs the four dispositions and the escalation contract.
- **Chapter `05`** — read after `04`, with the Seoul Frontier AI Safety Commitments and one Frontier Model Forum publication open in another tab. Exercise `05` composes the full tier-decision artefact end-to-end.

## Dependencies

- Requires mod-101 (release-assurance position — where the methodology owner sits in the peer ring; the four bodies of literature the tier gate maps to), mod-102 (assurance-case engineering — the tier claim is a top-level claim in the case), mod-103 (release-gate architecture — the surface-specific gate variants that compose with the capability-specific tier vector), mod-104 (evaluation evidence pipeline — pins the capability-evidence and cybersecurity-attestation artefacts by digest), and mod-105 (cards for external audiences — the tier decision seeds the deployment-tier paragraph of the external card).
- Consumed by mod-109 (third-party evaluator and auditor interface — external auditors read the tier-decision artefact as evidence), mod-110 (post-market surveillance — the periodic re-evaluation channel the FSF-style pattern requires; signals fire the reversal dispositions), mod-111 (GPAI systemic-risk assurance — the tier gate composes with EU AI Act Article 55 obligations), and mod-112 (owning an assurance program — the operating-model owns the tier-scheme template and the escalation contract with head of AI governance).
- All three capstone projects consume this module: the tier-decision artefact is one of the load-bearing outputs the capstone release-package carries.
