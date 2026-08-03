# exercise-02: Capability-Evidence Threshold Specs Tied to Peer-Produced Benchmarks

**Estimated effort:** 3 hours

## Objective

Author the **capability-evidence threshold-spec set** for one product's tier landing from exercise `01`. Every axis in the tier scheme must be discharged by at least one safety-side threshold spec and (where applicable) at least one capability-side threshold spec, each grounded in a *named peer-produced benchmark* with a *statistical framing*, a *decision rule*, and a *calibration reference*. Author the peer contracts that make the evidence deliverable, and the evidence-artefact schema the tier gate walker consumes.

The exercise is authoring the *threshold-spec side* of the deferral contract from chapter `02`. You do not build benchmarks; you do not run evals; you do not author eval harnesses. That work is owned by the peer specialists (`ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`). You specify what the evidence must be, how the number is turned into a decision, and where the artefact lands.

## Prerequisites

- Chapter [`02-capability-evidence-thresholds-tied-to-peer-benchmarks.md`](../02-capability-evidence-thresholds-tied-to-peer-benchmarks.md) — the deferral contract, the safety-side and capability-side benchmark families, the shape of a threshold spec, and the reproducibility precondition.
- Exercise [`exercise-01-enterprise-tier-scheme-in-rsp-shape.md`](exercise-01-enterprise-tier-scheme-in-rsp-shape.md) — the tier scheme and the specific product's tier landing you will discharge.
- Skim access to at least one benchmark paper per family:
  - Safety-side: [HarmBench (Mazeika et al., 2024)](https://arxiv.org/abs/2402.04249) or [AgentDojo (Debenedetti et al., 2024)](https://arxiv.org/abs/2406.13352).
  - Capability-side: [SWE-bench (Jimenez et al., 2023)](https://arxiv.org/abs/2310.06770) and the [SWE-bench Verified announcement](https://openai.com/index/introducing-swe-bench-verified/), or [τ-bench (Yao et al., 2024)](https://arxiv.org/abs/2406.12045), or [GAIA (Mialon et al., 2023)](https://arxiv.org/abs/2311.12983).
- Familiarity with the peer-role registry — the threshold specs name the peer role that produces each evidence artefact.
- Familiarity with basic statistical framing — point estimate + confidence interval; paired bootstrap or Wilson interval as the go-to estimators. A number without an interval is not a measurement.

## Problem statement

Pick one product from exercise `01`'s portfolio — the one whose tier landing pushes the scheme's axes most (typically the external-facing product with `tools:High`-or-above, or the sector-regulated product). Author the capability-evidence threshold-spec set that discharges every axis of that product's landing.

Two failure modes to design against, both from chapter `02`:

- **Backfill trap.** You will be tempted to author the benchmark yourself when the peer track is slow or silent. Do not; that collapses the deferral contract and the evidence loses its independence.
- **Prose thresholds.** You will be tempted to write thresholds as prose sentences ("HarmBench performance is acceptable at the current tier"). That is a governance claim, not a control. Every threshold spec must be numerical, statistical, and decisional.

## Requirements

Produce six artefacts in a single directory.

### 1. `product-scoping-brief.md`

A short brief that names:

- **Product and tier landing.** Named product from exercise `01`; the tier landing (single-ladder tier or vector across axes); pointer back to the tier scheme.
- **Deployment configuration under evaluation.** The specific configuration the peer track will evaluate — base model + fine-tune (if any) + system prompt + guardrail configuration + tool set + retrieval corpus. The configuration is the *object of evaluation*; ambiguity here means the evidence does not pin to a release candidate.
- **Peer-track partners.** For each axis of the tier landing, the peer track(s) the methodology owner has a delivery contract with (`ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`). Named lead per peer track (or placeholder name for the exercise).
- **Reference-set discipline.** How the reference set for each benchmark is versioned, held-out, protected from training-data contamination, and refreshed. The methodology owner does not own the reference set; the peer track does. But the methodology owner *requires* the discipline and cites it here.

### 2. `threshold-spec-catalogue.md`

The threshold-spec catalogue. One spec per row, with the following columns (each spec is short — half a page is typical). At minimum: **two safety-side specs** and **two capability-side specs**, but more is better. Every axis in the tier landing must be covered by at least one spec.

For each spec:

- **Identifier.** Stable, cited by the assurance case and the tier-decision artefact (`05`). Suggested naming: `TIER-CE-{PRODUCT}-{AXIS}-{SAFETY|CAP}-{NN}` — e.g. `TIER-CE-CS-TOOLS-INJECT-01` for the customer-support agent's tool-injection safety spec.
- **Benchmark reference.** Which benchmark suite, which version, on which configuration (the configuration is the one pinned in the scoping brief). Cite the benchmark's canonical URL and paper.
- **Metric.** The specific metric extracted — attack-success rate for HarmBench / AgentDojo / InjecAgent, task-success rate for τ-bench, resolved-issue rate for SWE-bench Verified, exact-match accuracy for GAIA. Name the metric unambiguously.
- **Statistical framing.** Point estimate + confidence interval + estimator (paired bootstrap, Wilson, whatever the peer contract specifies). Name the CI level (typically 95%).
- **Decision rule.** The rule that turns the measurement into a pass / fail. Typically two-part: *point estimate above / below threshold* AND *CI lower / upper bound above / below the same threshold*. The two-part rule prevents the case where the point estimate crosses but the uncertainty is enormous.
- **Calibration reference.** Which prior release, or which industry benchmark, the numerical threshold is calibrated to — the anchor for the numerical value. "Threshold set at the level of the prior release ± X" or "threshold set at the level of the published frontier-lab baseline ± X." Do not fabricate specific numbers; a placeholder or `<!-- needs-research: … -->` for the specific numerical anchor is legitimate.
- **Framework citation.** Which NIST AI RMF sub-category (MEASURE-2.7 for security / adversarial, MEASURE-2.11 for fairness, MEASURE-2.1 for accuracy, and so on), which EU AI Act article (Article 15 for accuracy / robustness / cybersecurity), which internal tier axis (from exercise `01`).
- **Evidence pointer.** Which peer track owns the artefact, which contract row, which evidence-pipeline (`mod-104`) location the artefact lands at.
- **Owner.** Named methodology-owner role responsible for the spec; named peer-specialist role responsible for the evidence.
- **Expiry.** When the evidence goes stale and the spec must be re-run against fresh evidence.

Cover both directions of the transition:

- **Safety-side floors.** Attack-success rates that must remain *below* threshold. If the floor is crossed upward (the model becomes measurably more vulnerable), the tier is either escalated in its mitigation set or the deployment is not permitted at that tier.
- **Capability-side transitions.** Capability metrics that mark tier boundaries. If a capability threshold is crossed *upward* (the model is measurably more capable), the tier landing may need to move upward and the mitigation set may need to escalate — a more capable model in the same tier is a *higher* risk profile, not a lower one. Below-threshold capability performance may argue the deployment tier is *over-permissive* relative to the actual capability.

### 3. `evidence-contract-set.md`

For each threshold spec in the catalogue, name the *evidence contract* the methodology owner has with the peer track. The contract is jointly owned (the methodology owner drafts, the peer track signs). Each contract row covers:

- **Deliverable artefact.** The named artefact (JSON, CSV, or PDF) the peer track will deliver, with the schema pinned. Fields for a benchmark-run artefact typically include: benchmark ID + version, run configuration (base model, fine-tune, system prompt, guardrail config, tool set, retrieval corpus — the same fields as the scoping brief), per-task raw scores, aggregate metrics with CI, estimator description, per-run seed and environment metadata, reproducibility manifest (harness commit, judge-model version, eval-set commit), timestamp, signer.
- **Reproducibility clauses.** How the peer track guarantees the run is reproducible — versioned eval set, pinned judge model, deterministic (or seeded-stochastic) harness, environment manifest. The clauses foreshadow `mod-104`'s evidence-pipeline reproducibility discipline.
- **Cadence.** Time cadence (quarterly regression, on-triggering-event, at every candidate release, at every tier boundary crossing).
- **Delivery mechanism.** Where the artefact lands (evidence-pipeline location); how the tier gate walker is notified.
- **Signers.** Peer-track lead who signs the artefact as delivered; methodology owner who signs the artefact as *consumed* (a separate signature).
- **Failure protocol.** What happens if the peer track cannot deliver on cadence or the reproducibility clauses fail — deferred criterion at the tier gate (with expiry), rollback to prior evidence, or gating defect that blocks release.

### 4. `evidence-artefact-schema.md`

The concrete JSON (or YAML) schema for one benchmark-run evidence artefact. Pick one benchmark from the catalogue (HarmBench, AgentDojo, τ-bench, SWE-bench Verified, or GAIA — the choice is yours) and sketch the artefact schema the peer track will deliver. Include:

- **Root object.** Top-level fields (benchmark_id, benchmark_version, run_id, timestamp, configuration, aggregate_metrics, reproducibility_manifest, signer).
- **Configuration sub-object.** Fully pinned run configuration.
- **Aggregate-metrics sub-object.** Per-metric fields with point estimate, CI, estimator name.
- **Per-task-result sub-array.** Per-task raw scores (may be omitted from public copy; must be retained in the internal artefact).
- **Reproducibility-manifest sub-object.** Harness commit hash, judge-model version, eval-set commit, seed, environment digest.
- **Signer sub-object.** Peer-track lead, timestamp, cryptographic signature (or `<placeholder>` for the exercise).

A short example artefact populated with realistic-shape placeholder values is helpful. Do not fabricate specific measured numbers; use `<placeholder>` or `<result>` markers where a number would land.

### 5. `reproducibility-preconditions-checklist.md`

Chapter `02` insists: thresholds are only meaningful if the evidence is reproducible. Author a short checklist the methodology owner *runs against a peer track's evidence artefact* before the artefact is admitted to the tier gate.

- **Eval-set integrity.** Eval set is versioned; contamination against training corpora is documented; canary strings or private eval-sets are present where applicable; benchmark-refresh cadence is stated.
- **Judge-model discipline.** Where the benchmark uses an LLM-as-judge, the judge model is pinned to a specific version; judge-model drift is monitored; a re-run against the same inputs produces the same scores within a stated tolerance.
- **Harness determinism.** Harness commit is pinned; seed is fixed (or seeded-stochastic runs are averaged over N seeds); environment is manifest-diffed.
- **Metric computation transparency.** The metric-computation code is versioned and auditable; the CI computation is auditable; per-task raw scores can be re-aggregated by an independent reviewer.
- **Signer independence.** The peer-track signer is independent of the methodology owner; the peer's evidence signature is separate from the methodology owner's consumption signature.
- **Retention.** The internal artefact is retained for the audit window (typically the assurance-case validity window plus the applicable statutory retention period).

Failing the checklist is a *gate defect*, not a soft warning. State the disposition: rework by the peer track (typical), rollback of the tier decision (where the evidence has already been consumed and a defect is found post-hoc), or deferred criterion with expiry (where a specific reproducibility clause is known-broken and a fix is in flight).

### 6. `threshold-drift-and-recalibration-plan.md`

Thresholds are not fixed. Benchmarks are refreshed, industry baselines shift, and the enterprise's own tolerance may change as evidence accumulates. Author the short plan for keeping threshold values current:

- **Review cadence.** When each threshold is opened for review (typically every candidate release for the currency check, and every N months for the numerical recalibration).
- **Recalibration triggers.** Specific events that force an ad-hoc recalibration — the benchmark publisher releases a new version; a Frontier Model Forum publication updates the industry baseline; a serious incident reveals a threshold that was too permissive; a false-alarm rate reveals a threshold that was too strict.
- **Signers.** Methodology owner signs numerical recalibrations within the current scheme's tolerance; head of AI governance signs recalibrations that materially change a tier landing.
- **Prior-release comparability.** Whenever a threshold is recalibrated, prior evidence artefacts must be *re-scored* against the new threshold, or explicitly flagged as *incomparable*. Silent recalibration breaks comparability.
- **Communication.** How the recalibration is communicated to peer tracks and to consumers of the tier-decision artefact.

## Starter guidance

- **Do not author the benchmark.** If your instinct is to write the benchmark's methodology paper in the exercise, you are backfilling peer work. Cite the benchmark and consume it.
- **Two safety-side and two capability-side is the floor.** For a product with `tools:High`, you will find you need at least one AgentDojo-style spec for indirect prompt injection and at least one HarmBench-style spec for the harm categories the product's surface exposes. Add τ-bench or SWE-bench Verified for capability. Cover every axis; there is no "the axis is not relevant" answer for an axis in the tier landing.
- **Every threshold spec is numerical, statistical, and decisional.** Point estimate + CI + decision rule. If your spec reads as prose, rewrite it. Placeholder numbers are fine; missing statistical framing is not.
- **Do not fabricate specific numerical thresholds.** Use placeholders (`<threshold>` or `<value>`) or `<!-- needs-research: … -->` markers with a note on how the number would be calibrated. Fabricated numbers read as fake and undermine the exercise.
- **Reproducibility precondition, not a footnote.** The reproducibility checklist is a hard gate, not a soft one. Frontier-lab evals themselves have had reproducibility issues (training-data contamination, judge-model drift, harness non-determinism). The methodology owner *runs the checklist* before admitting evidence.
- **Capability crossings can force mitigation escalation upward.** A model that is measurably more capable on SWE-bench Verified than the previous release may be *inappropriate for the previous tier's mitigation set*. The threshold spec is a two-way test: the capability threshold may be *exceeded upward*, and that is a tier-landing event.
- **The peer-track owner signs the evidence; the methodology owner signs the consumption.** The two signatures are separate. The threshold spec cites both.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the current version of a benchmark suite, the current published industry baseline, or the peer track's own current contract wording, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `product-scoping-brief.md` pins the product, the tier landing, the deployment configuration under evaluation, the peer-track partners, and the reference-set discipline.
- `threshold-spec-catalogue.md` covers at least two safety-side and two capability-side specs (more is better); every axis in the tier landing is discharged by at least one spec. Each spec has an identifier, benchmark reference, metric, statistical framing, decision rule, calibration reference, framework citation, evidence pointer, owner, and expiry.
- `evidence-contract-set.md` names, for each spec, the deliverable artefact, reproducibility clauses, cadence, delivery mechanism, signers, and failure protocol. The methodology-owner + peer-track split of signatures is preserved.
- `evidence-artefact-schema.md` sketches one benchmark-run artefact schema in JSON or YAML, with root object, configuration sub-object, aggregate-metrics sub-object, per-task-result sub-array, reproducibility-manifest sub-object, and signer sub-object. An example is populated with placeholder values.
- `reproducibility-preconditions-checklist.md` covers eval-set integrity, judge-model discipline, harness determinism, metric computation transparency, signer independence, and retention. The disposition for a checklist failure is stated.
- `threshold-drift-and-recalibration-plan.md` covers review cadence, recalibration triggers, signers, prior-release comparability, and communication.
- No specific numerical threshold is fabricated as if measured. Placeholders are used; `<!-- needs-research: … -->` markers cover unavoidable specifics.
- The catalogue is *internally consistent* — the axes in the scoping brief match the axes discharged in the catalogue, the peer-track partners match the evidence-contract signers, the schema in artefact 4 matches the deliverable named in the contract set.
- The methodology owner does not author the benchmark. Every spec cites the benchmark suite and its owning peer track.

## Stretch goals

- **Author the peer-contract memo the methodology owner sends to `ai-eval-engineer`.** In `peer-contract-memo.md`, draft the two-page memo the methodology owner sends when opening a new evidence contract — the tier axis the evidence discharges, the deliverable schema, the cadence, the reproducibility clauses, the escalation contract if delivery slips. This is what the peer track actually reads.
- **Add a red-team contract row.** Red-team evidence is not a benchmark run; it is a targeted probe with a written scope. In `red-team-contract.md`, sketch the red-team contract for the product — scope, threat model, out-of-scope, deliverable (findings report + severity classification + reproduction cases), signer, cadence, and how the findings-severity tags flow into a threshold-spec decision.
- **Author the online-eval slice contract.** Online eval (`mod-110`) produces evidence on live traffic, and the tier gate consumes it as *periodic re-evaluation*. In `online-eval-slice-contract.md`, sketch the online-eval slice's contract for the product — metric definitions, sampling design, ground-truth acquisition, cadence, delivery.
- **Sketch the CyBench-style capability-envelope memo.** For a product where the model has network access, code-execution, or security-relevant tooling, in `capability-envelope-memo.md`, sketch the memo that reads CyBench evidence as an *envelope signal* rather than a tier-transition — a capability crossing that does not itself move the tier but *does* force a review of the cybersecurity-attestation clauses (foreshadow chapter `03`).
- **Cross-reference the assurance-case leaves.** In `assurance-case-leaf-map.md`, for each threshold spec, name the assurance-case (`mod-102`) leaf the spec discharges. This foreshadows how the tier-decision artefact composes with the case (chapter `05`).
- **Draft the deferred-criterion memo for one spec that cannot pass at initial release.** In `deferred-criterion-memo.md`, pick one threshold spec whose evidence is realistically not available at the current release (a not-yet-versioned benchmark, a not-yet-hardened harness, a not-yet-negotiated eval-set access clause). Draft the deferred-criterion memo — the criterion, the deferral rationale, the expiry, the compensating control, the signer.
