# exercise-02: NIST AI RMF (with GenAI Profile) Crosswalk

**Estimated effort:** 3 hours

## Objective

Extend the anchor slice you produced in exercise `01` with the **NIST AI RMF cross-tag** — for every EU AI Act row, name the RMF sub-categories the deliverable contributes to, pin the Playbook version, and (for GenAI systems) add the AI 600-1 GenAI-Profile risk categories and suggested actions. Then add the *distinct* GenAI-Profile row block that has no one-to-one Article number but that an RMF-aligned audience will expect to see.

The output is a walkable single-row artefact that a US enterprise procurement team, a US federal deployer, or an AISI reviewer can pick up and read — every EU obligation is also visible in RMF sub-category vocabulary.

## Prerequisites

- Chapter [`03-nist-ai-rmf-crosswalk-with-genai-profile.md`](../03-nist-ai-rmf-crosswalk-with-genai-profile.md).
- Exercise [`exercise-01`](exercise-01-eu-ai-act-obligation-to-deliverable-map.md) — your anchor map is the input to this exercise.
- [NIST AI Risk Management Framework (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the four functions and the sub-category structure.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the per-sub-category suggested actions. Note the current publication date; you will pin it.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific risk categories and suggested actions.
- [NIST AI 100-2 — Adversarial Machine Learning Taxonomy](https://doi.org/10.6028/NIST.AI.100-2e2023) — the attack-taxonomy vocabulary for Article 15 cybersecurity sub-rows.

## Problem statement

Pick up the map you emitted in exercise `01` and extend every row with the RMF cross-tag columns:

- `sibling_nist_rmf` — one or more sub-category references (`MAP-1.1`, `MEASURE-2.7`, `MANAGE-1.3`, …).
- `sibling_nist_ai_600_1` — for GenAI systems, the applicable GenAI-Profile risk categories and suggested-action references (Playbook IDs like `MS-2.6-002`). Empty for non-GenAI systems, but the field is present.
- `nist_playbook_version` — the Playbook version-of-record you cross-tagged against (a date or version identifier).

Then add the *GenAI-Profile row block* — additional rows for AI 600-1 risk categories that do not have a one-to-one EU AI Act Article number (confabulation, harmful bias in GenAI outputs specifically, human-AI configuration, information integrity, IP, obscene / degrading / abusive content, value-chain and component integration, environmental impact). These rows have owners, deliverables, and evidence pointers the same as the anchor rows — but no `article_or_clause` field, because the anchor here is `nist-ai-600-1`.

If your exercise-`01` system was intentionally non-GenAI, either (a) revise the scoping brief to add a GenAI component (a summarisation layer, a chatbot support surface, an image-generation module) so this exercise has meaningful GenAI rows, or (b) explicitly mark the GenAI-Profile rows as `not-applicable` with a determination trail — either is acceptable, but the GenAI-Profile *columns* must still be present.

## Requirements

Produce three artefacts.

### 1. `nist-rmf-extended-map.yaml`

The exercise-`01` map, extended with the RMF cross-tag columns for every row. New / updated fields:

- Every row gains `sibling_nist_rmf: [ ... ]` populated with the sub-category IDs that apply, plus a per-row `rmf_rationale` field (a one-sentence rationale for the tag — why is `MEASURE-2.7` on this row?).
- Every row gains `sibling_nist_ai_600_1: [ ... ]`. Each entry has:
  - `risk` — the GenAI-Profile risk category name (from AI 600-1's list — confabulation, information integrity, IP, information security, harmful bias, value-chain and component integration, obscene / degrading / abusive content, environmental impact, human-AI configuration, …).
  - `suggested_actions` — a list of Playbook / AI 600-1 suggested-action IDs; use the actual IDs from the pinned Playbook version. If the ID's exact form has changed between Playbook releases, mark `<!-- needs-research: … -->` rather than guessing.
  - `applies` — boolean (some rows may cross-tag a risk with `applies: false` and a rationale, e.g., "no synthetic-content generation surface").
- The map header gains `frameworks_pinned.nist-ai-rmf` (a version — `"1.0"` for AI 100-1), `frameworks_pinned.nist-ai-600-1` (a date — the AI 600-1 publication date), `frameworks_pinned.nist-playbook` (the Playbook snapshot date you cross-tagged against), and `frameworks_pinned.nist-ai-100-2` (the AI 100-2 publication).

### 2. `nist-rmf-cross-tag-rationales.md`

A one-line-per-row rationale table:

| obligation_id | sibling_nist_rmf | one-line rationale |
| --- | --- | --- |
| `eu-ai-act.art9.plan` | `MAP-1.1, MAP-1.5, MAP-2.1` | Context, categorisation, and system-of-systems framing pre-requisites for the risk-management plan |
| `eu-ai-act.art9.harms` | `MAP-5.1, MAP-5.2` | Impact characterisation on individuals, groups, communities |
| … | … | … |

Every anchor row must appear in this table. The rationale is your defence at review — a reviewer challenging "why is `MANAGE-4.2` on this row?" reads the table.

### 3. `genai-profile-row-block.yaml`

The additional row block for AI 600-1 risk categories that do not have an EU AI Act Article one-to-one. For each risk category applicable to your system, one row:

- `obligation_id` — `nist-ai-600-1.confabulation.evaluation`, `nist-ai-600-1.information-integrity.watermarking`, `nist-ai-600-1.ip.training-data-licensing`, `nist-ai-600-1.value-chain.supplier-attestation`, etc.
- `instrument` — `nist-ai-600-1`.
- `instrument_version_pin` — the AI 600-1 publication.
- `obligation_summary` — one-sentence paraphrase of the risk category and the specific programme obligation.
- `applies_when` — the scoping condition (e.g., "GenAI system with public-facing text-generation surface").
- `deliverable` — the named artefact.
- `deliverable_kind` — as before.
- `owner_role`, `signing_role`, `tier_applicability`, `status`, `evidence_pointer`, `notes` — as before.
- `sibling_nist_rmf` — the RMF sub-categories the GenAI-Profile row cross-tags into (typically `MEASURE-2.6`, `MEASURE-2.7`, `MAP-4.1`, `MANAGE-4.1`).
- `sibling_eu_ai_act` — where the GenAI-Profile row also touches an anchor row, cross-reference it (e.g., `information-integrity` may cross-reference `eu-ai-act.art50.2` on watermarking).

Minimum row count for the block, if any GenAI surface is in scope: cover at least confabulation, information integrity, information security, harmful bias (GenAI-output-side, distinct from Article 10 dataset-side), and value-chain / component integration. Environmental impact is optional; obscene / degrading / abusive content depends on scope; IP is required only if your training-data posture makes it material.

## Starter guidance

- **The crosswalk is many-to-many.** Do not aim for a single RMF ID per row. Most rows carry 2–4 sub-category tags; that is expected.
- **Pin the Playbook.** The Playbook evolves. Your map's rows cite Playbook suggested-action IDs that were valid at the pinned date; if a Playbook revision has moved or renamed an action, you either (a) refresh to the current Playbook (bumping `frameworks_pinned.nist-playbook`) or (b) note the drift with a `<!-- needs-research: … -->` marker.
- **`sibling_nist_ai_600_1` needs an `applies` boolean per entry.** Silence looks like "the risk exists and we do not address it." An explicit `applies: false` with a one-sentence rationale (e.g., "no synthetic-image surface") is a real answer.
- **Some anchor rows are `citation-only`.** Article 49 (registration) plugs into `GOVERN-4.1` only weakly — it is primarily a filing action. Mark these rows with a `crosswalk_strength: citation-only` field (in `notes` if you prefer). The reader knows not to expect deep methodology overlap.
- **AI 100-2 tags on Article 15 sub-rows.** Article 15 cybersecurity sub-rows carry the attack-taxonomy branch from AI 100-2 (evasion / extraction / inference / poisoning × white-box / grey-box / black-box × goal / specificity). Encode this in a `nist_ai_100_2_branch` sub-field on the Article 15 sub-rows.
- **MEASURE-2.7 is a magnet.** Article 12 integrity, Article 15 cybersecurity, and every GenAI-Profile information-security row will end up at MEASURE-2.7. That is correct — the field is many-to-many.
- **A GenAI-Profile risk can apply without the system being fully generative.** A discriminative system that uses a small GenAI component for a narrow purpose still incurs information-integrity and possibly IP risks. Do not treat the block as all-or-nothing.
- **Do not fabricate Playbook IDs.** If you cannot find the exact suggested-action ID in the current Playbook, mark `<!-- needs-research: … -->`.

## Acceptance criteria

You have succeeded if:

- `nist-rmf-extended-map.yaml` retains every anchor row from exercise `01`, unchanged in its anchor fields, with the new `sibling_nist_rmf`, `sibling_nist_ai_600_1`, and `nist_playbook_version` fields populated.
- Every anchor row has at least one RMF sub-category tag (or is explicitly marked `crosswalk_strength: citation-only` with a rationale).
- Every anchor row's `sibling_nist_ai_600_1` field is present. For non-GenAI systems, entries are `applies: false` with rationale; for GenAI systems, at least the applicable risks are enumerated.
- The map header pins `nist-ai-rmf`, `nist-ai-600-1`, `nist-playbook`, and `nist-ai-100-2` versions.
- `nist-rmf-cross-tag-rationales.md` covers every anchor row with a one-line rationale — no row is unexplained.
- `genai-profile-row-block.yaml` adds the AI 600-1 rows that do not have EU AI Act one-to-ones. If the system is intentionally non-GenAI, the file is present but small, with each candidate row marked `not-applicable` with a determination trail rather than absent.
- Article 15 cybersecurity sub-rows carry the AI 100-2 taxonomy branch on each attack-category sub-row.
- Every Playbook ID cited is either verifiably in the pinned Playbook version or marked `<!-- needs-research: … -->`.
- A reviewer walking the map cold can identify, for any row, both its EU AI Act citation and its RMF sub-categories, and can open the Playbook to the suggested actions your programme is claiming to have performed.

## Stretch goals

- **Round-trip a reader from RMF to article.** Author a small tool (or a table in a markdown file) that takes an RMF sub-category ID and returns every row on your map that carries it. Reviewers use this to answer "we're audited against MEASURE-2.7 — show me every deliverable that tags to it." Adds mechanical value beyond the map.
- **Cover the GOVERN sub-categories deliberately.** Many anchor authors under-tag GOVERN (which is process / policy oriented) and over-tag MEASURE (which is evaluation-oriented). Audit your map: does every deliverable have a GOVERN tag where GOVERN-1 through GOVERN-6 apply? Programme-level maturity signals live under GOVERN.
- **Explicit Playbook-drift ledger.** Track (in a `nist-playbook-drift-ledger.md`) every place the Playbook's suggested action has moved between the version *you* pinned and the current published version. This is what a programme runs at each Playbook refresh; producing one now walks the discipline.
- **Add a `nist-ai-100-4` cross-tag on synthetic-content rows.** [NIST AI 100-4 (Reducing Risks Posed by Synthetic Content)](https://doi.org/10.6028/NIST.AI.100-4) is the synthetic-content-provenance reference; where your GenAI-Profile information-integrity rows exist, add an `ai_100_4_reference` sub-field with the relevant AI 100-4 section.
- **Author a one-page RMF-audience card summary.** In `rmf-audience-summary.md`, produce a one-page projection of your map that a US enterprise procurement team would consume: which RMF sub-categories are fully covered, which are partial, which are not covered, and where the AI 600-1 posture stands. This anticipates the card-side derivation from `mod-105`.
- **Cross-reference AISI evaluation methodology.** The [US AI Safety Institute at NIST](https://www.nist.gov/aisi) publishes methodology documents that align with specific RMF sub-categories (particularly MEASURE-2 rows on GenAI). Where your map's MEASURE-2 rows overlap AISI methodology, cite the AISI reference in a `sibling_aisi` sub-field. Prepares the hand-off shape in `mod-109`.
