# The Release-Gate Rubric — ISO/IEC 25059 Cross-Mapped to NIST AI RMF MEASURE

## Motivation

A release-gate rubric is the *columnar* view of the criterion set from chapter `01`. If the criterion set is a bag of thresholds, it becomes very hard to answer three questions: (1) does the gate *cover* the qualities the framework requires, (2) is the coverage *balanced* across quality dimensions, and (3) does each criterion map to an *auditable* framework hook? A rubric answers all three by fixing the columns first, then hanging criteria under them.

Two standards do most of the work.

**ISO/IEC 25059:2023** is the SQuaRE-family extension for AI systems. It inherits the ISO/IEC 25010 software-quality model and adds and adapts characteristics for AI: **functional adequacy**, **robustness**, **transparency**, **controllability**, **user-controllability**, **adaptability** (in the AI sense — the system's ability to remain fit-for-purpose under changes in input distribution or task), and **appropriate use of data**. It also refines existing quality characteristics (functional suitability, performance efficiency, usability, reliability, security, maintainability, portability, compatibility) with AI-specific sub-characteristics.

**NIST AI RMF 1.0** (mod-101 chapter `02`) organises measurement work under the **MEASURE** function. MEASURE has four sub-functions (MEASURE-1 through MEASURE-4) and roughly two dozen sub-categories that spell out what "measure" concretely means at operational scope.

Structuring the rubric around ISO/IEC 25059's characteristics and cross-mapping each row to a NIST AI RMF MEASURE sub-category gives every criterion two anchors: a *quality dimension* the criterion serves, and a *measurement obligation* the criterion discharges. Regulators and internal-audit read the rubric by walking those anchors. Peer tracks read the rubric to see where their evidence lands. And the assurance-case editor (mod-102) resolves each SACM `Claim.id` against a specific rubric row.

## What ISO/IEC 25059 actually adds

25059 keeps 25010's eight top-level characteristics and their sub-characteristics, and adds AI-specific quality characteristics and sub-characteristics that reflect the shape of an AI system. The ones that matter most for a release-gate rubric:

- **Functional adequacy.** How well the AI system's outputs match the intended function. This is the classic "does it work?" column. Sub-characteristics include appropriateness (the outputs are of the right type and shape) and accuracy (the outputs are correct at a stated rate).
- **Robustness.** How stable the outputs are under distributional shift, noisy input, adversarial input, and edge-case conditions. Robustness is where the 25059 model bites deepest, because the standard makes explicit that robustness is *not* a subset of accuracy — a system can be highly accurate on a benchmark and fragile under any drift. ISO/IEC 24029-2 provides the deeper methodology behind neural-network robustness measurement (mod-101 chapter `03`).
- **Transparency.** How well the system exposes the information a user, a deployer, an evaluator, or a regulator needs to understand its behaviour. Model / system / dataset cards (mod-105) are the operational form of transparency. EU AI Act Article 13 (transparency to deployers) and Article 26 (deployer obligations) are the statutes this dimension discharges.
- **Controllability.** How well a human operator can control the system's behaviour — interruption, override, human-in-the-loop, human-on-the-loop, and human-out-of-the-loop patterns. EU AI Act Article 14 (human oversight) is the primary statute; 25059 gives the quality-model shape.
- **Adaptability.** How well the system remains fit-for-purpose under environmental or task change. For a static model, adaptability is a scope claim ("the system is validated for this data range and not beyond"). For a system that fine-tunes, retrieves, or otherwise adapts online, adaptability includes the *governance* of that adaptation — this is where FDA's Predetermined Change Control Plan (PCCP) approach lives, and where ISO/IEC 42001 clause 8 change-control expectations attach.
- **Appropriate use of data.** How well the system's data lifecycle aligns with the purposes it was scoped for, at the granularity of collection, labelling, splitting, testing, deployment, and retirement. ISO/IEC 5259 (data-quality) and ISO/IEC 8183 (AI data-lifecycle) support this dimension. EU AI Act Article 10 (data governance) is the primary statute.

25059 also treats **usability** (with sub-characteristics for interpretability by the intended user), **reliability** (with attention to intermittency and gradual degradation modes), **security** (which the gate largely delegates to `ai-infra-security`), **maintainability**, **portability**, **compatibility**, and **performance efficiency** — but the six above tend to dominate the rubric for AI-specific release-gates. The exact allocation depends on the deployment surface and the sector, and mod-107 (sector-regulated assurance) refines the balance for regulated sectors.

## What NIST AI RMF MEASURE actually asks for

MEASURE is one of the four NIST AI RMF functions. Its sub-categories fall into four sub-functions (paraphrased from the AI RMF and the Playbook — the actual sub-category identifiers are stable and should be cited verbatim in the rubric):

- **MEASURE-1** — appropriate methods and metrics are identified and applied. This is where the release-gate rubric commits to *which* metric it uses, and where the model-eval track's statistical warrant lives.
- **MEASURE-2** — AI systems are evaluated for trustworthy characteristics (fairness/bias, robustness, security/resilience, accuracy, explainability/interpretability, privacy, safety). MEASURE-2 has the largest surface — sub-categories cover accuracy, safety, security and resilience (which cites AI 100-2's adversarial-ML taxonomy), fairness / harmful bias, explainability / interpretability, privacy, environmental impact, and other trustworthy characteristics.
- **MEASURE-3** — mechanisms for tracking identified AI risks are in place. This is the *continuous* face of MEASURE — the online-eval, drift-detection, and post-market monitoring that mod-104 and mod-110 own. The release-gate rubric cites MEASURE-3 for criteria whose satisfaction is *ongoing*, not point-in-time.
- **MEASURE-4** — feedback about efficacy of measurement is gathered and assessed. This is where the rubric itself is challenged. Internal audit, third-party evaluator feedback, and post-hoc gate-decision reviews land here.

Every ISO/IEC 25059 characteristic maps into one or more MEASURE sub-categories. The mapping is many-to-many; a robust rubric row cites *one* 25059 characteristic and *the specific* MEASURE sub-category identifier, not a range.

## Building the rubric — column headers

The rubric is a table with (at minimum) these columns:

| Column                 | Content                                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Criterion ID           | Stable ID (`GATE-FA-01`, `GATE-ROB-03`, etc.). Cross-referenced by the assurance case (mod-102) `Claim.id`.                                    |
| 25059 dimension        | Functional adequacy / Robustness / Transparency / Controllability / Adaptability / Appropriate use of data / (others per 25010 as needed).    |
| 25059 sub-characteristic | The specific sub-characteristic within the dimension, cited to the standard.                                                                |
| NIST AI RMF MEASURE    | The specific sub-category identifier (e.g. `MEASURE-2.5`, `MEASURE-2.7`, `MEASURE-3.1`).                                                     |
| EU AI Act article      | If applicable (Article 9–15, 26, 55, 61, 72). Blank if the criterion is not statute-tied.                                                    |
| ISO 42001 clause       | The clause the criterion's *evidence* discharges (typically 8.x or 9.x — see chapter `03`).                                                  |
| Sector rule            | If applicable (SR 11-7 model-risk clause, FDA GMLP principle, DORA article, etc.). Blank if not sector-scoped.                                |
| Metric                 | The named metric and its estimator (e.g. "per-class F1 with 95% bootstrap CI"; "ECE with 10-bin equal-width binning"; "attack-success rate on threat-model T"). |
| Threshold              | The pass level, hard-floor, or trend-direction. Cited to the harm-inventory row or the internal-goal that fixes it.                          |
| Hard / soft            | With a one-line justification.                                                                                                              |
| Owner peer track       | analyst L15 / risk L25 / AI-eval L30 / model-eval L30 / MLSec L35 / third-party.                                                            |
| Evidence pointer       | The SACM `Artifact` ID and the peer's evidence-contract clause.                                                                              |

The rubric row is a *design* artefact; the criterion set (chapter `01`) is the *runtime* artefact. Every runtime criterion resolves to exactly one rubric row; every rubric row may generate one or many runtime criteria (per deployment surface, per model version).

## Populating the rubric — the six dimensions, worked

### Functional adequacy

- **What the dimension asks.** Does the system do what it's for, at a stated rate, over the intended input distribution?
- **Typical metric.** Task-appropriate accuracy or F1, framed with confidence intervals; recall or precision at operating point for classification systems; groundedness for RAG systems; task-completion rate for agents; BLEU / ROUGE / task-specific rubric scores where they discharge a stated function.
- **NIST AI RMF MEASURE hooks.** Primarily MEASURE-2.5 (evaluation involving external sources / representative-of-intended-use) and MEASURE-1.1 (approaches identified and applied). MEASURE-2.11 sub-categories cover the fairness slice; MEASURE-2.9 the explainability slice.
- **EU AI Act.** Article 15(1) accuracy.
- **ISO/IEC 42001.** Clause 8.1 (operational control), clause 9.1 (monitoring, measurement, analysis, evaluation).
- **Where the evidence comes from.** The model-evaluation engineer owns the estimator; the AI-eval engineer owns the pipeline that measures it in the product context.

### Robustness

- **What the dimension asks.** Does the system stay within its stated accuracy / safety envelope under distribution shift, noise, adversarial perturbation, and edge-case input?
- **Typical metric.** Accuracy delta under stress-set, adversarial-attack-success rate (adversarial suite depth per AI 100-2 threat categories), stability under input perturbation (`24029-2` methodologies), long-tail slice accuracy.
- **NIST AI RMF MEASURE hooks.** MEASURE-2.6 (safety), MEASURE-2.7 (security and resilience — cites AI 100-2), MEASURE-2.10 (privacy), MEASURE-2.11 (environmental impact) depending on the specific robustness slice.
- **EU AI Act.** Article 15(1) robustness; Article 15(4) cybersecurity resilience.
- **ISO/IEC 42001.** Clause 8.1, clause 8.3 (impact assessment during operation).
- **Where the evidence comes from.** The risk engineer owns the adversarial and harm-driven slice; the model-eval engineer owns the statistical warrant on the robustness metric; the MLSec peer owns the security / supply-chain slice.

### Transparency

- **What the dimension asks.** Can each audience (users, deployers, evaluators, regulators, board) get the information they need to understand and correctly rely on the system?
- **Typical metric.** Coverage of the model / system / dataset card sections against a template (mod-105 owns the template and its per-audience variants), presence-and-freshness of the DoC (EU AI Act Article 47) and registration (Article 49), presence of the deployer-facing transparency notice (Article 13) and user-facing disclosures (Article 50 where applicable).
- **NIST AI RMF MEASURE hooks.** MEASURE-2.8 (explainability and interpretability), MEASURE-4.2 (documentation and communication), MEASURE-2.9 (transparency-related sub-categories).
- **EU AI Act.** Article 13 (transparency to deployers), Article 47 (DoC), Article 50 (disclosure), Article 26 (deployer obligations).
- **ISO/IEC 42001.** Clause 7.4 (communication), clause 8.1.
- **Where the evidence comes from.** Cards live in mod-105 (this program owns them); the analyst produces first-drafts; the AI-eval engineer owns the traces and evaluations that populate the "performance" section of the card.

### Controllability

- **What the dimension asks.** Can a human operator (or an automated fail-safe) stop, override, or steer the system when needed? Is the human-oversight mode named, tested, and monitored?
- **Typical metric.** Presence and coverage of oversight mechanisms; time-to-intervention benchmarks; false-intervention rate; escalation-path coverage; guardrail-effectiveness measurements from the risk engineer's guardrail-eval.
- **NIST AI RMF MEASURE hooks.** MEASURE-2.6 (safety, including human-oversight sub-categories) and MEASURE-3.3 (feedback mechanisms).
- **EU AI Act.** Article 14 (human oversight).
- **ISO/IEC 42001.** Clause 8.1 (operational control), clause 9.1 (monitoring).
- **Where the evidence comes from.** The risk engineer owns guardrail-eval; the AI-eval engineer owns operator-in-the-loop instrumentation; the assurance program cites both.

### Adaptability

- **What the dimension asks.** How does the system remain fit-for-purpose as inputs, tasks, or deployment context change? For static models, this is a scope claim; for adaptive systems, it is a change-control claim.
- **Typical metric.** For static systems: drift-detection thresholds (mod-110 owns the ongoing signals); for adaptive systems: the change-control envelope (permitted changes, retraining triggers, the PCCP-style scope for the specific FDA-regulated case); the frequency and depth of re-evaluation.
- **NIST AI RMF MEASURE hooks.** MEASURE-3.1 and MEASURE-3.2 (mechanisms for tracking risks, including drift).
- **EU AI Act.** Article 72 (post-market monitoring); Article 61 (post-market reporting of serious incidents); Article 15 (accuracy over the lifecycle).
- **ISO/IEC 42001.** Clause 8.2 (change-control on operation), clause 9.1, clause 10.1 (improvement).
- **Where the evidence comes from.** The AI-eval engineer's online-eval slice, the risk engineer's incident-derived learnings, and the change-management SOP.

### Appropriate use of data

- **What the dimension asks.** Are the data used to train, calibrate, evaluate, and monitor the system fit for those purposes, per the stated scope? Are there disjointness controls that prevent benchmark contamination? Is data governance auditable end-to-end?
- **Typical metric.** Datasheet coverage (Gebru et al.), ML-BOM completeness (mod-104), training-eval disjointness attestations, data-source provenance records, per-jurisdiction data-scope declarations.
- **NIST AI RMF MEASURE hooks.** MEASURE-2.10 (privacy), MEASURE-2.11 (bias / representativeness), MEASURE-2.12 (data-integrity), MEASURE-4.2 (documentation of data).
- **EU AI Act.** Article 10 (data governance).
- **ISO/IEC 42001.** Clause 7.5 (documented information), clause 8.3, Annex A controls under "Data for AI systems."
- **Where the evidence comes from.** The model-evaluation engineer owns benchmark-construction and contamination disjointness; the MLSec peer owns the eval-set exfiltration controls; the analyst produces the first-draft datasheet.

## Balance across dimensions

A rubric that lands only in functional adequacy is a rubric that will pass a lopsided release. A useful discipline: for the rubric to be approved at each deployment surface, it has to have *at least one hard-gate criterion* in each of functional adequacy, robustness, transparency, and controllability at T2 and above, and at least one *tracked criterion* (hard or soft) in adaptability and appropriate use of data at T1 and above. The specific hard-count and soft-count per dimension is a program choice; the point is that *every* dimension appears in the rubric, and *coverage* is auditable.

Where a program cannot furnish a criterion in a dimension (for example, an internal-only pilot has no controllability human-oversight mechanism because it is not user-facing), the rubric row is filled with `N/A — scope excluded`, cited to the deployment-surface scope decision. `N/A` is a *documented* choice, not an omitted row.

## Cross-mapping — a worked row

Take a criterion: "Per-class F1 ≥ 0.85 on calibration-set v3, with 95% bootstrap CI lower-bound ≥ 0.83, for the customer-intent classifier on the T2 deployment surface." The rubric row:

| Column                 | Content                                                                                                       |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| Criterion ID           | `GATE-FA-01`                                                                                                  |
| 25059 dimension        | Functional adequacy                                                                                           |
| 25059 sub-characteristic | Functional correctness (per 25010) and appropriateness recognisability (25059 extension where relevant)      |
| NIST AI RMF MEASURE    | `MEASURE-2.5` (evaluation involving external sources / representative-of-intended-use)                        |
| EU AI Act article      | Article 15(1) accuracy                                                                                        |
| ISO 42001 clause       | 8.1 (operational control), 9.1 (monitoring, measurement, analysis, evaluation)                                |
| Sector rule            | N/A (customer-service classifier, not regulated sector)                                                       |
| Metric                 | Per-class F1 with 95% bootstrap CI, `n=10_000` resamples, per MOD-EVAL evidence-contract v1 §4                |
| Threshold              | Point-estimate ≥ 0.85 *and* CI lower-bound ≥ 0.83, on calibration-set v3                                       |
| Hard / soft            | Hard — Article 15(1) accuracy is a statute obligation for high-risk systems                                    |
| Owner peer track       | model-evaluation-engineer (L30)                                                                               |
| Evidence pointer       | `Artifact:eval-report-rc-<hash>.json`, SACM `C1.1.15.a`                                                        |

The single row cross-references six frameworks and one peer track. The gate walker (chapter `01`) reads the row, resolves the evidence pointer, evaluates the threshold, and produces the runtime disposition for `GATE-FA-01`.

## Common failure modes

- **Cross-mapping to a topic instead of a sub-category identifier.** Writing "MEASURE — accuracy" is not a citation. Sub-category IDs (`MEASURE-2.5`) are stable; topics rot.
- **Choosing one 25059 characteristic and pretending it's the rubric.** A rubric that only covers functional adequacy fails the balance rule above.
- **Confusing 25010 characteristics with 25059 additions.** 25059 both *inherits* the 25010 characteristics and *adds* AI-specific ones. Cite the standard the sub-characteristic actually lives in.
- **Missing the sector rule column.** A high-risk system in a regulated sector needs the sector rule cited; a rubric that only cites the horizontal frameworks will be a gap the sector auditor finds.
- **Handing the same row to two peer tracks.** Contested rows (fairness, judge quality, threshold — mod-102 chapter `06`) split into two rows, not one shared row.

## Where this feeds

- Chapter `03` — the ISO 42001 clause column feeds the mapping from gate outputs into clause 8 and clause 9 evidence.
- Chapter `04` — the owner-peer column and the evidence pointer feed the consumer contracts with each peer track.
- Chapter `05` — the hard / soft column feeds the runbook: what triggers rollback, what triggers a deferred approval, what triggers an exception.
- Chapter `06` — the metric, threshold, and freshness columns feed the dashboard fields.

## Summary

- The rubric is the columnar view of the criterion set: dimensions on the top, criteria as rows.
- Structure dimensions around ISO/IEC 25059 (functional adequacy, robustness, transparency, controllability, adaptability, appropriate use of data — plus the inherited 25010 characteristics where relevant). Cite the exact sub-characteristic per the standard.
- Cross-map each row to a specific NIST AI RMF MEASURE sub-category identifier; do not use a topical shorthand.
- Add the EU AI Act article, the ISO/IEC 42001 clause, and (where applicable) the sector rule. `N/A — scope excluded` is a documented answer, not an omitted row.
- Balance is auditable: every dimension appears; at T2 and above, at least one hard-gate criterion per dimension.
- Each rubric row names the owner peer track and points to the SACM `Artifact` id the gate walker resolves.
- The next chapter maps the gate's outputs into ISO/IEC 42001 clauses 8 and 9 so the AIMS auditor sees the trail end-to-end.
