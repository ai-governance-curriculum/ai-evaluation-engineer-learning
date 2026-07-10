# Composing a System Card from the Evidence Tree

## Motivation

A model card describes a model. A dataset card describes a dataset. Neither, on its own, is what a regulator, notified body, third-party evaluator, or board reads to decide whether a *system* is fit for deployment. The system is the model plus the dataset(s) plus the evaluation evidence plus the safety-evidence summary plus the deployment-tier decision. The artefact that stitches those five together into one document is the **system card**.

The frontier labs converged on this shape independently. OpenAI publishes system cards for major model releases (GPT-4, GPT-4o, o1, o1-preview, Sora, DALL·E 3). Anthropic publishes model cards / addenda whose scope is system-level (the Claude 3, 3.5, 3.7, 4 model card families and their addendum releases). Google publishes Gemini model cards on the Gemini API pages and the Vertex AI documentation. Meta publishes Llama Responsible Use Guides and per-release model cards for Llama 2, 3, and 3.1. The four public examples are what this chapter reads against.

The rest of the module (chapters `04`–`07`) refines specific sections of the system card. This chapter fixes the *composition* — how the five inputs come together, how each maps to a node in the evidence tree (mod-104), and what the section-by-section walk looks like against the four worked examples.

## What a system card composes

The system card is a single external artefact whose five inputs are:

1. **Model card(s)** — the reporting unit for each model in the system (base model, fine-tuned variants, judges used as evaluators, tools whose weights are themselves a model).
2. **Dataset card(s)** — the reporting unit for each dataset that materially shapes system behaviour (training / fine-tuning corpora at whatever level of disclosure the provider chooses, eval sets, RLHF preference datasets, RAG corpora, guardrail training data).
3. **Evaluation evidence** — the eval reports the system's quality-attribute claims rest on (mod-104 chapter `03` reproducibility bundles), pointed at by digest.
4. **Safety-evidence summary** — the red-team, jailbreak, dangerous-capability, and guardrail evaluations, plus their residual-risk position. Mod-108 and mod-111 own the depth; the system card carries the summary.
5. **Deployment-tier decision** — the RSP / Preparedness / FSF tier (or, for non-frontier systems, the deployment-mode decision) and the specific evidence that drove the assignment.

Each of the five is a *pointer* in the assurance-card head (chapter `02`); the body walks the reader through each in a section written for the audience the variant is aimed at.

Two invariants over the composition:

- **The system card is a view over the evidence tree, not a re-authoring.** The eval report, the safety report, the tier decision are all already signed evidence nodes in the store (mod-104). The system card names them by digest and paraphrases them for the reader. The card cannot say something the underlying evidence does not say; if the reviewer follows the pointer and finds a different claim, the card is broken.
- **The five inputs are versioned together at the system-card release.** The card carries a single `subject.content_address` for the system as a whole, and each component under `subject.components[]` is pinned to a specific content-address (mod-104 chapter `01`). Later re-issues re-pin.

## Section walk: composing one system card

Take the six sections a well-formed system card carries and, for each, name what evidence node discharges it and what the four public worked examples do.

### §1 — System identity and version

**Discharges:** the head's `subject.system_id`, `subject.content_address`, and `subject.components[]` list.

**Body content:** the system's name and version, the release date, the components (base model, fine-tuned variants, tools, guardrails, retrieval index), and the licensing / access position.

**Worked examples.**

- OpenAI system cards ([platform.openai.com/docs → system cards](https://openai.com/index/gpt-4o-system-card/), the [GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf), the [o1 System Card](https://openai.com/index/openai-o1-system-card/)) open with a "System overview" that names the model, the training data cutoff (at whatever level of disclosure OpenAI ships), the modalities, and the deployment surfaces (ChatGPT, API, first-party product) covered.
- Anthropic model cards ([Claude 3 model card](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf), the Claude 3.5 Sonnet addendum, and the Claude 4 model card family) open with a "Model" section that lists the variants (Opus, Sonnet, Haiku) covered, the release date, and the training-data cutoff.
- Google Gemini model cards ([Gemini model cards on the Gemini docs](https://ai.google.dev/gemini-api/docs/models) and the Vertex AI page) list variant, context window, modalities, and knowledge cutoff.
- Meta Llama disclosures ([Llama 3 model card on GitHub](https://github.com/meta-llama/llama-models/blob/main/models/llama3/MODEL_CARD.md), the [Responsible Use Guide](https://ai.meta.com/static-resource/responsible-use-guide/)) list variant sizes (8B, 70B, 405B), context, training data cutoff, and license.

Enterprise-scale version: the section also carries `subject.components[]` with content-addresses into the store, and (for non-public variants) a `producer_signature` per component that a reviewer can verify.

### §2 — Intended purpose, appropriate use, and out-of-scope use

**Discharges:** the case node "the system is used within its intended purpose."

**Body content:** the intended primary use cases (extending Mitchell §2 — chapter `01`); the intended users; the deployment tiers this variant covers; the out-of-scope / foreseeable-misuse list; the *appropriate-use boundary* — the set of use cases the assurance case affirmatively demonstrates fitness for.

**Worked examples.**

- OpenAI system cards enumerate use-case categories (assistant, coding, content generation), user categories, and — critically — the out-of-scope categories the model is *not* released for, with an evidence-backed narrative of the guardrail decisions. The GPT-4 System Card devotes a substantial section to "harms of representation, allocation, and quality of service" as out-of-scope categories with mitigations.
- Anthropic model cards frame the intended purpose against the *Acceptable Use Policy* (linked in the card) and name specific use-restriction categories (weapons of mass destruction, critical infrastructure attacks, election interference, etc.).
- Gemini cards on Vertex frame intended use in terms of API-tier availability and the Google Cloud AI Prohibited Use Policy.
- Meta's Responsible Use Guide is the model's out-of-scope treatment for the Llama family: it enumerates deployment-context guardrails deployers are expected to add, and it names use categories Meta considers out-of-scope.

Enterprise-scale version: the section binds each use-case category to a specific case node (`goal:G1.S1.G-appropriate-use-{category}`) and to specific `evidence_pointers` in the head — either a fitness-for-purpose eval report, a red-team engagement report against the misuse category, or a guardrail-eval report showing the mitigation works.

### §3 — Training and evaluation data

**Discharges:** the case nodes "the training data was collected under the represented governance regime" (EU AI Act Article 10) and "the evaluation data is representative and integrity-checked" (mod-104 chapter `05`).

**Body content:** for each dataset in `subject.components[]`, a paraphrase of the Gebru datasheet content the assurance store carries. For training data, at whatever level of disclosure the provider chooses (Mitchell et al. allow partial disclosure); for evaluation data, the eval-set integrity attestation content-address must be present, and if the eval set contains PII or personal data, the section names the redaction status.

**Worked examples.**

- OpenAI system cards describe training data at the level of "publicly available data, information licensed from third-party providers, and information created by human reviewers." Specific dataset names are usually not disclosed; the section binds instead to data-governance and consent narratives. Eval data is often named specifically (Advanced Voice, red-team datasets, capability evaluations).
- Anthropic model cards describe training data in terms of the Constitutional AI process and the Acceptable Use guardrails. The Claude 3 model card enumerates capability evaluations (MMLU, MATH, HumanEval, GPQA, and others) and the datasets those evaluations run against.
- Gemini cards describe training corpora at category level (text, images, code, videos, multilingual) and cite the capability evaluations by name (MMLU, BIG-Bench Hard, HumanEval, WMT, and others).
- Meta Llama 3 model cards go the furthest on training-data disclosure — they name the token count, the pretraining data cutoff, the languages, and the fine-tuning data composition at category level.

Enterprise-scale version: every eval-set cited is pointed at by digest, the integrity attestation is available under the regulator or third-party variant, and the contamination-attestation (mod-104 chapter `05`) is cited for any public benchmark whose contamination status matters to the claim.

### §4 — Quality attributes and evaluation evidence

**Discharges:** the case's per-quality-attribute goals (`goal:G1.S1.G-{attribute}`). Chapter `05` walks the ISO/IEC 25059 spine that structures the section.

**Body content:** for each quality attribute (functional adequacy, reliability, robustness, transparency, controllability, societal-and-ethical-risk mitigation), the reported metrics, thresholds, CIs, and — for external audiences that need it — the eval-report digest.

**Worked examples.**

- OpenAI system cards report capability evaluations (academic benchmarks) and safety evaluations (harmful content, bias, hallucination, jailbreak) in separate tables with numerical results and, in most cases, comparison to previous models.
- Anthropic model cards report a *broad* capability battery (MMLU, MATH, GPQA, MMMU, HumanEval, MGSM, ARC-Challenge, BBH, and others) with numerical results and — as of the Claude 3 family and beyond — with agentic-benchmark evaluations (SWE-Bench, TAU-Bench). Safety evaluations are reported in an addendum (Anthropic uses a Responsible Scaling Policy report shape; mod-108 has depth).
- Gemini model cards report capability evaluations (MMLU, MATH, HumanEval, and others) with comparison to previous Gemini variants and to competitor models.
- Meta Llama model cards report capability evaluations against a similar battery and — since Llama 3 — a substantial safety evaluation section (CyberSecEval, refusal-rate, prompt-injection, malicious-code, adversarial robustness).

Enterprise-scale version: every reported metric has an `evidence_pointers` entry naming the eval-report digest. The reproducibility bundle (mod-104 chapter `03`) is available to third-party evaluators under mod-109. Statistically warranted thresholds and CIs are non-negotiable; a card that reports a point estimate without a CI has broken the ISO/IEC 25059 quality-attribute contract chapter `05` sets.

### §5 — Safety-evidence summary and residual risk

**Discharges:** the case's residual-risk claim and the safety-evaluation goals (`goal:G1.S4.G-residual-risk`).

**Body content:** the red-team methodology, the dangerous-capability evaluations, the guardrail evaluations, the residual-risk position after mitigations, and the escalation path if the residual-risk position degrades post-deployment.

**Worked examples.**

- OpenAI system cards devote substantial length to safety evaluation — the GPT-4 System Card describes the internal Red Teaming Network, the External Advisory Board, and per-category safety evaluation results. The GPT-4o System Card and o1 System Card extend to preparedness-framework evaluations (cybersecurity, CBRN, model autonomy, persuasion) and report the tier decision.
- Anthropic pairs the model card with a *Responsible Scaling Policy* evaluation report (mod-108 has depth) that names the AI Safety Level (ASL) assigned to the model, the evaluations that drove the assignment, and the deployment/security commitments the tier imposes.
- Gemini reports safety evaluations at category level (child sexual abuse material, dangerous content, harassment, hate speech) with red-team results and — for the Ultra tier — separate reporting.
- Meta's Llama Responsible Use Guide and per-release safety documentation report CyberSecEval, purple-team results, and adversarial robustness evaluations. Meta's [Llama 3.1 announcement documentation](https://ai.meta.com/blog/meta-llama-3-1/) references its trust-and-safety tooling (Llama Guard, Prompt Guard, Code Shield) as guardrails deployers can adopt.

Enterprise-scale version: the section binds to the risk-engineering peer's harm inventory (mod-102 chapter `06`; the peer is `ai-risk-engineer`), names the mitigation shipped per harm, cites the guardrail-eval digest that demonstrates the mitigation works, and reports the residual-risk position. Disclosure discipline matters here (chapter `06`): specific attack payloads that would reveal exploit primitives are redacted in the public variant and available under the regulator / third-party variant.

### §6 — Deployment-tier decision

**Discharges:** the case's tier-decision goal (`goal:G1.S3.G-tier-appropriate`).

**Body content:** for frontier systems, the RSP / Preparedness / FSF tier (mod-108) the release has been assigned to, the specific evaluations that drove the assignment, and the operational constraints the tier imposes (deployment restrictions, monitoring intensity, escalation thresholds). For non-frontier systems, the deployment-mode decision (staff-only, controlled deployer set, general availability) and its rationale.

**Worked examples.**

- OpenAI system cards report the [Preparedness Framework](https://openai.com/safety/preparedness/) tier decision for the four tracked categories (cybersecurity, CBRN, persuasion, model autonomy) and — for reasoning models — the deployment / research-only decision.
- Anthropic model cards / addenda report the [Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) AI Safety Level (ASL) the model has been assigned to and the deployment/security commitments that follow (ASL-2 vs ASL-3 imposes different security and deployment postures).
- Gemini publishes a [Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) with Critical Capability Levels; DeepMind's model releases reference the framework in accompanying safety documentation.
- Meta's [Frontier AI Framework](https://ai.meta.com/static-resource/meta-frontier-ai-framework/) frames its release decisions for Llama-family systems in terms of critical risk assessments (biological, cybersecurity, chemical), and its per-release cards or safety documentation carry the tier-relevant outcome.

Enterprise-scale version: the section names the *deployment-tier framework* the enterprise adopted (a program choice; frontier-lab RSP-adapted for internal use, or a NIST-AI-RMF-anchored tier ladder for non-frontier systems), the tier this release sits in, the evaluations that drove the assignment, and the operational constraints inherited. Chapter `07` returns to how the board variant summarises this for a business audience without collapsing the tier decision into a marketing narrative.

## Traceability — the walk end-to-end

A reviewer opening the system card should be able to walk any claim in six steps.

1. **Read the claim** — e.g., "the system passed the Article 15 accuracy criterion with macro-F1 = 0.912 on `harm-eval-set/v3.2`, 95% CI [0.897, 0.926]."
2. **Locate the pointer in the head** — `evidence_pointers.claim:accuracy-primary.evidence_content_address = sha256:74a1…` and `sacm_artifact_id = art:eval-report:rc-2026-05-07:gate-fa-01`.
3. **Resolve the pointer in the evidence store** — fetch the eval-record bytes at `sha256:74a1…`, re-canonicalise, re-hash, confirm equality (mod-104 chapter `01`).
4. **Verify the producer signature** — the eval record was signed by `model-evaluation-engineer` (level 30, ML Engineering family), matching the evidence-contract routing for this case node (mod-102 chapter `06`).
5. **Reach the assurance case** — the SACM `Artifact.id` maps into the case at `goal:G1.S1.G-15-accuracy` (mod-102 chapter `04`).
6. **Cross-check the reproducibility bundle** — if the reviewer chooses (or is contractually required to; mod-109), rerun the eval from the bundle content-address and confirm the reported number reproduces within CI (mod-104 chapter `03`).

If any of the six steps breaks, the claim is not defensible. The system card is *only* as defensible as this walk.

## Anti-patterns to avoid when composing

- **Rewriting the eval report inside the card.** The card paraphrases and cites; it does not replace. A card that reports a metric the underlying evidence node does not carry is broken.
- **Losing the version pin.** A system card that cites `harm-eval-set` without a version (`v3.2`) or a digest is not a card; it is a claim about a dataset name. Every dataset is pinned to a content-address.
- **Bundling too many components.** A system card that describes ten variants at once loses per-variant claim discipline. When variants have materially different behaviour (Opus vs. Haiku), publish a variant per system card and cross-reference.
- **Merging safety and capability into one table.** The reader reads safety and capability against different thresholds and with different disclosure discipline. Keep the tables distinct; the head carries them under separate `evidence_pointers` entries.
- **Marketing narrative in §5.** The safety-evidence summary is written for adversarial review. It reports residual risk, not sentiment. Chapter `07`'s board variant is the appropriate place for a decision-oriented narrative; the base variant is not.
- **Silent redaction.** A public variant that removes an eval result without an entry in the `redaction_manifest` is broken. Chapter `06` returns to the redaction discipline.

## Summary

- A system card composes model card + dataset card + evaluation evidence + safety-evidence summary + deployment-tier decision into a single external artefact.
- Each of the six sections (identity / intended purpose / data / quality / safety / tier) discharges specific assurance-case nodes and binds to specific `evidence_pointers` in the head.
- OpenAI, Anthropic, Google Gemini, and Meta Llama publish system-card-shaped disclosures that model the sectional structure; the enterprise-scale version adds evidence-pointer binding, producer signatures, and audience-variant discipline.
- The card is a *view* over the evidence tree, not a re-authoring; a reviewer can walk any claim from the body to a signed digest in the store in six steps.
- Chapters `04`–`07` refine specific sections: the ISO/IEC 42005 impact-assessment section (`04`), the ISO/IEC 25059 quality-attribute spine (`05`), C2PA content-provenance and disclosure trade-offs (`06`), and the four audience variants (`07`).
