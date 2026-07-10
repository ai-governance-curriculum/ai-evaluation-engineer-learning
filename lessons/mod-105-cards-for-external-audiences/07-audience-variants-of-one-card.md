# The Four Audience Variants of One Card

## Motivation

An assurance card has four external audiences (chapter `02` named them; chapter `06` fixed the redaction discipline). This chapter closes the module by making the derivation from a single canonical case to the four audience variants a mechanical, defensible operation — not four separate authoring efforts.

The failure mode this chapter avoids is *variant drift*. When each variant is authored independently, the public variant, the regulator submission, the third-party evaluator handoff, and the board narrative slowly disagree — a number is rounded here, a caveat softened there, a mitigation forgotten in the summary. Six months later, a market-surveillance authority puts the four variants side by side under EU AI Act Article 74 and finds that the same release said four different things. The card is not defensible.

The derivation-from-one-case rule fixes this. Every variant is a projection of the same canonical case with a variant-specific `redaction_manifest`; the projections are computed, not authored twice.

## The four audiences, in one paragraph each

**Public.** The world's readers: downstream deployers, journalists, researchers, civil-society reviewers, competitors. Their reading budget is short (five minutes for most, an hour for the researcher). Their access is unrestricted. Their trust in the card depends on transparency, comparability, and the absence of felt gaps. The public variant is the *default* — it is the widest disclosure the program can defensibly ship.

**Regulator submission.** A market-surveillance authority (EU AI Act Article 74), a notified body (Article 43 conformity assessment), the FDA (device software), the FTC (unfair-or-deceptive-practices scope), a national supervisory authority (GDPR / AI-specific), or a sector regulator (SR 11-7 for banking; DORA for financial resilience). Their reading budget is long; their questions are specific. Their access is regulated by law — confidentiality provisions apply and they are permitted content the public variant redacts. The regulator variant is the *most complete* variant.

**Third-party evaluator handoff.** An accredited independent evaluator — [UK AISI](https://www.aisi.gov.uk/), [US AISI](https://www.nist.gov/aisi), a notified body's evaluator, [METR](https://metr.org/), [Apollo Research](https://www.apolloresearch.ai/), an academic-lab evaluator, an industry consortium like [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/). Their reading budget is medium; their goal is *reproduction* — they will run the reproducibility bundle (mod-104 chapter `03`) and independently verify the claims. Their access is bounded by an evaluation agreement (mod-109) that governs what they see, what they may publish, and what they must return. The variant is the *reproducibility-shaped* variant.

**Board narrative.** An internal accountable body — the CEO's decision briefing, the board risk committee, the audit committee, the AI safety advisory board, the deployment-oversight body. Their reading budget is *very* short (5–15 pages including the appendix). Their goal is a decision (release / hold / escalate). Their access is unrestricted internally. The board variant is the *decision-shaped* variant.

The claims are consistent across the four; the disclosure levels differ.

## The derivation rule

There is one canonical case for a release (mod-102 chapter `04`; SACM-persisted). The four variants are derived from the case by three steps.

### Step 1 — apply the base card template

The base template is the public variant. It contains every section chapters `02`–`06` fixed: identity, intended purpose, data, quality attributes, impact assessment, safety-evidence summary, deployment-tier decision, post-market plan, change control, provenance / disclosure discipline. The head carries `evidence_pointers` for every claim in the body.

At the end of Step 1, you have a *public assurance card* whose signature closes the redaction position as the *widest disclosure the program can defensibly ship*. Any subsequent variant is a diff over this.

### Step 2 — apply a variant-specific `redaction_manifest`

Each non-public variant carries a `redaction_manifest` (chapter `06`). The manifest is a signed, content-addressed artefact — small; a hundred rows is a large one. Each row names:

- `path` — the section-and-field path in the base card the row operates on.
- `operation` — one of `redact`, `unredact`, `elaborate`, `restructure`.
- `reason` — the redaction policy row that applies.
- `rationale_content_address` — the specific rationale for this row.

**The regulator variant's manifest** is composed almost entirely of `unredact` operations against the public variant, along with `elaborate` operations that expand section content the public variant had summarised. It carries additional evidence pointers into the store — specific attack payloads, PII-containing eval sets, canary tokens under confidentiality provisions, specific supplier names, specific vulnerability reproductions. It generally *does not* restructure — the section order and headings mirror the public variant, so the regulator can hold both side by side and compare.

**The third-party evaluator variant's manifest** is composed of `unredact` operations for reproducibility content (reproducibility bundle content-addresses, seeds, judge prompts, eval-set integrity attestations) and *bounded* `unredact` operations for canaries under the evaluation agreement. The variant is often augmented with `elaborate` operations on the methodology sections (chapter `04` and `05`) that give the evaluator enough context to reproduce. It typically redacts the *board-oriented* narrative sections that a third-party evaluator does not need.

**The board variant's manifest** is composed of `restructure` operations — sections re-ordered around the decision the board is making (release / hold / escalate) — and `redact` operations that remove the eval-set-level technical detail. It is *augmented* with a decision briefing at the top (the tier decision, the residual-risk position, the escalation options) and a per-quality-attribute traffic-light summary. The board variant does *not* elaborate; if a topic requires more than a paragraph, the variant links back to a section of the public variant rather than duplicating.

At the end of Step 2, you have three additional variants, each a signed projection of the canonical case with an explicit redaction manifest.

### Step 3 — freeze, sign, and index

Each variant's head is canonicalised, signed by the card producer, and ingested into the evidence store (mod-104 chapter `01`) as its own content-addressed artefact. The store's index (mod-104 chapter `01`, index columns extended) carries a row per variant that names the `card_id`, the `audience`, and the `redaction_manifest_content_address`. The four variants are linked by their shared `subject.content_address` — a query on the subject returns all four variants.

The invariant Step 3 enforces: every variant is a separate, signed, content-addressed artefact. Editing one does not touch the others; each variant is walkable in isolation.

## What each variant *actually looks like*

Four rapid sketches. Each is illustrative; the precise section list is program-specific.

### The public variant — a Mitchell-shaped card, extended

Section order (public-variant-optimised):

1. System identity and version.
2. Intended purpose, appropriate use, and out-of-scope use.
3. Training and evaluation data (categories; datasheets by name/digest).
4. Quality attributes — ISO/IEC 25059 spine (chapter `05`).
5. Safety-evidence summary — categories, rates, taxonomies; payloads redacted.
6. Impact-assessment summary — ISO/IEC 42005 findings by ID and category; specific stakeholder details redacted where necessary.
7. Deployment-tier decision — the tier, the category rates, the operational constraints.
8. Post-market plan — signals, thresholds, escalation contacts.
9. Change control — versioning, deprecation, retention.
10. Provenance and disclosure — C2PA position (chapter `06`), watermarking, verification endpoint.
11. Access — how a reader with a specific question can reach the program (contact, structured intake, coordinated-disclosure address).

Reader budget: 30–60 minutes. Length: 20–60 pages depending on system complexity.

### The regulator variant — the full disclosure

Section order (mirrors public variant, adds and unredacts):

- Same eleven sections.
- Every eval report, every red-team engagement report, every impact-assessment finding, every guardrail-eval report *by content-address* and available on request.
- All attack payloads, all PII-containing eval sets, all canary tokens (under Article 74 confidentiality; not published).
- The specific supplier names and licensing terms; the specific contamination fingerprint data.
- The specific FRIA (EU AI Act Article 27) content, if in scope.
- The full change-log across releases and the retention artefact map for Article 18.

Reader budget: hours-to-days. Length: 100+ pages plus reproducibility bundles by reference.

### The third-party evaluator variant — the reproducibility-shaped card

Section order (methodology-forward):

1. System identity, versions, and access credentials for evaluation (bounded to the evaluation window).
2. Reproducibility bundles — each in scope, by content-address, with the harness and container-image manifests.
3. Eval-set integrity attestations — mod-104 chapter `05`, with canary access under the evaluation agreement.
4. Quality-attribute mapping brief (chapter `05`) — the metric-to-attribute rationale.
5. Impact-assessment methodology (chapter `04` §Impact-02) — the rubrics, the scoring rows, the participant-role list.
6. Safety-evidence methodology — the red-team methodology, the taxonomy, the payloads under the agreement.
7. Deployment-tier framework — how the tier was assigned and what evaluations drove it.
8. Handoff schedule and return-and-destroy commitment.

Reader budget: hours-to-days. Length: 30–80 pages plus bundles.

### The board narrative — the decision-shaped card

Section order (decision-forward):

1. **Decision brief.** The recommended decision (release / hold / escalate), the tier assignment, the residual-risk position in one paragraph, the top three defeaters and their status.
2. **Traffic-light dashboard.** Per-quality-attribute status (green / amber / red) against threshold with the trend against the prior release.
3. **Escalation options.** What the board can decide, what each option triggers, and the accountable role for each.
4. **Post-market plan (headline).** The signals that would re-open this decision.
5. **Appendix — links back to the public variant** for any section the board wants to read at depth.

Reader budget: 15–30 minutes for the main pack, an hour for the appendix reader. Length: 8–15 pages.

## What has to stay identical across all four variants

Six things do not change between variants. They are the load-bearing spine that keeps the four projections faithful.

- **The canonical case.** All four variants discharge case nodes from the same case (mod-102). The `assurance_case.case_content_address` in each head is identical.
- **The subject content-address.** All four variants describe the same system version at the same digest. The `subject.content_address` is identical.
- **The claim values.** A metric reported as `macro-F1 = 0.912` on one variant is `0.912` on all four; rounding is allowed only in the presentation layer of the board variant, and the head still carries `0.912`. If rounding is applied, the variant declares the rounding rule.
- **The evidence-pointer digests.** The evidence node behind a claim is the same content-address on every variant. A regulator opening the regulator variant reads the same digest a researcher opening the public variant reads.
- **The regime declarations.** The applicable regulatory regimes (`regime.eu_ai_act`, `regime.iso_iec_42001`, `regime.iso_iec_42005`, `regime.iso_iec_25059`) are identical across variants. The variants disagree on *what to disclose*, not on *what applies*.
- **The impact-assessment finding IDs.** A finding `imp:IAI-2026-05-07:F-014` on the public variant is the same finding under the same ID on the regulator, third-party, and board variants. Some details of the finding may be redacted (specific stakeholder identities), but the ID and the severity/likelihood classification are the same.

If any of the six diverges across variants, the derivation has broken and the audit-walk fails.

## The audit walk across variants

A market-surveillance authority under EU AI Act Article 74, holding all four variants side by side, expects to walk in three steps and find no drift:

1. **Compare the `subject.content_address` across variants.** All four match the same system version.
2. **Compare the reported values of every claim across variants.** Numbers are identical or (in the board variant) round-declared.
3. **Read the `redaction_manifest` for each non-public variant.** Every difference between variants is enumerated and rationalised.

If the walk passes, the four variants are *defensible together*. If the walk fails, the entire card family is a defeater.

## Interaction with mod-109 — the third-party evaluator interface

Mod-109 walks the third-party evaluator handoff at depth. The third-party variant of the card is the *first artefact* handed to the evaluator; mod-109's evaluation agreement is what binds their access; mod-109's reproducibility contract is what the variant's bundle pointers discharge. This chapter does not duplicate mod-109's engagement lifecycle; it fixes what the variant carries so that mod-109's handoff is walkable.

The rule that connects the two: an evaluator who receives the third-party variant should be able to reproduce every quality-attribute metric in the card within its published CI. If the evaluator cannot reproduce, the card is not walkable and the case has a defeater; if the evaluator can reproduce but reports a different result under adversarial conditions, the case still stands but a new defeater has been raised (chapter `05` of mod-102 handles the defeater lifecycle).

## Anti-patterns

- **Authoring four variants in parallel.** The variants drift; the audit walk fails. The base card is authored once, the redaction manifests are authored per variant, and the projections are computed.
- **Presenting a "regulator version" that is actually just the public version.** If the regulator variant is a copy of the public variant with no `unredact` operations, the regulator has received nothing extra and the confidentiality regime has bought the program nothing. The regulator variant is the *most complete* variant on purpose.
- **A board variant that is a compressed public variant.** The board reads for a decision, not for a summary. The board variant restructures around the decision options; if the board variant is only the public variant with sections shortened, it is not serving its audience.
- **Losing the shared spine.** If a number is different across variants, the card family is broken. This is the highest-severity defeater a card can carry; the release should not proceed until it is resolved.
- **Editing without re-signing.** Editing any variant invalidates its signature; a new content-address is required. Chapter `06` of mod-104 named the signing layer; here it is enforced per variant.
- **Redaction without inverse-recovery.** A regulator variant that redacts a field the regulator's regime requires is a defeater against the regulator submission. The redaction manifest reads to the regime the variant serves.
- **Confusing the board variant with a press release.** The board variant is an internal decision artefact and is *not* published. A press release is an entirely separate artefact drawn from the public variant; it is not one of the four audience variants this chapter covers.

## Summary

- One canonical assurance case; four audience variants derived by applying variant-specific `redaction_manifest`s to the public-variant base template.
- The four audiences are public (default disclosure), regulator (fullest disclosure), third-party evaluator (reproducibility-shaped), board (decision-shaped).
- Six things stay identical across variants: canonical case, subject content-address, claim values, evidence-pointer digests, regime declarations, impact-assessment finding IDs.
- Each variant is separately signed, content-addressed, and indexed; a subject query returns all four.
- The audit walk across variants is a three-step comparison the regulator can do side-by-side; drift on any of the six load-bearing spine items is a defeater.
- Chapter `07` closes the module. The next modules (mod-106 cross-jurisdictional obligation mapping; mod-109 third-party evaluator interface; mod-110 post-market surveillance) pick up threads this chapter set: mod-106 the regime declarations, mod-109 the third-party variant's engagement lifecycle, mod-110 the post-market plan.
