# Prerequisites for the AI Evaluation Engineer track (Governance family, level 35)

This is a level-35 specialist track. It assumes the learner already has:

## Engineering craft (level 10)

- Linux fundamentals, Git, HTTP APIs, packaging, Python fluency to the level owned by [`ai-infra-junior-engineer-learning`](https://github.com/ai-infra-curriculum/ai-infra-junior-engineer-learning).
- Reading pandas / SQL well enough to reconcile a model-registry export against a governance inventory row.

## Classical ML fundamentals (level 20)

- Awareness of the classical ML / PyTorch / sklearn-eval / packaging fundamentals owned by [`ml-engineer-learning`](https://github.com/ml-engineering-curriculum/ml-engineer-learning). This track evaluates ML systems for release; it does not re-teach how to build them.

## AI-governance analyst legwork (level 15)

- The analyst-tier operational workflow owned by [`ai-governance-analyst-learning`](https://github.com/ai-governance-curriculum/ai-governance-analyst-learning) — AI use-case intake, model / system inventory, first-draft NIST AI RMF / ISO 42001 / EU AI Act crosswalks, first-draft model / system / dataset cards, jurisdictional regulatory tracking. This track elevates from the analyst's outputs to program ownership.

## AI risk engineering (level 25)

- The engineering craft owned by [`ai-risk-engineer-learning`](https://github.com/ai-governance-curriculum/ai-risk-engineer-learning) — harm modelling, LLM / agent red-team engineering, adversarial-ML, fairness / bias / explainability engineering, privacy-risk engineering, guardrail engineering, AI-specific incident response. This track consumes the risk-engineer's outputs and threads them through the release-gate; it does not re-author them.

## Awareness of the peer specialist tracks (level 30)

The learner is expected to be able to read the outputs of these peer specialists and thread them into the release-gate. This track does not re-teach the peers' methodology:

- [`ai-eval-engineer-learning`](https://github.com/ai-engineering-curriculum/ai-eval-engineer-learning) (level 30, AI Engineering family) — application-layer evaluation engineering (trace / trajectory / RAG / judge / online-eval / eval-gated CI/CD / eval-data-platform slice).
- [`model-evaluation-engineer-learning`](https://github.com/ml-engineering-curriculum/model-evaluation-engineer-learning) (level 30, ML Engineering family) — model-eval methodology depth.

## Reading maturity

- Comfortable reading a regulation or standard end-to-end and translating an obligation into an engineering deliverable. The track cites, at minimum, the following primary sources as required reading:
  - NIST AI RMF 1.0 + Playbook + Generative AI Profile (AI 600-1)
  - ISO/IEC 42001:2023, ISO/IEC 23894:2023, ISO/IEC 42005:2025, ISO/IEC 25059:2023, ISO/IEC 24029-2:2023
  - EU AI Act (Regulation 2024/1689) — Articles 8–15, 17, 26, 43, 47, 49, 55, 61, 72, Annex III
  - Federal Reserve SR 11-7 and OCC 2011-12 (model-risk management)
  - FDA GMLP and PCCP guidance
  - Anthropic RSP, OpenAI Preparedness, Google DeepMind Frontier Safety Framework

## What this track does not require

- Formal legal training. Paralegal-level reading of regulations is in scope; formal legal opinion is not — escalations to counsel are the correct disposition.
- Deep frontier-agent red-team methodology (owned upward by [`agentic-safety-engineer-learning`](https://github.com/ai-governance-curriculum/agentic-safety-engineer-learning) at level 40).
- Board-level narration and institution-wide regulator interface (owned upward by [`head-of-ai-governance-learning`](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) at level 60).
