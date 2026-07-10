# exercise-01: Model Card for a Regulated Product

**Estimated effort:** 3 hours

## Objective

Write an **assurance-card model card** for a specific regulated-product scenario. The card must extend the Mitchell / Gebru / Hugging Face base into the shape chapter `02` fixed: machine-readable head + human-readable body, evidence-pointer bindings, discharges-mapping into an assurance case, redaction-manifest discipline, producer signature. This is the *model* variant of the card; exercise `02` composes it into a *system* card.

## Prerequisites

- Chapters [`01-lineage-from-mitchell-and-gebru.md`](../01-lineage-from-mitchell-and-gebru.md) and [`02-assurance-card-shape-for-external-audiences.md`](../02-assurance-card-shape-for-external-audiences.md).
- Familiarity with the head/body split; the base Mitchell sections (§1–9) and the base Gebru sections (§1–7).
- A local scripting environment that can canonicalise JSON or YAML (RFC 8785 JCS or an equivalent) and produce an Ed25519 signature (`pynacl`, `cryptography`, `libsodium`, or the language equivalent).

## Problem statement

Pick one of the three scenarios below. Author the model card for the *base model* underlying the scenario as a machine-readable head plus a human-readable body. Include a `redaction_manifest` (empty for the public variant is fine); include a producer signature over the canonicalised head+body pair; ensure every claim in the body has a corresponding `evidence_pointers` entry in the head. The exercise does *not* require you to compose the system card yet — that is exercise `02`.

### Scenario A — EU AI Act Annex III(3)(a), education

A classification model that supports admission decisions for a professional-training programme in an EU member state. The model receives a candidate profile and returns a recommended acceptance / waitlist / rejection with a calibrated confidence score. Deployed as a decision-support tool with a mandatory human reviewer per Article 14. In scope for Articles 9, 10, 11, 13, 14, 15, 17, 26 (deployer), and Article 27 (FRIA for public authorities and certain private deployers).

### Scenario B — FDA Software as a Medical Device (SaMD), Class II

An imaging-based screening model for a specific pathology, cleared under the FDA 510(k) pathway and shipped with a Predetermined Change Control Plan (PCCP) that defines the change envelope. Deployed as an assistive read (radiologist-in-the-loop) at named partner health systems. In scope for FDA GMLP guiding principles, 21 CFR Part 820 (Quality System Regulation), and the PCCP boundary conditions. The card's readers include the FDA reviewer, the deploying health system's compliance office, and the QA lead of the ML platform team.

### Scenario C — SR 11-7 model-risk banking

A credit-adjacent classification model deployed by a US bank into the credit decisioning stack, in scope for Federal Reserve SR 11-7 model-risk management (`model-inventory`, `annual-validation`, `independent-review`, `ongoing-monitoring`). The card is the primary artefact the second-line model-risk management (MRM) function reviews before the model is placed into production, and it feeds the annual validation cycle thereafter. Fair-lending obligations (ECOA / Regulation B) and adverse-action-notice content are in-scope for the disclosure narrative.

Pick one. If you have a real product in scope, you may substitute it as long as it maps to one of the three regulatory regimes (or a comparable one) and you document the substitution.

## Requirements

Produce four artefacts.

### 1. `head.yaml` (or `head.json`)

The machine-readable head. Follow chapter `02`'s shape at minimum:

- `card.schema_version`, `card.card_id`, `card.audience: "public"`, `card.produced_at`, `card.producer`.
- `subject.kind: "model"`, `subject.model_id`, `subject.content_address`.
- `assurance_case.case_id`, `assurance_case.case_content_address`, `assurance_case.discharges` — the specific case-node identifiers this model card supports.
- `regime.*` — the applicable regulatory regime, with specific articles / clauses / rules cited (per your chosen scenario).
- `evidence_pointers.*` — one entry per body claim, each with `metric`, `value`, `ci_95` (where applicable), `evidence_content_address` (a placeholder `sha256:…` is fine for the exercise; you do not need to produce a live store), and `sacm_artifact_id`.
- `redaction_manifest.variant: "public"`, `omitted_fields: []`.
- `provenance.producer_signature.*`, over the canonicalised head+body.

You do not need a running evidence store; placeholder digests are acceptable if you are explicit that they are placeholders. What matters is that the head is *structurally* valid — a validator could enforce the invariants from chapter `02`.

### 2. `body.md`

The human-readable body. Mirror chapter `03`'s six-section structure but scoped to the *model* (not yet the system):

- §1 Model identity and version.
- §2 Intended purpose, appropriate use, out-of-scope use — bound to your chosen regulatory regime's specific obligation (Article 13, Article 27, FDA "intended use," or SR 11-7 model-purpose statement).
- §3 Training and evaluation data — datasheet paraphrase and content-address pointers.
- §4 Quality attributes — ISO/IEC 25059 spine, per chapter `05` — with at least three quality attributes reported, each with metric + CI + threshold + rationale.
- §5 Safety-evidence summary — short; a full system-safety summary lives in exercise `02`.
- §6 Deployment-tier decision — for this scenario, name the deployment mode and the operational constraints (this is more nuanced than "tier" for non-frontier systems).

Length: 12–25 pages equivalent when rendered. Every claim in the body has an `evidence_pointers` entry in the head; grep-check this before you sign.

### 3. `assurance-case-nodes.md` (or `.json`)

A short document (or JSON file) that names the specific assurance-case nodes the card discharges — enough that a peer reviewer could construct a plausible GSN case from your list. Format:

```
goal:G1        — the release of <model> discharges applicable obligations.
goal:G1.S1.G-<article>-<topic>  — <article> obligation discharged by <evidence>.
```

You do not need to draw the case as GSN or persist it as SACM; you need to name the nodes and describe the argument shape.

### 4. `signature-manifest.json`

The Ed25519 signature over the canonicalised head+body pair, plus:

- The producer's public key (or key-id).
- The canonicalisation rule applied (JCS, sorted keys, LF newlines, UTF-8 no BOM).
- The signature bytes (base64).
- The verification command a reviewer would run to reproduce the check.

## Starter guidance

- **Start from the head.** Sketching the head — even in placeholder form — is what forces you to name the evidence pointers and case nodes. The body is easier to write once you know what claims it has to defend.
- **Pick a real regime for your scenario.** If you chose EU AI Act Annex III, read Articles 9–15 once before you start §2 of the body; the vocabulary "intended purpose," "foreseeable misuse," and "level of accuracy" are directly from the text. If you chose FDA GMLP, read the guiding principles page. If you chose SR 11-7, read the "Model" definition and the model-lifecycle activities (development, implementation, use).
- **Do not invent metric values.** For a fictitious model, name plausible metric *shapes* (macro-F1 for a classifier; AUC for a screening model; approval-rate parity for a credit model) but do not attach specific numbers unless you clearly mark them `<example>`. A card with invented specifics reads as though the underlying evidence exists.
- **Do not skip the CI.** Every metric row in §4 carries a CI. This is chapter `05`'s hardest invariant; get it right on the first artefact you write.
- **Redact honestly.** For scenarios B and C, the training data disclosure is limited by law (device / bank internal data); use the `redaction_manifest` (empty for public variant) to note that a regulator variant would carry additional detail, and move on. Do not fabricate.
- **The producer signature is over the canonicalised head + body.** Concatenate the canonical JCS of `head.yaml` (after YAML→JSON) with the canonical bytes of `body.md` (LF newlines, UTF-8 no BOM) — write the concatenation rule down as part of the signature manifest.

## Acceptance criteria

You have succeeded if:

- `head.yaml` conforms to chapter `02`'s schema shape at every invariant (unique `card_id`; `subject.content_address` populated; every body claim has an `evidence_pointers` entry; `assurance_case.discharges` names real nodes from `assurance-case-nodes.md`; `regime.*` cites specific articles / clauses / rules).
- `body.md` covers all six sections; §4 has at least three quality-attribute rows with metric + CI + threshold + rationale; §2 explicitly enumerates out-of-scope uses; §3 paraphrases datasheet content and cites content-addresses (placeholder digests are acceptable if marked).
- `assurance-case-nodes.md` names goal identifiers that mesh with the head's `discharges`; a reviewer could sketch the GSN case from your list without inventing nodes.
- `signature-manifest.json` verifies against the canonicalised head+body pair; the verification command works when run.
- A peer reviewer reading only your four artefacts can walk from any claim in §4 of the body to (a) the head pointer, (b) the placeholder digest, and (c) a case node — the six-step walk of chapter `03`.
- The card obeys the chapter `01` invariant: it is a Mitchell-flavored artefact (nine sections' worth of concerns), the disaggregation move is present in §4, and the out-of-scope-use list is a first-class field in §2 (not a footnote).

## Stretch goals

- **Wire it to a live evidence store.** If you completed mod-104 exercise `01` (content-addressed evidence store), ingest one placeholder eval-record into that store, replace one `evidence_pointers` digest with the real one, and run the byte-verification script from mod-104 exercise `01` against the card.
- **Author the FRIA specialisation.** For scenario A, produce a `head.yaml`-shape file for the Article 27 FRIA specialisation (chapter `04`'s pattern): same subject, same case, with the FRIA-specific fields (categories of natural persons affected, human-oversight measures, escalation arrangements) filled in. Cite the specific Article 27 sub-paragraphs each field discharges.
- **Author the machine-readable YAML frontmatter in Hugging Face `ModelCard` shape** (`huggingface_hub.ModelCard`) as a *second* representation of the head. Compare what fields survive the round-trip and what fields are enterprise-additions.
- **Author a plain-language addendum for scenario A.** Article 13 requires transparency provisions accessible to affected persons; write a two-page plain-language card annex that a candidate submitting an application would receive.
- **Cross-tab the head against ISO/IEC 42001 clauses.** Add an `iso_iec_42001_clause_map` block to the head that maps each `evidence_pointers` entry to the specific ISO/IEC 42001 clause it supports (7.5, 8.1, 8.2, 8.3, 9.1, 9.2). This foreshadows mod-106 (cross-jurisdictional obligation mapping).
