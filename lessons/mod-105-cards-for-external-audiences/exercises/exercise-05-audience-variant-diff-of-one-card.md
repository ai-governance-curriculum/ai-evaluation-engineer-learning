# exercise-05: The Four Audience Variants of One Card

**Estimated effort:** 3 hours

## Objective

Derive the **four audience variants** (public, regulator, third-party evaluator, board) of the canonical system card you have been building through exercises `01`–`04`. The four variants are computed projections of one canonical assurance case, each with its own signed `redaction_manifest`; drift on any of the six load-bearing spine items chapter `07` fixes is a defeater. This exercise makes the derivation and the audit walk mechanical.

## Prerequisites

- Chapter [`07-audience-variants-of-one-card.md`](../07-audience-variants-of-one-card.md); revisit chapter [`06-c2pa-provenance-and-disclosure-tradeoffs.md`](../06-c2pa-provenance-and-disclosure-tradeoffs.md) if the redaction-reason vocabulary is not still fresh.
- Exercises [`exercise-01`](exercise-01-model-card-for-a-regulated-product.md), [`exercise-02`](exercise-02-system-card-composition-from-evidence-tree.md), [`exercise-03`](exercise-03-iso-42005-impact-assessment-slice.md), and [`exercise-04`](exercise-04-c2pa-provenance-manifest-for-genai.md). This exercise reuses and derives from all of them; if a prior artefact is missing, stub it and note the stub in the exercise write-up.
- A JSON / YAML canonicaliser you can call (RFC 8785 JCS or an equivalent) and an Ed25519 signing routine (same tool you used for exercise `01`). Each variant is separately signed.

## Problem statement

You have one canonical case (exercise `02`'s system card is its public variant; the assurance case behind it comes from mod-102). Derive the four audience variants from it using chapter `07`'s three-step derivation rule:

1. Apply the base card template (the public variant is the base).
2. Apply a variant-specific `redaction_manifest` (composed of `redact`, `unredact`, `elaborate`, and `restructure` operations) to produce the regulator, third-party evaluator, and board variants.
3. Freeze, sign, and index each variant as its own content-addressed artefact.

The four variants must (a) satisfy the six load-bearing invariants that stay identical across variants and (b) pass the three-step cross-variant audit walk chapter `07` names.

## Requirements

Produce eight artefacts.

### 1. `variant-public/` (link to prior artefacts if unchanged)

The public variant is the base you have already authored across exercises `01`–`04`. If those artefacts are unchanged, you may reference them by relative path from this exercise's directory and note the reference in `variant-public/README.md`. If you had to touch any field to close a shared-spine invariant (see acceptance criteria), update the artefact in place and note the change in the README.

### 2. `variant-regulator/`

The regulator variant. It contains:

- `redaction-manifest.yaml` — variant-specific manifest. Predominantly `unredact` and `elaborate` operations against the public base. Every operation carries `path`, `operation`, `reason`, and `rationale_content_address`. At minimum: `unredact` the attack payloads (into a referenced-by-content-address bundle, not inline text), the PII-containing eval sets (by pointer + confidentiality declaration), the canary tokens (by pointer + Article 74 confidentiality invocation), the specific supplier names for the top-three training-data suppliers, and the specific FRIA content if in scope. `elaborate` at least the safety-evidence and impact-assessment sections to a level a market-surveillance authority would find complete.
- `head.yaml` — the regulator variant's head. Identical `subject.content_address`, `assurance_case.case_content_address`, `regime.*`, and `evidence_pointers.*` claim values as the public variant; the `redaction_manifest` field points at `redaction-manifest.yaml`; `card.audience: "regulator"`; new content-addresses for the variant-specific `unredact`-only pointers.
- `body.md` — the regulator body. Same section order as the public body; expanded content where `elaborate` operations apply; explicit pointers where `unredact` operations pull in evidence available under Article 74 confidentiality. The body is longer than the public body; anticipate 1.5–2× length.
- `signature.txt` — a fresh Ed25519 signature over the canonicalised head+body pair of the regulator variant. The signature is *not* the same as the public variant's signature.

### 3. `variant-third-party-evaluator/`

The third-party evaluator variant. It contains:

- `redaction-manifest.yaml` — variant-specific manifest. Predominantly `unredact` operations for reproducibility content (bundle content-addresses, seeds, judge prompts, eval-set integrity attestations) and bounded `unredact` for canaries under the evaluation-agreement clause. `elaborate` operations on methodology sections (impact-assessment methodology, safety-evidence methodology) that give the evaluator enough context to reproduce. Redact the board-oriented narrative content the evaluator does not need; this is a `redact` operation with reason `board-audience-only`.
- `head.yaml` — same shared-spine invariants as the regulator variant, plus a `access.evaluation_agreement_content_address` field pointing at the (hypothetical) evaluation agreement that binds the evaluator's access. `card.audience: "third-party-evaluator"`.
- `body.md` — reorganised around chapter `07`'s methodology-forward section order for the third-party variant. It carries reproducibility-bundle pointers, integrity attestations, and the methodology briefs; it does *not* carry the board decision brief.
- `signature.txt` — a fresh signature over the third-party variant.

### 4. `variant-board/`

The board narrative. It contains:

- `redaction-manifest.yaml` — the board variant is the most `restructure`-heavy. Sections are re-ordered around the decision (release / hold / escalate). `redact` operations remove the eval-set-level technical detail. A `restructure` operation adds the decision brief at the top and the traffic-light dashboard.
- `head.yaml` — same shared-spine invariants. If any rounding is applied for presentation (e.g., reporting `0.912` as `91%` in the traffic-light), the head declares the rounding rule (`rounding.rule: "one-decimal-percent"`, `rounding.applied_to: [ ... ]`), and the head still carries the full-precision value. `card.audience: "board"`.
- `body.md` — chapter `07`'s decision-forward section order: decision brief, traffic-light dashboard, escalation options, post-market plan headline, appendix linking back to the public variant for depth. Length target 8–15 pages.
- `signature.txt` — a fresh signature over the board variant.

### 5. `redaction-catalog.md`

An indexed catalog of *every* redaction row across the three non-public variants. Format:

| variant           | path                                                          | operation | reason                          | rationale_content_address |
|-------------------|---------------------------------------------------------------|-----------|---------------------------------|---------------------------|
| regulator         | `safety.attack_payloads`                                      | unredact  | article-74-confidentiality      | sha256:…                  |
| regulator         | `quality_attributes[…].raw_examples`                          | unredact  | article-74-confidentiality      | sha256:…                  |
| third-party       | `reproducibility.bundle_seeds`                                | unredact  | evaluation-agreement-clause-4.1 | sha256:…                  |
| third-party       | `provenance.c2pa.canaries`                                    | unredact  | evaluation-agreement-clause-4.2 | sha256:…                  |
| board             | `impact_assessment.per_finding_details`                       | redact    | board-audience-only             | sha256:…                  |
| board             | `body.section_order`                                          | restructure | decision-forward             | sha256:…                  |
| …                 | …                                                             | …         | …                               | …                         |

The catalog is a *view* over the three variant-specific manifests. Every row of every variant's manifest appears here; no rows appear here that are not in a variant manifest.

### 6. `shared-spine-check.md`

A short document that walks the six load-bearing invariants chapter `07` fixes and shows that they are identical across variants:

- `subject.content_address` — table with one row per variant; all four values are identical.
- `assurance_case.case_content_address` — same.
- Claim values (per key claim on the card) — table with one row per variant; all four values are identical (rounding declared where the board variant applies presentation-layer rounding).
- Evidence-pointer digests — spot-check at least ten pointers across the variants; the digest is identical on all four.
- `regime.*` — the applicable regimes and articles are identical across variants.
- Impact-assessment finding IDs — every `finding_id` on any variant is present with the same ID on the others (subject to redaction of specific finding *details*, not the ID itself).

If any of the six diverges, note the divergence, explain why, and fix the divergence. A note that says "we intentionally rounded the board variant's traffic-light number" is fine only if the head declares the rounding rule and the full-precision value is still there.

### 7. `audit-walk.md`

The three-step audit walk chapter `07` names, executed on your four variants. For each step, show *what a market-surveillance authority under Article 74 would see*:

1. **Compare `subject.content_address` across the four variants.** Result: identical or defect.
2. **Compare reported values of every claim across variants.** Show the comparison table; call out any presentation-layer rounding.
3. **Read every non-public variant's `redaction_manifest`.** Confirm that every difference between the public variant and the non-public variants is enumerated in the variant's manifest. If a delta appears without a manifest row, it is a defeater.

The document ends with a one-line verdict: `AUDIT WALK: PASS` or `AUDIT WALK: FAIL — <reason>`. If the walk fails on any of the three steps, do not simulate a pass; report the failure and remediate before considering the exercise complete.

### 8. `index.md` — the four-variant index

A single index the store's audience-variant index would carry. Format:

```yaml
subject:
  content_address: "sha256:..."
variants:
  - card_id: "..."
    audience: "public"
    head_content_address: "sha256:..."
    body_content_address: "sha256:..."
    redaction_manifest_content_address: "sha256:..."         # empty for public; may be null
    signature: "..."
  - card_id: "..."
    audience: "regulator"
    head_content_address: "sha256:..."
    body_content_address: "sha256:..."
    redaction_manifest_content_address: "sha256:..."
    signature: "..."
  - card_id: "..."
    audience: "third-party-evaluator"
    ...
  - card_id: "..."
    audience: "board"
    ...
```

The index is what a `subject`-scoped query returns; all four variants show up on the same query.

## Starter guidance

- **Author the base once, project three times.** Do not open a fresh editor for each variant. Each non-public variant starts from the public variant + a manifest; apply the manifest mechanically. If you find yourself hand-editing the same paragraph in two variants, you are probably drifting.
- **The redaction manifest is small.** A hundred rows is a large manifest. If your regulator manifest has three rows and each says "we added everything," you have not thought hard enough about what regulators need. If your board manifest has a thousand rows and reads like an outline, you are re-authoring rather than projecting.
- **`elaborate` is not the same as `unredact`.** `unredact` reveals a field the public variant redacted; `elaborate` expands prose the public variant summarised. Use both, but do not conflate them; the reasons and rationales differ.
- **Board `restructure` is load-bearing.** The board variant is the highest-risk variant for silent semantic drift because its section order changes. Every `restructure` operation must be enumerated in the board manifest; a board variant that quietly reorders without a manifest row is broken.
- **Presentation-layer rounding is legal only if declared.** The board variant may render `0.912` as `91%` for the traffic-light. The head still carries `0.912`, and the head declares the rounding rule. A board variant that shows `91%` in the body while the head shows `0.90` is a defect.
- **The audit walk is where the exercise pays off.** Walk it as if you were an Article 74 market-surveillance authority — comparing side by side, looking for silent deltas. If the walk uncovers a shared-spine divergence, fix it upstream (typically in the public variant's head) rather than papering over it in the manifest.
- **Sign each variant independently.** The same signature does not carry across variants; each variant's canonicalised head+body pair produces its own signature. If you sign once and copy the signature to the other three, the derivation is broken.

## Acceptance criteria

You have succeeded if:

- Each of `variant-public/`, `variant-regulator/`, `variant-third-party-evaluator/`, and `variant-board/` is a complete, separately signed variant. Each variant's `head.yaml` carries `card.audience` correctly and a `redaction_manifest_content_address` (empty for public, present for the other three).
- The `redaction-manifest.yaml` in each non-public variant enumerates every operation applied to derive that variant from the base. Every row has `path`, `operation`, `reason`, and `rationale_content_address`.
- `redaction-catalog.md` is a strict view over the three non-public manifests — no rows missing, no rows added.
- `shared-spine-check.md` shows the six load-bearing invariants are identical across the four variants (rounding declared where the board applies it). Any divergence has been resolved, not documented-away.
- `audit-walk.md` executes chapter `07`'s three-step audit walk and reports `AUDIT WALK: PASS` — the walk actually passes on the artefacts you shipped, not on a described-but-not-executed walk.
- `index.md` returns all four variants under one `subject.content_address` query.
- A peer reviewer holding the four variants side-by-side and reading `audit-walk.md` can independently confirm no unauthorised cross-variant drift.

## Stretch goals

- **Simulate a drift and catch it with the walk.** Deliberately introduce a shared-spine divergence — e.g., round a claim value in the regulator variant without declaring the rounding rule, or add an evidence pointer to the board variant that is not on the public variant, or change a `finding_id` between variants. Re-run the audit walk from `audit-walk.md`; confirm it now reports `AUDIT WALK: FAIL — <specific reason>` and names the offending field. Revert the drift.
- **Author the fifth variant — the press release — and note it is *not* one of the four.** A common failure mode chapter `07`'s anti-patterns names is confusing the board variant with a press release. Author a short `press-release-derived-from-public-variant.md`, and document that it is a *derived* artefact from the public variant that is *not* one of the four audience variants. The four audience variants remain four; the press release is a separate downstream artefact drawn from the public variant.
- **Draft the return-and-destroy commitment.** For the third-party evaluator variant, chapter `07` names the return-and-destroy clause that mod-109 will operationalise. Author a two-paragraph `return-and-destroy.md` for the third-party variant that names what the evaluator receives, the retention horizon, the destruction attestation, and the exception cases (e.g., regulatory hold). This is a foreshadow of mod-109.
- **Cross-reference the four variants to their assurance-case discharges.** Each variant discharges assurance-case goals. Chapter `06` notes that the `redaction_manifest` itself discharges `goal:G1.S3.G-audience-variant-faithful`. Author a `case-discharge-map.md` that shows, per variant, which case nodes each variant discharges — and specifically that the redaction manifest of each non-public variant discharges the corresponding faithfulness sub-goal. This ties the exercise back to mod-102.
- **Derive an interim `regulator-refresh` mini-variant.** In a post-market context (mod-110), regulators sometimes request a mini-update between full releases (e.g., a serious-incident notification under Article 73 alongside a status update). Derive a `variant-regulator-refresh/` that shares the shared-spine invariants but carries only the refresh-relevant sections and a `refresh_over: <public-variant-card-id>` field on the head. Note explicitly that this is a *sub-variant* under the regulator audience, not a fifth peer variant.
