# exercise-03: Peer-Track Consumer-Contract Set

**Estimated effort:** 3 hours

## Objective

Produce the **consumer-side evidence-contract set** for the release-gate designed in exercise `01` and the rubric authored in exercise `02`. One signed contract per peer track: `ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`, `ai-infra-security` (plus a thin `ai-governance-analyst` contract row if your scope needs it). Each contract specifies what the gate consumes, in what shape, at what freshness, with what warrant, and — the piece the mod-102 producer schema does not fully cover — *what the gate is committed to consuming* on the other side.

## Prerequisites

- Chapter `04-consumer-contracts-with-peer-tracks.md` (this module).
- Mod-102 chapter `06` (producer-side evidence-contract schema).
- Mod-101 chapter `06` (deferral contract).
- Exercise `01` (`gate-criteria-v1.md`, `gate-variants.md`) and exercise `02` (`rubric-v1.md`) outputs — the contract set is anchored to these.

## Problem statement

Every criterion in the rubric resolves to an artefact produced by a peer track. You have to write the *set of contracts* — one per peer track — that governs those interfaces from the gate's consumer side. Each contract is co-signed (the peer track's lead is a party), versioned, cited by the rubric rows and the SACM `Artifact` elements it governs, and specific enough that the release-gate walker can enforce it mechanically.

The exercise has three parts: (1) enumerate what evidence each peer owes, (2) fill in the per-peer contract using the consumer-side schema, (3) draft the renegotiation-triggers section for one peer and defend it against the peer's likely counter.

## Requirements

Produce five artefacts.

### 1. `consumer-contract-ai-eval-engineer.md`

Cover the AI-eval engineer's evidence obligations to the gate. Use the consumer-side schema from chapter `04` — the producer-side ten fields plus the four consumer-side additions (gate criteria discharged, gate-side acceptance test, gate-side consumption commitment, renegotiation triggers). Coverage:

- Trace / instrumentation, trajectory / tool-use, RAG groundedness, judge, online-eval, and eval-gated CI/CD evidence classes are each addressed.
- The consumer-side consumption commitment addresses **what the gate does not do with raw peer artefacts** (e.g., raw traces with user content are not republished to external audiences without a peer-owned redaction pass).
- Renegotiation triggers name at least three concrete events that would re-open the contract.

### 2. `consumer-contract-model-evaluation-engineer.md`

Cover the model-eval engineer's obligations. Same schema. Coverage:

- Benchmark evidence, calibration, benchmark-integrity attestations, and statistical warrant on robustness metrics.
- The consumer-side commitment addresses **the gate does not choose the estimator**.
- Renegotiation triggers name at least three concrete events (estimator change, benchmark replacement, calibration methodology change, new metric class).

### 3. `consumer-contract-ai-risk-engineer.md`

Cover the risk engineer's obligations. Same schema. Coverage:

- Harm inventory (versioned), adversarial / red-team, guardrail-eval, safety-benchmark, incident-derived learnings.
- The consumer-side commitment names **the harm inventory as the authoritative source** for what harms the gate protects against.
- Renegotiation triggers name at least three concrete events (threat-model change, new jurisdictional obligation, guardrail-eval technique change, mod-110 incident learning that expands the harm inventory).

### 4. `consumer-contract-ai-infra-security.md`

Cover the MLSec peer's obligations. Same schema. Coverage:

- Supply-chain (ML-BOM / SPDX-AI) and provenance, eval-set-integrity, judge-supply-chain pinning, cybersecurity-posture attestation.
- The consumer-side commitment addresses **the gate verifies attestations, not methodology**.
- Renegotiation triggers name at least three concrete events (BOM-schema upgrade, new supply-chain attack surface, security assurance case restructure).

### 5. `contested-renegotiation-defence-memo.md`

Pick *one* renegotiation trigger from any of the four contracts that the peer track's lead is likely to push back on — a trigger that would force the peer into unwanted work — and write the memo defending it. Two-to-three pages. The memo:

- Names the peer, the trigger, and why the gate requires it as a contract clause.
- Cites the framework text or the rubric row that makes the trigger load-bearing.
- Anticipates the peer's push-back — "this forces us to re-do methodology on a schedule you set," "this is out-of-scope for our track," "we don't have the capacity to guarantee this" — and responds on each.
- Names the counter — what happens if the peer refuses to co-sign this clause? What is the gate's disposition (defer the release, downgrade the tier, exception-approval)?
- Names the escalation path (head of AI governance, senior architect, CAIO).

## Starter guidance

- **Anchor to exercise `02`'s rubric.** Every consumer-contract clause should map to at least one rubric row. If a clause covers no rubric row, either the clause is unnecessary or the rubric is under-specified.
- **Do not paraphrase peer methodology.** The consumer contract cites `<PEER>-evidence-contract v1 §<clause>` verbatim. Paraphrasing is what causes the drift chapter `04` warns against.
- **Freshness and cadence are policy, not hopes.** A 7-day freshness on judge-agreement measurement that the AI-eval peer produces quarterly is a broken contract. Talk to the peer track's cadence-of-record (or, in an academic setting, argue from what the track's methodology can realistically produce).
- **The consumption commitment is the piece that keeps trust two-way.** If it is missing, the peer will discover at incident time that the gate did something with their artefacts they didn't sign off on.
- **Contested triggers are the point.** Renegotiation triggers that no peer would push back on are already implicit; the defence memo exercises the ones that force a real conversation.
- **The `ai-governance-analyst` (level 15) contract row is thin.** Not every exercise submission needs one; include it only if your rubric has analyst-produced rows (inventory linkage, jurisdictional watchlist, first-draft cards).

## Acceptance criteria

You have succeeded if:

- Four consumer contracts are present, each using the chapter-`04` schema in full (producer-side fields + consumer-side additions).
- Every consumer-contract clause maps to at least one rubric row from exercise `02`.
- Warrants cite peer methodology by clause identifier, not by paraphrase.
- Consumer-side consumption commitments are written and specific — retention windows, republication rules, and use limitations are named.
- Renegotiation triggers are concrete (at least three per contract) and cite the peer's methodology of record.
- The defence memo names the peer, the trigger, the framework citation, the anticipated push-back and response, and the escalation path.
- A peer lead reading their own contract would be able to sign it, or would raise a specific renegotiation topic — not "this whole document doesn't fit our track."

## Stretch goals

- Author the **peer lead's response** to your defence memo — imagine you are the peer lead and write the reply. Then revise the memo to close the strongest push-back.
- Extend one contract with an explicit **retirement clause** — how the contract is retired when the system leaves the release-assurance program's scope. Preview mod-112.
- Extend one contract with a **cross-peer joint-consumption clause** — the fairness or judge-quality case from mod-102 chapter `06` and chapter `04`'s "cross-peer consistency" section. Two peers, one criterion, one signed joint clause.
- Draft the **contract-diff SOP** the release-assurance program uses when a peer track updates methodology: how the diff is triggered, who reviews, how the SACM `Artifact` elements are updated with the new contract version, and how the change propagates into exercise-01's criterion set.
- Sketch the **third-party layering** (mod-109 preview) — for the highest tier your design covers, name the third-party evaluator whose evidence supplements or supersedes one of the four peer-track contracts. Draft one paragraph on how the third-party evidence layers into the same consumer-contract schema.
