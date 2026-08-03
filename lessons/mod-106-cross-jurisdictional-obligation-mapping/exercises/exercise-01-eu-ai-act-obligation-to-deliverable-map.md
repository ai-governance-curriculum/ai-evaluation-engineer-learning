# exercise-01: EU AI Act Obligation-to-Deliverable Map

**Estimated effort:** 3 hours

## Objective

Produce the **EU AI Act anchor slice** of an assurance-map for a single system you invent — one row per in-scope obligation, each row pointing at a concrete named deliverable, the peer role that owns it, and the signing state. This exercise builds the map's *anchor layer* as chapter `02` defines it. Later exercises (`02` NIST RMF crosswalk, `03` ISO crosswalk, `04` US-side overlay, `05` non-EU overlay, `06` AI Verify interoperability) extend the same map row-by-row; the anchor slice you produce here has to be usable as the base they attach to.

## Prerequisites

- Chapter [`01-why-cross-jurisdictional-mapping.md`](../01-why-cross-jurisdictional-mapping.md) — the four-layer map, the row shape, who consumes the map.
- Chapter [`02-eu-ai-act-obligations-to-deliverables.md`](../02-eu-ai-act-obligations-to-deliverables.md) — the article-by-article deliverable table this exercise operationalises.
- Skim access to [Regulation (EU) 2024/1689 (EU AI Act)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), particularly Chapter III Section 2 (Articles 8–15), Article 17 (QMS), Article 26 (deployer obligations), Article 43 (conformity assessment), Article 47 (declaration of conformity), Article 49 (registration), Article 61 (serious-incident reporting), Article 72 (post-market monitoring), Annex III (high-risk domains), Annex IV (technical documentation content), Annex V (declaration content).
- Familiarity with the peer-role registry for the AI Evaluation Engineer track (`ai-risk-engineer`, `model-evaluation-engineer`, `ai-governance-analyst`, `ai-infra-security`, platform-eng, product, legal, DPO, HR — plus your own role, `ai-evaluation-engineer`).

## Problem statement

Invent one *specific* AI system and fix its scoping decisions before you write any rows. Then produce a first version of its assurance-map, filled in for every in-scope EU AI Act row.

The system-invention step is not decorative. The `applies_when` column of the map is meaningless unless the system's intended purpose, deployment surface, jurisdictional scope, and Annex III typing are pinned. Pick concretely: a **CV-screening tool for large employers deploying in the EU**, an **AI-based credit-adjudication assistant used by consumer lenders**, an **AI triage tool used by a national health service**, a **facial-recognition access system at public venues**, or another Annex III use-case of your choice. Note explicitly whether your organisation is the *provider*, the *deployer*, or both (`dual-hat`), and whether the system is a GPAI model provider or a downstream product built on someone else's GPAI. If the system has no EU exposure, you have picked the wrong scenario for this exercise — the anchor is the EU AI Act and the scoping is mandatory.

Once the scoping is fixed, populate the anchor slice for every article chapter `02` walks — Article 9, 10, 11 (with Annex IV items 1–8), 12, 13, 14, 15, 26 (only if deployer), 43, 47 (with Annex V sub-fields), 49, 61, 72, plus the Annex III typing row and Article 17 (QMS). Where the article decomposes into sub-rows (e.g., Article 11's Annex IV items, Article 15's attack-category sub-rows from paragraph 5), each sub-row is its own row.

## Requirements

Produce five artefacts.

### 1. `system-scoping-brief.md`

A one-to-two page brief that fixes:

- **Product name and one-sentence purpose.** Named product; specific intended purpose.
- **Provider / deployer / dual-hat status.** Argument for the classification, cited to Article 3(3) / (4) / (9) / (11).
- **Annex III typing.** Which Annex III point(s) apply, and why. If you argue the system is *out* of Annex III, cite the reasoning.
- **Jurisdictional scope.** EU exposure route (placed on the market, put into service, output used in the Union). Any Member-State-specific overlays you are aware of.
- **GPAI status.** Is the system a GPAI model provider? A GPAI-with-systemic-risk provider? A downstream product built on a GPAI? (For this exercise, keep GPAI-provider status *out* of scope unless you have a specific GPAI reason — `mod-111` covers those rows.)
- **Deployment tier assumption.** Pick a tier (from `mod-108`'s planned scheme — tier-0 to tier-3, or your own labels) so `tier_applicability` columns are meaningful. Justify.
- **Substantial-modification stance.** Under what changes would you re-open Article 43 (and therefore re-verify most rows)? Reference Article 3(23).

The brief is the *set-up* for the map. Reviewers of your map will read this first.

### 2. `anchor-map.yaml`

The YAML map itself, following the row shape chapter `02` names and the map document shape chapter `08` fixes (header + rows). Fields required per row for this exercise:

- `obligation_id` — unique within the map, kebab-case, dotted (e.g., `eu-ai-act.art9.plan`, `eu-ai-act.art11.annex-iv.5`, `eu-ai-act.art15.cybersecurity.data-poisoning`).
- `instrument` — `eu-ai-act-2024-1689`.
- `instrument_version_pin` — the version-of-record you cite against.
- `article_or_clause` — Article and paragraph reference.
- `obligation_summary` — a one-sentence paraphrase. Do not quote the article text; paraphrase.
- `applies_when` — the scoping condition (provider / deployer / dual-hat, Annex III point, tier applicability, deployment-surface condition). Include a `determined_by` and `determination_date`.
- `deliverable` — a named artefact filename or artefact set (e.g., `risk-management-plan-v1.md`, `sysdoc/05-change-log.md`, `nyc-ll-144-bias-audit-report-<date>.pdf` — though the last is not in-scope here).
- `deliverable_kind` — one of `document | report | declaration | plan | card | manifest | log-attestation | cross-ref`.
- `owner_role` — the peer role from the registry that produces the substantive content.
- `signing_role` — the role whose signature closes the deliverable.
- `tier_applicability` — the tier list from your scoping.
- `status` — one of `covered | partial | open | waived-with-residual | not-applicable | pending-instrument`. Because this exercise is authoring, `open` and `partial` are the honest defaults for most rows.
- `evidence_pointer` — a placeholder is acceptable (`sha256:0000…placeholder`), but the row must state *what artefact* the pointer will resolve to.
- `notes` — the trap or nuance for the row (e.g., for Article 10, the Article 10(5) safeguards; for Article 15, the online-learning resilience clause under 15(4)).

Fields intentionally *not* required this exercise (they land in later exercises): `sibling_nist_rmf`, `sibling_nist_ai_600_1`, `sibling_iso_clauses`, `iso_soa_status`, `sibling_jurisdictions`, `interop_ai_verify_*`, `interop_mgf_*`. Leave these fields present but empty, so the schema evolves cleanly across exercises.

The header must include `schema_version`, `map_id`, `system_id`, `system_version`, `map_version`, `generated_at`, `generated_by.role`, `anchor: eu-ai-act-2024-1689`, `jurisdictional_scope`, `notified_body_ref` (null unless you chose Annex VII), and `frameworks_pinned.eu-ai-act`.

### 3. `annex-iv-worksheet.md`

Article 11's Annex IV is a content list, and every numbered item is a row on the map. Produce a worksheet that shows the eight Annex IV items, each with:

- The section name (from Annex IV).
- The concrete deliverable filename you have picked.
- The owner role and signing role.
- Whether the row is a cross-reference to another row (Annex IV items 4, 7, 8 are).
- The specific content you would put in that section for your invented system — a bullet list, not full prose.

This worksheet is what a reviewer walks alongside the map to confirm the Annex IV rows are not empty placeholders. It should read as a plausible dossier table of contents for your system.

### 4. `article-15-attack-category-worksheet.md`

Article 15(5) enumerates attack categories (data poisoning, model poisoning, adversarial examples, model evasion, confidentiality attacks). For each:

- The specific evaluation methodology you would use (name a NIST AI 100-2 branch, an academic paper, or a tool).
- The evaluation artefact (filename) that would land on the row.
- The threshold or acceptance criterion your programme would apply.
- Whether the category is in-scope for your system (some may be `not-applicable` — e.g., confidentiality attacks may not apply for a system that returns only public information; argue explicitly).

Where the system supports **online learning after deployment**, Article 15(4) adds a specific resilience obligation — flag whether it applies and, if so, add a sub-row for it.

### 5. `annex-v-declaration-shape.md`

A skeleton of the Article 47 / Annex V EU declaration of conformity for your system. Each Annex V content field is a section header; below it, either the value (product name, provider name, provider address) or a placeholder marker (e.g., `<harmonised standards applied — populated after chapter 03 crosswalk>`). The `.md` shape is fine for this exercise; note in a footer that the release-gate would also emit a machine-readable `.json` twin per chapter `02`'s trap.

## Starter guidance

- **Fix the scoping first, then write rows.** If you start with rows you will re-write the map three times. The scoping brief must be complete before the map.
- **Paraphrase, do not quote.** The map is a cross-reference into the primary text, not a redistribution of it. Every obligation summary is your one-sentence paraphrase, and `article_or_clause` points at where the reader opens the primary text.
- **Every row names a *deliverable*, not an activity.** "Perform risk management" is not a deliverable; `risk-management-plan-v1.md` signed by role X on date Y is. If you cannot name a deliverable filename, the row is under-specified.
- **Use placeholder evidence pointers.** `sha256:0000…placeholder` is acceptable so long as the row states what artefact will land there. Do not fabricate digests.
- **Distinguish `not-applicable` from `open`.** A row that does not apply (e.g., Article 14(5)'s two-natural-persons rule when your system is not Annex III point 1) is `not-applicable` with a determination trail. An in-scope obligation without evidence yet is `open`.
- **Provider vs. deployer splits the row set.** If you chose dual-hat, expect ~1.4× the row count and cross-reference between the two sub-maps. If you chose provider-only, do not populate Article 26 rows.
- **Substantial modification is a rule, not a row.** Note it in the scoping brief; do not create a row for it.
- **Legal counsel signs the substantive-content and scope rows.** The Annex III typing row, the Article 43 Annex VI/VII decision row, and the Article 10(5) safeguards row all countersign to legal. Note this even without a real signature.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need legal confirmation, market-surveillance-authority contact detail, or Article-72-template-when-published detail, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `system-scoping-brief.md` fixes the seven scoping decisions above with cited article-based reasoning. A reviewer can decide, from the brief alone, whether the system is provider / deployer / dual-hat, which Annex III point applies, and which deployment tier the map is authored against.
- `anchor-map.yaml` validates against the row shape from chapter `02` and the header shape from chapter `08`. Every row carries the required fields. Empty siblings fields are present but empty (not missing) so the schema is stable.
- Every article chapter `02` walks has at least one row on the map. Article 11 has eight sub-rows (Annex IV items 1–8). Article 15 has at least three primary rows (accuracy, robustness, cybersecurity) plus attack-category sub-rows from paragraph 5. Article 26 has rows only if the scoping brief classified the system as deployer / dual-hat.
- Every row's `deliverable` field names a concrete filename or artefact set. No `TBD`, no "documentation." No row has `owner_role: TBD`.
- Every `applies_when` entry carries a `determined_by` and `determination_date`; determinations that require legal counsel (Annex III typing, Article 10(5) invocation, Article 43 Annex VI vs. VII choice) name legal explicitly.
- `annex-iv-worksheet.md` shows the eight Annex IV items with plausible per-section content for your invented system. Items 4, 7, and 8 are cross-references.
- `article-15-attack-category-worksheet.md` covers all five Article 15(5) attack categories with a methodology, a deliverable name, an acceptance criterion, and (where applicable) a not-applicable determination. Article 15(4) online-learning resilience is addressed either as an in-scope sub-row or as an explicit out-of-scope note.
- `annex-v-declaration-shape.md` shows every Annex V content field, with the values you can fill in filled and the values that will be populated after the ISO / NIST crosswalks (chapter `03` / `04`) marked as such.
- Every place you needed a fact you could not verify (article sub-clause reference, Annex III sub-point name change, Article 72 template shape) is marked `<!-- needs-research: … -->` rather than a guess.
- The map is *diffable* — a reviewer running `diff` between two versions of the map (v1 with placeholders, v2 filled in) sees a clean per-row delta. Canonical key order matters.

## Stretch goals

- **Emit canonical JSON.** Run your YAML through a canonicaliser (RFC 8785 JCS or `yq . -o json --output-format=json --indent=2` with a lexicographic key sort) and produce `anchor-map.canonical.json`. Compute its SHA-256 and note the digest at the top of the file.
- **Sign the map.** Generate a fresh keypair (do *not* use a production key), sign the canonical JSON's digest with `openssl dgst -sha256 -sign`, and store the signature at `anchor-map.canonical.json.sig`. Note the key type and its fingerprint in a `README.md`. This walks the signing flow chapter `08` names.
- **Author the row-level countersign for Annex III typing.** Draft what a legal countersign attestation would look like — signer, scope (row `eu-ai-act.annex-iii.<n>.<sub>`), signed-at, signature pointer. You do not need to actually sign it; produce the attestation shape.
- **Draft the substantial-modification rule as YAML.** Turn your scoping brief's substantial-modification stance into a machine-readable rule (`substantial_modification_rule.yaml`) that names the fields on the system-scoping side whose change re-opens the article rows. The rule is the input to the release-gate's staleness check.
- **Add one row for Article 27 FRIA.** If your system is deployed by a public authority or otherwise triggered under Article 27 (fundamental-rights impact assessment for deployers of high-risk AI), add the row and cross-reference it back to the `iso/42005`-shape impact-assessment deliverable. Note explicitly whether Article 27 applies for your invented scenario.
- **Draft the reviewer-facing walk-through.** In `map-review-walkthrough.md`, walk a reviewer through the map in the order you would expect them to open it: scoping brief first, then Annex III row, then Article 17 QMS row, then the Article 9 / 10 / 11 spine, then the Article 12 / 13 / 14 / 15 evaluated rows, then the Article 43 / 47 / 49 declarations, then post-market rows (61, 72). Note where a reviewer would stop and challenge.
