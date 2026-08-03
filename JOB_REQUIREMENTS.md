# Job Requirements — AI Evaluation Engineer (Governance family)

**Role level:** 35 (deep specialist, AI Governance family — release-assurance methodology owner; peer to `ai-eval-engineer` (level 30, AI Engineering) and `model-evaluation-engineer` (level 30, ML Engineering); peer to `ai-infra-security` (level 35) on the security side; next-up from `ai-risk-engineer` (level 25) and `ai-governance-analyst` (level 15); inherited upward by `senior-ai-governance-architect` (level 50), `head-of-ai-governance` (level 60), `chief-ai-officer` (level 70))
**Track:** `ai-evaluation-engineer-learning`
**Research window:** 2026-05-04 → 2026-08-03 (last 90 days, strict); 2026-02-04 → 2026-08-03 (extended, for role variants whose in-window volume was low)
**Today:** 2026-08-03

This file documents the requirements catalog used to seed and now to validate the AI Evaluation Engineer curriculum. Raw normalized posting data lives in [`.aicg/job-requirements.json`](.aicg/job-requirements.json); the planned curriculum lives in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json); this cycle's proposed additions live in [`.aicg/curriculum-plan-delta.json`](.aicg/curriculum-plan-delta.json).

## Status — live posting sample completed 2026-08-03

**34 postings sampled** across five employer segments — above the 25-posting minimum. Every one of the 12 owned requirement themes is backed by ≥ 3 in-window (or near-in-window) posting citations. No new capability recurred at ≥ 30% frequency outside the existing 12-module vocabulary, so the additions-empty delta is the expected output this cycle.

Segments sampled (see [`.aicg/job-requirements.json → research_status.sourcing_notes`](.aicg/job-requirements.json) for the full breakdown):

- **Frontier labs and independent evaluators** (9 postings) — Anthropic (RSP PM, Frontier Red Team, Safeguards Evals, Model Evaluations, Safeguards Labs), Google DeepMind (Responsibility & Safety Evaluations, Frontier Safety Risk Assessment, Frontier Safety Mitigations, Assurance Evaluation), UK AI Security Institute (Frontier Research Engineer, Security), Apollo Research (Research Scientist/Engineer, Evaluations), Cohere (Senior Research Engineer, Model Evaluation).
- **Hyperscalers and enterprise responsible-AI** (5 postings, plus the four Anthropic-in-frontier that also anchor this segment) — Microsoft AI (MAI Superintelligence Evaluations Engineer), Amazon Web Services (Sr Data Scientist WWSO Bedrock; SDE Responsible AI), Salesforce (Lead Engineer, AI Trust & Governance), SAP (AI Engineer, Applied AI & Data Validation).
- **Regulated industries — banks / insurers / pharma** (10 postings) — Deutsche Bank AI/ML Model Validation Analyst, Barclays AVP ML and GenAI Model Validation, Morgan Stanley GenAI MRM Associate, M&T Bank Model Risk Senior Analyst (AI/Cyber/Tech), MetLife AI Model Risk Analyst, New York Life Sr Associate Model Validation & AI Governance, Citi Model Validation 2nd LOD Sr Analyst C12, JPMorgan Model Risk Analyst (MRGR), Modicus Prime AI Evaluation Engineer (J&J JLABS, GxP pharma), Bank of America Sr Audit Manager AI Model Risk.
- **Big Four assurance and governance vendors / defense** (5 postings) — Deloitte SEA A&A AI Assurance, EY Senior AI Engineer Data Analytics Assurance, PwC Responsible AI Senior Associate, Booz Allen AI Engineer (defense-adjacent), Accenture Responsible AI Engineer.
- **Enterprise-regulated applied-AI validation** (1 posting) — Carnival Corporation Engineer AI Security Posture & Model Validation.

### Coverage gaps for the next cycle

Direct WebFetch was blocked or returned JS-only shells for:

- OpenAI Preparedness / Safety Advisory Group / Model Behavior / Model Policy — every OpenAI careers URL either 403'd or returned an empty shell.
- Meta GenAI Trust & Safety / GenAI Evaluations — Meta careers 404s.
- US AI Safety Institute at NIST — USAJOBS timeouts.
- IBM watsonx.governance direct hires, NVIDIA Trustworthy AI, Databricks / Mosaic AI Governance, ServiceNow AI Control Tower (Agentic/GenAI Evaluations), Adobe / Oracle / Snowflake / Palantir.
- Governance-vendor Ashby-hosted listings — Credo AI, Holistic AI, ModelOp, Monitaur, Fiddler AI Trust, Modulos, Trustible, Fairly AI, Anch AI (all returned JavaScript-only shells).
- Legal-regtech applied-AI teams — Harvey, Thomson Reuters CoCounsel Trust, LexisNexis, Robin AI.

None of these gaps changes the shape of the curriculum this cycle — the sampled segments already cover every module theme and the deferred segments would only add reinforcing evidence to the same requirement clusters, not new ones.

### In-window vs. extended-window postings

Strict 90-day window (2026-05-04 onward): 25 postings. Six additional postings fall between 2026-02-04 and 2026-05-03 and are retained because they are the closest published exemplars of specific title / employer combinations (Modicus Prime "AI Evaluation Engineer" verbatim title, Barclays AVP ML/GenAI Model Validation, DeepMind Frontier Safety Mitigations, Anthropic Frontier Red Team RSP Evaluations, Anthropic Research Engineer Model Evaluations, Anthropic RE (Sr Staff+) Safeguards Labs). Three further postings are flagged as older than the extended window and retained as historical calibration (post-frontier-03 posted 2025-08-03).

## Methodology

1. Fanned out four parallel research agents (frontier labs + independents, hyperscalers + enterprise RAI, regulated industries, Big Four + vendors + defense T&E). Each agent WebSearched and WebFetched real posting URLs; agents were instructed never to fabricate.
2. Normalized 34 collected postings into `.aicg/job-requirements.json → postings` with employer, title, URL, `source_type` (direct/aggregator), `date_observed`, `date_posted`, location, `salary_range` (verbatim or null), `role_fit` (core/borderline), verbatim required and preferred bullets, a representative quote, and a closed-vocabulary `requirement_tags` array mapped 1:1 to the existing 12-module curriculum.
3. Scored per-requirement frequencies (`.aicg/job-requirements.json → requirement_tag_frequencies`) and backfilled `evidence_post_ids` for each of the 12 owned-requirement blocks.
4. Applied the continuity-bias rule for the delta: an addition is proposed only when (a) ≥ 3 distinct in-window postings cite a requirement not covered by the existing curriculum, (b) frequency ≥ 30%, and (c) no existing module can be incrementally extended. **No item cleared all three bars this cycle.**
5. Applied the ownership rule — no requirement was demoted or re-assigned because every backfilled requirement retained clear posting evidence in the AI Evaluation Engineer band (not the level-30 peer methodology tracks and not the level-15 analyst track).

## Requirement themes → curriculum ownership → posting evidence

`Freq` = fraction of the 34 postings whose `requirement_tags` include the tag. `Owner` is per the ownership rule in [`.aicg/job-requirements.json → ownership_rule`](.aicg/job-requirements.json).

| # | Theme | Freq | Owner role | Coverage |
|---|---|---|---|---|
| 1 | Release-assurance position: ladder placement, values baseline, deferral map | 0.74 | `ai-evaluation-engineer` (this) | [`mod-101-release-assurance-position`](lessons/mod-101-release-assurance-position) |
| 2 | Assurance-case engineering (GSN, CAE, SACM) for AI evaluation evidence | 0.24 | `ai-evaluation-engineer` | [`mod-102-assurance-case-engineering`](lessons/mod-102-assurance-case-engineering) |
| 3 | Release-gate architecture for AI products and platforms | 0.53 | `ai-evaluation-engineer` | [`mod-103-release-gate-architecture`](lessons/mod-103-release-gate-architecture) |
| 4 | Evaluation evidence pipeline: immutable logs, lineage, ML-BOM, signed release-gate outputs | 0.82 | `ai-evaluation-engineer` | [`mod-104-evaluation-evidence-pipeline`](lessons/mod-104-evaluation-evidence-pipeline) |
| 5 | Model / system / dataset cards for regulatory & third-party audiences | 0.12 | `ai-evaluation-engineer` | [`mod-105-cards-for-external-audiences`](lessons/mod-105-cards-for-external-audiences) |
| 6 | Cross-jurisdictional evaluation-obligation mapping (EU AI Act / NIST AI RMF / ISO 42001 / sector rules) | 0.21 | `ai-evaluation-engineer` | [`mod-106-cross-jurisdictional-obligation-mapping`](lessons/mod-106-cross-jurisdictional-obligation-mapping) |
| 7 | Sector-regulated assurance shape (SR 11-7 / OCC / SR 23-4 / FDA GMLP / PCCP / DORA) | 0.41 | `ai-evaluation-engineer` | [`mod-107-sector-regulated-assurance`](lessons/mod-107-sector-regulated-assurance) |
| 8 | Deployment-tier gating (RSP / Preparedness / DeepMind FSF shape adapted to enterprise) | 0.26 | `ai-evaluation-engineer` | [`mod-108-deployment-tier-gating`](lessons/mod-108-deployment-tier-gating) |
| 9 | Third-party evaluator and auditor interface (AISI / notified bodies / Big Four / independent audits) | 0.18 | `ai-evaluation-engineer` | [`mod-109-third-party-evaluator-and-auditor-interface`](lessons/mod-109-third-party-evaluator-and-auditor-interface) |
| 10 | Post-market surveillance and continuous assurance (EU AI Act Art. 72, FDA PCCP, incident-DB feedback) | 0.18 | `ai-evaluation-engineer` | [`mod-110-post-market-surveillance`](lessons/mod-110-post-market-surveillance) |
| 11 | GenAI / GPAI systemic-risk assurance (EU AI Act Art. 55, GPAI Code, RSP / Preparedness / FSF interface) | 0.09 | `ai-evaluation-engineer` | [`mod-111-gpai-systemic-risk-assurance`](lessons/mod-111-gpai-systemic-risk-assurance) |
| 12 | Owning an enterprise AI-evaluation-assurance program | 0.47 | `ai-evaluation-engineer` | [`mod-112-owning-an-assurance-program`](lessons/mod-112-owning-an-assurance-program) |
| 13 | Classical ML / packaging / eval-scripting fundamentals | n/a — prerequisite | `ml-engineer` (level 20) | Linked out in [`PREREQUISITES.md`](PREREQUISITES.md); not re-taught |
| 14 | AI use-case intake / inventory / framework crosswalk drafts / first-draft cards | n/a — prerequisite | `ai-governance-analyst` (level 15) | Linked out in [`PREREQUISITES.md`](PREREQUISITES.md); prerequisite for this role |
| 15 | Risk engineering craft (harm modelling, LLM / agent red-team engineering, adversarial-ML, guardrail engineering) | n/a — lower peer | `ai-risk-engineer` (level 25) | Consumed as evidence in mod-104 and mod-108; engineering craft linked out |
| 16 | Application-layer evaluation engineering (trace / trajectory / RAG / judge / online-eval / eval-gated CI/CD / eval-platform slice) | n/a — peer specialist | `ai-eval-engineer` (level 30, AI Engineering) | Consumed as evidence in mod-104 and mod-108; app-eval engineering linked out |
| 17 | Model-eval methodology depth (validity theory, bootstrap CIs, benchmark construction, calibration, judge-vs-human methodology, MLPerf) | n/a — peer specialist | `model-evaluation-engineer` (level 30, ML Engineering) | Consumed as evidence in mod-104 and mod-108; methodology linked out |
| 18 | Deep ML/AI security (eval-set exfiltration controls, judge supply-chain, adversarial-eval depth) | n/a — peer specialist | `ai-infra-security` (level 35) | Awareness in mod-104 and mod-108; controls consumed via evidence handoff |
| 19 | General product / application security fundamentals | n/a — peer track | `security-learning` (level 35) | Awareness in mod-104 and mod-108; controls consumed via evidence handoff |
| 20 | Frontier-agent red-team depth / dangerous-capability elicitation | n/a — higher level | `agentic-safety-engineer` (level 40) | Awareness in mod-108 and mod-111; depth owned upward |
| 21 | Control-library architecture / cross-jurisdiction reconciliation / policy taxonomy | n/a — higher level | `senior-ai-governance-architect` (level 50) | Linked out from mod-112; this role emits the release-assurance design that architect harmonises |
| 22 | Program leadership / board reporting / regulator interface at institution level | n/a — higher level | `head-of-ai-governance` (level 60) | Linked out from mod-112; this role produces the evidence that leadership narrates |
| 23 | Post-training (SFT / PEFT / RLHF / DPO) depth | n/a — peer specialist | `fine-tuning-engineer` (level 30) | Out of scope — this role evaluates fine-tuned outputs for release |
| 24 | Distributed training PLATFORM engineering | n/a — peer track | `training-pipeline-engineer` (level 25) | Out of scope |
| 25 | Formal legal opinion / advocacy | n/a — out of scope | legal counsel | Paralegal-level reading is in scope; legal opinion is not — escalations to counsel are the correct disposition |

### Reading the frequencies

- **`evidence-pipeline` (0.82)** and **`release-assurance-position` (0.74)** are the two dominant themes across the sample — a release-assurance-methodology owner is fundamentally in the business of packaging evidence and holding the ladder position between technical producers and external audiences. The 12-module curriculum's centre-of-mass sits exactly there ([mod-101](lessons/mod-101-release-assurance-position) + [mod-104](lessons/mod-104-evaluation-evidence-pipeline)).
- **`release-gate` (0.53)**, **`assurance-program-ownership` (0.47)**, and **`sector-regulated` (0.41)** are the second tier — release-gate architecture is universal at frontier labs (RSP / FSF) and hyperscalers; sector-regulated is the finance-heavy half of the sample (SR 11-7 shape at Barclays / M&T Bank / Citi / JPM MRGR / BofA plus FDA GxP at Modicus Prime).
- **`deployment-tier` (0.26)** and **`assurance-case` (0.24)** cluster together at frontier labs and 2nd-LOD MRM. Assurance-case notation (GSN / CAE / SACM) is never named in the postings verbatim, but the underlying discipline — building defensible evidence trees for "Capability Reports" (Anthropic RSP) and "independent challenge" validation reports (SR 11-7 MRM) — is exactly what postings are pricing.
- **`model-cards` (0.12)** is the lowest of the twelve. Anthropic's RSP PM posting explicitly names "system card reviews" as a duty; the rest of the sample refers to card-adjacent artefacts under other names ("validation report", "release evidence", "handover materials"). The module is retained because it is a core differentiator against peer level-30 tracks and because the low posting-frequency reflects diverse naming rather than absent demand.
- **`gpai` (0.09)** is the freshest theme — three postings (DeepMind Frontier Safety Risk Assessment, Deloitte SEA A&A AI Assurance, Barclays AVP GenAI Model Validation) name GPAI or systemic-risk vocabulary. The module is retained because enterprise deployers will start being audited against GPAI obligations under EU AI Act Article 55, and low current frequency signals a 2026-emerging obligation rather than an absent one.

## Ownership decisions this cycle

No requirement was demoted or moved. Every owned requirement kept its module. No new requirement cleared the continuity-bias bar. Nothing was added.

The three items that came closest to a possible addition — and the reason each was rejected:

1. **Automated fleet-scale discovery of AI workloads with regulatory-risk classification** — surfaced strongly in one posting (Amazon SDE Responsible AI: "systems that discover AI workloads across Amazon's fleet, classify them against regulatory risk frameworks, streamline compliance evidence collection through paved-path tooling"). Single-posting evidence, well under the 3-posting bar. If it grows next cycle, it fits as an exercise inside [`mod-112`](lessons/mod-112-owning-an-assurance-program), not as a new module.
2. **Cyber / technology model risk as a co-owned validation surface** — M&T Bank's "AI, Cyber, Technology" validation scope explicitly bundles all three. Only one posting; expansion into the AI/ML validator role at other banks is likely but not yet visible. If it grows, it fits inside [`mod-107`](lessons/mod-107-sector-regulated-assurance) as an additional sector overlay, not as a new module.
3. **Agentic-system evaluation as a distinct assurance surface** — mentioned in 6+ postings (Anthropic Safeguards Evals, Anthropic Research Model Evaluations, Anthropic Safeguards Labs, Barclays AVP, Apollo Research, Salesforce Lead Engineer AI Trust & Governance) but always as a specialisation of existing evaluation surfaces. Already threaded through [`mod-104`](lessons/mod-104-evaluation-evidence-pipeline) (agentic trace / trajectory evidence) and [`mod-108`](lessons/mod-108-deployment-tier-gating) (agentic-tier gating with AgentDojo-style benchmarks). No new module needed; if next cycle shows the frequency crossing 30% the response is an exercise inside mod-108, not a new module.

## Posting evidence — summary table

| ID | Employer | Title | Location | Date | Salary | Fit | Segment |
|---|---|---|---|---|---|---|---|
| post-frontier-01 | Anthropic | Program Manager, Responsible Scaling Policy | New York, NY | 2026-07-14 | $190,000 – $235,000 USD | core | frontier-lab |
| post-frontier-02 | Anthropic | Research Engineer, Frontier Red Team (RSP Evaluations) | San Francisco / Seattle | 2026-01-30 | $280,000 – $340,000 USD | core | frontier-lab |
| post-frontier-03 | Anthropic | Research Engineer, Frontier Red Team (RSP Evaluations) | San Francisco / Seattle | 2025-08-03 | $315,000 – $425,000 USD | core | frontier-lab |
| post-frontier-04 | Google DeepMind | Research Engineer, Frontier Safety Risk Assessment | London | 2026-07-03 | $136,000 – $245,000 USD | core | frontier-lab |
| post-frontier-05 | Google DeepMind | Research Engineer, Frontier Safety Mitigations | London | 2026-04-07 | not disclosed | core | frontier-lab |
| post-frontier-06 | UK AI Security Institute | Frontier Research Engineer, Security | London (+5 UK cities) | 2026-07-03 | £65,000 – £145,000 | borderline | independent-evaluator |
| post-frontier-07 | Apollo Research | Research Scientist/Engineer (Evaluations) | London / San Francisco | 2026-07-15 | not disclosed | core | independent-evaluator |
| post-frontier-08 | Anthropic | Research Engineer, Model Evaluations | SF / NY / Seattle | 2026-01-30 | $320,000 – $405,000 USD | borderline | frontier-lab |
| post-frontier-09 | Cohere | Senior Research Engineer, Model Evaluation | not specified | 2026-06-15 | not disclosed | borderline | frontier-lab |
| post-hyperscaler-01 | Google DeepMind | Research Engineering Manager, Responsibility & Safety Evaluations | London | estimate:2026-05 | not disclosed | core | hyperscaler |
| post-hyperscaler-02 | Anthropic | Staff+ Software Engineer, Safeguards Evals | SF / NY | estimate:2026-06 | $320,000 – $485,000 USD | core | frontier-lab |
| post-hyperscaler-03 | Anthropic | Research Engineer (Senior Staff+), Safeguards Labs | SF / NY | estimate:2026-06 | $350,000 – $850,000 USD | borderline | frontier-lab |
| post-hyperscaler-04 | Microsoft AI | Member of Technical Staff, Evaluations Engineer (MAI Superintelligence) | Multiple US | estimate:2026-07 | $142,800 – $331,200 USD | core | hyperscaler |
| post-hyperscaler-05 | Amazon Web Services | Sr Data Scientist, WWSO Bedrock | East Palo Alto / NY / Austin / Arlington / Seattle | estimate:2026-06 | $159,200 – $247,600 USD | borderline | hyperscaler |
| post-hyperscaler-06 | Amazon (Responsible AI) | SDE, Responsible AI | Seattle | estimate:2026-07 | $143,700 – $194,400 USD | borderline | hyperscaler |
| post-hyperscaler-07 | Salesforce | Lead Engineer - AI Trust & Governance | SF / Seattle / Chicago / PA / NY / Bellevue | estimate:2026-06 | not disclosed | core | hyperscaler |
| post-hyperscaler-08 | SAP | AI Engineer - Applied AI & Data Validation | Sofia, Bulgaria | 2026-07-22 | not disclosed | borderline | hyperscaler |
| post-hyperscaler-09 | Google DeepMind | Research Engineer - Assurance Evaluation | London | estimate:2026-05 | not disclosed | core | hyperscaler |
| post-audit-01 | Deloitte (SEA) | A&A - SG - AI Assurance (Consultant / Sr Consultant) | Singapore | 2026-07-19 | not disclosed | core | big-four |
| post-audit-02 | EY | Senior AI Engineer, Data Analytics Assurance | not specified | 2026-07-30 | competitive | borderline | big-four |
| post-audit-03 | PwC | Responsible AI Senior Associate | New York / Boston / Florham Park / Dallas / Philadelphia / Houston | estimate:2026-07 | $77,000 – $202,000 | borderline | big-four |
| post-audit-04 | Booz Allen Hamilton | AI Engineer (R0244899) | Washington, DC | estimate:2026-07 | $99,000 – $225,000 | borderline | big-four |
| post-audit-05 | Carnival Corporation | Engineer, AI Security Posture & Model Validation | Miami, FL | 2026-07-21 | not disclosed | core | enterprise-regulated |
| post-audit-06 | Accenture | Responsible AI Engineer (R00329071) | Multiple US | estimate:2026-06 | $68,300 – $220,400 | core | big-four |
| post-regulated-01 | Deutsche Bank | AI/ML Model Validation Analyst | Mumbai | estimate:2026 | not disclosed | core | regulated-finance |
| post-regulated-02 | Barclays | AVP ML and GenAI Model Validation | Noida, India | 2026-04-18 | not disclosed | core | regulated-finance |
| post-regulated-03 | Morgan Stanley | Generative AI - Model Risk Management Associate | Budapest | estimate:2026 | not disclosed | core | regulated-finance |
| post-regulated-04 | M&T Bank | Model Risk Senior Analyst - Validation (AI, Cyber, Technology) | Buffalo, NY | estimate:2026 | $103,000 – $171,600 USD | core | regulated-finance |
| post-regulated-05 | MetLife | AI Model Risk Analyst | New York, NY | estimate:2026-05 | $105,000 – $150,000 USD | core | regulated-insurance |
| post-regulated-06 | New York Life | Sr Associate - Model Validation and AI Governance | New York, NY | estimate:2026 | $124,000 – $177,000 USD | core | regulated-insurance |
| post-regulated-07 | Citi | Model Validation 2nd LOD Sr. Analyst - C12 | Tampa, FL | 2026-06-24 | $117,650 – $130,920 USD | borderline | regulated-finance |
| post-regulated-08 | JPMorgan Chase | Model Risk Analyst (MRGR) | Bengaluru | estimate:2026 | not disclosed | core | regulated-finance |
| post-regulated-09 | Modicus Prime (J&J JLABS) | AI Evaluation Engineer | US (Austin preferred) | 2026-02-08 | equity + cash mix | core | regulated-healthcare |
| post-regulated-10 | Bank of America | Sr Audit Manager - AI Model Risk | Remote | estimate:2026 | not disclosed | borderline | regulated-finance |

Verbatim required / preferred bullets and representative quotes for each posting are in [`.aicg/job-requirements.json → postings`](.aicg/job-requirements.json).

## Ownership map — quick reference

When you're triaging a posting for a future cycle, use this decision to keep the curriculum from drifting into peer territory:

- **AI Evaluation Engineer** (this track, level 35, AI Governance family) — owns the *release-assurance methodology*: turning raw evaluation evidence (produced by peers below and by peer specialists at level 30) into defensible release-gate decisions, model / system / dataset cards for external audiences, third-party audit packages, regulator-facing submissions, and post-market-surveillance evidence. **Release-assurance methodology and the interface to regulator / auditor / board audiences are the differentiators against peers.**
- **AI Eval Engineer** (peer, level 30, AI Engineering family, `ai-eval-engineer-learning`) — owns *application-layer evaluation engineering*: trace instrumentation, trajectory / tool-call scoring, LLM-as-judge in product pipelines, RAG evaluation, eval-gated CI/CD, online eval, eval-data-platform slice, app-side safety measurement. **This role consumes the trace / trajectory / RAG / judge / online-eval evidence and packages it for external audiences.**
- **Model Evaluation Engineer** (peer, level 30, ML Engineering family) — owns *model-eval methodology depth*: benchmark engineering, statistical estimation, calibration, judge-vs-human methodology, cross-modality harnesses, MLPerf. **This role cites this peer's methodology in evidence packages and validates that release-gate thresholds are statistically defensible.**
- **AI Risk Engineer** (lower peer, level 25) — owns *risk-engineering craft*: harm modelling engineering, LLM / adversarial-ML red-team engineering, guardrail engineering. **This role consumes the risk-engineer's outputs and threads them into the release-gate evidence.**
- **AI Governance Analyst** (prerequisite, level 15) — owns *operational analyst legwork*: intake, inventory, framework crosswalk drafts, first-draft cards, regulatory tracking. **This role elevates from the analyst's outputs to program ownership.**
- **AI Infra Security** (peer, level 35) and **Security Engineer** (peer, level 35) — own *deep MLSec and product security*. **This role consumes their controls in the supply-chain and evaluation-set-security clauses of the release-gate.**
- **Agentic Safety Engineer** (higher, level 40) — owns *frontier-agent red-team methodology*. **This role links up to that track's evidence for GPAI systemic-risk assurance in mod-111.**
- **Senior AI Governance Architect / Head of AI Governance / Chief AI Officer** (levels 50 / 60 / 70) — inherit this packet upward for architectural, methodological, and leadership scope.

## Salary evidence (from live postings this cycle)

Verbatim, cited, no fabrication. Ranges are as published on the posting page or the aggregator that carried it.

**Frontier labs (USD, IC-level, mid to senior)** — the ceiling reflects the frontier-lab premium.

- Anthropic Program Manager, Responsible Scaling Policy — $190,000 – $235,000
- Anthropic Research Engineer, Frontier Red Team (RSP Evaluations) — $280,000 – $340,000 (post-frontier-02) / $315,000 – $425,000 (post-frontier-03)
- Anthropic Staff+ Software Engineer, Safeguards Evals — $320,000 – $485,000
- Anthropic Research Engineer (Sr Staff+), Safeguards Labs — $350,000 – $850,000
- Anthropic Research Engineer, Model Evaluations — $320,000 – $405,000
- Google DeepMind Research Engineer, Frontier Safety Risk Assessment (London) — $136,000 – $245,000

**Hyperscalers (USD, US locations)** — leveled bands published in-jurisdiction.

- Microsoft AI Member of Technical Staff, Evaluations Engineer (MAI Superintelligence) — IC5: $142,800 – $274,800 std US / $188,000 – $304,200 SF Bay + NYC; IC6: $165,600 – $296,400 std US / $220,800 – $331,200 SF Bay + NYC
- Amazon Web Services Sr Data Scientist, WWSO Bedrock — $159,200 – $247,600 (varies by location)
- Amazon (Responsible AI) SDE, Responsible AI — $143,700 – $194,400 (Seattle)

**Regulated industries (USD, MRM/validation IC-mid)**.

- M&T Bank Model Risk Senior Analyst — $103,000 – $171,600
- MetLife AI Model Risk Analyst — $105,000 – $150,000 + Annual Bonus
- New York Life Sr Associate Model Validation & AI Governance — $124,000 – $177,000
- Citi Model Validation 2nd LOD Sr Analyst C12 — $117,650 – $130,920

**Big Four / audit / defense (USD, wide bands published across geographies)**.

- PwC Responsible AI Senior Associate — $77,000 – $202,000
- Booz Allen AI Engineer — $99,000 – $225,000
- Accenture Responsible AI Engineer — $68,300 – $220,400 (CA cap)

**Public-sector independent evaluator (GBP)**.

- UK AI Security Institute Frontier Research Engineer, Security — £65,000 – £145,000

Postings that did not publish a salary band: Anthropic Program Manager RSP (published), Apollo Research Research Scientist/Engineer, Cohere Sr Research Engineer, DeepMind (all), Salesforce Lead Engineer, SAP AI Engineer, Deloitte SEA A&A AI Assurance, EY Sr AI Engineer (competitive), all Deutsche Bank / Barclays / Morgan Stanley / JPMorgan / Bank of America non-US postings, Carnival Corporation, Modicus Prime (equity/cash mix).

## Change log

- **2026-08-03** — live posting cycle. 34 postings sampled across five employer segments. Every owned requirement backed with ≥ 3 posting citations except `gpai` (3) and `model-cards` (4). No requirement demoted, no new requirement cleared the continuity-bias bar. `.aicg/curriculum-plan-delta.json` proposes zero additions this cycle — the expected output per the packet rules when nothing has materially shifted.
- **2026-07-10** — initial bootstrap. Postings deferred; requirements grounded in the authoritative-reference set catalogued in `.aicg/job-requirements.json → authoritative_references`.
