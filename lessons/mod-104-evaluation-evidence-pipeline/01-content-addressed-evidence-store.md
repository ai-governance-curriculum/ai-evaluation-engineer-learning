# The Content-Addressed Evidence Store

## Motivation

An assurance case is only as defensible as the evidence its leaves resolve to (mod-102 chapter `05`). The release-gate is only as defensible as the bundle it walks (mod-103 chapter `01`). Both artefacts point *into* the evidence pipeline this module owns. If the pipeline cannot say — with digest-level certainty — which model version, which dataset, which prompt, which evaluator, which judge, which decoding-config, and which seed produced a given eval record, then the case is arguing about numbers whose provenance is a matter of trust rather than of proof.

Two release-assurance failure modes motivate the shape of the store.

The first is **mutable evidence**: an eval report is edited after it is signed, a benchmark score is quietly corrected between the release-gate decision and the auditor's arrival, or a "final" eval run gets a follow-up run that overwrites the original in the same location. Under ISO/IEC 42001 clause 7.5 (documented information: creation, updating, and control) and clause 9 (performance evaluation), an evidence artefact that can be edited in place is not evidence — it is a claim about the past. Under EU AI Act Article 12 (record-keeping) and Article 18 (retention of documentation) the same claim, in more legally binding language, is what a high-risk provider has to be able to hand to a market-surveillance authority.

The second is **decoupled lineage**: the evaluator ran, the score is stored, but nobody can reconstruct exactly which model checkpoint the score describes, which dataset revision the eval was run against, or which decoding config the sampler used. In practice this shows up when someone tries to reproduce a headline number six months later, gets a different result, and cannot tell whether the number moved because the model moved, because the eval-set moved, because a judge model was silently swapped, or because the sampler's temperature changed. Under NIST AI RMF MEASURE-2.13 (effectiveness of measurement) and MANAGE-4.1 (post-deployment monitoring), lineage-broken evidence is a broken measurement.

The rest of this chapter draws the substrate that avoids both.

## What "content-addressed" means

An artefact is **content-addressed** when its identifier is a cryptographic digest of its bytes under a canonicalisation rule. The identifier is not chosen by a naming committee, is not allocated by a database sequence, and is not a UUID — it is a function of the artefact itself.

Two consequences follow.

- **Immutability is automatic.** Editing the artefact changes its identifier. The old identifier and the old bytes remain the referent of anything that already cited them; the new identifier is a new artefact. There is no "in-place edit" primitive. This is what makes the store worth showing an auditor.
- **Deduplication is automatic.** Two runs that produce byte-identical eval records under the same canonicalisation share an identifier. The store is telling the truth about identity, not merely holding two rows.

The identifier is typically written as `sha256:<hex>` (or the same shape with a stronger digest — `sha384`, `sha512`, or a hash-agility scheme). The Open Container Initiative image-spec, in-toto attestations, Sigstore's Rekor transparency log, and Git commit objects all use this shape; when the pipeline emits a digest, it is joining a family of substrates the wider ecosystem already knows how to verify.

Canonicalisation matters as much as the digest. Two evaluators that produce logically equivalent JSON but disagree on key ordering or on whitespace will produce different digests, and the store will (correctly) treat them as different artefacts. The pipeline needs a single, written, versioned canonicalisation rule for each artefact class. Common choices:

- **JSON eval records** — RFC 8785 JSON Canonicalization Scheme (JCS), or a project-pinned equivalent (sorted keys, LF newlines, no trailing whitespace, UTF-8 without BOM).
- **Tabular data** — a canonical Parquet writer configuration (schema pinned, column order pinned, no row-group randomisation) or CSV with a pinned dialect.
- **Model checkpoints** — the on-disk file (safetensors — see chapter `04`) hashed directly; if the checkpoint is sharded, the manifest that lists the shards and their per-shard digests is what the pipeline addresses.
- **Prompts and templates** — the raw template text after variable-substitution normalisation; the template's *pre*-substitution form is a separate content-addressed artefact.

Whichever canonicalisation the program picks, it is written down, version-tagged (`canonicalisation-v1.md`), and the store rejects an artefact whose canonicalisation-version tag disagrees with the current rule. That rejection is a *feature* — it forces the reviewer to look at what changed.

## The seven lineage dimensions

An eval record does not stand alone. Every record is produced by an execution whose *inputs* are seven things — the objectives call them out one by one, and the store's schema treats each as a first-class citizen with its own content-addressed identifier:

| Dimension           | What it addresses                                                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Model version**   | The exact weights that produced the completion. Digest of the safetensors file (or shard manifest). If the model is hosted (a vendor API), the digest is over a provider-attested identifier — vendor snapshot ID plus any config the vendor exposes — see chapter `02`. |
| **Dataset hash**    | The exact eval-set revision. Digest of the canonicalised data (JSONL, Parquet, RO-Crate metadata — chapter `03`). Includes any pre-processing / filtering the store applies before the eval.                                                             |
| **Prompt**          | The template *and* the rendered form. Two content-addressed artefacts — the template pre-substitution, and the rendered per-example prompts (or a deterministic renderer + template + variables, whichever the program chooses to hash).                             |
| **Evaluator**       | The scoring code and its version. Digest of the evaluator's source (or its container image), plus the evaluator's configuration (which metric, which rubric, which reduction).                                                                                       |
| **Judge**           | If the evaluator is LLM-as-judge, the judge model and its prompt template are lineage on their own. Judge lineage is often longer than the primary model's — the judge, judge prompt, judge decoding config, judge seed all bind into the eval-record's identity.       |
| **Decoding config** | Temperature, top-p, top-k, max tokens, repetition penalty, tool schemas, stop sequences, any sampler-specific parameter. Bundled as a single canonicalised object and hashed.                                                                                        |
| **Seed**            | The random seed the sampler was pinned to (or a `null` marker that the run was intentionally stochastic — a `null` seed is *itself* a recorded value, not an absence).                                                                                                |

The eval record binds the seven dimensions into a **run identity**. In practice the record has a `lineage` field that is an object of digests, one per dimension, and the record's own identifier is the digest of the canonicalised record (which includes the `lineage` field). So the run identity is a *derived* content address, computed from the seven upstream addresses plus the result payload:

```
run-id = sha256(canonicalise({
  lineage: {
    model:            "sha256:<model-digest>",
    dataset:          "sha256:<dataset-digest>",
    prompt_template:  "sha256:<template-digest>",
    prompt_render:    "sha256:<rendered-digest>",
    evaluator:        "sha256:<evaluator-digest>",
    judge:            "sha256:<judge-digest>|null",
    decoding_config:  "sha256:<decoding-digest>",
    seed:             <int>|null,
  },
  results: <canonicalised results payload>,
  context: {
    executed_at:  "<RFC 3339 timestamp>",
    executor:     "<peer-track producer identity>",
    platform:     "<phoenix|langfuse|inspect|lm-eval|weave|vertex|bedrock|foundry|internal>",
    schema_ver:   "eval-record-vN",
  },
}))
```

The `context.executor` and `context.platform` fields are metadata about the *producer*, not part of what the identifier proves. What the identifier proves is that the seven lineage inputs and the results payload together produce a canonical byte-string with this hash — nothing more, nothing less.

## The store as a Merkle DAG

The seven lineage inputs are themselves content-addressed artefacts, each with its own identifier. So the store is a **Merkle-shaped directed acyclic graph** (DAG): each node is an artefact, each edge is a content-address reference from one artefact to another. An eval record points to seven upstream artefacts; those artefacts in turn may point further (a dataset artefact points to the datasheet it discharges; an evaluator artefact points to its container image manifest; a judge points to its prompt template and its own decoding config).

Two audit properties fall out for free:

- **Any subtree is verifiable in isolation.** An auditor who receives the record's digest and the seven upstream digests can independently hash each artefact and confirm the linkage. The pipeline does not need to be trusted; only the digest algorithm and canonicalisation rule do.
- **Any tampering is detectable.** Editing any node changes its digest, which invalidates every downstream reference. A dataset revision cannot be silently retro-fitted under an old eval record.

The DAG is the substrate on which the assurance case's SACM `Artifact` elements resolve (mod-102 chapter `04`). Each SACM `Artifact` references one node in the DAG by its content address; when the case is re-run against a later release, the diff between cycles is exactly the set of changed digests.

## What the store looks like on disk

The store is deliberately dumb. Two directory-shaped patterns show up in real programs:

**Object-store shape (typical):** an object store (S3, GCS, Azure Blob) with a bucket whose keys are the digests themselves:

```
s3://assurance-store/objects/sha256/ab/cd/abcd1234…/
    ├── payload.json          # canonicalised bytes
    ├── media-type            # single-line: application/vnd.assurance.eval-record+json;v=1
    └── legal-hold             # optional flag file for retention holds
```

The two-level prefix (`ab/cd`) is a shard for filesystem-friendly listing; the digest is written in full in the leaf directory name so an operator can inspect. Object versioning is *disabled* (or set to write-once) and bucket-level object-lock (S3 Object Lock in Compliance mode; GCS Bucket Lock; Azure immutable-storage policies) is turned on with a retention period at least equal to the highest applicable regulatory retention (EU AI Act Article 18 requires ten years of technical-documentation retention for high-risk providers; sector rules — SR 11-7, FDA — set longer horizons; the retention period the bucket carries is the *maximum* of the applicable ones plus a margin).

**Log-structured shape (secondary):** a transparency log — Sigstore Rekor, or an OpenSSF Sigstore-adjacent log the program runs itself — where each entry is a signed inclusion-proof for a digest. The log is *not* the primary evidence store; it is a witness that the digest existed at a given time under the program's key. The primary store still holds the bytes; the log holds the notarisation. Chapter `06` returns to the log when the assurance bundle is signed.

Both shapes co-exist. The object store is the *bytes*; the log is the *time*. Together they give a market-surveillance authority answering an Article 74 request everything they need to see: the artefact at digest `D` existed under the program's control by time `T`, and its bytes are still exactly `D`.

## Indexing without breaking immutability

A content-addressed store is not queryable by human intent — you cannot ask "show me all eval records for model version `mistral-2026-04`" using only digests. The store solves this with a *separate*, mutable **index** that maps human-friendly attributes to digests. The index is:

- **Rebuildable from the store.** The store is the source of truth; the index is a derived view. If the index is lost, it is recomputable by walking objects and reading their `lineage` metadata.
- **Immutable-per-entry, but appendable overall.** Each index row is written once and never edited; a correction is a new row that supersedes an older one, with a link to the superseded row. In practice this is either an append-only table (Parquet in a "hive-partitioned" layout, or a BigQuery / Snowflake table with insert-only permissions) or an event log (Kafka topic with infinite retention).
- **Signed at rebuild.** When the index is rebuilt from the store, the rebuild emits a signed manifest tying the index version to the set of digests it covers.

Typical index shape (one row per eval record):

| Column               | Content                                                                           |
| -------------------- | --------------------------------------------------------------------------------- |
| `record_digest`      | `sha256:<hex>` — the eval record's own content address.                            |
| `model_digest`       | `sha256:<hex>` — the model artefact this record used.                              |
| `model_label`        | Human-friendly name and version — e.g., `internal-assistant/v2026-04-11`.          |
| `dataset_digest`     | The eval-set revision this record ran against.                                     |
| `dataset_label`      | Human-friendly name — e.g., `harm-eval-set/v3.2`.                                  |
| `evaluator_digest`   | The evaluator artefact.                                                            |
| `evaluator_family`   | e.g., `lm-evaluation-harness`, `inspect`, `internal-judge-eval`.                   |
| `judge_digest`       | The judge artefact digest, if LLM-as-judge; else `null`.                           |
| `decoding_digest`    | The decoding-config artefact.                                                      |
| `seed`               | Integer or `null`.                                                                 |
| `executed_at`        | RFC 3339.                                                                          |
| `platform`           | e.g., `phoenix` \| `langfuse` \| `weave` \| `vertex` \| `bedrock` \| `foundry` \| `inspect` \| `lm-eval` \| `internal`. |
| `producer_identity`  | The peer-track producer (mod-102 chapter `06`).                                    |
| `sacm_artifact_id`   | The SACM `Artifact.id` this record discharges, if any (mod-102 chapter `04`).       |
| `gate_criteria_id`   | The `GATE-…` criterion(s) this record binds to (mod-103 chapter `01`).             |
| `retention_class`    | `10y-eu-ai-act` / `7y-sec` / `standard` / `legal-hold`.                            |
| `index_version`      | The signed index-manifest version this row is part of.                             |

A reviewer answering "which release candidates used dataset `harm-eval-set/v3.2`?" queries the index. A reviewer answering "does the byte content at digest `D` still match?" ignores the index and re-hashes the object. The two operations are separable, which is what lets the index be rebuilt while the store stays untouched.

## Retention and legal hold

Retention is set by the *maximum* applicable regulatory requirement, with room for a margin. Concretely:

- **EU AI Act Article 18** — high-risk providers keep technical documentation for **ten years** after the last placement on the market of the AI system. The retention class the store applies to records that discharge Article 9–15 evidence is at least ten years.
- **EU AI Act Article 19 / Article 12** — automatically generated logs kept for a period appropriate to intended purpose; providers of high-risk systems retain them for at least six months unless otherwise specified.
- **SR 11-7 / OCC 2011-12** — model-risk records typically retained per the institution's model-inventory policy; seven years is the common practice for U.S. financial-services record-keeping tied to accounting-record schedules.
- **FDA GMLP / 21 CFR Part 820 (Quality System Regulation)** — device-record retention typically the life of the device plus two years, but not less than two years from the release date.

A **legal hold** is a mutable annotation on an *immutable* artefact — it never touches the artefact bytes, only the retention flag. The store implements legal hold by (a) refusing to expire the artefact while any hold is active, (b) recording the hold's imposition and release as their own append-only log entries, and (c) surfacing "in legal hold" in the index. When counsel says "hold everything tied to release candidate `rc-2026-05-07`," the release-cycle's DAG is walked and every node's `retention_class` field gets a hold row.

## Producer identity and write authority

Not every peer track writes into the same slice of the store. The pipeline authorises writes per producer:

- **AI-eval engineer** (level 30) writes eval records, trace bundles, judge-agreement reports, online-eval slices.
- **Model-evaluation engineer** (level 30) writes benchmark reports, calibration reports, subgroup-metric reports, cross-modality reports.
- **Risk engineer** (level 25) writes harm-inventory revisions, red-team engagement reports, guardrail-eval reports, incident-derived learnings.
- **Ai-infra-security** (level 35) writes eval-set integrity attestations, judge-supply-chain attestations, cybersecurity-posture attestations (chapter `05`).
- **AI-governance analyst** (level 15) writes intake / inventory rows, first-draft cards, jurisdictional-crosswalk revisions.
- **Third-party evaluator** (mod-109) writes signed independent-evaluation reports.

Each producer signs its writes with its own key (chapter `06`), and the store records the producer identity on every write. The release-gate walker cross-checks producer identity against the evidence-contract routing (mod-102 chapter `06`) and rejects a record whose producer does not match the expected owner peer track for the SACM `Artifact` the record discharges. A model-eval report signed only by the AI-eval producer is *not* a model-eval report; it is a mis-routed artefact and is an audit finding.

## What the store does *not* do

It is worth naming three things the store is not, because release-assurance programs routinely misplace them:

- **The store is not the metric.** It stores the eval record, not the aggregated dashboard number. The number is a *view* over the record set (mod-103 chapter `06`). Dashboards read the index; they do not overwrite the store.
- **The store is not the trace database.** Production traces (OpenTelemetry Gen-AI, OpenInference) usually live in the AI-eval peer's observability substrate — Phoenix, Langfuse, Weave — because volume is enormous and the write-path is real-time. What lands in the assurance store is a *pinned slice* of traces referenced by an eval record: the record cites which traces its scoring rests on, and either archives the trace bundle by digest, or cites the trace database's own content-addressed retention (chapter `02`).
- **The store is not the training-artefact registry.** Training runs, checkpoints in development, LoRA adapters not yet promoted — these live in an MLOps registry (MLflow, W&B, Vertex Model Registry, SageMaker Model Registry). The assurance store *addresses* a promoted model by its digest and pins the provenance chain (chapter `04`); it does not re-host every intermediate checkpoint.

Keeping these boundaries clean is what lets the store stay small enough to reason about and immutable enough to defend.

## A worked walk

Take a single release-gate criterion from mod-103 chapter `01` — a hard functional-adequacy criterion `GATE-FA-01`: "per-class F1 ≥ 0.85 (95% bootstrap CI lower bound ≥ 0.83) on `harm-eval-set/v3.2`."

At release time, the walker resolves the criterion's evidence pointer to a SACM `Artifact` (mod-102 chapter `04`). The `Artifact.id` maps into the store's index. The index row names:

- The eval record's digest: `sha256:74a1…`.
- The dataset digest: `sha256:9ff2…` — the store's node for `harm-eval-set/v3.2`.
- The evaluator digest: `sha256:012c…` — the internal `f1-bootstrap-v4` evaluator.
- The judge digest: `null` — this is a scored classifier task, no LLM judge.
- The decoding-config digest: `sha256:47da…` — greedy, `max_tokens=1`, no sampling.
- The seed: `42`.
- Producer: `model-evaluation-engineer` (level 30, ML Engineering).
- SACM Artifact: `art:eval-report:rc-2026-05-07:gate-fa-01`.
- Gate criterion: `GATE-FA-01`.

The walker fetches the record's bytes from the object store at `sha256:74a1…`, verifies the digest, verifies each lineage digest, and verifies the producer's signature over the whole. If any digest disagrees, the walker refuses the criterion and the gate fails (mod-103 chapter `05` picks up the rest). Six months later, a market-surveillance authority under EU AI Act Article 74 asks for the record. The store answers with the bytes, the digest, the seven upstream artefacts, the producer's signature, and the transparency-log inclusion proof — exactly the same view the walker saw.

## Summary

- The evidence pipeline is a *content-addressed, immutable substrate*. Editing an artefact changes its identifier; there is no in-place edit primitive.
- Every eval record binds seven lineage inputs: model, dataset, prompt (template and rendered), evaluator, judge (or `null`), decoding config, seed. The record's own identifier is a canonicalised digest that includes the lineage.
- The store is a Merkle DAG: any subtree is verifiable in isolation, and any tampering is detectable at the digest.
- On disk the store is dumb — an object store with write-once buckets, digest-shaped keys, object-lock retention, and a rebuildable index for human-friendly queries.
- Retention is set by the maximum applicable regulatory requirement (EU AI Act Article 18 gives the ten-year floor for high-risk providers) with legal-hold as a separate mutable flag.
- Producers write into the store under their own signatures; the walker rejects mis-routed evidence.
- The store is not the metric, not the trace database, and not the training-artefact registry. Keeping these boundaries clean is what makes it defensible.
- Chapter `02` picks up the *ingest* problem: how peer platforms (Phoenix, Langfuse, Weave, Inspect, lm-eval-harness, OTel Gen-AI, Vertex, Bedrock, Foundry) emit evidence and how the pipeline normalises it into this substrate.
