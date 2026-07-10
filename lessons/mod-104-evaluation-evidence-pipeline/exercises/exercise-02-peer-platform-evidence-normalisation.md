# exercise-02: Peer-Platform Evidence Normalisation

**Estimated effort:** 3 hours

## Objective

Author a **normalisation layer** that reads evaluation output from at least three peer platforms — chosen from Arize Phoenix, Langfuse, W&B Weave, OpenTelemetry Gen-AI, OpenInference, Inspect, `lm-evaluation-harness`, Vertex AI Gen AI Evaluation, Amazon Bedrock Model Evaluation, and Azure AI Foundry Evaluation — and emits canonical assurance-store records shaped by chapter `01`. Reject rather than paper over drift: the adapter's job is to lift lineage cleanly, not to interpret metrics or fabricate missing inputs.

## Prerequisites

- Chapter [`02-peer-platform-evidence-normalisation.md`](../02-peer-platform-evidence-normalisation.md).
- Exercise `01` completed (or a stub store you can write to that respects the same canonicalisation rules).
- The three peer platforms you pick have public schema documentation (all ten listed above do); read the schema at least once before starting.
- Optional: `docker` / `podman` to run Phoenix, Langfuse, or Inspect locally against a toy model; alternately, use fixture JSON captured from a public run.

## Problem statement

Pick three peer platforms (at least one of which must be a *hosted*-evaluator service — Vertex, Bedrock, Foundry — and at least one of which must be an *offline*-harness — Inspect or `lm-evaluation-harness`). For each of the three, produce a capture spec, an adapter, and a conformance test. Then run a small demonstration where the *same* logical eval (a fixed model, fixed dataset, fixed evaluator target) is normalised through two of your adapters and the resulting store records are cross-checked for lineage-tuple equality.

The point is to feel three things: (i) how much the peer-platform schemas actually differ, (ii) how much of that difference has to be pushed into the *capture spec* rather than the *adapter*, and (iii) how a conformance test catches upstream drift before it lands in the release-gate.

## Requirements

Produce three artefacts per platform (nine total) plus one cross-adapter check.

### For each of the three platforms:

#### A. Capture spec (`capture-spec-<platform>-v1.md`)

The producer-side contract per chapter `02`. Sections:

1. **Producer surface.** Which platform, which SDK version, which OpenTelemetry semconv version (where relevant), which peer-track producer identity signs the emitted evidence.
2. **Required fields.** The exact schema keys the adapter reads (e.g., `gen_ai.request.model`, `openinference.span.kind`, Langfuse `generations[*].model`, Inspect `EvalSample.output.model`). Cite each with a link to the platform's schema documentation (in a comment if you keep everything local).
3. **Optional-but-recommended fields.** Fields whose absence does not block ingest but lowers evidence quality.
4. **Prohibited fields.** Fields the producer must not emit into the store (user-identifying content, internal debug flags with unstable semantics).
5. **Canonicalisation.** Pointer to your `canonicalisation-v1.md` from exercise `01`.
6. **Freshness and cadence.** How quickly emitted evidence must reach the store; foreshadows the release-gate freshness rule.
7. **Failure protocol.** What the adapter does when a required field is missing — record `null` with `missing_reason`, ingest, and flag; do not synthesise a placeholder.

Each capture spec is signed by both the peer-track producer (simulated for the exercise — a role in `producers.yaml`) and the release-assurance program lead.

#### B. Adapter (`adapters/<platform>.py` or equivalent)

A small, stateless module that:

- Takes the platform's *own* emitted output — a Phoenix export bundle, a Langfuse `traces` export, an Inspect `.eval` log, a `lm-evaluation-harness` `results.json` + `--log_samples` directory, a Vertex `EvaluationResult` proto/JSON, a Bedrock evaluation job's S3 output, or an Azure AI Foundry evaluation-results object — and produces canonical `eval-record` objects per exercise `01`'s schema.
- Populates `lineage.*` fields from the source; explicitly records `null` with `missing_reason` when a lineage input cannot be resolved.
- Records the adapter's own `name`, `version`, and `digest` on `context.adapter`.
- Emits **one record per logical evaluation unit** (typically per-example × per-scorer; document your chosen granularity in the capture spec).
- Refuses to run when the source's schema version disagrees with the capture spec.

The adapter never interprets metrics — it lifts them verbatim. The adapter never derives pass/fail — the release-gate walker does.

#### C. Conformance test (`conformance/<platform>/`)

- A small golden-fixture directory. At least one input fixture (an exported bundle or JSON), and the expected canonical output bytes.
- A test that (i) runs the adapter over the input, (ii) canonicalises the output, (iii) computes the digest, (iv) asserts byte-exact equality against the golden.
- A negative test: mutate the input (drop a required field, drift a value) and assert the adapter either records a `null` with `missing_reason` or refuses cleanly (not both — decide once and document).

### Cross-adapter check (`cross-check.py` or equivalent)

Pick two of your three adapters that could produce the same logical eval — for example, `lm-evaluation-harness` and Inspect running the same task on the same model. Run both, normalise both, and assert:

- The two records point at *the same seven lineage digests* (model, dataset, prompt-template, prompt-render, evaluator, judge-or-null, decoding-config).
- The two records point at each other via a `cross_reference` field on each.
- If the two records disagree on any lineage digest, the cross-check produces an audit-finding-shape output for later review.

## Starter guidance

- **Do not start from the platform's SDK; start from the platform's schema.** The SDK will happily lift some fields silently and swallow others; the schema is the contract.
- **Pin the SDK version.** Even the maturely-versioned platforms (Phoenix, Langfuse, Inspect, `lm-eval-harness`) ship breaking changes at minor-version boundaries; the capture spec should name the tested version.
- **Prefer fixtures over live runs.** For a first pass, capture a run once, save the raw output, and iterate against it. Live runs invite non-determinism into a canonicalisation exercise.
- **The Vertex / Bedrock / Foundry adapters are shape-only for the exercise.** You do not need to run against the live cloud; a canonical example output pulled from the provider's documentation (or a small handwritten fixture that faithfully mirrors the documented shape) is enough. Note the exercise's scope limit in the capture spec.
- **`null` beats `missing`.** A record with `lineage.judge = null, missing_reason = "no judge in this eval"` is honest and the walker knows how to treat it. A record missing the `lineage.judge` key entirely is ambiguous — is it not applicable, or is it a bug?
- **Do not "clean up" data in the adapter.** Empty strings stay empty; floats stay at whatever precision the source emitted (canonicalisation later normalises within the store's precision rule); locale-specific serialisations get normalised, but content does not.
- **Watch for hidden statefulness.** Adapters that touch a database, a cache, or a timestamp during normalisation are broken. The adapter is a pure function from `(source, capture_spec, canonicalisation)` to `records`.

## Acceptance criteria

You have succeeded if:

- Three capture specs are drafted, signed by both parties (in the fixture sense), and cite the platform's schema by URL or path.
- Three adapters exist, each < 300 lines of code, each stateless, each digest-stable across two runs of the same input.
- Nine conformance tests (one positive + two negatives per platform, or a superset thereof) pass byte-exactly.
- The cross-adapter check produces two eval-record digests whose `lineage` fields are identical for at least one shared eval.
- A peer reading the three adapters can identify (a) which line lifts each of the seven lineage dimensions, (b) which line records the adapter's own digest for provenance, and (c) which line refuses schema-version drift.
- The store's index (from exercise `01`) can be rebuilt including the new records without changes to the store's ingest code — i.e., the adapters' outputs are indistinguishable from any other producer's.

## Stretch goals

- **Round-trip a hosted evaluator.** Extend one of your Vertex / Bedrock / Foundry adapters to run against a real evaluation-service endpoint (a toy dataset, a cheap autorater) and demonstrate that a signed, canonical assurance-store record lands.
- **Trace-bundle attachment.** For the Phoenix or Weave adapter, capture the OpenInference span timeline for one eval example and archive it as a `trace-bundle` artefact in the store; reference it from the eval record's `context.trace_bundle` field.
- **Cassette-replay mode.** For an adapter that consumes a hosted-provider response, add a mode that reads a recorded response fixture instead of calling the provider live. This foreshadows the reproducibility-bundle cassette-replay from chapter `03`.
- **Schema-drift alert.** Add a small CI job that runs the three conformance tests on every push to the adapters and emits a red flag whenever a golden fixture has to be regenerated. Every regeneration is an event a mod-102 chapter `06` producer contract should have to acknowledge.
- **Fourth adapter.** Pick a fourth platform and repeat. Diminishing returns kick in fast; the exercise is instructive precisely because a fourth adapter forces you to notice which parts of the capture-spec / adapter / conformance shape are copy-paste and which are per-platform.
