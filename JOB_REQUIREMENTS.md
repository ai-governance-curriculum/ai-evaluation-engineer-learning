# Job Requirements — AI Evaluation Engineer (Governance family)

**Role level:** 35 (deep specialist, AI Governance family — release-assurance methodology owner; peer to `ai-eval-engineer` (level 30, AI Engineering) and `model-evaluation-engineer` (level 30, ML Engineering); peer to `ai-infra-security` (level 35) on the security side; next-up from `ai-risk-engineer` (level 25) and `ai-governance-analyst` (level 15); inherited upward by `senior-ai-governance-architect` (level 50), `head-of-ai-governance` (level 60), `chief-ai-officer` (level 70))
**Track:** `ai-evaluation-engineer-learning`
**Research window:** 2026-06-05 → 2026-09-03 (last 90 days, strict); 2026-03-04 → 2026-09-03 (extended, for role variants whose in-window volume was low)
**Today:** 2026-09-03

This file documents the requirements catalog used to seed and now to validate the AI Evaluation Engineer curriculum. Raw normalized posting data lives in [`.aicg/job-requirements.json`](.aicg/job-requirements.json); the planned curriculum lives in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json); this cycle's proposed additions live in [`.aicg/curriculum-plan-delta.json`](.aicg/curriculum-plan-delta.json).

## Status — refreshed posting sample completed 2026-09-03

**71 postings in the combined evidence base** (37 new this cycle + 34 retained from 2026-08), well above the 25-posting minimum. Every one of the 12 owned requirement themes is backed by ≥ 3 in-window posting citations. No new capability recurred at ≥ 30% full-sample frequency outside the existing 12-module vocabulary, so the additions-empty delta is the expected output this cycle. The strongest candidate, agentic-system evaluation as a distinct assurance surface, has grown from ~18% (2026-08) to ~24% full-sample (~55% within the hyperscaler segment); it clears the 3-posting bar with 11 fresh citations but still fails the 30% full-sample bar the prior cycle committed to as the trigger for an exercise addition inside `mod-108`.

Segments sampled this cycle (see [`.aicg/job-requirements.json → research_status.sourcing_notes`](.aicg/job-requirements.json) for the full breakdown):

- **Frontier labs and independent evaluators** (24 postings combined; 12 new) — Anthropic (RSP PM, Frontier Red Team RSP Evals + Autonomy + Hardware Lead, Safeguards Enforcement Analyst — Safety Evals + Integrity & Authenticity, Technical Policy Lead — Gov & Third-Party Safety Partnerships, Model Evaluations, Safeguards Labs), Google DeepMind (Frontier Safety Risk Assessment, Frontier Safety Mitigations, Assurance Evaluation, Responsibility & Safety Evaluations, Data Scientist — Responsible Development & Innovation, Sr Technical PM AI Safety), UK AI Security Institute (Frontier Research Engineer — Security, Software Engineer — Core Technology, EOI Next-generation Agentic Controls and Forensics), US Center for AI Standards and Innovation at NIST (AI Research Scientist), METR (MTS — Embedded Assessments, MTS — Cyberforensics), Apollo Research (Research Scientist/Engineer — Evaluations), Cohere (Sr Research Engineer — Model Evaluation).
- **Hyperscalers and enterprise responsible-AI** (17 postings combined; 8 new) — Microsoft AI (MAI Superintelligence Evaluations Engineer, MAI MTS AI Evaluations Health, MAI MTS Applied AI SE Health London, Sr SE Responsible AI CoreAI), Amazon Web Services (Sr Data Scientist WWSO Bedrock, SDE Responsible AI), Salesforce (Lead Engineer AI Trust & Governance, Sr AI/ML Engineer SMTS), SAP (AI Engineer + Sr AI Engineer — Applied AI & Data Validation Sofia), ServiceNow (Staff Software Engineer — Agent Eval Platform, Moveworks), Adobe (Sr AI Evaluation Specialist — IP Guardrails and Agentic Workflows), IBM (Sr AI/ML Engineer — watsonx.data intelligence / governance), Google DeepMind (Research Engineering Manager Responsibility & Safety Evaluations).
- **Regulated industries — banks / insurers / pharma / medical devices** (22 postings combined; 8 new) — JPMorganChase (Model Risk Analyst MRGR, Internal Audit AI Model Risk Associate, Software Engineer 1 MRGR Mumbai), Barclays (AVP ML and GenAI Model Validation), Morgan Stanley (GenAI MRM Associate), Deutsche Bank (AI/ML Model Validation Analyst Mumbai, Model Validation Specialist London), Wells Fargo (Quant Model Risk Validation Sr Manager — NLP/GenAI Models), Goldman Sachs (MRM AI Risk Analyst/Associate Dallas, Risk MRM Associate Warsaw), Capital One (Principal Associate Data Science — Model Risk Office), M&T Bank (Model Risk Sr Analyst — Validation AI/Cyber/Technology), MetLife (AI Model Risk Analyst), New York Life (Sr Associate Model Validation & AI Governance), Citi (Model Validation 2nd LOD Sr Analyst C12), Bank of America (Sr Audit Manager AI Model Risk), Modicus Prime / J&J JLABS (AI Evaluation Engineer, GxP pharma), Siemens Healthineers (Project Quality Engineer — AI Process Specialist Bangalore).
- **Big Four assurance / vendors / defense / legal regtech / notified bodies** (21 postings combined; 9 new) — Deloitte SEA (A&A AI Assurance), Deloitte US (Cyber AI Governance & Privacy Consultant, Agentic AI Engineer — Healthcare AI), EY (Sr AI Engineer Data Analytics Assurance, RC Process & Controls AI Governance Manager Noida), PwC (Responsible AI Sr Associate, AI Software QA Engineer Manager Middle East), KPMG (AI Engineer Sr Associate Audit Technology Alliance), Accenture (Responsible AI Engineer, S&C Global Network AI Responsible AI Sr Analyst Bengaluru), Booz Allen Hamilton (AI Engineer defense-adjacent), Harvey (Trust Engineer), ModelOp (AI Enablement Engineer), BSI Group (AI Auditor — AIMS ISO/IEC 42001).
- **Enterprise-regulated applied-AI validation** (1 posting) — Carnival Corporation (Engineer, AI Security Posture & Model Validation).

### Coverage gaps for the next cycle

Direct WebFetch was again blocked or returned JS-only shells for:

- OpenAI Preparedness / Safety Advisory Group / Model Behavior / Model Policy — openai.com/careers URLs returned HTTP 403 (Cloudflare) or empty JS shells on both direct pages and the Ashby mirror.
- Meta GenAI Trust & Safety / GenAI Evaluations — Meta careers still 404s.
- US AI Safety Institute at NIST — the AI Research Scientist announcement was captured via the NIST news page, but USAJOBS deep links continued to time out.
- Governance-vendor Ashby-hosted listings that returned JS-only shells this cycle: Credo AI, Holistic AI, Trustible, Monitaur, Fairly AI, Anch AI, Modulos. Harvey and ModelOp were the only two that yielded fetchable content.
- Databricks / Mosaic AI Governance and NVIDIA Trustworthy AI — the requisitions surfaced via search snippets but the direct careers URLs returned JS-only shells.
- Legal-regtech applied-AI teams beyond Harvey — Thomson Reuters CoCounsel Trust, LexisNexis (Sr Data Scientist III — AI Evaluation & Prompt Engineering surfaced only behind LinkedIn auth), Robin AI.
- Apollo Research and METR Lever URLs 403'd on WebFetch even though the requisitions are publicly listed; titles and one-line descriptions captured from mirrors but verbatim bullets could not be extracted.

None of these gaps changes the shape of the curriculum this cycle — the sampled segments already cover every module theme and the deferred segments would only add reinforcing evidence to the same requirement clusters, not new ones.

### In-window vs. extended-window postings

Strict 90-day window (2026-06-05 onward): 52 of the 71 postings. Fifteen additional postings fall between 2026-03-04 and 2026-06-04 and are retained because they are the closest published exemplars of specific title / employer combinations (Modicus Prime "AI Evaluation Engineer" verbatim title, Barclays AVP ML/GenAI Model Validation, DeepMind Frontier Safety Mitigations, Anthropic Frontier Red Team RSP Evaluations, Anthropic Research Engineer Model Evaluations, Accenture S&C Global Network AI Responsible AI Sr Analyst). Four further postings are flagged as older than the extended window and retained as historical calibration (post-frontier-03 posted 2025-08-03, IBM watsonx staffing requisition posted 2026-01-01, NIST CAISI announcement 2025-12-19).

## Methodology

1. Refreshed the prior cycle's four-agent fan-out (frontier labs + independents, hyperscalers + enterprise RAI, regulated industries, Big Four + vendors + defense T&E + legal regtech + notified bodies). Each agent WebSearched and WebFetched real posting URLs; agents were instructed never to fabricate.
2. Normalized the 37 new postings into `.aicg/job-requirements.json → postings` alongside the 34 retained from 2026-08, using the same schema — employer, title, URL, `source_type` (direct/aggregator), `date_observed`, `date_posted`, location, `salary_range` (verbatim or null), `role_fit` (core/borderline), verbatim required and preferred bullets, a representative quote, and a closed-vocabulary `requirement_tags` array mapped 1:1 to the existing 12-module curriculum.
3. Re-scored per-requirement frequencies (`.aicg/job-requirements.json → requirement_tag_frequencies`) against the combined 71-posting sample and refreshed `evidence_post_ids` for each of the 12 owned-requirement blocks.
4. Applied the continuity-bias rule for the delta: an addition is proposed only when (a) ≥ 3 distinct in-window postings cite a requirement not covered by the existing curriculum, (b) frequency ≥ 30% across the full sample, and (c) no existing module can be incrementally extended. **No item cleared all three bars this cycle.** The candidate that came closest — agentic-system evaluation as a distinct assurance surface — clears (a) decisively with 11 fresh citations but fails (b) at 24% full-sample and fails (c) because mod-104 and mod-108 already thread the theme.
5. Applied the ownership rule — no requirement was demoted or re-assigned. Every backfilled requirement retained clear posting evidence in the AI Evaluation Engineer band (not the level-30 peer methodology tracks and not the level-15 analyst track).

## Requirement themes → curriculum ownership → posting evidence

`Freq` = fraction of the 71 combined postings whose `requirement_tags` include the tag. `Owner` is per the ownership rule in [`.aicg/job-requirements.json → ownership_rule`](.aicg/job-requirements.json).

| # | Theme | Freq | Owner role | Coverage |
|---|---|---|---|---|
| 1 | Release-assurance position: ladder placement, values baseline, deferral map | 0.72 | `ai-evaluation-engineer` (this) | [`mod-101-release-assurance-position`](lessons/mod-101-release-assurance-position) |
| 2 | Assurance-case engineering (GSN, CAE, SACM) for AI evaluation evidence | 0.29 | `ai-evaluation-engineer` | [`mod-102-assurance-case-engineering`](lessons/mod-102-assurance-case-engineering) |
| 3 | Release-gate architecture for AI products and platforms | 0.59 | `ai-evaluation-engineer` | [`mod-103-release-gate-architecture`](lessons/mod-103-release-gate-architecture) |
| 4 | Evaluation evidence pipeline: immutable logs, lineage, ML-BOM, signed release-gate outputs | 0.83 | `ai-evaluation-engineer` | [`mod-104-evaluation-evidence-pipeline`](lessons/mod-104-evaluation-evidence-pipeline) |
| 5 | Model / system / dataset cards for regulatory & third-party audiences | 0.11 | `ai-evaluation-engineer` | [`mod-105-cards-for-external-audiences`](lessons/mod-105-cards-for-external-audiences) |
| 6 | Cross-jurisdictional evaluation-obligation mapping (EU AI Act / NIST AI RMF / ISO 42001 / sector rules) | 0.24 | `ai-evaluation-engineer` | [`mod-106-cross-jurisdictional-obligation-mapping`](lessons/mod-106-cross-jurisdictional-obligation-mapping) |
| 7 | Sector-regulated assurance shape (SR 11-7 / OCC / SR 23-4 / FDA GMLP / PCCP / DORA) | 0.42 | `ai-evaluation-engineer` | [`mod-107-sector-regulated-assurance`](lessons/mod-107-sector-regulated-assurance) |
| 8 | Deployment-tier gating (RSP / Preparedness / DeepMind FSF shape adapted to enterprise) | 0.31 | `ai-evaluation-engineer` | [`mod-108-deployment-tier-gating`](lessons/mod-108-deployment-tier-gating) |
| 9 | Third-party evaluator and auditor interface (AISI / notified bodies / Big Four / independent audits) | 0.23 | `ai-evaluation-engineer` | [`mod-109-third-party-evaluator-and-auditor-interface`](lessons/mod-109-third-party-evaluator-and-auditor-interface) |
| 10 | Post-market surveillance and continuous assurance (EU AI Act Art. 72, FDA PCCP, incident-DB feedback) | 0.21 | `ai-evaluation-engineer` | [`mod-110-post-market-surveillance`](lessons/mod-110-post-market-surveillance) |
| 11 | GenAI / GPAI systemic-risk assurance (EU AI Act Art. 55, GPAI Code, RSP / Preparedness / FSF interface) | 0.16 | `ai-evaluation-engineer` | [`mod-111-gpai-systemic-risk-assurance`](lessons/mod-111-gpai-systemic-risk-assurance) |
| 12 | Owning an enterprise AI-evaluation-assurance program | 0.59 | `ai-evaluation-engineer` | [`mod-112-owning-an-assurance-program`](lessons/mod-112-owning-an-assurance-program) |
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

- **`evidence-pipeline` (0.83)** and **`release-assurance-position` (0.72)** remain the two dominant themes across the combined sample — a release-assurance-methodology owner is fundamentally in the business of packaging evidence and holding the ladder position between technical producers and external audiences. The 12-module curriculum's centre-of-mass sits exactly there ([mod-101](lessons/mod-101-release-assurance-position) + [mod-104](lessons/mod-104-evaluation-evidence-pipeline)).
- **`release-gate` (0.59)** and **`assurance-program-ownership` (0.59)** both grew this cycle (from 0.53 and 0.47) as more hyperscaler and Big-Four postings surfaced with explicit release-gate / program-ownership language (Adobe IP Guardrails "quality gates that generative models must pass before shipping", Deloitte Cyber AI Governance "AI governance operating models, intake workflows, risk tiering, approvals, documentation standards", Salesforce SMTS "evaluation-led benchmarking … to ensure … Customer Trust", Harvey Trust Engineer "reporting layers that translate compliance signals into … risk posture and certification status").
- **`sector-regulated` (0.42)** stayed stable — the regulated-finance sample continues to anchor here (JPMorgan MRGR + Internal Audit, Goldman Sachs MRM AI Risk, Wells Fargo NLP/GenAI Sr Manager, Capital One Data Science MRO, Barclays / M&T / Citi / BofA / MetLife / NY Life / Modicus Prime / Siemens Healthineers).
- **`deployment-tier` (0.31)** crossed 30% this cycle (up from 0.26). Anthropic RSP + Frontier Red Team (Autonomy / Hardware Lead) + Frontier Safety Mitigations + AISI EOI Agentic Controls + METR Embedded Assessments + DeepMind Assurance Evaluation + Microsoft MAI Health + Adobe IP Guardrails + Deloitte Agentic Healthcare all price the tier-gating vocabulary explicitly. This is validation that mod-108's centre-of-mass is well-calibrated; no addition needed because the growth is inside the module's scope.
- **`assurance-case` (0.29)** grew from 0.24 as the Big-Four postings (Deloitte SEA AI Assurance, EY RC-Process AI Governance Manager, EY Sr AI Engineer Data Analytics Assurance, Modicus Prime, Siemens Healthineers) surfaced explicit "prepare clear, structured AI risk and quality reports" / "audit-ready evidence processes" / "certification and surveillance" language.
- **`gpai` (0.16)** grew from 0.09 — DeepMind Data Scientist (ReDI) explicitly names "systemic risk domains identified in the EU AI Act"; Barclays AVP names EU AI Act alongside SR 11-7 as the regulatory backbone; BSI AI Auditor covers ISO/IEC 42001 which is the certification pathway that Art. 55 GPAI providers will lean on; Anthropic RSP and DeepMind Frontier Safety Mitigations remain the frontier-lab anchors. The retention rationale stated last cycle continues to hold: this is a 2026-emerging obligation on trajectory, not an absent one.
- **`model-cards` (0.11)** stayed low. Anthropic RSP PM's "system card reviews" duty persists; the rest of the sample refers to card-adjacent artefacts under other names ("validation report", "release evidence", "handover materials", "audit-ready evidence process"). The module is retained because it is a core differentiator against peer level-30 tracks and because the low posting-frequency reflects diverse naming rather than absent demand.

## Ownership decisions this cycle

No requirement was demoted or moved. Every owned requirement kept its module. No new requirement cleared the continuity-bias bar. Nothing was added. The four candidates that came closest — and the reason each was rejected — are documented in full in [`.aicg/curriculum-plan-delta.json → continuity_bias_audit.candidates_considered`](.aicg/curriculum-plan-delta.json), summarised here:

1. **Agentic-system evaluation as a distinct assurance surface** — 11 fresh postings across all four segments (Anthropic Autonomy / Hardware Lead, MSFT MAI Health, MSFT Applied AI Health, ServiceNow Moveworks Agent Eval Platform, Adobe IP Guardrails, Salesforce SMTS Benchforce, Deloitte Cyber, Deloitte Agentic Healthcare, AISI EOI Agentic Controls, METR Embedded Assessments, Barclays AVP GenAI LangChain). Full-sample frequency 24% (up from 18%); hyperscaler-segment frequency 55%. Passes 3-posting bar decisively but fails 30% full-sample bar. Absorbable into [`mod-108`](lessons/mod-108-deployment-tier-gating) (agentic-tier gating with AgentDojo-style benchmarks is already threaded through) and [`mod-104`](lessons/mod-104-evaluation-evidence-pipeline) (agent trace / trajectory evidence normalisation). **Watchlist trigger set for next cycle: if full-sample frequency crosses 30%, add ONE exercise inside mod-108 per prior-cycle-committed response; do not create a new module.**
2. **Automated fleet-scale AI workload discovery + regulatory-risk classification pipeline** — 4 postings (AWS SDE Responsible AI, IBM watsonx regulation-mapping engine, ModelOp AI Enablement Engineer, Deloitte Cyber AI Governance Consultant). Up from 1 in the prior cycle, so the prior-cycle "if it grows, add exercise in mod-112" trigger is technically hit at the 3-posting bar — but frequency stays at 6% and the theme is a specialisation of coverage already in [`mod-112`](lessons/mod-112-owning-an-assurance-program). Documented for next-cycle revisit.
3. **Governance-vendor tooling operator (Credo AI / ModelOp / Fiddler customer-tenant configuration)** — 3 postings (ModelOp AI Enablement, Deloitte Cyber, Harvey Trust). Frequency 4%. Absorbable into [`mod-112`](lessons/mod-112-owning-an-assurance-program) and [`mod-109`](lessons/mod-109-third-party-evaluator-and-auditor-interface). No addition warranted.
4. **Notified-body / ISO/IEC 42001 external-auditor engagement (Art. 43 conformity assessment pathway)** — 3 postings (BSI AI Auditor JR0016802, Deloitte SEA A&A AI Assurance, EY RC Process Controls AI Governance Manager). Frequency 4%. Absorbable into [`mod-109`](lessons/mod-109-third-party-evaluator-and-auditor-interface), which already covers notified-body engagement for EU AI Act conformity assessment.

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

- Anthropic Program Manager, Responsible Scaling Policy — $190,000 – $285,000 (updated this cycle from prior $190,000 – $235,000)
- Anthropic Research Engineer, Frontier Red Team (RSP Evaluations) — $280,000 – $340,000
- Anthropic Research Engineer, Frontier Red Team (Autonomy / Hardware Lead) — $320,000 – $850,000
- Anthropic Research Engineer, Model Evaluations — $500,000 – $850,000 (updated Greenhouse posting this cycle)
- Anthropic Safeguards Enforcement Analyst, Safety Evaluations — $230,000 – $270,000
- Anthropic Safeguards Enforcement Analyst, Integrity & Authenticity — $285,000 – $330,000
- Anthropic Technical Policy Lead, Gov & Third-Party Safety Partnerships — $230,000 – $265,000
- Anthropic Staff+ Software Engineer, Safeguards Evals — $320,000 – $485,000
- Anthropic Research Engineer (Sr Staff+), Safeguards Labs — $350,000 – $850,000
- Google DeepMind Research Engineer, Frontier Safety Risk Assessment (London) — $136,000 – $245,000
- Google DeepMind Data Scientist, Responsible Development and Innovation (NYC) — $166,000 – $244,000
- Google DeepMind Senior Technical Program Manager, AI Safety (Mountain View) — $183,000 – $271,000

**Hyperscalers (USD, US locations)** — leveled bands published in-jurisdiction.

- Microsoft AI Member of Technical Staff, Evaluations Engineer (MAI Superintelligence) — IC5: $142,800 – $274,800 std US / $188,000 – $304,200 SF Bay + NYC; IC6: $165,600 – $296,400 std US / $220,800 – $331,200 SF Bay + NYC
- Microsoft AI Member of Technical Staff — AI Evaluations, Health (NYC) — IC4/IC5 across $119,800 – $304,200
- Microsoft AI Member of Technical Staff — Applied AI SE, Health (London) — £93,500 – £161,800
- Microsoft Senior SE Responsible AI (CoreAI) — IC4: $119,800 – $234,700; IC5: $142,800 – $274,800
- Amazon Web Services Sr Data Scientist, WWSO Bedrock — $159,200 – $247,600 (varies by location)
- Amazon (Responsible AI) SDE, Responsible AI — $143,700 – $194,400 (Seattle)

**Regulated industries (USD, MRM/validation IC-mid)**.

- M&T Bank Model Risk Senior Analyst — $103,000 – $171,600
- MetLife AI Model Risk Analyst — $105,000 – $150,000 + Annual Bonus
- New York Life Sr Associate Model Validation & AI Governance — $124,000 – $177,000
- Citi Model Validation 2nd LOD Sr Analyst C12 — $117,650 – $130,920
- Wells Fargo Quant Model Risk Validation Senior Manager — NLP/GenAI Models — $185,000 – $300,000
- Capital One Principal Associate, Data Science - MRO — $147,100 – $201,400 (varies by location)
- Morgan Stanley Generative AI - MRM Associate (Baltimore) — $80,000 – $115,000

**Big Four / audit / defense / legal regtech (USD, wide bands published across geographies)**.

- PwC Responsible AI Senior Associate — $77,000 – $202,000
- Booz Allen AI Engineer — $99,000 – $225,000
- Accenture Responsible AI Engineer — $68,300 – $220,400 (CA cap)
- Deloitte US Cyber AI Governance and Privacy Consultant — $82,600 – $162,800
- Deloitte US Agentic AI Engineer — Healthcare AI — $110,700 – $372,900
- Harvey AI Trust Engineer — $220,000 – $330,000 (plus equity)

**Public-sector independent evaluator (GBP / USD)**.

- UK AI Security Institute — £65,000 – £145,000 (Frontier Research Engineer Security and Software Engineer Core Technology both in the same band)
- US CAISI at NIST — AI Research Scientist — $120,579 – $195,200

Postings that did not publish a salary band remain: Apollo Research Research Scientist/Engineer, Cohere Sr Research Engineer, DeepMind (most European postings), Salesforce Lead Engineer, SAP AI Engineer, Deloitte SEA A&A AI Assurance, EY Sr AI Engineer (competitive), all Deutsche Bank / Barclays / Morgan Stanley (non-Baltimore) / JPMorgan / Bank of America non-US postings, Carnival Corporation, Modicus Prime (equity/cash mix), Siemens Healthineers, KPMG US, BSI Group, ModelOp, Adobe, ServiceNow Moveworks, IBM/Experis staffing.

## Change log

- **2026-09-03** — refresh cycle. 37 new postings normalized on top of the 34 retained from 2026-08 for a combined evidence base of 71. Every owned requirement backed with ≥ 3 posting citations; deployment-tier crossed 30% (0.31, up from 0.26), assurance-case grew to 0.29 (up from 0.24), gpai grew to 0.16 (up from 0.09). No requirement demoted; no new requirement cleared the continuity-bias bar. Four candidates closest to warranting new content — agentic-system evaluation (24% full-sample, 55% within hyperscaler segment), fleet-scale workload discovery + regulatory-risk classification (grew 1 → 4 postings), governance-vendor tooling operator (3 postings), notified-body / ISO 42001 auditor engagement (3 postings) — all fail 30% full-sample bar and all are absorbable into existing modules; `.aicg/curriculum-plan-delta.json` proposes zero additions with a rigorous continuity-bias audit. Watchlist trigger set for next cycle: if agentic-assurance full-sample frequency crosses 30%, add ONE exercise inside mod-108.
- **2026-08-03** — live posting cycle. 34 postings sampled across five employer segments. Every owned requirement backed with ≥ 3 posting citations except `gpai` (3) and `model-cards` (4). No requirement demoted, no new requirement cleared the continuity-bias bar. `.aicg/curriculum-plan-delta.json` proposes zero additions this cycle — the expected output per the packet rules when nothing has materially shifted.
- **2026-07-10** — initial bootstrap. Postings deferred; requirements grounded in the authoritative-reference set catalogued in `.aicg/job-requirements.json → authoritative_references`.
