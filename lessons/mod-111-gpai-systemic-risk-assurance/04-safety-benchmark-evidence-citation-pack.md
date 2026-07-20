# Safety-Benchmark Evidence — a Citation Pack

## Motivation

Chapter `01` set out Article 55(1)(a)'s requirement for "state-of-the-art model evaluation ... including conducting and documenting adversarial testing." Chapter `02` walked the frontier-lab frameworks that structure the tier / level decision. Chapter `03` walked the AI 600-1 crosswalk and the AISI-shape TEVV envelope. In every case, the assurance case ends up *citing* a specific benchmark suite as the source of a specific piece of capability evidence.

This chapter is the *citation pack* — the reference list of benchmark suites that show up as evidence in a GPAI-systemic-risk assurance package, with, per benchmark, what it evaluates, what its score means at the level the assurance case needs to understand, what the release-assurance programme cites (name, version, configuration, result), and what it does *not* try to reinterpret.

The last point is the critical one. The release-assurance methodology owner is not the benchmark methodology owner. Depth on any of these benchmarks — how the score is constructed, what its statistical properties are, whether it is representative of the deployment surface, whether it has known contamination issues — is owned by the peer `model-evaluation-engineer` and `ai-risk-engineer` (and, for agentic evaluations, `agentic-safety-engineer` at level 40). This chapter reads each benchmark at *citation depth*: enough to place it, enough to cite it, enough to hand off to the peer specialist who owns the depth.

## The citation shape

Every benchmark citation in the assurance bundle carries the same shape:

- **Name and version.** The benchmark's canonical name and its version (or release date; benchmarks are versioned inconsistently).
- **Source.** The publication or landing page the benchmark is authoritatively sourced from (arXiv paper, MLCommons landing page, GitHub repository).
- **Configuration.** Which of the benchmark's variants was run (sub-tasks selected, decoding parameters, evaluator model if any, temperature, sampling budget).
- **Result.** The score(s) reported, with the reporting convention the benchmark uses.
- **Peer methodology reference.** The `model-evaluation-engineer` or `ai-risk-engineer` artefact that carries the methodology reading — the reasoning about why *this* benchmark, run *this way*, is a valid source of evidence for *this* claim.
- **Reproducibility bundle reference.** The reproducibility bundle (`mod-104` chapter `03`) that contains the evaluation run.

The citation shape is uniform so that a reviewer at the AI Office, at UK / US AISI, at a notified body, or at internal audit can walk any benchmark citation the same way.

## MLCommons AI Safety Working Group — AILuminate

**What it evaluates.** The [MLCommons AI Safety Working Group](https://mlcommons.org/ai-safety/) develops safety-benchmark suites for large language models. Its first published benchmark, **AILuminate**, evaluates model responses across hazard categories (violent crimes, non-violent crimes, sex-related crimes, child sexual exploitation, indiscriminate weapons of mass destruction, hate, suicide and self-harm, and more) using an evaluator ensemble that scores responses on a safe / unsafe axis, aggregated into a per-hazard and overall grade.

<!-- needs-research: verify AILuminate's first public release date (public reporting places it in late 2024, sometimes cited as 2024-12), the current version, the exact hazard-category set, and the current grading scale (public reporting describes an A / B / C / D grading). Confirm the current landing page at https://mlcommons.org/ai-safety/ or the AILuminate-specific URL. -->

**What its score means at citation depth.** AILuminate reports a grade per hazard category and an overall grade, plus underlying safe / unsafe rates. The grades are relative to a peer set and to an evaluator-ensemble consensus; they are not absolute safety guarantees.

**What the release-assurance programme cites.** The benchmark name, the version, the per-hazard grades, the overall grade, and the peer `model-evaluation-engineer` artefact that reads the grades in context.

**What the release-assurance programme does NOT try to reinterpret.** The evaluator ensemble's construction, the peer-set normalisation, the hazard-taxonomy design decisions, or the appropriateness of AILuminate for a specific deployment surface. Those are peer-owned.

## AIR-Bench 2024

**What it evaluates.** [AIR-Bench 2024](https://arxiv.org/abs/2407.17436) is a safety benchmark whose taxonomy is derived from a survey of government AI regulations and company AI policies, producing a hierarchical risk categorisation used to structure prompt sets across the covered risk domains.

<!-- needs-research: verify the arXiv identifier 2407.17436, the exact taxonomy structure, and the reporting conventions of AIR-Bench 2024 (e.g., how it aggregates across risk categories and how it reports refusal versus compliance). -->

**What its score means at citation depth.** AIR-Bench 2024 reports scores across its hierarchical risk taxonomy, structured for cross-jurisdictional comparability. Because the taxonomy is derived from regulatory and policy sources, its citation carries useful signal about which risks are covered by which regimes.

**What the release-assurance programme cites.** The benchmark, the version, the per-category scores, and the peer methodology reading.

**What it does NOT try to reinterpret.** The taxonomy derivation methodology, the prompt-set construction, or the appropriateness of the taxonomy for a specific downstream use.

## HarmBench

**What it evaluates.** [HarmBench](https://arxiv.org/abs/2402.04249) is a standardised evaluation framework for automated red-teaming of large language models against harmful behaviours. It carries a curated set of harmful-behaviour prompts across categories (chemical / biological, cybercrime and unauthorised intrusion, harassment and bullying, harmful content, illegal activity, misinformation and disinformation, and more) and pairs them with attack methodologies to measure the model's resistance to being induced into harmful outputs.

<!-- needs-research: verify the arXiv identifier 2402.04249, the current version of HarmBench, and the exact behaviour-category set. -->

**What its score means at citation depth.** HarmBench reports an attack-success rate (ASR) per model, per behaviour category, per attack methodology. Lower ASR is better; ASR under a specific attack methodology reflects both the model's baseline refusal behaviour and its resistance to that specific attack.

**What the release-assurance programme cites.** The benchmark, the version, the attack methodologies configured, the per-category ASR, and the peer methodology reading.

**What it does NOT try to reinterpret.** The attack-set construction, the choice of attack methodologies, the appropriateness of a specific ASR threshold, or the coverage claims of the behaviour set. Peer-owned.

## AgentDojo

**What it evaluates.** [AgentDojo](https://arxiv.org/abs/2406.13352) is an evaluation framework for prompt injection and other attacks against tool-using LLM agents. It defines an environment with tools, benign user tasks, and adversarial injections in tool outputs; it measures whether the agent completes benign tasks and whether it resists injections that try to redirect the agent to harmful actions.

<!-- needs-research: verify the arXiv identifier 2406.13352, the current version of AgentDojo, and the exact metric set (utility on benign tasks, targeted attack success rate on injections, untargeted attack success rate). -->

**What its score means at citation depth.** AgentDojo reports both utility (does the agent complete benign tasks?) and injection-resistance (does the agent resist adversarial injections?). Both dimensions matter: an agent that resists injections but cannot complete benign tasks is not useful; an agent that completes benign tasks but capitulates to injections is unsafe.

**What the release-assurance programme cites.** The benchmark, the version, the utility metric, the injection-resistance metric, and the peer methodology reading — often owned by `agentic-safety-engineer` for agentic-deployment release-gates.

**What it does NOT try to reinterpret.** The environment design, the injection-set construction, or the metric-weighting decisions.

## InjecAgent

**What it evaluates.** [InjecAgent](https://arxiv.org/abs/2403.02691) is a benchmark for indirect prompt injection against tool-using LLM agents, with particular attention to attacks that come from tool outputs (rather than from the primary user input). It measures the agent's susceptibility to being redirected by injected content from tool responses.

<!-- needs-research: verify the arXiv identifier 2403.02691, the current version, and the exact metric conventions (targeted attack success rate, untargeted attack success rate, and any enhanced-attack variant). -->

**What its score means at citation depth.** InjecAgent reports attack-success rates under indirect-injection scenarios, often split by whether the injection targets a specific harmful action or just tries to hijack the agent generically.

**What the release-assurance programme cites.** The benchmark, the version, the attack-success rates, and the peer methodology reading.

**What it does NOT try to reinterpret.** The indirect-injection scenario design, the choice of harmful-action targets, or the coverage claims.

## SafetyBench

**What it evaluates.** [SafetyBench](https://arxiv.org/abs/2309.07045) is a multiple-choice benchmark for evaluating LLM safety understanding across categories including offensiveness, unfairness and bias, physical health, mental health, illegal activities, ethics and morality, and privacy. It is structured as multiple-choice questions rather than open-ended generation, which makes scoring deterministic.

<!-- needs-research: verify the arXiv identifier 2309.07045, the current SafetyBench version, and the exact category set. The multiple-choice format is what distinguishes SafetyBench from open-ended-generation safety benchmarks. -->

**What its score means at citation depth.** SafetyBench reports per-category accuracy on multiple-choice questions about safety. Because the format is multiple-choice, the score measures the model's ability to *identify* safe versus unsafe responses in a structured setting — a different question from whether the model itself would produce safe outputs in open generation.

**What the release-assurance programme cites.** The benchmark, the version, the per-category accuracy, and the peer methodology reading, noting the multiple-choice-vs-generation distinction.

**What it does NOT try to reinterpret.** The question-set construction, the mapping from multiple-choice performance to generative-behaviour claims, or the coverage of the safety-category set.

## CyBench

**What it evaluates.** CyBench is a benchmark for evaluating LLM and LLM-agent capabilities on cybersecurity tasks, including capture-the-flag (CTF) challenges. It is used to characterise the model's cyber-offensive capability uplift — a direct input to the Cybersecurity / cyber-offensive-uplift tracked risk category across the frontier-lab frameworks (chapter `02`).

<!-- needs-research: verify the current publication venue and identifier for CyBench (arXiv preprint typical), the current version, the CTF challenge set, and the reporting conventions (task-solve rate, first-blood time, cost-to-solve). -->

**What its score means at citation depth.** CyBench reports task-solve rates on CTF challenges, often stratified by challenge category (crypto, forensics, pwn, web, reverse engineering, misc) and difficulty. High solve rates on hard challenges indicate substantial cyber-offensive capability uplift.

**What the release-assurance programme cites.** The benchmark, the version, the per-category solve rates, and the peer methodology reading.

**What it does NOT try to reinterpret.** The challenge-set curation, the difficulty banding, or the mapping from CTF performance to real-world cyber-offensive capability.

## WMDP

**What it evaluates.** The [Weapons of Mass Destruction Proxy (WMDP)](https://arxiv.org/abs/2403.03218) benchmark is a set of multiple-choice questions about hazardous knowledge in biosecurity, cybersecurity, and chemical security, designed as a *proxy* for CBRN uplift capabilities the model may possess. It also serves as an evaluation target for *unlearning* research — measuring whether unlearning interventions reduce WMDP performance without damaging general capability.

<!-- needs-research: verify the arXiv identifier 2403.03218, the current WMDP version, the exact question counts and category breakdown (bio, cyber, chem), and the current landing page. -->

**What its score means at citation depth.** WMDP reports per-domain accuracy. High accuracy indicates the model possesses hazardous knowledge in the domain. The *proxy* framing is deliberate — WMDP does not directly measure the capability to *use* the knowledge, only the capability to answer questions demonstrating it.

**What the release-assurance programme cites.** The benchmark, the version, the per-domain accuracy, and the peer methodology reading, noting the proxy-vs-use distinction.

**What it does NOT try to reinterpret.** The proxy design, the mapping from proxy performance to real-world uplift, or the appropriateness of WMDP for a specific CBRN-uplift assessment.

## Frontier-agent evidence from `agentic-safety-engineer` (level 40)

A distinct evidence category the release-assurance programme consumes but does not own is the *frontier-agent red-team evidence* produced by the `agentic-safety-engineer` role at level 40. This includes:

- **Structured red-team evaluations of agentic capabilities** — sandboxed environments in which the agent is scored on multi-step task completion under adversarial conditions.
- **Elicitation studies** for capabilities that only emerge when the agent has tool access, extended context, or persistent memory.
- **Mitigation-effectiveness evaluations** for agentic guardrails (kill-switches, sandbox escapes, tool-permission enforcement, cost limits, self-modification detection).

**Release-assurance implication.** The programme cites these artefacts by reference. The citation shape is the same — name, version, configuration, result, peer methodology reference, reproducibility bundle reference — but the peer methodology owner is `agentic-safety-engineer` rather than `model-evaluation-engineer`. The distinction matters at handoff: the assurance case's methodology-reference field cites the correct peer role, so the AISI-style TEVV evaluator (chapter `03`) can escalate methodology questions to the correct owner.

## What the citation pack does not cover

This chapter is deliberately restricted to safety-relevant benchmarks that recur in GPAI-systemic-risk assurance packages. It does *not* cover:

- **General-capability benchmarks** (MMLU, MMLU-Pro, GPQA, MATH, HumanEval, and similar) — these are typically cited in the model card's general-capability section (`mod-105`) rather than in the Article 55 evidence set.
- **Task-specific evaluations** (long-context retrieval, tool-use accuracy, function-calling correctness) — often cited in the deployment-tier evidence for specific use-cases (`mod-108`).
- **Fairness benchmarks** (BBQ, WinoBias, HolisticBias, and similar) — cited in the fairness sections of the assurance case; owned by `ai-risk-engineer`.
- **Alignment / preference benchmarks** (RewardBench, Chatbot Arena) — cited in the alignment-evidence section; typically owned by `ai-alignment-engineer` or `model-evaluation-engineer`.

The exclusion is not because these benchmarks are unimportant — many are load-bearing in the broader assurance case — but because they are not what the systemic-risk-specific Article 55 discharge typically cites.

## Worked example — the safety-benchmark evidence set in the systemic-risk-GPAI bundle

Continuing the worked example from chapters `01`–`03`, the assurance bundle for the release candidate carries a *safety-benchmark evidence subset* citing:

- **AILuminate v1.x** with per-hazard grades and the overall grade, in the reproducibility-bundle format (`mod-104` chapter `03`).
- **AIR-Bench 2024** with per-category scores across the derived-from-regulation taxonomy.
- **HarmBench** with per-behaviour ASR across the configured attack methodologies.
- **AgentDojo** and **InjecAgent** with utility and injection-resistance metrics for the agentic-deployment surface.
- **SafetyBench** with per-category multiple-choice accuracy.
- **CyBench** with per-category CTF task-solve rates, feeding the Cybersecurity tracked-risk-category evidence.
- **WMDP** with per-domain accuracy (bio, cyber, chem), feeding the CBRN tracked-risk-category evidence and — for the release candidate — evidence of the unlearning intervention's effect on WMDP performance without damage to general capability.
- **Frontier-agent red-team evidence** from the `agentic-safety-engineer` peer, cited by reference.

Each citation carries the shape at the top of this chapter, with the peer methodology-reference field pointing at the correct peer's artefact. The AI Office's reviewer (chapter `01`), the AISI-style TEVV evaluator (chapter `03`), and the internal ISO/IEC 42001 auditor can all walk the same set the same way.

## Anti-patterns

- **Benchmark laundering.** Citing a strong benchmark score for a related-but-different capability domain than the one the release-gate criterion actually needs. A high SafetyBench multiple-choice accuracy is not evidence of safe generation; a low HarmBench ASR under one attack methodology is not evidence of resistance under a different methodology.
- **Version drift.** Citing a benchmark by name without the version pinned. Benchmark suites revise over time; a citation without a version is un-walkable six months later.
- **Reinterpretation drift.** The release-assurance programme adding its own interpretation on top of a peer's benchmark reading. The programme cites; the peer interprets.
- **Coverage inflation.** Claiming the benchmark set covers a risk category more comprehensively than the peer methodology reading supports. The AI 600-1 crosswalk (chapter `03`) is the check — every risk category should point at *peer-owned* coverage claims, not release-assurance-programme claims.

## Where this shows up in the rest of the track

- `mod-104` (evaluation evidence pipeline) — the reproducibility-bundle shape every benchmark citation resolves to.
- `mod-108` (deployment-tier gating) — the tier / level decision consumes these benchmark citations as capability evidence.
- `mod-109` (third-party evaluator interface) — the AISI-style TEVV evaluator reproduces a chosen subset of these benchmarks independently.
- Chapter `01` — Article 55(1)(a) "state-of-the-art model evaluation" is discharged by this set.
- Chapter `02` — the frontier-lab frameworks structure the tier decision the benchmark evidence feeds into.
- Chapter `03` — the AI 600-1 crosswalk names the risk categories the benchmarks map onto.

## Summary

- A GPAI-systemic-risk assurance bundle cites a specific set of safety-benchmark suites as evidence for Article 55(1)(a) "state-of-the-art model evaluation" — MLCommons AILuminate, AIR-Bench 2024, HarmBench, AgentDojo, InjecAgent, SafetyBench, CyBench, WMDP.
- The citation shape is uniform: name, version, source, configuration, result, peer methodology reference, reproducibility bundle reference.
- The release-assurance methodology owner cites; the peer `model-evaluation-engineer`, `ai-risk-engineer`, and `agentic-safety-engineer` (level 40) own the methodology depth.
- Frontier-agent red-team evidence from `agentic-safety-engineer` (level 40) is a distinct evidence category consumed by reference, not duplicated by methodology.
- Benchmark laundering, version drift, reinterpretation drift, and coverage inflation are the recurring anti-patterns to avoid.
- Exercise 04 has you build the safety-benchmark citation pack for a specific release candidate, with every citation carrying the uniform citation shape and the peer methodology reference.
