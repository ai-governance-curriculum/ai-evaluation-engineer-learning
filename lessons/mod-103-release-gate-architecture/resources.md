# Resources for mod-103-release-gate-architecture

Primary sources first. Every URL below is to a primary organisation's own page, a published academic reference, or the standards body's specification of record — so you can pin your understanding to text that survives editorial rewrites.

## Quality-model and measurement standards (chapter `02`)

- [ISO/IEC 25059:2023 — Software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Quality model for AI systems](https://www.iso.org/standard/80655.html) — the standard behind the rubric structure. Read chapters covering functional adequacy, robustness, transparency, controllability, adaptability, appropriate use of data, and how 25059 relates to 25010.
- [ISO/IEC 25010:2023 — Software engineering — SQuaRE — Product quality model](https://www.iso.org/standard/78176.html) — the base model 25059 extends. Cite when a rubric row discharges an inherited (non-AI-specific) quality characteristic.
- [ISO/IEC 24029-2:2023 — Assessment of the robustness of neural networks — Part 2: Methodology for the use of formal methods](https://www.iso.org/standard/79804.html) — deeper robustness methodology behind the robustness dimension.
- [ISO/IEC TR 24028:2020 — Overview of trustworthiness in AI](https://www.iso.org/standard/77608.html) — background for the trustworthiness framing used across the rubric.
- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the AI RMF text. MEASURE is where the rubric's cross-mapping lands.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the per-sub-category operational reference. Use this to pin the exact MEASURE sub-category identifiers cited in the rubric.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI profile of the AI RMF. Read if the system-in-scope includes generative AI.
- [NIST AI 100-2 — Adversarial ML Taxonomy](https://doi.org/10.6028/NIST.AI.100-2e2023) — reference behind the MEASURE-2.7 (security / resilience) sub-category and behind the robustness / adversarial rubric rows.

## AI management system (chapter `03`)

- [ISO/IEC 42001:2023 — AI management system](https://www.iso.org/standard/81230.html) — the AIMS standard. Clauses 4–10 are the auditable requirements; clauses 8 (operation) and 9 (performance evaluation) are the ones the release-gate outputs stream into.
- [ISO/IEC 23894:2023 — AI risk-management guidance](https://www.iso.org/standard/77304.html) — the method behind clause 6.1 risk assessment and clause 8.2 risk-assessment-during-operation.
- [ISO/IEC 42005:2025 — AI system impact assessment](https://www.iso.org/standard/44545.html) — the method behind clause 6.1 and clause 8.4 impact assessment.
- [ISO/IEC 42006](https://www.iso.org/standard/44546.html) — accreditation requirements for bodies certifying AIMS. Background for the mod-109 auditor interface.
- ISO/IEC 5259 series — data quality for analytics and ML; consult the ISO catalogue for the current parts (supports the appropriate-use-of-data dimension).
- [ISO/IEC 8183:2023 — Data life-cycle framework for AI](https://www.iso.org/standard/83628.html) — complements the 5259 series.

## EU AI Act and instruments (chapters `01`, `02`, `05`)

- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — official text. Articles 9–15 are the primary release-gate hooks (risk management system, data governance, technical documentation, records, transparency, human oversight, accuracy / robustness / cybersecurity); Article 17 (QMS), Article 26 (deployer), Article 47 (declaration of conformity), Article 49 (registration), Article 55 (GPAI systemic-risk), Article 61 (post-market), Article 72 (post-market monitoring plan), Article 73 (serious-incident reporting) all feed rubric / runbook clauses.
- [European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the Commission body overseeing GPAI obligations.
- [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — operational reference for Article 55 discharge. Preview for mod-111.
- [European Commission — AI Act implementation resources](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — official implementation hub.

## Model-risk / sector-regulated shape (chapter `05`)

- [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the source of the second-line effective-challenge convention used in chapter `05`.
- [OCC 2011-12 — Sound practices for model risk management](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — the OCC-side companion to SR 11-7.
- [SR 23-4 — Interagency guidance on third-party relationships](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm) — relevant where a third-party model provider is in the release-gate scope.
- [FDA — Good Machine Learning Practice (GMLP) guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — sector-regulated overlay for medical-device software.
- [FDA — Predetermined Change Control Plans (PCCP) for AI-enabled device software](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions) — informs the adaptability dimension for regulated deployments.
- [DORA — Regulation (EU) 2022/2554](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) — operational-resilience overlay relevant for financial-services deployments.

## Frontier-lab deployment-tier frameworks (chapters `01`, `05`)

- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — informs T3+ tier design.
- [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/) — parallel framework for frontier-model deployment tiers.
- [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — third parallel framework. All three are the deep coverage of mod-108.
- [Frontier Model Forum](https://www.frontiermodelforum.org/) — industry consortium collating shared practices.

## Assurance-case notation and supporting standards (chapters `04`, `06`)

- [Goal Structuring Notation (GSN) Community Standard v3](https://scsc.uk/gsn) — the notation the SACM `Artifact.id` linkage referenced in chapters `04` and `06` maps to.
- [OMG Structured Assurance Case Metamodel (SACM)](https://www.omg.org/spec/SACM/) — the persistence substrate the SACM `Artifact` elements the chapters cite live in.
- [ISO/IEC/IEEE 15026-2:2022 — Assurance-case content](https://www.iso.org/standard/80625.html) — the notation-independent content baseline.

## Observability substrate (chapters `04`, `06`)

- [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the span schema the AI-eval peer's trace-instrumentation attestation cites.
- [OpenInference](https://github.com/Arize-ai/openinference) — vendor-neutral instrumentation library.
- [OpenTelemetry](https://opentelemetry.io/) — the parent project.

## Supply-chain and ML-BOM (chapter `04`)

- [SPDX](https://spdx.dev/) — SBOM standard family. The AI-BOM extension (SPDX 3.0 AI Profile) supports the MLSec peer's supply-chain attestations.
- [CycloneDX ML-BOM](https://cyclonedx.org/capabilities/mlbom/) — parallel supply-chain schema for AI / ML.
- [in-toto](https://in-toto.io/) — attestation framework the supply-chain digest chain often uses.
- [Sigstore](https://www.sigstore.dev/) — signing and verification toolchain used to satisfy the "signature verified" gate-side acceptance test.

## Incident registries and post-market surveillance (chapter `05`, mod-110 preview)

- [AI Incident Database (AIID)](https://incidentdatabase.ai/) — public incident registry.
- [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents) — OECD-hosted incident tracking.
- [MIT AI Risk Repository](https://airisk.mit.edu/) — risk-category taxonomy that supports harm-inventory coverage.

## AISI-shape independent evaluators (chapter `04`, mod-109 preview)

- [UK AI Safety Institute](https://www.aisi.gov.uk/) and its [Inspect](https://inspect.aisi.org.uk/) evaluation framework.
- [US AI Safety Institute (NIST AISI)](https://www.nist.gov/aisi) and the [AISI Consortium](https://www.nist.gov/aisi/artificial-intelligence-safety-institute-consortium-aisic).
- [Singapore IMDA AI Verify Foundation](https://aiverifyfoundation.sg/).
- [METR](https://metr.org/), [Apollo Research](https://www.apolloresearch.ai/), [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/).

## International values baseline (background)

- [OECD AI Principles (2019, updated 2024)](https://oecd.ai/en/ai-principles).
- [Council of Europe Framework Convention on AI (2024)](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence).
- [UNESCO Recommendation on the Ethics of AI (2021)](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics).

## Cards and transparency substrate (chapter `02`, mod-105 preview)

- Mitchell et al., *Model Cards for Model Reporting* — [arXiv:1810.03993](https://arxiv.org/abs/1810.03993).
- Gebru et al., *Datasheets for Datasets* — [arXiv:1803.09010](https://arxiv.org/abs/1803.09010).
- [Hugging Face Model Card Guidebook](https://huggingface.co/docs/hub/model-card-guidebook).
- [C2PA content provenance](https://c2pa.org/).

## Adjacent evaluation-methodology references (chapters `02`, `04`)

- [EleutherAI lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) — community evaluation harness whose outputs land as evidence in many release-cases.
- [MLPerf](https://mlcommons.org/en/inference-datacenter/) — MLCommons benchmark suite; informs the model-eval peer's methodological anchors.

## Suggested reading order for this module

1. Chapter `01` of this module, then a re-read of mod-101 chapter `01` (role) and mod-102 chapter `06` (evidence contract, producer side). One sitting.
2. Chapter `02` of this module, then a skim of ISO/IEC 25059 (via the ISO catalogue page) and the NIST AI RMF Playbook's MEASURE section. One sitting.
3. Chapter `03` of this module, then a re-read of ISO/IEC 42001 clauses 8 and 9 (via the ISO catalogue page). One sitting.
4. Chapter `04` of this module, then a re-read of mod-102 chapter `06` and a skim of OpenTelemetry Gen-AI semantic conventions and SPDX-AI. One sitting.
5. Chapter `05` of this module, then SR 11-7 and OCC 2011-12 for the second-line effective-challenge convention. One sitting.
6. Chapter `06` of this module, then the exercises.

You are not expected to memorise sub-category or article numbers. You are expected to know which framework and which article / clause / sub-category shape a given release-gate criterion and where to look up the specific identifier.
