# AISI TEVV and the NIST AI RMF Generative AI Profile as the Evaluator Envelope

## Motivation

Chapter `01` walked Article 55 as the statutory driver of the GPAI-systemic-risk assurance package. Chapter `02` walked the frontier-lab frameworks as the industry-shape template. This chapter walks the third leg: the *evaluator-facing envelope* — the reference paraphrase of the framework that a third-party evaluator (US or UK AI Safety Institute, notified-body-style evaluator, independent audit house) reads when they attach to the assurance case.

Two reference documents govern that envelope.

The first is the **NIST AI RMF Generative AI Profile**, [NIST AI 600-1](https://doi.org/10.6028/NIST.AI.600-1), published 2024-07. Where `mod-101` chapter `02` walked NIST AI RMF 1.0 as the outer envelope of every AI governance programme, AI 600-1 is the *GenAI paraphrase* of that framework — a per-risk elaboration of GenAI-specific concerns cross-referenced back into the four core functions (GOVERN, MAP, MEASURE, MANAGE).

The second is the **Testing, Evaluation, Verification, and Validation (TEVV)** framing that the AISIs (both the [UK AI Safety Institute](https://www.aisi.gov.uk/) and the [US AI Safety Institute](https://www.nist.gov/aisi)) publish and operationalise. TEVV is not a single document but a *shape*: the set of pre-deployment and iterative evaluation activities a third-party evaluator performs, together with the reporting outputs and the interface with the provider.

For a release-assurance methodology owner, the point of this chapter is: what does the assurance programme *hand over* so that an AISI-shape TEVV evaluation can attach to the assurance case *cleanly*, without duplicating the peer-owned methodology and without leaving gaps the evaluator would flag as unfinished?

## NIST AI 600-1 — the Generative AI Profile

### What the profile is

NIST AI 600-1 (the *Generative AI Profile*) is a companion to AI RMF 1.0 that identifies risks unique to or exacerbated by generative AI systems, and per risk lists suggested actions cross-referenced back to the four AI RMF functions. It does *not* replace the AI RMF; it profiles it. A release-assurance programme running for a GenAI system uses AI RMF 1.0 as the outer sub-category ontology and AI 600-1 as the GenAI-specific paraphrase.

### The twelve GenAI risk categories

AI 600-1 identifies a set of GenAI-specific risks. The categories, as published in the 2024-07 profile, are:

1. **CBRN Information or Capabilities** — chemical, biological, radiological, nuclear information or capabilities that could enable weapons development or use.
2. **Confabulation** — production of confidently stated but erroneous or false content ("hallucination").
3. **Dangerous, Violent, or Hateful Content** — content that promotes or incites violence, hatred, or dangerous acts.
4. **Data Privacy** — exposure of personal or sensitive information through training data memorisation, inference, or output.
5. **Environmental Impacts** — energy and resource consumption of training and inference.
6. **Harmful Bias or Homogenisation** — biased outputs, or homogenisation across outputs that reduces diversity of representation.
7. **Human-AI Configuration** — misconfiguration or mismatch between human oversight roles and system capabilities.
8. **Information Integrity** — degradation of the information environment through synthetic content, misinformation, or disinformation.
9. **Information Security** — vulnerabilities the model or its outputs introduce into information-security posture (including prompt injection, model exfiltration, and downstream attack surfaces).
10. **Intellectual Property** — training-data IP exposure and output-side IP infringement.
11. **Obscene, Degrading, and/or Abusive Content** — including CSAM and non-consensual intimate imagery.
12. **Value Chain and Component Integration** — risks introduced through integration of upstream foundation models, downstream systems, plug-ins, tools, and third-party data.

<!-- needs-research: verify the exact category count and naming against the current AI 600-1 text at https://doi.org/10.6028/NIST.AI.600-1; the profile has been reviewed and may have been updated since the 2024-07 publication. Confirm in particular whether the "CBRN Information or Capabilities" category retains its original wording. -->

### Per-risk suggested actions and cross-references

For each risk, AI 600-1 lists suggested actions and cross-references them into the four AI RMF functions using the standard `FUNCTION-CATEGORY.SUBCATEGORY` shape. A suggested action for the *Information Integrity* risk might cross-reference into MEASURE-2.7 (evaluations for security, resilience, and adversarial-ML posture), MANAGE-4.1 (post-deployment monitoring), and GOVERN-3.2 (workforce-diversity considerations for evaluator teams), among others.

**Release-assurance implication.** A GenAI release-assurance programme carries an AI 600-1 crosswalk in its assurance case: per risk category, which release-gate criteria address it, which sub-categories are cited, and which peer evidence discharges the criteria. This crosswalk is what a NIST-aligned reviewer walks first — before drilling into any specific criterion.

## The TEVV framing

### What TEVV is

TEVV — *Testing, Evaluation, Verification, and Validation* — is a systems-engineering framing that predates GenAI (its roots are in defence and safety-critical systems engineering) and has been picked up by the AISI community as the umbrella term for third-party AI-evaluator activity. Each of the four verbs has a specific meaning:

- **Testing** — running the system against inputs and observing outputs. In AI evaluation, this covers benchmarks, red-team probes, capability elicitations, and structured evaluation runs.
- **Evaluation** — judging test outputs against criteria. In AI evaluation, this covers scoring, threshold comparison, and the interpretation of test results into capability claims.
- **Verification** — confirming that the system meets its stated requirements. In AI evaluation, this covers checking that the model's actual behaviour matches its declared capability envelope and mitigation posture.
- **Validation** — confirming that the system meets the *intended* real-world need. In AI evaluation, this covers deployment-context evaluation, external-audit sign-off, and evidence that mitigations discharge the risks they were designed to address.

**Release-assurance implication.** The four verbs are the shape of what a third-party AISI-style evaluator does. The assurance programme's evaluator handoff has to name each of the four and identify the artefacts the evaluator will consume — the test inputs, the evaluation criteria, the verification-against-requirements record, and the validation-against-intent narrative.

### UK AISI — public evaluation guidance and Inspect

The [UK AI Safety Institute](https://www.aisi.gov.uk/) publishes evaluation methodology, capability-evaluation reports on specific frontier models (typically post-engagement with the provider), and — significantly — the [Inspect](https://inspect.aisi.org.uk/) evaluation framework, an open-source Python library for authoring and running AI evaluations with common patterns for multi-turn dialogues, tool use, sandboxed agent execution, and result aggregation.

**Release-assurance implication.** Inspect is *significant* for the assurance package because it is a shared substrate — evaluations expressed in Inspect are directly re-runnable by the UK AISI (and by any other party that has the Inspect runtime and the evaluation definition). The assurance programme's evaluator handoff can include Inspect-expressed evaluations as reproducibility bundles (`mod-104` chapter `03`); the reviewer runs the same evaluation and confirms the reported results independently.

### US AISI — evaluation profiles and voluntary agreements

The [US AI Safety Institute](https://www.nist.gov/aisi), hosted at NIST, publishes evaluation profiles, methodology guidance, and outputs from voluntary pre-deployment evaluation agreements with frontier developers. US AISI's outputs interconnect with the broader NIST AI standards portfolio (AI 600-1, AI 100-2 adversarial-ML taxonomy, AI 100-4 dual-use foundation models risk documentation, and ongoing work).

<!-- needs-research: verify the current set of US AISI published outputs and any updated voluntary-agreement structure at https://www.nist.gov/aisi; also confirm the status of the pre-deployment testing framework AISI has scoped. -->

**Release-assurance implication.** The US AISI's outputs are the reference for how a NIST-aligned assurance case reads under the US institutional envelope. A GPAI-systemic-risk provider offering the model into the EU *and* into the US typically produces one evidence set that satisfies both AI Office (EU) and US AISI (US) walkability requirements, with jurisdiction-specific narrative frames (see `mod-106`).

### Where TEVV and AI 600-1 meet

The two frames are complementary, not competing. AI 600-1 is *what* is evaluated — the risk categories and the sub-category cross-references. TEVV is *how* the evaluation is performed and reported — the test/evaluate/verify/validate cycle the evaluator runs. A well-formed AISI-shape engagement carries both: an evaluation report structured against AI 600-1's risk categories, with each report section carrying the four TEVV verbs' worth of artefacts (which tests were run, how the results were evaluated against criteria, how the results verify against the provider's stated requirements, how the results validate against the intended real-world need).

The release-assurance programme's evaluator handoff (below) is structured to make this pairing easy to walk — the handoff's table of contents can be indexed by AI 600-1 risk category or by TEVV verb, and both indices resolve to the same underlying artefact set.

### The convergence: what an AISI-shape TEVV engagement looks like

An AISI-shape TEVV engagement (whether formally UK AISI, US AISI, or a broadly similar third-party evaluator) typically carries:

- **Pre-engagement scoping.** The evaluator and the provider agree on capability categories in scope, evaluation methodology, access model (pre-deployment access, post-deployment access, structured-access API, tool-use environment), reporting format, and disclosure timelines.
- **Evaluator access to the model.** The provider grants access to a specific model checkpoint or a hosted API, under an evaluation agreement that governs attack-payload non-disclosure, IP protection, and result-reporting terms (`mod-109` chapter `01`).
- **Evaluator access to the assurance case.** The evaluator reads the assurance case, the evidence store (`mod-104`), the frontier-framework citation (chapter `02`), and any relevant Article 55 evidence (chapter `01`).
- **Independent evaluation.** The evaluator runs its own evaluations, using its own methodology and tools (Inspect for UK AISI; the US AISI methodology for US AISI). It may reproduce specific evaluations from the provider's assurance case.
- **Reporting.** The evaluator produces a report, which the provider may respond to, and which is (variably) publicly released or held under embargo.

## The evaluator-facing envelope from the assurance programme

The release-assurance programme prepares an *evaluator handoff* — a self-contained package the third-party evaluator receives, with clear pointers into the assurance case and the evidence store. The handoff typically contains:

- **The assurance case at engagement start.** The SACM `ArgumentPackage` (`mod-102`), with per-claim citations to evidence and to obligation sources (EU AI Act articles, ISO/IEC 42001 clauses, AI RMF sub-categories, AI 600-1 risk categories).
- **The AI 600-1 crosswalk.** Per GenAI-specific risk category, the release-gate criteria and evidence the programme cites.
- **The frontier-framework citation.** The framework the enterprise adopts (chapter `02`), with the specific version referenced and the tier / level the release candidate sits in.
- **The evaluator-facing evidence subset.** From the assurance bundle (`mod-104` chapter `06`), the subset the evaluator has access to under the evaluation agreement — typically the reproducibility bundles for capability evaluations, the red-team reports, the guardrail-evaluation reports, and the mitigation-effectiveness measurements.
- **The methodology declaration.** Which evaluation protocols the programme used (chapter `04`), which versions, and which configurations. State-of-the-art justification (chapter `01`) lands here.
- **The reproduction instructions.** For each reproducibility bundle, the environment specification, the pinned dependency set, and the run instructions.
- **The access artefacts.** API keys, model checkpoints, evaluation datasets, canary tokens (under the eval-set-security regime, `mod-104` chapter `05`), and any other resource the evaluator needs.
- **The evaluation agreement.** The signed agreement governing attack-payload non-disclosure, IP protection, and result disclosure (`mod-109` chapter `01`).

The handoff is *itself* content-addressed and signed — an evaluator six months later can walk from the report back to the exact handoff bundle they received.

## Handoff timing — pre-, at-, and post-deployment access

An AISI-shape TEVV engagement can attach to the assurance case at three timings, and the handoff shape differs at each:

- **Pre-deployment.** The evaluator engages with a specific release candidate before it is placed on the market. This is the strongest form of the engagement — the evaluator's findings can influence whether the release happens, at what tier, and with which mitigations. The handoff carries the assurance-case-at-freeze plus the evaluator-access artefacts for the candidate.
- **At-deployment.** The evaluator engages at release time, with post-release access to the same model checkpoint the deployed system is running. Findings inform the post-market plan (`mod-110`) and future releases rather than the current release.
- **Post-deployment.** The evaluator engages with a model already in production, typically to characterise capabilities that were not fully elicited pre-release. Findings drive re-evaluation of the tier, potential deployment-restriction changes, and updates to the systemic-risk assessment.

The three timings are not mutually exclusive; a well-run programme usually carries at least one of each across a release's lifetime.

## What the assurance programme does NOT hand over — methodology depth

The evaluator handoff carries *citations* into peer-owned methodology depth; it does not carry the depth itself.

- **Benchmark methodology depth** (how a specific benchmark is authored, how its scoring is designed, how its coverage claims are validated) is owned by the peer `model-evaluation-engineer` and `ai-risk-engineer`. The handoff cites the benchmark and its provenance; the evaluator reads the peer artefacts if they need methodology depth.
- **Red-team methodology depth** (how a red-team attack set is designed, how coverage is measured, how attacker-effort is calibrated) is owned by `ai-risk-engineer` and, for agentic capabilities, `agentic-safety-engineer` at level 40. The handoff cites the red-team report; the evaluator reads the peer artefacts if they need methodology depth.
- **Guardrail-evaluation methodology depth** is owned by `ai-risk-engineer` and `model-evaluation-engineer`. Same pattern.

This separation matters because the release-assurance methodology owner is *not* the methodology owner for these peer disciplines. Trying to be would duplicate ownership and undermine the peer specialists' authority. The programme's contribution is *plumbing* — the evidence flows cleanly, cites correctly, and reproduces on the evaluator's environment — not *methodology*.

## Worked example — evaluator handoff for a systemic-risk GPAI

Suppose the GPAI-systemic-risk provider from chapter `01`'s worked example is preparing a UK AISI TEVV engagement pre-deployment. Concretely, the evaluator handoff:

- Contains the SACM `ArgumentPackage` at engagement start, with per-claim citations into the evidence store.
- Contains the AI 600-1 crosswalk — per risk category (CBRN, confabulation, dangerous content, data privacy, environmental impact, harmful bias, human-AI configuration, information integrity, information security, IP, obscene/degrading content, value-chain), the release-gate criteria and evidence.
- Cites the enterprise's frontier-framework artefact (FSL-1..FSL-4 in chapter `02`'s hypothetical), with the release candidate sitting at FSL-3.
- Contains the Inspect-expressed capability evaluations for the FSL-3-relevant categories, as reproducibility bundles.
- Contains the red-team reports from the internal team, `agentic-safety-engineer`, and a prior third-party engagement, all signed and cited.
- Contains the guardrail-evaluation reports, with mitigation-effectiveness measurements per chapter `02`'s FSF-derived primitive.
- Contains the state-of-the-art justification citing MLCommons AILuminate, HarmBench, WMDP, AgentDojo (chapter `04`) and the Frontier Model Forum's issue-brief library.
- Contains the access artefacts — a UK AISI evaluator API key, a checkpoint reference, evaluation datasets under the DPA (`mod-105` chapter `06`).
- Contains the signed evaluation agreement.

The UK AISI runs its own evaluations, reproduces a chosen subset of the provider's evaluations under Inspect, and produces a report. The report becomes a new evidence node in the assurance bundle (`mod-104` chapter `06`), signed by UK AISI, and cited into the assurance case as a new evidence claim.

## Where this shows up in the rest of the track

- `mod-101` chapter `02` (NIST AI RMF and Playbook) — the outer framework AI 600-1 profiles for GenAI.
- `mod-104` (evaluation evidence pipeline) — the evidence-store shape, reproducibility-bundle shape, eval-set-security clauses, and signed assurance bundle that the evaluator handoff is derived from.
- `mod-109` (third-party evaluator interface) — the evaluation agreement, attack-payload non-disclosure, and evaluator-relationship management.
- Chapter `04` of this module — the benchmark suites the state-of-the-art justification cites.
- Chapter `01` of this module — the Article 55 obligations the evaluator's report contributes evidence toward.

## Summary

- NIST AI 600-1 (the *Generative AI Profile*, 2024-07) is the GenAI paraphrase of NIST AI RMF 1.0; it identifies GenAI-specific risk categories (CBRN, confabulation, dangerous content, data privacy, environmental impact, harmful bias, human-AI configuration, information integrity, information security, IP, obscene content, value chain) and per-risk suggested actions cross-referenced into GOVERN / MAP / MEASURE / MANAGE.
- TEVV (Testing, Evaluation, Verification, Validation) is the umbrella framing for third-party AI-evaluator activity; the four verbs map onto specific evaluator artefacts.
- The [UK AISI](https://www.aisi.gov.uk/) publishes evaluation methodology and the open-source [Inspect](https://inspect.aisi.org.uk/) framework as a shared evaluation substrate; the [US AISI](https://www.nist.gov/aisi) publishes evaluation profiles and voluntary-agreement outputs interconnected with the broader NIST portfolio.
- The release-assurance programme prepares an evaluator handoff — the assurance case, the AI 600-1 crosswalk, the frontier-framework citation, the evaluator-facing evidence subset, the reproducibility bundles, the access artefacts, and the signed evaluation agreement — content-addressed and signed as a self-contained package.
- The handoff carries *citations* into peer-owned methodology depth; the release-assurance methodology owner does not duplicate the depth owned by `model-evaluation-engineer`, `ai-risk-engineer`, or `agentic-safety-engineer`.
- Exercise 03 has you design the evaluator envelope for a specific systemic-risk GPAI, per AI 600-1 risk category, with the TEVV-shape artefacts the AISI-style evaluator will consume.
