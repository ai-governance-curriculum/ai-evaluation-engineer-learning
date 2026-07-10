# Consumer Contracts With the Four Peer Tracks Feeding the Gate

## Motivation

Mod-102 chapter `06` introduced the evidence-contract row schema as the *producer-side* interface between the assurance case and each peer track. This chapter takes the same interface from the release-gate's *consumer* side: what the gate expects to arrive from each peer, in what shape, with what warrant, at what freshness, and — the piece the producer schema does not fully cover — *what the gate is committed to consuming* on the other side of the contract.

Four peer tracks feed the gate directly:

- **`ai-eval-engineer` (level 30, AI Engineering).** Trace / trajectory / RAG / judge / online-eval evidence.
- **`model-evaluation-engineer` (level 30, ML Engineering).** Statistical warrant, benchmark evidence, calibration methodology.
- **`ai-risk-engineer` (level 25, AI Governance).** Harm-inventory evidence, safety-benchmark evidence, red-team evidence, guardrail-eval evidence.
- **`ai-infra-security` (level 35, AI Infrastructure).** Supply-chain evidence, eval-set-security evidence, cybersecurity-posture evidence.

The `ai-governance-analyst` (level 15) also feeds the gate — with inventory linkage, jurisdictional watchlist, and first-draft cards — but the interface is thin and largely procedural. Mod-101 chapter `06` (the deferral contract) and mod-102 chapter `06` cover the analyst-side; this chapter focuses on the four production peers whose evidence is directly load-bearing on the release decision.

Getting these contracts right buys three things: (1) the peer tracks own their own methodology and are not asked to re-argue it at every gate; (2) the release-gate does not backfill peer craft, which is the mod-101 charter; (3) the assurance case's leaves each resolve to a *pinned artefact*, which is what the SACM diff and the audit walk depend on.

## The consumer-side contract row

The producer-side row from mod-102 chapter `06` had ten fields (claim ID, owner, artefact, format/storage, warrant, freshness, cadence, sign-off, framework citations, escalation). The consumer-side row adds four:

| Field                          | Content                                                                                                                     |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| Gate criterion IDs it discharges | The list of `GATE-*` criteria from the rubric (chapter `02`) this artefact resolves. One artefact can discharge many criteria. |
| Gate-side acceptance test      | The mechanical check the gate walker performs when the artefact arrives: schema validation, signature verification, warrant extraction. |
| Gate-side consumption commitment | What the gate promises the peer track: what the artefact is used for, what it is *not* used for, retention window on the gate side. |
| Renegotiation triggers         | When the consumer contract itself has to be re-opened (peer track publishes new methodology version, framework change, incident-derived requirement). |

The consumer-side contract set is *co-signed* with the peer track. It is *not* imposed. It is a two-way document because a one-sided contract fails at the first methodology update the peer makes independently.

Storage lives in the same repository as the assurance case, under `evidence-contracts/consumer/<peer-track>.md` (one file per peer), tagged and versioned. The SACM `Artifact` elements cite the consumer-contract clause number they arrived under.

## Consumer contract with `ai-eval-engineer`

**What the peer produces.** Trace instrumentation output (per OpenTelemetry Gen-AI semantic conventions where applicable, or the peer's chosen span schema), trajectory / tool-call scoring, RAG groundedness and context-relevance measurements, LLM-as-judge scores with agreement rate against a human panel, online-eval slice measurements (drift, coverage of the intended-use distribution), and eval-gated CI/CD outcomes for the release candidate.

**What the gate consumes.**

- **Trace-completeness evidence.** For the pilot / canary window preceding the gate, the peer attests that instrumentation coverage exceeded a stated fraction of production sessions, with schema conforming to the pinned span-schema version. This discharges the transparency and adaptability dimensions of the rubric (chapter `02`).
- **Trajectory / tool-use evidence.** For tool-using systems (agents), the peer produces trajectory-correctness measurements with a stated estimator and interval.
- **RAG evidence.** For retrieval-augmented systems, the peer produces context-relevance and answer-groundedness measurements per the peer's methodology.
- **Judge evidence.** For any pipeline using LLM-as-judge, the peer produces the judge-vs-human agreement rate with a stated CI, on a documented held-out set. This is *not* the same artefact as the model-eval peer's methodology check on judge-vs-human; the two rows split (see mod-102 chapter `06`, "when routing is contested").
- **Online-eval evidence.** Drift signals, coverage-of-intended-use measurements, and the online-eval slice's readiness attestation for post-market handoff (mod-110).
- **Eval-gated CI/CD outcomes.** Pass / fail from the CI-side gates run against the release candidate.

**Warrant shape.** Warrants are the peer's own. The consumer contract cites `AI-EVAL evidence-contract v1 §<clause>` and does not re-derive the methodology. The gate-side acceptance test is a schema check and a warrant-extraction check (does the artefact declare its warrant clause, is the clause version supported by the current consumer contract).

**Freshness.** Per-release-candidate for the trace, trajectory, judge, and eval-gated CI/CD artefacts. Rolling-window (e.g., 7-day) for online-eval attestations, refreshed at each gate.

**Sign-off.** AI-eval engineering lead.

**Framework citations.** NIST AI RMF MEASURE-2.5 (accuracy in intended use), MEASURE-2.6 (safety), MEASURE-2.8 (interpretability/explainability), MEASURE-3.1/3.2 (drift and ongoing risk), EU AI Act Article 13 (transparency for deployers), Article 14 (human oversight — where trajectory instrumentation exposes intervention signal), Article 15 (accuracy over the lifecycle). ISO/IEC 42001 clauses 7.5, 8.1, 9.1.

**Renegotiation triggers.**

- The peer publishes a new judge-vs-human methodology version.
- OpenTelemetry Gen-AI semantic conventions change materially.
- A post-market incident reveals a trace-instrumentation blind spot the current contract does not cover.
- The rubric adds a new dimension the current AI-eval contract does not feed.

**Consumption commitment.** The gate uses the artefacts *only* for the criteria the contract discharges. Online-eval artefacts are retained for the AIMS retention window (mod-104 policy); traces are governed by the peer's retention policy (the peer owns the storage). The gate does not re-publish peer-internal artefacts (e.g., raw traces containing user content) to external audiences without a redaction pass owned by the peer.

## Consumer contract with `model-evaluation-engineer`

**What the peer produces.** Benchmark evidence (per-property measurements with named estimators and CIs), calibration measurements (Brier, ECE, or the peer's calibration technique of record), benchmark-construction attestations (train / eval disjointness, representativeness of the calibration set, documentation of holdout selection), cross-modality evidence where applicable, MLPerf-style methodology attestations for infrastructure-tied claims.

**What the gate consumes.**

- **Statistical warrant on the primary functional-adequacy metrics.** Every hard-gate functional-adequacy criterion resolves to a per-property measurement carrying an interval and an estimator, produced by this peer.
- **Calibration evidence.** Where the gate has a calibration criterion (typically at T2 and above), this peer produces it.
- **Benchmark integrity.** Attestation that the benchmark used to discharge a functional-adequacy or robustness criterion is not contaminated by the training corpus. Attestation names the disjointness check and the technique.
- **Statistical warrant on robustness metrics.** For the robustness rubric rows whose metric is statistical (long-tail slice accuracy with a CI, adversarial-attack-success rate with a CI on threat-model T, etc.), this peer's warrant is what the gate consumes. The threat-model *definition* lives with the risk-engineer peer.

**Warrant shape.** Statistical, always. The estimator is named, its assumptions are declared, and the peer's evidence-contract v1 clause is cited. The gate-side acceptance test verifies (a) the estimator is one the current consumer contract accepts, (b) the assumption declarations are present, (c) the benchmark version is one the disjointness attestation covers, and (d) the CI's confidence level matches the rubric row's requirement.

**Freshness.** Per-release-candidate for the primary property benchmarks; per-model-fine-tune for the calibration and disjointness attestations (which may be more stable than per-candidate); per-quarter for the benchmark-construction attestation (the benchmark itself is a peer-owned artefact that does not shift per candidate).

**Sign-off.** Model-evaluation engineering lead.

**Framework citations.** NIST AI RMF MEASURE-1.1 (approaches identified and applied), MEASURE-2.5 (accuracy / representative-of-intended-use), MEASURE-2.7 (security / resilience — cites AI 100-2), MEASURE-4.1 (feedback about measurement efficacy). EU AI Act Article 15 (accuracy, robustness, cybersecurity — the accuracy sub-clause specifically). ISO/IEC 42001 clauses 8.1, 8.2, 9.1. ISO/IEC 25059 functional adequacy / robustness dimensions.

**Renegotiation triggers.**

- The peer changes its estimator of record for a metric class.
- The benchmark is replaced or extended.
- A calibration methodology is added or retired.
- The rubric adds a metric the current model-eval contract does not warrant.

**Consumption commitment.** The gate does not choose the estimator. If the release-owner disputes the estimator's suitability, the dispute is a renegotiation trigger, not an override. The gate cites the peer's evidence-contract clause verbatim in the decision record; the gate does not paraphrase the warrant.

## Consumer contract with `ai-risk-engineer`

**What the peer produces.** Harm inventory (versioned), adversarial / red-team engagement reports with coverage attestation against the threat model, guardrail-eval reports (guardrail-effectiveness measurements), incident-derived learnings and their propagation into the harm inventory, safety-benchmark results where the safety benchmark is one the peer's methodology owns (per AI 100-2 taxonomy categories or per a documented internal threat model).

**What the gate consumes.**

- **Harm-inventory version cited on each release.** The gate refuses to run without a stated harm-inventory version. Where the delta risk-assessment (mod-101 chapter `03`, ISO 42001 clause 8.2) has updated the inventory, the gate cites the delta.
- **Adversarial / red-team evidence.** For each threat-model category in scope for the deployment tier, the peer attests coverage. For higher tiers (T3+), the peer's evidence includes an *independent* red-team report (mod-109) or a documented reason why one is not required.
- **Guardrail-eval evidence.** For each guardrail configured in production, the peer produces a guardrail-effectiveness measurement — pass-rate on adversarial suites, false-block rate, degradation cost on the benign distribution.
- **Safety-benchmark evidence.** For the safety benchmarks the peer's methodology maintains (or contracts to an independent evaluator for), the peer produces measurements with the peer's chosen warrant.
- **Incident-derived learnings.** Where the post-market loop (mod-110) has produced a learning attributable to the system, the peer attests that the learning has been propagated into the harm inventory and is reflected in the gate's rubric.

**Warrant shape.** Procedural + statistical. Harm inventories carry procedural warrant (signed by risk-lead + peer review). Adversarial suites carry statistical warrant on attack-success rate with a CI. Guardrail-eval carries both. Safety-benchmark warrants match the peer's methodology-of-record.

**Freshness.** Per-release-candidate for the adversarial / red-team retest and the guardrail-eval on the current candidate. Per-quarter for the harm-inventory baseline. On-event for incident-derived learnings and for guardrail-eval on guardrail-config change.

**Sign-off.** AI risk engineering lead (with the safety-benchmark evidence co-signed by the third-party evaluator where mod-109 requires).

**Framework citations.** NIST AI RMF MAP (harm identification), MEASURE-2.6 (safety), MEASURE-2.7 (security and resilience — AI 100-2 taxonomy). EU AI Act Article 9 (risk-management system), Article 15 (robustness sub-clause), Article 55 (systemic-risk GPAI, if applicable), Article 26 (deployer obligations for safety). ISO/IEC 42001 clauses 8.2, 8.3 (risk assessment and treatment during operation), Annex A. ISO/IEC 23894 (risk-management method).

**Renegotiation triggers.**

- The threat model changes (new attack category from AI 100-2 update, new incident class from mod-110).
- A new jurisdictional obligation (e.g., a new sector rule or a new EU AI Act delegated act) adds a harm class.
- The peer track adopts a new guardrail-eval technique.

**Consumption commitment.** The gate consumes the harm inventory as the *authoritative source* for what harms the release-gate is protecting against. The gate does not enumerate harms independently; when the gate detects a harm the inventory does not cover, the gate raises a *renegotiation trigger*, not a workaround.

## Consumer contract with `ai-infra-security`

**What the peer produces.** Supply-chain provenance and integrity attestations (ML-BOM / SPDX-AI in the shape mod-104 curates), eval-set-integrity attestations (calibration and eval-set have not leaked to the model provider; exfiltration controls are documented), judge supply-chain pinning (judge model digest, judge prompt versioning, judge-config supply-chain), cybersecurity-posture attestations for the AI system as a whole (per EU AI Act Article 15(4)), and eval-set-integrity across the model lifecycle (holdout hygiene from training through deployment).

**What the gate consumes.**

- **Supply-chain attestation.** The release candidate's ML-BOM / SPDX-AI, model provenance (base model digest, fine-tune configuration digest, dataset provenance references), and code / dependency provenance. Signature verification is a gate-side acceptance test.
- **Eval-set integrity.** Attestation that the calibration set, the eval set, and the safety-benchmark set have not leaked to the model provider or into training data. This bites hardest for closed-model API-consumed systems where the peer's control set is over the client-side surface.
- **Judge supply-chain.** Attestation that the LLM-as-judge is pinned by digest, that the judge prompt is versioned, and that the judge's underlying model is on the supply-chain-allowlist.
- **Cybersecurity-posture attestation.** For high-risk systems under EU AI Act Article 15(4), an attestation on the system's cybersecurity posture. This is typically an *away-goal* to the security assurance case rather than a leaf claim; the gate consumes the version and the SACM cross-reference.

**Warrant shape.** Procedural (policy conformance) + digest-chain integrity (signatures verified). The gate-side acceptance test verifies signatures against the pinned trust root, verifies BOM completeness against the pinned schema, and verifies that all named components have provenance rows.

**Freshness.** Per-release-candidate for BOM, provenance, and judge supply-chain (any of these change per candidate). Per-quarter for the cybersecurity-posture away-goal (unless a security incident forces a fresh attestation).

**Sign-off.** AI infra-security lead (with a countersign from the wider security organisation for the cybersecurity-posture away-goal).

**Framework citations.** NIST AI RMF MEASURE-2.7 (security / resilience — cites AI 100-2). EU AI Act Article 15(4) (cybersecurity). ISO/IEC 42001 clause 8.1, Annex A (AI-specific controls in security-adjacent areas). SR 11-7 model-risk (for the closed-model consumption case where the model provider is a third party under SR 23-4 third-party-relationships guidance).

**Renegotiation triggers.**

- The ML-BOM or SPDX-AI schema is upgraded materially.
- A new supply-chain attack surface (judge exfiltration, prompt injection with data-exfil, model-extraction against a closed API) is added to the threat model.
- The security assurance case away-goal changes owner or shape.

**Consumption commitment.** The gate does not re-verify the peer's methodology; it verifies the *attestation*. The gate does not accept "the peer will attest later" — the attestation must be present at gate time, or the criterion fails and is escalated per the runbook (chapter `05`).

## Cross-peer consistency

Some criteria have evidence from more than one peer. The rubric row splits (mod-102 chapter `06`) — but the release-gate also needs to consume the *joint* evidence coherently. Two examples:

- **Judge quality.** The AI-eval peer produces the judge-agreement measurement; the model-eval peer verifies the judge-vs-human methodology. The gate consumes both: it verifies the AI-eval measurement passes threshold *and* that the model-eval methodology attestation is present.
- **Fairness.** The risk-engineer produces the harm-inventory row and the guardrail-eval; the model-eval peer produces the subgroup metric with a CI. The gate consumes both; a subgroup-metric pass without a harm-inventory tie-in is a coverage gap.

Cross-peer consistency is a *design property* of the rubric (chapter `02`) and a *runtime check* by the gate walker (chapter `01`). It is not a peer contract clause on its own.

## Contract lifecycle

Consumer contracts follow the same lifecycle as producer contracts (mod-102 chapter `06`):

- **Authored** by the assurance program, negotiated with the peer track's lead.
- **Signed** by both sides.
- **Versioned** in Git alongside the assurance case.
- **Cited** by the SACM `Artifact` elements and by each decision record.
- **Reviewed** annually and on the renegotiation triggers named per contract.
- **Retired** when a peer track winds down (rare) or when the release-assurance program stops consuming a class of evidence (also rare).

Retirement is documented, not implicit — an unciti contract that stops appearing in decision records is a governance gap, not a graceful transition.

## What the contract is *not*

- **Not a service-level agreement.** The contract does not bind the peer to a delivery-time in wall-clock. It binds the peer to a *cadence* and a *sign-off party*. Wall-clock urgency lives in the runbook (chapter `05`).
- **Not a set of criteria.** The rubric row is the criterion. The contract governs the artefact the criterion is discharged by.
- **Not a subset of the peer's methodology.** The peer's methodology lives with the peer. The contract cites the peer's methodology-of-record clause; it does not paraphrase it.
- **Not a mechanism for the assurance owner to reshape peer craft.** The contract cannot pull work into the release-assurance program that the deferral contract (mod-101 chapter `06`) has kept out. Any drift is a renegotiation topic, not a unilateral extension.

## Common failure modes

- **Consumer contract exists but is not signed by the peer.** The gate has an interface but no other party. Renegotiation triggers cannot fire.
- **Warrant clause is paraphrased.** The gate cites "bootstrap CI on F1" instead of "MOD-EVAL v1 §4." The peer's methodology drift is not detected.
- **Consumption commitment is unstated.** The peer discovers, at incident time, that raw traces went to an external card unredacted. This breaks the two-way trust the contract requires.
- **Renegotiation triggers are absent.** The rubric adds a dimension; the peer's contract does not cover it; the gap is discovered at audit.
- **One artefact discharges too many criteria.** The gate consumes the same artefact for functional adequacy, robustness, adaptability, and controllability; when the artefact fails, the whole gate collapses because there is no *diversity of evidence*.

## Where this feeds

- Chapter `05` — the runbook uses the consumption commitments to name what the on-call does when a peer's artefact is missing / stale / warrant-failing.
- Chapter `06` — the dashboard's freshness column and the peer-track lane both come from the consumer contract set.
- mod-102 chapter `06` — the producer-side row is the mirror; the two together are what a peer track signs.
- mod-104 — the evidence pipeline enforces the schema and pinning that the consumer-side acceptance tests rely on.
- mod-109 — the third-party evaluator interface layers on top of these four contracts for the tiers that require independent evidence.

## Summary

- The gate is a consumer of four peer tracks' evidence: `ai-eval-engineer` (traces / trajectory / RAG / judge / online-eval), `model-evaluation-engineer` (statistical warrant / benchmarks / calibration), `ai-risk-engineer` (harm inventory / safety benchmarks / red-team / guardrail-eval), and `ai-infra-security` (supply-chain / eval-set-security / cybersecurity posture).
- The consumer-side contract row extends the mod-102 producer-side row with four fields: gate criteria discharged, gate-side acceptance test, gate-side consumption commitment, and renegotiation triggers.
- Contracts are co-signed, versioned, cited by the SACM `Artifact` elements, and reviewed on named triggers. They are not SLAs, not criteria, and not paraphrases of peer methodology.
- Cross-peer criteria (judge quality, fairness) split into two contract rows; the gate walker enforces joint consumption.
- Common failure modes are unsigned contracts, paraphrased warrants, unstated consumption commitments, and evidence over-loading. Fixing each is a design responsibility, not a runtime one.
- The next chapter turns the contracts into the *runbook* the on-call reads when a peer contract's artefact is missing, stale, or warrant-failing.
