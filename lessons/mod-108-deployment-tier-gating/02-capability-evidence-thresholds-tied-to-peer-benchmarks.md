# Capability-Evidence Thresholds Tied to Peer-Produced Benchmarks

## Motivation

Chapter `01` set out the frontier-lab pattern: a tier is a capability envelope with associated mitigation obligations, and the tier gate fires when the capability envelope changes. That framing is only useful if the capability envelope is *measurable*. A tier gate whose transition triggers are prose sentences ("substantial uplift in cyber-offensive capability") is a governance claim, not a control.

The release-assurance methodology owner does *not* build benchmarks, does *not* run evals, does *not* author eval harnesses. That work is owned by peer specialists — `ai-eval-engineer` and `model-evaluation-engineer` at level 30, `ai-risk-engineer` at level 25. The methodology owner's job is to *specify thresholds* on the metrics those peers produce and *consume the evidence* those peers deliver.

This chapter walks the concrete benchmark suites the enterprise tier gate cites, the deferral contract that keeps the methodology owner out of eval-authoring, and the shape of a threshold spec. The point is to make the tier transition triggers from chapter `01` concrete enough that a reviewer can look at a candidate release and answer, without judgement, whether it sits in the tier the artefact claims.

## The deferral contract

The methodology owner writes threshold specs. The peer specialists produce the evidence. The two roles have a *contract* whose failure modes are worth naming:

- **The methodology owner does not author the benchmark.** If they do, they are backfilling peer work (mod-101 backfill trap) and the "independent" evidence loses its independence.
- **The peer specialist does not set the threshold.** If they do, the specialist is now signing off on the policy the evidence discharges, which is a governance conflict.
- **Neither role can silently rewrite the other's output.** A threshold change requires re-review; an evidence protocol change requires re-review.

The contract has three artefacts (mod-102 chapter `06`, mod-103 chapter `04`):

- **The threshold spec** — owned by the methodology owner: which metric on which benchmark suite at which numerical threshold with which statistical framing at which decision rule.
- **The evidence contract** — owned jointly: what the peer will deliver (the artefact schema, the reproducibility clauses, the calibration reference, the versioning).
- **The evidence artefact** — owned by the peer: the delivered measurement, pinned by digest into the pipeline (`mod-104`).

The rest of this chapter reads the two families of benchmarks the enterprise tier gate typically consumes — safety-side and capability-side — and then the shape of the threshold spec that ties them to a tier transition.

## Safety-side evidence

Safety-side benchmarks measure whether the model produces harmful, unsafe, or policy-violating outputs. The methodology owner cites them as *floor* thresholds — a candidate release cannot sit in tier T unless the safety-side evidence at T is present and above the specified floor. Peer specialists at `ai-risk-engineer` and `ai-eval-engineer` own the runs; the methodology owner reads the reports.

### HarmBench

**What it is.** HarmBench is a standardised evaluation framework for automated red-teaming and robustness of refusal behaviours. It offers a curated set of harmful-behaviour prompts across multiple harm categories, and a scoring methodology for measuring attack success rate against a target model. [HarmBench](https://www.harmbench.org/) is the reference site; the associated arXiv paper is [Mazeika et al., "HarmBench" (arXiv:2402.04249)](https://arxiv.org/abs/2402.04249).

**What the release-gate consumes.** Attack-success-rate per harm category, per attack method, on the specific model configuration under review (base model + system prompt + guardrails). The methodology owner specifies the categories in scope and the per-category floor.

**Tier-gate use.** HarmBench-style attack-success-rate metrics land in the safety-floor row of the enterprise tier scheme. A high-tier deployment (broad external reach, high tool autonomy) has stricter floors than a low-tier internal deployment.

### AIR-Bench 2024

**What it is.** AIR-Bench 2024 is a safety benchmark that scores model responses against a *risk taxonomy* derived from AI regulatory guidance (regulatory-inspired risk categories rather than a purely academic harm taxonomy). <!-- needs-research: verify canonical URL and current version of AIR-Bench 2024; verify the associated paper reference (Zeng et al.) and the specific regulatory sources the taxonomy is derived from. -->

**What the release-gate consumes.** Per-risk-category safety scores calibrated against the regulatory-inspired taxonomy — useful for a release-gate that has to defend its evidence set to a regulator, because the axis structure aligns with what the regulator expects to see.

**Tier-gate use.** Cite as an alternative or complementary safety-floor to HarmBench, especially where the deployment surface is regulator-facing.

### SafetyBench

**What it is.** SafetyBench is a multiple-choice safety benchmark, covering safety-related categories through a multiple-choice question format that supports rapid, cheap, and reproducible measurement. <!-- needs-research: verify canonical URL for SafetyBench and current version; confirm the specific safety categories in the current release. --> The paper is [Zhang et al., "SafetyBench" (arXiv:2309.07045)](https://arxiv.org/abs/2309.07045).

**What the release-gate consumes.** Per-category safety accuracy on the MCQ set, useful as a regression signal (a fast eval that fires between full HarmBench runs) rather than as the authoritative floor.

**Tier-gate use.** Threshold spec cites SafetyBench as a *regression-guard* at every candidate release, with HarmBench as the authoritative safety floor at tier boundaries.

### AgentDojo

**What it is.** AgentDojo is an evaluation framework for LLM-based agent robustness against prompt-injection attacks in tool-use settings — the threat model is that an attacker-controlled input reaches the agent through a tool response (e.g., a returned email body, a returned document) and attempts to hijack the agent's behaviour. <!-- needs-research: verify canonical URL agentdojo.spylab.ai and current version; verify associated paper (Debenedetti et al., "AgentDojo" arXiv:2406.13352). -->

**What the release-gate consumes.** Attack-success-rate on prompt-injection scenarios, per attack class, on the specific agent configuration under review (base model + tool set + system prompt + guardrails).

**Tier-gate use.** Any tier where `tool-invocation autonomy` is `Med` or higher cites AgentDojo-style evidence as a mitigation prerequisite. Without it, the mitigation obligation for tool-use is not discharged.

### InjecAgent

**What it is.** InjecAgent is a benchmark for evaluating indirect prompt-injection resilience of LLM agents interacting with tool outputs, complementary to AgentDojo. The associated paper is [Zhan et al., "InjecAgent" (arXiv:2403.02691)](https://arxiv.org/abs/2403.02691). <!-- needs-research: verify current canonical benchmark URL and any version updates. -->

**What the release-gate consumes.** Per-tool-class attack-success-rate for indirect prompt injection.

**Tier-gate use.** Cite alongside AgentDojo for tool-use tiers where the tool set is heterogeneous (email + web + files + APIs) rather than homogeneous.

## Capability-side evidence

Capability-side benchmarks measure what the model can *do*, not what it *refuses*. The methodology owner cites them as *transition triggers* — a capability crossing a threshold moves the candidate up (or forces the mitigation obligations to escalate). Peer specialists at `ai-eval-engineer` and `model-evaluation-engineer` own the runs.

### SWE-bench Verified

**What it is.** SWE-bench Verified is a human-verified subset of SWE-bench (a benchmark of real-world software-engineering tasks scraped from GitHub issues). The Verified variant filters the original set to tasks whose specification, test coverage, and evaluation are validated by human annotators. [SWE-bench Verified announcement](https://openai.com/index/introducing-swe-bench-verified/); the original benchmark is [Jimenez et al., "SWE-bench" (arXiv:2310.06770)](https://arxiv.org/abs/2310.06770).

**What the release-gate consumes.** Resolved-issue rate on the Verified subset, with a stated statistical uncertainty (paired bootstrap, per-task variance).

**Tier-gate use.** Any tier for a coding-assistant product cites SWE-bench Verified performance as the capability floor. A tier admitting *autonomous* PR-authoring cites a stricter threshold than a tier admitting only *suggestion-mode* completion. Capability crossings here are typically upward — a new model with markedly higher SWE-bench Verified performance may not fit the previous tier's mitigation set (broader autonomy admissible, but also broader potential impact per action).

### τ-bench

**What it is.** τ-bench (tau-bench) is a benchmark for evaluating agents in realistic multi-turn interactive settings with tool use and simulated users — the tasks are drawn from customer-support-agent-like scenarios (airline booking, retail), and the metric is a task-success rate under simulated user interaction. The paper is [Yao et al., "τ-bench" (arXiv:2406.12045)](https://arxiv.org/abs/2406.12045).

**What the release-gate consumes.** Task-success rate per domain, with per-episode variance.

**Tier-gate use.** For a customer-support agent tier, τ-bench is the capability floor: if the agent cannot achieve a stated success rate on τ-bench-like tasks, it does not belong in the tier that admits customer-facing interactions. For higher tiers, τ-bench performance may *force* mitigation escalation: an agent capable of high task-success in multi-turn tool-use settings is also capable of higher-impact misbehaviour in those settings.

### GAIA

**What it is.** GAIA is a general-purpose assistant benchmark evaluating an agent's ability to answer questions requiring reasoning, multi-modal understanding, web-browsing, and tool use, structured around real-world open-ended questions with a verifiable answer. The paper is [Mialon et al., "GAIA" (arXiv:2311.12983)](https://arxiv.org/abs/2311.12983).

**What the release-gate consumes.** Level-graded exact-match accuracy, with per-level variance.

**Tier-gate use.** For a general-purpose assistant deployment, GAIA reads as the *breadth-of-capability* signal. A tier admitting broad tool use and long-horizon question-answering cites GAIA at the appropriate level as evidence that the capability is present. Below-threshold performance on GAIA may argue the deployment tier is over-permissive relative to the actual capability, which is a different failure mode from over-mitigation — but equally worth catching.

### CyBench

**What it is.** CyBench is a benchmark for evaluating cybersecurity capabilities of LLM-based agents, using capture-the-flag style tasks drawn from real cybersecurity competitions. <!-- needs-research: verify canonical CyBench URL and associated paper (Zhang et al., "Cybench" arXiv:2408.08926) and current version. -->

**What the release-gate consumes.** Task-completion rate on offensive-cybersecurity tasks at graded difficulty.

**Tier-gate use.** Any deployment where the model has network access, code-execution capabilities, or tooling relevant to security operations cites CyBench-style evidence as a capability-envelope signal. Crossing a CyBench threshold may not itself change the deployment tier, but it *does* force review of the cybersecurity-attestation clauses (`03`) — if the model is measurably more capable at offensive-cyber tasks, the deployment surface has to demonstrate mitigation.

## The shape of a threshold spec

A threshold spec is the artefact the methodology owner writes and the tier gate walker (mod-103 chapter `01`) reads. Its shape:

- **Identifier.** Stable, cited by the assurance case and the tier-decision artefact (`05`), e.g., `TIER-CE-SAFETY-01` for "tier capability-evidence, safety, criterion 01."
- **Benchmark reference.** Which benchmark suite, which version, on which configuration (base model + fine-tune + system prompt + guardrails + tool set).
- **Metric.** The specific metric extracted — attack-success rate for HarmBench, task-success rate for τ-bench, resolved-issue rate for SWE-bench Verified.
- **Statistical framing.** Point estimate + confidence interval + estimator (paired bootstrap, Wilson interval, whatever the peer contract specifies). "A number without an interval is not a measurement."
- **Decision rule.** The rule that turns the measurement into a pass / fail. Typically: point estimate above / below threshold *and* CI lower / upper bound above / below the same threshold. The two-part rule prevents the case where the point estimate crosses but the uncertainty is enormous.
- **Calibration reference.** Which prior release, or which industry benchmark, the threshold is calibrated to — the anchor for the numerical value. "Threshold set at the level of the prior release ± X" or "threshold set at the level of the frontier-lab published baseline ± X."
- **Framework citation.** Which NIST AI RMF sub-category (MEASURE-2.7 for security / adversarial, MEASURE-2.11 for fairness, and so on), which EU AI Act article (Article 15 for accuracy / robustness / cybersecurity), which internal tier axis (from chapter `01`).
- **Evidence pointer.** Which peer track owns the artefact, which contract row, which SACM `Artifact` ID.
- **Owner.** Named methodology-owner role responsible for the spec; named peer-specialist role responsible for the evidence.

A tier gate carries a set of threshold specs, each in this shape. The tier decision (`05`) is the join of the specs and their evidence.

## Reproducibility is a precondition

Thresholds are only meaningful if the evidence is reproducible. If the peer track cannot re-run the benchmark on demand — because the eval-set is not versioned, because the judge model is not pinned, because the harness is not deterministic — then a threshold spec cited against the evidence is theatre. The evidence pipeline (`mod-104`) owns the reproducibility clauses; the tier gate consumes evidence *only* from artefacts the pipeline has certified as reproducible.

This is not a niche concern. Frontier-lab evals themselves have had reproducibility issues (contamination of eval sets by training-data overlap; judge-model drift across scoring runs; harness non-determinism). The methodology owner reads the peer contract's reproducibility clauses (chapter `mod-104` chapter contents apply) *before* threshold-spec authoring, not after.

## Worked shape — a threshold spec for the customer-support agent

Continuing the `T-CS` product from chapter `01`'s worked shape: a customer-support agent at `(data:Med, tools:High, reach:High, sector:none)`. The tier gate carries the following capability-evidence threshold specs (representative subset):

- `TIER-CE-SAFETY-01` (HarmBench). Attack-success-rate on the "misinformation" and "cybercrime" category subsets, per attack method, on the T-CS configuration. Metric: mean attack-success-rate; decision rule: point estimate ≤ 0.05 AND 95% CI upper-bound ≤ 0.08 per category. Calibration: to the prior T-CS release's measured level. Framework: MEASURE-2.7; EU AI Act Article 15(4); tier axis `data:Med`.
- `TIER-CE-INJECT-01` (AgentDojo). Attack-success-rate on the indirect-prompt-injection scenarios matching the T-CS tool set (email-read, CRM-read). Metric: mean attack-success-rate; decision rule: point estimate ≤ 0.03 AND 95% CI upper-bound ≤ 0.05. Calibration: to the frontier-lab published baseline ± 0.02. Framework: MEASURE-2.7; EU AI Act Article 15(4); tier axis `tools:High`.
- `TIER-CE-CAP-01` (τ-bench). Task-success rate on the retail and customer-service subsets, matching the T-CS deployment domain. Metric: mean task-success rate; decision rule: point estimate ≥ 0.55 AND 95% CI lower-bound ≥ 0.50. Calibration: to the previous T-CS release's measured level (this is a floor; below-threshold means the product is not fit for the tier). Framework: MEASURE-2.1; EU AI Act Article 15(1); tier axis `reach:High`.
- `TIER-CE-CAP-02` (GAIA). Level-1 accuracy on GAIA. Metric: exact-match accuracy at Level-1; decision rule: point estimate ≥ 0.30 AND CI lower-bound ≥ 0.25. Calibration: to the frontier-lab published baseline. Framework: MEASURE-2.1; tier axis `reach:High` (breadth-of-capability signal that the tier is *appropriate* to the model, not over-permissive).

The tier gate for T-CS *passes* only if every spec passes; if a capability spec fails upward (the model is measurably more capable than the previous release), the tier gate re-runs the *tier landing* — the vector may need to move, which may in turn escalate mitigation obligations (`03`, `04`).

## Where this shows up in the rest of the track

- `03` — the mitigation-obligation side: cybersecurity attestation clauses that stack on top of the capability-evidence thresholds.
- `04` — what happens when a threshold is missed at gate or when the evidence expires.
- `05` — the tier-decision artefact composes the threshold specs and their evidence into a single reviewable document.
- `mod-103` chapter `04` — the peer-contract shape for evidence pipelines (the contract layer this chapter cites).
- `mod-104` — the evidence pipeline that pins the evidence artefacts by digest and enforces reproducibility.
- `mod-110` — the online-eval slice that provides the periodic re-evaluation the FSF-style pattern requires.
- `mod-111` — for GPAI systemic-risk deployments, the threshold set is scaled to the EU AI Office's expected evaluation protocols.

## Summary

- The methodology owner writes threshold specs; peer specialists (`ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`) produce the evidence. The two roles are separated by a contract; blurring them breaks independence.
- Safety-side evidence comes from HarmBench, AIR-Bench 2024, SafetyBench (regression signal), AgentDojo, InjecAgent — floor thresholds per tier axis.
- Capability-side evidence comes from SWE-bench Verified, τ-bench, GAIA, CyBench — transition triggers per tier axis (may force mitigation escalation upward, or may indicate a tier is over-permissive).
- A threshold spec has: identifier, benchmark reference, metric, statistical framing, decision rule, calibration reference, framework citation, evidence pointer, owner.
- Reproducibility is a precondition. Evidence not certified reproducible by `mod-104` cannot ground a threshold spec.
- Exercise 02 has you author threshold specs for a worked enterprise tier, tying each spec to a peer benchmark and to a framework citation.
