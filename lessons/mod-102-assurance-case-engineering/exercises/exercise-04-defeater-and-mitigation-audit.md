# exercise-04: Defeater and Mitigation Audit

**Estimated effort:** 2 hours

## Objective

Run the **five-pass audit** from chapter `05` against an assurance case *you did not author*, produce a written audit ledger, and defend the top three findings in writing to the case's owner. The point is to build the reviewer's instinct — you are looking for undermining evidence, unstated assumptions, insufficient diversity, defeater / mitigation gaps, and residual-risk problems in a case that reads plausibly on first pass.

This is the applied output of chapter `05`.

## Prerequisites

- Chapter `05-auditing-an-assurance-case.md`.
- Chapter `03` (for the CAE Blocks + Defeaters vocabulary the audit uses).
- Chapter `04` (for SACM identifiers used in the audit ledger).

## Problem statement

You are auditing a submitted release-case. Pick one of the following case sources — you are *reviewing*, not *authoring*, so choose a case whose weaknesses you did not put there yourself:

- **Option A — Peer case.** Swap cases with a classmate or colleague who did exercises `01`–`03` on a different scenario. You audit theirs; they audit yours.
- **Option B — Self-authored incorrect variant.** If you did the exercise `01` stretch goal (an incorrect variant of your own case), audit that variant. Force yourself into reviewer mode by treating the case as one you have never seen; do not silently repair it as you read.
- **Option C — Published public case.** Pick a publicly available AI or ML assurance case (see `resources.md` for pointers to published examples in academia and industry) and audit it. Note that published cases sometimes have known weaknesses the authors have *deliberately* left visible for teaching — that is fine; the audit ledger records what you find.

## Requirements

Produce a single `audit-ledger.md` (or CSV / spreadsheet) plus a short `top-findings-memo.md`.

### `audit-ledger.md`

For each finding, one row with the schema from chapter `05`:

| Field                | Content                                                                                    |
| -------------------- | ------------------------------------------------------------------------------------------ |
| Finding ID           | Unique within your audit.                                                                  |
| Pass                 | Structural / Unstated assumption / Defeater / Diversity / Residual-risk.                   |
| Target               | SACM identifier or case-native identifier of the node the finding targets.                 |
| Statement            | One-sentence description of the issue.                                                     |
| Severity             | Blocking / Elevate / Note.                                                                 |
| Disposition          | Repair / Escalate / Accept-as-assumption / Accept-with-rationale.                          |
| Owner                | Party responsible for closing (release-owner, peer track, external body).                  |
| Deadline             | Date by which the disposition is due (relative to the case's decision date).               |
| Confidence delta     | For residual-risk findings: how much this finding moves your confidence in the top-level claim. |

Coverage minima:

- At least **five findings in pass 1 (structural)** or a written statement that the case is structurally well-formed with the specific checks you ran to conclude that.
- At least **three findings in pass 2 (unstated assumptions)**, each naming a specific load-bearing premise not attached as an assumption node in the submitted case.
- At least **five findings in pass 3 (defeaters and mitigations)**, distributed across at least three different argument nodes, mixing rebutting and undercutting defeaters, each with the mitigation currently in place (if any) and the residual.
- At least **two findings in pass 4 (diversity of evidence)** naming a leaf whose evidence is thin along one or more of the axes (method, party, time, dataset) — with a disposition that either accepts the diversity at this deployment tier or asks for additional evidence, with rationale.
- At least **one finding in pass 5 (residual-risk / confidence-in-argument)** naming the top-level claim's confidence and what specifically load-bears.

### `top-findings-memo.md`

Pick the three highest-severity findings from your ledger and write them up as a memo the case's owner would receive on release-eve. For each finding:

1. **What the finding is** — the plain-language issue, tied to the specific node.
2. **Why it matters at this release-gate** — the release-obligation the case's discharge is now weaker for.
3. **What the recommended disposition is** — repair, escalate, accept-as-assumption with rationale, or block release.
4. **What the case's owner needs from a peer track to close** — the evidence contract row (chapter `06`) that would close the finding.

The memo is deliverable-shaped: it is what you would actually send to the case's owner. Keep it to two pages.

## Starter guidance

- **Do the passes in order.** Do not read pass 5 questions on your first read; you will drift into narrative mode. Start with pass 1 mechanical checks (structural well-formedness), then pass 2 assumption hunt, and so on.
- **The unstated-assumption pass is where beginners underdeliver.** Chapter `05` lists the five common flavours (representativeness, independence, stationarity, monotonicity, threshold-derivation). Walk each flavour against every load-bearing argument in the case — do not skim.
- **Defeater brainstorming needs adversarial mode.** Ask "what would a lawyer for the harmed party say?" and "what would an evaluator paid to find the weaknesses find?" — not "does this look ok?"
- **Diversity is a proportion argument.** A T1 pilot release does not need methodology / party / time / dataset diversity across every leaf. A T3 external release does. Note the deployment tier from the case header before you judge.
- **Confidence rationale is prose, not a score.** You are describing what would move your confidence up or down, not producing a number. If a number falls out (a subjective probability, a semi-quantitative bucket), fine — but the reasoning is what the release-owner reads.
- **If you find yourself repairing the case rather than recording the finding, stop.** The audit ledger is a *record*; the disposition assigns the repair to someone (often not you). Chapter `05`'s discipline is exactly this separation.

## Acceptance criteria

You have succeeded if:

- The audit ledger meets or exceeds the coverage minima above.
- Every finding names a specific target node in the case (no generic "the case is weak" findings).
- Every finding has a severity and a disposition; no finding is un-owned.
- Pass 3 findings mix rebutting and undercutting defeaters and name the mitigation currently in place (if any) and the residual (if any).
- Pass 4 findings state the deployment tier and defend the diversity disposition against it.
- Pass 5 finding produces a written confidence rationale for the top-level claim that names what specifically load-bears.
- The top-findings memo is deliverable-shaped, two pages or fewer, and each finding maps to a proposed peer-track evidence-contract row.

## Stretch goals

- Persist the audit ledger as SACM annotations on the target nodes (per chapter `04`) so the ledger survives across release cycles alongside the case.
- Cross-audit — re-do the audit against a *different* case (peer's, or a published public one) and compare which findings recur across cases. Chronic findings become program-level curriculum in mod-112.
- Write the case owner's *response memo* — for each of your top-three findings, draft what the owner might reasonably reply. This forces you to strengthen findings that would not survive push-back.
- Extend the audit with a **framework-conformance pass** — check the case against ISO/IEC/IEEE 15026-2 content requirements and note any content-requirement item the case omits.
