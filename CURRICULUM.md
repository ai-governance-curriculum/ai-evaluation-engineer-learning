# AI Evaluation Engineer Curriculum (Governance family, level 35)

Release-assurance-methodology specialist track. Turns raw evaluation evidence into defensible release-gate decisions, model / system / dataset cards for external audiences, third-party audit packages, regulator-facing submissions, and post-market surveillance evidence.

> **Status**: curriculum plan authored 2026-07-10. Postings sample deferred to the next autonomous cycle — see [`JOB_REQUIREMENTS.md → Status`](JOB_REQUIREMENTS.md#status--bootstrap-session-postings-deferred). Lesson content and worked exercises land on subsequent cycles.

## Level ladder

Level 35, AI Governance family. Peer to `ai-eval-engineer` (level 30, AI Engineering — application-layer eval engineering) and to `model-evaluation-engineer` (level 30, ML Engineering — model-eval methodology depth); peer to `ai-infra-security` and `security-learning` (level 35); next-up from `ai-risk-engineer` (level 25) and `ai-governance-analyst` (level 15); inherited upward by `agentic-safety-engineer` (level 40), `senior-ai-governance-architect` (level 50), `head-of-ai-governance` (level 60), `chief-ai-officer` (level 70).

Full ownership map lives in [`.aicg/curriculum-plan.json → ownership_rule`](.aicg/curriculum-plan.json) and in [`JOB_REQUIREMENTS.md → Ownership map`](JOB_REQUIREMENTS.md#ownership-map--quick-reference-for-next-cycle).

## Module plan

Total taught hours: ~167 (modules) + ~130 (projects) = ~297 hours.

| Module | Title | Hours | Status |
|---|---|---|---|
| [mod-101](lessons/mod-101-release-assurance-position/) | Release-Assurance Position: The Assurance Methodology Owner on the Ladder | 12 | planned |
| [mod-102](lessons/mod-102-assurance-case-engineering/) | Assurance-Case Engineering for AI Evaluation Evidence | 14 | planned |
| [mod-103](lessons/mod-103-release-gate-architecture/) | Release-Gate Architecture for AI Products and Platforms | 15 | planned |
| [mod-104](lessons/mod-104-evaluation-evidence-pipeline/) | Evaluation Evidence Pipeline: Immutable Logs, Lineage, and Reproducibility Bundles | 15 | planned |
| [mod-105](lessons/mod-105-cards-for-external-audiences/) | Model, System, and Dataset Cards for Regulatory and Third-Party Audiences | 14 | planned |
| [mod-106](lessons/mod-106-cross-jurisdictional-obligation-mapping/) | Cross-Jurisdictional Evaluation-Obligation Mapping | 16 | planned |
| [mod-107](lessons/mod-107-sector-regulated-assurance/) | Sector-Regulated Assurance: SR 11-7 / OCC / SR 23-4 / FDA GMLP / PCCP / DORA | 15 | planned |
| [mod-108](lessons/mod-108-deployment-tier-gating/) | Deployment-Tier Gating: RSP / Preparedness / DeepMind FSF Adapted to Enterprise | 14 | planned |
| [mod-109](lessons/mod-109-third-party-evaluator-and-auditor-interface/) | Third-Party Evaluator and Auditor Interface | 12 | planned |
| [mod-110](lessons/mod-110-post-market-surveillance/) | Post-Market Surveillance and Continuous Assurance | 12 | planned |
| [mod-111](lessons/mod-111-gpai-systemic-risk-assurance/) | GenAI / GPAI Systemic-Risk Assurance | 14 | planned |
| [mod-112](lessons/mod-112-owning-an-assurance-program/) | Owning an Enterprise AI-Evaluation-Assurance Program | 14 | planned |

## Projects

| Project | Title | Hours | Integrates |
|---|---|---|---|
| [project-101](projects/project-101-release-gate-capstone/) | Release-Gate Capstone: End-to-End Release-Gate for a Regulated AI Product | 40 | mod-101, 102, 103, 104, 105 |
| [project-102](projects/project-102-cross-jurisdictional-compliance-map/) | Cross-Jurisdictional Evaluation-Obligation Compliance Map | 35 | mod-105, 106, 107, 110 |
| [project-103](projects/project-103-assurance-program-slice/) | Enterprise Assurance-Program Slice: Intake, Evidence, Cards, Third-Party Handoff, Post-Market | 55 | mod-101–112 |

## Deferrals — what this curriculum does NOT re-teach

- **Analyst legwork** (intake, inventory, first-draft cards, jurisdictional tracking) — owned by [`ai-governance-analyst`](https://github.com/ai-governance-curriculum/ai-governance-analyst-learning) (level 15).
- **Risk-engineering craft** (harm modelling, LLM / adversarial-ML red-team engineering, guardrail engineering) — owned by [`ai-risk-engineer`](https://github.com/ai-governance-curriculum/ai-risk-engineer-learning) (level 25).
- **Application-layer evaluation engineering** (trace / trajectory / RAG / judge / online-eval / eval-gated CI/CD / eval-data-platform slice) — owned by [`ai-eval-engineer`](https://github.com/ai-engineering-curriculum/ai-eval-engineer-learning) (level 30, AI Engineering family).
- **Model-eval methodology depth** (validity theory, bootstrap CIs, benchmark construction, calibration methodology, cross-modality harnesses, MLPerf) — owned by [`model-evaluation-engineer`](https://github.com/ml-engineering-curriculum/model-evaluation-engineer-learning) (level 30, ML Engineering family).
- **Deep MLSec** (eval-set exfiltration controls, adversarial-eval depth, judge supply-chain, model-extraction at platform scale) — owned by [`ai-infra-security`](https://github.com/ai-infra-curriculum/ai-infra-security-learning) (level 35).
- **Frontier-agent red-team methodology depth** — owned by [`agentic-safety-engineer`](https://github.com/ai-governance-curriculum/agentic-safety-engineer-learning) (level 40).
- **Control-library architecture, cross-jurisdiction reconciliation, policy taxonomy** — owned by [`senior-ai-governance-architect`](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) (level 50).
- **Program leadership, board reporting, regulator interface at institution scope** — owned by [`head-of-ai-governance`](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) (level 60) and [`chief-ai-officer`](https://github.com/ai-governance-curriculum/chief-ai-officer-learning) (level 70).

## Sources

Every module and project is grounded in the authoritative-reference set catalogued in [`.aicg/job-requirements.json → authoritative_references`](.aicg/job-requirements.json). Requirement claims that lack posting evidence are flagged with `<!-- needs-research: ... -->` in [`JOB_REQUIREMENTS.md`](JOB_REQUIREMENTS.md).
