# exercise-01: GSN Case for a Real Release Decision

**Estimated effort:** 3 hours

## Objective

Author a **Goal Structuring Notation (GSN)** assurance case for a *specific*, *dated* AI release decision at a realistic organisation of your choice. The case must include the seven core node types (goal, strategy, solution, context, assumption, justification, away-goal) and the two link types (`SupportedBy`, `InContextOf`) per the [GSN Community Standard v3](https://scsc.uk/gsn), and it must be walk-able top-down by an unfamiliar reviewer.

This is the applied output of chapters `01` and `02`.

## Prerequisites

- Chapter `01-why-assurance-cases.md`.
- Chapter `02-gsn-for-ai-release-decisions.md`.
- The GSN Community Standard v3 (skim once end-to-end before drafting).
- Mod-101's deferral contract exercise output (you will re-use its ownership map when routing away-goals — full contract handling is exercise `05`).

## Problem statement

You are the AI Evaluation Engineer at an organisation that has to make a release-gate decision *this cycle*. Pick **one** of the three scenarios below (or write your own equivalent, if you have specific context you want to use). Every scenario names one AI system, one deployment tier promotion, one jurisdiction set, and one applicable framework set — you do not get to change these mid-exercise.

### Scenario A — Foundation-model-backed customer-service triage in a US+EU bank

A US-and-EU multinational bank is promoting an internal document-triage assistant from limited pilot (200 users, US only, 8 weeks) to production (all users, US + EU). The system uses a fine-tuned foundation model with retrieval and is high-risk per EU AI Act Annex III paragraph 5(b) (creditworthiness / financial services). SR 11-7 model-risk-management applies to the fine-tuned derivative.

### Scenario B — Diagnostic-decision-support AI in a US hospital network

A US hospital network is promoting a diagnostic-decision-support model (radiology triage) from pre-deployment validation to clinical use in six pilot sites. The system is regulated as SaMD (Software as a Medical Device) under FDA Class II with a submitted 510(k), and FDA GMLP guiding principles apply. A Predetermined Change Control Plan (PCCP) has been proposed. HIPAA controls are in scope.

### Scenario C — GPAI provider under EU AI Act Article 55

A GPAI provider is releasing a new foundation model checkpoint that has been designated (or is under credible designation) as GPAI with systemic risk under EU AI Act Article 55. The release is external (developer API + hosted product) into the EU and beyond. The EU GPAI Code of Practice is the operational reference; the provider also intends to satisfy its own Responsible Scaling / Preparedness / FSF-shape internal deployment-tier framework.

## Requirements

Produce a `gsn-case.md` (or `.pdf`, or a diagram export) containing:

1. **Case header.** Two or three paragraphs — the system, the release-tier promotion, the jurisdictions in scope, the decision date, and the frameworks the case discharges. Cite the framework identifiers exactly (Article number, sub-category, clause).
2. **Top-level goal (`G1`).** One dated, scoped statement of what is claimed at the release-gate. See chapter `02` for the shape.
3. **Context, assumption, and justification nodes attached to `G1`.** At minimum: deployment-tier scope, jurisdictional scope, one assumption you know will need declaring, and one justification for the top-level strategy.
4. **First-level strategy.** Choose one of per-obligation / per-framework / per-property / per-risk decomposition (chapter `02`) with a written justification for your choice against this scenario.
5. **Sub-goals (`G2…Gn`).** At least one sub-goal per applicable article or framework component. For scenario A: at least Articles 9, 10, 11, 12, 13, 14, 15, 17, 26 + SR 11-7 clauses on validation and independent review. For scenario B: FDA GMLP guiding principles (all 10) + HIPAA administrative and technical safeguards for identified data flows + PCCP change-control claim. For scenario C: Article 55 obligations + your chosen deployment-tier framework's per-threshold claims.
6. **One branch fully developed to a leaf.** Pick one branch that you will develop end-to-end — parent goal → strategy → sub-goals → leaf claim → solution (evidence node with name, version, digest placeholder, and warrant). The other branches can stop at first-level sub-goals so long as they are structurally well-formed.
7. **At least one away-goal.** Point one leaf (cybersecurity posture / independent evaluation / harm inventory) to an away-goal in a peer module you cite by identifier and version. If the peer module does not exist yet at your organisation, invent a placeholder identifier and declare that gap in the case header.
8. **At least three explicitly attached assumptions.** Load-bearing assumptions must be attached to the specific node they load-bear on, not to the top-level goal generically.

## Starter guidance

- **Choose a scenario you will not be tempted to under-specify.** If you cannot answer "which fine-tune version, which release candidate hash, which pilot window" you are being too abstract; add specifics before you start the graph.
- **Draw the top three levels first, then descend.** Reviewers walk top-down; getting the top three right is 70% of the case's readability.
- **Every solution node names an artefact.** "Signed eval report" is not a solution; "eval-report-rc-2026-07-a3c1 v1.0.0, `sha256:c3a9e5…`, warrant per MOD-EVAL evidence-contract v1" is. If a real digest doesn't exist yet, use a placeholder — but keep the schema right.
- **Every away-goal names its target module and version.** `AG-SEC-1 → SEC-ARM-v2 §C-2.3` is walkable; `AG-SEC-1 → 'security case'` is not.
- **If the case would not survive a hostile-but-competent reviewer at chapter `05`'s pass 2 (unstated assumptions), fix it now.** Write down the assumption; do not hide it in the prose.
- **Do not backfill peer craft.** If the leaf's evidence is authored by another peer track, cite the peer track's ownership in the solution's warrant field. Full evidence-contract handling is exercise `05` — for now, note the routing.

## Acceptance criteria

You have succeeded if:

- The case has one top-level goal, dated and scoped, with at least three explicitly-attached context / assumption / justification nodes.
- The first-level strategy is one of the four canonical strategies (per-obligation / per-framework / per-property / per-risk) *chosen with a written justification*.
- The first level fans into at least the minimum number of sub-goals for the chosen scenario (see requirements).
- Exactly one branch is developed to leaf-level, with a solution node carrying a name, version, digest placeholder, and warrant, and the leaf is contextualised by an assumption or context node where it load-bears.
- At least one away-goal points to a peer module with an identifier and version.
- No goal restates its parent verbatim.
- No solution is a category ("signed eval report") without an artefact identifier.
- A reviewer unfamiliar with the case can walk from `G1` to the developed leaf without you narrating.

## Stretch goals

- Draw the case in a real GSN tool (Sphinx-Assure, [ASCE](https://www.adelard.com/asce/), or an open-source GSN library) rather than in ASCII. Attach the export.
- Develop a second branch to leaf-level, so the case has two independent leaves discharged by different peer tracks.
- Add a **module map** — a one-page diagram showing which sub-cases (safety-property modules, jurisdiction modules, evaluation-methodology modules) the release-case's away-goals point to. Exercise `05` will build the evidence contracts against this map.
- Author one *incorrect* variant of the case (over-fanned strategy, hidden assumption, uncited away-goal) that will be the input to exercise `04`'s audit exercise. Keep it plausible.
