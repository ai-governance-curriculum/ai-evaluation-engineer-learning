# exercise-05: Evidence Contract Routing

**Estimated effort:** 2 hours

## Objective

Produce the **evidence-contract set** for the assurance case authored in exercises `01`–`03`. Every leaf claim in the case gets one signed evidence-contract row, routed to the correct owner peer track (analyst L15 / risk L25 / AI-eval L30 / model-eval L30 / MLSec L35 / third-party evaluator), with the artefact, warrant, freshness policy, cadence, sign-off party, framework citations, and escalation path filled in. Then defend one contested contract row against the peer lead who would raise it.

This is the applied output of chapter `06`, and it is the module capstone.

## Prerequisites

- Chapter `06-evidence-contracts-and-routing.md`.
- Mod-101's deferral contract exercise output — the evidence contract is a specialisation of that broader deferral contract to the leaves of an assurance case, so re-read it before starting.
- Exercises `01`–`03` outputs — the case, the CAE recast, and the SACM v1 instance.

## Problem statement

Every leaf in the assurance case from exercises `01`–`03` discharges to an artefact produced by a peer track. You have to write the set of contracts that governs those interfaces. Each contract is a governed artefact — versioned, signed, cited by the SACM `Artifact` elements it produces — and each contract is defensible against the peer lead who has to sign it.

The exercise has three parts: (1) enumerate the leaves and route them, (2) fill in the per-leaf contract row for every leaf, (3) pick one contested row and write the memo you would send to the peer lead to defend it.

## Requirements

Produce two artefacts:

### 1. `evidence-contract-set.md` (or CSV / spreadsheet)

For every leaf claim in the case, one contract row using the schema from chapter `06`:

| Field                     | Content                                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Claim identifier          | The SACM `Claim.id` from exercise `03`.                                                                        |
| Owner peer track          | analyst L15 / risk L25 / AI-eval L30 / model-eval L30 / MLSec L35 / third-party.                                |
| Artefact                  | Named, versioned artefact (not a category).                                                                    |
| Format / storage          | File format(s), storage location, digest scheme, retention.                                                    |
| Warrant                   | Statistical or procedural warrant, cited to the peer track's own evidence-contract clause where applicable.     |
| Freshness policy          | Max age at release-gate.                                                                                        |
| Cadence                   | Per-release-candidate / per-quarter / on-event.                                                                 |
| Sign-off party            | Named role.                                                                                                     |
| Framework citations       | Applicable NIST AI RMF sub-category, ISO/IEC 42001 clause, EU AI Act article, sector rule, etc.                 |
| Escalation                | What the release-gate does for missing / stale / warrant-failing artefacts.                                     |

Coverage minima:

- Every leaf in the case has a row. If exercise `01` developed one branch fully and left others at first-level sub-goal, use judgement to add plausible leaves for at least the other first-level sub-goals — the exercise is about coverage across the ownership map, not sheer node count.
- At least **one row per peer track** in the ownership map (analyst L15 / risk L25 / AI-eval L30 / model-eval L30 / MLSec L35). Away-goal leaves that point to a peer module still get a row; the row just points to the peer case's version and warrant clause.
- At least **one third-party row** — an independent evaluator, notified-body conformity assessor, or Big-Four assurance firm — if the case has a leaf at a deployment tier or under a framework that expects independent evidence (Article 55 GPAI, SR 11-7 independent validation, EU AI Act Article 43 conformity assessment).
- At least **one contested row** — a leaf where the routing is not obvious. Chapter `06`'s "when routing is contested" section named fairness, judge quality, and threshold as recurring contested cases; add another if your scenario has one.

Each row has to be actionable in a scheduling sense — cadence, freshness, and sign-off are named, not blank. Framework citations use exact identifiers (`EU AI Act Article 15(1)(a)`, `NIST AI RMF MEASURE-2.5`, `ISO/IEC 42001 clause 8.3`), not topical shorthand.

### 2. `contested-row-defence-memo.md`

Pick one contested row and write the memo you would send to the peer lead to defend the routing. Two-to-three pages, deliverable-shaped. The memo must:

- Name the leaf claim, the artefact, and the peer lead being asked to own it.
- State *why* the artefact belongs on that peer's desk — cite the framework's expectation, cite the peer track's ownership per mod-101's deferral contract, and cite the specific chapter `06` disambiguation rule if applicable.
- Anticipate the peer lead's likely push-back — "this is not my methodology," "this belongs on party X's desk," "the warrant you are asking me to carry is out-of-scope for my track" — and respond to each in writing.
- Name the **counter-position** — what would happen if the peer lead refused to sign the contract? What is the release-gate's disposition? What is the next escalation up the ladder (release-owner, head of AI governance)?

## Starter guidance

- **Start from the SACM v1 leaves, not from the ownership map.** The point is to walk *every* leaf and *route* it; if you start from the ownership map, you will forget leaves.
- **Do not sneak methodology into your contract.** The contract cites the peer track's evidence-contract clause for warrant; it does not re-derive the estimator. If a leaf's warrant reads "bootstrap CI 95% per-class F1" and you have not read the model-eval track's evidence-contract to know that MOD-EVAL v1 §4 is the right clause, go read it (or the peer's equivalent standing document).
- **Freshness and cadence are release-cycle policy, not tossed-off numbers.** A 14-day freshness that no peer track can operationally hit is a broken contract. Talk to the peer track (or, in an academic setting, argue from the peer track's known cadence) before you commit.
- **Contested rows are the point.** If every row is uncontroversial, you have either mis-scoped the case or hidden the ambiguity. The audit pass (`05`) will surface it; better it surface here.
- **The defence memo is a document you would actually send.** No "because I said so." Every claim in the memo cites a framework, a deferral contract, or a case-specific fact. Be prepared to be pushed back on in a real meeting.

## Acceptance criteria

You have succeeded if:

- Every leaf in the case has a row; every row has all schema fields populated with actionable content.
- Every peer track named in mod-101's deferral contract that would produce evidence for this case has at least one row.
- At least one row is a third-party (mod-109 preview) if the case scope calls for it.
- Warrants cite the peer track's own evidence-contract clause; freshness and cadence are named; sign-off party is a specific role; framework citations use exact identifiers.
- The contested-row defence memo names the leaf, the peer, the framework citation, the disambiguation rule, the anticipated push-back and response, and the escalation path if the contract is refused.
- No row invents evidence a peer cannot in principle produce (e.g., asking the analyst for a bootstrap CI, or asking the risk engineer for the estimator's statistical warrant).
- The memo would survive a 20-minute meeting with the peer lead.

## Stretch goals

- Persist the contract set as `Artifact` metadata inside `sacm-v1.json` from exercise `03` so the contracts are traceable from the case rather than living in a parallel file. Update `sacm-v2.json` to show a contract-version change and its downstream evidence-node effect.
- Author the **peer lead's response** to your defence memo — imagine you are the peer lead and write the reply. This is a good way to find weaknesses in the defence memo.
- Extend the contract set with **retirement clauses** — what happens to the contract when the system is decommissioned, per ISO/IEC 42001 lifecycle expectations and per the peer track's retention policy.
- Draft the **program charter paragraph** (mod-112 preview) that references the evidence-contract set as a governed artefact of the release-assurance program.
- Chain to the project-101 capstone by building this contract set on a case sized for that project — the artefact is directly reusable.
