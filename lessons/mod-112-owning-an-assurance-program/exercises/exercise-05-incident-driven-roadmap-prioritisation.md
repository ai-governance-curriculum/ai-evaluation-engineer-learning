# exercise-05: Incident-Driven Roadmap Prioritisation

**Estimated effort:** 3 hours

## Objective

Run the **incident-driven roadmap-prioritisation ritual** against a real incident from the [AI Incident Database](https://incidentdatabase.ai/) or the [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents), for the assurance programme pinned in exercises `01`–`04`. Translate the incident into concrete release-gate evidence-gap rows, rank the resulting queue using the `(likelihood × severity) ÷ cost` formula, produce the escalation packet for gaps whose closure requires peer-track investment beyond the programme's authority, defend the ranking against your peer leads, and prepare the quarterly roadmap pack the head of AI governance signs.

This exercise is design and authoring, not solving. `<!-- needs-research: … -->` markers are legitimate answers where an incident record's specifics would need verification against the source database at reading time, or where a peer-track's capacity would need verification against the peer's current planning cycle.

## Prerequisites

- Chapter [`05-incident-driven-roadmap-prioritisation.md`](../05-incident-driven-roadmap-prioritisation.md) — the four incident-signal sources; the four-question incident-to-gap translation; the ranking formula; the reactive-vs-preventive split; the escalation packet; the quarterly ritual; the mental-health-disclosure worked example.
- Exercises [`exercise-01`](exercise-01-operating-model-and-effective-challenge-convention.md)–[`exercise-04`](exercise-04-build-vs-buy-platform-fit-gap-analysis.md) — the pinned organisation, the operating model, the peer-contract matrix, the interfaces, the tooling substrate. The ritual reads from all four.
- Familiarity with [`mod-101-release-assurance-position`](../../mod-101-release-assurance-position/) chapter `06` (the deferral contract's failure-mode row shapes the reactive vs preventive split), [`mod-102-assurance-case-engineering`](../../mod-102-assurance-case-engineering/) chapter `05` (the audit passes for unstated assumptions, defeaters, and diversity of evidence — the pattern the ritual applies at programme scope), and [`mod-110-post-market-surveillance`](../../mod-110-post-market-surveillance/) (the post-market signals feed the same queue).
- Skim access to the four incident-signal sources:
  - [AI Incident Database (AIID)](https://incidentdatabase.ai/) — community-maintained database of publicly-reported AI incidents. The Goals / Methods / Failures (GMF) taxonomy is useful for grouping.
  - [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents) — the intergovernmental incident monitor. Lower volume, higher curation, tied to policy-relevance signals. Verify current scope and update cadence at reading time.
  - [MIT AI Risk Repository](https://airisk.mit.edu/) — a repository of AI-risk taxonomies, incident sources, and academic risk categorisations. Useful for the categorisation pass.
  - The pinned organisation's own near-miss log — the soft-fails, deferred approvals, exception approvals, and post-market-surveillance signals from `mod-110` that did not rise to serious-incident status.

## Problem statement

Pick one incident (or one small set of related incidents) from AIID or the OECD.AI Incidents Monitor that plausibly pattern-matches to at least one system in the pinned organisation's inventory. The incident must:

- **Be a real published incident.** Cite the source database, the incident record identifier, and the publication date. Do not invent an incident. If the source database's specifics have moved or the record has been amended since the drafting date, mark `<!-- needs-research: reconfirm incident record at reading time -->`.
- **Have enough public detail to walk the four questions of the incident-to-gap translation.** An incident with only a headline and no post-mortem detail cannot support the ritual; pick one where the community post-mortem, provider corrective statement, or regulator report gives enough shape for the second question ("would our release-gate have detected it").
- **Pattern-match to at least one system in the pinned inventory.** Not the same system, not the same organisation — a pattern-relevant system whose deployment shape (LLM chatbot, agentic tool user, RAG system, classifier in a decisioning workflow, multimodal input handler) matches the incident's system class enough for the translation to be defensible.

Three complications to consider:

- **The incident may have a shape that spans peer tracks.** A single incident often surfaces gaps in risk-engineer coverage, AI-eval coverage, and model-eval methodology simultaneously. The ritual routes each gap to its own peer without collapsing them.
- **The ranking must be defensible against your actual peer leads.** The formula's `cost-to-close` term is not the programme's cost alone — it includes the peer-track's FTE-weeks. A ranking that assumes peer capacity the peer does not have is a broken ranking, and the escalation-packet artefact is the mechanism for negotiating it.
- **The ritual must produce a signed quarterly-roadmap pack.** The roadmap is not a wish-list; it is a signed commitment from the head of AI governance that authorises the criterion-set changes, the peer investments, and the deferred-decision expenditures for the next quarter.

## Requirements

Produce five artefacts in a single `roadmap/` directory.

### 1. `roadmap/incident-brief.md`

The setup for the ritual. A one-page brief that pins:

- **Source citation.** The incident-database (AIID / OECD.AI / MIT AI Risk Repository), the incident record identifier, the publication date, the canonical URL, and one paragraph summarising the incident in the reviewer's own words (not a copy-paste). Mark `<!-- needs-research: reconfirm incident record at reading time -->` where the source's specifics may have moved.
- **Incident class.** The GMF category (if using AIID) and the harm-inventory category the incident maps to for the pinned organisation (safety, fairness, privacy, security, information-integrity, agentic-safety, or the categories the pinned organisation's harm inventory uses).
- **Pattern-relevant systems in the pinned inventory.** Which systems in the pinned inventory could plausibly exhibit the same failure mode. Name them by system-id, deployment-tier, and intended-use. State the count.
- **Sources of independent corroboration.** Where the community post-mortem, provider corrective statement, or regulator report says something the AIID record does not — cite each.
- **Why this incident.** One paragraph on why this incident is the right one for the ritual this cycle — likelihood-in-inventory, severity-in-context, or a pattern the near-miss log has been surfacing that this incident materialises.

### 2. `roadmap/incident-to-gap-translation.md`

The mechanical core of the ritual. For the incident, walk the four questions chapter `05` names and write short answers.

- **Question 1 — What harm did the incident cause (or would it have caused)?** Named against the pinned organisation's harm inventory (from exercise `02`'s risk-engineer row).
- **Question 2 — If a system in our inventory had the same shape as the incident's system, would our release-gate have detected the gap that led to the harm?** Answered by walking the criterion set (from `mod-103`) and checking whether a criterion covers the gap. State the specific criterion-ids the walk touched and the answer per criterion (covered / partially covered / uncovered).
- **Question 3 — If not, what specific criterion or evidence would have caught it?** Named at the level of the rubric row, not at the level of "we should evaluate for X." For each new criterion (or amended existing criterion), state the id (e.g. `GATE-SAF-crisis-01`), the specific eval or evidence artefact the criterion requires, the peer-track owner (from the peer-contract matrix), and the assurance-case node the criterion discharges.
- **Question 4 — Whose peer track owns the evidence that discharges the new criterion?** Named against the peer-track contract matrix. For each row, state whether the peer's current freshness cadence and artefact schema can support the new criterion, or whether a renegotiation trigger is activated.

The output is a **release-gate evidence-gap row set** with a citation to the incident source, a citation to the affected systems in the pinned inventory (or "none currently but pattern-relevant"), the proposed criterion or evidence, and the peer owner.

### 3. `roadmap/prioritised-queue.md`

The queue after ranking with the chapter `05` formula: `priority = (likelihood-in-your-inventory × severity-if-repeated) ÷ cost-to-close`.

Structure as a table with rows *evidence-gap-id*, columns *likelihood*, *severity*, *cost-to-close*, *priority score*, *reactive-or-preventive*, *quarter to close*.

- **Likelihood.** A count-with-conviction of how many systems in the pinned inventory could plausibly exhibit the failure mode. Conservative — a specific fit is worth more than a broad category. A gap that affects zero current systems is not zero-priority (the pattern may be relevant to a system in the next planning cycle) but is lower.
- **Severity.** Scored against the pinned organisation's harm-inventory severity axes (physical, psychological, financial, reputational, societal). A fatality-adjacent harm outweighs a productivity loss; a reputational harm at institution scale outweighs a per-user annoyance.
- **Cost-to-close.** FTE-weeks for the assurance programme plus FTE-weeks for the peer-track that owns the closing evidence. Cite the peer-track name for the peer FTE-weeks.
- **Priority score.** The formula's output, ranked descending in the table.
- **Reactive or preventive.** *Reactive* if the gap closes a specific incident's failure mode with a narrow criterion; *preventive* if the gap closes a category of failure modes by pattern. State the split across the queue — a healthy quarterly split is roughly 30-50 percent reactive and 50-70 percent preventive.
- **Quarter to close.** The target quarter for closure — this-quarter, next-quarter, or deferred-with-rationale.

Include a summary block below the table: the reactive vs preventive split, the total FTE-week estimate across the programme and the peer tracks, the deferred rows and their deferral rationale, and any queue-shape signals (a lopsided reactive split may signal the programme is running behind the incident stream; a queue with no near-quarter closures may signal the programme is not honouring the lived-experience signal).

### 4. `roadmap/escalation-packet.md`

The escalation packet for at least one gap whose closure requires peer-track investment beyond the peer's current capacity. Chapter `05` names the packet's shape.

- **The incident (or set of incidents) that surfaced the gap.** Cite the AIID / OECD.AI records and the near-miss-log rows.
- **The specific evidence a release-gate would need that the peer does not currently produce.** Named at rubric-row granularity, with the peer-track contract matrix cited as the current state.
- **The proposed change to the peer's evidence-contract.** Which row of the matrix changes, what freshness / schema / sign-off changes, and what the peer's current capacity constraint is.
- **The joint priority ranking.** The priority score from artefact 3 for this gap, plus a paragraph justifying why the gap warrants the peer's investment relative to the peer's other in-flight commitments (from the peer's own roadmap where visible).
- **The peer's response, drafted.** As if the peer responded — *accepted*, *accepted-next-cycle*, *declined-with-rationale*, or *escalated*. Do not skip this — the exercise's job is to rehearse the packet, and rehearsal includes the response.
- **The head-of-AI-governance escalation clause (if the peer declines or defers).** How the packet escalates to the head for cross-team reprioritisation, per `mod-101/06` and exercise `03`'s reporting-line contract.

### 5. `roadmap/quarterly-roadmap-pack.md`

The pack the programme lead brings to the quarterly roadmap-review ritual. Chapter `05` names the shape.

- **Cover page.** The pinned organisation, the quarter being reviewed and the quarter being planned, the programme lead's name (or role slug), the attendee list (programme team, peer-track representatives whose gaps are on the queue, the senior architect as a listener, the head of AI governance as approver).
- **Last-quarter roadmap review.** The previous quarter's signed roadmap, its closure rate per item, the deferred items and the reason.
- **Current-quarter queue walk.** The top of the queue from artefact 3, with the ranking rationale for each row and the peer-response state from artefact 4.
- **Escalation walk.** The escalation packets from artefact 4, with the head's expected decisions per packet.
- **Next-quarter roadmap draft.** The signed-roadmap draft — named owners per item, a target closure date, the evidence-gap each closes, and the criterion-set edit each drives (the MAJOR / MINOR / PATCH bump per `mod-104` chapter `06` for each affected assurance bundle).
- **Approval block.** The programme-lead signature line and the head-of-AI-governance approval line. This is the pack's *output* — a signed roadmap that authorises the next quarter's investment.

## Starter guidance

- **Pick an incident with enough public detail.** The AIID incident record often has a short summary; the community post-mortem or the provider's corrective statement is where the shape lives. Without at least one of those, the second and third questions of the translation are guesses.
- **Translate at rubric-row granularity, not at "we should evaluate for X."** The output is a criterion or evidence artefact that the walker (per `mod-103`) can enforce. A gap named at the level of "improve safety evaluations" is not walkable; a gap named as `GATE-SAF-crisis-01: crisis-scenario eval coverage with clinical-domain judge and hard-fail refusal threshold` is.
- **Cost-to-close includes the peer-track FTE.** A gap the programme can close in a criterion-set edit costs less than a gap that requires a new evaluation harness from a peer team. The ranking must reflect the peer's cost, not just the programme's.
- **The reactive-vs-preventive split is a health metric.** A programme that is 100 percent reactive is running behind the incident stream; a programme that is 100 percent preventive is not honouring the lived-experience signal. Both are governance defects. The 30-50 / 50-70 range is the healthy zone.
- **The escalation packet is compact and evidenced.** A packet that reads as a demand ("please build X for us next quarter") without an evidenced case will be refused. A packet that reads as a joint-priority proposal with the incident citations, the affected in-inventory systems, and a specific renegotiation trigger stands a chance of acceptance.
- **The ritual runs to time.** The quarterly review is 90 minutes with a fixed pack, a fixed attendee list, a fixed agenda, and a signed output. If the pack takes 90 minutes to walk without approval, the pack is too big — cut items to next quarter and record the deferral.
- **The head of AI governance signs the roadmap.** The pack's output is not a status update; it is a signed commitment. The exercise's approval block is not decorative — it is the artefact that authorises the criterion-set edits and the peer investments.
- **`<!-- needs-research: … -->` is a legitimate answer** for incident-record specifics that may have moved since the drafting date, for peer-track capacity that would need verification against the peer's current planning cycle, and for standards-clause numbers that would need verification against the current text.

## Acceptance criteria

You have succeeded if:

- `roadmap/incident-brief.md` cites a real published incident from AIID or the OECD.AI Incidents Monitor (with source, record identifier, publication date, canonical URL), maps it to the pinned harm inventory, names the pattern-relevant systems in the pinned inventory by system-id and tier, cites at least one source of independent corroboration, and justifies why this incident is the right one for the ritual this cycle.
- `roadmap/incident-to-gap-translation.md` walks the four questions from chapter `05` in order. Question 3's output is at least three release-gate evidence-gap rows named at rubric-row granularity, each with a criterion-id, the specific eval or evidence artefact, the peer-track owner from the matrix, and the assurance-case node the criterion discharges.
- `roadmap/prioritised-queue.md` presents the ranked queue in a table with likelihood, severity, cost-to-close, priority score, reactive-or-preventive tag, and quarter-to-close. The reactive-vs-preventive split is stated. The total FTE-week estimate across the programme and the peer tracks is stated.
- `roadmap/escalation-packet.md` covers at least one gap whose closure requires peer-track investment; it names the incident source, the specific evidence gap, the proposed peer-contract change, the joint priority ranking, a drafted peer response, and the head-of-AI-governance escalation clause where applicable.
- `roadmap/quarterly-roadmap-pack.md` covers cover page, last-quarter review, current-quarter queue walk, escalation walk, next-quarter roadmap draft, and the approval block with programme-lead signature line and head-of-AI-governance approval line. The pack is Git-trackable and structured (not a narrative).
- Every incident-record citation is either verified against the source database or marked `<!-- needs-research: reconfirm incident record at reading time -->`.
- Every peer-track cost estimate cites the peer-track by name and is grounded in the peer-contract matrix's freshness cadence.
- The queue does not consist entirely of reactive items or entirely of preventive items; the split is defensibly in the 30-50 / 50-70 healthy zone.

## Stretch goals

- **Run a second incident and merge the queues.** In `roadmap/second-incident-brief.md`, pick a second incident (from a different source — if the first is from AIID, the second from the OECD.AI Monitor or the MIT Risk Repository) and walk artefacts 1–3 for it. Then merge the two queues in `roadmap/merged-queue.md`, with the priority scores harmonised and the reactive-vs-preventive split re-checked across the combined queue.
- **Cross-reference to the near-miss log.** In `roadmap/near-miss-integration.md`, walk the pinned organisation's near-miss log (from exercise `01` artefact 3's exception log and deferred-approval log) and identify which rows in the queue are near-miss-signalled rather than external-incident-signalled. Both signal classes feed the same queue; the distinction is provenance.
- **Draft the pack's dashboard companion.** In `roadmap/dashboard-view.md`, extend the on-call and programme-owner dashboards from `mod-103` chapter `06` and exercise `01` to show the queue's progress in real time — items closed, items in flight, items deferred, escalations in flight.
- **Rehearse the peer-lead defence.** In `roadmap/peer-lead-defence-rehearsal.md`, walk a rehearsal of the escalation packet's presentation to the peer lead — what the peer will push back on, what the programme concedes, what the programme escalates to the head if the peer declines. This is analogous to the effective-challenge convention from chapter `01` but for the *ranking*, not the *case*.
- **Cross-map to the assurance-case audit passes.** In `roadmap/audit-passes-crosswalk.md`, walk each evidence-gap row from artefact 2 and pin which `mod-102` chapter `05` audit pass (unstated assumptions, defeaters, diversity of evidence) it maps to. The ritual is the programme-scope analogue of the case-scope audit passes.
