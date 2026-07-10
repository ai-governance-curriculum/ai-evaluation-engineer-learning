# mod-105-cards-for-external-audiences: Model, System, and Dataset Cards for Regulatory and Third-Party Audiences

Extends the Mitchell / Gebru / Hugging Face card lineage into the enterprise-scale **assurance-card** shape a regulator, notified body, third-party evaluator, or board audience will actually read. Composes a system card that stitches model card + dataset card + evaluation evidence + safety-evidence summary + deployment-tier decision into a single external artefact; structures the quality-attribute section around ISO/IEC 25059; carries an ISO/IEC 42005 impact-assessment output section whose findings are traceable to concrete nodes in the underlying GSN assurance case (mod-102); attaches C2PA content-provenance manifests for GenAI outputs; and derives the four audience variants (published disclosure, regulator submission, third-party evaluator handoff, board narrative) from a single canonical case using a signed `redaction_manifest`.

**Estimated effort:** 14 hours

## Learning objectives

- Extend Mitchell et al. model cards, Gebru et al. datasheets, and the Hugging Face model-card guidebook into the enterprise-scale assurance-card shape a regulator, notified body, third-party evaluator, or board audience will read.
- Compose a system card that stitches model card + dataset card + evaluation evidence + safety-evidence summary + deployment-tier decision into a single external artefact, using OpenAI system cards, Anthropic model cards, Google Gemini cards, and Meta Llama disclosures as worked examples.
- Author an ISO/IEC 42005 AI-impact-assessment output section that consumers can trace to concrete evidence nodes in the underlying GSN case.
- Structure card content around ISO/IEC 25059 quality dimensions so a reviewer can walk from a quality attribute to the eval evidence and back.
- Attach C2PA content-provenance manifests for GenAI outputs and reason about disclosure-vs-secrecy trade-offs (attack-payload non-disclosure, PII scrubbing, statistical redaction of decontamination fingerprints).
- Draft the internal-vs-external variants of a card (published disclosure, regulator submission, third-party evaluator handoff, board narrative) and reason about what each audience needs.

## Lecture chapters

1. [`01-lineage-from-mitchell-and-gebru.md`](01-lineage-from-mitchell-and-gebru.md) — Mitchell et al.'s nine model-card sections, Gebru et al.'s seven datasheet sections, the Hugging Face model-card guidebook's YAML-frontmatter / Markdown-body separation, and the variants worth recognising (Data Cards, Nutrition Labels, Croissant, FactSheets, Reward Reports, Interactive Model Cards). What each lineage source fixes, and what it leaves for the assurance card.
2. [`02-assurance-card-shape-for-external-audiences.md`](02-assurance-card-shape-for-external-audiences.md) — The assurance-card definition: machine-readable head + human-readable body, evidence-pointer bindings into the store (mod-104), discharges-mapping into the assurance case (mod-102), redaction-manifest discipline, producer signature. The three-way binding claim ↔ digest ↔ case node.
3. [`03-system-card-composition-from-evidence-tree.md`](03-system-card-composition-from-evidence-tree.md) — Six-section system-card composition (identity / intended purpose / data / quality / safety / tier) walked against OpenAI, Anthropic, Google Gemini, and Meta Llama public system cards. The six-step audit walk from a body claim to a signed digest in the store to a goal in the case.
4. [`04-iso-iec-42005-impact-assessment-section.md`](04-iso-iec-42005-impact-assessment-section.md) — The five sub-sections of an ISO/IEC 42005 impact-assessment section (scope, methodology, findings, treatments, residual position), each traceable by content-address to the underlying impact-assessment artefact. Interaction with EU AI Act Article 27 FRIA.
5. [`05-iso-iec-25059-quality-attribute-spine.md`](05-iso-iec-25059-quality-attribute-spine.md) — The ISO/IEC 25059 quality-attribute row shape (attribute, sub-attribute, intended-purpose scope, metrics with CIs, thresholds with rationale, eval-report digest, reproducibility-bundle digest, `sacm_artifact_id`). The seven-step walk end-to-end and the reverse walk from a report back to the card.
6. [`06-c2pa-provenance-and-disclosure-tradeoffs.md`](06-c2pa-provenance-and-disclosure-tradeoffs.md) — C2PA manifest structure and its `provenance.c2pa` block in the card. The five recurring disclosure-vs-secrecy tensions (attack payloads, PII in eval sets, decontamination canaries, trade-secret / IP training-data disclosures, vulnerability windows) and the reasoning per audience variant.
7. [`07-audience-variants-of-one-card.md`](07-audience-variants-of-one-card.md) — Derivation from one canonical case to four audience variants (public / regulator / third-party evaluator / board) using a signed `redaction_manifest`. The six load-bearing invariants that stay identical across variants, and the three-step audit walk that catches drift.

## Structure

- `01-…md` … `07-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapter `01`** — read once, then read Mitchell et al. (2019) and Gebru et al. (2021) in one sitting to internalise the base vocabulary. The rest of the module quietly assumes you can name the nine and the seven.
- **Chapter `02`** — read after `01`. Draft the assurance-card head as a YAML skeleton for a system you know; getting the head right before opening an exercise saves rework.
- **Chapter `03`** — read alongside a real published system card (any of the OpenAI GPT-4o, Anthropic Claude 3, Google Gemini, or Meta Llama 3 cards on the vendor pages). Exercise `01` writes a model card for a regulated product; exercise `02` composes the system card.
- **Chapter `04`** — read after `03`. ISO/IEC 42005 is worth reading the abstract of directly (see `resources.md`). Exercise `03` produces the impact-assessment section against a worked scenario.
- **Chapter `05`** — read alongside a real quality-attribute-mapping exercise; the ISO/IEC 25059 vocabulary makes the section fall into place. This chapter has no dedicated exercise; the quality-attribute row shape shows up in exercises `01` and `02`.
- **Chapter `06`** — read after `05`. C2PA reading is worth an hour on the specification page. Exercise `04` builds a working C2PA manifest for a GenAI output and reasons about the disclosure position.
- **Chapter `07`** — read at the end. The audience-variant derivation is easier to internalise once chapters `03`–`06` have named what the base card carries. Exercise `05` produces the four variants of one card and their `redaction_manifest`.

## Dependencies

- Requires mod-101 (release-assurance position — framework overview, deferral contract), mod-102 (assurance-case engineering — the case is what the card discharges into), mod-103 (release-gate architecture — the tier decision the card reports), and mod-104 (evaluation evidence pipeline — every claim on the card is a pointer into the store).
- Consumed by mod-106 (cross-jurisdictional obligation mapping — the `regime` block on the head), mod-107 (sector-regulated assurance — sector-specific card variants), mod-108 (deployment-tier gating — the tier-decision section), mod-109 (third-party evaluator interface — the third-party variant is the first handoff artefact), mod-110 (post-market surveillance — the post-market plan section), mod-111 (GPAI systemic-risk assurance — the Article 55 / GPAI Code disclosure extends the card), and mod-112 (owning an assurance program — aggregate card-family reporting).
- All three capstone projects consume this module. Project-101 (release-gate capstone) ships a full assurance card. Project-102 (cross-jurisdictional compliance map) uses the card as the cross-tab spine. Project-103 (assurance-program slice) integrates card production into the release cycle end-to-end.
