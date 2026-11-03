# Job Requirements — AI Evaluation Engineer (Governance family)

**Role level:** 35 (deep specialist, AI Governance family — release-assurance methodology owner; peer to `ai-eval-engineer` (level 30, AI Engineering) and `model-evaluation-engineer` (level 30, ML Engineering); peer to `ai-infra-security` (level 35) on the security side; next-up from `ai-risk-engineer` (level 25) and `ai-governance-analyst` (level 15); inherited upward by `senior-ai-governance-architect` (level 50), `head-of-ai-governance` (level 60), `chief-ai-officer` (level 70))
**Track:** `ai-evaluation-engineer-learning`
**Research window:** 2026-08-05 → 2026-11-03 (last 90 days, strict); 2026-05-05 → 2026-11-03 (extended, for role variants whose in-window volume was low)
**Today:** 2026-11-03

This file documents the requirements catalog used to seed and now to validate the AI Evaluation Engineer curriculum. Raw normalized posting data lives in [`.aicg/job-requirements.json`](.aicg/job-requirements.json); the planned curriculum lives in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json); this cycle's proposed additions live in [`.aicg/curriculum-plan-delta.json`](.aicg/curriculum-plan-delta.json).

## Status — refreshed posting sample completed 2026-11-03

**178 postings in the combined evidence base** (57 new this cycle + 121 retained from 2026-10), well above the 25-posting minimum. Every one of the 12 owned requirement themes continues to be backed by ≥ 3 in-window posting citations. No new capability recurred at ≥ 30% full-sample frequency outside the existing 12-module vocabulary, so the additions-empty delta is the expected output this cycle. The 2026-10 cycle already added `exercise-06-agentic-release-gate-and-trajectory-evidence` to `mod-108-deployment-tier-gating` in response to agentic-assurance crossing 30%; this cycle confirms the frequency has held above the bar (0.37, up from 0.35) and that the response is still correct — no further exercise warranted. Four secondary candidates (governance-platform-operator shape, MCP / agent-security tier-permission scoping, bundled AI + Cyber + Technology validation surface, clinical-AI release-gate language with FDA GMLP + EU MDR dual-regulator vocabulary) each clear the 3-posting bar but remain below the 30% full-sample bar and are absorbable into existing modules per prior-cycle decisions.

Segments sampled this cycle (see [`.aicg/job-requirements.json → research_status.sourcing_notes`](.aicg/job-requirements.json) for the full breakdown):

- **Frontier labs and independent evaluators** (39 postings combined; 15 new) — Anthropic (Policy PM Safeguards Regulatory, Research Engineer Post-Training Model Evaluations, TPM Safeguards Infrastructure & Evals, Safeguards Enforcement Analyst Safety Evaluations refetched, Research Engineer Frontier Red Team RSP refetched, plus 2026-10 retains for RSP PM, Safeguards Enforcement Integrity & Authenticity, Technical Policy Lead), OpenAI (Researcher Safety Frontier Assurance, Model Policy Manager National Security — first OpenAI captures this cycle via a16z and workatailab mirrors), Google DeepMind (Senior Research Scientist Gemini Release Evaluations, Research Engineer Frontier Safety Mitigations refetched, plus 2026-10 retains for Frontier Safety Risk Assessment, Assurance Evaluation, Responsibility & Safety Evaluations, Data Scientist ReDI, Sr TPM AI Safety), UK AISI (EOI Cyber & Autonomous Systems, EOI Core Technology, plus 2026-10 retains for Frontier Research Engineer Security, Software Engineer Core Technology, EOI Next-generation Agentic Controls and Forensics, Human Influence RE), US CAISI at NIST (AI Standards Architect retained; AI Research Scientist retained from 2026-10), METR (MTS Embedded Assessments refetched; MTS Cyberforensics retained), Apollo Research (Lead Research Scientist/Engineer Embedded Evaluations — fresh posting replacing prior requisition), Mistral and Cohere captures retained from 2026-10.
- **Hyperscalers and enterprise responsible-AI** (29 postings combined; 12 new) — Microsoft AI (Software Engineer Health Evaluations NYC, Senior SE Responsible AI CoreAI Mountain View refetched; plus 2026-10 retains for MAI Superintelligence Evaluations Engineer, MAI MTS Evaluations Health, MAI MTS Applied AI SE Health London), NVIDIA (Evaluation and ML Systems Engineer AI Safety & Security, Harness and Platform Engineer AI Safety & Security — paired fresh captures), Apple (AIML Sr SWE AI Evaluation Cupertino, AIML ML Engineer Evaluation Responsible AI & Safety Cambridge — first Apple captures this cycle), Databricks (Staff SE Agent Quality), Snowflake (Sr SE Cortex Quality — first Snowflake capture), Oracle (Senior AI Agent Engineer), SAP (Sr AI Engineer Applied AI & Data Validation Sofia refetched), Amazon (SDE Responsible AI refetched), Cisco (Lead ML Engineer AI Defense — first Cisco capture), plus 2026-10 retains for AWS Bedrock, Salesforce AI Trust & Governance + SMTS, ServiceNow Agent Eval Platform + Moveworks, Adobe Firefly IP Guardrails, IBM watsonx.
- **Regulated industries — banks / insurers / pharma / medical devices** (46 postings combined; 15 new) — Starling Bank (Lead Analyst Model Validation, Model Validation Manager — first Starling captures), Handelsbanken (MRM Senior Analyst London — first Handelsbanken capture), Goldman Sachs (AI Model Validation Associate London), Citi (Model Validation Senior Analyst Warsaw — the Wilmington 2nd LOD role 404'd this cycle), Capital One (Principal Associate Data Science MRO refetched, Principal Quantitative Analyst MRO McLean), M&T Bank (Model Risk Senior Analyst Validation AI/Cyber/Technology refreshed), Thomson Reuters (Lead Research Engineer AI Evaluation & Benchmarking Eagan — first TR capture this cycle on direct URL), Commonwealth Bank of Australia (Chapter Lead AI & General Model Validation Sydney — first CBA / APRA capture), Illumina (Sr Staff Engineer Quality Engineering AI & Test Automation — first Illumina capture), GE HealthCare (SQA Lead AI Quality Engineering Waukesha, AI Regulatory Engineer Haifa — paired fresh captures), BBVA (AI Transformation Compliance & Non-Financial Risk Senior Associate NY), Edwards Lifesciences (Principal Scientist AI/ML Irvine — first Edwards capture), plus 2026-10 retains for JPMorgan, Barclays, Morgan Stanley, Deutsche Bank, Wells Fargo, Goldman Sachs Dallas/Warsaw, MetLife, NY Life CVP + Sr Associate, Bank of America, Modicus Prime, Siemens Healthineers, Novartis, AstraZeneca, Santander Madrid.
- **Big Four assurance / vendors / defense / legal regtech / notified bodies / strategy consultants** (36 postings combined; 15 new) — MITRE (Lead AI Assurance Engineer VA — first MITRE capture), Harvey (Trust Engineer refetched on direct URL), Deloitte US (AI Governance & Assurance Strategy Manager, AI Governance Senior Consultant, AI Governance Manager Global Confidentiality & Privacy), EY (Risk Consulting AI Governance Senior Chennai, Senior AI Governance Consultant Katowice refetched), KPMG (Manager SAP AI & Agent Governance, Manager Securing AI LA — first MCP security + AI agent control frameworks capture), KPMG Belgium (Trusted AI Manager Zaventem), Capgemini (Responsibly Adopting Workplace AI Managing Consultant UK — first Capgemini capture), Cognizant (AI Governance Process Lead Burlington NJ — ServiceNow AICT operator shape), ModelOp (AI Enablement Engineer refetched), Deloitte SEA (DRSC Assurance AI Solution Developer Consultant KL), Deloitte Israel (AI Assurance & SOC 2 Consultant Tel Aviv), plus 2026-10 retains for Deloitte SEA A&A AI Assurance, Deloitte US Cyber AI Governance + Agentic AI Healthcare, EY RC Process & Controls AI Governance Manager Noida, PwC Responsible AI + Middle East QA Engineer, KPMG Audit Technology Alliance, Accenture Responsible AI Engineer + S&C Global Network AI, Booz Allen Agentic AI Engineer, BSI AI Auditor AIMS, TÜV UK AIMS Lead Auditor, Credo AI.
- **Enterprise-regulated applied-AI validation** (1 posting) — Carnival Corporation (Engineer, AI Security Posture & Model Validation retained from 2026-10).

### Coverage gaps for the next cycle

Direct WebFetch was again blocked or returned JS-only shells for:

- OpenAI Preparedness / Safety Advisory Group / Model Behavior — openai.com/careers URLs continued to 403 on direct hits; the two OpenAI roles captured this cycle (Frontier Assurance Researcher, Model Policy Manager National Security) were extractable via a16z Portfolio Jobs and workatailab mirrors.
- Meta GenAI Trust & Safety / MSL Research Engineer AI Trust + Privacy Evals — metacareers.com continues to return JS-only shells.
- Governance-vendor Ashby-hosted listings still returning JS shells: Credo AI (other reqs), Holistic AI, Trustible, Monitaur, Fairly AI, Anch AI, Modulos. Harvey, ModelOp, and Cognizant's ServiceNow AICT role were the three extractable this cycle.
- Notified bodies — BSI Group GQA Certification & Regulatory Lead AI (Workday JS shell blocked verbatim bullets); TÜV SÜD / DEKRA / DNV / UL Solutions / SGS / Intertek / Bureau Veritas direct AI auditor postings did not surface in-window.
- Legal-regtech beyond Harvey + Thomson Reuters — LexisNexis AI Evaluation and Robin AI Trust still LinkedIn-auth only.
- Lloyds Banking Group — Workday error 1007 on two in-window Market & AI Modelling Independent Validation Manager pages; UBS / HSBC / Credit Agricole dedicated AI validation roles did not surface in-window.
- AIG, Prudential, Progressive, Allianz, AXA dedicated AI governance validation — NY Life Senior Associate / MetLife AI Model Risk Analyst / Pfizer Director AI / Humana AVP Model & AI Governance were all closed or MD/ED-tier.

None of these gaps changes the shape of the curriculum this cycle — the sampled segments already cover every module theme and the deferred segments would only add reinforcing evidence to the same requirement clusters, not new ones.

### In-window vs. extended-window postings

Strict 90-day window (2026-08-05 onward): 128 of the 178 postings. Forty-four additional postings fall between 2026-05-05 and 2026-08-04 and are retained because they are the closest published exemplars of specific title / employer combinations (Anthropic RSP PM 2026-07-14, DeepMind Frontier Safety Mitigations 2026-07-30 initial post, DeepMind Senior Research Scientist Gemini Release Evaluations 2026-08-14 just inside the strict window, UK AISI EOI Cyber & Autonomous Systems 2026-07-30, NVIDIA Evaluation and ML Systems Engineer AI Safety & Security 2026-07-26). Six further postings are flagged as older than the extended window and retained as historical calibration (post-frontier-02 Anthropic Frontier Red Team RSP 2026-01-30, post-frontier-03 Anthropic Frontier Red Team RSP 2025-08-03, post-frontier-08 Anthropic Research Engineer Model Evaluations 2026-01-30, post-frontier-21 US CAISI AI Research Scientist 2025-12-19, post-frontier-46 CAISI AI Standards Architect 2026-02-03, post-hyperscaler-17 IBM watsonx staffing 2026-01-01).

## Methodology

1. Refreshed the four-agent fan-out (frontier labs + independents, hyperscalers + enterprise RAI, regulated industries, Big Four + vendors + defense T&E + legal regtech + notified bodies). Each agent WebSearched and WebFetched real posting URLs; agents were instructed never to fabricate.
2. Normalized the 57 new postings into `.aicg/job-requirements.json → postings` alongside the 121 retained from 2026-10, using the same schema — employer, title, URL, `source_type` (direct/aggregator/mirror), `date_observed`, `date_posted`, location, `salary_range` (verbatim or null), `role_fit` (core/borderline), verbatim required and preferred bullets, a representative quote, and a closed-vocabulary `requirement_tags` array mapped 1:1 to the existing 12-module curriculum.
3. Re-scored per-requirement frequencies (`.aicg/job-requirements.json → requirement_tag_frequencies`) against the combined 178-posting sample and refreshed `evidence_post_ids` for each of the 12 owned-requirement blocks.
4. Applied the continuity-bias rule for the delta: an addition is proposed only when (a) ≥ 3 distinct in-window postings cite a requirement not covered by the existing curriculum, (b) frequency ≥ 30% across the full sample, and (c) no existing module can be incrementally extended. **No item cleared all three bars this cycle.** The strongest watchlist candidate — agentic-system evaluation as a distinct assurance surface — stayed above the 30% bar at 0.37 (65/178, up from 0.35) but the required exercise was already added in 2026-10 (`mod-108 / exercise-06-agentic-release-gate-and-trajectory-evidence`); the sustained frequency validates that decision, no further addition is warranted. Four secondary candidates (governance-platform-operator shape, MCP / agent-security tier-permission scoping, bundled AI + Cyber + Technology validation surface, clinical-AI release-gate FDA GMLP + EU MDR dual-regulator vocabulary) each clear (a) with ≥ 3 citations but fail (b) at 0.05–0.09 full-sample and are absorbable into existing modules.
5. Applied the ownership rule — no requirement was demoted or re-assigned. Every backfilled requirement retained clear posting evidence in the AI Evaluation Engineer band (not the level-30 peer methodology tracks and not the level-15 analyst track).

## Requirement themes → curriculum ownership → posting evidence

`Freq` = fraction of the 178 combined postings whose `requirement_tags` include the tag. `Owner` is per the ownership rule in [`.aicg/job-requirements.json → ownership_rule`](.aicg/job-requirements.json).

| # | Theme | Freq | Owner role | Coverage |
|---|---|---|---|---|
| 1 | Release-assurance position: ladder placement, values baseline, deferral map | 0.70 | `ai-evaluation-engineer` (this) | [`mod-101-release-assurance-position`](lessons/mod-101-release-assurance-position) |
| 2 | Assurance-case engineering (GSN, CAE, SACM) for AI evaluation evidence | 0.19 | `ai-evaluation-engineer` | [`mod-102-assurance-case-engineering`](lessons/mod-102-assurance-case-engineering) |
| 3 | Release-gate architecture for AI products and platforms | 0.53 | `ai-evaluation-engineer` | [`mod-103-release-gate-architecture`](lessons/mod-103-release-gate-architecture) |
| 4 | Evaluation evidence pipeline: immutable logs, lineage, ML-BOM, signed release-gate outputs | 0.72 | `ai-evaluation-engineer` | [`mod-104-evaluation-evidence-pipeline`](lessons/mod-104-evaluation-evidence-pipeline) |
| 5 | Model / system / dataset cards for regulatory & third-party audiences | 0.05 | `ai-evaluation-engineer` | [`mod-105-cards-for-external-audiences`](lessons/mod-105-cards-for-external-audiences) |
| 6 | Cross-jurisdictional evaluation-obligation mapping (EU AI Act / NIST AI RMF / ISO 42001 / sector rules) | 0.25 | `ai-evaluation-engineer` | [`mod-106-cross-jurisdictional-obligation-mapping`](lessons/mod-106-cross-jurisdictional-obligation-mapping) |
| 7 | Sector-regulated assurance shape (SR 11-7 / OCC / SR 23-4 / FDA GMLP / PCCP / DORA / APRA CPS / PRA SS1/23) | 0.40 | `ai-evaluation-engineer` | [`mod-107-sector-regulated-assurance`](lessons/mod-107-sector-regulated-assurance) |
| 8 | Deployment-tier gating (RSP / Preparedness / DeepMind FSF shape adapted to enterprise) | 0.19 | `ai-evaluation-engineer` | [`mod-108-deployment-tier-gating`](lessons/mod-108-deployment-tier-gating) |
| 8a | Agentic release-gate: trajectory evidence, tool-call boundaries, multi-turn simulation thresholds | 0.37 | `ai-evaluation-engineer` | [`mod-108 / exercise-06-agentic-release-gate-and-trajectory-evidence`](lessons/mod-108-deployment-tier-gating) (added 2026-10) |
| 9 | Third-party evaluator and auditor interface (AISI / notified bodies / Big Four / independent audits) | 0.22 | `ai-evaluation-engineer` | [`mod-109-third-party-evaluator-and-auditor-interface`](lessons/mod-109-third-party-evaluator-and-auditor-interface) |
| 10 | Post-market surveillance and continuous assurance (EU AI Act Art. 72, FDA PCCP, incident-DB feedback) | 0.13 | `ai-evaluation-engineer` | [`mod-110-post-market-surveillance`](lessons/mod-110-post-market-surveillance) |
| 11 | GenAI / GPAI systemic-risk assurance (EU AI Act Art. 55, GPAI Code, RSP / Preparedness / FSF interface) | 0.08 | `ai-evaluation-engineer` | [`mod-111-gpai-systemic-risk-assurance`](lessons/mod-111-gpai-systemic-risk-assurance) |
| 12 | Owning an enterprise AI-evaluation-assurance program | 0.60 | `ai-evaluation-engineer` | [`mod-112-owning-an-assurance-program`](lessons/mod-112-owning-an-assurance-program) |
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

- **`evidence-pipeline` (0.72)** and **`release-assurance-position` (0.70)** remain the two dominant themes across the combined 178-posting sample — a release-assurance-methodology owner is fundamentally in the business of packaging evidence and holding the ladder position between technical producers and external audiences. The 12-module curriculum's centre-of-mass sits exactly there ([mod-101](lessons/mod-101-release-assurance-position) + [mod-104](lessons/mod-104-evaluation-evidence-pipeline)). Minor drift from last cycle (0.74 / 0.75) is noise from the new sample tilting slightly more toward release-gate + assurance-program-ownership.
- **`assurance-program-ownership` (0.60)** and **`release-gate` (0.53)** stayed in the dominant band. New captures reinforce: Illumina Senior Staff QE AI "create the evaluation framework that gates every agent release: golden datasets, LLM-as-judge scoring, red teaming, tool-call correctness, safety and cost checks" is the single most literal release-gate line in the 178-posting sample; MITRE Lead AI Assurance Engineer "assessing systems for security, reliability, risk, compliance, responsible use, and/or mission suitability"; Deloitte AI Governance & Assurance Strategy Manager with ISO/IEC 42001 + 27001 + 9001 Lead Auditor scope; Capgemini Managing Consultant UK "AI governance frameworks, controls, operating models, three lines of defence, auditable processes".
- **`sector-regulated` (0.40)** stayed stable. The regulated-finance sample broadens to UK PRA SS1/23 (Starling + Handelsbanken) and APRA CPS 230/234 (CommBank Chapter Lead) alongside the US SR 11-7 anchor; regulated-pharma broadens to Class II/III medical device + SaMD (Illumina, GE HealthCare x 2, Edwards Lifesciences, Siemens Healthineers retained) with explicit FDA GMLP + EU MDR dual-regulator vocabulary.
- **`agentic-assurance` (0.37)** sustained above the 30% bar (up slightly from 0.35). The 2026-10 cycle added `mod-108 / exercise-06-agentic-release-gate-and-trajectory-evidence` in response to the crossing; this cycle validates that the frequency is holding and that the exercise is the correct response. New captures: Microsoft MAI Health "informs launch/no-launch decisions for clinical features", Microsoft CoreAI RAI "Agent governance and control-plane capabilities", KPMG Securing AI "MCP (Model Context Protocol) security, AI agent security, agentic AI control frameworks", KPMG SAP AI "least privilege, role-based access, delegated authority, segregation of duties", Illumina "evaluation framework that gates every agent release ... tool-call correctness", Handelsbanken "Agentic AI solutions and third-party AI-enabled applications".
- **`cross-jurisdictional` (0.25)** ticked up from 0.22 as the Big-Four + hyperscaler + regulated-pharma sample added explicit EU AI Act + NIST AI RMF + ISO 42001 + FDA GMLP + EU MDR language. Anthropic Policy PM Safeguards Regulatory ("obligations under AI safety laws globally") and GE HealthCare AI Regulatory Engineer (FDA + EU MDR verbatim) are the strongest in-sample exemplars.
- **`deployment-tier` (0.19)** continued the drift down (0.21 → 0.19) because new postings tagged release-gate / assurance-program-ownership more heavily than naming 'tier' explicitly. Mod-108 remains well-calibrated; the agentic-tier addition from 2026-10 (exercise-06) absorbs the tier-permission-scoping growth.
- **`assurance-case` (0.19)**, **`post-market` (0.13)**, **`gpai` (0.08)**, **`model-cards` (0.05)** stayed low. All four remain retained because: (a) each has ≥ 3 posting citations in-sample, (b) each is a documented differentiator against the level-30 peer tracks, and (c) the under-naming phenomenon continues to hide these themes under other vocabulary (validators call cards "validation report", frontier labs call them "system card", regulators call them "technical documentation", GPAI tiers surface as "AI safety laws globally" or "systemic risk domains" without the EU AI Act Art. 55 verbatim call-out).

## Ownership decisions this cycle

No requirement was demoted or moved. Every owned requirement kept its module. No new requirement cleared the continuity-bias bar. **Zero additions proposed this cycle.** The strongest watchlist candidate — agentic-system evaluation — stayed above 30% at 0.37 but the response (`mod-108 / exercise-06`) was already added in 2026-10, so no further addition is warranted. The four secondary candidates considered this cycle — and the reason each was rejected — are documented in full in [`.aicg/curriculum-plan-delta.json → continuity_bias_audit.candidates_considered`](.aicg/curriculum-plan-delta.json), summarised here:

1. **Agentic-assurance (sustained above 30%)** — 65/178 postings (0.37, up from 0.35). The 2026-10 cycle added `exercise-06-agentic-release-gate-and-trajectory-evidence` to [`mod-108`](lessons/mod-108-deployment-tier-gating); this cycle validates the response — frequency is holding, and the exercise's scope (ARGA composition, trajectory-evidence intake clause, tool-call + action-boundary attestation thresholds, multi-turn simulation thresholds, autonomy / tool-permission escalation) absorbs the growth. **No further addition warranted this cycle.** Watchlist trigger for next cycle: if frequency rises to ≥ 0.50 across the full sample, revisit whether the exercise should split into (a) agent-tier gating and (b) MCP / agent-security tier-permission scoping as sibling exercises inside mod-108.
2. **Governance-platform-operator shape (Credo AI / ModelOp / Fiddler / ServiceNow AICT customer-tenant configuration)** — 7 postings (ModelOp AI Enablement x2 across cycles, Harvey Trust x2, Cognizant AI Governance Process Lead with ServiceNow AICT, Deloitte Cyber, Credo AI Senior AI Engineer AI Systems India). Full-sample frequency 4%. Up from 5 postings last cycle, but still absorbable into [`mod-112`](lessons/mod-112-owning-an-assurance-program) (vendor build-vs-buy) and [`mod-109`](lessons/mod-109-third-party-evaluator-and-auditor-interface) (customer-tenant configuration is the operator's version of the third-party interface). No addition warranted.
3. **MCP / agent-security tier-permission scoping (RBAC on agents, delegated authority, segregation of duties for agent toolchains)** — 4 postings (KPMG Manager Securing AI LA with explicit "MCP (Model Context Protocol) security, AI agent security, agentic AI control frameworks" verbatim; KPMG Manager SAP AI & Agent Governance with "least privilege, role-based access, delegated authority, segregation of duties"; Microsoft CoreAI RAI "Agent governance and control-plane capabilities"; Cisco Lead ML Engineer AI Defense "prompt injection, agent misuse, and data exfiltration"). Full-sample frequency 2%. Absorbable into [`mod-108 / exercise-06`](lessons/mod-108-deployment-tier-gating) which already names "tool allow-list" and "autonomy / tool-permission tiers" in its scope. Documented for next-cycle revisit if the specific MCP-security framing grows further.
4. **Bundled AI + Cyber + Technology validation surface (unified 2nd-line validator remit spanning statistical / ML / LLM / cyber-detection / tech models)** — 4 postings (M&T Bank Model Risk Senior Analyst — Validation AI/Cyber/Technology re-posted this cycle, Deutsche Bank London Model Validation Specialist retained, Deloitte AI Security Engineer Manager retained, Illumina Senior Staff QE AI & Test Automation with GxP + SOX overlap). Full-sample frequency 2%. Clears the 3-posting bar but frequency stays low and the bundle shape fits inside [`mod-107`](lessons/mod-107-sector-regulated-assurance) as a sector-overlay specialisation. If next cycle shows the bundle spreading across other banks (HSBC / UBS / Lloyds / Credit Agricole), fold into mod-107 as a sector-overlay exercise — not a new module.
5. **Clinical-AI release-gate FDA GMLP + EU MDR dual-regulator vocabulary** — 5 postings (Microsoft MAI Health NYC verbatim "FDA guidance on AI-enabled devices and predetermined change-control plans, EU AI Act", GE HealthCare SQA Lead + AI Regulatory Engineer paired, Illumina GxP + medical device, Edwards Lifesciences SaMD partner-with-AI-Evaluation, Siemens Healthineers STED retained). Full-sample frequency 3%. Clears the 3-posting bar but the module ownership stays squarely in [`mod-107`](lessons/mod-107-sector-regulated-assurance) (FDA GMLP + PCCP + EU MDR covered as a sector overlay). If next cycle shows the dual-regulator vocabulary growing above 0.10, fold into mod-107 as an exercise on clinical-AI release-gate composition rather than a new module.

## Posting evidence — summary table

The 121-posting roster from 2026-10 is retained verbatim below; the 57 new 2026-11 captures are appended at the end of the table under the `2026-11 refresh` separator.

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
| post-frontier-10 | Anthropic | Research Engineer, Frontier Red Team (Autonomy) | San Francisco, CA | 2026-08 (observed) | $320,000 – $850,000 USD | borderline | frontier-lab |
| post-frontier-11 | Anthropic | Research Engineer, Frontier Red Team (Hardware Lead) | San Francisco, CA | 2026-08 (observed) | $850,000 USD | borderline | frontier-lab |
| post-frontier-12 | Anthropic | Safeguards Enforcement Analyst, Safety Evaluations | US Remote / SF / DC / NY | 2026-08 (observed) | $230,000 – $270,000 USD | core | frontier-lab |
| post-frontier-13 | Anthropic | Safeguards Enforcement Analyst, Integrity & Authenticity | US Remote / SF / NY / DC | 2026-08 (observed) | $285,000 – $330,000 USD | borderline | frontier-lab |
| post-frontier-14 | Anthropic | Technical Policy Lead, Government & Third-Party Safety Partnerships | SF / DC / London | 2026-08 (observed) | $230,000 – $265,000 USD | core | frontier-lab |
| post-frontier-15 | UK AI Security Institute | Software Engineer — Core Technology | London | 2026-08 (observed) | £65,000 – £145,000 | core | independent-evaluator |
| post-frontier-16 | UK AI Security Institute | EOI — Next-generation Agentic Controls and Forensics | London (+5 UK cities) | 2026-08-31 | £65,000 – £145,000 | borderline | independent-evaluator |
| post-frontier-17 | Google DeepMind | Data Scientist, Responsible Development and Innovation | New York, NY | 2026-08 (observed) | $166,000 – $244,000 USD | core | hyperscaler |
| post-frontier-18 | Google DeepMind | Senior Technical Program Manager, AI Safety | Mountain View, CA | 2026-08 (observed) | $183,000 – $271,000 USD | borderline | hyperscaler |
| post-frontier-19 | METR | Member of Technical Staff, Embedded Assessments | Berkeley, CA (implied) | 2026-08-31 | not disclosed | core | independent-evaluator |
| post-frontier-20 | METR | Member of Technical Staff, Cyberforensics | Berkeley, CA (implied) | 2026-08-31 | not disclosed | borderline | independent-evaluator |
| post-frontier-21 | US CAISI at NIST | AI Research Scientist (IT Specialist AI ZP-2210-IV/V) | Washington, DC / San Francisco | 2025-12-19 | $120,579 – $195,200 USD | core | independent-evaluator |
| post-hyperscaler-01 | Google DeepMind | Research Engineering Manager, Responsibility & Safety Evaluations | London | estimate:2026-05 | not disclosed | core | hyperscaler |
| post-hyperscaler-02 | Anthropic | Staff+ Software Engineer, Safeguards Evals | SF / NY | estimate:2026-06 | $320,000 – $485,000 USD | core | frontier-lab |
| post-hyperscaler-03 | Anthropic | Research Engineer (Senior Staff+), Safeguards Labs | SF / NY | estimate:2026-06 | $350,000 – $850,000 USD | borderline | frontier-lab |
| post-hyperscaler-04 | Microsoft AI | Member of Technical Staff, Evaluations Engineer (MAI Superintelligence) | Multiple US | estimate:2026-07 | $142,800 – $331,200 USD | core | hyperscaler |
| post-hyperscaler-05 | Amazon Web Services | Sr Data Scientist, WWSO Bedrock | East Palo Alto / NY / Austin / Arlington / Seattle | estimate:2026-06 | $159,200 – $247,600 USD | borderline | hyperscaler |
| post-hyperscaler-06 | Amazon (Responsible AI) | SDE, Responsible AI | Seattle | estimate:2026-07 | $143,700 – $194,400 USD | core | hyperscaler |
| post-hyperscaler-07 | Salesforce | Lead Engineer - AI Trust & Governance | SF / Seattle / Chicago / PA / NY / Bellevue | estimate:2026-06 | not disclosed | core | hyperscaler |
| post-hyperscaler-08 | SAP | AI Engineer - Applied AI & Data Validation | Sofia, Bulgaria | 2026-07-22 | not disclosed | borderline | hyperscaler |
| post-hyperscaler-09 | Google DeepMind | Research Engineer - Assurance Evaluation | London | estimate:2026-05 | not disclosed | core | hyperscaler |
| post-hyperscaler-10 | Microsoft | Senior Software Engineer - Responsible AI (CoreAI) | Mountain View, CA | 2026-04-28 | $119,800 – $274,800 USD | core | hyperscaler |
| post-hyperscaler-11 | Microsoft AI | Member of Technical Staff — AI Evaluations, Health (MAI) | New York, NY | 2026-08 (observed) | $119,800 – $304,200 USD | core | hyperscaler |
| post-hyperscaler-12 | Microsoft AI | Member of Technical Staff — Applied AI SE, Health | London, UK | 2026-08 (observed) | £93,500 – £161,800 | core | hyperscaler |
| post-hyperscaler-13 | SAP | Senior AI Engineer - Applied AI & Data Validation | Sofia, Bulgaria | 2026-08-20 | not disclosed | borderline | hyperscaler |
| post-hyperscaler-14 | ServiceNow (Moveworks) | Staff Software Engineer, Agent Eval Platform | Santa Clara, CA | 2026-08-20 | not disclosed | borderline | hyperscaler |
| post-hyperscaler-15 | Adobe | Senior AI Evaluation Specialist — IP Guardrails and Agentic Workflows | San Jose, CA | 2026-08 (observed) | not disclosed | core | hyperscaler |
| post-hyperscaler-16 | Salesforce | Senior AI/ML Engineer - SMTS | Redwood City, CA | 2026-08 (observed) | not disclosed | core | hyperscaler |
| post-hyperscaler-17 | IBM (via Experis staffing) | Senior IBM AI/ML Engineer (watsonx.data intelligence / governance) | Philadelphia, PA — US Remote | 2026-01-01 | Depending on Experience | borderline | hyperscaler |
| post-audit-01 | Deloitte (SEA) | A&A - SG - AI Assurance (Consultant / Sr Consultant) | Singapore | 2026-07-19 | not disclosed | core | big-four |
| post-audit-02 | EY | Senior AI Engineer, Data Analytics Assurance | not specified | 2026-07-30 | competitive | borderline | big-four |
| post-audit-03 | PwC | Responsible AI Senior Associate | New York / Boston / Florham Park / Dallas / Philadelphia / Houston | estimate:2026-07 | $77,000 – $202,000 | borderline | big-four |
| post-audit-04 | Booz Allen Hamilton | AI Engineer (R0244899) | Washington, DC | estimate:2026-07 | $99,000 – $225,000 | borderline | big-four |
| post-audit-05 | Carnival Corporation | Engineer, AI Security Posture & Model Validation | Miami, FL | 2026-07-21 | not disclosed | core | enterprise-regulated |
| post-audit-06 | Accenture | Responsible AI Engineer (R00329071) | Multiple US | estimate:2026-06 | $68,300 – $220,400 | core | big-four |
| post-audit-07 | EY | RC Process & Controls — AI Governance Manager | Noida, India | 2026-08-19 | not disclosed | core | big-four |
| post-audit-08 | Deloitte US | Cyber AI Governance and Privacy Consultant | 51 US locations | 2026-08 (observed) | $82,600 – $162,800 | core | big-four |
| post-audit-09 | Deloitte US | Agentic AI Engineer — Healthcare AI | 40 US locations | 2026-08 (observed) | $110,700 – $372,900 | borderline | big-four |
| post-audit-10 | PwC Middle East | AI Software Quality Assurance Engineer - Manager | Amman, JO | 2026-08-28 | not disclosed | borderline | big-four |
| post-audit-11 | Accenture | S&C Global Network AI, Responsible AI, Sr Analyst | Bengaluru, India | 2026-03-05 | not disclosed | core | big-four |
| post-audit-12 | Harvey AI | Trust Engineer | San Francisco, CA | 2026-06-23 | $220,000 – $330,000 USD | core | legal-regtech |
| post-audit-13 | ModelOp | AI Enablement Engineer | Utah / Chicago / Remote | 2026-08 (observed) | not disclosed | core | governance-vendor |
| post-audit-14 | KPMG LLP | AI Engineer - Senior Associate (Audit Technology Alliance) | Dallas / Montvale / NY / Orlando / Philadelphia / DC | 2026-08 (observed) | not disclosed | borderline | big-four |
| post-audit-15 | BSI Group | AI Auditor (AIMS – ISO/IEC 42001) | Japan / China (home-based; 40% field travel) | 2026-08 (observed) | not disclosed | core | notified-body |
| post-audit-16 | Deloitte SEA (retained duplicate reference) | see post-audit-01 | Singapore | 2026-07-19 | see post-audit-01 | core | big-four |
| post-regulated-01 | Deutsche Bank | AI/ML Model Validation Analyst | Mumbai | estimate:2026 | not disclosed | core | regulated-finance |
| post-regulated-02 | Barclays | AVP ML and GenAI Model Validation | Noida, India | 2026-04-18 | not disclosed | core | regulated-finance |
| post-regulated-03 | Morgan Stanley | Generative AI - Model Risk Management Associate | Budapest / Baltimore | estimate:2026 | $80,000 – $115,000 (Baltimore) | core | regulated-finance |
| post-regulated-04 | M&T Bank | Model Risk Senior Analyst - Validation (AI, Cyber, Technology) | Buffalo, NY | estimate:2026 | $103,000 – $171,600 USD | core | regulated-finance |
| post-regulated-05 | MetLife | AI Model Risk Analyst | New York, NY | estimate:2026-05 | $105,000 – $150,000 USD | core | regulated-insurance |
| post-regulated-06 | New York Life | Sr Associate - Model Validation and AI Governance | New York, NY | estimate:2026 | $124,000 – $177,000 USD | core | regulated-insurance |
| post-regulated-07 | Citi | Model Validation 2nd LOD Sr. Analyst - C12 | Tampa, FL | 2026-06-24 | $117,650 – $130,920 USD | borderline | regulated-finance |
| post-regulated-08 | JPMorgan Chase | Model Risk Analyst (MRGR) | Bengaluru | estimate:2026 | not disclosed | core | regulated-finance |
| post-regulated-09 | Modicus Prime (J&J JLABS) | AI Evaluation Engineer | US (Austin preferred) | 2026-02-08 | equity + cash mix | core | regulated-healthcare |
| post-regulated-10 | Bank of America | Sr Audit Manager - AI Model Risk | Remote | estimate:2026 | not disclosed | borderline | regulated-finance |
| post-regulated-11 | Wells Fargo | Quant Model Risk Validation Senior Manager — NLP / GenAI Models | Irving, TX (+6 US) | 2026-08 (observed) | $185,000 – $300,000 USD | core | regulated-finance |
| post-regulated-12 | Goldman Sachs | Model Risk Management, AI Risk, Analyst/Associate | Dallas, TX | 2026-08 (observed) | not disclosed | core | regulated-finance |
| post-regulated-13 | Capital One | Principal Associate, Data Science - Model Risk Office | McLean / Plano / Chicago / NY | 2026-06-08 | $147,100 – $201,400 USD | core | regulated-finance |
| post-regulated-14 | JPMorganChase | Internal Audit AI Model Risk — Associate | France (Hybrid) | 2026-08 (observed) | not disclosed | core | regulated-finance |
| post-regulated-15 | Siemens Healthineers | Project Quality Engineer — AI Process Specialist | Bangalore, India | 2026-08-10 | not disclosed | core | regulated-healthcare |
| post-regulated-16 | Goldman Sachs | Risk, Model Risk, Associate | Warsaw, Poland | 2026-08 (observed) | not disclosed | core | regulated-finance |
| post-regulated-17 | Deutsche Bank | Model Validation Specialist | London, UK | 2026-08 (observed) | not disclosed | borderline | regulated-finance |
| post-regulated-18 | JPMorganChase | Software Engineer 1 (MRGR tooling) | Mumbai, India | 2026-08 (observed) | not disclosed | borderline | regulated-finance |
| ────── | ──────── 2026-11 refresh — 57 new postings on top of the 121 above ──────── | | | | | | |
| post-frontier-34 | Anthropic | Policy Program Manager, Safeguards Regulatory | San Francisco, CA | 2026-10-19 | $245,000 - $285,000 USD | core | frontier-lab |
| post-frontier-35 | Anthropic | Research Engineer, Post-Training Model Evaluations | SF / Seattle | 2026-10-21 | $500,000 - $850,000 USD | core | frontier-lab |
| post-frontier-36 | Anthropic | Program Manager, Responsible Scaling Policy (refetch) | New York, NY | 2026-07-14 | $190,000 - $235,000 USD | core | frontier-lab |
| post-frontier-37 | Anthropic | Technical Program Manager, Safeguards (Infra & Evals) | SF / NY / Seattle | 2026-11 (observed) | $290,000 - $365,000 USD | core | frontier-lab |
| post-frontier-38 | Anthropic | Safeguards Enforcement Analyst, Safety Evaluations (refetch) | New York, NY | 2026-11 (observed) | $230,000 - $270,000 USD | core | frontier-lab |
| post-frontier-39 | Anthropic | Research Engineer, Frontier Red Team (RSP Evaluations) (refetch) | SF / Seattle | 2026-11 (observed) | $280,000 - $340,000 USD | core | frontier-lab |
| post-frontier-40 | OpenAI | Researcher, Safety - Frontier Assurance | San Francisco, CA | 2026-10-13 | $380,000 - $500,000 USD + Equity | core | frontier-lab |
| post-frontier-41 | OpenAI | Model Policy Manager, National Security | SF / DC / US Remote | 2026-10-16 | $207,000 - $335,000 USD | core | frontier-lab |
| post-frontier-42 | Google DeepMind | Senior Research Scientist, Gemini Release Evaluations | Mountain View / NYC / London | 2026-08-14 | $174,000 - $252,000 USD | borderline | frontier-lab |
| post-frontier-43 | Google DeepMind | Research Engineer, Frontier Safety Mitigations (refetch) | Mountain View, CA | 2026-10-12 | $174,000 - $252,000 USD + bonus | borderline | frontier-lab |
| post-frontier-44 | UK AI Security Institute | EOI - Cyber & Autonomous Systems Team | London, UK | 2026-07-30 | £65,000 - £145,000 | core | independent-evaluator |
| post-frontier-45 | UK AI Security Institute | EOI - Core Technology Team | London, UK | 2026-10-08 | £65,000 - £145,000 | borderline | independent-evaluator |
| post-frontier-46 | US CAISI at NIST | AI Standards Architect | SF or Washington, DC | 2026-02-03 | $85,447 - $187,093 USD | core | independent-evaluator |
| post-frontier-47 | METR | MTS, Embedded Assessments (refetch) | Berkeley, CA | 2026-11 (observed) | $402,048 - $687,759 USD | core | independent-evaluator |
| post-frontier-48 | Apollo Research | Lead Research Scientist/Engineer (Embedded Evaluations) | London / SF | 2026-10-30 | $245,000 - $590,000 USD / £160,000 - £395,000 | borderline | independent-evaluator |
| post-hyperscaler-30 | Microsoft AI | Software Engineer, Health Evaluations | New York City, NY | 2026-10-23 | $142,800 - $274,800 USD (US) / $188,000 - $304,200 USD (SF/NYC) | core | hyperscaler |
| post-hyperscaler-31 | Microsoft | Sr SE, Responsible AI - CoreAI (refetch) | Mountain View, CA | 2026-10-12 | $119,800 - $274,800 USD (IC4/IC5) | core | hyperscaler |
| post-hyperscaler-32 | NVIDIA | Evaluation and ML Systems Engineer, AI Safety & Security | Santa Clara, CA | 2026-07-26 | $152,000 - $241,500 USD | core | hyperscaler |
| post-hyperscaler-33 | NVIDIA | Harness and Platform Engineer, AI Safety & Security | United States | 2026-10-21 | $152,000 - $241,500 USD | core | hyperscaler |
| post-hyperscaler-34 | Apple | AIML - Sr SWE - AI, Evaluation | Cupertino, CA | 2026-10-01 | not disclosed | core | hyperscaler |
| post-hyperscaler-35 | Apple | AIML - ML Engineer, Evaluation - Responsible AI & Safety | Cambridge, MA | 2026-10-29 | not disclosed | core | hyperscaler |
| post-hyperscaler-36 | Databricks | Staff Software Engineer, Agent Quality | New York City, NY | 2026-09-21 | $190,000 - $270,000 USD | core | hyperscaler |
| post-hyperscaler-37 | Snowflake | Senior Software Engineer, Cortex Quality | Menlo Park, CA | 2026-10-03 | $200,000 - $270,000 USD + bonus + equity | borderline | hyperscaler |
| post-hyperscaler-38 | Oracle | Senior AI Agent Engineer | United States | 2026-08-12 | $89,200 - $209,500 USD | borderline | hyperscaler |
| post-hyperscaler-39 | SAP | Sr AI Engineer - Applied AI & Data Validation (refetch) | Sofia, Bulgaria | 2026-10-24 | not disclosed | core | hyperscaler |
| post-hyperscaler-40 | Amazon | SDE, Responsible AI (refetch) | Seattle, WA | 2026-11 (observed) | $143,700 - $194,400 USD | borderline | hyperscaler |
| post-hyperscaler-41 | Cisco | Lead ML Engineer, AI Defense (Hybrid) | San Jose, CA | 2026-10-29 | $216,300 - $280,800 USD | borderline | hyperscaler |
| post-regulated-32 | Starling Bank | Lead Analyst - Model Validation | London, UK | 2026-10-15 | not disclosed | core | regulated-finance |
| post-regulated-33 | Starling Bank | Model Validation Manager | London / Manchester / Cardiff, UK | 2026-10-14 | not disclosed | core | regulated-finance |
| post-regulated-34 | Handelsbanken | MRM Senior Analyst | London, UK | 2026-09-03 | Competitive | core | regulated-finance |
| post-regulated-35 | Goldman Sachs | Risk - AI Model Validation - Associate - London | London, UK | 2026-10-21 | not disclosed | core | regulated-finance |
| post-regulated-36 | Citi | Model Validation Senior Analyst | Warsaw, Poland (Hybrid) | 2026-08-21 | PLN 165,020 - 280,980 | core | regulated-finance |
| post-regulated-37 | Capital One | Principal Associate, Data Science - MRO (refetch) | McLean / Plano / Chicago / NYC | 2026-10-06 | $147,100 - $201,400 USD | core | regulated-finance |
| post-regulated-38 | Capital One | Principal Quantitative Analyst - MRO | McLean, VA | 2026-10-13 | $161,800 - $184,600 USD | core | regulated-finance |
| post-regulated-39 | M&T Bank | Model Risk Sr Analyst - Validation (AI, Cyber, Tech) | Wilmington / Buffalo | 2026-09-23 | $113,000 - $189,000 USD | core | regulated-finance |
| post-regulated-40 | Thomson Reuters | Lead Research Engineer - AI Evaluation & Benchmarking | Eagan, Minnesota | 2026-10-30 | not disclosed | core | legal-regtech |
| post-regulated-41 | Commonwealth Bank of Australia | Chapter Lead (EM), AI & General Model Validation | Sydney NSW, Australia | 2026-10-31 | not disclosed | core | regulated-finance |
| post-regulated-42 | Illumina | Senior Staff Engineer, Quality Engineering, AI & Test Automation | San Diego, CA | 2026-10-27 | not disclosed | core | regulated-pharma |
| post-regulated-43 | GE HealthCare | SQA Lead - AI Quality Engineering | Waukesha, Wisconsin | 2026-10-12 | $106,000 - $158,000 USD | core | regulated-pharma |
| post-regulated-44 | GE HealthCare | AI Regulatory Engineer | Haifa, Israel | 2026-10-13 | not disclosed | core | regulated-pharma |
| post-regulated-45 | BBVA | AI Transformation Compliance & Non-Financial Risk Senior Associate | New York, NY | 2026-10-21 | $120,000 - $145,000 USD | borderline | regulated-finance |
| post-regulated-46 | Edwards Lifesciences | Principal Scientist, AI / ML | Irvine, CA | 2026-10-07 | $132,000 - $186,000 USD | borderline | regulated-pharma |
| post-audit-29 | MITRE | Lead AI Assurance Engineer | VA (hybrid) | 2026-10-29 | $174,000 - $261,000 USD | core | defense |
| post-audit-30 | Harvey | Trust Engineer (refetch) | SF / NY | 2026-11 (observed) | $220,000 - $330,000 USD + equity | core | legal-regtech |
| post-audit-31 | Deloitte | AI Governance & Assurance Strategy Manager | Philadelphia + 16 US cities | 2026-09-04 | $161,925 - $269,875 USD | core | big-four |
| post-audit-32 | Deloitte | AI Governance Senior Consultant | 9 US cities East Coast | 2026-11 (observed) | $110,700 - $218,300 USD | core | big-four |
| post-audit-33 | Deloitte | AI Governance Manager (Global Confidentiality & Privacy) | 7 US cities Midwest/South | 2026-10-24 | $85,000 - $156,000 USD | borderline | big-four |
| post-audit-34 | EY | Risk Consulting - AI Governance - Senior | Chennai, India | 2026-10-07 | not disclosed | core | big-four |
| post-audit-35 | EY | Senior AI Governance Consultant (refetch) | Katowice, Poland | 2026-10-31 | not disclosed | core | big-four |
| post-audit-36 | KPMG | Manager, SAP AI & Agent Governance | 14 US cities | 2026-11 (observed) | $114,095 - $268,180 USD (CA) | borderline | big-four |
| post-audit-37 | KPMG | Manager, Securing AI | Los Angeles, CA | 2026-11 (observed) | $114,095 - $268,180 USD (CA) | borderline | big-four |
| post-audit-38 | KPMG Belgium | Trusted AI Manager | Zaventem, Belgium / Remote | 2026-10-24 | not disclosed | borderline | big-four |
| post-audit-39 | Capgemini | Responsibly Adopting Workplace AI - Managing Consultant | 4 UK cities | 2026-10-30 | not disclosed | core | big-four |
| post-audit-40 | Cognizant | AI Governance Process Lead | Burlington, NJ | 2026-10-29 | $100,000 - $117,000 USD | core | governance-vendor |
| post-audit-41 | ModelOp | AI Enablement Engineer (refetch) | Utah / Chicago / Remote | 2026-11 (observed) | not disclosed | core | governance-vendor |
| post-audit-42 | Deloitte SEA | DRSC Assurance - AI Solution Developer - Consultant | Kuala Lumpur, Malaysia | 2026-10-12 | not disclosed | borderline | big-four |
| post-audit-43 | Deloitte Israel | AI Assurance & SOC 2 Consultant | Tel Aviv, Israel | 2026-11 (observed) | not disclosed | core | big-four |

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

Verbatim, cited, no fabrication. Ranges are as published on the posting page or the aggregator that carried it. New entries from 2026-11 are flagged `[new]`.

**Frontier labs (USD, IC-level, mid to senior)** — the ceiling reflects the frontier-lab premium.

- Anthropic Program Manager, Responsible Scaling Policy — $190,000 – $235,000 (refetched this cycle; 2026-10 cycle noted a wider published range elsewhere)
- Anthropic Policy Program Manager, Safeguards Regulatory — $245,000 – $285,000 `[new]`
- Anthropic Research Engineer, Post-Training Model Evaluations — $500,000 – $850,000 `[new]`
- Anthropic Technical Program Manager, Safeguards (Infra & Evals) — $290,000 – $365,000 `[new]`
- Anthropic Research Engineer, Frontier Red Team (RSP Evaluations) — $280,000 – $340,000
- Anthropic Research Engineer, Frontier Red Team (Autonomy / Hardware Lead) — $320,000 – $850,000
- Anthropic Safeguards Enforcement Analyst, Safety Evaluations — $230,000 – $270,000
- Anthropic Safeguards Enforcement Analyst, Integrity & Authenticity — $285,000 – $330,000
- Anthropic Technical Policy Lead, Gov & Third-Party Safety Partnerships — $230,000 – $265,000
- Anthropic Staff+ Software Engineer, Safeguards Evals — $320,000 – $485,000
- Anthropic Research Engineer (Sr Staff+), Safeguards Labs — $350,000 – $850,000
- OpenAI Researcher, Safety - Frontier Assurance — $380,000 – $500,000 + Equity `[new]`
- OpenAI Model Policy Manager, National Security — $207,000 – $335,000 `[new]`
- Google DeepMind Senior Research Scientist, Gemini Release Evaluations — $174,000 – $252,000 `[new]`
- Google DeepMind Research Engineer, Frontier Safety Mitigations — $174,000 – $252,000 + 15% bonus `[new, previously undisclosed]`
- Google DeepMind Research Engineer, Frontier Safety Risk Assessment (London) — $136,000 – $245,000
- Google DeepMind Data Scientist, Responsible Development and Innovation (NYC) — $166,000 – $244,000
- Google DeepMind Senior Technical Program Manager, AI Safety (Mountain View) — $183,000 – $271,000
- METR MTS, Embedded Assessments — $402,048 – $687,759 `[new, previously undisclosed]`
- Apollo Research Lead Research Scientist/Engineer, Embedded Evaluations — $245,000 – $590,000 USD / £160,000 – £395,000 `[new, previously undisclosed]`

**Hyperscalers (USD, US locations)** — leveled bands published in-jurisdiction.

- Microsoft AI Member of Technical Staff, Evaluations Engineer (MAI Superintelligence) — IC5: $142,800 – $274,800 std US / $188,000 – $304,200 SF Bay + NYC; IC6: $165,600 – $296,400 std US / $220,800 – $331,200 SF Bay + NYC
- Microsoft AI Member of Technical Staff — AI Evaluations, Health (NYC) — IC4/IC5 across $119,800 – $304,200
- Microsoft AI Software Engineer, Health Evaluations (NYC) — $142,800 – $274,800 std US / $188,000 – $304,200 SF/NYC `[new]`
- Microsoft AI Member of Technical Staff — Applied AI SE, Health (London) — £93,500 – £161,800
- Microsoft Senior SE Responsible AI (CoreAI) — IC4: $119,800 – $234,700; IC5: $142,800 – $274,800
- NVIDIA Evaluation and ML Systems Engineer, AI Safety & Security — $152,000 – $241,500 `[new]`
- NVIDIA Harness and Platform Engineer, AI Safety & Security — $152,000 – $241,500 `[new]`
- Databricks Staff SE, Agent Quality (NYC) — $190,000 – $270,000 `[new]`
- Snowflake Senior Software Engineer, Cortex Quality — $200,000 – $270,000 + bonus + equity `[new]`
- Oracle Senior AI Agent Engineer — $89,200 – $209,500 `[new]`
- Cisco Lead ML Engineer, AI Defense (San Jose) — $216,300 – $280,800 `[new]`
- Amazon Web Services Sr Data Scientist, WWSO Bedrock — $159,200 – $247,600 (varies by location)
- Amazon (Responsible AI) SDE, Responsible AI — $143,700 – $194,400 (Seattle)

**Regulated industries (USD / local currency, MRM/validation IC-mid)**.

- M&T Bank Model Risk Senior Analyst (bundled AI/Cyber/Technology) — $113,000 – $189,000 `[refreshed]`
- MetLife AI Model Risk Analyst — $105,000 – $150,000 + Annual Bonus
- New York Life Sr Associate Model Validation & AI Governance — $124,000 – $177,000
- Citi Model Validation Senior Analyst (Warsaw) — PLN 165,020 – 280,980 `[new]`
- Wells Fargo Quant Model Risk Validation Senior Manager — NLP/GenAI Models — $185,000 – $300,000
- Capital One Principal Associate, Data Science - MRO — $147,100 – $201,400 (varies by location)
- Capital One Principal Quantitative Analyst - MRO (McLean) — $161,800 – $184,600 `[new]`
- BBVA AI Transformation Compliance & Non-Financial Risk Senior Associate (NY) — $120,000 – $145,000 `[new]`
- Morgan Stanley Generative AI - MRM Associate (Baltimore) — $80,000 – $115,000
- GE HealthCare SQA Lead - AI Quality Engineering (Waukesha) — $106,000 – $158,000 `[new]`
- Edwards Lifesciences Principal Scientist, AI/ML (Irvine) — $132,000 – $186,000 `[new]`

**Big Four / audit / defense / legal regtech (USD, wide bands published across geographies)**.

- PwC Responsible AI Senior Associate — $77,000 – $202,000
- Booz Allen AI Engineer — $99,000 – $225,000
- Accenture Responsible AI Engineer — $68,300 – $220,400 (CA cap)
- Deloitte US Cyber AI Governance and Privacy Consultant — $82,600 – $162,800
- Deloitte US Agentic AI Engineer — Healthcare AI — $110,700 – $372,900
- Deloitte AI Governance & Assurance Strategy Manager — $161,925 – $269,875 `[new]`
- Deloitte AI Governance Senior Consultant (East Coast) — $110,700 – $218,300 `[new]`
- Deloitte AI Governance Manager (Global Confidentiality & Privacy, Midwest/South) — $85,000 – $156,000 `[new]`
- KPMG Manager, SAP AI & Agent Governance — $114,095 – $268,180 (CA) `[new]`
- KPMG Manager, Securing AI (LA) — $114,095 – $268,180 (CA) `[new]`
- MITRE Lead AI Assurance Engineer (VA) — $174,000 – $261,000 `[new]`
- Cognizant AI Governance Process Lead (Burlington, NJ) — $100,000 – $117,000 `[new]`
- Harvey AI Trust Engineer — $220,000 – $330,000 (plus equity) `[refetched]`

**Public-sector independent evaluator (GBP / USD)**.

- UK AI Security Institute — £65,000 – £145,000 (Frontier Research Engineer Security and Software Engineer Core Technology both in the same band)
- US CAISI at NIST — AI Research Scientist — $120,579 – $195,200

Postings that did not publish a salary band remain: Apollo Research Research Scientist/Engineer, Cohere Sr Research Engineer, DeepMind (most European postings), Salesforce Lead Engineer, SAP AI Engineer, Deloitte SEA A&A AI Assurance, EY Sr AI Engineer (competitive), all Deutsche Bank / Barclays / Morgan Stanley (non-Baltimore) / JPMorgan / Bank of America non-US postings, Carnival Corporation, Modicus Prime (equity/cash mix), Siemens Healthineers, KPMG US, BSI Group, ModelOp, Adobe, ServiceNow Moveworks, IBM/Experis staffing.

## Change log

- **2026-11-03** — refresh cycle. 57 new postings normalized on top of the 121 retained from 2026-10 for a combined evidence base of 178. Every owned requirement remains backed with ≥ 3 posting citations. Dominant themes stable at the curriculum's centre-of-mass: evidence-pipeline 0.72, release-assurance-position 0.70, assurance-program-ownership 0.60, release-gate 0.53, sector-regulated 0.40. Agentic-assurance sustained above 30% at 0.37 (up from 0.35) — confirming the 2026-10 decision to add `exercise-06-agentic-release-gate-and-trajectory-evidence` to `mod-108` is still correct; no further addition warranted. Four secondary candidates — governance-platform-operator shape (7 postings, 0.04), MCP/agent-security tier-permission scoping (4 postings, 0.02), bundled AI+Cyber+Technology validation (4 postings, 0.02), clinical-AI release-gate FDA GMLP + EU MDR dual-regulator vocabulary (5 postings, 0.03) — each clears the 3-posting bar but fails the 30% full-sample bar and remains absorbable into existing modules. `.aicg/curriculum-plan-delta.json` proposes **zero additions** this cycle. First OpenAI captures of the live-postings era: OpenAI Researcher Safety - Frontier Assurance and OpenAI Model Policy Manager National Security both extractable via mirrors. First MITRE Lead AI Assurance Engineer, Illumina Senior Staff QE AI, Apple AIML Evaluation (x2), Commonwealth Bank of Australia Chapter Lead, Starling Bank x2, Handelsbanken, Snowflake Cortex Quality, Cisco AI Defense, Capgemini Responsibly Adopting Workplace AI, Cognizant AI Governance Process Lead, Deloitte AI Governance & Assurance Strategy Manager captures as well.
- **2026-10-03** — refresh cycle. 50 new postings on top of the 71 retained from 2026-09 for a combined evidence base of 121. Agentic-assurance crossed the 30% full-sample bar at 0.35 (42 of 121 postings carry the agentic-assurance tag). Per the prior-cycle commitment, `.aicg/curriculum-plan-delta.json` added exactly ONE new exercise inside `mod-108-deployment-tier-gating` — `exercise-06-agentic-release-gate-and-trajectory-evidence` — rather than a new module. Four other secondary candidates failed the 30% bar and were documented in continuity_bias_audit.
- **2026-09-03** — refresh cycle. 37 new postings normalized on top of the 34 retained from 2026-08 for a combined evidence base of 71. Every owned requirement backed with ≥ 3 posting citations; deployment-tier crossed 30% (0.31, up from 0.26), assurance-case grew to 0.29 (up from 0.24), gpai grew to 0.16 (up from 0.09). No requirement demoted; no new requirement cleared the continuity-bias bar. Four candidates closest to warranting new content — agentic-system evaluation (24% full-sample, 55% within hyperscaler segment), fleet-scale workload discovery + regulatory-risk classification (grew 1 → 4 postings), governance-vendor tooling operator (3 postings), notified-body / ISO 42001 auditor engagement (3 postings) — all fail 30% full-sample bar and all are absorbable into existing modules; `.aicg/curriculum-plan-delta.json` proposes zero additions with a rigorous continuity-bias audit. Watchlist trigger set for next cycle: if agentic-assurance full-sample frequency crosses 30%, add ONE exercise inside mod-108.
- **2026-08-03** — live posting cycle. 34 postings sampled across five employer segments. Every owned requirement backed with ≥ 3 posting citations except `gpai` (3) and `model-cards` (4). No requirement demoted, no new requirement cleared the continuity-bias bar. `.aicg/curriculum-plan-delta.json` proposes zero additions this cycle — the expected output per the packet rules when nothing has materially shifted.
- **2026-07-10** — initial bootstrap. Postings deferred; requirements grounded in the authoritative-reference set catalogued in `.aicg/job-requirements.json → authoritative_references`.
