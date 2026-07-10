# exercise-01: Ownership Map and Deferral Contract

**Estimated effort:** 2 hours

## Objective

Draft a **deferral contract** for the release-assurance program at a *realistic* organisation you choose. The contract must name every party that produces evidence for the release-gate and every party the release-gate produces artefacts for, with the specific artefact, the reason the release-gate needs it, and the framework citation. Then defend one row of the contract that is likely to be contested (i.e. a peer or higher-track lead could reasonably ask "why is this on my desk?").

This exercise is the practical output of chapters `01` and `06`.

## Prerequisites

- Chapter `01-release-assurance-position-on-the-ladder.md`.
- Chapter `06-deferral-contract.md`.
- The `PREREQUISITES.md` reading list for framework fluency (NIST AI RMF, ISO/IEC 42001, EU AI Act).

## Problem statement

You are the newly hired AI Evaluation Engineer (level 35, AI Governance family) at a fictional but realistic organisation. Pick **one** of the following organisation types for the exercise (or write your own equivalent):

- A **provider** of a healthcare-diagnostic AI system, subject to FDA GMLP and EU AI Act Annex III high-risk classification.
- A **deployer** of a foundation-model-based customer-support agent inside a US-and-EU multinational bank; also *provider* of the fine-tuned derivative.
- A **provider** of a GPAI model that is likely to be designated with systemic risk under EU AI Act Article 55.

For your chosen organisation, sketch:

- The **AI systems in scope** for the release-assurance program (name them, one paragraph each).
- The **peer / prerequisite / higher-track roles** that exist inside or adjacent to your program (adapt the ladder from chapter `01` — some may be missing at your organisation, and that gap is itself content for the contract).
- The **release-gate scope** — which systems go through the gate, which do not.

## Requirements

Produce a `deferral-contract.md` (or `.pdf`, `.pptx` — pick a format your future audience can act on) containing:

1. **Organisation and program header.** Two or three paragraphs — the organisation, the systems in scope, the release-gate scope, the applicable jurisdictions and sector rules.
2. **Evidence-in table.** One row per artefact each party owes the release-gate, using the shape from chapter `06`:

   | Party (role, level) | Owed artefact | Why the release-gate needs it | Framework citations | Delivery cadence | Format / storage |
   | ------------------- | ------------- | ----------------------------- | ------------------- | ---------------- | ---------------- |

   Cover, at minimum: analyst (L15), risk engineer (L25), eval engineer (L30, AI Eng.), model-eval engineer (L30, ML Eng.), MLSec (L35), agentic-safety engineer (L40, *only if in scope*), architect (L50), head of AI governance (L60).
3. **Artefacts-out table.** One row per artefact this program owes each party, same shape.
4. **Third-party rows.** Separate short table for third-party evaluators / notified body / auditors / deployers or providers on the other side of the handoff.
5. **Escalation matrix.** For each of the four failure modes in chapter `06` (missing evidence, unclear boundary, dispute, inadequate evidence), name who escalates to whom and what the release-gate does in the interim.
6. **Contested-row defence.** Pick one row that a peer lead is likely to push back on. Write a one-page memo defending why the artefact belongs on that party's desk, with citations to NIST AI RMF sub-categories, ISO/IEC 42001 clauses, and EU AI Act articles.

## Starter guidance

- **Do not copy chapter `06`'s tables verbatim.** They are the *template*. Your job is to instantiate the template to a specific organisation and to add / remove rows where the specific context calls for it (e.g. a healthcare provider will have rows for QMS / clinical validation that a customer-support deployer will not; a GPAI provider will have Article 55 rows a Annex III deployer will not).
- **Every row names an artefact, not a topic.** "Harm inventory v3 signed by risk-engineering lead" beats "risk documentation." "EU declaration of conformity per Annex V" beats "compliance evidence."
- **If a party is missing at your organisation, note the gap and record who currently backfills it.** That gap is a program risk and should be flagged for the head of AI governance.
- **Framework citations use the exact identifier.** `NIST AI RMF MEASURE-2.7` and `ISO/IEC 42001 clause 6.1.2` and `EU AI Act Article 15` — not "MEASURE" or "clause 6."
- **The contested-row defence** should look and read like something you would send in email to the peer lead. Cite the framework, name the release-gate obligation the artefact discharges, and explicitly say what happens if the contract breaks.

## Acceptance criteria

You have succeeded if:

- The contract names **all** parties from chapter `06` that are relevant to your organisation, with any additions the specific context requires.
- Every row has a **named artefact**, a **release-gate reason**, and a **framework citation**.
- Every row is **actionable in a scheduling sense** — cadence and format are specified.
- The escalation matrix covers all four failure modes and is walk-throughable end-to-end without you narrating it.
- The contested-row defence would survive a 15-minute meeting with the peer lead, i.e. it does *not* rely on "because I said so" and does *not* backfill peer craft.
- No row invents evidence a peer cannot in principle produce (a common failure is asking for statistical framing from a peer with no statistical training).

## Stretch goals

- Write the **counter-defence** the peer lead might raise for the contested row, and your response.
- Add a second contested row (a different party) so the exercise covers both a lower peer and a higher track.
- Extend the contract with a **retirement row** — what evidence flows when the system is decommissioned, per ISO/IEC 42001 lifecycle expectations.
- Draft the **program charter paragraph** (`mod-112`) that references the deferral contract as a governed artefact.
