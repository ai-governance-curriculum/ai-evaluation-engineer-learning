# exercise-05: FRVT Shape Lessons and Enterprise Adaptation

**Estimated effort:** 2 hours

## Objective

Read a **current FRVT / FRTE round** and adapt the **five shape lessons** (sealed evaluation, published demographic breakdowns, versioned vendor identifiers, longitudinal comparison across evaluation rounds, portfolio across modalities) into a **next-generation AISI-shape engagement design** for one enterprise deployment. Produce the shape-study report, the sealed-evaluation concept-of-operations, the versioned-identifier and longitudinal-comparison design, the portfolio-adapter design, and the two-disanalogy defence memo that names where the shape lessons stop generalising.

The exercise is design and authoring, not solving. The core discipline is *shape study* — reading FRVT/FRTE for the workflow pattern rather than for its biometric-specific content, and adapting the pattern to the AISI-shape interface at the maturity level FRVT/FRTE has reached over two decades.

## Prerequisites

- Chapter [`05-frvt-frte-as-the-public-sector-independent-evaluator-worked-example.md`](../05-frvt-frte-as-the-public-sector-independent-evaluator-worked-example.md) — the FRVT / FRTE programme, the sealed-envelope workflow, the demographic-differentials report shape, the five shape lessons, and the two disanalogies (deployment surface, evaluation ownership).
- Chapter [`01-aisi-shape-third-party-evaluators-and-attack-payload-non-disclosure.md`](../01-aisi-shape-third-party-evaluators-and-attack-payload-non-disclosure.md) — the current AISI-shape interface's six-component envelope and the three-pipe non-disclosure discipline, which the sealed-evaluation adaptation is designed to *replace at the workflow level* over time.
- Chapter [`06-delivery-timing-envelope-and-evidence-hardening-playbook.md`](../06-delivery-timing-envelope-and-evidence-hardening-playbook.md) — the engagement-charter and evidence-hardening playbook the sealed-evaluation adaptation slots into.
- Familiarity with `mod-104` chapter `02` (evidence-pipeline adapters, including the AISI-interface adapter) and `mod-104` chapter `04` (model-digest pinning and ML-BOM SPDX/SLSA/Sigstore packaging) — the substrate the sealed-evaluation adaptation runs on.
- Access to the current FRVT/FRTE ongoing-results publication at [pages.nist.gov/frvt/](https://pages.nist.gov/frvt/) <!-- needs-research: verify current results-publishing URL and the current track structure --> and to the NIST FRVT/FRTE programme home at [nist.gov/itl/iad/image-group/face-recognition-vendor-test-frvt](https://www.nist.gov/itl/iad/image-group/face-recognition-vendor-test-frvt).

## Problem statement

Pick one enterprise deployment being handed to an AISI-shape evaluator (the same shape as exercise `01`, but pinned to a target end-state design at FRVT/FRTE-level maturity rather than to the current AISI-shape interface's bespoke state). Two dimensions to pin:

- **Deployment shape.** A frontier-tier deployment whose surface and user population justify an AISI-shape engagement. Common shapes worth considering are the same set as exercise `01` (internal-facing coding-and-agent assistant, external customer-support agent, analyst-copilot for regulated-industry decision support, long-horizon research agent). If you did exercise `01`, using the *same* deployment here is legitimate — the exercise's discipline is designing the *next-generation* interface for the same underlying engagement.
- **Evaluator identity.** One AISI-shape evaluator. Where exercise `01` accepts any of UK AI Security Institute, US AI Safety Institute, Singapore AI Verify Foundation, METR, Apollo Research, or MLCommons AI Safety Working Group, this exercise's five shape lessons apply most directly to the *sovereign or quasi-sovereign* institutes (UK / US / Singapore) whose institutional shape most closely matches NIST's. Pick one such institute for the primary design; where the design's portfolio adapter accommodates the other institutes as well, note that in the portfolio-adapter artefact.

Pin the deployment and the evaluator before you begin the artefact set.

## Requirements

Produce five artefacts in a single directory.

### 1. `frvt-shape-study.md`

A short structured report (three to five pages) documenting the shape study of the current FRVT/FRTE round. This artefact is the *reading log* the exercise's later artefacts cite. Sections:

- **Round identity.** The specific FRVT / FRTE track(s) read (one-to-one verification, one-to-many identification, morph-attack detection, or others), the current published round, and the date of the reading.
- **Aggregate-performance section.** How NIST discloses aggregate performance in the report — the specific metrics reported, the test-set-size disclosure, and the format the numbers are presented in.
- **Per-slice performance section.** How NIST discloses per-demographic-slice performance — the specific slices reported, the sample-size disclosure per slice, and the statistical treatment (confidence intervals, precision digits).
- **Cross-vendor comparison section.** How NIST presents vendor-level cross-comparison — the ranking presentation, the identifier used per vendor, the treatment of vendors with multiple submissions.
- **Longitudinal comparison section.** How NIST publishes trajectory — the time-series shape, the label of each vendor's successive submissions, the treatment of retired algorithms.
- **Methodology annex.** What NIST includes in the methodology annex — protocol, test-set characteristics (to the extent disclosable without compromising sequestration), computed-statistics definitions.

For each section, note *the shape*, not the specific numbers — the exercise's discipline is on the workflow pattern rather than on the biometric-specific content.

### 2. `sealed-evaluation-conops.md`

The sealed-evaluation concept-of-operations document for the next-generation AISI-shape engagement. Chapter `05`'s shape lesson `sealed evaluation` is the direct target. Sections:

- **Submission shape.** The sealed model or system snapshot the enterprise submits to the AISI-shape institute. Concrete — the packaging format (`mod-104` chapter `04` ML-BOM with SPDX/SLSA/Sigstore packaging), the hardware-independent packaging strategy, the model-digest pin as the primary identifier.
- **Institute-side execution environment.** The institute-controlled infrastructure on which the sealed submission runs — where the vendor's model is instantiated, where the institute's evaluation harness runs, where the raw outputs are captured, where the results are aggregated for publication.
- **Test-data sequestration.** How the institute's evaluation set is held sequestered from the vendor — the specific access controls, the segregation from any vendor-facing surface, and the retention regime after evaluation completion. Where the AISI-shape institute uses `Inspect`-based task suites (chapter `01`'s substrate), the sequestration applies to the task-specification content and to the elicitation prompts.
- **API specification.** The interface the sealed submission exposes to the institute's harness — the input format (prompt / tool-call schema / task specification), the output format (response / tool-invocation / task-result), and the metadata channel (self-reported operating parameters analogous to FRVT/FRTE's).
- **Contamination-impossibility argument.** The workflow-level argument that vendor-side contamination of the evaluation set is *structurally impossible* under this design — the vendor never sees the evaluation set; the vendor's model has been submitted at a pinned digest before the evaluation runs; any subsequent vendor-side observation is on aggregate results only. Cross-reference chapter `01`'s three payload-leakage failure modes to show how the sealed workflow addresses each.
- **Vendor's dispute channel.** Where the vendor's disagreement channel is bounded — on aggregate metric interpretation, not on individual test-item labelling or curation. This is a substantive change from the current AISI-shape interface's negotiation surface.

### 3. `versioned-identifier-and-longitudinal-design.md`

The design for versioned model identifiers and longitudinal comparison across engagement rounds. Chapter `05`'s shape lessons `versioned vendor identifiers` and `longitudinal comparison across evaluation rounds` are the direct targets. Sections:

- **Identifier scheme.** The identifier each sealed submission carries — the enterprise's model digest from `mod-104` chapter `04`, the model-registry identifier, and the submission-date metadata analogous to FRVT/FRTE's. How the identifier propagates through the institute's report so the report's citation is stable and machine-comparable.
- **Cross-submission comparison.** How the institute's report positions the current submission against the enterprise's prior submissions — the trajectory shape (improvement, regression, plateau), the metric-family stability across rounds, the treatment of retired model versions.
- **Cross-vendor comparison.** How the institute's report positions the enterprise's submission against peer submissions from other providers — the peer-set definition (all sovereign-institute submissions in the current round, all submissions in a task-suite-defined peer group), the ranking presentation, the treatment of the enterprise's identifier in the public output.
- **Assurance-case implication.** How the longitudinal series enters the assurance case (`mod-102` chapter `06`) — as a *trajectory* leaf rather than a *point-in-time* leaf. What the release-gate criterion reads from the trajectory (monotone improvement, no regression from prior round, no adverse cross-vendor position) versus what a point-in-time criterion would read.
- **Card-integration implication.** How the trajectory series enters the external card (`mod-105`) — the published aggregate results the card cites, the trajectory summary the card carries for the deployer audience, and the update cadence the card commits to.

### 4. `portfolio-adapter-design.md`

The design for the AISI-interface portfolio adapter. Chapter `05`'s shape lesson `portfolio across modalities` is the direct target. Sections:

- **Adapter scope.** The single adapter the release-assurance programme builds to accommodate multiple AISI-shape institutes and multiple AISI-shape evaluation tracks. The adapter is the `mod-104` chapter `02` evidence-pipeline adapter, extended to accept and emit the sealed-submission workflow described in `sealed-evaluation-conops.md`.
- **Institute-family matrix.** The current AISI-shape institutes the adapter accommodates — UK AI Security Institute, US AI Safety Institute, Singapore AI Verify Foundation, METR, Apollo Research, MLCommons AI Safety Working Group — with the per-institute metadata (institute identifier, evaluation-track catalogue, submission API version, report-return API version).
- **Track-family matrix.** The evaluation tracks the adapter accommodates — dangerous-capability evaluation, cyber-uplift evaluation, biological-uplift evaluation, deceptive-alignment evaluation, autonomy evaluation, and adjacent tracks the AISI-shape ecosystem is expected to publish. Cross-reference the analogous NIST portfolio (FRVT / FRTE, SRE, IREX, fingerprint-vendor-technology-evaluation lineage) as the maturity-target pattern.
- **Submission-shape invariance.** The invariant submission shape the adapter presents to the release-assurance programme — the same ML-BOM packaging, the same digest-pin, the same metadata channel, regardless of which institute or which track the submission is being sent to. Where the invariant cannot be maintained, note the deviation and its cost.
- **Return-artefact ingestion.** The invariant return-artefact ingestion the adapter presents — the report is ingested into the `mod-104` chapter `06` assurance bundle as an external-evaluator leaf with per-institute metadata and per-track metadata. The release-gate case reads the leaves through the invariant even where the institutes' report formats differ.
- **Development plan.** Where the adapter is not yet built (the shape lessons name a target end state, not the current state), the incremental development plan — which institute is prioritised first (typically the sovereign institute whose scheme the enterprise is under greatest supervisory pressure from), which tracks are prioritised first (typically the tracks with the greatest release-gate weight), and the milestone plan.

### 5. `two-disanalogy-defence-memo.md`

The memo that names where the FRVT/FRTE shape lessons stop generalising, so the enterprise's next-generation design does not over-generalise them. Chapter `05` names two disanalogies explicitly. Sections:

- **Disanalogy 1: deployment surface.** FRVT/FRTE evaluates narrow-task biometric algorithms with a well-defined input-output specification (a pair of images or a probe against a gallery). AISI-shape evaluations target general-purpose models and agentic systems whose deployment surface is vastly larger and harder to specify.
  - **Where the sealed-envelope workflow adapts.** The sealed submission of the model or system snapshot; the institute-side execution environment; the test-data sequestration.
  - **Where the API specification does not adapt without extension.** The FRVT/FRTE per-track API is narrow; the AISI equivalent has to be model-family-general (accepting many model families under a common invocation interface) and elicitation-methodology-open (accepting many task-suite formats, evolving over time). The `Inspect` framework's task-suite format is one such openness (chapter `01`); the ecosystem has not yet converged on a shared version.
  - **Design mitigation.** The `sealed-evaluation-conops.md` API specification names the shape and versioning strategy that accommodates the open elicitation methodology — the metadata channel, the task-specification schema evolution, and the compatibility guarantees the adapter carries across schema versions.
- **Disanalogy 2: evaluation ownership.** FRVT/FRTE is a single-programme, single-institute operation. AISI-shape evaluation is inherently multi-institute — a frontier release may be evaluated by multiple institutes in parallel, with different evaluation surfaces and different reporting cadences.
  - **Where the portfolio adapter adapts.** The single adapter accommodates multiple institutes and multiple tracks (per `portfolio-adapter-design.md`).
  - **Where cross-institute coordination has no direct FRVT/FRTE analogue.** How institutes coordinate on comparable results, on shared task suites, on cross-institute publication cadences — none of this has a direct precedent in FRVT/FRTE. The International Network of AI Safety Institutes ([commerce.gov/news/press-releases/2024/11/first-ever-international-network-ai-safety-institutes-set-launch-san](https://www.commerce.gov/news/press-releases/2024/11/first-ever-international-network-ai-safety-institutes-set-launch-san)) is the coordinating body, but the coordination protocols are still developing.
  - **Design mitigation.** The programme's portfolio-adapter design carries per-institute metadata explicitly, does not assume cross-institute result comparability at the numeric level, and treats each institute's report as an independent evidence leaf whose synthesis into the assurance case is programme-side rather than adapter-side.
- **Where the shape lessons still apply despite the disanalogies.** Sealed evaluation, versioned identifiers, longitudinal comparison, portfolio adapter design — each remains the right target. The disanalogies refine *how* the programme applies them, not *whether*.

## Starter guidance

- **Shape study, not technical study.** The exercise's reading of the FRVT/FRTE round is for workflow pattern, not for face-recognition-specific detail. If your `frvt-shape-study.md` reads as a face-recognition primer, re-focus on the reporting structure and workflow controls.
- **Design at target end state, not at current AISI state.** Chapter `05` is emphatic — the shape lessons are the target end state the AISI-shape ecosystem is likely to converge on as it matures. The exercise's design is what the enterprise should be prepared for, not what the current engagement will use verbatim. Where the current engagement's interface differs from the design (typically it will), that gap is what the release-assurance programme has to bridge over time.
- **The `Inspect` framework is a substrate, not a solution.** Chapter `01`'s note on `Inspect` as a shared substrate is worth returning to. The `Inspect` task-suite format is what makes the sealed-evaluation workflow's task-specification schema evolvable across the ecosystem; but it does not itself provide the sealed-evaluation workflow. The design adds the workflow around the substrate.
- **The two disanalogies are load-bearing.** Do not skip `two-disanalogy-defence-memo.md`. First-time programmes over-generalise the FRVT/FRTE lessons and design an interface that fails the deployment-surface breadth or the multi-institute coordination test. The defence memo is where the over-generalisation is caught.
- **The portfolio adapter is a `mod-104` chapter `02` extension.** The adapter lives alongside the existing evidence-pipeline adapters, not as a separate system. Its uniformity across institutes and tracks is what makes it operationally maintainable.
- **`<!-- needs-research: … -->` markers are legitimate.** The FRVT / FRTE URL structure, the AISI-shape institutes' current API surfaces, and the International Network of AI Safety Institutes' current coordination protocols are all subject to revision. Where you would need to verify a specific citation, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `frvt-shape-study.md` documents the shape study of a current FRVT/FRTE round with sections on aggregate performance, per-slice performance, cross-vendor comparison, longitudinal comparison, and methodology annex. The reading is on shape, not on face-recognition specifics.
- `sealed-evaluation-conops.md` covers the submission shape, institute-side execution environment, test-data sequestration, API specification, contamination-impossibility argument, and vendor's dispute channel. The contamination-impossibility argument explicitly addresses chapter `01`'s three payload-leakage failure modes.
- `versioned-identifier-and-longitudinal-design.md` covers the identifier scheme, cross-submission comparison, cross-vendor comparison, assurance-case implication (trajectory leaf), and card-integration implication.
- `portfolio-adapter-design.md` names the adapter scope, institute-family matrix, track-family matrix, submission-shape invariance, return-artefact ingestion, and incremental development plan. The adapter is a `mod-104` chapter `02` extension, not a separate system.
- `two-disanalogy-defence-memo.md` walks both disanalogies (deployment surface, evaluation ownership) with the specific adaptations and the specific limits, and closes with the shape lessons that still apply despite the disanalogies.
- The design is pinned at target end state — the current AISI-shape interface's gap to the design is noted, and the incremental bridging plan is present.
- The exercise's five shape lessons are covered exhaustively — sealed evaluation, published demographic breakdowns (or the AISI equivalent — capability-elicitation breakdowns on dangerous-capability axes), versioned vendor identifiers, longitudinal comparison, portfolio across modalities — each with a design section citing chapter `05`'s formulation.
- Every place a fact would need to be verified against the current FRVT/FRTE round's URL structure, a specific institute's current API surface, or the AI Safety Institutes' current coordination protocols is marked `<!-- needs-research: … -->`.

## Stretch goals

- **Compose the cross-vendor-comparison mock-up.** In `cross-vendor-mockup.md`, sketch what a mature AISI-shape institute's cross-vendor comparison publication would look like for the enterprise's tracked dangerous-capability axes — the ranking presentation, the metric-family, the trajectory representation. This is the publication the enterprise's `mod-105` external card will cite once the ecosystem reaches maturity.
- **Author the release-gate criterion for AISI-shape trajectory.** In `release-gate-trajectory-criterion.md`, express the trajectory leaf as a `mod-103` chapter `02`-format release-gate criterion — the input signals (current-round report, prior-round report, cross-vendor position), the disposition logic, and the artefact the criterion emits. Extend the substantial-modification test from exercise `02` where the trajectory shows regression.
- **Draft the multi-institute coordination memo.** In `multi-institute-coordination.md`, sketch the coordination protocol the enterprise proposes when the same release candidate is being handed to two sovereign institutes simultaneously — the shared reproducibility bundles, the differentiated NDAs, the coordinated publication cadence, and the release-gate's handling of parallel reports.
- **Author the `Inspect`-framework interoperability note.** In `inspect-interoperability-note.md`, describe how the enterprise's own `mod-104` chapter `01` evidence pipeline shares task suites with the AISI-shape institute's `Inspect` deployment — where the enterprise's internal task suite can be lifted into an AISI-shape submission with minimal transformation, and where the transformation cost is non-trivial.
- **Extend to non-AISI-shape independent evaluators.** In `non-aisi-independent-evaluator-extension.md`, note where the sealed-evaluation shape lessons apply to non-AISI-shape independent evaluators (academic labs, MLCommons submissions, some Big-Four attest engagements' technical-testing components) and where they do not. This foreshadows the next-generation composition of chapters `01`–`04` under the shape-mature pattern chapter `05` describes.
