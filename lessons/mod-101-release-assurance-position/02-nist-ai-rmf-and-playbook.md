# NIST AI RMF 1.0 — GOVERN / MAP / MEASURE / MANAGE, and the Playbook

## Motivation

NIST AI RMF 1.0 (published 2023-01) is the anchor risk-management framework the U.S. federal government has aligned to, and it is the framework that most U.S. and multinational enterprises use as the outer envelope of their AI governance program. It is a *voluntary* framework — but its language is now the reference language, and its sub-categories are cited in requirements at almost every large deployer.

For a release-assurance program the framework matters in one very concrete way. Its four functions and their sub-categories are the *slots* into which every release-gate obligation must be plugged, so that a regulator, an auditor, or a peer team can walk from "we require evidence of X at gate" to "that is NIST AI RMF sub-category MEASURE-2.7." That mapping is what makes the release-gate defensible and comparable across systems.

This chapter paraphrases the four functions in the shape the release-assurance program uses them, and points at the day-to-day reference — the NIST AI RMF Playbook — that carries the practical suggested actions.

## The four functions in one paragraph each

Every function reads first as an outcome family, then as a set of categories, then as sub-categories. Numbering follows NIST's own `FUNCTION-CATEGORY.SUBCATEGORY` shape.

### GOVERN

**What it is.** GOVERN establishes a culture and standing structure for AI risk management inside the organisation — policies, roles, accountability, workforce, third-party governance, and the process by which risks are escalated and dispositioned. It is horizontal: it is not attached to any one AI system, but to the organisation's ability to manage AI systems as a class.

**Categories** (paraphrased from NIST AI 100-1, section 5.1):

- **GOVERN 1** — Policies, processes, procedures, and practices across the organisation are in place, transparent, and implemented effectively.
- **GOVERN 2** — Accountability structures are in place so appropriate teams and individuals are empowered, responsible, and trained.
- **GOVERN 3** — Workforce diversity, equity, inclusion, and accessibility processes are prioritised.
- **GOVERN 4** — Organisational teams are committed to a culture that considers and communicates AI risk.
- **GOVERN 5** — Processes are in place for robust engagement with relevant AI actors.
- **GOVERN 6** — Policies and procedures are in place to address AI risks from third-party software and data.

**Release-assurance implication.** GOVERN is where the assurance program *itself* is authorised: who signs a release-gate decision, who can veto, how a fail is dispositioned, how third-party evaluators are engaged, how the risk register connects to the release process. Nothing else in the framework is meaningful without this.

### MAP

**What it is.** MAP builds context around a particular AI system before it is measured or managed: what it is used for, by whom, in what setting, with what impacts, and how it depends on other systems, data, and actors. MAP is where "release-gate scope" is set.

**Categories** (paraphrased):

- **MAP 1** — Context is established and understood.
- **MAP 2** — Categorisation of the AI system is performed.
- **MAP 3** — AI capabilities, targeted usage, goals, and expected benefits and costs are understood.
- **MAP 4** — Risks and benefits are mapped for all components of the AI system, including third-party parts and impact on external actors.
- **MAP 5** — Impacts to individuals, groups, communities, organisations, and society are characterised.

**Release-assurance implication.** MAP is where an assurance case starts. Before the release-gate can require evidence, it has to know what tier of system this is, what the intended use is, what the reasonably foreseeable misuses are, and who the affected parties are. Every subsequent measurement clause depends on this framing being on file.

### MEASURE

**What it is.** MEASURE is the analytical function: it selects methods and metrics, applies them, tracks trustworthy-AI characteristics (validity and reliability, safety, security and resilience, accountability and transparency, explainability and interpretability, privacy, fairness with harmful bias managed), and feeds back to MAP and MANAGE.

**Categories** (paraphrased):

- **MEASURE 1** — Appropriate methods and metrics are identified and applied.
- **MEASURE 2** — AI systems are evaluated for trustworthy characteristics.
- **MEASURE 3** — Mechanisms for tracking identified AI risks over time are in place.
- **MEASURE 4** — Feedback about efficacy of measurement is gathered and assessed.

**Release-assurance implication.** MEASURE is where the release-gate has its highest evidentiary density. Almost every artefact this role produces — pre-deployment evaluations, red-team results, robustness / accuracy / safety measurements, statistical justification for thresholds — cites into MEASURE. The peer evaluation specialists (`ai-eval-engineer`, `model-evaluation-engineer`) engineer the raw measurements; this role wires them into MEASURE-2 sub-categories in the assurance case.

### MANAGE

**What it is.** MANAGE prioritises the risks identified in MAP and measured in MEASURE, decides on response strategies (accept / mitigate / transfer / avoid), implements the response, monitors it, and communicates it — including incident response and continuous improvement.

**Categories** (paraphrased):

- **MANAGE 1** — AI risks based on assessments and other analytical output from MAP and MEASURE are prioritised, responded to, and managed.
- **MANAGE 2** — Strategies to maximise AI benefits and minimise negative impacts are planned, prepared, implemented, documented, and informed by input from relevant AI actors.
- **MANAGE 3** — AI risks and benefits from third-party entities are managed.
- **MANAGE 4** — Risk treatments, including response and recovery, and communication, are documented and monitored regularly.

**Release-assurance implication.** MANAGE is where the release-gate *decision* lives — accept the release, mitigate before ship, delay, or refuse. It is also where post-market surveillance and incident response hook back in, keeping the release-gate decision alive after ship (`mod-110`).

## The Playbook is the day-to-day reference

NIST AI 100-1 is the framework document. It is deliberately terse: functions, categories, sub-categories, one paragraph each. The *NIST AI RMF Playbook* is the companion knowledge base (published on `airc.nist.gov`) that carries, per sub-category, **suggested actions**, **transparency and documentation clauses**, and **cross-references to other frameworks** (ISO/IEC 42001, ISO/IEC 23894, EU AI Act, and more).

The Playbook is what a release-assurance program leans on when it plugs a release-gate obligation into a sub-category. Some worked examples of the shape:

- **MEASURE-2.7** — the Playbook lists suggested actions for evaluating security, resilience, and adversarial-ML posture, and cross-references NIST AI 100-2 (adversarial-ML taxonomy). A release-gate that requires "red-team evidence" for a tier-3 deployment cites into MEASURE-2.7 and pulls the Playbook's suggested actions as the pattern.
- **MEASURE-2.11** — the Playbook lists suggested actions for evaluating fairness with harmful bias managed, and cross-references NIST SP 1270 (bias in AI). A release-gate that requires "disaggregated performance by protected group" cites here.
- **GOVERN-6.1 / 6.2** — the Playbook carries suggested actions for third-party governance. A release-gate that requires "supplier attestations for foundation-model providers" cites here (and threads into `mod-107` for SR 23-4).
- **MANAGE-4.1** — the Playbook carries suggested actions for post-deployment monitoring and improvement. A release-gate that produces a "post-market surveillance plan" cites here (and threads into `mod-110`).

Two other NIST documents extend the framework and matter for this program:

- **NIST AI 600-1 — Generative AI Profile.** A profile of AI RMF 1.0 for GenAI, published 2024-07. It carries risk categories specific to GenAI (confabulation, dangerous or violent recommendations, environmental impact, harmful bias, human-AI configuration, information integrity, information security, intellectual property, obscene or degrading content, value chain and component integration, and more) and per-risk suggested actions cross-referenced into GOVERN / MAP / MEASURE / MANAGE. When the release gate is for a GenAI system, this profile is the paraphrase of the framework in use.
- **NIST AI 100-2 — Adversarial-ML taxonomy.** The reference taxonomy for adversarial-ML risks. The MEASURE-2.7 pattern above pulls from this document.

## Worked example — one obligation, plugged in

Suppose the release-gate for a customer-support-agent RAG system requires: *"Evidence of robustness to prompt-injection under the deployment surface, at or above threshold T, with a stated statistical uncertainty."*

The release-assurance program plugs this in as follows:

- **MAP-1.1** — record system context: RAG over a knowledge base, deployment surface is a customer-support chat, threat model includes user-supplied text.
- **MAP-2.3** — categorisation: LLM-based product, prompt-injection is a foreseeable misuse.
- **MEASURE-2.7** — evidence of security / resilience: red-team results from a prompt-injection suite, threshold T, statistical framing (owned by `model-evaluation-engineer`), citation into NIST AI 100-2.
- **MEASURE-2.13** — evidence of measurement efficacy: how do we know the suite is representative? Cite the risk-engineer's harm model (owned by `ai-risk-engineer`) and the peer eval engineer's coverage.
- **MANAGE-1.3** — response strategy: what happens if the evidence falls below T? Mitigation, delay, refuse.
- **MANAGE-4.1** — post-deployment monitoring: how does the online eval keep this alive after ship? Cite `ai-eval-engineer`'s online-eval slice.

That is the shape. Every obligation the release-gate carries should be walkable in the same way — from obligation text, into one or more sub-categories, into the peer evidence that discharges it, into the assurance case.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — the assurance case is structured so each claim cites its sub-category and its evidence in one hop.
- `mod-103` (release-gate architecture) — the release-gate schema carries an explicit `nist_ai_rmf_subcategory` field per obligation.
- `mod-104` (evidence pipeline) — every logged artefact carries its sub-category tag so an auditor can retrieve by function.
- `mod-105` (cards for external audiences) — the model / system / dataset card layout carries a NIST AI RMF crosswalk section.
- `mod-106` (cross-jurisdictional mapping) — NIST AI RMF is one of four columns of the crosswalk, with ISO/IEC 42001 and EU AI Act as the others.
- `mod-110` (post-market surveillance) — the surveillance plan cites MANAGE-4 sub-categories.
- `mod-111` (GPAI systemic-risk assurance) — the GenAI Profile (AI 600-1) is the paraphrase of the framework used.

## Summary

- NIST AI RMF 1.0 has four functions: GOVERN (organisational), MAP (context of a system), MEASURE (analytical), MANAGE (response). Each has categories and sub-categories in `FUNCTION-CATEGORY.SUBCATEGORY` shape.
- The Playbook (`airc.nist.gov/AI_RMF_Knowledge_Base/Playbook`) is the day-to-day reference — per sub-category suggested actions, transparency clauses, and cross-references to other frameworks.
- The release-assurance program plugs each release-gate obligation into one or more sub-categories, and cites peer evidence (risk engineer, eval engineer, model-eval engineer, MLSec) as the discharge.
- The GenAI Profile (AI 600-1) is the paraphrase of the framework for GenAI systems; NIST AI 100-2 is the adversarial-ML taxonomy MEASURE-2.7 relies on.
- Exercise 02 has you build the obligation → sub-category → evidence map for a worked release-gate.
