# exercise-02: System Card Composition from Evidence Tree

**Estimated effort:** 3 hours

## Objective

Compose a **system card** for the scenario you chose in exercise `01`, following chapter `03`'s six-section structure and its worked-example discipline (OpenAI, Anthropic, Google, Meta system cards). The composition is a *view* over the evidence tree — model card (from exercise `01`) + dataset card(s) + evaluation-evidence bundle + safety-evidence summary + deployment-tier decision — stitched into one signed external artefact whose reviewer can walk any claim in six steps.

## Prerequisites

- Chapter [`03-system-card-composition-from-evidence-tree.md`](../03-system-card-composition-from-evidence-tree.md).
- Exercise [`exercise-01-model-card-for-a-regulated-product.md`](exercise-01-model-card-for-a-regulated-product.md) — this exercise reuses the model card and extends it.
- At least skim access to one public system card from OpenAI, Anthropic, Google Gemini, or Meta Llama (see [`resources.md`](../resources.md)). Read one end-to-end before starting.

## Problem statement

Extend exercise `01`'s model card into a system card. Add: dataset card(s) for the training, fine-tuning, and evaluation datasets referenced; an evaluation-evidence bundle description that points at the reproducibility bundle content-addresses; a safety-evidence summary that references the red-team methodology, the guardrail-eval results, and the residual-risk position; and a deployment-tier decision section that names the tier assigned and the operational constraints.

The system card is the artefact a regulator or notified body would receive. The public variant is what you author here; exercise `05` derives the four audience variants from the same canonical case.

## Requirements

Produce five artefacts.

### 1. `head.yaml` — extended

Extend the head from exercise `01`:

- `subject.kind: "system"` (was `"model"`).
- `subject.components[]` — every constituent artefact by ID and content-address: the base model (from exercise `01`), each dataset that materially shapes system behaviour, each eval-bundle used, each guardrail, each judge model if applicable.
- `evidence_pointers` — extended with entries for the safety-evidence summary claims, the eval-bundle claims, and the tier-decision claims. Each entry cites an `evidence_content_address` and a `sacm_artifact_id`.
- `regime.*` — the regulatory regime should not have changed from exercise `01`, but the `articles` / `clauses` covered will typically extend (safety-evidence discharges Article 15 cybersecurity; tier-decision discharges tier-appropriate operational constraints).

### 2. `body.md` — six sections

The full six-section system-card body, per chapter `03`:

- **§1 System identity and version.** Every constituent by name, version, and content-address; the release date; the system architecture at a high level (components, guardrails, retrieval index if any).
- **§2 Intended purpose, appropriate use, and out-of-scope use.** Extends the model-card intended-purpose section with system-level appropriate-use boundaries — deployment tiers permitted, jurisdictions, deployer categories.
- **§3 Training and evaluation data.** Datasheets for each dataset in `subject.components[]`. Where the training data has limited disclosure (typical for scenarios B and C in exercise `01`), name the disclosure category and cite the applicable regime.
- **§4 Quality attributes and evaluation evidence.** ISO/IEC 25059 spine per chapter `05`. Every quality-attribute row cites the eval report by content-address and the reproducibility bundle by content-address. At least six quality-attribute rows across at least four ISO/IEC 25059 characteristics.
- **§5 Safety-evidence summary and residual risk.** Red-team methodology at category level, guardrail-eval results with rates and thresholds, dangerous-capability evaluation results if in scope, residual-risk position (a narrative bounded by a scoring frame). Attack payloads are redacted from the public variant; the redaction is noted (this feeds into exercise `05`'s redaction manifest).
- **§6 Deployment-tier decision.** For a frontier system, the tier per RSP / Preparedness / FSF. For a non-frontier system, the deployment-mode decision (staff-only / controlled-deployer-set / general-availability) and rationale.

Length: 30–60 pages equivalent when rendered. Every claim in every section has an `evidence_pointers` entry in the head.

### 3. `evidence-tree.md`

A single-file summary of the evidence tree that the system card is a view over. Format: a directed list showing each `evidence_pointers` entry in the head and what upstream artefacts each cites. Example rows:

```
sha256:74a1... (eval-report:gate-fa-01)
  ├── lineage.dataset            → sha256:012c...
  ├── lineage.evaluator          → sha256:beef...
  ├── lineage.judge              → null (classifier task)
  ├── lineage.decoding_config    → sha256:47da...
  ├── lineage.seed               → 42
  └── producer                    → model-evaluation-engineer

sha256:c33d... (redteam-report:gate-rb-02)
  ├── lineage.dataset            → sha256:4b12...
  ├── lineage.evaluator          → sha256:e00d...
  └── producer                    → ai-risk-engineer
```

The evidence tree should have at least ten evidence-node entries corresponding to the head's `evidence_pointers`. The point is to *see* the DAG — the tree the card is a projection of.

### 4. `worked-example-comparison.md`

A short comparison (2–4 pages) between your system card and a public system card from OpenAI, Anthropic, Google Gemini, or Meta Llama:

- What sections match (identity, intended purpose, safety-evidence summary, tier decision)?
- What sections your card adds that the public card does not (evidence-pointer bindings, `sacm_artifact_id` discipline, machine-readable head)?
- What sections the public card carries that yours does not — and why (e.g., a headline capability-benchmark leaderboard is a marketing choice; the assurance card cites the benchmark by content-address in §4 but does not headline)?

Reference the public card explicitly with a URL from [`resources.md`](../resources.md).

### 5. `signature-manifest.json` — extended

Signature over the extended canonicalised head + body pair. Rotate the signature manifest from exercise `01`; the same producer identity signs but the signed bytes are different (new content-address for the system-card artefact).

## Starter guidance

- **Reuse exercise `01`.** The system card *contains* the model card; do not re-author. The model card's §1 becomes a subsection of the system card's §1; the model card's §4 becomes part of the system card's §4 (subject-scoped).
- **Compose from the tree.** Chapter `03` said the system card is a view over the evidence tree; write `evidence-tree.md` *before* writing §5 and §6 of the body. If a claim you want to make on the body has no node on the tree, you know before you write it that the claim is undischarged.
- **Do not merge §4 and §5.** Quality attributes and safety evidence live in different sections. Chapter `03`'s anti-pattern list warned against merging them; a single table conflates thresholds (§4) with residual-risk narrative (§5).
- **Read one public system card end-to-end.** The [OpenAI GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf) or the [Claude 3 model card](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) are worth an hour each. You will produce a better artefact if you have seen one that ships to a real external audience.
- **Do not headline capability benchmarks.** A capability-benchmark leaderboard is a marketing choice. An assurance card cites the benchmarks in the ISO/IEC 25059 §4 spine, and cites them by content-address; the reader reaches the number through the spine, not from a headline table.
- **Tier decision is real, even for non-frontier systems.** Chapter `03` §6 said this. A non-frontier deployment still makes a decision (staff-only vs. general availability); the card writes that decision down and cites the evidence.
- **Safety-evidence summary respects the redaction rule from chapter `06`.** In the public variant, attack payloads are omitted; the omission is noted and the rate + taxonomy + trend are published. Save the specific attack-payload disclosure for the regulator / third-party variants in exercise `05`.

## Acceptance criteria

You have succeeded if:

- `head.yaml` is a valid extension of exercise `01`'s head; `subject.kind = "system"` and `subject.components[]` names every constituent by ID and content-address.
- `body.md` covers all six sections with the depth chapter `03` requires; §4 carries at least six quality-attribute rows across at least four ISO/IEC 25059 characteristics; §5 carries a residual-risk narrative bounded by a scoring frame; §6 names the tier / mode and its rationale.
- `evidence-tree.md` shows a DAG with at least ten nodes; every `evidence_pointers` entry in the head corresponds to a node in the tree; every node names its upstream lineage inputs and its producer identity.
- `worked-example-comparison.md` cites a real public system card by URL and enumerates matches, additions, and omissions with rationale.
- `signature-manifest.json` verifies against the canonicalised system-card artefact.
- A reviewer opening the body can walk any claim to (a) an `evidence_pointers` entry in the head, (b) a node in the evidence tree, (c) a producer identity, and (d) a case node — chapter `03`'s six-step audit walk succeeds for every claim.
- The card does not headline a capability benchmark; ISO/IEC 25059 §4 is the spine of the quality-attribute reporting.
- The card does not merge §4 and §5; safety evidence lives in §5 with its own redaction discipline.
- Public-variant redactions (attack payloads, PII in eval sets, canaries) are noted at the section where the redaction is applied; exercise `05` will make them explicit in the `redaction_manifest`.

## Stretch goals

- **Add a `provenance.c2pa` block for GenAI outputs.** If your chosen scenario has a GenAI-output surface (scenario A or a stretch of B), foreshadow exercise `04`: draft the `provenance.c2pa` block in the head and a §Provenance sub-section in the body. This is not the full C2PA manifest — that is exercise `04` — but it is the card-side interface.
- **Cross-reference impact-assessment findings from §5.** Chapter `04` said impact-assessment findings often serve as evidence for safety-evidence summary claims. Add cross-references from §5's safety-evidence rows to the specific `imp:IAI:F-…` finding IDs your (upcoming) impact-assessment section will carry. This foreshadows exercise `03`.
- **Author the safety-evidence summary against a taxonomy.** Bind every safety-evidence row to a specific row in a public taxonomy — [MITRE ATLAS](https://atlas.mitre.org/), the [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/), or an internal taxonomy — with the row cited by ID. This is what chapter `06`'s attack-payload disclosure discipline needs.
- **Compose a supplementary card for a fine-tuned variant.** Frontier labs ship system cards for base models and separate cards for major fine-tuned variants. Author a *supplementary* system card for a fine-tuned variant (e.g., a domain-adapted derivative) that inherits §1–3 from the base and re-authors §4–6 for the variant. Document the inheritance rule in the head.
- **Produce a rendered PDF.** Author the body in a format that renders to PDF (Pandoc, Sphinx, Typst); include the canonicalised head as an appendix. A rendered artefact is what the regulator actually receives.
