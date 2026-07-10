# mod-104-evaluation-evidence-pipeline: Evaluation Evidence Pipeline: Immutable Logs, Lineage, and Reproducibility Bundles

Builds the **immutable, content-addressed evidence substrate** the release-gate reads. Designs the store's lineage schema across model version / dataset hash / prompt / evaluator / judge / decoding-config / seed; specifies the normalisation layer that consumes evidence emitted by peer platforms (Arize Phoenix, Langfuse, W&B Weave, OpenTelemetry Gen-AI, OpenInference, Inspect, `lm-evaluation-harness`, Vertex AI Gen AI Evaluation, Amazon Bedrock Model Evaluation, Azure AI Foundry Evaluation); packages a reproducibility bundle a third-party evaluator can rerun end-to-end; attaches AI supply-chain provenance (CycloneDX ML-BOM, SPDX 3.0 AI Profile, SLSA v1.0, Sigstore, safetensors, ModelScan / picklescan); contracts eval-set exfiltration and contamination controls with the `ai-infra-security` peer; and signs the release-gate output artefact that persists into ISO/IEC 42001 records.

**Estimated effort:** 15 hours

## Learning objectives

- Design an immutable evaluation-log store with content-addressed lineage across model version / dataset hash / prompt / evaluator / judge / decoding-config / seed.
- Consume evidence emitted by peer platforms — Arize Phoenix, Langfuse, W&B Weave, OpenTelemetry Gen-AI, OpenInference, Inspect, `lm-evaluation-harness`, Vertex AI Gen AI Evaluation, Amazon Bedrock Model Evaluation, Azure AI Foundry Evaluation — and normalise it into the assurance store.
- Produce a reproducibility bundle (dataset + task-definition + evaluator + judge + prompt + decoding-config + seed + result hashes) that a third-party evaluator can rerun end-to-end.
- Attach AI supply-chain provenance to the assurance bundle: CycloneDX ML-BOM, SPDX 3.0 AI Profile, SLSA v1.0 build attestations, Sigstore signatures, safetensors safe-loading, and ModelScan / picklescan checkpoint scanning.
- Reason about eval-set exfiltration and eval-set-contamination risks with `ai-infra-security` (peer, level 35) and thread supply-chain-security clauses into the assurance bundle.
- Sign the assurance bundle and produce the release-gate output artefact that persists into ISO/IEC 42001 records.

## Lecture chapters

1. [`01-content-addressed-evidence-store.md`](01-content-addressed-evidence-store.md) — The immutability contract, the seven lineage dimensions, the Merkle-DAG on-disk shape, retention under EU AI Act Article 18, producer identity, and where the store *stops*.
2. [`02-peer-platform-evidence-normalisation.md`](02-peer-platform-evidence-normalisation.md) — The capture spec / adapter / conformance-test contract for each supported peer platform (OTel Gen-AI, OpenInference, Phoenix, Langfuse, Weave, Inspect, `lm-eval`, Vertex, Bedrock, Foundry); reject-rather-than-drift discipline.
3. [`03-reproducibility-bundle-format.md`](03-reproducibility-bundle-format.md) — The bundle a third-party evaluator can rerun end-to-end: manifest, dataset (or licensed reference), task / evaluator / scorer, prompt template and render, judge, decoding config, seeds, result digests, reproduction contract, container-pinned runtimes, cassette-replay for retired vendor snapshots.
4. [`04-supply-chain-provenance.md`](04-supply-chain-provenance.md) — The four attestation families (CycloneDX ML-BOM, SPDX 3.0 AI Profile, SLSA v1.0 build provenance, Sigstore signatures) plus loader-side discipline (safetensors, ModelScan, picklescan); vendor-hosted-model provenance; interaction with the release-gate.
5. [`05-eval-set-exfiltration-and-contamination.md`](05-eval-set-exfiltration-and-contamination.md) — The MLSec threat model; three contracted MLSec artefact classes (contamination attestation, exfiltration-control attestation, supply-chain-security clauses); public-benchmark contamination; canary tokens; where the release-assurance program *stops* and the `ai-infra-security` peer owns depth.
6. [`06-signed-assurance-bundle-and-42001-records.md`](06-signed-assurance-bundle-and-42001-records.md) — The release-gate output artefact: top-level manifest, five signing layers (producer / reproducibility-bundle / assurance-bundle / second-line / Rekor), mechanical verification, and the ISO/IEC 42001 clause map (7.5, 8.1–8.4, 9.1, 9.2, 9.3, 10.1, 10.2). EU AI Act Article 74 access.

## Structure

- `01-…md` … `06-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapter `01`** — read once, then draft the store's canonicalisation rule and lineage schema before opening exercise `01`. The store's shape drives every later chapter.
- **Chapter `02`** — read after `01`. The adapter contract only makes sense once the store's schema is fixed. Exercise `02` walks a real peer-platform fixture through the adapter and asserts byte-exact conformance.
- **Chapter `03`** — read after `02`. The reproducibility bundle is a *packaging* of what the store already contains; exercise `03` produces the format spec and a working reproducer script.
- **Chapter `04`** — read alongside `03`. Provenance attestations *live inside* the reproducibility bundle; exercise `04` attaches the four attestation families to the bundle produced in exercise `03`.
- **Chapter `05`** — read after `04`. The MLSec threat model reframes what the provenance layer is defending against; exercise `05` is done in coordination with a peer playing the `ai-infra-security` role (or in a table-top with the peer's methodology documents as fixtures).
- **Chapter `06`** — read after all five. The signed release-gate output artefact ties together everything the module has built. There is no dedicated exercise for `06`; the four preceding exercises produce the artefacts the signed bundle consumes.

## Dependencies

- Requires mod-101 (release-assurance position, framework overview, deferral contract), mod-102 (assurance-case engineering — especially chapter `04` SACM persistence and chapter `06` evidence contracts), and mod-103 (release-gate architecture — especially chapter `04` peer contracts and chapter `06` dashboard).
- Consumed by mod-105 (cards — the machine-readable side of every card is a view over this substrate), mod-107 (sector-regulated overlays that require model-risk records — SR 11-7, FDA GMLP — read from this substrate), mod-109 (third-party evaluator interface — bundle handoff), mod-110 (post-market surveillance — signals compared against bundle-frozen baselines), mod-111 (GPAI systemic-risk — extends the bundle with Article 55 evidence), and mod-112 (program ownership — aggregate reporting over bundles feeds ISO/IEC 42001 clause 9.3 management review). All three capstone projects consume this module.
