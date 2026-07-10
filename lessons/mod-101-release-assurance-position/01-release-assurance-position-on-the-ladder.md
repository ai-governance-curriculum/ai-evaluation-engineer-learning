# The Release-Assurance Position on the Ladder

## Motivation

A release-assurance program lives or dies by whose desk each obligation lands on.
If the assurance owner tries to author harm models, run trace-eval instrumentation, and hand-tune a judge prompt, the program loses altitude and cannot answer a regulator with a straight face. If they push everything downward, they end up narrating evidence they did not shape and cannot defend. Peer specialists are already accountable for those crafts, and higher-level architects and heads are already accountable for the control library and program leadership.

This module opens the track by pinning the role to one job: **own the release-assurance methodology** — the standing procedure that turns evaluation evidence into defensible release-gate decisions and into artefacts external audiences (regulators, auditors, deployers, boards) can rely on.

Before we can walk the standards (NIST AI RMF, ISO/IEC 42001, EU AI Act, values baseline) or draft the deferral contract, we have to fix where this role sits, what it owns, and what it explicitly does not own.

## The one-sentence charter

> The AI Evaluation Engineer owns the *release-assurance methodology*: the standing procedure by which evaluation evidence is captured, structured into an assurance case, decided on at a release gate, and packaged for regulators, auditors, deployers, and boards — including post-market surveillance.

Everything in the twelve-module plan is a specialisation of that sentence. Everything not in that sentence is a deferral.

## Level ladder — where this role sits

The role is **level 35, AI Governance family**. Its neighbours on the ladder shape what it owns and what it defers.

```
level  role                                     family                what it owns
-----  ---------------------------------------  --------------------  ------------------------------------------------
 10    ai-infra-junior-engineer                 AI Infrastructure     linux / git / http / python / packaging
 15    ai-governance-analyst                    AI Governance         intake, inventory, framework crosswalk drafts,
                                                                     first-draft cards, jurisdictional tracking
 20    ml-engineer                              ML Engineering        classical ML, sklearn eval, packaging
 25    ai-risk-engineer                         AI Governance         harm modelling, LLM / adversarial-ML red-team,
                                                                     guardrail engineering
 30    ai-eval-engineer                         AI Engineering        trace / trajectory / RAG / judge / online-eval /
                                                                     eval-gated CI/CD / eval-data-platform slice
 30    model-evaluation-engineer                ML Engineering        model-eval methodology depth (validity theory,
                                                                     bootstrap CIs, benchmark construction,
                                                                     calibration, MLPerf)
 35 →  ai-evaluation-engineer  (this track)     AI Governance         RELEASE-ASSURANCE METHODOLOGY
 35    ai-infra-security  /  security-learning  AI Infrastructure     MLSec, evaluation-set integrity, product security
 40    agentic-safety-engineer                  AI Governance         frontier-agent red-team methodology depth
 50    senior-ai-governance-architect           AI Governance         control-library architecture, cross-jurisdiction
                                                                     reconciliation, policy taxonomy
 60    head-of-ai-governance                    AI Governance         program leadership, board reporting, regulator
                                                                     interface at institution scope
 70    chief-ai-officer                         AI Governance         AI strategy at institution scope
```

Two neighbours matter most and are the ones most likely to be confused with this role: `ai-eval-engineer` (level 30, AI Engineering) and `model-evaluation-engineer` (level 30, ML Engineering). Both peer specialists have the word "evaluation" in their titles. Neither of them owns the release-assurance methodology.

## Distinguishing the role from each peer

### vs. `ai-eval-engineer` (level 30, AI Engineering — application-layer eval engineering)

That peer owns the *engineering surface* of evaluation inside a product: trace instrumentation, trajectory / tool-call scoring, LLM-as-judge in product pipelines, RAG evaluation, eval-gated CI/CD, online eval, an eval-data-platform slice, application-side safety measurement.

**This role does not re-implement that surface.** It consumes the traces, judge scores, online-eval slices, and eval-gated CI/CD signals as inputs to a release-gate decision. Where the peer engineers the evidence, this role reasons over the evidence and stakes an assurance case on it.

Concretely: the peer answers "is our judge correlated with human raters, is our RAG grounded, does our online eval catch drift?" This role answers "does that judge / RAG / online-eval evidence, threaded into an assurance case, discharge the obligations at the release gate and stand up in front of an auditor?"

### vs. `model-evaluation-engineer` (level 30, ML Engineering — model-eval methodology depth)

That peer owns the *methodological depth* of model evaluation: validity theory, bootstrap confidence intervals, benchmark construction, calibration methodology, judge-vs-human methodology, cross-modality harnesses, MLPerf.

**This role does not re-derive that methodology.** It cites it. Where a release-gate threshold requires statistical defensibility, this role reads and cross-links the peer's methodology into the assurance case, and validates that the threshold's justification is intact end-to-end.

Concretely: the peer answers "is a bootstrap CI the right estimator here, and is this benchmark well-constructed?" This role answers "does the threshold we are gating on rest on a benchmark and estimator that would survive an independent evaluator's review, and where is the trail of justification?"

### vs. `ai-risk-engineer` (level 25 — risk-engineering craft)

That role owns the *engineering craft* of AI risk: harm modelling engineering, LLM / adversarial-ML red-team engineering, guardrail engineering, AI-specific incident response.

**This role does not re-author harm models or run the red team.** It threads their outputs (harm inventory, red-team findings, guardrail-effectiveness measurements, incident learnings) into the release-gate evidence.

Concretely: the peer answers "here is the harm model, the adversarial suite, and the guardrail evaluation." This role answers "does that risk-engineering evidence, integrated with the peer eval evidence, discharge the release-gate obligations for this deployment tier?"

### vs. `ai-governance-analyst` (level 15 — operational analyst legwork)

That role owns *analyst legwork*: use-case intake, model / system inventory, first-draft framework crosswalks (NIST AI RMF, ISO 42001, EU AI Act), first-draft cards, jurisdictional regulatory tracking.

**This role does not do the analyst's intake and does not maintain the inventory.** It elevates from the analyst's outputs (the first-draft crosswalk, the first-draft card, the jurisdictional watchlist) into a program that owns the release-assurance methodology and decides.

Concretely: the analyst answers "we have this system in inventory and here is a first-draft NIST AI RMF crosswalk." This role answers "here is the release-gate assurance case; here are the cards produced for our external audiences; here is the post-market plan."

### vs. `senior-ai-governance-architect` (level 50) / `head-of-ai-governance` (level 60)

Those higher tracks own the *architecture and leadership* layer: cross-organisation control-library architecture, cross-jurisdiction reconciliation, policy taxonomy, program leadership, board reporting, institution-scale regulator interface.

**This role does not architect the control library and does not brief the board.** It produces the release-assurance methodology and its evidence in a form the architect can harmonise across the institution and the head can narrate upward. Where the architect draws the taxonomy of controls, this role delivers the artefacts that live inside those controls; where the head narrates institution-scale posture, this role provides the release-gate evidence and the post-market data behind that narration.

## What "release-assurance methodology" actually contains

At this altitude, the role's methodology is the union of:

- **A release-gate architecture** — the standing structure that says which pieces of evidence are required to pass, who signs, and how a fail is dispositioned. Owned in `mod-103`.
- **An assurance case** — the reasoned argument that connects the evidence to the release-gate obligations (typically in GSN, CAE, or SACM form). Owned in `mod-102`.
- **An evidence pipeline** — immutable logs, lineage, ML-BOM / SPDX AI, signed release-gate outputs. Owned in `mod-104`.
- **External-audience cards** — model / system / dataset cards for regulators, deployers, and third-party auditors. Owned in `mod-105`.
- **Cross-jurisdictional obligation mapping** — one release-gate map that satisfies NIST AI RMF, ISO/IEC 42001, EU AI Act, and applicable sector rules. Owned in `mod-106`.
- **Sector-specific assurance shape** — SR 11-7 / OCC 2011-12 / SR 23-4 / FDA GMLP / PCCP / DORA. Owned in `mod-107`.
- **Deployment-tier gating** — RSP / Preparedness / DeepMind FSF adapted to enterprise deployment tiers. Owned in `mod-108`.
- **Third-party evaluator / auditor interface** — the standing interface to AISI-shape independent evaluators, notified bodies, and Big Four assurance firms. Owned in `mod-109`.
- **Post-market surveillance** — the continuous-assurance loop that keeps the release-gate decision alive after ship. Owned in `mod-110`.
- **GPAI systemic-risk assurance** — the extra loop for GPAI models with systemic risk (EU AI Act Article 55 / GPAI Code / RSP / Preparedness / FSF). Owned in `mod-111`.
- **Program ownership** — running the assurance program as a standing organisational function. Owned in `mod-112`.

All eleven of those are the deep specialisation. `mod-101` places the position; the rest fill it in.

## What this role explicitly does not own

Restating the deferrals in one place, because they matter more than the ownership list:

- Not intake, inventory, jurisdictional tracking, or first-draft crosswalks — those belong to `ai-governance-analyst`.
- Not harm-model authoring, red-team engineering, or guardrail engineering — those belong to `ai-risk-engineer`.
- Not the application-layer eval engineering surface (trace / trajectory / RAG / judge / online-eval / eval-gated CI/CD) — that belongs to `ai-eval-engineer`.
- Not benchmark-construction or estimator methodology depth — that belongs to `model-evaluation-engineer`.
- Not the deep MLSec surface (eval-set exfiltration controls, judge supply-chain, model-extraction at platform scale) — that belongs to `ai-infra-security`.
- Not frontier-agent red-team methodology depth — that belongs to `agentic-safety-engineer`.
- Not control-library architecture or cross-jurisdictional reconciliation at institution scope — that belongs to `senior-ai-governance-architect`.
- Not board reporting or institution-scale regulator interface — that belongs to `head-of-ai-governance`.
- Not formal legal opinion — escalation to counsel is the correct disposition.

The rule for edge cases: **assign to the lowest-level role that genuinely requires the skill; this role links back rather than duplicates.**

## The differentiator, restated

Every peer touches evaluation. The peer at level 30 in AI Engineering *runs* it inside product; the peer at level 30 in ML Engineering *methodologises* it; the peer at level 25 *engineers the risks* being evaluated. What is different about this role is that it stakes an assurance case, decides the release, packages the evidence for audiences outside the engineering surface, and keeps the decision alive after ship.

That is why the role sits at level 35 in the Governance family rather than at level 30 in engineering families. It is not a more-senior eval engineer. It is the owner of a different discipline.

## Summary

- The role owns the release-assurance methodology — release-gate decisions, external-audience cards, third-party audit packages, regulator submissions, post-market surveillance.
- It sits at level 35 in AI Governance, peer to two level-30 evaluation specialists in other families and to an infra-security peer at level 35.
- It defers craft downward (analyst / risk / eval / model-eval / MLSec) and defers architecture and leadership upward (architect / head / CAIO).
- The next chapters walk the four bodies of literature the release-gate must map into: NIST AI RMF, ISO/IEC 42001, EU AI Act, and the international values baseline (OECD / CoE / UNESCO). The final chapter (`06`) writes the deferral contract explicitly.
