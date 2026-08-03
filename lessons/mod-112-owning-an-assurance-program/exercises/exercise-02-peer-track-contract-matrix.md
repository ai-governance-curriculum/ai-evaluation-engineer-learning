# exercise-02: Peer-Track Contract Matrix

**Estimated effort:** 3 hours

## Objective

Author the **peer-track contract matrix** for the organisation pinned in exercise `01`. The matrix is the single compact artefact — six rows, one row per peer track — that the assurance owner reads at every intake triage, that each peer-team lead co-signs, and that the auditor consults when they ask "how does the programme know the eval-set-security posture is what the attestation claims?" The exercise also rehearses the escalation path for a broken contract so that the failure-mode row is more than an abstraction.

This exercise is design and authoring, not solving. Placeholder role-name fields and `<!-- needs-research: … -->` markers are legitimate answers where a peer-track schema is not yet pinned, or where a specific standard's clause number would need verification against the current text.

## Prerequisites

- Chapter [`02-peer-track-contract-matrix.md`](../02-peer-track-contract-matrix.md) — the six columns; the six rows; the cross-peer routing rules; the matrix's living-document conventions.
- Exercise [`exercise-01`](exercise-01-operating-model-and-effective-challenge-convention.md) — the operating model the matrix feeds; pin the same organisation.
- Familiarity with [`mod-101-release-assurance-position`](../../mod-101-release-assurance-position/) chapter `06` (the deferral contract at shape level) and [`mod-103-release-gate-architecture`](../../mod-103-release-gate-architecture/) chapter `04` (the consumer-contract-set at the release-gate).
- Familiarity with the six peer-track role registries: `ai-governance-analyst` (level 15), `ai-risk-engineer` (level 25), `ai-eval-engineer` (level 30), `model-evaluation-engineer` (level 30), `ai-infra-security` (level 35), `agentic-safety-engineer` (level 40).
- Skim access to the [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/), the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook), and the CycloneDX / SPDX / SLSA / Sigstore substrate cited by `mod-104` chapters `04` and `05`.

## Problem statement

Carry the same organisation as exercise `01` — same inventory count, same tier distribution, same programme-team size, same jurisdictional / sector posture. The matrix must be defensible against that specific organisation, not against a generic mid-size company. If the organisation has no T3 systems, the agentic-safety row is thin but not absent (the row activates the moment a T3 candidate enters the queue). If the organisation has no EU exposure, the peer contracts do not carry EU AI Act clauses but they still carry the equivalent obligations under the local horizontal regime.

Explicitly consider the following complications when drafting:

- **A missing peer.** If the organisation does not yet have a named `agentic-safety-engineer` counterparty, the matrix row still exists — either pointing at a placeholder role the head of AI governance owes the programme, or at an interim discharge via the risk-engineer role with an explicit renegotiation trigger to migrate to the dedicated peer once hired. Do not silently omit the row.
- **A joint peer.** For the cross-peer artefacts (judge quality, fairness, adversarial evaluation, trace-instrumentation coverage), *both* peer rows appear in the matrix; the rule is unchanged from chapter `02` — the matrix carries two rows and the release-gate consumes them jointly.
- **A contract-under-renegotiation.** At least one row's freshness cadence or artefact schema should be under active renegotiation (a peer adopted a new methodology-of-record; a supply-chain incident triggered a new attestation class; a tier moved from T1 to T2). Represent the renegotiation state in the row.

## Requirements

Produce four artefacts in a single `peer-contracts/` directory, plus one row-per-peer file in a `peer-contracts/rows/` subdirectory.

### 1. `peer-contracts/rows/` — one file per peer

Six files, one per peer, named `<peer-track-slug>.md`. Each file carries the six columns from chapter `02` in full detail:

- **Peer track (role, level, family).** Role slug, level number, family (AI Governance, ML Engineering, AI Engineering, AI Infrastructure).
- **Artefact schema (or schema pointer).** For every artefact the peer owes the programme, name the artefact and pin its schema (or mark `<!-- needs-research: schema not yet pinned in the peer-track repository -->` where the schema is not stable). At minimum, the artefact list from chapter `02` for that peer must be covered.
- **Freshness contract.** Per-artefact freshness expectation with the pinned cadence — per-change, per-release-candidate, per-quarter, per-major-model-version, on-event. State the wall-clock trigger (calendar cadence, event class, or both).
- **Sign-off party.** The role slug of the peer-side signer for each artefact. State whether co-signature with a third party (an external evaluator per `mod-109`, the wider security organisation, a sector-compliance function) is required.
- **Escalation path when the contract breaks.** A numbered sequence: first counterparty, cadence to escalate, second counterparty, cadence to re-escalate, terminal counterparty (typically the head of AI governance, and for GPAI-systemic-risk-adjacent cases, direct to the head plus the senior architect). Include the specific failure classes that trigger the path — missing evidence, stale evidence, warrant-failing evidence.
- **What the programme owes back.** For each artefact the peer owes in, name the artefact class the programme owes back — release-gate incorporation, post-market feedback, threshold-update requests, revised harm-mapping tie-ins, the assurance-case framing the peer's evidence lands in.

The six files, at minimum:

- `ai-governance-analyst.md`
- `ai-risk-engineer.md`
- `ai-eval-engineer.md`
- `model-evaluation-engineer.md`
- `ai-infra-security.md`
- `agentic-safety-engineer.md`

### 2. `peer-contracts/matrix.md`

The compact matrix — the six rows collapsed into the six-column table from chapter `02` for at-a-glance reading. This is the artefact printed on the wall of the team's stand-up area and re-read at every intake triage. Include the changelog stanza at the top (last-updated date, last-updated author, the specific row and column that changed, the pull-request pointer). Include the co-signature block at the bottom (one signature per peer-team lead, with a signed-through date).

### 3. `peer-contracts/cross-peer-routing.md`

The cross-peer routing rules for artefacts with two plausible owners. Extend `mod-102` chapter `06`'s routing rule with the specifics for the pinned organisation:

- **Judge quality.** Which peer owns the judge-vs-human agreement measurement (AI-eval per chapter `02`), which peer verifies the judge-vs-human methodology (model-eval), and how the release-gate consumes both jointly.
- **Fairness.** Which peer owns the harm-inventory tie-in (risk-engineer), which peer owns the subgroup metric with a confidence interval (model-eval), and how the release-gate rejects a subgroup metric without a harm-inventory tie-in as a coverage gap.
- **Adversarial evaluation.** Which peer owns the adversarial suite as a threat-model artefact (risk-engineer), which peer owns the statistical warrant on attack-success rate (model-eval), and how both rows discharge the release-gate criterion jointly.
- **Trace-instrumentation coverage.** Which peer owns the coverage measurement (AI-eval), which peer owns the tamper-evidence on the trace store (infra-security), and how the release-gate reads the two rows against each other.

For each routed artefact, state the SACM `Artifact` element citations from `mod-102`, the freshness cadence, and the failure-mode that surfaces when the two rows drift out of alignment.

### 4. `peer-contracts/escalation-rehearsal.md`

A rehearsal of the escalation path for at least three broken-contract scenarios drawn from the pinned organisation. Each scenario is a short worked walkthrough — the failure, the escalation cadence, the terminal disposition — with the deferral log's expected row as the output. Cover at least:

- **A missing adversarial-eval refresh at T2+.** The risk-engineer team is capacity-blocked and cannot deliver the refresh for a scheduled release-candidate. Walk the path: assurance owner notes the missing evidence at scope assessment, escalates to the risk-engineering lead within one cadence, receives an accepted-next-cycle response, walks the deferral to the head of AI governance for reprioritisation (per `mod-101/06`), logs the deferral row, communicates the delay to the release-owner team, updates the operating model's dashboard.
- **A signature-verification failure on a supply-chain attestation.** The infra-security peer's ML-BOM signature fails verification on a release-candidate. Walk the path: assurance owner rejects the evidence at pipeline-provisioning, escalates to the security lead and the programme lead in the same event, blocks the release-gate, walks the incident-response playbook, resolves either into a re-signed attestation and re-run gate, or into a supply-chain incident with a `mod-104` chapter `04` follow-up.
- **A benchmark-contamination finding on a canonical benchmark.** The model-eval peer surfaces a contamination finding on a benchmark cited as state-of-the-art in the current criterion set. Walk the path: assurance owner escalates immediately to the model-eval lead and the programme lead, walks the criterion set for every release that cites the benchmark, initiates a criterion-set update (a MAJOR bump per `mod-104` chapter `06`), coordinates the peer's benchmark-replacement work, updates the exception log for every affected release.

For each scenario, state the wall-clock service time from breakage to resolution, the specific artefacts that land in the deferral / exception / decision logs, and the operating-model handbook section that governs the response.

## Starter guidance

- **Ground the matrix in the pinned organisation, not in the generic worked example.** A six-person programme inside a four-hundred-person AI org has different freshness cadences from a five-person programme inside a fifty-person AI org.
- **The matrix is a controlled document.** Pull requests, peer-team-lead review, signed changelog. Do not draft the matrix in a shared narrative document that anyone can edit — the audit-walk needs the change history.
- **Cross-peer rows are two rows, not a merged one.** The release-gate consumes them jointly, but the matrix routes them separately. This is the same discipline as `mod-101/06`: **assign to the lowest-level role that genuinely requires the skill; the programme links back rather than duplicates.**
- **Escalation paths terminate — always.** Every escalation path has a terminal counterparty (typically the head of AI governance). A path that loops back to the same peer without a terminal counterparty is a broken path and a governance defect.
- **The programme owes back, not just consumes.** Every row's "what the programme owes back" column is what keeps the peer contract bidirectional and durable. Rows where the programme's owed-back column is empty are extractive rows and will not survive the peer's next capacity review.
- **A missing peer is a matrix row with a renegotiation trigger, not a matrix omission.** If the organisation does not yet have a named agentic-safety-engineer, the row still exists and either points at a placeholder role or names the interim discharge; the matrix records the migration trigger.
- **The renegotiation state is a row, not a footnote.** A row under active renegotiation carries the current state (the artefact schema or freshness that is changing, the target date, the reason). Auditors reading the matrix should see the renegotiation as an active line item, not a comment appended to the row.
- **`<!-- needs-research: … -->` is a legitimate answer** for schema pointers that are not yet pinned in the peer-track repository, for standards clauses that would need verification against the current text, and for organisation-specific role-name conventions the exercise scope does not fix.

## Acceptance criteria

You have succeeded if:

- `peer-contracts/rows/` contains six files, one per peer track, each with the full six-column detail — role / level / family; artefact schema (or pointer); freshness contract; sign-off party; escalation path with numbered steps and terminal counterparty; what the programme owes back. Every artefact the peer owes in from chapter `02`'s enumeration is covered.
- `peer-contracts/matrix.md` collapses the six rows into the compact six-column table, with a changelog stanza at the top and a co-signature block at the bottom.
- `peer-contracts/cross-peer-routing.md` covers judge quality, fairness, adversarial evaluation, and trace-instrumentation coverage, with the two-row routing rule, the SACM `Artifact` citations, and the misalignment-detection signal for each.
- `peer-contracts/escalation-rehearsal.md` walks at least three broken-contract scenarios (missing adversarial-eval refresh, signature-verification failure on a supply-chain attestation, benchmark-contamination finding), each with the wall-clock service time, the deferral / exception / decision-log rows, and the handbook section that governs the response.
- Every row is defensible against the pinned organisation from exercise `01`, not against a generic mid-size company.
- At least one row carries an active renegotiation state (the artefact / freshness under change, the target date, the reason).
- If the organisation lacks a named agentic-safety-engineer, that row is present with a placeholder role or an interim-discharge note plus a migration trigger; the row is not silently omitted.
- Every escalation path terminates at a named counterparty (typically the head of AI governance, with the senior architect added for GPAI-systemic-risk-adjacent cases per chapter `03`).
- Every row's "what the programme owes back" column is filled with a specific artefact class (release-gate incorporation, post-market feedback, threshold-update request, revised harm-mapping tie-in), not left empty.

## Stretch goals

- **Draft the peer-onboarding worksheet.** In `peer-onboarding.md`, produce the worksheet a new peer-team lead fills in when their team joins the matrix — the artefacts they can commit to owing, the freshness cadence they can support, the sign-off party's role slug, the escalation path they accept, and the artefact classes they expect back.
- **Cross-map to the release-gate consumer contract.** In `release-gate-consumer-crosswalk.md`, walk each row of the matrix and pin which `mod-103` chapter `04` consumer-contract row consumes it. The two views should reconcile row-for-row.
- **Draft the annual peer-contract review packet.** In `annual-review-pack.md`, produce the pack the programme lead assembles for the annual peer-contract review — health metrics per row (evidence delivered on cadence, escalations logged, warrant-failing evidence surfaced), renegotiation triggers activated, contract-retirement candidates.
- **Add a seventh row for a nascent peer.** In `peer-contracts/rows/<nascent-peer>.md`, draft the row for a peer track that the pinned organisation does not yet have but expects to add in the next planning cycle (a cross-modality-eval team, a dedicated evaluation-research group, an internal red-team). Include the addition-in-progress state and the target activation date.
- **Draft the matrix's Git workflow.** In `matrix-git-workflow.md`, formalise the pull-request template, the reviewer set (which peer-team leads review which rows), the merge criteria, and the CODEOWNERS mapping the matrix repository uses to route reviews.
