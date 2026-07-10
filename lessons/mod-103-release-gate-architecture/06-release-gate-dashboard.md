# The Release-Gate Dashboard the On-Call Reads Before Approval

## Motivation

The runbook (chapter `05`) is what the on-call executes; the dashboard is what the on-call *reads*. It answers a small, focused question: *can I sign this release right now, and if not, what is the specific blocker?* Nothing on the dashboard is decorative. Every field maps to a criterion, a peer contract, a runbook trigger, or an AIMS-clause hook. A dashboard that shows more than the on-call needs is a dashboard that hides the blocker; a dashboard that shows less is a dashboard that requires side-channel querying to sign.

Three failure modes motivate a designed dashboard rather than a grown one.

The first is **status-sprawl**. Metrics accumulate over incidents; the dashboard becomes a scrap-heap of green tiles that no one has audited for six months. The on-call cannot tell which tiles are *load-bearing* on the release decision and which are historical.

The second is **rot-in-place**. A tile shows a peer track's freshness signal, but the peer track has quietly changed the source; the tile is still green because it defaults to green when the source is missing. Silent failure of the observer means silent failure of the runbook trigger it feeds.

The third is **audience confusion**. The same board is used by the release-owner, the assurance owner, the head of AI governance, and the deployer. Each audience wants different fields; a board that tries to serve all four surfaces none well. In particular, the on-call assurance engineer's board is *narrower* and *deeper* than a program-wide board.

This chapter designs the dashboard for the on-call assurance engineer's use, at the moment of approval. The chapter also names the *program-level* boards that consume the same underlying data at other cadences.

## What the on-call needs, at a glance

The board is organised into five lanes. Each lane answers a single question. Read the lanes top-to-bottom in order; a red lane means don't sign until it's dispositioned.

1. **Scope lane.** Is the release-in-scope well-defined, and is the criterion set the one the assurance case (mod-102) authored?
2. **Evidence-freshness lane.** For every criterion, is the pinned artefact present and within its freshness window?
3. **Pass-criteria lane.** For every criterion, has the walker resolved the threshold and produced a pass / soft-fail / hard-fail?
4. **Peer-track lane.** Are all four peer-track contracts (chapter `04`) in good standing (signed, not in renegotiation, no unclosed challenges)?
5. **Runbook readiness lane.** Are the rollback and rollforward contracts tested-current? Is the incident-response interface reachable? Are exception / deferral registers open for review?

Each lane's colour is derived, not decorative. Green requires all named checks passed; yellow flags at least one soft-fail or one open deferral; red flags at least one hard-fail, one broken contract, or one un-executable runbook procedure.

## Lane 1 — Scope

**Fields.**

- Release-in-scope: `system-id | model-version-digest | config-digest | deployment-surface | tier`.
- Criterion-set version: `gate-criteria-vN` — the exact tag.
- Assurance-case version: `sacm-vN` — the exact tag, matched to the criterion set.
- Consumer-contract set version: chapter `04`'s repo state at a tag.
- Runbook version.
- Effective-date: the wall-clock window the gate authorises.

**Fail-states.**

- Any digest field is unset. Do not sign.
- Criterion-set version does not match the assurance case's tag. The two got out of sync; do not sign.
- Runbook version is older than the last incident-derived corrective action. Assurance owner must acknowledge before signing.

## Lane 2 — Evidence freshness

**Fields.** One row per criterion. Columns:

- Criterion ID (from the rubric).
- Owner peer track (from the consumer contract).
- Artefact ID and digest (the SACM `Artifact.id` and the content digest).
- Freshness state — a per-row derived field from `(now - artefact-produced-at)` against the consumer-contract freshness policy: `fresh` / `stale` / `missing`.
- Cadence (per-release-candidate / per-quarter / on-event).
- Sign-off party and signature-verification state (`verified` / `unverified` / `signature-missing`).

**Presentation.** Group rows by peer track so a peer-track outage is visible as a block rather than scattered. Show a per-peer-track summary row (`4/4 fresh`, `3/4 fresh — 1 missing`, etc.).

**Fail-states.**

- `missing` on a hard-gate row — hard-fail. Escalates per runbook.
- `stale` on a hard-gate row — hard-fail with a runbook-defined path (regenerate, defer, or exception).
- `unverified` on any row — hard-fail; the contract's acceptance test is not met.
- `stale` on a soft-gate row — yellow; must be dispositioned.

## Lane 3 — Pass criteria

**Fields.** One row per criterion. Columns:

- Criterion ID.
- Metric, threshold (as pre-registered).
- Measured value (from the walker's resolution against the evidence bundle).
- Result — `pass` / `soft-fail` / `hard-fail` / `deferred` / `exceptioned`.
- Hard / soft label.
- ISO 25059 dimension (chapter `02`).
- NIST AI RMF MEASURE sub-category (chapter `02`).
- EU AI Act article (where applicable).
- Framework citation completeness — `complete` / `missing`.

**Presentation.** Group rows by ISO 25059 dimension so the coverage balance from chapter `02` is visible at a glance. Show a per-dimension summary: `functional-adequacy 4/4 pass | robustness 3/4 pass / 1 hard-fail | transparency 2/2 pass | controllability 1/1 pass | adaptability 2/3 pass / 1 soft-fail | appropriate-use-of-data 2/2 pass`.

**Fail-states.**

- Any `hard-fail` — do not sign; runbook path is either rollback (if already promoted), defer (if not), or exception-approval.
- Any dimension with zero criteria at T2 and above — coverage gap; the rubric is under-covering that dimension.
- Any row with `framework citation completeness: missing` — the row does not resolve to an AIMS clause; internal-audit will find it. Do not sign until the citation is written.

## Lane 4 — Peer-track health

**Fields.**

- Peer track name, contract version, signed-through date.
- Renegotiation state — `stable` / `in-renegotiation` / `overdue-review`.
- Open challenges — the count from the decision-record challenge log across recent releases, and a link to the log.
- Recent artefact-supply state — a small per-peer rollup of the artefacts produced in the current window vs. the expected cadence (proxy for whether the peer track is actually keeping up).

**Presentation.** One tile per peer track: `ai-eval-engineer` / `model-evaluation-engineer` / `ai-risk-engineer` / `ai-infra-security`. Each tile shows contract version, signed-through date, and any open renegotiation.

**Fail-states.**

- `in-renegotiation` for a hard-gate criterion's owner peer — the contract is not stable; the on-call must confirm the current gate criteria are covered by the pre-renegotiation contract clause and defer signing if not.
- Open challenges above a program-set threshold — the peer track is receiving more challenges than are being closed; a governance signal, though not necessarily a per-release blocker.
- `overdue-review` — the contract's annual review has lapsed. Yellow, not red — sign, but pin the review as a follow-up.

## Lane 5 — Runbook readiness

**Fields.**

- Rollback contract: `tested-current` (last reverse-drill within the tested cadence), `tested-stale` (drill overdue), `never-tested`.
- Rollforward test-set: freshness state (per-tier).
- Incident-response contact reachable (a simple ping check).
- Article 73 (or equivalent) notification path — the wall-clock and the contact set — visible and current.
- Deferred approvals register: count of active deferrals, count nearing expiry.
- Exception-approvals register: count of active exceptions, count nearing expiry.
- Post-market handoff to mod-110: is the online-eval slice ready, are drift detectors configured, are dashboards linked?

**Fail-states.**

- `tested-stale` or `never-tested` rollback contract at T2 and above — hard-fail. The runbook does not work.
- Notification path missing at any tier where a serious-incident-notifiable event could occur — hard-fail.
- Any exception nearing expiry with no revisit trigger scheduled — yellow.
- Post-market handoff incomplete — hard-fail at T2 and above.

## Wiring the dashboard to the evidence

The dashboard does not compute the underlying data; it *reads* it. Every field points at a source:

- Lane 2 rows read the SACM `Artifact` elements (mod-102 chapter `04`) and the digests recorded in the evidence pipeline (mod-104).
- Lane 3 rows read the walker's per-criterion output for the release-in-scope.
- Lane 4 tiles read the consumer-contract set (chapter `04`) and the challenge-log entries across recent decision records.
- Lane 5 rows read the runbook (chapter `05`), the reverse-drill log, the incident-response system state, and the mod-110 online-eval configuration.

None of the reads is derived from a middleware calculation the on-call cannot audit. The rule: *what a lane shows must be reproducible from the immutable evidence store the AIMS's clause 7.5 documented-information substrate contains* (mod-104). If a signal cannot be reproduced from that store, it is a *derived alert*, and it does not go on the on-call board — it goes on a program-level board (see below) with its own audit trail.

## Silent-failure protection

Rot-in-place is the most dangerous failure mode. Two design choices push against it:

- **Every observer emits a heartbeat.** If the observer has not reported within its own cadence, the field shows `stale` (yellow) or `no-signal` (red), not `green`. A defaulted-green field is a program defect.
- **Every observer's source is pinned.** Fields cite the source path or query the on-call can inspect. Sources are pinned in the dashboard's configuration and versioned; changes to the source are dashboard-config changes with review.

Silent-failure protection is what makes the dashboard a *control*, not a display.

## The audiences and their boards

Four boards, sharing an evidence substrate but tuned to their reader:

1. **On-call assurance engineer's board (this chapter).** Read at approval and during the post-release watch. Optimised for *sign / do-not-sign* decisions on a single release-in-scope.
2. **Release-owner's board.** Read at approval and during the post-release watch. Adds product-side metrics — user-facing outcome, adoption, business-side telemetry — which are the release-owner's remit. The gate's lanes appear as sub-panels.
3. **Assurance-program owner's board.** Read at management-review cadence (ISO 42001 clause 9.3). Shows program-level metrics — gate throughput, exception counts, deferral counts, rollback events, incident correlations, peer-track health across cycles.
4. **External-audit board.** Read at internal or external audit (ISO 42001 clause 9.2). Shows the trail — versioned SOPs, versioned rubric, versioned criterion sets, decision records with challenge logs, corrective-action closure.

Boards 3 and 4 are *not* the on-call board. They share source data but ask different questions. The on-call board's design is *not* the right board for management review; if it becomes so, it usually means the on-call board has drifted into program-metric territory and lost focus.

## Worked example — one release, one board

The T2 gate from chapter `05` promotes an updated customer-intent classifier. On the day of approval, the on-call opens the board:

- **Lane 1** — `system-id: intent-classifier`, `model-digest: sha256:9f…`, `config-digest: sha256:0a…`, `surface: prod-canary-30pct`, `tier: T2`, `gate-criteria-v3`, `sacm-v3`, `consumer-contract-set-v2.4`, `runbook-v1.7`, `effective: 2026-07-10 14:00 – 15:00 UTC`. Green.
- **Lane 2** — 12 rows across 4 peer tracks. All rows `fresh`, all signatures `verified`. Green.
- **Lane 3** — 12 rows resolving to 6 dimensions. All hard-gate rows `pass`; one adaptability soft-gate row `soft-fail` (drift on a minor input feature is trending). Green, with a yellow flag on adaptability.
- **Lane 4** — 4 tiles. All contracts `stable`, all signed-through dates current. 2 open challenges below the program threshold. Green.
- **Lane 5** — Rollback contract `tested-current` (drill 2 weeks ago). Rollforward test-set fresh. Notification path current. 1 open deferral (unrelated) not near expiry. Post-market handoff complete. Green.

Board reads green; on-call signs, documents the adaptability soft-fail disposition (open a corrective action to add drift-detector on the minor feature), and hands to mod-110.

Contrast with the trigger-firing case from chapter `05` twelve hours later:

- **Lane 3** — `GATE-FA-01` row now shows measured F1 CI-lower 0.79, threshold 0.83. Result: `hard-fail`.
- **Lane 5** — rollback contract's `execute` link is visible and pre-authorised for the tier.

The on-call executes rollback per runbook. The dashboard's job here is not to *make* the decision — it is to *surface* the trigger and *route* the on-call to the runbook step.

## Common failure modes

- **Board built as a summary of program metrics rather than a per-release approval control.** Everything is a trend line; nothing is a sign / do-not-sign field. The on-call cannot use it at approval time.
- **Silent-green tiles.** No heartbeat check; a broken observer defaults green. Fix by requiring every observer to declare stale.
- **Lane 3 without dimension grouping.** The 25059 coverage balance is not visible; the rubric can be under-covering without the board showing it.
- **Peer-track lane missing.** Contracts are assumed stable; a renegotiation is invisible; on-call signs against an out-of-date contract.
- **Runbook readiness assumed.** Reverse-drills happen; the dashboard does not show it; drills lapse silently.

## Where this feeds

- Chapter `01` — the dashboard is the reader's view of the release-gate at approval.
- Chapter `05` — every runbook trigger has a dashboard field it observes.
- mod-104 — the evidence pipeline is the substrate the dashboard reads.
- mod-110 — the post-market handoff row is where the dashboard's *ongoing* view lands, and mod-110 owns the ongoing dashboards themselves.

## Summary

- The dashboard is the on-call assurance engineer's per-release approval control. It answers *sign / do-not-sign* and points to the specific blocker if not.
- Five lanes, each with a defined fail-state: Scope, Evidence freshness, Pass criteria (grouped by ISO 25059 dimension), Peer-track health, Runbook readiness.
- Every field points at an immutable source; nothing is derived from a middleware calculation the on-call cannot audit.
- Silent-failure protection — every observer emits a heartbeat; defaulted-green is a program defect.
- Multiple boards for multiple audiences (on-call, release-owner, program-owner, audit); do not overload the on-call board with program metrics.
- The board makes the runbook readable at a glance and turns the design of chapters `01`–`05` into a control the on-call can actually execute.
