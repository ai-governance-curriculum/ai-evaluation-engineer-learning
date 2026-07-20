# The Peer-Track Contract Matrix

## Motivation

Chapter `01` gave the programme its running loop. That loop has *inputs* — evidence flowing in from six peer tracks — and *outputs* — artefacts flowing back to those same peers and outward. `mod-101/06` drafted the deferral contract at the shape level: who owes what to whom, in the abstract. `mod-103/04` drew the consumer-side of the four production-peer contracts at the release-gate. This chapter sits between those two: a single, compact **peer-track contract matrix** at the *programme-ownership* altitude, covering all six inputs, that the assurance owner reads before every intake triage and re-reads at every quarterly management review.

Two failure modes motivate a single matrix rather than six separate contract documents.

The first is **contract drift by peer**. Each peer's contract lives in a separate file; over time, the freshness policies, escalation paths, and artefact schemas drift out of alignment with each other. When a case arrives that spans multiple peers (which is the common case at T2 and above), the assurance owner has to reconcile the drift at case time — the operating model's stage-two service time balloons.

The second is **the missing peer**. A new peer track is added to the ecosystem (an agentic-safety team, an infra-security team) and the assurance owner never opens a contract with them; the peer's evidence arrives unpinned, the release-gate consumes it informally, and there is no acceptance test. When an audit asks *how does the programme know the eval-set-security posture is what the attestation claims*, the answer is "we asked" — which is not an answer.

The matrix is the single artefact the programme uses to keep the six inputs coherent and complete.

## Matrix shape

Every peer-track row carries six columns. Read the columns in order; each column answers one question.

| Column | Answers |
| ------ | ------- |
| **Peer track (role, level, family)** | Who is the counterparty? |
| **Artefact schema (or schema pointer)** | What shape does each input take? Where is the schema pinned? |
| **Freshness contract** | How long before an artefact is considered stale? |
| **Sign-off party** | Who on the peer's side is the authoritative signer? |
| **Escalation path when the contract breaks** | If evidence is missing, stale, or warrant-failing, who does the assurance owner call, in what order? |
| **What the programme owes back** | Which artefacts flow back to the peer? |

The matrix is co-signed with each peer's team lead (per `mod-103/04`). It is stored in the assurance programme's Git repository under `peer-contracts/<peer-track>.md` and referenced by the intake worksheet at scope assessment. Changes to the matrix are pull requests, reviewed by the counterparty peer.

## Row 1 — `ai-governance-analyst` (level 15, AI Governance)

**Inputs owed to the programme.**

- The **intake worksheet** — the analyst's structured record of the change under consideration, with system-id, intended-use delta, deployment-tier delta, and jurisdictional-scope delta. Schema: the analyst's intake-form-v*N* pinned in the analyst-track repository.
- The **inventory record** — the current AI-inventory entry for the system-under-change. Schema per ISO/IEC 42001 clause 4 + Annex A information register.
- **First-draft model / system / dataset cards** — the analyst-authored drafts the assurance programme elevates for external audiences (`mod-105`).
- **Jurisdictional scoping** — the analyst's current-jurisdictions record for the system's markets, and the delta since last gate.

**Freshness contract.** Intake worksheet: per-change. Inventory record: continuously current; a check at scope assessment. Cards: per-release-candidate for material changes; per-quarter otherwise. Jurisdictional scoping: per-quarter refresh, on-event when a new regulation lands.

**Sign-off.** Analyst-team lead for the intake worksheet and inventory record; individual analyst plus lead for first-draft cards.

**Escalation.** Missing intake worksheet blocks the intake stage; escalate to the analyst-team lead within one cadence. Missing inventory record for a system that appears in the queue is an inventory-hygiene defect; escalate to the analyst lead and, if unresolved in two cadences, to the head of AI governance.

**What the programme owes back.** The consolidated crosswalk that supersedes the analyst's first draft; the approved card templates so future first drafts converge faster; the interested-parties register update.

## Row 2 — `ai-risk-engineer` (level 25, AI Governance)

**Inputs owed to the programme.**

- The **harm inventory** — versioned, signed, tied to the intended-use and the harm-model methodology of record.
- **Adversarial-eval refresh** — per-release-candidate red-team retest against the current threat model, with coverage attestation.
- **Red-team report** — for T2 and above, a full engagement report with methodology, coverage, findings, and residuals.
- **Guardrail attestation** — per-guardrail effectiveness measurements (pass-rate, false-block rate, benign-degradation).
- **Incident-response depth** — a tested incident-response playbook for the system class, referenced by the release-gate readiness lane (`mod-103/06`).

**Freshness contract.** Harm inventory: per-quarter baseline plus on-event delta assessments. Adversarial-eval refresh: per-release-candidate. Red-team report: annual for T2, per major release for T3, on-event when the threat model updates. Guardrail attestation: per-release-candidate and on guardrail-config change. Incident-response playbook: tested per-quarter, refreshed on-event.

**Sign-off.** AI-risk-engineering lead; safety-benchmark evidence co-signed by any third-party evaluator (`mod-109`).

**Escalation.** Missing adversarial-eval refresh at T2+ is a hard blocker; the release-gate delays. Escalate to the risk-engineering lead within one cadence; if capacity-bound, escalate to the head of AI governance for reprioritisation (per `mod-101/06`).

**What the programme owes back.** Release-gate incorporation of the harm inventory (which harms mapped to which sub-categories, which residuals accepted); post-market feedback on which harms materialised; threshold-update requests when the risk landscape shifts.

## Row 3 — `ai-eval-engineer` (level 30, AI Engineering)

**Inputs owed to the programme.**

- **Application-layer eval evidence** — trace, trajectory, tool-call, RAG-groundedness, and judge-agreement measurements for the release candidate.
- **Online-eval configuration** — the drift-detection slice, coverage-of-intended-use slices, and the online-eval readiness attestation for the post-market handoff.
- **Regression-signal wiring** — the eval-gated CI/CD signal for the release candidate.
- **Trace-based evidence per [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/)** — instrumentation spans conforming to the pinned semantic-convention version (or the peer's documented divergence rationale).

**Freshness contract.** Per-release-candidate for trace / trajectory / judge / eval-gated CI/CD. Rolling 7-day window for online-eval attestations, refreshed at each gate.

**Sign-off.** AI-eval-engineering lead.

**Escalation.** Trace-coverage below the contract's floor for the release-candidate window is a hard blocker at T2+; escalate to the AI-eval lead. Judge-vs-human agreement drift below the threshold is a renegotiation trigger; escalate to the model-eval peer for methodology check before re-consuming.

**What the programme owes back.** The release-gate signal (pass / fail / delayed) so the peer's CI/CD can react; update requests to the online-eval slice when a criterion tightens; the reproducibility-bundle spec for eval evidence (`mod-104/03`).

## Row 4 — `model-evaluation-engineer` (level 30, ML Engineering)

**Inputs owed to the programme.**

- **Statistical framing per threshold** — estimator, confidence interval, sample-size justification for each hard-gate functional-adequacy criterion.
- **Bootstrap-CI methodology** and calibration-methodology-of-record.
- **Benchmark-construction record** (or citation to a public benchmark with its provenance) for each metric.
- **Model-eval reproducibility bundle** — the peer's own reproducibility bundle for benchmark runs (feeds `mod-104/03`).
- **Calibration measurements** where the release-gate consumes probability outputs.

**Freshness contract.** Per-release-candidate for primary property benchmarks; per-model-fine-tune for calibration and disjointness attestations; per-quarter for the benchmark-construction attestation.

**Sign-off.** Model-evaluation-engineering lead.

**Escalation.** An estimator change that has not been negotiated into the consumer contract is a renegotiation trigger, not a case-time override; escalate to the model-eval lead. A benchmark contamination finding is a hard blocker at any tier; escalate immediately to both the model-eval lead and the assurance-programme lead.

**What the programme owes back.** Release-gate incorporation of the peer's statistical framing (which benchmarks / estimators are canonical); post-market drift data so calibration and benchmarks can be maintained; the "needs replacement" list for benchmarks approaching end-of-life.

## Row 5 — `ai-infra-security` (level 35, AI Infrastructure)

**Inputs owed to the programme.**

- **Eval-set-security posture** — attestations on contamination controls, exfiltration controls, tamper-evidence, and holdout hygiene across the model lifecycle.
- **Judge supply-chain attestation** — pinning of the LLM-as-judge model digest, judge prompt versioning, and judge-model allowlisting.
- **Model-extraction risk** — a documented assessment for closed-model API-consumed systems and for provider-side model exposure.
- **Supply-chain provenance** — ML-BOM / SPDX-AI / SLSA / Sigstore artefacts (feeds `mod-104/04`).

**Freshness contract.** Per-release-candidate for ML-BOM, provenance, and judge supply-chain. Per-quarter for the cybersecurity-posture away-goal, per-quarter for eval-set-integrity attestations, on-event when a supply-chain incident lands.

**Sign-off.** AI-infra-security lead; cybersecurity-posture away-goal co-signed by the wider security organisation.

**Escalation.** Signature-verification failure on any supply-chain attestation is a hard blocker; escalate to the security lead and the assurance-programme lead. A newly discovered eval-set-exfiltration path is a hard blocker at any tier and a renegotiation trigger for the contract.

**What the programme owes back.** Release-gate incorporation of the attestations and the threat model; escalation on any release-gate failure caused by a supply-chain or eval-set-integrity finding; feedback on which controls are load-bearing on the release decision.

## Row 6 — `agentic-safety-engineer` (level 40, AI Governance)

**Inputs owed to the programme.**

- **Frontier-agent capability evidence** — dangerous-capability elicitation results for GPAI use cases and for any agentic system in scope for tier-3 gating.
- **Autonomy-envelope attestation** — the current agent's action space, tool allowlist, and human-oversight surface (feeds `mod-108`).
- **Systemic-risk assessment feed** — for Article 55 GPAI systems, the peer's contribution to the systemic-risk assessment (`mod-111`).

**Freshness contract.** Per-major-model-version for capability elicitation; per-release-candidate for the autonomy-envelope attestation; per-quarter for the systemic-risk feed, on-event when a frontier-capability threshold is triggered.

**Sign-off.** Agentic-safety-engineering lead.

**Escalation.** A newly discovered dangerous capability is a hard blocker at any tier; escalate to the peer lead, the assurance-programme lead, and (for GPAI-systemic-risk cases) the head of AI governance in the same escalation event. This peer's evidence often drives escalations that leave the team-scope authority (per `mod-101/06` and chapter `01`).

**What the programme owes back.** Release-gate incorporation of the capability evidence for the specific deployment; feedback from post-market surveillance on agent behaviour in production; the assurance-case framing the peer's evidence lands in.

## The compact matrix

The six rows in one glance. Read this at every intake triage.

| Peer track | Level, family | Key artefacts | Freshness | Sign-off | Escalation on break |
| ---------- | ------------- | ------------- | --------- | -------- | ------------------- |
| `ai-governance-analyst` | 15, Governance | Intake worksheet, inventory record, first-draft cards, jurisdictional scoping | Per-change; per-quarter refresh | Analyst-team lead | Analyst lead → head of governance |
| `ai-risk-engineer` | 25, Governance | Harm inventory, adversarial-eval refresh, red-team report, guardrail attestation, incident-response playbook | Per-quarter baseline; per-release-candidate delta | Risk-engineering lead | Risk lead → head of governance |
| `ai-eval-engineer` | 30, AI Engineering | Trace / trajectory / RAG / judge evidence, online-eval slice, eval-gated CI/CD, OTel Gen-AI spans | Per-release-candidate; rolling 7-day for online-eval | AI-eval-engineering lead | AI-eval lead → programme lead |
| `model-evaluation-engineer` | 30, ML Engineering | Statistical framing, bootstrap CIs, benchmark records, calibration, reproducibility bundle | Per-release-candidate; per-quarter benchmark-construction | Model-eval-engineering lead | Model-eval lead → programme lead |
| `ai-infra-security` | 35, AI Infrastructure | Eval-set-security posture, judge supply-chain, model-extraction risk, ML-BOM / SPDX-AI / SLSA / Sigstore | Per-release-candidate; per-quarter posture | AI-infra-security lead | Security lead → programme lead |
| `agentic-safety-engineer` | 40, Governance | Frontier capability evidence, autonomy envelope, systemic-risk feed | Per-major-model-version; per-release-candidate envelope | Agentic-safety-engineering lead | Peer lead → programme lead → head of governance |

## Cross-peer routing

Some artefacts have two plausible peer owners. The matrix routes them explicitly (extending `mod-102/06`'s routing rule):

- **Judge quality.** AI-eval engineer produces the judge-vs-human agreement measurement; model-eval engineer verifies the judge-vs-human methodology. The matrix carries both rows, and the release-gate consumes them jointly (`mod-103/04`).
- **Fairness.** Risk engineer owns the harm inventory tie-in; model-eval engineer owns the subgroup metric with a CI. Both rows appear; a subgroup metric without a harm-inventory tie-in is a coverage gap.
- **Adversarial evaluation.** Risk engineer owns the adversarial suite as a threat-model artefact; model-eval engineer owns the statistical warrant on attack-success rate. Both rows appear.
- **Trace-instrumentation coverage.** AI-eval engineer owns the coverage measurement; infra-security owns the tamper-evidence on the trace store. Both rows appear.

The rule for routing is unchanged from `mod-101/06`: **assign to the lowest-level role that genuinely requires the skill; the programme links back rather than duplicates.** Where a case is genuinely joint, the matrix carries two rows and the SACM `Artifact` elements cite each.

## Where the matrix lives and how it evolves

The matrix is a Git-tracked, versioned artefact. Every row carries the peer contract's signed-through date (`mod-103/04`) and the current renegotiation state. Reviews happen on a fixed cadence — annually, plus on the named renegotiation triggers of each contract — and are tracked as pull requests against the matrix file.

Changes fall in three classes:

- **Row edits.** A single peer's artefact schema, freshness, or escalation shifts. Pull request; peer lead reviews.
- **Row additions.** A new peer track joins the ecosystem (a fresh cross-modality-eval team, a dedicated evaluation-research group). Pull request; peer lead + head of AI governance review.
- **Row deletions.** A peer track winds down or the programme stops consuming a class of evidence. Pull request; documented rationale; the matrix row is not silently removed — it is *retired* (per `mod-103/04` on contract retirement).

The matrix carries a compact changelog at the top so an auditor can walk it and see what shifted in the last cycle. This is not decorative; it discharges ISO/IEC 42001 clause 9.1 monitoring at the programme level.

## Worked example — the six-person team from chapter `01`

Consider the same six-person assurance team inside the four-hundred-person AI-engineering organisation. Their matrix has six rows plus one addition-in-progress (a nascent cross-modality-eval team that owns the video-and-audio harness).

- The analyst row is stable; the analyst function is distributed (eleven analysts across the product lines) and the assurance-programme analyst is the coordinator.
- The risk-engineer row is under renegotiation: the peer team recently adopted the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) as its methodology-of-record for harm modelling, and the freshness cadence is being tightened from per-quarter to per-two-months for T2 systems.
- The AI-eval and model-eval rows are stable and joint on judge quality; the two peer leads share the effective-challenge review for any judge-related renegotiation.
- The infra-security row was recently amended: a new eval-set-exfiltration threat model was published after an industry incident, and the matrix now carries an added row for the exfiltration-control attestation.
- The agentic-safety row is stable but rarely triggered — only the single T3 system consumes it; when the T3 system's next release candidate lands, the matrix row activates the escalation path immediately.

The compact matrix table (above) is printed on the wall of the team's stand-up area, updated at every quarterly review, and referenced at every intake triage.

## Where this shows up in the rest of the track

- `mod-101/06` — the deferral contract is the input; the matrix is its running instantiation at programme scope.
- `mod-103/04` — the consumer-contract-set is the release-gate-side view; the matrix is the programme-ownership-side view. The two are two views of the same contracts.
- `mod-104/03` and `mod-104/04` — the reproducibility bundles and the supply-chain provenance are two of the matrix's inputs; the matrix pins which peer signs each.
- `mod-108` — the deployment-tier gating draws different freshness cadences from the matrix per tier.
- `mod-109` — the third-party-evaluator interface layers on top of the matrix at tiers that require independent evidence.
- Chapter `03` — the interfaces upward (senior architect, head of AI governance, external supervisors) sit above the matrix; the matrix is the interface downward.
- Chapter `05` — incident-driven roadmap prioritisation reads the matrix to identify which peer's evidence gap an incident closes.

## Summary

- The peer-track contract matrix is a single, compact artefact covering all six peer inputs (analyst, risk, AI-eval, model-eval, infra-security, agentic-safety) at programme-ownership altitude.
- Every row carries the peer, the artefact schema, the freshness contract, the sign-off party, the escalation path, and what the programme owes back.
- Cross-peer artefacts (judge quality, fairness, adversarial eval, trace-instrumentation coverage) carry two rows; the release-gate consumes them jointly.
- The matrix is Git-tracked, versioned, co-signed with each peer's lead, and reviewed on a fixed cadence plus on named renegotiation triggers.
- The matrix is the input side of the operating model; chapter `03` draws the interfaces upward and outward.
- Exercise-02 asks you to draft the six-row matrix for a realistic organisation, defend each row against the counterparty peer, and rehearse the escalation path for a broken contract.
