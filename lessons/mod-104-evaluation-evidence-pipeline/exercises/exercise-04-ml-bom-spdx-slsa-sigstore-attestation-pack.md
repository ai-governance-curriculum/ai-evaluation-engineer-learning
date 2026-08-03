# exercise-04: ML-BOM, SPDX-AI, SLSA, and Sigstore Attestation Pack

**Estimated effort:** 3 hours

## Objective

Attach the **four supply-chain provenance attestations** from chapter `04` — CycloneDX ML-BOM, SPDX 3.0 AI Profile, SLSA v1.0 build provenance, and Sigstore keyless signatures — plus the loader-side discipline (safetensors + ModelScan / picklescan) to the reproducibility bundle you produced in exercise `03`. Verify the whole pack the way an auditor would: hash, walk, verify, and cross-check that the provenance manifests point at the same underlying artefact digests the reproducibility bundle already carries.

The exercise is instructive when the pack actually verifies end-to-end on a clean machine without you present. A pack that only verifies with a hidden environment variable, a hardcoded path, or an interactive prompt is a pack an auditor cannot reason about.

## Prerequisites

- Chapter [`04-supply-chain-provenance.md`](../04-supply-chain-provenance.md).
- Exercise `03` completed — you have a working reproducibility bundle with a signed `manifest.json`, at least one model artefact, and at least one evaluator container image whose digest is pinned.
- Tooling installed locally (any modern versions):
  - `cosign` (Sigstore CLI, `sigstore/cosign` on GitHub) — for signing and verifying.
  - CycloneDX CLI or SDK (`cyclonedx-cli`, or the CycloneDX Python `cyclonedx-python-lib`) — for generating and validating ML-BOM.
  - An SPDX 3.0 toolchain — `spdx-tools` or the SPDX 3.0 reference implementation. The AI Profile is still being tooled up; hand-authoring the JSON against the published schema is acceptable.
  - `slsa-verifier` (`slsa-framework/slsa-verifier`) or an equivalent verifier for in-toto envelopes.
  - `picklescan` (`mmaitre314/picklescan`) and `ModelScan` (`protectai/modelscan`).
  - `safetensors` (via `pip install safetensors` or the equivalent) — to load and re-serialise weights if your exercise-03 bundle ships a non-safetensors checkpoint.
- Optional: a GitHub Actions workflow (or GitLab CI, or a local `sigstore-python` OIDC flow) so you can experience the *keyless* signing path end-to-end. A hand-rotated Fulcio-issued cert against a workload identity is the closest local equivalent.

## Problem statement

Take the reproducibility bundle from exercise `03`. Under its `data/provenance/` directory, produce the four attestation families and the two loader-side scan reports so that every model / evaluator / bundle artefact is provenance-covered. Then write a verifier that walks the bundle, checks every attestation, cross-checks digests against the reproducibility-bundle manifest, and produces a machine-readable pass/fail report per artefact and per attestation family.

If your exercise-03 evaluator or model was not stored under safetensors, migrate before continuing — pickle-based checkpoints do not enter this pipeline.

## Requirements

Produce six artefacts (plus one verifier and one report).

### 1. `data/provenance/cyclonedx-mlbom.json`

A CycloneDX ML-BOM covering the model(s) in the bundle.

- Use a `component` of `type: "machine-learning-model"` per the CycloneDX ML-BOM profile; populate the `modelCard` sub-object with the model's name, version, source, training-set summary, evaluation-set summary, and considerations (ethical / fairness / safety / environmental where you can honestly speak to them). Where you cannot speak to a field, use the schema's `null`/absent convention rather than inventing content.
- Reference each training and evaluation dataset as a separate `component` and connect them via CycloneDX's dependency graph.
- Include tokeniser, adapter weights (if any), and embedding-model dependencies as their own components.
- Validate against the current CycloneDX ML-BOM JSON schema (`cyclonedx-cli validate` or the CycloneDX SDK's validator). Ship the validator invocation as part of your test script.
- Pin the CycloneDX schema *version* used in the file's `specVersion` field, and note the version in your `format-spec-v1.md` (from exercise `03`).

### 2. `data/provenance/spdx-ai.spdx.json`

An SPDX 3.0 SBOM using the AI Profile (and the Dataset Profile as a companion).

- Model as an SPDX Package with `packageType: "AI"` and AI-Profile-specific fields for usage instructions, safety-risk assessment, type of model, and evaluation.
- Datasets as SPDX Packages of type `dataset` with Dataset-Profile fields for licensing, anonymisation, data-collection process, known biases, and sensitive-personal-information handling.
- Use SPDX 3.0 relationships to express "this model was trained on this dataset" and "this evaluator uses this judge model" (where applicable).
- Use SPDX licence expressions (or `NOASSERTION` / `NONE` — never omit) for every third-party dependency.
- Validate against the current SPDX 3.0 schema.

### 3. `data/provenance/slsa-provenance-*.intoto.jsonl`

Three (or four) SLSA v1.0 provenance attestations, one per artefact, as in-toto envelopes:

- **`slsa-provenance-model.intoto.jsonl`** — over the model checkpoint (subject digest = the safetensors file digest or the shard-manifest digest).
- **`slsa-provenance-evaluator.intoto.jsonl`** — over the evaluator container image (subject digest = the OCI image digest from exercise `03`).
- **`slsa-provenance-bundle.intoto.jsonl`** — over the reproducibility bundle itself (subject digest = the `bundle_id` from exercise `03`'s `manifest.json`).
- **`slsa-provenance-judge.intoto.jsonl`** (optional) — if you used a self-built judge model.

Each attestation must:

- Use `predicateType: "https://slsa.dev/provenance/v1"`.
- Name a real `buildDefinition.buildType` (e.g., your CI system's SLSA build-type URL, or a documented local build-type URL you author for the exercise).
- Populate `buildDefinition.externalParameters` with the source ref (commit hash) and any user-supplied inputs.
- Populate `runDetails.builder.id` with an identity you can verify (an OIDC identity when signing via GitHub / GitLab / Sigstore's local OIDC helper; otherwise a documented local builder identity).
- Aim for SLSA **Build L2** at minimum. Note in the attestation which requirements you satisfy; where you fall short of L2, log the gap in the verifier's report rather than pretending.

### 4. `data/provenance/sigstore-bundle.json`

The Sigstore signatures binding every attestation and the bundle manifest.

- Use `cosign sign-blob` (keyless where possible; local key pair if OIDC is not available in your environment — document the choice) to sign:
  - Each SLSA attestation (`cosign sign-blob --bundle`).
  - The CycloneDX ML-BOM file.
  - The SPDX-AI file.
  - The reproducibility bundle's `manifest.json`.
  - The model checkpoint's safetensors file (or its shard manifest).
- Collect every signature and every Rekor inclusion proof (public Sigstore Rekor is fine for the exercise; a private Rekor deployment is a stretch goal) into a single `sigstore-bundle.json` in the Sigstore-bundle format (or an equivalent single-file collection you document).
- Every signature must record the OIDC identity (or the local-key identity) so a verifier can decide *who* signed.

### 5. `data/provenance/modelscan-report.json` and `data/provenance/picklescan-report.json`

Run `ModelScan` and `picklescan` against every model artefact in the bundle. Record:

- The scanner name, version, and the exact CLI invocation.
- The artefact digest scanned.
- The scan result (clean / flagged / errored) with per-finding detail if any.
- The scan timestamp.

A positive from either scanner is a **hard reject**: the exercise's verifier (artefact 7) must fail the pack when either report shows a finding. Do not paper this over with an "accepted risk" toggle — chapter `04`'s discipline is that a positive blocks.

If your bundle uses vendor-hosted models rather than local weights, produce a `data/provenance/vendor-attestations/<vendor>-<snapshot>.attest.json` per invocation instead — a pipeline-side envelope recording the request-payload digest, the response-payload digest, the vendor snapshot ID, and any relevant response headers, DSSE-signed by the producer.

### 6. `data/provenance/README.md`

A short (one page) walk of what lives in `data/provenance/`, who signed each artefact, and what a verifier can check without trusting anyone at the producer. This is the file an auditor reads first.

### 7. `verify-provenance.py` (or equivalent)

A verifier script that, given a bundle path (from exercise `03`) plus the public roots (Fulcio, Rekor, and any local trust roots you use), walks the pack in this order:

1. Load the reproducibility-bundle manifest; confirm the `bundle_id` hashes back to the manifest bytes.
2. Verify every Sigstore signature in `sigstore-bundle.json` against Fulcio (or the local trust root); verify each Rekor inclusion proof (or the local log's proof).
3. For each SLSA attestation, verify its DSSE envelope signature; verify the `subject.digest` equals the corresponding artefact digest in the reproducibility-bundle manifest (model → model artefact digest; evaluator → evaluator container digest; bundle → `bundle_id`).
4. Validate the CycloneDX ML-BOM against its published schema; assert the `component.hashes` for the model matches the reproducibility-bundle manifest's model digest.
5. Validate the SPDX-AI file against its published schema; assert the model's `packageChecksum` matches; assert every relationship resolves.
6. Read the ModelScan and picklescan reports; fail the pack if either shows a finding.
7. Emit `provenance-report.json` with a pass/fail row per artefact and per attestation family, plus the SLSA build level achieved.

### 8. `provenance-report.json`

The verifier's output when run against your pack. For a well-authored pack this should be all-pass; if not, use the report to drive the fixes (do not lower the verifier's bar to make it green).

## Starter guidance

- **Do not hand-author SLSA envelopes if you can help it.** Use a CI system with SLSA-native support (GitHub's `slsa-github-generator`, GitLab's built-in SLSA support, or an equivalent). The value is that the builder identity, the source ref, and the invocation are populated *by the builder*, not by you — that is what makes the attestation trustworthy.
- **CycloneDX and SPDX field names drift.** CycloneDX ML-BOM field names differ across 1.5 / 1.6; SPDX 3.0's AI Profile is still stabilising. Pin the version in your file's schema-version field, and pin your validator's version alongside. If a field name has moved between your reading of chapter `04` and today, follow the current schema.
- **Sign every artefact once at rest, then never sign in place.** If you edit the CycloneDX ML-BOM after signing, the signature is meaningless. Treat signed artefacts as content-addressed inputs to downstream steps.
- **Do the safetensors migration first.** If your exercise-03 checkpoint is `.pt` / `.bin` / `.pkl`, converting to safetensors is a one-liner (`from safetensors.torch import save_file; save_file(state_dict, "model.safetensors")` or equivalent for your framework) and unblocks the rest. picklescan on a pickle file will *always* find worrying opcodes; the point of safetensors is to eliminate the surface, not to argue about which opcodes are benign.
- **Run the verifier on a fresh clone.** Same discipline as exercise `03`: `git clone` into `/tmp/fresh` (or `docker run -v $BUNDLE:/bundle …`) and run `verify-provenance.py` there. Any hidden dependence on your development environment is a bug.
- **Use `cosign verify-blob` with `--certificate-identity` and `--certificate-oidc-issuer`.** Verifying the signature without pinning who signed it means an attacker with any Fulcio-issued cert passes verification. The identity pins are what make Sigstore's keyless flow trustworthy.
- **Failing a scan is a pass for the exercise.** If you deliberately feed the verifier a bundle whose ModelScan report has a synthetic finding, the verifier should fail loudly. Test that path; a verifier that only reports pass is not a verifier.

## Acceptance criteria

You have succeeded if:

- The four attestation files (CycloneDX ML-BOM, SPDX-AI, SLSA envelopes, Sigstore bundle) exist under `data/provenance/` in the exercise-03 reproducibility bundle, and each validates against its published schema.
- Every SLSA attestation's `subject.digest` matches the corresponding artefact digest recorded in the reproducibility-bundle manifest — model, evaluator, bundle — with no divergence.
- Every model artefact in the bundle is stored as safetensors (or the exercise notes a documented, hard-tested exception) and has clean ModelScan and picklescan reports.
- `verify-provenance.py` runs on a fresh working directory against the bundle, using only the bundle plus the public roots (Fulcio, Rekor, and any local trust root you document), and produces `provenance-report.json` with an all-pass result.
- `verify-provenance.py` fails loudly if you tamper with any attestation (edit one byte in the CycloneDX ML-BOM, or point one SLSA subject digest at the wrong artefact) — test both failure modes and record the verifier's behaviour.
- The pack demonstrates SLSA **Build L2 or higher** for at least the bundle-assembly attestation. Where any attestation falls short of L2, the shortfall is documented rather than hidden.
- A peer reading your pack plus `data/provenance/README.md` can, in under fifteen minutes and without asking you a follow-up, explain what every attestation asserts, who signed it, and how they would independently verify it.

## Stretch goals

- **Keyless from a real OIDC issuer.** Move signing into a GitHub Actions workflow (or GitLab CI job) so the Fulcio cert is bound to a `workflow_ref` identity rather than a local key. Update the verifier's identity pin accordingly and demonstrate that a signature produced from a different workflow ref fails verification.
- **Private Rekor.** Stand up a local Rekor instance (`sigstore/rekor` in a container) and route the pack's signatures through it. Show how the verifier can be pointed at the private log via `--rekor-url` and how the pack becomes verifiable in an air-gapped environment given the log's public key.
- **Vendor-hosted-model envelope.** If your exercise-03 bundle uses a hosted API, produce `data/provenance/vendor-attestations/<vendor>-<snapshot>.attest.json` per invocation — DSSE-signed by the producer, recording request digest, response digest, snapshot ID, and headers. Extend the verifier to require the envelope for any hosted-model invocation.
- **SLSA Build L3.** Move the bundle-assembly build into a hardened builder (SLSA-framework-endorsed GitHub-hosted runners with `slsa-github-generator`, or the equivalent on your CI) and demonstrate Build L3 for the bundle-assembly attestation. Document the specific L3 requirements you meet.
- **CycloneDX ↔ SPDX diff.** Produce a small tool that reads both provenance files and reports fields that disagree (e.g., licence for the same dependency, or hash for the same artefact). Any disagreement is a finding — one of the two is wrong.
- **VEX statements.** Where a dependency in the ML-BOM has a known CVE, attach a CycloneDX or CSAF VEX statement documenting exploitability status for your usage. This foreshadows how post-market surveillance (mod-110) will treat evolving vulnerability information.
- **Reproducer-side scan.** Have the exercise-03 reproducer script (`reproduce.py`) run ModelScan / picklescan on the model *before* loading it, and refuse to proceed on any finding. This closes the loop between the pack the producer publishes and the discipline the re-runner enforces.
