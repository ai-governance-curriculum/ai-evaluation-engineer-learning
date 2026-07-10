# Signing the Assurance Bundle and Persisting Into ISO/IEC 42001 Records

## Motivation

The store (chapter `01`), the adapters (chapter `02`), the reproducibility bundle (chapter `03`), the supply-chain provenance (chapter `04`), and the eval-set-security clauses (chapter `05`) are all *inputs*. What the release-gate emits — the artefact the assurance program has to be able to show a regulator, a notified body, or an internal ISO/IEC 42001 auditor months or years later — is one signed, self-describing, versioned bundle that ties the whole together and lands in the AIMS records.

Two failure modes motivate the shape of this chapter.

The first is **the phantom bundle**: an assurance program has all the pieces but does not stitch them into a single signed artefact. The evidence lives in one system, the provenance in another, the MLSec clauses in a third; the "release-gate output" is a PDF someone exported and stored. Under ISO/IEC 42001 clause 7.5 (documented information), a PDF disconnected from its evidence is a claim about the past. Under EU AI Act Article 11 / Annex IV (technical documentation) and Article 74 (market-surveillance access) the burden is on the provider to *demonstrate*, not to assert.

The second is **the frozen bundle**: an assurance program does sign a bundle but freezes it too early — before the release decision, before rollback contract testing, before the third-party evaluator's report has landed — and then treats the bundle as complete. The bundle is missing the *decision* it was supposed to record. Auditors reading ISO/IEC 42001 clause 9.1 (monitoring, measurement, analysis, evaluation) or clause 10 (improvement) find a bundle that stopped at approval and cannot answer what actually happened.

This chapter draws the shape of the signed release-gate output artefact and how it persists into the AIMS records.

## What "assurance bundle" means at this stage

Chapters `01`–`05` used *bundle* loosely — the reproducibility bundle (chapter `03`) is one thing; the release-gate's overall evidence set is another. This chapter is precise about the top-level artefact, the **assurance bundle** (or "release-gate output artefact" — the two names are used interchangeably in this program), which contains:

- **The decision record.** The release-gate walker's output: which criteria passed, which failed, which were dispositioned as soft, what the signed disposition is (go / no-go / defer / promote-at-lower-tier), the signer(s), the RACI (mod-103 chapter `05`).
- **The pre-registered criterion set.** The `gate-criteria-vN.md` (mod-103 chapter `01`) that the walker walked.
- **The evidence-index snapshot.** A canonicalised index (chapter `01`) restricted to the digests the criterion set resolved to — a self-contained "which evidence was consumed here" record.
- **The reproducibility bundles.** One per hard criterion whose policy required one (chapter `03`), plus optional bundles for higher-scrutiny soft criteria.
- **The provenance sub-tree.** The CycloneDX ML-BOM, SPDX-AI, SLSA, Sigstore artefacts for every model / evaluator / judge / dataset in scope (chapter `04`).
- **The MLSec sub-tree.** The contamination attestation, exfiltration-control attestation, supply-chain clauses, canary attestation (chapter `05`).
- **The rollback / rollforward contract.** The pre-tested reversal procedure (mod-103 chapter `05`), pinned to the digests of the current and previous release candidates.
- **The post-market handoff.** The online-eval slice, the incident-detection thresholds, the review cadence the release-gate hands to mod-110.
- **The assurance case at freeze.** The SACM `ArgumentPackage` (mod-102 chapter `04`) as of the release decision, tied to the evidence-index snapshot.
- **The signatures.** DSSE envelopes for every producer's contribution, plus the release-assurance program's own signature over the top-level manifest, plus the Rekor inclusion proofs.

The assurance bundle is one archive (RO-Crate, BagIt, or OCI, per chapter `03`'s serialisation choice) with a top-level manifest whose digest is the bundle's identity.

## The top-level manifest

Extending the reproducibility-bundle manifest shape from chapter `03`:

```json
{
  "bundle_schema": "assurance-release-gate-bundle-v1",
  "bundle_id": "sha256:<self-digest>",
  "produced_at": "2026-05-07T18:42:11Z",
  "producer": {
    "role": "release-assurance-program",
    "identity": "did:web:assurance.provider.example",
    "key_fingerprint": "SHA256:…"
  },
  "system_under_release": {
    "product": "internal-assistant",
    "release_candidate": "rc-2026-05-07",
    "surface_tier": "T2",
    "previous_release_candidate": "rc-2026-04-19"
  },
  "gate": {
    "criterion_set_version": "gate-criteria-v7",
    "criterion_set_digest": "sha256:…",
    "walker_version": "gate-walker-v3.2",
    "decision_record_digest": "sha256:…",
    "disposition": "promote",
    "signers": [
      { "role": "release-assurance-on-call",     "identity": "did:web:…", "key_fingerprint": "SHA256:…" },
      { "role": "second-line-effective-challenge", "identity": "did:web:…", "key_fingerprint": "SHA256:…" }
    ]
  },
  "evidence_index_snapshot_digest": "sha256:…",
  "reproducibility_bundles": [
    { "criterion": "GATE-FA-01", "digest": "sha256:…" },
    { "criterion": "GATE-ROB-02", "digest": "sha256:…" },
    { "criterion": "GATE-TRANS-01", "digest": "sha256:…" },
    …
  ],
  "provenance_manifest_digest": "sha256:…",
  "mlsec_manifest_digest": "sha256:…",
  "rollback_contract_digest": "sha256:…",
  "post_market_handoff_digest": "sha256:…",
  "assurance_case_freeze_digest": "sha256:…",
  "signatures": [
    { "role": "release-assurance-program", "kind": "dsse", "digest": "sha256:…", "rekor_log_index": 12345678 },
    { "role": "second-line",              "kind": "dsse", "digest": "sha256:…", "rekor_log_index": 12345679 }
  ],
  "aims_persistence": {
    "record_id": "AIMS-REL-rc-2026-05-07",
    "iso_42001_clause_map": {
      "7.5": "documented information — bundle as controlled document",
      "8.1": "operational planning and control — walker + rollback contract",
      "8.2": "AI-system-impact assessment — impact-assessment cross-reference",
      "8.3": "AI-system requirements — criterion set discharge",
      "8.4": "life-cycle activities — release-cycle position",
      "9.1": "monitoring, measurement, analysis, evaluation — decision record + walker output",
      "9.2": "internal audit — audit-ledger cross-reference",
      "9.3": "management review — periodic review of gate outcomes",
      "10.1": "continual improvement — corrective actions from soft-fail dispositions",
      "10.2": "nonconformity and corrective action — hard-fail dispositions, if any"
    }
  }
}
```

The `bundle_id` is the digest of this manifest under the pinned canonicalisation. A regulator, an auditor, or a third-party evaluator who receives `bundle_id` can independently:

1. Fetch the manifest bytes from the store (chapter `01`).
2. Verify the manifest hashes to `bundle_id`.
3. Verify every referenced digest resolves and its own bytes hash correctly.
4. Verify both signatures against Fulcio-issued certs; verify Rekor inclusion proofs.
5. Verify the walker's decision record against the criterion set (deterministic given the evidence index snapshot).
6. Verify the assurance case at freeze against the evidence index snapshot.

None of the six operations requires trusting anyone at the provider.

## The signing story in detail

Signing is layered — each layer signs a different thing, and every layer is verifiable independently.

### Layer 1 — Per-producer signatures

Every producer contributing to the bundle signs their own contribution:

- The AI-eval engineer signs their evidence records.
- The model-evaluation engineer signs their bench reports and reproducibility bundles.
- The risk engineer signs the harm inventory revision, red-team report, guardrail-eval report.
- The `ai-infra-security` peer signs the MLSec attestations.
- The AI-governance analyst signs the first-draft cards and jurisdictional crosswalks.
- The third-party evaluator, when present, signs the independent-evaluation report.

Each signature is a DSSE envelope over the artefact's canonical bytes. The signer's identity is a Fulcio-issued cert bound to the producer's OIDC identity (the peer track's CI system, the peer track's HSM-backed workflow identity, or a hardware token). Rekor records the inclusion proof.

### Layer 2 — Reproducibility-bundle signatures

For each reproducibility bundle produced under chapter `03`, the bundle's manifest is DSSE-signed by the producer. The signature covers the whole bundle by construction (the manifest lists every artefact's digest).

### Layer 3 — Assurance-bundle signature

The top-level assurance bundle is DSSE-signed by the release-assurance program itself. The signing identity is *the program's*, not any individual engineer's — the program's OIDC identity, or a program-owned HSM-backed key, or a program-owned Fulcio-issued cert. This layer is what the market-surveillance authority verifies when they receive `bundle_id`.

### Layer 4 — Second-line effective-challenge signature

For hard-tier releases, the second-line reviewer (mod-103 chapter `05`, SR 11-7 effective-challenge shape) signs the assurance bundle independently. Their signature attests that they performed the effective-challenge and that they concur with the disposition (or that they logged a documented disagreement with an audit finding on the record). Two signatures land in the top-level `signatures` array — the release-assurance program's and the second-line's — with distinct roles.

### Layer 5 — Transparency-log inclusion

Every signature at layers 1–4 lands in Rekor (or the program's own transparency log). The Rekor log-index and inclusion-proof are recorded in the manifest. A future auditor can query Rekor independently and confirm the entry exists at the expected index and the proof verifies.

## The AIMS records

ISO/IEC 42001 clauses are the destination the bundle lands in. Six clauses matter directly:

### Clause 7.5 — Documented information

Clause 7.5 governs how the AIMS creates, updates, and controls documented information. The assurance bundle is a *controlled document* under this clause:

- **Identification.** The bundle has a unique identifier (`bundle_id`).
- **Format.** The bundle's serialisation is pinned (RO-Crate / BagIt / OCI).
- **Review and approval.** The signatures at layers 3 and 4 are the review-and-approval record.
- **Distribution, access, retrieval, use.** The bundle's storage location and access controls (chapter `01`).
- **Storage and preservation.** Retention class per chapter `01`.
- **Change control.** The bundle is immutable; a change is a new bundle-id superseding the old one, with the supersession recorded in an append-only supersession log.
- **Retention and disposition.** Retention per chapter `01`; disposition per the legal-hold rules.

The AIMS's "controlled documents register" lists the bundle by `bundle_id`, its clause mapping, and its retention class.

### Clause 8.1 — Operational planning and control

Clause 8.1 requires the AIMS to plan, implement, and control the processes needed to meet AI-management-system requirements. The bundle's `gate.walker_version` and `rollback_contract_digest` fields are the operational-control evidence. The walker's operation (mod-103 chapter `01`) is a controlled operational process; its outputs land here.

### Clause 8.2 — AI system impact assessment

Where an ISO/IEC 42005 impact assessment is required for the system-under-release, the impact-assessment record is *referenced* by the bundle (typically produced by the AI-governance analyst and elevated by the mod-105 pipeline). The reference resolves to a store artefact with its own digest.

### Clause 8.3 — AI system requirements

Clause 8.3 governs the AI-system requirements the AIMS has committed to. The pre-registered criterion set (`gate-criteria-vN`) is the requirements record for this release cycle.

### Clause 8.4 — Life-cycle activities

Clause 8.4 covers the AI-system life cycle (design, development, deployment, operation, decommissioning). The bundle records where in the life-cycle the release candidate sits (`system_under_release.surface_tier`) and pins the previous release candidate (`previous_release_candidate`) so the life-cycle can be walked.

### Clause 9.1 — Monitoring, measurement, analysis, evaluation

Clause 9.1 is the AIMS's evaluation clause. The walker's decision record and its per-criterion pass/fail record are the primary artefacts here.

### Clause 9.2 — Internal audit

Clause 9.2 requires periodic internal audit against clauses 4–10. The bundle's `evidence_index_snapshot` gives an internal auditor a self-contained view of the evidence consumed at this release, without having to trust the state of the wider store months later.

### Clause 9.3 — Management review

Clause 9.3 requires top management to review the AIMS at planned intervals. Aggregate reporting over bundles (period → gate outcome distribution, disposition mix, soft-fail counts, exception-approval counts, rollback-invocation counts) is what feeds management review; the individual bundles are the primary sources.

### Clause 10.1 / 10.2 — Continual improvement, nonconformity, and corrective action

Soft-fail dispositions generate corrective-action records; hard-fail dispositions or exception approvals generate nonconformity records. Both classes reference back to the bundle.

## Persistence procedure

Concretely, once the walker has produced its decision record and the two signatures are in place:

1. **Assemble.** The pipeline builds the archive by walking every referenced digest in the top-level manifest, fetching bytes from the store, and packaging them per the pinned serialisation. If any digest is missing or fails verification, the assembly aborts.
2. **Canonicalise.** The top-level manifest is emitted under the store's canonicalisation rule (chapter `01`).
3. **Sign.** The release-assurance program's key signs the manifest as a DSSE envelope; the second-line reviewer signs independently. Both signatures include OIDC identity claims.
4. **Log.** Both signatures are submitted to Rekor (or the program's own log). The log-indexes and inclusion-proofs are added to the manifest, and the manifest is re-emitted with the updated `signatures[*].rekor_log_index` fields. (The manifest's digest changes at this step, so the top-level digest recorded on Rekor is the *pre-log-index* digest; the assembly writes both — the `bundle_id` seen at ingest is the post-log-index digest, and the log-index is recorded under a `bundle_id_pre_log` field the reader can compute.)
5. **Persist.** The bundle is written to the store (write-once bucket, object-lock retention per chapter `01`), and to the AIMS controlled-document register with the clause mapping.
6. **Notify.** Downstream consumers — mod-105 (cards), mod-109 (third-party evaluator), mod-110 (post-market surveillance) — receive the bundle-id and can pull.

## Verification procedure — the auditor's walk

A regulator, notified body, or internal auditor with a `bundle_id` walks the bundle in this order:

1. Fetch the manifest bytes; hash and confirm the digest matches `bundle_id`.
2. Verify layer 3 signature: the DSSE envelope over the manifest verifies against a Fulcio-issued cert tied to the release-assurance program's OIDC identity.
3. Verify Rekor inclusion for the layer 3 signature at the recorded log-index.
4. Verify layer 4 signature (second-line) similarly, if present at this tier.
5. For each referenced digest in the manifest, fetch the bytes and confirm the digest.
6. For each reproducibility bundle referenced, walk the reproducibility manifest similarly (chapter `03`).
7. For each provenance attestation, verify its DSSE envelope; verify the SLSA subjects match reproducibility-bundle artefact digests; verify SPDX-AI / ML-BOM structural conformance.
8. For each MLSec attestation (chapter `05`), verify the peer's signature and the clause references.
9. Cross-check the walker's decision record against the criterion set: does the recorded pass/fail per criterion correspond to the evidence in the index snapshot?
10. Verify the assurance-case-at-freeze parses as SACM and its `Artifact` references resolve into the evidence index snapshot.

Every step is mechanical; no step requires trust in a party inside the provider. This is what makes the bundle *defensible*.

## Interaction with EU AI Act instruments

EU AI Act Article 11 / Annex IV requires high-risk providers to maintain technical documentation. The bundle-id is the technical-documentation record's persistent reference. Article 12 (record-keeping) and Article 18 (documentation-retention) drive the retention class. Article 47 (declaration of conformity) references the technical documentation set the bundle discharges into. Article 61 / 72 / 73 (post-market monitoring and reporting) draw from bundles as the reference for "what was true at release" against which post-market signals are compared. Article 55 (GPAI systemic-risk providers) adds obligations covered in mod-111.

Article 74 (access to documentation on market-surveillance request) is the specific place where the bundle-id — and its bytes — has to be produceable. A market-surveillance authority sends a request; the provider's response is the bundle plus the walker's verification instructions plus the Fulcio and Rekor public roots. The authority does the walk in their own environment.

## What the release-gate output artefact enables downstream

Once the bundle is signed and persisted:

- **Mod-105 (cards).** The model card, system card, and dataset card the assurance program publishes for external audiences are *views* over the bundle. The card's "evaluation" section resolves to bundle-referenced evidence; the "risk" section resolves to the harm-inventory freeze in the bundle; the "supply-chain" section resolves to the provenance sub-tree.
- **Mod-109 (third-party evaluator interface).** The third-party evaluator receives the bundle-id, walks the reproducibility bundles, and produces their own signed independent-evaluation report. Their report is a new store artefact that the bundle's SACM `ArgumentPackage` is later amended to reference.
- **Mod-110 (post-market surveillance).** Post-market monitors evaluate the deployed system's behaviour and compare against the bundle-referenced baseline. When a signal indicates a regression, the reproducibility bundles inside the assurance bundle are what the peer track reruns to disambiguate.
- **Mod-111 (GPAI systemic-risk).** For GPAI-systemic-risk-tier releases the bundle is extended with additional Article 55 evidence (systemic-risk assessment, adversarial red-team, cybersecurity assessments) covered in the GPAI module.
- **Mod-112 (program ownership).** The set of bundles a program has produced across a period is the substrate for AIMS management review (clause 9.3) and for corrective-action programs (clauses 10.1 / 10.2).

## Summary

- The release-gate emits one signed, self-describing, versioned **assurance bundle** — the release-gate output artefact — whose identity is the digest of its top-level manifest.
- The manifest binds the decision record, criterion set, evidence-index snapshot, per-criterion reproducibility bundles, provenance sub-tree, MLSec sub-tree, rollback/rollforward contract, post-market handoff, and assurance case at freeze.
- Signing is layered: producers sign contributions; reproducibility bundles are signed; the assurance bundle is signed by the release-assurance program; the second-line signs independently at higher tiers; every signature is Rekor-logged.
- Verification is mechanical and does not require trust in the provider — hash, verify, walk. Auditors, notified bodies, third-party evaluators, and market-surveillance authorities all walk the same steps.
- The bundle persists into ISO/IEC 42001 clauses 7.5, 8.1–8.4, 9.1, 9.2, 9.3, 10.1, and 10.2 with an explicit clause map.
- The bundle is the reference EU AI Act Articles 11 / 12 / 18 / 47 / 61 / 72 / 73 / 74 discharge against; where GPAI systemic-risk applies (Article 55), the bundle is extended in mod-111.
- Downstream, the bundle feeds mod-105 (cards), mod-109 (third-party evaluators), mod-110 (post-market), mod-111 (GPAI systemic-risk), and mod-112 (program ownership).
- Chapters `01`–`06` together give the AI Evaluation Engineer the evidence pipeline that the release-gate reads and the assurance program persists. What remains — cards, cross-jurisdictional mapping, sector overlays, deployment-tier gating, third-party interface, post-market, GPAI systemic-risk, program ownership — is covered in the following modules.
