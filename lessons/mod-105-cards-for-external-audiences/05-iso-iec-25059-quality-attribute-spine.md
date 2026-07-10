# The ISO/IEC 25059 Quality-Attribute Spine

## Motivation

A system card that reports metrics without a structuring principle is a bag of numbers. Different releases in the same organisation report different metrics; two vendors' cards for functionally similar systems cannot be compared; a regulator opening the card cannot walk from a *quality property* to the *evidence that discharges it* and back. Chapter `03`'s §4 (quality attributes and evaluation evidence) needs a spine that fixes the shape.

That spine is [ISO/IEC 25059:2023 — *Software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Quality model for AI systems*](https://www.iso.org/standard/80655.html). ISO/IEC 25059 extends the ISO/IEC 25010:2011 (2023 rev) product-quality model with AI-specific quality characteristics; it is the international-standard vocabulary for talking about *what an AI system's quality is made of*.

This chapter shows how to structure the quality-attributes section of the card around ISO/IEC 25059 dimensions, and — critically — how to make each dimension walkable: quality attribute ↔ metric ↔ threshold ↔ eval-report digest ↔ reproducibility bundle ↔ case node. The end result is that a reviewer opening the card can pick any quality attribute and reach the evidence that discharges it, or open the evidence and reach the quality attribute it supports.

## What ISO/IEC 25059 fixes

ISO/IEC 25059 is a *specialisation* of the ISO/IEC 25010 SQuaRE product-quality model for AI systems. The base 25010 model carries eight product-quality characteristics (functional suitability, performance efficiency, compatibility, interaction capability, reliability, security, maintainability, flexibility) and a data-quality model (25012 / 25024). 25059 adds and adjusts characteristics specifically for AI systems.

The core additions and adjustments (at the level of the standard's abstract):

- **Functional adaptability** — the ability of the AI system to adapt its behaviour to changes in inputs, environment, or context without losing functional adequacy.
- **User controllability** — the extent to which a user can meaningfully control the AI system's behaviour and outcomes, including the ability to stop, override, or contest.
- **Transparency** — the extent to which the AI system's behaviour is explicable to relevant stakeholders (users, developers, regulators, third parties).
- **Robustness** — retained from 25010's reliability characteristic, but sharpened for AI: the ability of the AI system to retain functional adequacy under adversarial, out-of-distribution, or perturbed inputs.
- **Societal and ethical risk mitigation** — the extent to which the AI system's design, deployment, and use mitigate societal and ethical risks including fairness, non-discrimination, and privacy.
- **Intervenability** — the ability of authorised parties to intervene in the AI system's operation.

The exact naming and numbering of characteristics in ISO/IEC 25059 evolves across the standard's revisions; the chapter names the ones a card author will encounter without pinning to a specific character-count that the standard itself may adjust.

<!-- needs-research: enumerate the full and current list of quality characteristics and sub-characteristics in ISO/IEC 25059:2023 (and any amendments through 2026), including the exact naming and the ISO/IEC 25010:2011/2023 characteristics it inherits vs. adjusts vs. adds — cite the specific clause numbers. -->

## The card section, structured

The quality-attributes section of the system card is a table (or a repeated block) with one row per quality attribute the release claims fitness on. The row shape:

```yaml
quality_attributes:
  - attribute: "functional-adequacy"                # ISO/IEC 25059 characteristic
    subattribute: "task-completion-correctness"     # sub-characteristic, if the standard names one
    intended_purpose_scope: "primary-classification-task"
    metrics:
      - metric_id: "metric:macro-f1"
        metric_family: "iso-25059:classification-correctness"
        value: 0.912
        ci_95: [0.897, 0.926]
        threshold: 0.85
        threshold_ci_lower_floor: 0.83
        threshold_rationale_content_address: "sha256:6dd1..."
        eval_report_content_address: "sha256:74a1..."
        reproducibility_bundle_content_address: "sha256:9922..."
        eval_set_id: "harm-eval-set/v3.2"
        eval_set_content_address: "sha256:012c..."
        sacm_artifact_id: "art:eval-report:rc-2026-05-07:gate-fa-01"
    case_node: "goal:G1.S1.G-25059-functional-adequacy"
  - attribute: "robustness"
    subattribute: "adversarial-robustness"
    intended_purpose_scope: "primary-classification-task"
    metrics:
      - metric_id: "metric:attack-success-rate"
        metric_family: "iso-25059:robustness-adversarial"
        value: 0.031
        ci_95: [0.019, 0.049]
        threshold_upper_bound: 0.05
        threshold_rationale_content_address: "sha256:aa02..."
        eval_report_content_address: "sha256:c33d..."
        reproducibility_bundle_content_address: "sha256:beef..."
        eval_set_id: "adversarial-eval-set/v2.1"
        eval_set_content_address: "sha256:4b12..."
        sacm_artifact_id: "art:redteam-report:rc-2026-05-07:gate-rb-02"
    case_node: "goal:G1.S1.G-25059-robustness"
```

Six invariants over each row:

- **Every row names a case node.** A quality attribute reported on the card without a case node it discharges is broken — the reviewer cannot reach the argument that says "meeting this threshold matters."
- **Every metric names a threshold.** A quality attribute reported without a threshold is uninterpretable — the reviewer cannot decide whether the number is good.
- **Every threshold has a rationale.** The rationale content-address points at a document (a threshold-setting brief) that explains *why* this threshold was chosen. Chapter `05` of mod-102 (assurance case audit) is where a defeater against the threshold-setting brief lives.
- **Every metric has a CI.** A point estimate without a CI cannot survive statistical scrutiny; the ISO/IEC 25059 spine assumes bootstrap CIs (or an equivalent) throughout. Mod-104 chapter `03` names the reproducibility bundle that carries the seeds a reviewer needs.
- **Every metric names the eval set by content-address.** A card that reports macro-F1 on "our eval set" without pinning the set to a digest is broken; a reviewer six months later cannot reconstruct.
- **Every metric names the reproducibility bundle by content-address.** A third-party evaluator (mod-109) reruns the bundle, not the metric; a card without a bundle pointer cannot be independently verified.

## The mapping — quality attributes to metrics

The card author's harder problem is the *choice of metric* per quality attribute. ISO/IEC 25059 does not name specific benchmarks; it names quality characteristics and sub-characteristics. The mapping from quality characteristic to metric is a program choice that the assurance case documents.

Two rules make the mapping defensible.

- **The mapping is written down before the release-gate runs.** A brief per attribute (`quality-attribute-to-metric-mapping-v1.md`) lists, for each attribute, the metrics that will discharge it, the eval sets they run against, the thresholds, and the rationale. The brief is signed and content-addressed; the card cites its digest.
- **The mapping is challenged.** Chapter `05` of mod-102 (assurance case audit) asks: does this metric measure this quality attribute? Are there sub-characteristics the metric does not touch? Are there population subgroups the eval set does not cover? A defensible mapping documents the answers, including where the mapping is thin. A card that reports macro-F1 as the sole discharge of *functional adequacy* has probably not asked the question — macro-F1 doesn't touch task-completion-latency, tool-use correctness, or long-tail-subgroup performance.

An indicative mapping (the actual mapping depends on the system's intended purpose and jurisdiction):

| ISO/IEC 25059 characteristic         | Sub-characteristic (illustrative)      | Candidate metric family                                                                                                                                            |
| ------------------------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Functional adequacy                  | Task-completion correctness             | Task-specific ground-truth metrics (accuracy, F1, BLEU, ROUGE, exact-match), LLM-as-judge with agreement estimates, per-subgroup breakdowns.                       |
| Functional adequacy                  | Task-completion latency                 | End-to-end latency percentiles per task class; time-to-first-token; time-to-completion.                                                                             |
| Functional adaptability              | Distributional shift retention          | Cross-domain evaluation, cross-time evaluation, per-jurisdiction subgroup metrics.                                                                                  |
| Reliability                          | Availability & correctness under load   | Availability SLIs, error-rate under load, per-region reliability.                                                                                                   |
| Robustness                           | Adversarial robustness                  | Attack-success-rate (jailbreak, prompt-injection), red-team-engagement pass-rate, cybersecurity-eval results (per CyberSecEval, per SAIF / MITRE ATLAS taxonomy).    |
| Robustness                           | Out-of-distribution retention           | OOD detection metrics, calibration under shift, abstention correctness.                                                                                             |
| User controllability                 | Steerability & override                 | Instruction-following on override prompts; refusal / opt-out consistency; user-preferences respected metrics.                                                       |
| Transparency                         | Explicability                           | Explanation coverage; citation/attribution correctness (for RAG); model-card completeness relative to a checklist.                                                   |
| Intervenability                      | Human-oversight support                 | HITL escalation-rate, override-correctness, kill-switch latency.                                                                                                     |
| Societal & ethical risk mitigation   | Fairness (allocative)                   | Per-subgroup disparity metrics with CIs; demographic-parity, equal-opportunity gaps.                                                                                 |
| Societal & ethical risk mitigation   | Fairness (representational)             | Stereotype-evaluation results, per-subgroup harm-eval results.                                                                                                       |
| Societal & ethical risk mitigation   | Privacy                                 | PII-in-output rate, memorisation-eval results, membership-inference resistance.                                                                                      |
| Security (25010, retained)           | Cybersecurity                           | Prompt-injection resistance, model-extraction resistance, tool-use safety (per `ai-infra-security` peer, level 35).                                                  |
| Maintainability / Flexibility        | Update-safety                           | Regression-eval pass-rate between versions, per-release drift, PCCP change-envelope compliance (FDA-regulated systems; mod-107).                                     |

Two notes on the table:

- The metric families are illustrative, not exhaustive. A card built for a specific product will trim, extend, or replace rows to match the intended purpose. Chapter `05` of mod-102 audits the choice.
- Metric names in the "candidate metric family" column are not benchmarks — they are metric shapes. A card cites a specific benchmark (e.g., MMLU, BIG-Bench, HELM, MATH, CyberSecEval, TruthfulQA, MMMU, HumanEval, SWE-Bench, TAU-Bench) or an internal eval set by digest; chapter `03` walked how the frontier labs cite these on their public cards.

## The walk end-to-end

A reviewer opening the quality-attributes section and following a single row (`functional-adequacy → macro-F1 = 0.912`) walks:

1. **Read the row on the card body** — attribute, sub-attribute, intended-purpose scope, metric name, value, CI, threshold, threshold rationale.
2. **Follow the head pointer** — `quality_attributes[...].metrics[0].eval_report_content_address = sha256:74a1…`.
3. **Resolve the eval report** — fetch bytes, re-canonicalise, re-hash, verify producer signature (`model-evaluation-engineer`).
4. **Cross-check the eval set** — the eval-report's `lineage.dataset` field carries `sha256:012c…` and the card's `eval_set_content_address` carries `sha256:012c…`; they match. Fetch the eval-set integrity attestation from mod-104 chapter `05`.
5. **Cross-check the threshold rationale** — fetch `sha256:6dd1…`, read the brief, confirm the threshold is bound to (a) an intended-use requirement, (b) a comparison against an established baseline, or (c) a statistically warranted floor.
6. **Rerun the reproducibility bundle (optional but available)** — under a third-party evaluator handoff (mod-109), fetch `sha256:9922…`, execute the bundle end-to-end, confirm the reported number reproduces within CI.
7. **Reach the case** — `sacm_artifact_id = art:eval-report:rc-2026-05-07:gate-fa-01` maps to `goal:G1.S1.G-25059-functional-adequacy` in the assurance case.

Seven steps. Every quality attribute reported on the card is walkable in this way. A row that is not walkable is not defensible.

## The reverse walk

The card is walkable in reverse: an evaluator opening a report in the store can walk back to the card and to the case.

1. **Open the eval-report bytes at `sha256:74a1…`.**
2. **Read the record's `lineage.evaluator` and `context.platform` fields** to confirm which peer produced it.
3. **Query the index by `record_digest = sha256:74a1…`** (mod-104 chapter `01`) to find the `sacm_artifact_id`.
4. **Query the case at `sacm_artifact_id`** to find `goal:G1.S1.G-25059-functional-adequacy`.
5. **Query the card by `evidence_pointers.*.evidence_content_address = sha256:74a1…`** to find `quality_attributes[attribute=functional-adequacy]`.
6. **Read the row on the card body** to see how the number is presented to an external audience.

The reverse walk is what a third-party evaluator uses in practice. They arrive with a report in hand; they need to know what claim it supports and what card discloses it. The index (mod-104 chapter `01`) is what makes the reverse walk efficient.

## Interaction with the impact-assessment section (chapter `04`)

A quality-attribute finding is often the *evidence* for an impact-assessment finding. When per-subgroup fairness metrics show a 12-point disparity between subgroup A and subgroup B, that fact is *both* a quality-attribute row (`societal-and-ethical-risk-mitigation.fairness-allocative`) and the evidence for an impact-assessment finding (`imp:IAI:F-014`, adverse impact on subgroup B). The card's cross-reference:

- The quality-attribute row cites `sacm_artifact_id = art:eval-report:rc-2026-05-07:subgroup-fairness-01`.
- The impact-assessment finding's `evidence_pointers` cites the same `content_address` for the subgroup-fairness eval report.
- The case has two goals discharged by the same evidence node: `goal:G1.S1.G-25059-fairness` and `goal:G1.S4.G-impact-F-014-evaluated`.

The evidence is not double-counted; the same node discharges two different goals. This is the value of the DAG shape from mod-104 chapter `01`.

## Interaction with the safety-evidence summary (chapter `03` §5)

Robustness and cybersecurity metrics appear in *both* the quality-attributes section and the safety-evidence summary. The two sections read to different audiences: the quality-attributes section is walkable by an ISO/IEC 25059-fluent reviewer against a formal quality model; the safety-evidence summary is walkable by an adversarial reviewer against a threat model.

The card's shared discipline:

- The metric appears once in each section, with the same value, the same CI, the same eval-report content-address.
- The quality-attributes section reports the metric against a fixed threshold; the safety-evidence summary reports the metric against the residual-risk narrative.
- If the numbers differ across sections, the card is broken.

Chapter `07` returns to how the safety-evidence summary is redacted for public disclosure (attack payloads and canary tokens are omitted) without breaking the shared-metric discipline.

## Anti-patterns

- **Point estimates without CIs.** A macro-F1 of 0.912 without a CI is not walkable — the reviewer cannot decide whether it clears the threshold within statistical warrant. Every metric row carries a CI (mod-104 chapter `03` gives the reproducibility bundle that carries the seeds).
- **Metric-of-convenience.** Reporting a metric because it is easy to compute (top-line accuracy on a public benchmark) rather than because it discharges the quality attribute. Chapter `05` of mod-102 audits this.
- **Threshold-of-convenience.** Choosing a threshold *after* the metric is measured so that the metric passes. The threshold's rationale content-address is versioned; if the threshold moves, the version bumps and the rationale documents why.
- **Missing eval-set pin.** Reporting on "our eval set" without a content-address. A reviewer six months later cannot walk the row.
- **Quality attribute claimed but not evaluated.** A card that lists *user controllability* as a quality attribute but reports no metric on it is over-claiming. Either report a metric or drop the attribute from the section.
- **Aggregate-only reporting.** A card that reports only overall metrics without per-subgroup breakdowns has broken the disaggregation move Mitchell et al. built the base card around (chapter `01`).

## Summary

- The ISO/IEC 25059 quality-attribute spine structures §4 of the system card so a reviewer can walk from a quality attribute to a metric to an eval report to a reproducibility bundle to a case node — and back.
- Every quality-attribute row on the card carries: attribute, sub-attribute, intended-purpose scope, one or more metrics with values and CIs, thresholds and their rationale, eval-report content-address, reproducibility-bundle content-address, eval-set content-address, and `sacm_artifact_id`.
- The mapping from quality characteristic to metric is a program choice, written down as a signed brief, and audited under mod-102 chapter `05`. Metrics-of-convenience and thresholds-of-convenience are the primary defeaters.
- Quality-attribute findings often serve double duty as impact-assessment evidence (chapter `04`) and as safety-evidence-summary content (chapter `03` §5); the DAG shape lets one signed node discharge multiple goals without double-counting.
- Chapter `06` picks up C2PA content-provenance for GenAI outputs and the disclosure-vs-secrecy trade-offs (attack payloads, PII, decontamination canaries).
