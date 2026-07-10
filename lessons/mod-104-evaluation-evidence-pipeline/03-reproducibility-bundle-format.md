# The Reproducibility Bundle

## Motivation

The release-gate's evidence bundle (mod-103 chapter `01`) is what the on-call assurance engineer walks at approval time. But the assurance program's obligations extend past approval: an independent evaluator (mod-109) has to be able to *rerun* the eval end-to-end and land within an acceptable band of the original number; a notified body under EU AI Act Article 43 has to be able to verify the technical documentation at Article 11 / Annex IV level; a market-surveillance authority under Article 74 has to be able to answer "would you get the same score today?" without asking anyone at the provider a follow-up question.

Two failure modes motivate the shape of the bundle.

The first is **irreproducible-because-implicit**: the eval report lists the numbers but not the seed, the sampler config appears in a `notes.md` that was not copied over, the dataset lives at a URL that has since redirected, or the judge model was silently upgraded between the report and the audit. When the auditor tries to rerun, the reproduction diverges by an amount nobody can attribute. Under NIST AI RMF MEASURE-3.1 (relevant AI actors have access to evaluation results) and MEASURE-2.13 (effectiveness of measurement) the case cannot argue that the number is a *property* of the system — it is only a property of a moment.

The second is **irreproducible-because-un-runnable**: the bundle is complete on paper but the third-party evaluator does not have the compute, the API keys, the internal packages, or the tooling permissions to actually rerun it. The evaluator sends back a "cannot verify" letter and the case's independent-evaluation leaf (mod-102 chapter `06`, mod-109) is a leaf with no artefact.

The bundle format this chapter draws is the release-assurance program's answer to both. It is not a directory of files — it is a **contract** between the producer of an eval result and any future re-runner.

## What a reproducibility bundle is

A **reproducibility bundle** is a signed, content-addressed, self-describing package that contains everything a third-party evaluator needs to rerun the eval end-to-end and to attribute any divergence between their run and the original run to a documented, well-formed cause.

Concretely, one bundle discharges *one eval-record* (or a small, related family of records — a full benchmark run with all sub-tasks). It contains:

1. **A manifest** — the top-level document that lists every artefact in the bundle by name, digest, and role.
2. **The dataset** — the exact eval-set bytes the eval was run against (or a pinned reference to them, if licensing prevents redistribution).
3. **The task / eval definition** — the harness code, evaluator code, scorer code, and metric definitions.
4. **The prompt template** — the pre-substitution template *and* the rendering function (or a byte-exact record of the rendered per-example prompts).
5. **The evaluator** — as source code, container image, or both. If as image, the image digest is pinned.
6. **The judge** — if LLM-as-judge, the judge's identity (a hosted-provider snapshot ID or an open-weights model digest), the judge prompt template, the judge decoding config, and the judge seed.
7. **The decoding config** — the sampler parameters for the primary model, canonicalised.
8. **The seed(s)** — the seed for the primary model's sampler, the seed for the judge's sampler (if any), and any auxiliary seeds the harness sets.
9. **The result hashes** — the digest of every output artefact the run produced: per-example completions, per-example scores, aggregates. Reproduction lands when the re-runner's re-computed digests match (up to a documented tolerance for the stochastic case).
10. **The reproduction contract** — a written specification of what "reproduced" means for this bundle: exact-match for deterministic cases, statistical band for sampled cases, and the tolerance rules for known unavoidable sources of variance.
11. **Provenance attestations** — the CycloneDX ML-BOM, SPDX-AI, SLSA build attestations, Sigstore signatures the bundle inherits from chapter `04`.
12. **A signed statement** — the bundle's own signature, tying it to the producer's key and to a Sigstore transparency-log entry (chapter `06`).

The bundle is a single archive — a directory tree serialised into a BagIt bag, an RO-Crate zip, or an OCI image layer, depending on the program's substrate choice — but the *shape* is invariant across the choice.

## Serialisation shape — choose one, pin it

Three serialisation shapes are worth naming; the program picks one and writes it into the format specification.

### RO-Crate

**Research Object Crate (RO-Crate)** is a community-supported format for packaging research data with metadata. An RO-Crate is a directory (or a zip of a directory) with a `ro-crate-metadata.json` at its root, describing every file and its role using schema.org vocabulary plus RO-Crate profile terms.

Why it fits: RO-Crate is designed for reproducibility, it has an active community around ML and computational reproducibility (a "Workflow RO-Crate" profile exists for computational workflows), and it plays cleanly with common metadata standards. The `ro-crate-metadata.json` is machine-readable and can be canonicalised for hashing.

Why it might not fit: RO-Crate profiles targeted at LLM evaluation specifically are still maturing; a program using RO-Crate today will typically extend it with an in-house profile pinned into the format spec.

### BagIt

**BagIt (RFC 8493)** is the Library of Congress-authored fixity-and-transfer format. A "bag" is a directory with `bagit.txt`, `manifest-<algo>.txt` (containing per-file digests), an optional `tagmanifest-<algo>.txt`, and a `data/` subdirectory containing the payload. Its purpose in life is *fixity* — you can hand a bag to anyone and they can verify every file's digest against the manifest.

Why it fits: BagIt is battle-tested at scale in national archives, has straightforward tooling, and gives per-file fixity for free. The `manifest-sha256.txt` is what a re-runner uses to verify the bundle survived transfer.

Why it might not fit: BagIt is agnostic about *meaning*. It says the files arrived unchanged; it does not say what any file is for. A program using BagIt puts the meaning into `bag-info.txt` and into a separate manifest artefact under `data/`.

### OCI image

**Open Container Initiative (OCI) image manifest** is the container-image substrate. The bundle is packaged as one image with layers containing the dataset, evaluator, harness, and results; the manifest lists digests; distribution uses OCI Distribution (the same protocol Docker Hub, GHCR, ECR speak).

Why it fits: OCI has a mature signing story (`cosign` / Sigstore), transparency-log integration (Rekor), replication (registry mirroring), and permission model (registry ACLs). If the program already ships model checkpoints as OCI artefacts, the reproducibility bundle joins that pipeline naturally.

Why it might not fit: OCI is opinionated about layer semantics — payload files inside a container image do not intrinsically carry roles, and readers have to inspect an in-manifest role-annotation to know what a given layer is for. Some regulatory readers prefer the "directory of files" mental model that RO-Crate / BagIt give.

Most programs adopt one primary shape and produce an alternate form on demand (e.g., an OCI bundle exported as a BagIt bag when a regulator requests it in that shape). What matters is that *one* is authoritative and pinned in the format spec.

## The manifest

Whatever the serialisation, the bundle carries a **manifest**: a canonical document listing every artefact by role, path, digest, and provenance. A representative shape:

```json
{
  "bundle_schema": "assurance-repro-bundle-v1",
  "bundle_id": "sha256:<self-digest>",
  "produced_at": "2026-05-07T14:22:01Z",
  "producer": {
    "peer_track": "model-evaluation-engineer",
    "identity": "did:web:evaluation.provider.example",
    "key_fingerprint": "SHA256:…"
  },
  "system_under_release": {
    "product": "internal-assistant",
    "release_candidate": "rc-2026-05-07",
    "surface_tier": "T2"
  },
  "eval_record_digest": "sha256:74a1…",
  "lineage": {
    "model":            { "role": "primary", "digest": "sha256:aa11…", "attestation": "in-toto v1.0" },
    "dataset":          { "role": "eval-set", "digest": "sha256:9ff2…", "reference": "harm-eval-set/v3.2" },
    "prompt_template":  { "role": "template", "digest": "sha256:22bb…" },
    "prompt_render":    { "role": "rendered", "digest": "sha256:33cc…" },
    "evaluator":        { "role": "evaluator", "digest": "sha256:012c…", "image": "sha256:def0…" },
    "judge":            { "role": "judge", "digest": "sha256:ff44…" },
    "decoding_config":  { "role": "sampler", "digest": "sha256:47da…" },
    "seed":             42
  },
  "results": [
    { "role": "per-example",   "digest": "sha256:55ee…", "path": "data/results/per-example.jsonl" },
    { "role": "aggregate",     "digest": "sha256:66ff…", "path": "data/results/aggregate.json" },
    { "role": "confidence-ci", "digest": "sha256:7700…", "path": "data/results/bootstrap-ci.json" }
  ],
  "reproduction_contract": {
    "role": "contract",
    "digest": "sha256:88aa…",
    "path": "data/reproduction-contract.md"
  },
  "provenance": {
    "cyclonedx_ml_bom": { "digest": "sha256:99bb…", "path": "data/provenance/cyclonedx-mlbom.json" },
    "spdx_ai":          { "digest": "sha256:aabb…", "path": "data/provenance/spdx-ai.spdx.json" },
    "slsa_provenance":  { "digest": "sha256:bbcc…", "path": "data/provenance/slsa-attestation.intoto.jsonl" },
    "sigstore_bundle":  { "digest": "sha256:ccdd…", "path": "data/provenance/sigstore-bundle.json" }
  },
  "signatures": [
    { "signer": "producer",       "kind": "dsse", "digest": "sha256:ddee…" },
    { "signer": "release-assurance", "kind": "dsse", "digest": "sha256:eeff…" }
  ]
}
```

The manifest is itself content-addressed and its digest is what the bundle *is* — the `bundle_id`. A reader who receives a bundle-id can independently verify: (a) the manifest hashes to the id, (b) every artefact in the manifest hashes to its listed digest, (c) every provenance attestation is well-formed, (d) both signatures verify.

## Redistribution vs. reference

Not every dataset can travel. Some eval-sets carry licensing terms that prohibit redistribution (proprietary vendor datasets, user-consented data with narrow processing terms), some are large enough that shipping them defeats the point (multi-terabyte corpora), and some contain material that has to be handled under a data-processing agreement rather than shipped in a bundle.

For these cases the bundle carries a **reference** rather than the bytes. The reference is:

- The dataset's stable identifier (an artefact-registry URL, a Hugging Face repo tag, a Croissant-format dataset record) *plus* its content digest under the pinned canonicalisation, *plus* the licensing terms under which the re-runner is expected to acquire it.
- A conformance test that the re-runner runs *before* rerunning the eval: given the acquired dataset bytes, the test canonicalises and verifies the digest matches the bundle's manifest. If the digest fails, the re-runner refuses to proceed (running against a different dataset is *not* reproducing the eval; it is running a different eval).

References are the exception, not the default. When they are used, they are documented in the manifest with `"role": "reference"` and the reason (`"licensing"`, `"size"`, or `"regulatory"`) is on the record.

## The reproduction contract

The most important document in the bundle is not the dataset or the evaluator — it is the **reproduction contract**. This is a plain-language specification of what "reproduced" means for this specific bundle. Without it, the re-runner's judgment about whether their re-run "matches" is theirs alone, and disagreement is unarbitrable.

A reproduction contract has six sections.

### 1. Determinism assumptions

Which parts of the run are supposed to be exactly reproducible, and which are not.

Typical determinism assumptions:

- **Greedy decoding on a fixed model checkpoint** — expected to be exact-reproducible up to hardware-level nondeterminism (which the contract calls out; see section 3).
- **Sampled decoding with a fixed seed** — expected to be exact-reproducible on the same runtime + framework versions the container image pins; documented to diverge across different framework versions or hardware.
- **LLM-as-judge** — the judge is expected to be exact-reproducible for hosted-provider snapshots that expose deterministic mode (e.g., `seed` parameter on OpenAI's Chat Completions, `temperature=0` where the provider documents determinism guarantees); otherwise the contract falls back to the statistical band in section 4.

### 2. Exact-match artefacts

Which artefacts the re-runner must reproduce byte-exactly. Typically:

- The rendered per-example prompts (given the template digest, the rendering function digest, and the dataset digest, the rendered outputs are a function of these three).
- The evaluator's per-example scores (given the completions and the evaluator digest, the scores are a function of these two).
- Any purely-symbolic aggregates.

The contract lists these by manifest role, and the re-runner's report cites which ones matched and which did not.

### 3. Documented sources of variance

Sources of variance that are *known and expected* and that the re-runner is instructed to tolerate.

Common categories:

- **Hardware nondeterminism.** Different GPUs, different CUDA versions, or different math-library kernels can produce bit-different floating-point outputs even at greedy decoding with a fixed seed. The contract names the reference hardware and the expected divergence magnitude; the re-runner's report notes their hardware and whether their divergence is within band.
- **Provider-side model snapshots.** Hosted providers occasionally rotate snapshots even when a pinned tag is requested. The contract records the snapshot identifier at run time; the re-runner records theirs; a snapshot mismatch is a documented cause of divergence.
- **Framework version drift.** Different versions of PyTorch, JAX, or the model provider's SDK can produce different outputs. The container image pins these; the contract references the container digest and notes that running outside the image is at the re-runner's own risk.
- **Judge-model non-determinism.** LLM-as-judge outputs vary even at `temperature=0` if the judge is a hosted model that does not guarantee determinism. The contract distinguishes deterministic-judge runs (exact-match expected) from non-deterministic-judge runs (statistical band expected; see section 4).

### 4. Statistical bands

For the stochastic cases, the contract specifies the *statistical* reproduction criterion.

Typical form:

- **Score-level.** "The re-runner's aggregate score must fall within the published 95% CI of the original aggregate. If it does not, the reproduction is a divergence and section 5 applies."
- **Distribution-level.** For sampling-heavy runs, the contract may specify a two-sample statistical test — e.g., the re-runner's per-example score distribution must not reject the null of equality against the original at the p=0.01 level under a two-sample Kolmogorov–Smirnov test — with the estimator and the acceptance region pinned.
- **Rate-level.** For safety-benchmark rates ("rate of harmful outputs on this attack set"), the contract may specify a binomial-CI-based band whose width scales with the number of eval-set examples.

The estimator and its assumptions come from the model-evaluation engineer (peer, level 30) — the release-assurance program does not invent the estimator, it *cites* it.

### 5. What to do when reproduction diverges

The contract states, in plain language, what happens when the re-runner's numbers fall outside the expected band:

- Log the divergence with the specific artefact whose digest did not match and the magnitude of the numeric divergence.
- Do not attempt to *tune* to close the gap — the contract requires the re-runner to run once and report, not to iterate.
- Return the divergence report to the assurance program along with the re-runner's runtime environment (hardware, framework versions, provider snapshot IDs).
- The assurance program, on receiving a divergence, opens an audit finding — chapter `05` (eval-set exfiltration / contamination) and mod-102 chapter `05` (defeaters) both live to receive these.

### 6. Legal terms and scope

- Redistribution terms for each artefact in the bundle.
- The re-runner's obligations around confidentiality and around not reusing the bundle for other purposes.
- The relationship of the re-run to any independent-evaluator or notified-body contract (mod-109).

## Deterministic execution

The bundle is only reproducible if the execution environment is. Two disciplines matter:

- **Container-pinned runtimes.** The evaluator (and, where applicable, the model runtime) ships as an OCI image whose digest is pinned in the manifest. The image contains every runtime dependency by exact version. The re-runner does not have to solve a `requirements.txt` at reproduction time; the image is already solved.
- **Recorded external calls.** If the eval calls a hosted provider (OpenAI, Anthropic, Google, or others), the bundle records — for every call — the request payload digest, the response payload digest, the provider snapshot identifier the provider returned, and any request headers relevant to determinism (like `seed` where supported). The re-runner can then either (a) rerun against the same provider snapshot and compare, or (b) load the recorded responses as a fixture and re-score. Option (b) — sometimes called "cassette-based replay" or "VCR-style replay" — is what the re-runner does when the hosted provider has retired the snapshot; the reproduction is then partial (evaluator + judge determinism only, not model-invocation determinism), and the contract's statistical band is what remains.

## The bundle at the release-gate

At the release-gate, the walker (mod-103 chapter `06`) resolves each hard criterion's evidence pointer to an assurance-store record and — where the criterion requires a reproducibility bundle by policy — to the bundle that discharges it. Not every criterion requires a bundle attached; typical policy is:

- **Bundle required** — every hard criterion tied to a statute (EU AI Act Articles 9–15 evidence, sector rules like SR 11-7 independent-validation), every criterion whose warrant is contested, every criterion consumed by a third-party evaluator (mod-109).
- **Bundle optional but recommended** — soft criteria whose disposition might later be questioned.
- **Bundle not required** — small, cheap-to-rerun criteria that discharge internal-goal soft rows.

Where a bundle is required, the walker asserts the bundle's manifest is well-formed, that every digest in the manifest resolves in the store or via a documented reference, and that the bundle's signature verifies against the producer's key. A bundle that fails any of these is a walker fail.

## The bundle after the release-gate

Post-release, the bundle is the artefact the assurance program hands to auditors, notified bodies, and third-party evaluators. Concrete workflows:

- **Third-party evaluator (mod-109).** The evaluator receives the bundle, runs it under the reproduction contract, and returns a signed reproduction report. The report becomes its own artefact in the store; the release-cycle's SACM `ArtifactPackage` (mod-102 chapter `04`) is amended to reference it.
- **Notified body (EU AI Act Article 43 conformity assessment).** For high-risk providers, the bundle is what the notified body verifies during a Article 43 assessment; the bundle plus the technical documentation (Article 11 / Annex IV) is what the conformity assessment consumes.
- **Market-surveillance authority (Article 74).** On request, the bundle is what the provider ships to the authority. The authority does not have to trust anyone at the provider; they hash and verify.
- **Post-market surveillance (Article 72 / mod-110).** When a post-market signal indicates a regression, the reproduction bundle for the prior release is what the assurance program runs to establish "was this signal already present at release, or is it new?"

## Summary

- A reproducibility bundle is a signed, content-addressed, self-describing package that discharges one eval-record (or a small related family) and that a third-party can rerun end-to-end.
- The bundle contains the dataset (or a licensed reference to it), the task / evaluator / scorer, the prompt template and render, the judge (if any), the decoding config, the seed(s), the result digests, the reproduction contract, the provenance attestations, and the signature.
- One of RO-Crate, BagIt, or OCI is picked as the primary serialisation and pinned in the format spec; alternate forms are produced on demand.
- The manifest is the single canonical document; the bundle's identity is the digest of the manifest.
- The reproduction contract specifies determinism assumptions, exact-match artefacts, documented sources of variance, statistical bands, divergence-response, and legal terms.
- Determinism is preserved via container-pinned runtimes and recorded external calls; cassette-replay is the fallback when hosted-provider snapshots are retired.
- The release-gate walker consumes the bundle at approval; auditors, notified bodies, and third-party evaluators consume it post-release.
- Chapter `04` picks up the supply-chain-provenance side: CycloneDX ML-BOM, SPDX-AI, SLSA build attestations, Sigstore signatures, safetensors, ModelScan / picklescan — the artefacts the bundle attaches under `data/provenance/`.
