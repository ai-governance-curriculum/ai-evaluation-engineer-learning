# exercise-04: EU AI Act Articles → Release-Gate Map

**Estimated effort:** 2 hours

## Objective

Take a fictional in-scope AI system and produce a **release-gate map** that names, article by article, the EU AI Act obligations the release-gate is discharging, the evidence artefact behind each, the peer role that owes the artefact, and the sibling framework citations (NIST AI RMF sub-category and ISO/IEC 42001 clause).

This exercise operationalises chapter `04` and is the direct precursor to `mod-103` (release-gate architecture) and `mod-106` (cross-jurisdictional mapping).

## Prerequisites

- Chapter `04-eu-ai-act-articles-shaping-the-release-gate.md`.
- Chapter `06-deferral-contract.md`.
- The EU AI Act text (Regulation (EU) 2024/1689) open in browser — via EUR-Lex — for direct citation.

## Problem statement

Pick one of the following in-scope scenarios (or write your own equivalent):

- **Scenario A — Annex III high-risk provider.** Provider of an AI system for **employment / worker management** (Annex III, point 4). Specifically: an AI-assisted CV screening and ranking system used by hiring managers.
- **Scenario B — Annex III high-risk deployer + provider.** Deployer, in a US-and-EU bank, of a **credit-scoring AI system** (Annex III, point 5), fine-tuned from a foundation model. The bank is *deployer* of the foundation model and *provider* of the fine-tuned derivative.
- **Scenario C — GPAI provider with systemic risk.** Provider of a **GPAI model** trained on ≥10^25 FLOPs, with a downstream deployment surface across many customers.

For your chosen scenario, produce the map described below.

## Requirements

Produce `eu-ai-act-release-gate-map.md` containing:

1. **Scenario header.** One page: the system, the actor(s) (provider / deployer / both), the deployment context, the affected populations, whether Article 6 / Annex III classification applies and why, and any Article 5 prohibited-practice concerns already ruled out.
2. **Article-by-article table** covering (at minimum) the articles from chapter `04`. Adjust in / out as relevant to your scenario:

   | Article | Obligation (short) | Applies to us? (Y / N / partially) | Reason | Release-gate evidence artefact | Peer role owing evidence | Sibling NIST AI RMF | Sibling ISO 42001 clause | Notes |
   | ------- | ------------------ | ---------------------------------- | ------ | ------------------------------ | ------------------------ | ------------------- | ------------------------ | ----- |

   Cover Articles 8, 9, 10, 11, 12, 13, 14, 15, 17, 26, 43, 47, 49, 55, 61, 72 as a minimum. Add Article 5, 6, 27, 53, 71, 73, or any Annex III sub-point if your scenario requires it.
3. **Article 11 dossier outline.** Draft the outline (headings only, one paragraph per) of the technical documentation dossier per Annex IV — the internal-facing statutory dossier. Do *not* write the content, just the outline the release-gate would populate.
4. **Article 47 declaration outline.** Draft the outline of the EU declaration of conformity per Annex V for your system, with each Annex V required element listed and marked "on file" or "gap."
5. **Article 72 post-market monitoring plan outline.** Two or three paragraphs — what data is collected, from whom (deployer or provider counterparty), at what cadence, how it feeds the risk-management system, and how it connects to Article 61 incident reporting.
6. **Cross-jurisdictional flag.** Name one non-EU jurisdiction that your scenario also has to satisfy (e.g. Colorado AI Act SB24-205 for scenario A, NYC Local Law 144 for scenario A, US federal or California CPPA for scenario B, US EO 14110 successor guidance for scenario C) and note which articles' evidence will need re-shaping. This flag threads into `mod-106`.

## Starter guidance

- **Cite each article correctly.** "EU AI Act Article 15(1)" and "EU AI Act Article 15(4)" carry different obligations. Where an article has sub-paragraphs relevant to your evidence, cite them.
- **"Applies to us?" is not always yes.** Article 55 does not apply to a scenario-A CV-screening system; Article 26 applies only to deployers. Explicitly saying "N — this actor is not a deployer" is a valid row.
- **Do not conflate provider and deployer obligations.** Article 16 (provider obligations, general) and Article 26 (deployer obligations) split cleanly. Scenario B carries both.
- **Article 11 and Article 13 are different documents.** Article 11 is the internal-facing technical documentation (Annex IV); Article 13 is the instructions for use for the deployer. The system card for external audiences (`mod-105`) derives from both.
- **Annex IV and Annex V are content lists, not templates.** Your outline should match their numbered structure but be adapted to your scenario.
- **The post-market monitoring plan cannot be one paragraph.** It is a small SOP: data sources, cadence, thresholds, feedback loop, incident escalation.

## Acceptance criteria

You have succeeded if:

- All the articles listed in chapter `04` are represented in the table, with a Y / N / partially decision and a reason.
- Each applying article has a **named evidence artefact** and a **peer role owner**.
- Each row cross-cites the sibling **NIST AI RMF sub-category** and **ISO/IEC 42001 clause**.
- The Article 11 dossier outline follows Annex IV's structure and marks gaps.
- The Article 47 declaration outline follows Annex V's structure and marks gaps.
- The Article 72 plan outline names the data sources, the cadence, and the incident-reporting hook.
- The cross-jurisdictional flag names a specific non-EU instrument and specific articles it re-shapes.

## Stretch goals

- Extend to Article 27 (fundamental-rights impact assessment) for a scenario-A or scenario-B deployer that is a public-sector body — including the FRIA content list.
- For scenario C, walk the GPAI Code of Practice signatory obligations that shape Article 55 discharge, and note which peer role (agentic-safety engineer at L40 vs. this role at L35) owns each.
- Draft the release-gate *pass criterion* for each article — the concrete "pass if X, else fail" statement — so the map becomes a release-gate schema draft usable in `mod-103`.
- Add a "residual risk" column noting where the release-gate accepts a partial discharge and escalates the residual to the head of AI governance.
