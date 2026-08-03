# exercise-05: Incident-DB Back-Feed and Non-Compliance Escalation

**Estimated effort:** 3 hours

## Objective

Author (a) the **external-registry ingest procedure** for one in-scope high-risk deployment, (b) the **match assessment** for one real, cited public incident (from the AI Incident Database or the OECD.AI Incidents Monitor) against that deployment's harm inventory and assurance case, and (c) the walked **non-compliance escalation** from re-review through co-signed disposition with a documented dissent process — landing on one of the five outcome states chapter `05` defines (reaffirm / forced retest / forced downgrade / withdrawal / standing-review update). Close the exercise with a determination on whether the incident (translated onto the picked deployment) also meets Article 3(49) serious-incident thresholds and, if so, how the Article 73 wall-clocks (chapter `02`) run alongside the escalation record.

The exercise is design and authoring. The one hard rule: the incident being matched must be a *real* AIID or AIM record, cited by ID. The whole point of the exercise is grounding in real evidence, not inventing incident content.

## Prerequisites

- Chapter [`05-incident-db-back-feed-and-non-compliance-escalation.md`](../05-incident-db-back-feed-and-non-compliance-escalation.md) — the three external registries; the three-axis matching discipline; the four dispositions; the five outcome states; the co-signing contract; the escalation-record schema; five anti-patterns.
- Chapter [`03-peer-eval-and-risk-signal-into-the-re-review-cycle.md`](../03-peer-eval-and-risk-signal-into-the-re-review-cycle.md) — the five-step re-review procedure and the trigger contract that governs internal signal.
- Chapter [`02-eu-ai-act-article-73-serious-incident-workflow.md`](../02-eu-ai-act-article-73-serious-incident-workflow.md) — the Article 3(49) disjunct rules and the three concurrent wall-clocks the parallel-check invokes.
- Familiarity with `mod-102` chapter `05` (defeaters vocabulary), `mod-103` chapter `05` (second-line effective-challenge signer), `mod-104` chapter `01` and `06` (signed artefacts and supersession discipline), and `mod-108` (tier architecture — forced-downgrade lands on the tier scheme; T3-and-above dispositions escalate to head-of-AI-governance).
- ISO/IEC 42001 clauses 9.3 (management review) and 10.2 (nonconformity and corrective action) — the trigger register, fire register, and escalation record are standing inputs.
- Skim access to the three registries:
  - AI Incident Database — [incidentdatabase.ai](https://incidentdatabase.ai/).
  - OECD.AI Incidents Monitor — [oecd.ai/en/incidents](https://oecd.ai/en/incidents/).
  - MIT AI Risk Repository — [airisk.mit.edu](https://airisk.mit.edu/).

## Problem statement

Two choices must be pinned before authoring:

- **Deployment.** Pick one in-scope high-risk deployment. For coherence, reuse the deployment from exercise-01 or exercise-03; alternatively, pin a new one. The deployment must have an existing assurance case with named claims (Article 9 misuse-resistance, Article 15 accuracy, Article 15 cybersecurity, etc.) that a match can defeat.
- **Public incident.** Pick one real AIID incident or OECD.AI AIM record that is *plausibly related* to the deployment's capability class, deployment context, or supply chain. **Cite the incident ID.** Do not invent the incident content — the exercise's discipline is grounding in a real record.

If the deployment does not have a plausibly-related public incident in AIID or AIM, broaden the deployment shape (e.g., from a narrow internal fraud-triage model to a wider "customer-service assistant" so a wider set of public incidents becomes plausibly-related) until a real match exists. The exercise cannot be run on an invented incident.

Common shapes worth considering:

- **Customer-service assistant** — matches against a wide pool of AIID incidents involving chatbot hallucinations, unauthorised financial advice, customer-support-agent misbehaviour.
- **Hiring or promotion decision-support AI** — matches against AIID incidents involving hiring-tool bias, resume-screener discrimination, or promotion-recommendation disparate impact.
- **Content-moderation AI** — matches against AIID and AIM incidents involving over-moderation of specific speech communities, under-moderation of coordinated harm, or fairness regressions.
- **Medical-imaging classifier** — matches against AIID incidents involving imaging-classifier subgroup regressions or robustness failures on out-of-distribution imaging equipment.
- **Fraud-detection scoring model** — matches against AIID incidents involving false-positive fraud freezes, disparate-impact-on-legitimate-transactions, or adversarial-evasion.
- **Coding assistant** — matches against AIID / AIM incidents involving generated-code vulnerabilities, license-contamination, or unsafe-tool-use.

Pin the deployment (with the specific claims), the AIID / AIM incident ID, the current release candidate, the deployment tier, and the peer-track owners (`ai-risk-engineer` for match methodology, `ai-eval-engineer` for any refresh signal) before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `external-registry-ingest-procedure.md`

The three cadences chapter `05` defines, formalised for the picked deployment.

**Weekly scan** — the scripted query against AIID and AIM new-incidents-since-last-scan. Sections:

- Query template — the exact filter (capability class, deployment context, taxonomy tags) the scan applies. Cite the AIID / AIM query URL structure or API endpoint (mark `<!-- needs-research: verify the current AIID API endpoint and query interface as of 2026-07 -->` where uncertain).
- Scan-artefact class — a content-addressed record produced by every scan (query text + timestamp + returned incident IDs + reviewer). Every scan produces an artefact even when it returns zero matches — the null result is evidence the scan happened.
- Named on-call owner — the release-assurance on-call runs the scan; single named individual with a named backup.
- Store landing — where the scan artefact lands in the content-addressed store (`mod-104` chapter `01`).

**Monthly triage review** — the joint session with the peer `ai-risk-engineer`. Sections:

- Participants — the release-assurance methodology owner + `ai-risk-engineer` peer + release-owner on rotation.
- Inputs — every match assessment produced by the weekly scans in the past month.
- Outputs — borderline-match escalations queued for second opinion; escalation-record drafts for any match assessment above the escalation threshold.
- Store landing — the review record lands as a signed artefact.

**Annual comprehensive walk** — the MIT AI Risk Repository walk. Sections:

- Cadence — annually, calibrated with the ISO/IEC 42001 clause 9.3 management-review cycle.
- Scope — every taxonomy entry in the MIT AI Risk Repository, cross-referenced against the deployment's harm inventory (`mod-102` chapter `06`).
- Output — an amended harm inventory (with new rows for any taxonomy entry not covered) plus, where applicable, amended monitored characteristics in the Article 72 plan (chapter `01`).

**Null-result-still-recorded discipline** — the explicit rule that scan artefacts land in the store even when they return no matches. Chapter `05`'s framing: "the null result is evidence that the scan happened".

**Adjacent registries** — how the procedure accommodates a new registry (a national safety-institute registry, a sectoral registry) — the intake schema, the scan cadence, the escalation rule.

### 2. `match-assessment.md`

The match assessment for the picked incident. **Cite the incident ID** (AIID ID like `Incident 123` or the AIM record identifier) and link to the incident's canonical URL. Sections:

- **Incident summary** — a two-paragraph summary of the incident drawn from the registry's own text, cited verbatim where useful. The summary is *neutral* — it does not editorialise on whether the incident is relevant; the match assessment does.
- **Capability match.** Does the incident involve a capability class present in the deployment's inventory? Reasoning cited — specific capability-class alignment (text generation, image classification, agentic tool-use), specific dissimilarities (single-turn vs multi-turn, autonomous vs human-in-the-loop).
- **Deployment-context match.** Does the incident involve a deployment context present in the deployment? Reasoning cited — user population, industry, regulatory context.
- **Evidence-gap match.** Does the incident implicate a failure mode the assurance case does not have a discharging evidence artefact for? This is chapter `05`'s most-valuable match axis. Reasoning cited — the specific claim, the discharging-evidence artefact class the case has (or lacks), and whether the incident's failure mode is within the coverage of that artefact.
- **Match score** — a rubric the learner designs (e.g., match on each axis binary + weighted; or a 0-3 severity ordinal per axis + aggregate). Chapter `05` does not prescribe the rubric — the exercise's discipline is that the rubric is *documented and applied consistently*.
- **Disposition** — one of the four chapter `05` names: `no action` / `read-only awareness` / `re-review trigger` / `escalation`. Signed by the assurance methodology owner with a rationale linking the disposition to the match score.
- **Store landing** — the match assessment lands as a content-addressed artefact; digest placeholder; DSSE-signed by the assurance owner.

### 3. `re-review-record.md`

If the disposition from artefact 2 was `re-review trigger` or `escalation`, walk the five-step re-review procedure from chapter `03` applied to the picked incident against the affected claim(s). If the disposition was `no action` or `read-only awareness`, still author this artefact as a *hypothetical* walk showing what the re-review *would* look like — the exercise's pedagogical value is in the walk.

Sections (per chapter `03`'s five-step procedure):

1. **Identify the defeated claim.** The specific assurance-case claim the trigger defeats, with the citation to the case.
2. **Pull the discharging evidence.** From the assurance bundle, the artefact class + digest that discharged the claim at gate. Verify the digest still resolves; verify the producer signature. Digests are placeholders.
3. **Refresh or challenge.** Which route the re-review takes — refresh (peer runs the methodology; new signed artefact produced) or challenge (defeater identified in existing evidence; documented). Cite the peer artefact refreshed and its new digest placeholder, or the defeater rationale.
4. **Update the case.** The outcome state proposed: reaffirm / forced retest / forced downgrade / defeat/withdrawal / standing-review update. The rationale connects the refresh / challenge to the case's evidence contract.
5. **Update the store.** The supersession pointer — the assurance bundle for the current release candidate is superseded by the new re-review record; the superseded pointer is the reference; the retention class is unchanged.

Include the wall-clock the re-review runs to (per chapter `03`'s wall-clock discipline — reaffirm within one business week; forced retest within N days; forced downgrade within one business day of co-sign; withdrawal within 24 hours).

### 4. `escalation-record.md`

The escalation record per chapter `05`'s schema. Every field.

- **Trigger reference** — link to artefact 2's match assessment (the AIID / AIM incident ID plus the match-assessment artefact digest).
- **Affected release-candidate** — the assurance bundle identifier for the current release candidate.
- **Affected claim(s)** — the assurance-case claim(s) the trigger defeats or challenges.
- **Evidence walked** — the artefact digests reviewed in the re-review, with reviewer and review-date per artefact (placeholders).
- **Disposition proposed** — one of the five outcome states.
- **Rationale** — the argument for the disposition, referencing evidence, defeaters, and any framework citation (NIST AI RMF `MANAGE-4.1`, ISO/IEC 42001 clause 10.2, EU AI Act Article 20).
- **Signers** — release-owner, second-line effective-challenge signer, and head-of-AI-governance where required by chapter `05`'s co-sign contract (withdrawal, or forced-downgrade at T3+, or adversarial-severity S1).
- **Dissent** — a first-class field with *at least one* plausible documented dissent (the learner authors the dissent). Chapter `05` is emphatic — dissent is documented, not suppressed. Example: the release-owner signs under protest on a forced downgrade because they read the match assessment's evidence-gap axis as weaker than the assurance owner does.
- **Wall-clocks** — the disposition wall-clock plus the corrective-action wall-clock (Article 20, or sector-rule counterpart).
- **Supersession pointer** — the specific superseded assurance-bundle reference the disposition amends.
- **Signing infrastructure** — DSSE-signed by every signer, Rekor-logged, lodged in the store under the same retention class as the underlying assurance bundle (per `mod-104` chapter `06`). Placeholders for the DSSE envelopes and Rekor log-entry URLs.
- **Cross-reference to Article 20 corrective action** — the corrective-action record the escalation drives (or the reasoning that no Article 20 route is required for reaffirm / standing-review update).

### 5. `article-73-parallel-check.md`

A short determination on whether the incident (or the underlying facts of the picked public incident, translated onto the deployment) meets Article 3(49) serious-incident thresholds.

Sections:

- **Article 3(49) disjunct-by-disjunct analysis** — for each of the four disjuncts (death; serious harm to health; serious and irreversible critical-infrastructure disruption; infringement of Union-law fundamental-rights obligations; serious harm to property or environment — chapter `02` splits the last), does the picked incident meet the threshold? Reasoning cited.
- **Wall-clock determination** — if any disjunct is met, the shortest applicable of the three clocks (2 / 10 / 15 days) is named. If no disjunct is met, the reasoning is documented so the assurance owner cannot be second-guessed by an audit six months later.
- **Parallel-run coordination** — if a wall-clock applies, cross-reference to exercise-02's Article 73 workflow: the shared incident identifier, the joint drafting with the DPO if personal data involved, the sector-parallel notifications if sector-regulated (cross-reference to exercise-04 for medical-device deployments).
- **Non-triggering documented rationale** — the explicit rationale for why the incident does NOT trigger Article 73 (where that is the determination). This protects the assurance owner against an audit finding of "should have notified".

## Starter guidance

- **The incident MUST be a real AIID or AIM record.** Do not invent one. The whole point of the exercise is grounding in real evidence. If the picked deployment does not have a plausibly-related public incident, broaden the deployment until it does.
- **A match on any one axis is worth reading.** A match on all three axes is usually a re-review trigger. Chapter `05`'s three-axis discipline is not a threshold — it is a *reading order*.
- **Dispositions are signed artefacts.** Informal downgrades are the anti-pattern chapter `05` warns against — "the re-review runs informally, no signed artefact lands in the store, the release decision is quietly downgraded without an audit trail".
- **Dissent is documented, not suppressed.** Chapter `05` is emphatic — the escalation record's dissent field is first-class. A signer who disagrees signs under protest with a documented objection; the audit reads dissent as a signal about programme health, not as a personal failing.
- **Head-of-AI-governance co-sign is non-optional.** For withdrawal, and for forced-downgrade at T3+. Chapter `05` names the escalation-as-signal-loss anti-pattern — a disposition that escalates to the head-of-AI-governance and never returns leaves the release-owner without a decision. The escalation record's wall-clock is the enforcement.
- **The supersession pointer is what makes the audit trail defensible.** A withdrawal or downgrade that does not supersede the current assurance-bundle version leaves the store in an inconsistent state. Chapter `04` and `05`'s supersession discipline is non-negotiable.
- **The Article 73 parallel-check has to be defensible either way.** If the answer is "not a serious incident under Article 3(49)", the rationale is documented so the assurance owner is not second-guessed later. If the answer is "yes, serious incident", the workflow from exercise-02 runs in parallel.
- **`<!-- needs-research: … -->` markers are legitimate.** Where the AIID API endpoint, the AIM URL structure, or a specific AIID incident's most-current taxonomy tagging would need to be verified, mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `external-registry-ingest-procedure.md` covers all three cadences (weekly scan, monthly triage review, annual comprehensive walk) with named on-call owners, query templates, store landings, and the null-result-still-recorded rule.
- `match-assessment.md` cites a real AIID or AIM incident by ID and canonical URL; the three match axes are each addressed with cited reasoning; the match rubric is documented; the disposition is one of the four chapter `05` names and is signed with a rationale.
- `re-review-record.md` walks the five-step procedure with digest placeholders, wall-clocks, and outcome state; if the disposition from artefact 2 was `no action` or `read-only awareness`, the artefact is a hypothetical walk with that framing stated.
- `escalation-record.md` has every field from chapter `05`'s schema; the signers are correct per the co-sign contract and the tier; at least one plausible dissent is documented; the DSSE / Rekor placeholders and the supersession pointer are present.
- `article-73-parallel-check.md` walks the four Article 3(49) disjuncts with reasoning per disjunct; the wall-clock determination is explicit; the parallel-run coordination or the non-triggering rationale is documented and defensible.
- The whole artefact set is internally consistent — the AIID / AIM ID cited in artefact 2 flows through artefact 4's trigger reference; the affected claims in artefacts 3 and 4 match; the wall-clocks in artefact 4 and artefact 5 are consistent.
- Every place a fact would need to be verified against the current AIID API, the current AIM URL structure, a specific incident's current taxonomy, or the enterprise's own tier scheme is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Retrospective audit query.** In `retrospective-audit-query.md`, design the query — "given a real 2025-2026 incident that later made national news, could our scan have caught it before it made news?" Include the query text, the expected time-to-detection, and the escalation if the answer is "no".
- **National safety-institute registry extension.** In `national-registry-extension.md`, extend the ingest procedure to accommodate a national AI-safety-institute incident registry (mark `<!-- needs-research: … -->` for which national registries have launched by 2026-07). Include the intake schema, the scan cadence, and any language / translation considerations.
- **MIT AI Risk Repository harm-inventory walk.** In `mit-risk-repository-walk.md`, walk the MIT AI Risk Repository taxonomy against the deployment's harm inventory one row at a time — one line per taxonomy entry with covered / not-covered / covered-by-adjacent-inventory disposition. Include the amended harm-inventory diff at the end.
- **Unilateral-reversal audit-finding memo.** In `unilateral-reversal-audit-memo.md`, draft the audit-finding memo for a case where the escalation contract was bypassed — the release-assurance owner reversed the release decision without the co-sign. Cover the finding statement, the root-cause analysis (why the co-sign was bypassed), the corrective action, and the ISO/IEC 42001 clause 10.2 record. This is a self-defence exercise — the memo is the pre-mortem that keeps the anti-pattern from recurring.
- **GPAI systemic-risk integration.** In `gpai-systemic-risk-integration.md`, sketch how the ingest procedure and the escalation contract extend for a GPAI systemic-risk deployment (cross-reference `mod-111`) — the additional AI Office notification channel that runs alongside the Member State market-surveillance authority notification.
