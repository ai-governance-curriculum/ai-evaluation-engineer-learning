# exercise-05: Eval-Set Supply-Chain Clauses With the `ai-infra-security` Peer

**Estimated effort:** 2 hours

## Objective

Contract the **three MLSec artefact classes** from chapter `05` — a contamination attestation (Class A), an exfiltration-control attestation (Class B), and per-artefact supply-chain-security clauses (Class C) — with the `ai-infra-security` peer track, thread them into your reproducibility bundle (exercise `03`) and provenance pack (exercise `04`), and extend the release-gate verifier so a missing, stale, or warrant-failing MLSec artefact blocks the pack.

The exercise is a **table-top** by construction. You are not writing the peer track's methodology (that is out-of-scope depth this program defers to the peer). You are exercising the *interface* — the evidence contract, the artefact shapes, the escalation path, and the walker's cross-check. If you have a peer to pair with, do it live. If you do not, fixture the peer with a small `mlsec-peer/` directory containing the peer's methodology documents and the peer's signing key so the artefacts flow through the shape as if the peer were real.

## Prerequisites

- Chapter [`05-eval-set-exfiltration-and-contamination.md`](../05-eval-set-exfiltration-and-contamination.md).
- Exercises `01` (store), `03` (reproducibility bundle), and `04` (provenance pack) completed.
- Familiarity with the mod-102 chapter `06` evidence-contract shape (the row-per-artefact form: claim, owner peer, artefact, warrant, freshness, escalation). If you have not read that chapter, skim it before starting; the MLSec rows below are the same shape.
- Optional but valuable: a partner playing the `ai-infra-security` peer role. If you can pair with someone who has actually read the peer track's material (Carlini-style canary literature, provider-side data-retention terms, network-egress policy design), the exercise is much sharper. If you cannot, fixture as described below.
- One of the public benchmarks discussed in chapter `05` (MMLU, GSM8K, HumanEval, MATH, or a similar widely-indexed set) available locally as a canonical eval-set your bundle exercises. Public benchmarks are the case where contamination is a live concern and the assurance case has to say so out loud.

## Problem statement

Take the reproducibility bundle you produced in exercise `03`, augmented by the provenance pack from exercise `04`. Extend it with a `data/security/` sub-tree containing four artefact families (Class A contamination attestation, Class B exfiltration-control attestation, four Class C supply-chain-security clauses, and a canary attestation), plus the peer's methodology documents referenced by digest. Draft the evidence-contract rows for each artefact family in the mod-102 chapter `06` shape. Then extend your exercise-04 verifier to walk the MLSec sub-tree — verifying the peer's signature, cross-checking digest references, and enforcing freshness — so a missing or stale attestation blocks the pack.

Where you cannot pair with a peer, fixture the peer role: seed `mlsec-peer/` with a small methodology document per class, a peer signing key, and a runbook you would hand to the peer.

## Requirements

Produce five artefact classes under `data/security/`, a peer fixture directory, a contract addendum, and an extended verifier.

### 1. `data/security/contamination-attestation.json` (Class A)

For at least one eval-set that discharges a hard release-gate criterion in your bundle, produce a signed contamination attestation. It must contain:

- The eval-set digest under test (matching the `dataset` lineage digest in the reproducibility bundle).
- The model digest under test (matching the `model` lineage digest).
- A reference to the peer methodology used (a `mlsec-peer/contamination-methodology.md` you fixture) by digest, with the methodology name — typical choices: n-gram overlap, canary-token probe, log-probability signature, paraphrase detection, or a documented combination.
- The numeric result and its warrant: estimator, threshold, CI. For public benchmarks in this exercise the honest answer is often "contamination detected under threshold T for these examples" — record it faithfully, do not pretend the benchmark is clean.
- The disposition: either "no finding" or the finding-plus-mitigation record (which examples are compromised, whether they can be re-authored, whether the eval-set has to be rotated).
- Freshness: an `attested_at` RFC 3339 timestamp and a `valid_until` — per chapter `05`, per-release-candidate for high-tier work, per-quarter for low-tier.
- Signature: DSSE envelope signed by the peer's key (from the fixture — or the real peer if you paired).

The release-assurance program does **not** sign the attestation's content. Self-signing here means nothing. The peer signs.

### 2. `data/security/exfiltration-attestation.json` (Class B)

For the same run, produce an exfiltration-control attestation covering the run window. It must contain:

- The eval-set digest exercised.
- A reference to the exfiltration-control policy (a `mlsec-peer/exfil-policy.md` you fixture) by digest, naming which controls were in force. At minimum touch on:
  - Provider-side data-retention posture (which endpoint, opt-out status, zero-data-retention flag, contractual reference).
  - Network-egress ACL (Kubernetes NetworkPolicy digest, or the equivalent for your compartment).
  - Log-scrub / log-restrict discipline (scrubber version and scan result over the run window).
  - Compartment isolation (identity, credential scope, storage scope).
  - Judge-side controls (if any).
- The run window (`window_start`, `window_end` RFC 3339 timestamps).
- Observability results: audit-log lookups over the window; anomaly-detection outcomes; any observed near-misses.
- Disposition: "no exfiltration observed" or the observed finding plus mitigation.
- Peer signature (DSSE).

Where a policy control cannot be evidenced in your local environment (you do not run a network-egress ACL, you do not have log-scrub), state the gap explicitly in the attestation body under `unmet_controls[]`. The exercise's value is exposing what the peer would actually have to bring — not synthesising a clean-looking attestation.

### 3. `data/security/supply-chain-clauses/*.clause.json` (Class C)

Four supply-chain-security clauses — one for each of model, evaluator, judge, dataset — that bind the exercise-04 provenance attestations to the peer's supply-chain-security policy. Each clause names:

- The artefact class (`model` / `evaluator` / `judge` / `dataset`) and the artefact digest.
- A reference to the peer's supply-chain policy (a `mlsec-peer/supply-chain-policy.md` you fixture) by digest.
- Which exercise-04 provenance artefacts satisfy which sections of the policy: e.g., "the SLSA attestation and CycloneDX ML-BOM together discharge §3 acceptance criteria for `model`" or "the picklescan + ModelScan clean reports discharge §4 deserialisation-safety criteria." Reference the exercise-04 artefacts by their digests.
- If a policy section is *not* discharged, name the gap explicitly under `unmet_sections[]` — the release-gate criterion consuming this clause should then flag it.
- Peer signature (DSSE) — signed by the peer, not by the release-assurance program.

For the `judge` clause: if the judge is the same artefact as the model (a self-judge configuration), record a documented deferral to the `model` clause rather than duplicating.

### 4. `data/security/canary-attestation.json`

A canary probe attestation covering the eval-set:

- Reference to the peer's canary methodology (`mlsec-peer/canary-methodology.md`) by digest.
- The canary tokens seeded into the eval-set (or their construction rule — chapter `05` deliberately says "high-entropy identifiers"; do not put the raw canaries themselves anywhere your bundle would distribute if the bundle leaves the assurance boundary).
- The probe result: whether the model, at inference on unrelated prompts, ever emitted any canary. Include the FAR / FRR the peer records.
- Freshness and peer signature as above.

### 5. `data/security/mlsec-methodology-refs/` (peer methodology documents)

Three short methodology docs the attestations reference by digest:

- `contamination-methodology.md` — one page describing the method the peer used (n-gram overlap, canary probe, log-prob signature, etc.), the estimator, and the threshold rule.
- `exfil-policy.md` — one page describing the control set the peer runs and the audit-log discipline behind it.
- `canary-methodology.md` — one page describing canary construction, seeding cadence, and the probe protocol.
- (Optional) `supply-chain-policy.md` — one page mapping the four Class-C artefacts (model / evaluator / judge / dataset) to policy sections and acceptance criteria.

These are peer-authored documents. In the fixture they are one-page stubs; in the paired-partner version they are the peer's real docs. Either way they are content-addressed and referenced from the attestations by digest.

### 6. `mlsec-peer/` (peer fixture — if not pairing)

A separate directory that stands in for the peer's environment:

- The peer's Ed25519 (or cosign-compatible) signing key and public key.
- Copies of the methodology documents above.
- A one-page runbook the release-assurance program would hand to the peer: what to sign, when, into which store, and how to escalate.

If you are pairing, replace this directory with a small handoff document to your peer partner naming the same things.

### 7. `contract-addendum.md`

An addendum to your mod-102-shaped evidence contract (if you have one) or a stand-alone contract document containing one row per MLSec artefact class. Row shape:

- **Claim** — the plain-language claim the artefact discharges (e.g., "eval-set `harm-eval-set/v3.2` has not been memorised by release-candidate model `rc-2026-05-07`").
- **Owner peer** — always `ai-infra-security`.
- **Artefact** — file name, format, signing key expected.
- **Warrant** — procedural + statistical (which methodology, which estimator, which threshold).
- **Freshness** — per-release-candidate for high-tier; per-quarter for low-tier.
- **Escalation** — the exact path when the artefact is missing, stale, or contains a finding (who is notified, in what window, and whether the release defers, promotes at a lower tier, or accepts a residual with justification).

Chapter `05`'s "peer runbook interlock" section is the source; you are turning it into a contract you could hand a peer.

### 8. `verify-security.py` — verifier extension

Extend the exercise-04 `verify-provenance.py` (or ship a companion script) that:

- Reads `data/security/` and asserts every attestation exists per the contract's artefact list. Missing → hard fail with the specific claim named in the output.
- Verifies each attestation's DSSE envelope signature against the peer's public key (from the fixture or the paired partner). Missing peer signature or wrong signer identity → hard fail.
- Cross-checks the attestations' `artefact_digest` references against the reproducibility-bundle manifest — the contamination attestation's `dataset_digest` must equal the bundle's `lineage.dataset.digest`; the Class-C clauses' artefact digests must equal the corresponding bundle digests. Any mismatch → hard fail.
- Reads each attestation's `attested_at` / `valid_until`; if the attestation is stale (past `valid_until`, or the current time is outside the freshness window defined in the contract), → hard fail.
- Reads each attestation's `disposition`; if the disposition is a *finding* without a mitigation record referenced back to the release decision, → hard fail with the finding surfaced.
- Extends `provenance-report.json` (from exercise `04`) with per-attestation pass/fail rows and a top-level summary.

## Starter guidance

- **Do the contract first, then the artefacts.** If you build the attestations before the contract, you will inevitably invent claims to fit the artefacts you happen to produce. Draft the contract rows first; then produce artefacts that discharge them; then verify. This is the same discipline as chapter `01`'s "canonicalisation first" and chapter `03`'s "contract before reproducer."
- **Do not backfill peer methodology.** If you cannot honestly say your fixture's contamination methodology is defensible (you are not the peer, you have not read the Carlini paper in depth, you did not choose the estimator's threshold), leave the fixture as a stub that names the methodology and defers detail to the peer. An assurance-program engineer authoring MLSec methodology is out over their skis; the fixture that acknowledges the gap is more honest than the fixture that pretends the gap is closed.
- **Public benchmarks are contaminated by default.** If your bundle uses MMLU / GSM8K / HumanEval / MATH or similar, the contamination attestation's honest disposition is likely "contamination detected." Say so. Then add a `contract-addendum` note that the release-gate criterion consuming this eval-set treats the score as "evidence of retention on a known set" rather than "generalisation to novel examples" — chapter `05`'s public-benchmark assumption. This is the case that chapter `05` was written for; do not paper over it.
- **The peer signs, not you.** Every attestation carries the peer's signature. If you self-sign because you cannot pair, use a *separate* peer key in the fixture — do not reuse the release-assurance program key. This makes the sign-diversity visible in the verifier; self-signed MLSec attestations are what the diversity-of-evidence audit (mod-102 chapter `05`) exists to catch.
- **Store the raw canaries out-of-band.** The canary attestation records that a probe ran; it should not embed the raw canary strings into a bundle that will circulate. Store the raw strings in a compartment (or a note file outside the bundle) and reference by digest.
- **Contamination is a spectrum, not a boolean.** An eval-set can be partially contaminated — some fraction of examples are known-leaked, others are held-out. The attestation should record the counts and the percentage, not a single yes/no. The release-gate criterion consuming the attestation is what decides whether the percentage is acceptable at the release tier.
- **When you are stuck, name it.** If a control the exfiltration attestation would claim (e.g., "network-egress ACL enforced during the run") does not actually exist in your setup, put it under `unmet_controls[]` in the attestation body. The verifier should fail the pack until either the control is implemented or the contract row is amended. That is the correct outcome.

## Acceptance criteria

You have succeeded if:

- `data/security/` contains one contamination attestation, one exfiltration-control attestation, one canary attestation, and four Class-C supply-chain-security clauses, each DSSE-signed by the peer's key (fixture or real), and each referencing a methodology document by digest.
- `contract-addendum.md` records one row per MLSec artefact class in the mod-102 chapter `06` shape (claim, owner, artefact, warrant, freshness, escalation).
- `verify-security.py` runs cleanly on the well-authored pack and fails loudly on each of the following synthetic tampers you introduce and record in your report:
  - The contamination attestation's `dataset_digest` is edited to a different value.
  - The exfiltration attestation's `valid_until` is set in the past.
  - One Class-C clause is signed by the release-assurance program key rather than the peer key.
  - The `canary-attestation.json` is deleted.
- At least one attestation in the pack has an honest **finding** or **unmet control** on the record (this exercise is instructive precisely when the peer's genuine state is exposed rather than papered over). The contract addendum's escalation row shows what the release does next.
- A peer reading the bundle, the contract addendum, and the verifier's report can, in under ten minutes, name where the ownership boundary between the release-assurance program and the `ai-infra-security` peer sits — what the release-assurance program contracts and what it defers.

## Stretch goals

- **Pair with a real peer.** If you have not paired yet, do. Hand your fixture peer's runbook (artefact 6) to the partner playing `ai-infra-security` and have them produce Class A / B / C artefacts against your bundle. The gap between your fixture and their real methodology is the exercise's most valuable output.
- **Second-adapter contamination cross-check.** Run n-gram overlap contamination detection *and* canary-probe contamination detection against the same eval-set + model, and record both in the Class-A attestation. Chapter `05` calls out that diversity-of-evidence is what makes the MLSec sub-argument survive.
- **Real network-egress ACL.** Run your exercise-03 reproducer inside a container with an actual egress-blocking `NetworkPolicy` (or an Envoy egress ACL) and record the policy digest in the exfiltration attestation. Demonstrate that a modified reproducer that tries to phone home is blocked and the block is logged.
- **Held-out companion.** For a public-benchmark eval-set you know is contaminated, author a small held-out companion (50 novel examples authored by you, seeded with canaries) and add the companion's contamination attestation to the pack. Update the release-gate criterion so the *hard* warrant rests on the companion; the public score is *soft* corroborating evidence. This is the chapter `05` discipline in action.
- **Rotation runbook.** Fixture an eval-set rotation: bundle version A uses `harm-eval-set/v3.2`; version A+1 uses `harm-eval-set/v3.3`. The contract addendum documents the rotation trigger (a positive finding, or a fixed cadence), the old-and-new digests, and how the release-cycle criterion set is updated. Demonstrate the verifier accepts the new eval-set once the peer's fresh attestation lands.
- **Threading to the release-gate walker.** Extend the release-gate walker (or its stub, if you have not built one yet — mod-103 chapter `06` is where it lives in the curriculum) so that a missing MLSec attestation causes the specific `GATE-SUPPLY-*` criterion from chapter `04` (and any hard criterion whose evidence rests on the eval-set) to fail. The exercise ends when a bundle without the MLSec pack cannot pass the walker.
