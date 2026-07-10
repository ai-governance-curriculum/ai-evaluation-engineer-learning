# exercise-02: ISO/IEC 25059 Quality-Rubric Mapping

**Estimated effort:** 3 hours

## Objective

Produce the **release-gate rubric** for the system designed in exercise `01`, structured around the ISO/IEC 25059 quality dimensions and cross-mapped, row-by-row, to specific NIST AI RMF MEASURE sub-category identifiers. Then defend one **dimension-balance** decision — where you drew the line between hard-gated and soft-gated criteria in a dimension whose statute coverage is contested.

## Prerequisites

- Chapter `02-iso-25059-quality-rubric.md` (this module).
- Exercise `01` outputs — `system-scope.md`, `gate-criteria-v1.md`, `gate-variants.md`.
- A reading pass through the NIST AI RMF Playbook's MEASURE section (chapter `02` and mod-101 chapter `02` cite the relevant sub-categories). The Playbook's sub-category identifiers are the source of truth for the cross-map.
- Recommended: skim ISO/IEC 25059:2023 (via the ISO catalogue) for the specific sub-characteristic names.

## Problem statement

Exercise `01` produced a bag of criteria. This exercise structures them into a rubric — a columnar view where each row cites a 25059 dimension, a MEASURE sub-category, an EU AI Act article, an ISO/IEC 42001 clause, and (where applicable) a sector rule. The rubric is a *design* artefact; the exercise-01 criterion set was a *runtime* artefact. Every runtime criterion resolves to exactly one rubric row.

The exercise has three parts: (1) build the rubric, (2) audit the coverage balance across dimensions, and (3) defend one contested balance decision.

## Requirements

Produce three artefacts.

### 1. `rubric-v1.md` (or CSV / spreadsheet)

The rubric, using the schema from chapter `02`. One row per rubric entry; columns:

| Column                 | Content                                                                                                                                                                     |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Criterion ID           | Stable ID (`GATE-…`), cross-referenced by the assurance case's `Claim.id`.                                                                                                    |
| 25059 dimension        | Functional adequacy / Robustness / Transparency / Controllability / Adaptability / Appropriate use of data / (25010 inherited characteristic where relevant).                 |
| 25059 sub-characteristic | The specific sub-characteristic, cited to the standard.                                                                                                                    |
| NIST AI RMF MEASURE    | The specific sub-category identifier (e.g., `MEASURE-2.5`), not a topic.                                                                                                     |
| EU AI Act article      | If applicable.                                                                                                                                                              |
| ISO/IEC 42001 clause   | The clause the row's evidence discharges (typically 8.x or 9.x).                                                                                                             |
| Sector rule            | If applicable (SR 11-7 clause, FDA GMLP principle, DORA article, etc.).                                                                                                     |
| Metric                 | Named metric and estimator.                                                                                                                                                 |
| Threshold              | Pass level, tied to the harm-inventory row or internal-goal that fixes it.                                                                                                  |
| Hard / soft            | With a one-line justification.                                                                                                                                              |
| Owner peer track       | analyst L15 / risk L25 / AI-eval L30 / model-eval L30 / MLSec L35 / third-party.                                                                                              |
| Evidence pointer       | The SACM `Artifact.id` and the peer's evidence-contract clause.                                                                                                              |

Coverage minima:

- **All six ISO/IEC 25059 dimensions** appear (functional adequacy, robustness, transparency, controllability, adaptability, appropriate use of data). A dimension not applicable at your system's tier is filled with `N/A — scope excluded` cited to the scope decision, *not* left blank.
- **At least one hard-gate criterion per dimension** at T2 (or your equivalent-mid-tier). Where the tier of exercise `01`'s design is lower and a dimension does not warrant a hard criterion, use `N/A — tier below hard-gate threshold` cited to the tier decision.
- **NIST AI RMF MEASURE cross-map is per sub-category identifier**, not per topic. Every populated row cites a specific sub-category (`MEASURE-2.5`, not "MEASURE — accuracy").
- Framework citations for EU AI Act use exact article identifiers (`Article 15(1)(a)`, not "Article 15 accuracy").

### 2. `coverage-balance-audit.md`

A short (1-page) audit of the rubric against the balance rule from chapter `02`:

- Per-dimension summary: number of hard criteria, number of soft criteria, `N/A` rows and their justifications.
- Overweighting analysis: is any dimension carrying more than roughly a third of the total hard-gate count? If so, is the overweighting justified by the system's shape (e.g., a high-stakes decision surface justifies over-weighted controllability)?
- Undercoverage flag: any dimension with only soft criteria or only `N/A` rows at T2 or above.
- Peer-track load: how many rows land on each peer track? Any peer track carrying an unrealistic load has a coverage-design problem.

### 3. `dimension-balance-defence-memo.md`

Pick one contested balance decision from the audit and write the memo you would send to the head of AI governance or the second-line reviewer defending it. Two-to-three pages. Contested cases include:

- A dimension where you chose to keep a criterion *soft* despite a plausible reading of the statute that would make it hard.
- A dimension where you chose to gate at a *lower* tier than the mid-tier default, because the statute or the harm inventory calls for stricter posture.
- A dimension where you chose `N/A — scope excluded` despite a colleague arguing the dimension applies.

The memo:

- Names the dimension, the criterion(a) in question, the tier, and the disputed classification.
- Cites the framework text (the specific 25059 sub-characteristic, the specific MEASURE sub-category, the specific EU AI Act article) that supports your read.
- Cites the harm inventory or internal-goal that supports the classification.
- Anticipates the reviewer's push-back and responds.
- Names the escalation path if the reviewer refuses — is this a rubric-version disagreement (dispositioned via the assurance program's own review process), an exception-approval path (per chapter `05`), or a policy escalation to the head of AI governance?

## Starter guidance

- **Start from the criterion set, not from the standard.** Walk each exercise-01 criterion into a rubric row; then look for dimensions that have no criteria and add rows for coverage.
- **Do not conflate 25010 and 25059.** ISO/IEC 25059 both inherits 25010 characteristics and adds AI-specific ones. If a criterion is discharging classical software-quality (say, reliability under load), cite 25010's characteristic and note that 25059 uses it verbatim. If the criterion is discharging an AI-specific quality (controllability's human-oversight nuance, adaptability's drift-under-change nuance), cite 25059's addition.
- **NIST AI RMF sub-category identifiers require reading the Playbook.** Do not guess. If you cannot pin a sub-category identifier, the row's cross-map is not done.
- **Sector-rule column is not a checkbox.** If your system is *not* in a regulated sector, most rows leave the column blank; if it *is*, most rows populate it. Do not populate the column just because the rubric has one.
- **The defence memo is not a hedge.** Pick the balance decision most likely to draw scrutiny and defend it plainly. If you cannot defend it plainly, the rubric row is wrong.

## Acceptance criteria

You have succeeded if:

- The rubric has one row per criterion from exercise `01`, plus any rows added for dimension coverage.
- All six ISO/IEC 25059 dimensions appear; `N/A` rows are justified.
- Every populated row cites a specific 25059 sub-characteristic, a specific NIST AI RMF MEASURE sub-category identifier, and (where applicable) a specific EU AI Act article, ISO/IEC 42001 clause, and sector rule.
- The metric column names both the metric and its estimator; the threshold column ties to a harm-inventory row or an internal-goal.
- The owner-peer column matches mod-101 chapter `06`'s deferral contract, and the evidence pointer resolves to a SACM `Artifact.id`.
- The coverage-balance audit flags any overweighted or undercovered dimension and cites the tier / scope / harm decisions that justify the pattern.
- The dimension-balance defence memo names one contested decision, cites the framework text, anticipates and responds to push-back, and names the escalation path.

## Stretch goals

- Extend the rubric with a **retirement column** — how each row's evidence contract is retired if the system leaves the release-assurance program's scope. Preview mod-107 and mod-112.
- Author a **crosswalk** from your rubric to the EU AI Act obligations for high-risk systems: for each Article 9–15 obligation, name the rubric row(s) that discharge it. Preview mod-106.
- Draft an **audit table** that walks a hypothetical AIMS auditor through the rubric per ISO/IEC 42001 clause 9.1: for each 9.1 monitoring topic, name the rubric rows that are the monitored characteristic. Preview chapter `03`.
- Extend the rubric with **freshness and cadence** columns (preview chapter `04`'s consumer-side contract row). Note where the freshness clashes with the peer's realistic cadence and would trigger a renegotiation.
- Draft a short **rubric-change SOP** — when the rubric can be revised, who signs, what the diff looks like, how the diff propagates into exercise-01's criterion set and into exercise-05's dashboard.
