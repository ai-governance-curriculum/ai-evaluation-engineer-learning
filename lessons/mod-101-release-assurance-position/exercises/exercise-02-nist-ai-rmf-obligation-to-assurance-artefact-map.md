# exercise-02: NIST AI RMF Obligation → Assurance-Artefact Map

**Estimated effort:** 2 hours

## Objective

Take a sample release-gate obligation set (provided below) and produce a two-way map:

- **Forward** — from each release-gate obligation to the NIST AI RMF sub-category (or sub-categories) it plugs into, plus the Playbook suggested actions that shape the discharge, plus the peer role that produces the underlying evidence.
- **Backward** — from a sampled NIST AI RMF sub-category to the release-gate obligation(s) that reference it, so an auditor walking the framework can find your evidence.

This exercise operationalises chapter `02`.

## Prerequisites

- Chapter `02-nist-ai-rmf-and-playbook.md`.
- Chapter `06-deferral-contract.md` (for the peer-owner column).
- NIST AI RMF 1.0 (AI 100-1) and the NIST AI RMF Playbook (`airc.nist.gov/AI_RMF_Knowledge_Base/Playbook`) — open in browser as reference.
- NIST AI 600-1 (Generative AI Profile) if your chosen system is GenAI.
- NIST AI 100-2 (adversarial-ML taxonomy) if security / adversarial-ML is in scope.

## Problem statement — the sample release-gate

Assume a release-gate for a **customer-support agent** built on a hosted foundation model, RAG over a proprietary knowledge base, with tool-calling to internal APIs (order lookup, refund initiation up to a capped amount). Deployer of the foundation model; provider of the fine-tuned system-integrated derivative. In-scope jurisdictions: EU and California. Not GPAI itself; downstream of a GPAI.

The release-gate carries the following (ten) obligations. Your job is to map each into NIST AI RMF and the Playbook. This obligation set is deliberately mixed — some organisational, some system-specific.

1. There is a documented risk-management system for this system, covering identification, analysis, evaluation, and treatment of risks across its lifecycle.
2. The training-data governance for the RAG index has been reviewed for gaps, bias, and licensing, and the review record is on file.
3. Instructions for use are drafted for the human customer-support agents who oversee the system, meeting Article 13 content requirements.
4. Human-oversight measures (interrupt, override, refuse-to-execute) are designed, tested, and demonstrably usable by a trained overseer.
5. Accuracy on the deployment surface is measured against a threshold `T_acc` with stated statistical uncertainty; robustness against prompt injection is measured against threshold `T_robust`.
6. Cybersecurity: the supply chain of the foundation model, the RAG components, and any judge model is attested.
7. Third-party dependencies are inventoried and the foundation-model provider's SOC 2 / ISO 27001 / DPA is on file.
8. Serious-incident procedure is documented, tested end-to-end, and includes the EU AI Act Article 61 timelines.
9. Post-deployment monitoring (online eval, drift detection, feedback capture) is designed and live before ship.
10. Continuous improvement: a corrective-action loop is in place tying incident findings back to threshold revision and mitigation update.

## Requirements

Produce `rmf-obligation-map.md` (or `.csv` + narrative) containing:

1. **Forward map** — a table with these columns:

   | Obligation # | Obligation text (short) | Primary NIST AI RMF sub-category | Additional sub-categories (if any) | Playbook suggested-action IDs consulted | Peer role owing evidence | Notes |
   | ------------ | ---------------------- | -------------------------------- | ---------------------------------- | -------------------------------------- | ------------------------ | ----- |

   Cover all ten obligations. Use the exact identifier for sub-categories (`MEASURE-2.7`, `GOVERN-6.1`, `MANAGE-4.1`, etc.). If your organisation is a GenAI provider, cite the AI 600-1 risk category as well (e.g. `AI 600-1: Information Security`).
2. **Backward map** — pick three sub-categories that would matter to an auditor (at minimum: one GOVERN, one MEASURE, one MANAGE) and, for each, list which of the ten obligations reference it and what artefact the auditor would be shown.
3. **Coverage narrative** — a one-page narrative that:
   - Identifies any sub-categories the ten obligations do *not* touch and comments on whether that's a scope-appropriate absence or a coverage gap.
   - Identifies any obligation that plugs into an unusually high number of sub-categories and comments on whether the obligation should be split.
   - Names any obligation whose Playbook suggested actions materially expand the release-gate evidence requirement (i.e. the obligation says one thing but the Playbook implies more).
4. **AI 100-2 cross-link** — for the cybersecurity / adversarial-ML obligations (5b and 6), point at the NIST AI 100-2 attack categories that the release-gate evidence should specifically address.

## Starter guidance

- **Do not over-plug.** An obligation typically primary-plugs into one sub-category and secondary-plugs into one or two. If you find yourself citing five sub-categories for one obligation, ask whether the obligation is really two obligations.
- **Playbook suggested-action IDs.** The Playbook lists actions per sub-category with numeric IDs. Cite them (e.g. "MEASURE-2.7 → Playbook actions 1, 4, 7").
- **Peer role.** Refer back to chapter `06`'s deferral contract. If you assign risk-engineer craft (like harm modelling) to your own program you are losing altitude — that is the deferral-contract failure mode.
- **The obligations mix organisational and system-specific.** Obligation 1 is organisational (GOVERN / MAP); obligation 5 is system-specific (MEASURE). This mix is intentional and appears in real release-gates.
- **When multiple sub-categories apply**, name the primary one (the one an auditor would first look under) and list the others in the secondary column.

## Acceptance criteria

You have succeeded if:

- All ten obligations have a **primary** sub-category assigned with the exact identifier.
- Each obligation cites at least one **Playbook suggested-action ID** or explains why the Playbook is silent on that sub-category (rare but possible).
- Each obligation names the **peer role** that owns the underlying evidence, drawn from the ladder in chapter `01`.
- The backward map is walkable — an auditor reading a sub-category can find the obligation and the artefact.
- The coverage narrative flags at least one gap or splittable-obligation observation.
- NIST AI 100-2 categories are cited for the adversarial-ML obligation.

## Stretch goals

- Add a fourth column to the forward map: the ISO/IEC 42001 clause that is the management-system sibling of the NIST AI RMF sub-category, so the map begins to look like the `mod-106` cross-jurisdictional crosswalk.
- Rewrite the ten obligations so each is stated in NIST AI RMF *outcome* language ("the risk-management system is documented and maintained") rather than in artefact language ("we have an RMS document"). The outcome shape is the shape the Playbook uses.
- Assume this system is now a *GPAI derivative with systemic risk*. Which obligations change, which are added, and which sub-categories become active that were not before?
