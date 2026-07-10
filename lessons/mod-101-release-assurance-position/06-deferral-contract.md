# The Deferral Contract — Who Owes What to This Program

## Motivation

Chapter `01` placed the release-assurance role on the ladder and named the peers, prerequisites, and higher tracks it interacts with. Chapters `02`–`05` walked the four bodies of literature (NIST AI RMF, ISO/IEC 42001, EU AI Act, values baseline) that shape release-gate obligations.

None of that is actionable until the role's *deferral contract* is written down. A deferral contract says, explicitly, what evidence each peer, prerequisite, and higher track **owes this program** as inputs to the release-gate, and what artefacts this program **owes each of them** as outputs. Without it, the release-gate slides: obligations that a peer should have discharged are reworked by this role (loss of altitude); artefacts that this role should have produced go unclaimed by the higher tracks (loss of authority).

The contract is a *live artefact* — it is edited as team boundaries shift and as new frameworks land. In a running program the contract lives in the assurance program's charter (`mod-112`) and is co-signed by the peer team leads. This chapter drafts the baseline contract; exercise `01` asks you to instantiate it for a real (or realistic) organisation.

## Contract shape

Each contract row is:

| Party (role) | Direction | What they owe | Why the release-gate needs it | Framework citations |
| ------------ | --------- | ------------- | ----------------------------- | ------------------- |

Every row must name a *specific* artefact, not a topic — "harm inventory v3 signed by risk-engineering lead" beats "risk documentation." The framework-citation column pins the row to one or more NIST AI RMF sub-categories, ISO/IEC 42001 clauses, EU AI Act articles, or Values-baseline principles, so an auditor can follow the trail.

## What each party OWES this program (evidence in)

### From `ai-governance-analyst` (prerequisite, level 15)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| System entry in the AI inventory, with intended purpose, deployer / provider classification, and jurisdictional scope | Release-gate scope statement cannot be drafted without this | NIST AI RMF MAP-1.1, MAP-2; ISO 42001 clause 4; EU AI Act Article 6 + Annex III (classification) |
| First-draft NIST AI RMF / ISO 42001 / EU AI Act crosswalk for the system | Release-gate obligation list is elevated from this crosswalk, not authored from scratch | NIST AI RMF GOVERN-1.1; ISO 42001 clause 4 |
| First-draft model / system / dataset cards | Release-gate produces the audience-ready cards in `mod-105`; it does not compose them from blank | ISO 42001 Annex A (information for interested parties); EU AI Act Article 13 |
| Jurisdictional watchlist for the system's markets | Release-gate has to know what has changed since last gate | EU AI Act Article 26 (deployer); Framework Convention procedural principles |
| Interested-parties register | Program's Clause 4 context input | ISO 42001 clause 4.2 |

### From `ai-risk-engineer` (lower peer, level 25)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Harm model / harm inventory for the system, versioned and signed | Release-gate risk-management-system claim depends on this | NIST AI RMF MAP-5; ISO 42001 clause 6.1.2 (risk assessment); EU AI Act Article 9 |
| Red-team / adversarial-ML evaluation report with methodology, coverage, and residuals | Release-gate cybersecurity / robustness claim depends on this | NIST AI RMF MEASURE-2.7; NIST AI 100-2; EU AI Act Article 15 |
| Fairness / bias / disaggregated-performance evidence | Release-gate fairness claim depends on this | NIST AI RMF MEASURE-2.11; EU AI Act Article 10 |
| Guardrail-effectiveness measurements (in-scope and out-of-scope suites) | Release-gate mitigation claim depends on this | NIST AI RMF MANAGE-1.3; EU AI Act Article 9 |
| Incident-response playbook for the system class | Release-gate cannot pass without a tested procedure | EU AI Act Article 61; NIST AI RMF MANAGE-4 |

### From `ai-eval-engineer` (peer, level 30, AI Engineering family)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Trace / trajectory / tool-call evaluation results across the deployment surface | Release-gate operational-behaviour claim depends on this | NIST AI RMF MEASURE-2.1, 2.5; EU AI Act Article 15 |
| Judge-vs-human calibration record (for any judge used in the eval suite) | Release-gate validity claim for judge-derived metrics depends on this | NIST AI RMF MEASURE-4; ISO 42001 Annex A |
| RAG grounding / retrieval-quality evidence, where applicable | Release-gate accuracy claim for RAG systems depends on this | NIST AI RMF MEASURE-2.3; EU AI Act Article 15 |
| Eval-gated CI/CD signal and the drift-detection online-eval slice | Release-gate change-control claim and post-market-monitoring plan depend on this | NIST AI RMF MANAGE-4.1; EU AI Act Article 72 |
| Instrumentation design that satisfies the log-retention requirement | Release-gate record-keeping claim depends on this | EU AI Act Article 12 |

### From `model-evaluation-engineer` (peer, level 30, ML Engineering family)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Statistical framing of each threshold — estimator, confidence interval, sample-size justification | Release-gate MEASURE claims must be statistically defensible | NIST AI RMF MEASURE-1, MEASURE-4 |
| Benchmark-construction record (or citation to a public benchmark plus its provenance) for each metric | Release-gate validity claim depends on the benchmark being fit for purpose | NIST AI RMF MEASURE-1.1; ISO/IEC 25059 |
| Calibration methodology and calibration measurements where the release-gate consumes probability outputs | Release-gate calibration claim | NIST AI RMF MEASURE-2.4 |
| Cross-modality harness evidence where the system is multimodal | Release-gate scope-completeness claim | NIST AI RMF MEASURE-1, MAP-3 |
| Robustness measurement evidence tied to ISO/IEC 24029-2 method | Release-gate robustness claim | ISO/IEC 24029-2; EU AI Act Article 15 |

### From `ai-infra-security` (peer, level 35) and `security-learning` (peer, level 35)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Evaluation-set integrity controls (exfiltration, contamination, tamper-evidence) | Release-gate cannot rely on eval results if the eval set is not integrity-protected | NIST AI RMF MEASURE-4; EU AI Act Article 15 |
| Model supply-chain attestations (SLSA level, provenance, safetensors verification) | Release-gate supply-chain claim | NIST AI RMF GOVERN-6; EU AI Act Article 15 |
| Judge supply-chain attestations (if judge models are third-party) | Release-gate validity claim for judge outputs | NIST AI RMF GOVERN-6.1 |
| Threat-model artefact tied to MITRE ATLAS / OWASP LLM Top 10 | Release-gate cybersecurity claim | NIST AI RMF MEASURE-2.7; EU AI Act Article 15 |

### From `agentic-safety-engineer` (higher peer, level 40)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Frontier-agent capability elicitation results, when the system is agentic and in scope for tier-3 gating | Release-gate deployment-tier claim depends on this | NIST AI RMF MEASURE-2.7; EU AI Act Article 55 |
| Dangerous-capability evaluation results tied to RSP / Preparedness / FSF criteria | Release-gate for GPAI systemic-risk assurance depends on this | EU AI Act Article 55; GPAI Code of Practice |

### From `senior-ai-governance-architect` (higher, level 50)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| The institution's control library (Annex A-shape) that the release-gate references | Release-gate cannot reference controls that do not exist | ISO 42001 clause 6.1.3 (Annex A applicability); Framework Convention |
| Cross-jurisdictional reconciliation of overlapping obligations | Release-gate obligation list is trimmed of duplicates by this reconciliation | NIST AI RMF GOVERN-1.1; EU AI Act; sector rules |
| Policy taxonomy (accepted use / prohibited use / escalation) that the release-gate enforces | Release-gate cannot enforce a policy the institution has not written | ISO 42001 clause 5.2; EU AI Act Article 5 |

### From `head-of-ai-governance` (higher, level 60) and `chief-ai-officer` (higher, level 70)

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Program authorisation and top-management commitment | Program cannot exist without this | ISO 42001 clause 5.1; NIST AI RMF GOVERN-1.1, GOVERN-2 |
| Resource allocation (headcount, tooling, third-party budget) | Program cannot run without this | ISO 42001 clause 7.1 |
| Institution-level risk appetite | Release-gate thresholds are derived from this | NIST AI RMF GOVERN-1.3 |

### From external third parties

| Owes to this program | Why | Frameworks |
| -------------------- | --- | ---------- |
| Third-party evaluator results (AISI-shape, notified body, or Big Four) | Release-gate for systems requiring notified-body involvement or independent evaluation depends on this | EU AI Act Article 43; ISO/IEC 42006 |
| Sub-processor and foundation-model supplier attestations | Release-gate supply-chain claim | NIST AI RMF GOVERN-6; EU AI Act Article 25 |
| Deployer feedback (for a provider program) or provider instructions-for-use (for a deployer program) | Release-gate cannot pass without the two sides of the handoff | EU AI Act Articles 13, 26 |

## What this program OWES each party (artefacts out)

### To the analyst

- Consolidated crosswalk that supersedes their first draft; feedback on gaps in intake / inventory
- Approved model / system / dataset card templates so future first drafts converge faster
- Updated interested-parties register for their reference

### To the risk engineer

- Release-gate incorporation of the harm model — which risks got mapped to which sub-categories, which residuals are being accepted
- Post-market feedback on which harms materialised, so the harm model can be updated
- Threshold updates when the risk landscape shifts

### To the eval engineer

- Release-gate signal — pass, fail, delayed — so the peer's CI/CD can react
- Update requests to the online-eval slice when a release-gate criterion tightens
- Reproducibility-bundle spec for eval evidence (from `mod-104`)

### To the model-evaluation engineer

- Release-gate incorporation of their statistical framing — which benchmarks / estimators are canonical, which are on the "needs replacement" list
- Post-market drift data so calibration and benchmarks can be maintained

### To MLSec / security

- Release-gate incorporation of their attestations and threat model
- Escalation on any release-gate failure caused by a supply-chain or eval-set-integrity finding

### To the architect

- Release-gate evidence artefacts (assurance cases, decision records, cards, declarations of conformity, post-market surveillance plans) in the form the architect can harmonise across the institution
- Feedback on control-library gaps discovered during release-gate operation
- Deprecation requests for controls that have proven unenforceable at release-gate scope

### To the head of AI governance / CAIO

- Release-gate throughput and outcome metrics (pass, delayed, refused, dispositions)
- Assurance-case posture for narration to the board and to regulators
- Post-market surveillance signal, especially serious-incident reports (EU AI Act Article 61) and material changes to the risk landscape
- Program-KPI reporting

### To the third-party evaluator / auditor and to the regulator

- Release package: technical documentation (EU AI Act Article 11 / Annex IV), instructions for use (Article 13), EU declaration of conformity (Article 47 / Annex V), post-market monitoring plan (Article 72)
- AIMS certification evidence set (ISO/IEC 42001 clauses 4–10 with Annex A applicability)
- NIST AI RMF crosswalk

### To the deployer (for a provider program) or to the provider (for a deployer program)

- Instructions for use (as provider) or use-monitoring reports (as deployer)
- Change-control notifications when the release-gate ships a material change
- Incident notifications with the timelines the regulation requires

## What to do when a party does not deliver

Contracts break. The release-gate has to know how to respond:

1. **The evidence is missing but the deferral is well-defined.** The release-gate delays and files a nonconformity (ISO 42001 clause 10). This role does not backfill the missing evidence itself — it escalates to the party that owes it. If the party is out of capacity, escalation goes to the head of AI governance for reprioritisation.
2. **The evidence is present but the deferral is unclear (two parties think the other owns it).** The release-gate cannot decide until the boundary is drawn. This role escalates to the architect for boundary drawing and files a contract-update ticket.
3. **The party disputes the deferral.** This role does not adjudicate. It escalates to the architect, who reconciles.
4. **The evidence is present but inadequate.** This role writes an explicit inadequacy finding, requests a specific piece of extra evidence, and does *not* redo the peer's craft. Redoing it is the loss-of-altitude failure mode.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — every claim in the assurance case cites the party who owes the evidence.
- `mod-103` (release-gate architecture) — the release-gate schema carries an `evidence_owner` field for each obligation, pointing at the contract row.
- `mod-104` (evidence pipeline) — pipeline access controls follow the contract's owning parties.
- `mod-109` (third-party interface) — the contract's third-party rows become the interface specification.
- `mod-112` (owning the program) — the contract is a core artefact of the program charter, reviewed on a standing cadence.

## Summary

- A deferral contract names every party that produces evidence for the release-gate and every party the release-gate produces artefacts for, with the specific artefact, the reason the release-gate needs it, and the framework citation.
- Evidence-in comes from analyst, risk engineer, eval engineer, model-eval engineer, MLSec / security, agentic-safety engineer (for tier-3), architect, head / CAIO, and external third parties.
- Artefacts-out go to those same parties plus regulators, third-party evaluators, and deployers or providers on the other side of the handoff.
- When the contract breaks, the release-gate delays and escalates — it does not backfill peer craft.
- Exercise 01 has you write the contract for a realistic organisation and defend each row against a peer or higher-track lead.
