# Resources for mod-104-evaluation-evidence-pipeline

Primary sources first. Every URL below points at the organisation that owns the artefact — the standards body, the tool's own project, the framework's own documentation — so your reading pins to text that survives editorial rewrites. Secondary and community references live at the bottom.

## Content-addressed storage and canonicalisation (chapter `01`)

- [RFC 6234 — US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF)](https://www.rfc-editor.org/rfc/rfc6234) — the SHA-2 family reference. The store's identifier grammar rests on it.
- [RFC 8785 — JSON Canonicalization Scheme (JCS)](https://www.rfc-editor.org/rfc/rfc8785) — the canonicalisation rule for JSON records.
- [RFC 8493 — The BagIt File Packaging Format](https://www.rfc-editor.org/rfc/rfc8493) — Library of Congress-authored fixity-and-transfer format; one of the reproducibility-bundle serialisation choices in chapter `03`.
- [OCI Image Format Specification](https://github.com/opencontainers/image-spec) — the container-image manifest shape; the `sha256:<hex>` digest grammar.
- [OCI Distribution Specification](https://github.com/opencontainers/distribution-spec) — the pull/push protocol behind bundles-as-OCI-artefacts.
- [OCI Artifacts guidance](https://github.com/opencontainers/image-spec/blob/main/artifacts-guidance.md) — how non-image artefacts (SBOMs, attestations, bundles) live in an OCI registry.
- [S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html), [GCS Bucket Lock](https://cloud.google.com/storage/docs/bucket-lock), and [Azure immutable-storage policies](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview) — the write-once retention primitives the store's object layer relies on.

## Peer-platform evidence schemas (chapter `02`)

- [OpenTelemetry Semantic Conventions — Generative AI](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the current OTel Gen-AI attribute set. The adapter's contract cites these.
- [OpenInference specification](https://github.com/Arize-ai/openinference/tree/main/spec) — vendor-neutral instrumentation for LLM, retrieval, tool, agent, chain, and evaluation spans.
- [Arize Phoenix documentation](https://arize.com/docs/phoenix) — Phoenix's `Dataset`, `Experiment`, and evaluation surfaces.
- [Langfuse documentation](https://langfuse.com/docs) — traces, generations, scores, and datasets. See `/docs/scores` for the atomic evidence unit.
- [W&B Weave documentation](https://weave-docs.wandb.ai/) — the `Evaluation` primitive, `Model` object, and `EvaluationResults`.
- [UK AI Safety Institute — Inspect](https://inspect.aisi.org.uk/) and the [Inspect repository](https://github.com/UKGovernmentBEIS/inspect_ai) — task decorator, solver/scorer, eval log.
- [EleutherAI `lm-evaluation-harness`](https://github.com/EleutherAI/lm-evaluation-harness) — task registry, `results.json`, `--log_samples`.
- [Vertex AI Gen AI Evaluation Service](https://cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview) — pointwise / pairwise autorater methodology; the `vertexai.evaluation` SDK.
- [Amazon Bedrock Model Evaluation](https://docs.aws.amazon.com/bedrock/latest/userguide/model-evaluation.html) — automatic and human evaluation jobs; S3 output shape.
- [Azure AI Foundry Evaluation](https://learn.microsoft.com/azure/ai-foundry/how-to/develop/evaluate-sdk) and the [`azure-ai-evaluation` SDK](https://learn.microsoft.com/python/api/overview/azure/ai-evaluation-readme) — built-in evaluators (relevance, groundedness, safety, protected-material, indirect-attack) and custom evaluator surface.

## Reproducibility bundle packaging (chapter `03`)

- [Research Object Crate (RO-Crate) specification](https://www.researchobject.org/ro-crate/) — the community reproducibility-packaging format.
- [Workflow RO-Crate profile](https://about.workflowhub.eu/Workflow-RO-Crate/) — RO-Crate profile for computational workflows.
- [Croissant metadata format for ML datasets](https://mlcommons.org/working-groups/data/croissant/) — MLCommons dataset-metadata standard; useful for the `references-vs-embed` policy when a dataset cannot travel.
- [ML Reproducibility Checklist (Pineau et al.)](https://www.cs.mcgill.ca/~jpineau/ReproducibilityChecklist.pdf) — background reading for what a reproducibility contract has to cover.
- [Papers with Code — Machine Learning Reproducibility Checklist v2](https://github.com/paperswithcode/releasing-research-code) — companion checklist for released code.

## AI supply-chain provenance (chapter `04`)

### CycloneDX ML-BOM

- [CycloneDX specification](https://cyclonedx.org/specification/overview/) and the [CycloneDX ML-BOM capability page](https://cyclonedx.org/capabilities/mlbom/) — schema, examples, and tooling.
- [CycloneDX ML-BOM authoring guidance](https://cyclonedx.org/guides/) — the practical guide for populating the `machine-learning-model` component and `modelCard` sub-object.
- [CycloneDX CLI](https://github.com/CycloneDX/cyclonedx-cli) and the [CycloneDX Python library](https://github.com/CycloneDX/cyclonedx-python-lib).

### SPDX 3.0 AI Profile

- [SPDX specification landing](https://spdx.dev/use/specifications/) — current SPDX 3.0 spec and the AI and Dataset profiles.
- [SPDX 3 GitHub organisation](https://github.com/spdx) — reference implementations and schema files.
- [ISO/IEC 5962:2021 — SPDX 2.2.1 as an ISO/IEC standard](https://www.iso.org/standard/81870.html) — the ISO reference SPDX inherits from.

### SLSA v1.0

- [SLSA specification, v1.0](https://slsa.dev/spec/v1.0/) — framework overview, requirements, and level definitions.
- [SLSA provenance format v1](https://slsa.dev/spec/v1.0/provenance) — the `buildDefinition` / `runDetails` payload.
- [in-toto Attestation Framework](https://github.com/in-toto/attestation) — envelope specification (`predicateType`, `subject`).
- [`slsa-github-generator`](https://github.com/slsa-framework/slsa-github-generator) — GitHub Actions builders that produce SLSA attestations.
- [`slsa-verifier`](https://github.com/slsa-framework/slsa-verifier) — the verifier a reader uses to check the pack.

### Sigstore

- [Sigstore project](https://www.sigstore.dev/) and the [Sigstore documentation](https://docs.sigstore.dev/).
- [Cosign](https://github.com/sigstore/cosign) — signing CLI.
- [Fulcio](https://github.com/sigstore/fulcio) — the OIDC-bound short-lived-cert CA.
- [Rekor](https://github.com/sigstore/rekor) — the append-only transparency log.
- [DSSE — Dead Simple Signing Envelope](https://github.com/secure-systems-lab/dsse) — the envelope format Sigstore signs over.
- [Sigstore Bundle Format](https://github.com/sigstore/protobuf-specs) — the single-file collection of signatures + inclusion proofs.

### Loader-side (safetensors, ModelScan, picklescan)

- [safetensors format](https://github.com/huggingface/safetensors) and the [safetensors specification](https://huggingface.co/docs/safetensors/en/index) — the no-code-execution checkpoint format.
- [ModelScan (Protect AI)](https://github.com/protectai/modelscan) — scanner for pickle, TensorFlow SavedModel, Keras H5, ONNX.
- [picklescan (Trail of Bits)](https://github.com/mmaitre314/picklescan) — pickle-opcode scanner.
- [Trail of Bits — "Never a dull moment: how pickled models can be weaponized"](https://blog.trailofbits.com/2021/03/15/never-a-dl-moment-how-pickled-models-can-be-weaponized-for-supply-chain-attacks/) — background on why safetensors exists.
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — LLM04 (Data and Model Poisoning), LLM05 (Improper Output Handling), LLM10 (Unbounded Consumption); relevant to the loader-side discipline.
- [OWASP AI Exchange](https://owaspai.org/) — practical guidance including supply-chain and model-file safety.

## Eval-set contamination and exfiltration (chapter `05`)

- [Carlini et al., *Extracting Training Data from Large Language Models* (2020)](https://arxiv.org/abs/2012.07805) — the foundational memorisation-and-extraction result. Background for canary methodology.
- [Carlini et al., *Quantifying Memorization Across Neural Language Models* (2022)](https://arxiv.org/abs/2202.07646) — extends the memorisation quantification framework.
- [Brown et al., *Language Models are Few-Shot Learners* (GPT-3 paper, 2020)](https://arxiv.org/abs/2005.14165) — Section 4 discusses training-set contamination and n-gram-overlap detection.
- [Sainz et al., *NLP Evaluation in Trouble: On the Need to Measure LLM Data Contamination for Each Benchmark* (2023)](https://arxiv.org/abs/2310.18018) — a survey of contamination in modern benchmarks.
- [Golchin & Surdeanu, *Time Travel in LLMs: Tracing Data Contamination in Large Language Models* (2023)](https://arxiv.org/abs/2308.08493) — practical contamination-detection technique.
- [Deng et al., *Investigating Data Contamination in Modern Benchmarks for Large Language Models* (2023)](https://arxiv.org/abs/2311.09783) — evidence across widely used benchmarks.
- [NIST AI 100-2 E2023 — Adversarial Machine Learning Taxonomy](https://doi.org/10.6028/NIST.AI.100-2e2023) — reference taxonomy for MLSec attack classes, including data-poisoning and evasion.
- [MITRE ATLAS](https://atlas.mitre.org/) — adversarial threat landscape for AI systems; framework for reasoning about exfiltration paths.
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — LLM06 (Sensitive Information Disclosure) and LLM04 (Data and Model Poisoning) touch exfiltration and contamination respectively.

## Signing the assurance bundle and ISO/IEC 42001 records (chapter `06`)

- [ISO/IEC 42001:2023 — AI management system](https://www.iso.org/standard/81230.html) — clauses 4–10 the bundle discharges into; Annex A controls.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Article 11 / Annex IV (technical documentation), Article 12 (record-keeping), Article 18 (retention), Article 47 (declaration of conformity), Article 61 (post-market monitoring), Article 72 (post-market plan), Article 73 (serious-incident reporting), Article 74 (market-surveillance access), and Article 55 (systemic-risk GPAI).
- [ISO/IEC 42005:2025 — AI system impact assessment](https://www.iso.org/standard/44545.html) — the impact-assessment record clause 8.2 references.
- [ISO/IEC 5259 series](https://www.iso.org/standard/81088.html) — data quality for analytics and ML.
- [ISO/IEC 25059:2023 — SQuaRE for AI](https://www.iso.org/standard/80655.html) — quality dimensions that many gate criteria discharge into.

## Adjacent methodology (background reading)

- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the framework the release-gate obligations plug into; especially MEASURE-2.7 (security / resilience), MEASURE-2.13 (effectiveness of measurement), MANAGE-4.1 (post-deployment monitoring).
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — per-sub-category suggested actions.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — AI RMF profile for generative AI.
- [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the effective-challenge / second-line shape chapter `06` references.
- [FDA Good Machine Learning Practice (GMLP) guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — record-keeping context for regulated-device deployments.
- [21 CFR Part 820 — Quality System Regulation](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfcfr/CFRSearch.cfm?CFRPart=820) — FDA device record-retention rules.

## Cards and provenance context (background reading; deep coverage in mod-105)

- Mitchell et al., *Model Cards for Model Reporting* — [arXiv:1810.03993](https://arxiv.org/abs/1810.03993).
- Gebru et al., *Datasheets for Datasets* — [arXiv:1803.09010](https://arxiv.org/abs/1803.09010).
- [Hugging Face Model Card Guidebook](https://huggingface.co/docs/hub/model-card-guidebook).
- [C2PA content provenance](https://c2pa.org/) — media-provenance signing (adjacent to the bundle-signing story).

## Suggested reading order for this module

1. Chapter `01`, then RFC 8785 (JCS) and the OCI image / distribution specs — one sitting.
2. Chapter `02`, then the OpenTelemetry Gen-AI semantic conventions and one peer-platform doc of your choice (Phoenix, Langfuse, or Inspect) — one sitting.
3. Chapter `03`, then RO-Crate or BagIt (whichever your program will use) plus the ML Reproducibility Checklist — one sitting.
4. Chapter `04`, then the CycloneDX ML-BOM overview, the SPDX 3.0 spec landing, the SLSA v1.0 spec, and the Sigstore docs — one sitting.
5. Chapter `05`, then Carlini's memorisation-extraction paper and NIST AI 100-2 — one sitting.
6. Chapter `06`, then EU AI Act Articles 11 / 12 / 18 / 47 / 74 and ISO/IEC 42001 clauses 7.5, 8.1–8.4, 9.1, 9.2, 9.3, 10.1, 10.2 — one sitting.

You are not expected to memorise every schema field or clause number. You are expected to know which family owns each attestation, which article shapes which retention or access obligation, and to be able to look up the specific identifier confidently.
