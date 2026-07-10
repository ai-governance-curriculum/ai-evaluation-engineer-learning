# Consuming and Normalising Peer-Platform Evidence

## Motivation

The release-assurance program does not run its own evaluations. It reads evidence produced by peer tracks (mod-101 chapter `06`, mod-102 chapter `06`, mod-103 chapter `04`) and by external systems those peer tracks operate. In 2026 the fragmentation of that upstream is real: the AI-eval engineer instruments with OpenTelemetry Gen-AI semantic conventions and OpenInference under a Phoenix, Langfuse, or W&B Weave observability layer; the model-eval engineer runs `lm-evaluation-harness` and Inspect; the risk engineer runs adversarial harnesses whose output shape follows its own conventions; the platform engineer sits on a hyperscaler-provided evaluation service — Vertex AI Gen AI Evaluation, Amazon Bedrock Model Evaluation, or Azure AI Foundry Evaluation. Every one of these emits a *slightly* different record shape.

Two release-assurance failure modes come from letting the shape drift into the assurance case.

The first is **format drift**: an assurance-case leaf cites `eval-report-v1.2` but nobody has written down what a v1.2 report contains. Two release cycles later a field has silently changed meaning, an auditor cannot answer basic questions ("what does `pass_rate` mean here — sample-level, class-level, or class-mean?"), and the leaf's warrant is a footnote to memory. Under NIST AI RMF MEASURE-2.13 (effectiveness of measurement) a metric whose definition floats is not a measurement.

The second is **producer-side lock-in**: the pipeline reads Phoenix natively, so every eval record has to be produced through Phoenix, so the AI-eval peer track cannot change platforms without breaking the case. This inverts the ownership: the release-assurance program starts *dictating* peer-track tooling instead of consuming its evidence. The deferral contract (mod-101) collapses.

The pipeline avoids both by putting a **thin, versioned normalisation layer** between the peer platforms and the store. The layer's contract is single-directional: it accepts the platform's *own* emitted shape, canonicalises into an assurance-store record (chapter `01`), and refuses records it cannot bind to the seven lineage dimensions. This chapter draws that layer.

## The normalisation contract

Concretely, for each peer platform the pipeline supports, the assurance program owns three things:

1. A **producer-side capture spec** — what the AI-eval peer track (or the equivalent producer) has to emit for the pipeline to normalise it. The spec is versioned (`capture-spec-phoenix-v1.md`) and negotiated as part of the mod-102 chapter `06` evidence contract. It tells the producer which OpenTelemetry attributes, which OpenInference span kinds, or which Phoenix / Weave / Langfuse fields the pipeline reads.
2. A **normalisation adapter** — code that reads the platform's output and emits an assurance-store record shaped by the chapter `01` schema. The adapter is content-addressed itself; its digest is part of the eval record's provenance chain.
3. A **conformance test** — a fixture set (canonical inputs, canonical expected outputs) that the adapter is re-run against on every change. Adapters change; the conformance test is what keeps the change honest.

The store never accepts raw peer-platform output; it always accepts the adapter's canonical output. That is what lets the AI-eval peer swap Phoenix for Langfuse (or Weave for a bespoke observability slice) without touching the assurance case. The peer changes their platform; the release-assurance program writes or updates one adapter; the case's SACM `Artifact` references stay the same because the store's content-addressed schema stays the same.

## Coverage map — the ten upstream shapes worth naming

The learning objective names ten upstream shapes explicitly. It is worth walking each and pinning what the adapter has to lift out of it.

### OpenTelemetry Gen-AI semantic conventions

OpenTelemetry's Gen-AI semconv (published under `semconv/gen-ai/` on the OTel site) pins span attributes for LLM invocations: request model, response model, token counts, latencies, sampler parameters, tool calls. The adapter reads the OTLP spans emitted by any producer that instruments to this convention.

What the adapter lifts:

- The **model version** — `gen_ai.request.model` (or the response-side counterpart if the provider echoes a snapshot ID). Digest against the artefact registry entry the platform team keeps for that model tag, or against a provider-attested snapshot ID (chapter `04` for the supply-chain-side of vendor attestation).
- The **decoding-config bundle** — the sampler attributes: temperature, top-p, max tokens, stop sequences, seed if present. The adapter builds a canonical decoding-config object, hashes it, and stores that hash on the record.
- The **prompt-render digest** — the rendered per-example prompt bytes, hashed. The template digest is a separate artefact the producer emits alongside.
- The **trace identity** — trace-ID and span-IDs pin the record to a slice of the observability substrate; the adapter records them as identity, not as evidence.

<!-- needs-research: the exact attribute names in OpenTelemetry Gen-AI semconv are still moving under the `otel-genai` working group — before pinning `gen_ai.request.model` vs `gen_ai.request.model.id` in a program's capture spec, check the current published version at opentelemetry.io/docs/specs/semconv/gen-ai/. -->

### OpenInference

OpenInference (Arize's vendor-neutral instrumentation library) defines span kinds for LLM, embedding, retrieval, tool, agent, chain, reranker, and evaluation spans. It layers on top of OTLP and adds the semantic categories the OTel Gen-AI attributes do not natively express.

What the adapter lifts:

- The **span kind** — e.g., `EVALUATION` for an evaluator's own execution, `LLM` for the invocation under evaluation, `RETRIEVER` for a RAG grounding step. Span kind determines which lineage dimensions the record binds to.
- The **input / output payloads** — canonicalised, hashed, and stored. If the payload is large, the adapter stores it as its own store node and puts only the digest in the record.
- The **evaluator relationship** — an `EVALUATION` span points at the `LLM` span it evaluates. The adapter turns that pointer into a lineage edge in the record's DAG.

### Arize Phoenix

Phoenix persists OpenInference spans and exposes them via a queryable trace store. In practice the release-assurance program treats Phoenix as the *observability substrate* the AI-eval peer runs; the adapter reads spans through Phoenix's API (or from an export bundle) and produces store records.

What the adapter lifts:

- **Datasets and experiments** — Phoenix's `Dataset` / `Experiment` objects carry a stable identity that the adapter maps to the assurance store's `dataset` and `eval-run` artefacts.
- **Evaluations** — Phoenix's `evaluations` (LLM-as-judge, code, classification, hallucination heuristics) each become an `EVALUATION` span; the adapter binds the evaluator digest per evaluator family.
- **Annotations** — human-in-the-loop labels the peer track collected; the adapter carries them into the record but marks them with the annotator identity, not as machine-produced.

### Langfuse

Langfuse organises evidence as traces containing observations (spans, generations, events), scores, and datasets. Scores are the atomic evidence unit; a trace can carry many scores from different evaluators.

What the adapter lifts:

- **Generations** — each generation carries model, prompt, decoding config, and completion. These map 1:1 to lineage fields.
- **Scores** — each score has a `name`, a `value`, a `dataType` (numeric / categorical / boolean), a `source` (API / annotation / eval), and a `comment` field. The adapter binds `source` to the producer identity (chapter `01`).
- **Datasets and dataset items** — the eval-set slice a score was computed against. The adapter binds the dataset revision to the record's `dataset` lineage field.

### W&B Weave

Weave is Weights & Biases' LLM-focused tracing and evaluation surface. It ships an `Evaluation` primitive that binds a dataset, a model, and one or more scorers, and it produces `EvaluationResults` objects that carry per-example scores and aggregates.

What the adapter lifts:

- The **`Evaluation` binding** — model, dataset, scorers — maps directly to the seven lineage dimensions minus the seed and decoding config, which come from the `Model` object's `predict` config.
- The **`EvaluationResults`** — per-example score payload, aggregated per scorer. The adapter emits one store record per (example, scorer) or one per aggregate depending on the program's granularity contract (which is written into the capture spec).
- The **`Object` versioning** — Weave's object graph is versioned; the adapter records the Weave object versions and cross-checks them against the digests it computes independently.

### Inspect (UK AISI evaluation framework)

Inspect (`inspect.aisi.org.uk`) is the UK AI Safety Institute's evaluation framework. Its unit of evidence is the **eval log** — a JSON file per eval run containing task metadata, per-sample messages, tool calls, judge outputs, scores, and the run's configuration.

What the adapter lifts:

- **Task and dataset identity** — Inspect's `task` decorator names the task; the adapter binds the task's version and its dataset to store artefacts.
- **Solver / scorer** — the evaluator lineage; solver is the model-side program and scorer is the evaluator-side program. Both are digested.
- **Model config** — provider, model ID, decoding config; the adapter builds the canonical decoding-config artefact from this.
- **Sample-level messages and tool calls** — canonicalised and stored; large runs are stored as chunked artefacts referenced by the record.

Inspect logs are already close to the store's target shape — they carry lineage explicitly — which makes the Inspect adapter one of the simplest.

### EleutherAI `lm-evaluation-harness`

`lm-evaluation-harness` produces a `results.json` per run with task-by-task aggregate metrics, the model tag, the prompt version, few-shot count, seed, and a subset of decoding parameters. It also emits per-example logs under `--log_samples`.

What the adapter lifts:

- **Task / version / prompt** — `results.json` names the task id and version, and the harness's internal prompt version; the adapter binds the harness's task registry and the version to a dataset+prompt-template digest.
- **Model tag and provider** — the harness records the model as invoked (e.g., a Hugging Face repo id, a hosted-provider tag); the adapter resolves it to a model digest via the supply-chain layer (chapter `04`).
- **Aggregate metrics with stderr** — the harness computes bootstrap standard errors for many tasks; the adapter records the point estimate, the standard error, and the estimator name.
- **Per-sample logs** — under `--log_samples` the harness emits per-example inputs, targets, and model outputs; the adapter chunks and hashes these as their own artefacts.

### Vertex AI Gen AI Evaluation

Google Cloud's Vertex AI Gen AI Evaluation Service (part of Vertex AI Studio) runs pointwise and pairwise autoraters against user-supplied datasets, exposes computation-based metrics, and returns a structured evaluation result including per-example scores, rationales, and aggregate summaries.

What the adapter lifts:

- The **evaluation task configuration** — the metric family (e.g., pointwise autorater vs. pairwise, or a rubric), the autorater model identity, the dataset upload identity.
- The **per-example score** — score, rationale, and any autorater intermediate output.
- The **aggregate** — mean, per-slice breakdown, autorater confidence.

<!-- needs-research: Vertex Gen AI Evaluation exposes both a Python client (`vertexai.evaluation.EvalTask`) and REST endpoints; the exact field names for autorater output shape (e.g., `metric_results` vs `results`) shift between SDK minor versions — check the current SDK version pinned in the peer track's capture spec before writing the adapter. -->

### Amazon Bedrock Model Evaluation

Bedrock Model Evaluation runs automatic evaluations (built-in and custom) and human evaluations against Bedrock models. Automatic jobs produce a JSON results file in S3 with per-metric aggregates and per-record scoring; human jobs produce reviewer-tagged records.

What the adapter lifts:

- **Job configuration** — model, evaluation type (automatic / human), dataset ARN, task type (text summarisation, Q&A, classification, or custom).
- **Per-record scoring** — per-record inputs, model output, metric score.
- **Aggregate metrics** — per-metric summary, plus reviewer inter-annotator agreement for human jobs.

### Azure AI Foundry Evaluation

Azure AI Foundry Evaluation (evolved from Azure AI Studio's evaluation service) ships built-in evaluators (relevance, groundedness, coherence, fluency, safety), a custom-evaluator SDK, and an evaluation-results object persisted in the Foundry workspace. The `azure-ai-evaluation` Python SDK provides the local runner.

What the adapter lifts:

- **Evaluator identity** — built-in evaluator names (e.g., `RelevanceEvaluator`, `GroundednessEvaluator`, `ProtectedMaterialEvaluator`, `IndirectAttackEvaluator`) or the custom-evaluator's signature.
- **Per-example inputs and outputs** — the dataset row, the target model's response, and the evaluator's score.
- **Aggregate** — per-evaluator mean, per-safety-category breakdown for the safety evaluators.

<!-- needs-research: the Foundry safety evaluators include content-safety, protected-material, indirect-attack, and code-vulnerability categories in the currently published `azure-ai-evaluation` SDK — before pinning a capture spec, confirm the current evaluator set at learn.microsoft.com/azure/ai-foundry/how-to/develop/evaluate-sdk. -->

## The adapter shape

Adapters are small, single-purpose, and stateless. A reasonable interface:

```python
class Adapter(Protocol):
    NAME: str        # e.g. "phoenix", "langfuse", "weave", "inspect", ...
    VERSION: str     # semver — pinned into the record's provenance chain

    def can_handle(self, source: Source) -> bool: ...

    def normalise(
        self,
        source: Source,
        capture_spec: CaptureSpec,      # peer-negotiated (mod-102 ch 6)
        canonicalisation: CanonSpec,    # store-wide canonicalisation rule
    ) -> Iterable[EvalRecord]:
        """
        Read peer-platform output; return canonicalised EvalRecord objects,
        each with `lineage` populated and the adapter's own digest recorded
        under record.context.adapter.
        """
```

Adapters are content-addressed themselves — the record's `context.adapter` field is `{ name, version, digest: sha256:... }`, so a re-normalisation with a fixed adapter produces a *new* record with a new digest, and the old record stays where it is. This is the same immutability contract chapter `01` draws for evidence records: adapter changes never rewrite the past.

Two things adapters do not do:

- **Interpret the metric.** An adapter reads `pass_rate: 0.86` and writes `pass_rate: 0.86`. It does not decide whether that number is above threshold — the release-gate walker does (mod-103 chapter `06`). Adapters that start "clean up" data are a source of silent breakage.
- **Fabricate lineage.** If the source is missing a lineage input, the adapter records the input as `null` with an explicit `missing_reason`. It does not synthesise a placeholder. A record with `null` model digest is a record the release-gate walker will surface at approval time; a record with a fabricated placeholder will look valid and pass the walker silently.

## The capture spec — what the producer has to emit

The capture spec is a plain-language document, versioned and part of the mod-102 chapter `06` evidence contract. Its function is to make the producer-side effort explicit so the release-assurance program is not silently expanding its ownership into peer-track platform choices.

A capture spec has these sections:

1. **Producer surface** — which platform (e.g., "Phoenix v6.0.x"), which SDK version (e.g., `arize-phoenix-client >= 4.0`), which OTel semconv version (`gen-ai/v1.29.0` or whatever the program pins).
2. **Required span attributes / fields** — the exact keys the adapter reads. Example: `gen_ai.request.model`, `gen_ai.request.temperature`, `gen_ai.usage.input_tokens`, `openinference.span.kind`.
3. **Optional-but-recommended fields** — fields whose absence does not block ingest but reduces evidence quality (e.g., the response's `system_fingerprint` where available; the tool schema when a tool was called).
4. **Prohibited fields** — fields the producer must *not* emit into the assurance-store record. Example: user-identifying content that would violate the data-minimisation clause; internal-only debug flags whose semantics change frequently.
5. **Canonicalisation** — pointer to the store-wide canonicalisation-vN spec.
6. **Freshness and cadence** — how quickly evidence has to be ingested after the run finishes (typically bounded by the release-gate freshness rule from mod-102 chapter `06`).
7. **Failure protocol** — what happens if a required field is missing. Usually: adapter records `null` with `missing_reason`, the record ingests, and the SACM `Artifact` element is flagged so the walker treats the criterion as unresolved.

The capture spec is signed by the peer-track lead and by the release-assurance program lead. Both parties know what they owe.

## Conformance testing

Adapters break when the peer platform changes. The way to catch the break early is to run a **conformance test** on every adapter change:

- **Golden fixtures.** For each peer platform, keep a small set of canonical inputs — a Phoenix export bundle, a Langfuse trace dump, an Inspect eval-log JSON, an `lm-evaluation-harness` `results.json` — and their canonical expected outputs (the assurance-store record bytes the adapter should produce). Store both in the repo, address them by digest.
- **Byte-exact assertions.** The test hashes the adapter's output and asserts equality against the golden. Byte drift is the fault; the test does not attempt to be "clever" about diffs.
- **Round-trip check.** Where the peer platform's identity is stable enough, re-hash the fixture and confirm the identity is stable across re-normalisation.
- **Cross-adapter invariants.** For records that could be produced by two adapters (e.g., an Inspect eval and an `lm-eval` run of the same task on the same model), assert the *lineage tuple* is identical, even if the record shape differs in peripheral fields. Cross-adapter divergence in lineage is a red flag.

The conformance test suite is run in CI, and every adapter version tag ships with its passing suite pinned into the release-notes.

## What the pipeline emits into the store

At the end of the normalisation layer, one peer-platform event becomes one (or several) assurance-store nodes:

- One or more **eval-record** nodes (chapter `01` shape).
- Zero or more **prompt-template** nodes (if the template was not already in the store).
- Zero or more **prompt-render** nodes for per-example rendered prompts (or a canonical render function reference + template digest, depending on the program's granularity choice).
- Zero or more **evaluator** nodes (if the evaluator's code / config artefact was not already in the store).
- Zero or more **judge** nodes for LLM-as-judge configurations (if the judge is new).
- Zero or more **decoding-config** nodes (if the exact sampler config was not already there).
- Zero or more **trace-bundle** nodes for archived trace slices the record cites.

The index (chapter `01`) is updated to point at the new nodes. Every write is signed by the adapter's producer identity and by the peer-track producer's key.

## When the adapter has to reject

Adapters reject records; they do not paper over drift. Reject when:

- A required lineage input is *not* `null`-marked but is unresolvable (e.g., the model tag references a snapshot the artefact registry does not know; the dataset ID does not resolve to a store artefact).
- The canonicalisation-version tag on the source disagrees with the store's current canonicalisation rule, *and* the mismatch is not one the program's rewrite policy declares safe.
- The producer identity on the source does not match the peer-track expected owner (mod-102 chapter `06`).
- The source's schema version is a version the adapter does not know (introduced upstream after the adapter's release).

Rejections are logged into a dead-letter store (with the same immutability and retention as the main store — an audit-visible rejection is itself evidence), and the peer track is notified per the mod-102 chapter `06` escalation path.

## A worked cross-platform record

Take one eval — an offline safety-benchmark run of an internal model on `harm-eval-set/v3.2`, executed under Inspect but instrumented via OpenInference for cross-check into Phoenix.

Inspect emits an eval log. OpenInference emits spans into Phoenix. The pipeline runs both adapters:

- The **Inspect adapter** reads the eval log, resolves the model tag `internal-assistant/v2026-04-11` to model digest `sha256:aa11…`, resolves the dataset to `sha256:9ff2…`, hashes the solver/scorer to `sha256:012c…`, canonicalises the decoding config to `sha256:47da…`, and emits eval-record `sha256:74a1…`.
- The **Phoenix adapter** reads the OpenInference spans for the same run, produces its own eval-record `sha256:74b3…` with the same lineage but slightly different trace-bundle context (Phoenix carries the trace-ID and span-timeline; Inspect carries the eval-log).

Both records point at the same seven lineage digests. Both records point at each other via a `cross_reference` field (`cross_reference.adapter=inspect, cross_reference.digest=sha256:74a1…` on the Phoenix record; symmetric on the Inspect record). A release-gate walker resolving the criterion picks one record as the primary evidence and cross-checks the second. If the two lineage tuples disagreed, the walker would surface the disagreement at approval time — a class of finding the case's mod-102 chapter `05` diversity-of-evidence audit lives to catch.

## Summary

- The pipeline puts a thin, versioned normalisation layer between peer platforms and the store; the store never sees raw peer-platform output.
- For each supported platform (OpenTelemetry Gen-AI, OpenInference, Phoenix, Langfuse, Weave, Inspect, `lm-evaluation-harness`, Vertex AI Gen AI Evaluation, Amazon Bedrock Model Evaluation, Azure AI Foundry Evaluation), the program owns three artefacts: capture spec, adapter, conformance test.
- Adapters lift the seven lineage dimensions and the results payload out of the source; they do not interpret metrics and they do not fabricate missing lineage.
- Capture specs are signed as part of the mod-102 chapter `06` evidence contract and pin the producer's obligations without dictating the peer's tooling choice.
- Conformance tests hash adapter output byte-exactly against golden fixtures; cross-adapter runs of the same task assert lineage-tuple equality.
- Rejections are audit-visible, land in a dead-letter store, and escalate through the peer-track contract.
- Chapter `03` picks up the *output* of the store: how a reproducibility bundle is assembled from a set of store nodes so a third-party evaluator can rerun the case end-to-end.
