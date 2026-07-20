# Incident-Driven Roadmap Prioritisation

## Motivation

Chapter `01` gave the programme a running loop. Chapter `02` and `03` fixed the interfaces. Chapter `04` chose the tooling. This chapter turns the programme's *forward planning* into a repeatable ritual driven by concrete incident signal rather than by intuition, vendor pitch, or the loudest voice in the room.

Two failure modes motivate an incident-driven ritual.

The first is **the roadmap driven by conference talks**. The programme lead reads a talk on a fashionable evaluation topic; the next quarter's investment is a partial rebuild in that direction; the release-gate criterion set is retrofitted to match. The programme is now measured against work whose relevance to the *actual* systems in the inventory is unproven. Six months later, an incident lands in a category the programme did not invest in; the retrospective is embarrassing.

The second is **the roadmap driven by escalation memory**. The last thing that broke gets fixed; the item after that gets fixed; the programme spends every quarter reacting to the most recent incident. Categorical patterns across incidents are missed; the same class of gap recurs across systems because each incident is treated as a one-off.

The incident-driven prioritisation ritual sits between the two. Concrete incidents drive the queue; a categorisation pass drives the prioritisation; a quarterly review binds the queue into a defensible plan the head of AI governance can approve.

## The incident-signal sources

Four sources of incident signal feed the queue. Each has a different flavour of failure mode and a different treatment.

- **The [AI Incident Database (AIID)](https://incidentdatabase.ai/)** — the community-maintained database of publicly-reported AI incidents. High volume, variable quality, useful for surfacing categorical patterns and for producing worked examples that release-gate proposers can read. The database's taxonomies (Goals, Methods, Failures — GMF) are useful for grouping.
- **The [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents)** — an official incident-monitor tracking AI-related incidents across jurisdictions. Lower volume, higher curation, tied to policy-relevance signals. <!-- needs-research: verify current OECD.AI Incidents Monitor scope and update cadence as of 2026-07 -->
- **The [MIT AI Risk Repository](https://airisk.mit.edu/)** — a repository of AI-risk taxonomies, incident sources, and academic risk categorisations. Useful for the categorisation pass because the taxonomy work is done.
- **The internal near-miss log.** The programme's own log of soft-fails, deferred approvals, exception approvals, and post-market-surveillance signals from `mod-110` that did *not* rise to serious-incident status but revealed a gap. This is the highest-signal source because every row is in a system already in your inventory and every row already has a scoped owner.

The four sources feed one queue; the sourcing is recorded per row for provenance, but the queue itself is unified. Every row is either an incident (a materialised harm) or a near-miss (a harm that did not materialise but could have).

## The incident-to-gap translation

Every row in the queue is translated from "an incident happened" to **a concrete evidence-gap in the release-gate**. The translation is the mechanical core of the ritual; without it, the queue is a list of anecdotes rather than a list of engineering work.

**Shape.** For each incident row, the assurance owner asks four questions and writes short answers:

1. **What harm did the incident cause (or would it have caused)?** Named against the harm inventory's categories where possible (`mod-101/06` risk-engineer row).
2. **If a system in our inventory had the same shape as the incident's system, would our release-gate have detected the gap that led to the harm?** Answered by walking the criterion set (`mod-103`) and checking whether a criterion covers the gap.
3. **If not, what specific criterion or evidence would have caught it?** Named at the level of the rubric row, not at the level of "we should evaluate for X."
4. **Whose peer track owns the evidence that discharges the new criterion?** Named against the peer-track contract matrix (chapter `02`).

The output of the translation is a **release-gate evidence-gap row** with a citation to the incident source, a citation to the affected systems in our inventory (or "none currently but pattern-relevant"), the proposed criterion or evidence, and the peer owner.

**Failure modes.** Translating in a way that inflates the gap (a chatbot mishandling one interaction becomes "we need to evaluate all chatbot behaviour comprehensively"); translating in a way that assumes the incident's specific system when the pattern is broader (missing category-level investment); leaving the peer owner unnamed (the gap has no path to closure).

**What good looks like.** Every row names a specific criterion or evidence at rubric-row granularity, a peer owner drawn from the contract matrix, and either a specific in-scope system or a pattern-relevance note. The row is small enough that a single quarter's work can close it.

## Ranking the queue — the reactive-vs-preventive split

Once the gaps are named, they need to be ranked. The ranking formula is compact and defensible:

> priority = (likelihood-in-your-inventory) × (severity-if-repeated) ÷ (cost-to-close)

**Likelihood-in-your-inventory.** A count-with-conviction of how many systems in your current inventory could plausibly exhibit the same failure mode. The count is *conservative* — a specific fit is worth more than a broad category. A gap that affects zero current systems is *not* zero-priority (the pattern may be relevant to a system in the next planning cycle) but it is lower.

**Severity-if-repeated.** Scored against the harm inventory's severity axes (physical, psychological, financial, reputational, societal). A fatality-adjacent harm outweighs a productivity loss; a reputational harm at institution scale outweighs a per-user annoyance.

**Cost-to-close.** FTE-weeks for the assurance programme plus FTE-weeks for the peer track that owns the closing evidence. A gap the programme can close in one criterion-set edit costs less than a gap that requires a new evaluation harness from a peer team.

The ranking has a *reactive-vs-preventive* split baked in. Two flavours of investment show up in the queue:

- **Reactive investment.** Close this specific gap after a specific incident. The likelihood term is high (the gap has just materialised in your inventory or in a very similar inventory); the severity term is what the incident showed; the cost is what it takes to add the criterion, provision the evidence, and re-run the affected release-gates. Reactive investment is small, sharp, and always in the top of the queue after a serious incident.
- **Preventive investment.** Close a *category* of gaps by pattern. The likelihood term is a sum across many potential incident classes; the severity term is a distribution; the cost is a larger engineering commitment that pays across many future release-gates. Preventive investment is what turns a queue of anecdotes into a defensible criterion set.

A healthy quarterly split is roughly 30-50 percent reactive and 50-70 percent preventive. A programme that is 100 percent reactive is running behind the incident stream; a programme that is 100 percent preventive is not honouring the lived-experience signal.

## Escalating gaps a release-gate cannot close alone

Not every gap can be closed by a release-gate change. Some gaps require a peer track to change *its* methodology, its harness, its coverage. The programme's role in those cases is *not* to work around the peer — it is to package an evidenced case and hand it to the peer's roadmap.

**Shape.** For each gap whose closure requires peer-track investment, the programme produces an escalation packet: the incident (or set of incidents) that surfaced the gap; the specific evidence a release-gate would need that the peer does not currently produce; the proposed change to the peer's evidence-contract (chapter `02`); the joint priority ranking; and (if the peer is capacity-constrained) an escalation to the head of AI governance for cross-team reprioritisation (per `mod-101/06`).

**Failure modes.** Working around the peer with a release-gate patch (loss of altitude; the deferral contract breaks); assigning the peer work unilaterally without an evidenced case (the peer refuses on grounds of scope; the gap does not close); escalating every peer request to the head of AI governance (the head is overloaded; the assurance owner's authority looks weak).

**What good looks like.** The escalation packet is compact and evidenced; the peer's response is documented in the queue (accepted / accepted-next-cycle / declined-with-rationale / escalated); the closure path is visible on the queue's status page. When a peer declines, the queue records the decline and the disposition (the release-gate lives with the gap and the exception log records why).

## The quarterly roadmap-review ritual

The prioritisation is executed on a quarterly cadence, timed to feed the head of AI governance's own quarterly management review (per chapter `03` and ISO/IEC 42001 clause 9.3).

**Shape.** The ritual has a fixed pack, a fixed attendee list, a fixed agenda, and a fixed output.

- **Pack.** The prioritised queue with rankings; the decision log's exception and deferral summary for the quarter; the peer-contract renegotiation state; the previous quarter's roadmap and its closure rate.
- **Attendees.** The assurance-programme lead and their team; representatives of each peer track whose evidence appears in the queue's escalations; the senior architect (as a listener, to catch cross-organisation patterns); the head of AI governance (as approver of the resulting roadmap).
- **Agenda.** (a) Review last quarter's roadmap and its closure; (b) walk the top of the current-quarter queue; (c) discuss escalations; (d) approve the next-quarter roadmap.
- **Output.** A signed roadmap for the next quarter (assurance-team lead + head of AI governance signatures), with named owners for each item, a target closure date, and the evidence-gap each closes.

**Failure modes.** The ritual becomes a status meeting (no decisions get made; the queue keeps growing); the head of AI governance is not in the room (approval is deferred; the roadmap does not carry authority); peers are surprised by escalations at the review (the escalation packet was not shared in advance); the pack is written in narrative rather than in structured rows (auditors cannot walk it later).

**What good looks like.** The ritual runs to time (90 minutes), produces a signed roadmap, and results in every attendee leaving with a specific item they have committed to. The pack is Git-tracked and versioned; the roadmap is referenced by the operating model's stage-two scope assessment for cases in the next quarter.

## Worked example — a mental-health disclosure incident

An entry lands in the AI Incident Database: a general-purpose chatbot deployed by a large consumer-facing provider mishandled a user's mental-health disclosure, responding in a way that a clinical reviewer subsequently classified as harmful. The incident is widely reported; the provider issues a corrective statement; the community post-mortem identifies specific failure modes.

**Step 1 — surface.** The AIID entry lands in the programme's queue via the weekly incident-monitor scan. The team's chatbot systems (three in the inventory, all T2) are pattern-relevant.

**Step 2 — translate.** The assurance owner walks the four questions:

1. *What harm did the incident cause?* — psychological, potentially escalating; against the harm inventory the row maps to the "safety-critical user-state disclosure" category, which the current inventory covers thinly.
2. *Would our release-gate have detected it?* — walking the criterion set, the answer is *no with a caveat*: the current suite covers general safety refusal patterns but does not cover crisis-scenario handling as a specific criterion, does not require documentation of the escalation-path design, and does not cover the human-oversight surface for this specific interaction shape.
3. *What specifically would have caught it?* — three evidence-gap rows:
   - **`GATE-SAF-crisis-01`**: crisis-scenario eval coverage (a dedicated suite of adversarial mental-health-disclosure inputs, scored by a clinical-domain-trained judge with human-panel calibration, with a hard-fail threshold on refusal-plus-escalation-behaviour).
   - **`GATE-DOC-esc-01`**: escalation-path documentation as a required artefact (the assurance case must include an escalation-path diagram naming the human-oversight surface, the routing thresholds, and the follow-up channels).
   - **`GATE-HO-crisis-01`**: human-oversight design attestation for the crisis interaction class (with sign-off by the product's clinical or safety consultant, where applicable).
4. *Whose peer track owns the evidence?* — the crisis-scenario eval is jointly owned by `ai-risk-engineer` (suite construction, harm-inventory tie-in) and `ai-eval-engineer` (evaluation execution, judge-vs-human calibration). The escalation-path documentation is owned by the analyst plus the product team. The human-oversight design is owned by the product team with peer review from `ai-risk-engineer`.

**Step 3 — rank.** Likelihood: three systems in the inventory could exhibit the pattern; several more incoming in the next planning cycle. Severity: high (safety-critical, reputational at institution scale). Cost-to-close: the eval-set construction is meaningful FTE-weeks on the risk-engineer side; the criterion-set edit is small FTE-days on the assurance side; the documentation and design pieces are moderate FTE-weeks. Overall priority: high, reactive, top of the queue.

**Step 4 — escalate.** The eval-set construction requires risk-engineer investment beyond current capacity; the assurance owner produces an escalation packet with the AIID citation, the affected in-inventory systems, and the joint priority; hands to the risk-engineer lead. The risk-engineer accepts the item at accepted-next-cycle priority.

**Step 5 — schedule.** The three release-gate evidence-gap rows are added to the criterion set with a target enforcement date at the end of next quarter; the criterion set update ships; the affected release-gates re-run at their next scheduled cycle. The exception log carries three exceptions (one per system) with revisit triggers at the new criterion-set enforcement date.

**Step 6 — review.** At the next quarterly roadmap review, the pack shows the item as accepted, in-progress on the risk-engineer side, closed on the assurance side. The head of AI governance signs the roadmap.

The specific incident (one bad interaction, one company, one AIID entry) became five concrete release-gate changes (three new criteria, one escalation packet, three exceptions) delivering against a categorical gap that would otherwise have remained silent.

## Where this shows up in the rest of the track

- `mod-101/06` — the deferral contract's failure-mode row ("evidence present but inadequate") maps to the reactive-investment class; the "evidence missing" row maps to the escalation packet class.
- `mod-102/05` — the audit passes (unstated assumptions, defeaters, diversity of evidence) are the pattern the incident-driven ritual applies at programme scope; incidents surface defeaters that the assurance case's audit passes should have caught.
- `mod-103/06` — the on-call dashboard's exception-approvals register is one of the internal near-miss log's primary inputs.
- `mod-104/06` — every incident-closure that lands in the criterion set is a MAJOR bump on the affected assurance bundles.
- `mod-110` — the post-market surveillance signals feed the same queue as external incident sources; the queue does not distinguish (it distinguishes on severity and likelihood, not on source).
- `mod-111` — GPAI-systemic-risk incidents (frontier-capability disclosures, cross-institution reputational events) feed the queue at the highest severity band and typically also trigger the escalation-outside-team-authority path from chapter `03`.
- Chapters `01`–`04` — the ritual is the recurring reason the operating model, contract matrix, interfaces, and tooling substrate all get re-visited on a fixed cadence.

## Summary

- Incident-driven prioritisation replaces intuition-driven roadmap-building with a repeatable ritual grounded in concrete signal from AIID, OECD.AI, MIT AI Risk Repository, and the internal near-miss log.
- Every incident row is translated into a release-gate evidence-gap row by walking four questions: what harm, would we have caught it, what specifically would have caught it, whose peer owns the evidence.
- The queue is ranked by `(likelihood-in-your-inventory × severity-if-repeated) ÷ cost-to-close`, with a healthy split of roughly 30-50 percent reactive and 50-70 percent preventive investment.
- Gaps that require peer-track change (not release-gate change) escalate through an evidenced escalation packet; the release-gate does not work around the peer.
- The quarterly roadmap-review ritual (fixed pack, fixed attendees, fixed agenda, signed output) turns the queue into a defensible plan the head of AI governance approves.
- The mental-health-disclosure worked example shows how a single AIID entry translates into three criterion rows, one escalation packet, three exceptions, and one signed roadmap item.
- Exercise-05 asks you to run the ritual against a real incident from AIID or OECD.AI, produce the evidence-gap rows and the escalation packet, and defend the ranking against your peer leads.
