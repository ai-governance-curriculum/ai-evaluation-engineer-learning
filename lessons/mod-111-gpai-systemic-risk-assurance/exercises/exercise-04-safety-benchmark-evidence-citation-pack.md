# exercise-04: Safety-Benchmark Evidence Citation Pack

**Estimated effort:** 3 hours

## Objective

Build the **safety-benchmark evidence citation pack** for the release from exercise `01` — the assurance-case-visible artefact that discharges Article 55(1)(a)'s "state-of-the-art model evaluation ... including adversarial testing" language with a uniform citation shape across every benchmark cited. The pack indexes each cited benchmark by name and version, resolves each row to a specific reproducibility bundle in the store (`mod-104` chapter `03`), and — critically — cites peer-owned methodology for the *reading* of every result without duplicating the depth owned by `model-evaluation-engineer`, `ai-risk-engineer`, and `agentic-safety-engineer` (level 40).

The exercise is citation-pack authoring, not solving. Placeholder benchmark results, `<!-- needs-research: … -->` markers, and pointers into peer artefacts (that this exercise does not itself produce) are legitimate answers.

## Prerequisites

- Chapter [`04-safety-benchmark-evidence-citation-pack.md`](../04-safety-benchmark-evidence-citation-pack.md) — the uniform citation shape, the specific benchmarks (MLCommons AILuminate, AIR-Bench 2024, HarmBench, AgentDojo, InjecAgent, SafetyBench, CyBench, WMDP), the peer-methodology-ownership discipline, and the recurring anti-patterns (benchmark laundering, version drift, reinterpretation drift, coverage inflation).
- Chapter [`01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md`](../01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md) — Article 55(1)(a) is the statutory driver.
- Chapter [`03-aisi-tevv-and-nist-ai-600-1-generative-ai-profile-as-the-evaluator-envelope.md`](../03-aisi-tevv-and-nist-ai-600-1-generative-ai-profile-as-the-evaluator-envelope.md) — the pack populates the "Testing artefacts" column of the TEVV index and lands under the safety-relevant AI 600-1 categories.
- Skim access to the arXiv preprints (or landing pages) for each cited benchmark:
  - [MLCommons AI Safety Working Group / AILuminate](https://mlcommons.org/ai-safety/).
  - [AIR-Bench 2024 (arXiv:2407.17436)](https://arxiv.org/abs/2407.17436).
  - [HarmBench (arXiv:2402.04249)](https://arxiv.org/abs/2402.04249).
  - [AgentDojo (arXiv:2406.13352)](https://arxiv.org/abs/2406.13352).
  - [InjecAgent (arXiv:2403.02691)](https://arxiv.org/abs/2403.02691).
  - [SafetyBench (arXiv:2309.07045)](https://arxiv.org/abs/2309.07045).
  - CyBench (`<!-- needs-research: verify current arXiv or landing-page URL -->`).
  - [WMDP (arXiv:2403.03218)](https://arxiv.org/abs/2403.03218).
- Familiarity with `mod-104` chapter `03` (reproducibility bundle shape), chapter `02` (content-addressed store), and chapter `06` (signed assurance bundle).

## Problem statement

Continue from the release pinned in exercise `01` (or pin one afresh). The pack must:

- **Cite every benchmark that discharges an Article 55(1)(a) claim for the release's modality set and deployment surface.** For a text-only closed-weight LLM without tool use, agentic benchmarks (AgentDojo, InjecAgent) may be out-of-scope with a stated reason. For a multimodal agentic model, essentially all named benchmarks apply.
- **Adopt the uniform citation shape from chapter `04`.** Every row carries the seven fields (name, version, source, configuration, result, peer methodology reference, reproducibility bundle reference). No shortcuts, no ad hoc rows.
- **Cite peer artefacts, not peer methodology.** Every row's *peer methodology reference* field points at a `model-evaluation-engineer` or `ai-risk-engineer` or `agentic-safety-engineer` artefact that carries the methodology reading. The pack does not itself interpret scores.
- **Include the state-of-the-art justification.** Chapter `01` names this — the assurance case has to record *why* this set at *this* release is the state of the art. The pack carries a distinct state-of-the-art justification artefact.

## Requirements

Produce five artefacts in a single directory.

### 1. `pack-scoping-brief.md`

A one-page brief that pins the pack's scope:

- **Release under evaluation.** The model name, version, digest, and modality set from exercise `01`.
- **Deployment surface.** Closed-weight via API, gated-open, or open-weight; tool-use enabled or not; the specific tool set if applicable.
- **AI 600-1 categories the pack addresses.** From exercise `03`'s crosswalk (or a fresh pin) — the safety-relevant categories the pack's citations feed evidence to. Cross-reference chapter `03`.
- **Article 55(1)(a) discharge claim.** The specific top-level claim in the assurance case (`mod-102`) the pack discharges — "the release has been evaluated in accordance with state-of-the-art protocols and adversarial testing has been conducted and documented as of the release date."
- **In-scope / out-of-scope benchmarks.** For each of the eight benchmarks named in chapter `04`, state whether it is in-scope for the release with a one-sentence reason. Out-of-scope must state where the corresponding capability is otherwise evaluated (e.g., "AgentDojo out-of-scope because the release does not carry tool-use; agentic capability is addressed via internal red-team `red-team-agentless-v3`").
- **Frontier-agent evidence subset.** From `agentic-safety-engineer` (level 40) — which agentic red-team reports are cited by reference (chapter `04` treats these as a distinct evidence category consumed by reference, not duplicated).

### 2. `benchmark-citation-pack.md`

The pack itself. Structured as a table with the following columns:

| Column | Content |
| --- | --- |
| Benchmark | The benchmark's canonical name. |
| Version / date | The version identifier (or release date; benchmarks are versioned inconsistently). Mark `<!-- needs-research: verify current version -->` if the pin is uncertain. |
| Source | The publication (arXiv identifier), landing page, or GitHub repository the version resolves to. |
| Configuration | Which sub-tasks were selected, decoding parameters, evaluator-model choice, temperature, sampling budget, attack methodologies (for HarmBench and InjecAgent), tool set (for AgentDojo). |
| Result | The score(s) reported, in the reporting convention the benchmark uses (grade, accuracy, ASR, per-category vector). Placeholders acceptable — the discipline is *shape*, not *specific numbers*. |
| Peer methodology reference | The store digest and artefact class of the peer-owned artefact that carries the methodology reading. Points at `model-evaluation-engineer`, `ai-risk-engineer`, or `agentic-safety-engineer` (level 40). |
| Reproducibility bundle reference | The store digest of the reproducibility bundle (`mod-104` chapter `03`) that contains the evaluation run. |
| AI 600-1 category | The primary AI 600-1 category the citation feeds evidence to; secondary categories in parentheses. |
| Article 55(1)(a) sub-claim | The specific sub-claim in the assurance case the citation discharges. |

At minimum, the pack has one row for each in-scope benchmark from artefact 1. For a text-only closed-weight LLM:

- **AILuminate** — per-hazard grades, overall grade.
- **AIR-Bench 2024** — per-category scores across the derived-from-regulation taxonomy.
- **HarmBench** — per-behaviour ASR across the configured attack methodologies.
- **SafetyBench** — per-category multiple-choice accuracy (note the multiple-choice-vs-generation distinction from chapter `04`).
- **CyBench** — per-category CTF task-solve rates.
- **WMDP** — per-domain accuracy (bio, cyber, chem), plus the pre-/post-unlearning delta if an unlearning intervention was applied.

For an agentic release, add:

- **AgentDojo** — utility on benign tasks, targeted attack success rate on injections, untargeted attack success rate.
- **InjecAgent** — indirect prompt injection targeted / untargeted attack success rate.

Under the table, include a two-paragraph *anti-pattern-avoidance note* that names, per benchmark, the anti-pattern the citation is guarding against. Chapter `04`'s four recurring anti-patterns (benchmark laundering, version drift, reinterpretation drift, coverage inflation) are the vocabulary.

### 3. `state-of-the-art-justification.md`

The justification narrative for *why* the cited set is the state of the art at the release date. Structured as follows:

- **Reference set.** The public library the justification anchors against — [Frontier Model Forum](https://www.frontiermodelforum.org/) issue briefs (cross-reference exercise `02`), AISI publications (cross-reference exercise `03`), the Code-of-Practice safety-and-security chapter, MLCommons AI Safety Working Group publications.
- **Benchmark-choice rationale.** Per benchmark in the pack, one to two sentences on *why this benchmark* (not another) at the release date. Anchor into the reference set — a Frontier Model Forum brief citing the benchmark, an AISI publication using the benchmark, or a Code-of-Practice implementation guideline recommending it. `<!-- needs-research: verify current AISI methodology publications and current FMF issue-brief list -->` where necessary.
- **Coverage argument.** A two-paragraph argument that the pack's benchmarks *together* cover the state-of-the-art surface for the release's modality set and deployment surface. Name any known gaps and how the assurance case handles them (via red-team evidence, via peer artefacts not in this pack, via a `<!-- needs-research: … -->` marker if the gap has no cover yet).
- **Adversarial-testing discipline.** How the pack's citations satisfy Article 55(1)(a)'s "conducting and documenting adversarial testing" language — cite the HarmBench / AgentDojo / InjecAgent rows plus the internal red-team artefacts, and note the frontier-agent red-team evidence from `agentic-safety-engineer` consumed by reference.
- **Signer.** The head-of-AI-governance role (or equivalent) signs the state-of-the-art justification. Placeholder name is legitimate.

### 4. `peer-methodology-reference-index.md`

For each row in `benchmark-citation-pack.md`, this index resolves the peer methodology reference to a specific peer role and a specific peer artefact class:

- **Row identifier.** The row's benchmark name (matches artefact 2).
- **Peer role.** `model-evaluation-engineer`, `ai-risk-engineer`, `agentic-safety-engineer` (level 40), or another peer role explicitly named.
- **Peer artefact class.** The class in the peer's own store (e.g., `benchmark-reading-methodology`, `red-team-methodology-note`, `mitigation-effectiveness-methodology`). Placeholder class names are legitimate.
- **Peer artefact store digest.** The content-addressed digest, or a placeholder + `<!-- needs-research: verify actual digest once the peer artefact is committed -->`.
- **What the peer artefact carries.** One to two sentences on the methodology reading the peer artefact provides — the score's statistical properties, the coverage claim, the interpretation of the result in context.
- **Escalation path.** Which peer role receives methodology questions from the third-party evaluator (chapter `03`) or from the AI Office reviewer if the citation is challenged.

The index is the *discipline artefact*. Chapter `04`'s reinterpretation-drift anti-pattern is exactly what this index prevents: the release-assurance methodology owner *cites*; the peer *interprets*.

### 5. `frontier-agent-evidence-by-reference.md`

The frontier-agent red-team evidence from `agentic-safety-engineer` (level 40) is a distinct evidence category the pack cites but does not enumerate at the same shape as the benchmarks. This artefact captures the reference discipline:

- **Frontier-agent evidence set.** The specific reports from `agentic-safety-engineer` at level 40 cited in the assurance bundle for this release. Include: structured red-team evaluations of agentic capabilities (sandboxed multi-step task completion under adversarial conditions), elicitation studies for tool-access-only or extended-context-only capabilities, and mitigation-effectiveness evaluations for agentic guardrails.
- **Per-report citation shape.** For each report, the same seven-column shape as `benchmark-citation-pack.md` — name, version, source (the peer's own store), configuration, result summary, peer methodology reference (which points at the level-40 role explicitly), and reproducibility bundle reference.
- **Boundary note.** Explicit note that the *methodology depth* of the frontier-agent reports is owned by the level-40 role. The pack cites; it does not restate. If the AI Office reviewer wants to walk the methodology, the walk goes through the level-40 role's own artefacts.
- **Non-duplication check.** A list of methodology areas the release-assurance programme has *not* attempted to duplicate — attacker-effort calibration, agentic-scaffold-coverage claims, sandbox-escape probes, cost-limit-evasion probes — with pointers at the level-40 role's owner artefacts.

## Starter guidance

- **The uniform citation shape is non-negotiable.** Chapter `04` opens with it and returns to it. Every row carries the seven fields, or the pack collapses. If a field cannot be pinned yet, mark `<!-- needs-research: … -->` — do not omit the column.
- **Pin the benchmark version.** Chapter `04`'s version-drift anti-pattern is what this pack guards against most directly. Benchmark suites revise; a citation without a version is un-walkable six months later. If the version is uncertain, mark and move on.
- **The peer methodology reference is a hard link, not a category name.** "Owned by `model-evaluation-engineer`" is not a peer methodology reference. A digest into `model-evaluation-engineer`'s own artefact store (or a placeholder + `<!-- needs-research: … -->`) is.
- **Coverage arguments are honest.** Chapter `04`'s coverage-inflation anti-pattern is easy to reintroduce in the state-of-the-art justification. If the pack has a gap — a category the benchmarks do not cover, a modality the pack does not evaluate — say so. Say what covers the gap (red-team, peer artefact, out-of-scope justification), or mark the gap `<!-- needs-research: … -->`.
- **HarmBench and AgentDojo require configuration.** Both benchmarks are attack-methodology configurable; the configuration column has to name *which methodologies* were configured. A HarmBench citation with an unnamed methodology is a citation of a moving target.
- **WMDP is a proxy, not a use test.** Chapter `04` calls out the proxy-vs-use distinction. The peer methodology reference names it explicitly; the reader of the pack should not conclude from a low WMDP score that the model cannot be *used* for hazardous ends.
- **SafetyBench's format matters.** Multiple-choice accuracy is a different question from open-ended-generation safety. The peer methodology reference names the distinction; the reader should not conclude from a high SafetyBench score that open-generation safety is discharged.
- **Frontier-agent evidence is by reference, not by duplication.** `frontier-agent-evidence-by-reference.md` explicitly names the boundary. The release-assurance programme carries the level-40 role's report by digest; the methodology depth stays with the level-40 role.
- **The state-of-the-art justification is signed.** It is not a boilerplate paragraph; it is a signed narrative that the head-of-AI-governance role attests to at release date.
- **`<!-- needs-research: … -->` is a legitimate answer.** Benchmark versions, arXiv identifiers, current publication landing pages, and the current AISI methodology publications drift. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `pack-scoping-brief.md` fixes the release, the deployment surface, the AI 600-1 categories, the discharge claim, and the in-scope / out-of-scope benchmark set with a one-sentence reason per row. The frontier-agent evidence subset is enumerated.
- `benchmark-citation-pack.md` has one row per in-scope benchmark from artefact 1, each carrying all nine columns (benchmark, version, source, configuration, result, peer methodology reference, reproducibility bundle reference, AI 600-1 category, Article 55(1)(a) sub-claim). Every version is pinned or marked `<!-- needs-research: … -->`. The anti-pattern-avoidance note is present.
- `state-of-the-art-justification.md` carries the reference set, per-benchmark choice rationale, coverage argument, adversarial-testing discipline, and signer. Anchors into the Frontier Model Forum, AISI publications, and the Code of Practice are cited.
- `peer-methodology-reference-index.md` resolves every row in artefact 2 to a specific peer role, artefact class, store digest (or placeholder + `<!-- needs-research: … -->`), and escalation path.
- `frontier-agent-evidence-by-reference.md` carries the frontier-agent evidence set with the seven-column citation shape, plus the boundary note and the non-duplication check.
- No row's peer methodology reference is missing or generic. No score is *reinterpreted* by the pack; the peer artefact is where interpretation lives.
- Every place a fact would need to be verified against a current benchmark version, a current AISI methodology publication, or a specific peer artefact digest is marked `<!-- needs-research: … -->` rather than guessed.
- The coverage argument is honest — gaps are named, not glossed over.
- The state-of-the-art justification is signed (with a placeholder role name if the actual signer is not pinned).

## Stretch goals

- **Add a fairness-benchmark supplement (by reference).** In `fairness-benchmark-supplement.md`, cite the fairness benchmarks (BBQ, WinoBias, HolisticBias) as a *reference* pack — noting they are owned by `ai-risk-engineer` and not part of the Article 55(1)(a) core pack (chapter `04` explicitly scopes them out). This makes the coverage argument tighter.
- **Author the reproducibility-bundle worked example.** In `worked-reproducibility-bundle.md`, pick one row from `benchmark-citation-pack.md` and expand the reproducibility bundle end-to-end — the evaluation definition, the pinned dependencies, the run instructions, the result recording. Cross-reference `mod-104` chapter `03`.
- **Draft the benchmark-refresh cadence.** In `benchmark-refresh-cadence.md`, sketch how the pack is refreshed on new benchmark versions or new benchmarks — the review cadence (quarterly for benchmark versions, on-demand for new benchmarks), the responsible role, the interlock with the frontier-framework re-evaluation cadence (exercise `02`).
- **Cross-reference `mod-108`.** In `mod-108-tier-evidence-note.md`, describe how the pack's citations feed the frontier-framework tier landing (exercise `02`, `mod-108` chapter `02`). A WMDP score is capability evidence; the tier decision consumes it via `mod-108`'s scheme.
- **Draft the AI-Office-visible summary.** In `ai-office-benchmark-summary.md`, write the one-page reviewer-facing summary of the pack — the benchmark set, the state-of-the-art justification, the peer methodology owners, and the walk-path an AI Office reviewer follows to resolve any citation to its reproducibility bundle. This is the reviewer-facing surface the pack presents.
