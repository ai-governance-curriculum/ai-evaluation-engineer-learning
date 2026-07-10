# exercise-03: Reproducibility Bundle Format

**Estimated effort:** 3 hours

## Objective

Design a **reproducibility bundle format** — the packaged, self-describing artefact a third-party evaluator can rerun end-to-end — and ship one working bundle for a small, honest eval you have run yourself. Then verify the bundle by running the reproducer script on it (as if you were the third-party evaluator receiving it cold) and confirming the digests match under a written reproduction contract.

## Prerequisites

- Chapter [`03-reproducibility-bundle-format.md`](../03-reproducibility-bundle-format.md).
- Exercises `01` (store) and `02` (adapters) completed, or their stubs.
- A small, cheap eval you can actually run. Recommendations:
  - A short `lm-evaluation-harness` task (e.g., a handful of `mmlu_high_school_*` sub-tasks or `arc_easy` at a small sample count) against a small open-weights model that runs on a laptop CPU (e.g., `Qwen2.5-0.5B-Instruct`, `SmolLM-135M`, or similar).
  - An Inspect task against the same model.
  - A tiny custom eval — a text-classification eval you write yourself with 50 examples and a pinned scorer.
- Container tooling (`docker` or `podman`).

## Problem statement

Pick one small eval. Run it, capture its output through your exercise-02 adapter, and package the run — dataset, task/evaluator, prompt, decoding config, seed, result digests, reproduction contract, and (for stretch goals) provenance attestations — as a signed reproducibility bundle. Then pretend to be a third party: on a fresh working directory, receive the bundle, verify all digests, run the reproducer, and produce a reproduction report.

The exercise is instructive when the reproduction *actually reproduces* — the same numbers come back, byte-exactly for deterministic pieces and within the contract's band for stochastic pieces. If the reproduction diverges by an amount you cannot attribute, that is the exercise's most valuable finding: the contract needs another documented source of variance or the run's determinism assumption is weaker than you thought.

## Requirements

Produce five artefacts.

### 1. `format-spec-v1.md`

A written specification for the bundle format. Sections:

1. **Serialisation choice.** Pick one of RO-Crate, BagIt, or OCI image, and justify. Document the alternate-form export path (if any).
2. **Directory layout.** The full tree the bundle contains, including `manifest.json`, `data/dataset/`, `data/task/`, `data/prompt/`, `data/evaluator/`, `data/decoding-config/`, `data/results/`, `data/reproduction-contract.md`, `data/provenance/` (chapter `04`), `data/security/` (chapter `05`), `signatures/`.
3. **Manifest schema.** The `manifest.json` structure, adapted from chapter `03`'s example. Include the `bundle_schema` version tag.
4. **Reference-vs-embed policy.** When the dataset (or model) is *referenced* rather than embedded, what the reference records (identifier, digest, licensing, acquisition instructions) and how the reproducer verifies the acquired bytes match.
5. **Canonicalisation.** Pointer to your `canonicalisation-v1.md` from exercise `01`.
6. **Signature layers.** Which parties sign the bundle (for this exercise: producer + reproducibility-program stand-in; layer 4 second-line and layer 5 Rekor are stretch goals).

### 2. `build-bundle.py` (or equivalent)

A build script that:

- Reads the eval record's digest from the store (exercise `01`).
- Walks the record's `lineage` fields, fetches each upstream artefact by digest, and copies bytes into `data/` under the layout from artefact 1.
- If the dataset is referenced (see below), records the reference in the manifest instead of embedding.
- Reads the container image manifest for your evaluator (see the container discipline below) and pins the image digest in the manifest.
- Writes `data/reproduction-contract.md` (artefact 3).
- Canonicalises `manifest.json`, computes `bundle_id = sha256(manifest.json)`, DSSE-signs the manifest with a producer key, and drops the signature into `signatures/`.
- Serialises the whole tree per artefact 1's choice (an RO-Crate zip, a BagIt bag, or an OCI image push).

### 3. `data/reproduction-contract.md`

The plain-language contract per chapter `03`. Sections:

1. **Determinism assumptions.** For every piece of the run — dataset load, prompt render, model inference, evaluator scoring, aggregate computation — state whether the piece is *exact-reproducible* or falls under a *statistical band*. If your eval uses a hosted judge, spell out the judge's determinism guarantee (or its absence).
2. **Exact-match artefacts.** The list of artefacts whose digests the reproducer must match byte-exactly. Typical: the rendered per-example prompts, the evaluator's per-example scores under greedy decoding on a fixed seed.
3. **Documented sources of variance.** Hardware nondeterminism, framework versions outside the pinned container, hosted-provider snapshot rotation, judge non-determinism. Name the reference environment.
4. **Statistical bands.** For any stochastic piece, the estimator and acceptance region. For a tiny eval this might be as simple as "the aggregate accuracy must fall within ±0.02 of the recorded value; wider divergence is a documented divergence." Cite the estimator.
5. **Divergence response.** What the reproducer does when a digest fails or a statistical band is exceeded (log, attribute, do not iterate).
6. **Legal terms.** Redistribution terms for the dataset (or licensed reference), the reproducer's confidentiality obligations if any.

### 4. `reproduce.py` (or equivalent)

The reproducer script. This is what the third-party evaluator would run. It must:

- Take a bundle path and a working directory as input.
- Verify the bundle's manifest signature against a producer public-key fixture you ship separately (a `producer-pubkey.pem` outside the bundle — the reproducer needs to acquire the key through a separate trust channel; in the exercise this is a manual copy-paste).
- Verify every digest in the manifest against the bytes in the bundle (or, for references, run the acquisition step and verify the acquired bytes hash correctly).
- Pull the pinned container image by digest and run the eval inside it, mounting `data/dataset/` (or the acquired dataset) and `data/evaluator/` as inputs.
- Compare the eval's output digests against the manifest's `results.*` digests under the reproduction contract.
- Emit a `reproduction-report.json` naming pass/fail per artefact and pass/fail per statistical band.

### 5. `reproduction-report.json`

The report your reproducer emits after running against the bundle you built. It should show, for a well-authored bundle, exact matches on the deterministic artefacts and within-band results on the stochastic ones.

## Container discipline

The evaluator has to run inside a pinned container. Concretely:

- Write a small `Dockerfile` that pins the base image by digest (`FROM python:3.11.7-slim@sha256:…` or equivalent), pins every `pip install` version, and copies the evaluator code.
- Build the image locally; record its digest.
- Include the image *in the bundle* as an OCI layout (`data/evaluator/image/`), or as a tarball (`docker save`) that the reproducer loads into its local runtime. The bundle should not require the reproducer to have network access to a registry to run.
- Pin the model checkpoint by digest too. If you use an open-weights model from Hugging Face, capture the safetensors file, hash it, and either embed or reference (embedding is fine for models < 500 MB; reference otherwise).

## Starter guidance

- **Pick the smallest eval that will still exercise the shape.** 50 examples is enough. Do not run MMLU end-to-end.
- **Prefer greedy decoding.** Sampled decoding is instructive but adds a statistical-band section you may not want to write for a first bundle. Do greedy, get the exact-reproducible loop working, then add sampling as a stretch.
- **Do not embed anything you cannot re-license.** If your eval uses `mmlu_high_school_*` or another CC-licensed dataset, cite the licence and either embed under the licence or reference. If your evaluator is your own code, keep it under an MIT/Apache licence you can ship.
- **Do the reproducer on a fresh clone.** After you build the bundle, `git clone` into `/tmp/fresh` (or spin up a fresh container) and run `reproduce.py` there. It is startlingly easy to accidentally rely on state in your development directory.
- **When determinism fails, do not tune.** If greedy decoding on your local CPU produces one number and greedy decoding in the container produces another, the divergence is the *finding*. Write it into the contract as a documented variance source rather than editing the run to make them agree.
- **Write the contract before the reproducer.** If you write the reproducer first, you will implicitly encode the contract into the code and later readers will not know what "reproduced" means. Contract first, then implement.

## Acceptance criteria

You have succeeded if:

- `format-spec-v1.md` names the serialisation, layout, manifest schema, reference-vs-embed policy, canonicalisation, and signature layers — with no hand-waving.
- `build-bundle.py` produces a bundle whose manifest signature verifies and whose `bundle_id` is stable across two rebuilds of the same eval record.
- `data/reproduction-contract.md` distinguishes determinism from statistical band, names sources of variance, and specifies divergence response.
- `reproduce.py` runs on a fresh working directory, verifies every digest, runs the eval inside the pinned container, and emits a `reproduction-report.json` that (a) matches all exact-reproducible artefacts byte-exactly and (b) reports pass/fail per statistical band.
- A peer receiving your bundle plus the reproducer plus the producer public key can reproduce your run without asking you a follow-up question. If the peer cannot, that is not a peer failure; it is a bundle failure.
- The bundle carries at least one *referenced* artefact (the dataset if it is licence-restricted, or the model if it is too large) plus an acquisition-verification step in the reproducer.

## Stretch goals

- **Cassette-replay for a hosted call.** Add a hosted-judge call to the eval, record the request/response pair with the provider snapshot ID, and add a cassette-replay mode to the reproducer so the bundle is reproducible even after the provider retires the snapshot.
- **Sampled decoding + statistical band.** Rerun the eval under sampled decoding with a fixed seed, write the CI-band section of the contract, and demonstrate that ten reproducer runs cluster inside the band.
- **Sigstore-signed manifest.** Replace the local Ed25519 producer signature with a `cosign sign-blob` flow; record the Rekor log index in the manifest under `signatures[*].rekor_log_index`.
- **RO-Crate + BagIt dual export.** Ship the bundle primarily as one and produce the alternate on demand; verify a reproducer can round-trip either shape.
- **Cross-hardware reproduction.** Run the reproducer on a different machine (a different laptop, a cloud VM with a different CPU or GPU) and record the divergence, if any. Update the contract's variance section with what you found.
- **Bundle in an OCI registry.** Push the bundle as an OCI artefact to a registry (`ghcr.io` or a local `zot`/`distribution` instance); pull it from a clean environment and reproduce.
