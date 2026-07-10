# AI Supply-Chain Provenance for the Assurance Bundle

## Motivation

The reproducibility bundle (chapter `03`) proves that a re-runner *can* re-execute the eval. Supply-chain provenance proves what was actually inside the run. Which model weights loaded — and where they came from. Which training and eval datasets built the model — and how they got there. Which container image ran the evaluator — and what was baked into it. Which build system produced that image — and did the build honestly correspond to source. Every one of these is a link in the chain the assurance case (mod-102) argues from, and every one is a link an adversary — or an accident — can break silently.

Two release-assurance failure modes drive the shape of this chapter.

The first is **provenance-by-affidavit**: the eval report contains a paragraph about which model was used, which datasets it was trained on, and which build system produced the artefact. There is no cryptographic linkage; the paragraph is a claim about the past that the reader either believes or doesn't. Under EU AI Act Article 11 / Annex IV (technical documentation) a paragraph is not evidence. Under Article 15 (accuracy, robustness, cybersecurity) and Article 61 (post-market monitoring) the same paragraph will not answer the market-surveillance authority when the authority asks "prove it."

The second is **checkpoint-as-code-execution**: a checkpoint file is loaded with a permissive deserialiser that executes attacker-controlled code during load, and the "checkpoint" was actually a malicious payload that quietly modified the container's runtime before the eval ran. The eval numbers look normal because the model was still the model; the pipeline's sandbox was silently exfiltrating tokens or eval-set contents (chapter `05`). This is a documented class of vulnerability — pickle-based deserialisation is not a hypothetical, it is a live threat against ML pipelines that continue to load `.bin` / `.pt` / `.pkl` files without vetting them.

The provenance layer this chapter draws is the assurance program's answer to both. It sits *around* the bundle: the bundle contains the artefacts, and the provenance attestations bind those artefacts to a signed chain of origin.

## The four attestation families

Four families of attestation cover the AI supply-chain in current 2026 practice, and the assurance bundle carries one of each — plus the safe-loading discipline for the model weights themselves.

1. **CycloneDX ML-BOM** — an ML-specific bill of materials, published by OWASP CycloneDX, that describes model components, training datasets, considerations (ethical, fairness, safety, environmental), and inputs/outputs. It answers "what is inside this model, and what did it come from?"
2. **SPDX 3.0 AI Profile** — a Software Package Data Exchange 3.0 document with the AI Profile (and the Dataset Profile as a companion), providing an ISO/IEC standard-aligned SBOM shape for AI systems. It answers the same question SPDX has always answered — "what are the components, licenses, and relationships in this artefact" — extended for AI.
3. **SLSA v1.0 build provenance** — Supply-chain Levels for Software Artifacts, an OpenSSF-hosted framework whose `slsa-provenance` attestation records how an artefact was built: builder identity, source repository, build-configuration digest, materials, and the invocation. It answers "did the artefact come from an honest build of the source it claims?"
4. **Sigstore keyless signatures** — public-good signing infrastructure with a transparency log (Rekor) and OIDC-derived short-lived certificates (Fulcio). Sigstore is not itself a *content* attestation; it is the *notarisation* layer that binds the other three to a signed, timestamped, transparency-log-visible event.

And one loader-side discipline:

5. **safetensors + ModelScan / picklescan** — the loader side. `safetensors` (a Hugging Face-authored format) eliminates the code-execution surface of pickle-based checkpoints. `ModelScan` (Protect AI) and `picklescan` (Trail of Bits) scan checkpoints for known-malicious deserialisation patterns before load. This is not an *attestation*; it is a *precondition* the loader enforces before ingest is allowed.

Together, the five give the release-assurance program a story it can tell in one paragraph: "Every artefact in this bundle has an SBOM (SPDX-AI), an ML-BOM (CycloneDX), a build-provenance attestation (SLSA v1.0), and a keyless signature with a transparency-log entry (Sigstore). Model weights are stored in the safetensors format and scanned with ModelScan / picklescan before load. The bundle's own signature ties the whole to the release cycle's key."

## CycloneDX ML-BOM in detail

CycloneDX (OWASP-hosted, ECMA-standardised) has extended its BOM schema with an **ML-BOM** profile that models ML-specific components. The relevant top-level element is a `component` with `type: "machine-learning-model"`, carrying an `modelCard` sub-object.

What the ML-BOM captures for the assurance bundle:

- **Model identity** — name, version, description, source (Hugging Face repo, internal registry, vendor snapshot ID).
- **Model card fields** — quantitative-analysis results, considerations (ethical, fairness, safety, environmental), model parameters (architecture, task, distribution details), training-set summary, evaluation-set summary. These fields are *machine-readable versions* of the same content the model card (mod-105) makes human-readable.
- **Training and evaluation data references** — CycloneDX ML-BOM lets a component reference `datasets` with their own components; each dataset has an identity, a governance record, a description, and a graphic description of ownership, sensitivity, and licensing.
- **Dependencies** — the model's dependency graph: parent checkpoints (for fine-tunes), adapter weights (LoRA, QLoRA), embedding models, tokenisers, judge models.

The bundle carries the ML-BOM as `data/provenance/cyclonedx-mlbom.json` (or `.xml`). The file is content-addressed; its digest lands in the manifest under `provenance.cyclonedx_ml_bom.digest`.

<!-- needs-research: the CycloneDX ML-BOM schema has evolved across CycloneDX 1.5 and 1.6; specific field names (e.g., `modelCard.modelParameters` vs `modelCard.model_parameters` — the schema is JSON-schema case-sensitive) shift; before pinning a program capture spec, verify the current published version at cyclonedx.org/capabilities/mlbom/. -->

## SPDX 3.0 AI Profile in detail

SPDX 3.0 (the SPDX Working Group's major-version bump, ISO/IEC 5962 as an earlier baseline) introduces *profiles* — modular extensions that specialise the base SBOM schema for specific ecosystems. The **AI Profile** covers AI packages; the **Dataset Profile** covers datasets. Both are typically used together for an AI-system SBOM.

What the SPDX-AI document captures:

- **AI package descriptors** — the model as an SPDX Package, with `packageType: "AI"` and AI-Profile-specific fields covering the model's usage instructions, safety-risk assessment, standards compliance, evaluation, type of model, etc.
- **Dataset descriptors** — training and evaluation datasets as SPDX Packages of type `dataset`, with Dataset-Profile fields for licensing, anonymisation, data-collection process, known biases, sensitive-personal-information handling.
- **Relationships** — SPDX 3.0's rich relationship model expresses "this model was trained on this dataset," "this evaluator uses this judge model," and other AI-native links. The relationships are queryable by an auditor.
- **License and copyright** — the classic SPDX license-expression covers third-party dependencies and licensed datasets; ambiguity is captured as `NOASSERTION` (present but unstated) or `NONE` (explicitly absent), rather than omitted.

<!-- needs-research: SPDX 3.0.1 vs 3.0 field-name specifics are in flux and the AI Profile has an SPDX Working Group-maintained JSON-schema; when pinning a program capture spec, check the current published schema at spdx.dev/use/specifications/. -->

The bundle carries the SPDX-AI file as `data/provenance/spdx-ai.spdx.json`.

The pair of ML-BOM (CycloneDX) and SPDX-AI is *not redundant*. Programs commonly use both because:

- Downstream consumers differ. Enterprises and government procurement often specify SPDX by name in contracts (SPDX is ISO/IEC-referenced). Security-tooling vendors are commonly wired against CycloneDX (OWASP-hosted, adopted by SAST/DAST scanners).
- Coverage is not perfect in either. CycloneDX ML-BOM has richer model-card fields; SPDX 3.0 has richer relationships and a stricter license-expression grammar. Programs that carry both do not have to answer which one the reader expects.

For a program that has to pick one, pick SPDX 3.0 as primary if the deployment sector is regulated (SR 11-7 second-line reviewers, notified bodies under EU AI Act Article 43, FDA GMLP submissions all know SPDX); pick CycloneDX ML-BOM as primary if the pipeline is already OWASP-tooling-heavy and the risk conversation is dominated by application security.

## SLSA v1.0 build provenance in detail

SLSA (Supply-chain Levels for Software Artifacts, OpenSSF-hosted, current v1.0) defines a framework for attesting how an artefact was built. The core artefact is a **provenance attestation** — an in-toto attestation whose `predicateType` is `https://slsa.dev/provenance/v1` and whose payload names:

- **`subject`** — the artefact(s) being attested (name + digest).
- **`buildDefinition`** — the "recipe": the build type (e.g., a specific CI/CD system's schema URL), the external parameters that triggered the build (source ref, commit, PR number), the internal parameters the build system chose, and any resolved dependencies pinned into the build.
- **`runDetails`** — who ran the build (`builder.id`), the build metadata (invocation ID, start/finish times), and byproducts.

SLSA has four levels (Build L1 → L4) that reflect increasing rigor about how the provenance is generated and how tamper-evident the build environment is. For assurance-bundle purposes, aim for **Build L2 at minimum** (provenance signed by the builder, tamper-evident) and **Build L3 where possible** (hardened build platform, hermetic-ish builds). Build L4 is aspirational for many pipelines but is where high-stakes bundles are heading.

What SLSA provenance means for the AI supply-chain: the pipeline needs *three or four* SLSA attestations for a typical bundle:

- **The model checkpoint's SLSA attestation** — the checkpoint's build provenance, tying it to the training pipeline, the training dataset commits, the training-code commit, and the reproducibility context (accelerator generation, framework version, seed). Many organisations run this attestation over the *training run* itself; the training-run identifier lands in the attestation subject.
- **The evaluator container image's SLSA attestation** — the container image the eval ran in, tied to its source repository and build system.
- **The bundle-assembly's SLSA attestation** — the reproducibility bundle *itself* is a build output; the pipeline that stitched together the bundle emits its own SLSA attestation over the bundle bytes.
- **(Optionally) The judge-model checkpoint's SLSA attestation** — if the judge is an open-weights model built by the same organisation, the same attestation shape applies.

Each attestation lives as an in-toto envelope (`.intoto.jsonl`) in `data/provenance/`. Each is signed (Sigstore, or a program's own key infrastructure), and the signature is verifiable independently of the bundle.

## Sigstore signatures in detail

Sigstore is the notarisation layer. Its components:

- **Cosign** — the CLI (and libraries) that produces and verifies signatures.
- **Fulcio** — a CA that issues short-lived (10-minute) X.509 certificates bound to an OIDC identity (a GitHub Actions workflow identity, a GitLab CI identity, a workload-identity token, a hardware-token identity, etc.). Fulcio-issued certs are *keyless* in the sense that no long-lived private key is stored by the signer; the private key is generated per-signature and destroyed.
- **Rekor** — the immutable, append-only transparency log where every signature's inclusion proof is recorded. Rekor is public (the Sigstore-run instance) or private (a Rekor deployment the program runs).
- **DSSE envelope** — the Dead Simple Signing Envelope (`https://github.com/secure-systems-lab/dsse`) is the envelope format Sigstore signs *over*. DSSE separates the signed payload from the signature, prevents canonicalisation ambiguity, and is the standard envelope for in-toto attestations.

What Sigstore does for the bundle:

- **Signs every provenance attestation.** Each `.intoto.jsonl` is DSSE-wrapped and signed with a Fulcio cert; the cert's OIDC identity records *who signed*. Rekor records *when*.
- **Signs the bundle manifest itself.** The bundle's `bundle_id` (chapter `03`) is signed with the release-assurance program's own key; the signature and the Rekor inclusion proof land in `data/provenance/sigstore-bundle.json`.
- **Signs the model checkpoint.** For open-weights models the pipeline builds itself, cosign signs the safetensors file (or its shard manifest); for vendor-hosted models the provider's own signature or attestation is what the pipeline records.

Sigstore signatures at the assurance-store side plug into chapter `01`'s transparency-log discussion — Rekor is the log the store's log-structured secondary shape references.

## safetensors — the loader-side default

**`safetensors`** is a checkpoint file format authored by Hugging Face that stores tensors as bytes with a JSON header and *no executable-code paths*. Loading a safetensors file involves mapping the bytes into memory as tensors; there is no `pickle.loads`, no `__reduce__`, no attacker-controlled deserialisation. If the file is malformed, the loader errors; it does not execute.

The assurance-store's write-policy for model artefacts:

- **Accept only safetensors for weights.** Pipelines that historically loaded `.bin`, `.pt`, `.pkl`, or `.ckpt` (all pickle-based, or that use torch's `pickle_module` under the hood) migrate to safetensors before they can ingest into the assurance store. Where migration is not possible (a legacy model must be preserved), the loader wraps the read in a mandatory `ModelScan` / `picklescan` pass and refuses to load if the scanner flags any known pattern.
- **safetensors + explicit device.** The loader specifies the device and dtype at load time rather than trusting the file's metadata to set them.
- **Shard manifests are content-addressed too.** For sharded checkpoints (multi-file), the manifest that lists shards and their per-shard digests is itself in the store; the model's canonical digest is the manifest's digest, not any single shard's.

## ModelScan and picklescan — the pre-load scan

`ModelScan` (Protect AI) and `picklescan` (Trail of Bits) are static-analysis tools that scan model files for known-malicious deserialisation patterns:

- **`picklescan`** parses pickle streams and flags opcodes that indicate arbitrary code execution paths (imports of `os`, `subprocess`, `builtins.eval`, `builtins.exec`, `posix.system`, etc.). It operates on the pickle bytecode directly and does not execute the pickle.
- **`ModelScan`** covers a broader surface — pickle-based formats (`.pkl`, `.pt`, `.bin`, `.dill`, `.joblib`), TensorFlow SavedModel format, Keras H5, ONNX — and flags patterns known to enable code execution or resource abuse during load.

Assurance-pipeline discipline:

- Every model artefact ingested into the store is scanned by *both* tools; a positive from either is a hard reject.
- Scan reports land as their own store artefacts, digested and referenced by the model's `provenance` metadata.
- Scans are re-run on model rotation and on any new-scanner-version release; the *scanner version* is pinned into the report.

## The provenance sub-tree of the bundle

Combining all of the above, a bundle's `data/provenance/` directory typically looks like:

```
data/provenance/
├── cyclonedx-mlbom.json                     # ML-BOM for the model
├── spdx-ai.spdx.json                        # SPDX-AI SBOM
├── slsa-provenance-model.intoto.jsonl       # SLSA over the model checkpoint
├── slsa-provenance-evaluator.intoto.jsonl   # SLSA over the evaluator container
├── slsa-provenance-bundle.intoto.jsonl      # SLSA over the bundle itself
├── sigstore-bundle.json                     # Sigstore bundle format tying signatures + Rekor proofs
├── modelscan-report.json                    # ModelScan output on the model file
├── picklescan-report.json                   # picklescan output on the model file
└── vendor-attestations/                     # (optional) provider-issued attestations for hosted models
    └── <vendor>-<snapshot>.attest.json
```

The bundle manifest (chapter `03`) references each of these by role and digest. Every one is independently verifiable — an auditor with the bundle and the four public roots (Fulcio, Rekor, the SLSA framework schema, the SPDX / CycloneDX schemas) can walk the whole chain without having to trust the provider.

## Vendor-hosted models

Not every model is one the pipeline builds. Hosted models — OpenAI, Anthropic, Google, Cohere, Mistral through hosted endpoints — do not expose the weights or the training pipeline. What the pipeline can still record:

- **The provider's snapshot identifier** — e.g., `gpt-*-2026-04-18`, `claude-*-20260426`, or the equivalent identifier the provider emits in the response.
- **The provider's own attestations, where they exist** — some providers publish signed model cards, transparency reports, or standardised model attestations; the pipeline captures whatever the provider commits to.
- **The pipeline-side envelope** — the request payload, the response payload, the response headers, and the provider snapshot identifier are recorded and signed by the pipeline. The bundle then carries a `vendor-attestation` file per hosted invocation that says: "this pipeline invoked provider X, received response Y from snapshot Z, and here is the DSSE-signed envelope over the exchange." The re-runner can compare their re-run's envelope against this one.

Vendor-hosted models are the case where determinism guarantees (chapter `03` section 3) are weakest. The provenance layer does what it can: it records what happened, signs it, and puts the fact of the vendor's opacity on the record so the assurance case is not silent about it.

## Interaction with the reproducibility bundle

The provenance attestations *live inside* the reproducibility bundle (`data/provenance/`), but their function is orthogonal: the reproducibility bundle proves the eval is *rerunnable*; the provenance attestations prove the eval is *rooted in an honest supply-chain*. A bundle without provenance is a bundle where the re-runner has to trust the producer's word about what the model came from; a provenance file without a reproducibility bundle is a supply-chain claim about an artefact nobody can independently exercise.

The two together give the release-gate its defensibility: the walker (mod-103 chapter `06`) checks that both are present, both verify, and both point at the same underlying artefacts. Divergence between the ML-BOM's model version and the reproducibility bundle's model digest is a walker fail.

## Interaction with the release-gate

The release-gate consumes provenance attestations as their own criteria under the ISO/IEC 25059 "appropriate use of data" dimension and under NIST AI RMF MEASURE-2.7 (security and resilience) and MANAGE-4.1 (post-deployment monitoring). Typical criteria that show up in the mod-103 gate:

- `GATE-SUPPLY-01` (hard): "Every artefact in the bundle has a verifiable ML-BOM (CycloneDX or SPDX-AI); missing → block; stale → block; warrant-failing → block."
- `GATE-SUPPLY-02` (hard): "Every artefact in the bundle has a SLSA v1.0 provenance attestation at Build L2 or higher; the attestation's subject digest matches the artefact's own digest."
- `GATE-SUPPLY-03` (hard): "Every provenance attestation is Sigstore-signed with a valid Fulcio-issued certificate, with a valid Rekor inclusion proof."
- `GATE-SUPPLY-04` (hard): "Every model artefact is safetensors-formatted (or a hard-tested exception is in place); every model artefact has a clean ModelScan and picklescan report; a positive from either scanner blocks."
- `GATE-SUPPLY-05` (soft, tier-dependent): "Vendor-hosted models carry a captured vendor-attestation envelope; providers whose responses cannot be pinned by snapshot are flagged for tier-dependent disposition."

These criteria are usually contested for routing — they mix the release-assurance program's ownership with the peer `ai-infra-security` track's expertise. Chapter `05` picks up the routing.

## Summary

- Every reproducibility bundle carries provenance attestations for the artefacts inside it — CycloneDX ML-BOM, SPDX 3.0 AI-Profile SBOM, SLSA v1.0 build provenance, and Sigstore signatures — plus loader-side discipline (safetensors, ModelScan / picklescan).
- ML-BOM (CycloneDX) and SPDX-AI cover *what is inside* the model. Programs commonly carry both because downstream consumers differ; SPDX-AI is the ISO-standard-aligned shape for regulated sectors.
- SLSA v1.0 attests *how the artefact was built* — the model checkpoint, the evaluator container, and the bundle itself all get their own SLSA envelopes. Aim for Build L2+.
- Sigstore is the notarisation layer: Fulcio issues short-lived keyless certs bound to OIDC identities, Rekor records inclusion proofs, DSSE wraps in-toto attestations. The bundle's own signature and every attestation's signature go through Sigstore.
- safetensors eliminates code-execution paths at load; ModelScan and picklescan catch known-malicious deserialisation patterns before ingest. A positive from either is a hard reject.
- Vendor-hosted models are captured via pipeline-side envelopes (request/response/snapshot ID, DSSE-signed). Providers whose responses cannot be pinned by snapshot are flagged.
- Provenance sits *inside* the reproducibility bundle at `data/provenance/`; the release-gate walker cross-checks provenance digests against reproducibility-bundle digests.
- Chapter `05` picks up the *threats* the provenance layer defends against: eval-set exfiltration, eval-set contamination, and the boundary with the `ai-infra-security` peer track that owns the deep MLSec view of the same problems.
