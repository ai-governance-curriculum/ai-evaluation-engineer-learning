# exercise-01: Content-Addressed Evidence Store

**Estimated effort:** 3 hours

## Objective

Design and implement a small, working **content-addressed evidence store** that ingests evaluation records, canonicalises them, computes digests over the seven lineage dimensions from chapter `01`, and exposes a rebuildable index by which a release-gate walker can resolve criteria to store artefacts. The store is the substrate every later exercise in this module builds on; getting the immutability and canonicalisation contracts right here saves rework in exercises `02`–`05`.

## Prerequisites

- Chapter [`01-content-addressed-evidence-store.md`](../01-content-addressed-evidence-store.md).
- Familiarity with any content-addressed system (Git objects, OCI images, IPFS) at the "what is a digest" level; deeper familiarity is a bonus but not required.
- A local scripting environment (Python 3.11+, or the language of your choice — the exercise is language-agnostic).
- Optional: an object store (a `minio` container or a real S3 bucket you can write to); the exercise can equivalently run against a local filesystem in `objects/sha256/…/` shape.

## Problem statement

Build a small store — call it `assurance-store` — that accepts eval records shaped by chapter `01`'s schema, canonicalises them, computes the record's own digest, verifies each of the seven lineage-input digests, writes the record to the store's object layer as *write-once*, and appends a row to the store's index. Then build a small query tool that answers three questions against the index without touching the store's byte layer:

- "Show me every eval record for dataset `harm-eval-set/v3.2`."
- "Given eval-record digest `sha256:…`, show me the seven upstream artefacts."
- "Show me every eval record whose evaluator family is `lm-evaluation-harness`."

## Requirements

Produce five artefacts.

### 1. `canonicalisation-v1.md`

A written specification for canonicalising every artefact class the store accepts:

- **`eval-record`** (JSON) — RFC 8785 JSON Canonicalization Scheme (JCS), or a documented equivalent (sorted keys, no trailing whitespace, LF newlines, UTF-8 without BOM, no significant floats beyond a documented precision). Fix the precision explicitly.
- **`prompt-template`**, **`prompt-render`**, **`decoding-config`** — the JSON form of each; same JCS rule.
- **`dataset-snapshot`** (JSONL) — line-canonical (one JSON object per line, each line JCS-canonicalised, LF newline separators, no trailing newline). If you also support tabular data, pin the Parquet writer options (compression, page size, column order) or the CSV dialect.
- **`evaluator-manifest`** and **`judge-manifest`** — JSON, JCS.
- **Prohibited fields.** List which fields the store rejects at ingest (e.g., a `timestamp` field on the artefact itself, which would prevent deduplication; a `producer_notes` field whose content is inherently non-canonical).

Version the doc as `canonicalisation-v1`. The store refuses records whose canonicalisation-version tag disagrees.

### 2. `store/` — the implementation

A small module or package that:

- Exposes an `ingest(record: dict, artefact_refs: dict) -> str` function that (a) canonicalises the record, (b) computes its `sha256` digest, (c) verifies each lineage digest resolves in the store, (d) writes the canonical bytes as write-once (refuse overwrites), and (e) returns the digest.
- Persists to `objects/sha256/<2-hex>/<2-hex>/<40-hex>/payload.json` (or an equivalent object-store key layout).
- Persists a `media-type` sidecar (single line, e.g., `application/vnd.assurance.eval-record+json;v=1`) alongside `payload.json`.
- Refuses to overwrite an existing object. Refuses to accept a lineage-input digest whose bytes are not present in the store (chicken-and-egg is solved by ingesting the inputs first; document the ingest ordering).
- Emits a producer signature over the canonical bytes. For this exercise you may use a locally-generated Ed25519 key (chapter `06`'s Fulcio + Rekor layering is out of scope here; use it as a stretch goal).
- Refuses a record whose declared producer identity does not appear in a small `producers.yaml` (a fixture you seed for the exercise).

You may implement in any language. Keep the module small (< 500 lines is easy for this scope).

### 3. `index/` — the rebuildable index

A separate module (or a set of scripts) that:

- Walks the object layer, reads each record's `payload.json`, and produces an append-only index (Parquet, SQLite, DuckDB, JSONL — pick one). One row per eval record.
- Rows carry the columns from chapter `01`'s indexing schema: `record_digest`, `model_digest`, `model_label`, `dataset_digest`, `dataset_label`, `evaluator_digest`, `evaluator_family`, `judge_digest`, `decoding_digest`, `seed`, `executed_at`, `platform`, `producer_identity`, `sacm_artifact_id`, `gate_criteria_id`, `retention_class`, `index_version`.
- Emits a signed `index-manifest.json` at the end of the rebuild, naming every record digest it observed and the index version. The signature is over the canonicalised manifest.

### 4. `query/` — the three queries

Three small scripts (or three subcommands of one CLI) that use the index to answer the questions above. The queries must operate on the index only and must not open any file under `objects/`.

### 5. `verify/` — the byte-layer verification

One small script that:

- Given an eval-record digest, fetches the bytes, re-canonicalises, re-hashes, and asserts equality against the requested digest.
- Given a record, walks its `lineage` fields, fetches each upstream artefact, re-hashes it against the recorded digest.
- Returns a machine-readable report (pass / fail per node).

## Starter guidance

- **Do the canonicalisation spec first.** If you write the code first and the canonicalisation later, you will discover that "obvious" JSON serialisation disagrees between libraries about float precision, key ordering, and whitespace. The spec (artefact 1) is what forces the disagreement into the open.
- **Start with a single artefact class.** Build ingest / verify for `eval-record` end-to-end before adding `prompt-template`, `evaluator-manifest`, etc. Getting one artefact right is worth more than getting five artefacts half-right.
- **Do not implement `datetime.now()` inside canonicalisation.** The record carries its `executed_at` from the input; the store never re-stamps. Any per-run non-determinism inside the store will break every downstream digest test.
- **Refuse overwrites loudly.** Log a clear error, do not silently succeed, and do not "helpfully" merge. Chapter `01`'s immutability contract is the whole point of the store.
- **`retention_class` is metadata, not policy enforcement.** For this exercise, record the class on the index row; do not implement bucket-level object-lock or retention holds. Note the stretch goal below if you want to.
- **Keep the producers.yaml small.** Two or three producers (e.g., `model-evaluation-engineer`, `ai-eval-engineer`, `ai-infra-security`) each with a single public key is enough. Peer-track routing (mod-102 chapter `06`) is contested territory the exercise flags without solving.
- **Seed the store with at least 10 records** across at least 3 model versions, 2 datasets, and 3 evaluator families. The queries are un-instructive against a single record.

## Acceptance criteria

You have succeeded if:

- `canonicalisation-v1.md` is versioned, covers every artefact class you support, and pins float precision, key ordering, whitespace, and newlines explicitly.
- `store/` refuses (a) overwrites, (b) missing-lineage-digest records, (c) records whose declared producer identity is not in `producers.yaml`.
- `index/` can be rebuilt from `objects/` alone with no loss; the rebuilt index matches the previous version's records exactly (byte-diff the two index files or diff the record-digest set).
- The three queries return correct results against a seeded corpus of at least 10 records.
- `verify/` returns byte-exact pass on unmodified records and byte-exact fail on any record you tamper with (test by editing one byte inside `payload.json`; verify catches it).
- Every write is signed by the producer's key; a record whose signature does not verify is rejected at ingest.
- A peer reading the four modules can identify where the immutability guarantee lives (which line refuses overwrites), where the canonicalisation is applied (which function normalises before hashing), and how the index would be rebuilt if lost.

## Stretch goals

- **Sigstore-style signing.** Replace the local Ed25519 signature with a keyless flow via Sigstore (`cosign sign-blob`) and record the Rekor log index on each record. This foreshadows chapter `06`'s Layer 5.
- **Object-lock retention.** Point `store/` at a real S3 (or MinIO) bucket with Object Lock in Compliance mode; set a 30-day retention as a rehearsal for the EU AI Act Article 18 ten-year floor from chapter `01`. Document the difference between per-object retention and per-bucket retention.
- **Cross-adapter cross-check.** Ingest the same logical eval from two adapters (foreshadow exercise `02`), assert the lineage tuples are identical, and flag divergence as an audit finding.
- **Legal-hold flag.** Add a mutable legal-hold annotation stored as a separate append-only log entry (not on the artefact itself). Demonstrate that placing a hold blocks expiry without touching the artefact bytes.
- **Merkle-diff between release cycles.** Given two release-candidate identifiers, compute the set of changed digests between their evidence sub-trees and produce a human-readable diff. This foreshadows mod-102 chapter `04`'s SACM diff.
