# exercise-05: Release-Gate Dashboard Slice

**Estimated effort:** 3 hours

## Objective

Design and build a **working slice** of the on-call assurance engineer's release-gate dashboard for the system from exercises `01`–`04`. The slice covers the five lanes from chapter `06` (Scope, Evidence freshness, Pass criteria, Peer-track health, Runbook readiness) and is *reproducible from the immutable evidence store*, not derived from a middleware calculation the on-call cannot audit. Then perform a *silent-failure red-team* — deliberately break an observer and prove the dashboard turns red (or yellow with `no-signal`) instead of defaulting green.

This is the module capstone. It ties the criterion set (`01`), rubric (`02`), contracts (`03`), and runbook (`04`) into a control the on-call can actually execute.

## Prerequisites

- Chapter `06-release-gate-dashboard.md` (this module).
- Chapters `01`–`05` and exercises `01`–`04` outputs.
- A minimal implementation environment: your choice of Python + a static-site generator, a Grafana / Datadog / equivalent panel set, a Notion / Confluence rendered from source, or a raw HTML page. What matters is the wiring from source data to lane, not the rendering framework.

## Problem statement

Chapter `06` designed the five lanes. This exercise builds one. The slice does not have to cover every rubric row — pick a *coherent subset*: at least the release-in-scope from exercise `01`, at least three rubric rows drawn from at least two ISO/IEC 25059 dimensions, and at least one peer-track health tile per peer track named in exercise `03`.

The exercise has three parts: (1) build the dashboard slice, (2) wire it to a working evidence store (or a fixture that stands in for one), (3) run a silent-failure red-team and record the outcome.

## Requirements

Produce four artefacts.

### 1. `dashboard-slice/` (the working slice)

The rendered dashboard, with its source. Structure:

- `README.md` explaining how to run / view the slice.
- Source files (Python, HTML, dashboard-tool JSON, or whatever your framework demands).
- A `fixtures/` directory containing the evidence-store data the dashboard reads (SACM `Artifact` JSON, signed peer-track attestations as stubs, dashboard-config YAML, decision-record fixture from a hypothetical release). Fixtures are as close as the exercise gets to a real evidence store; they must be *pinned* — the dashboard reads a specific version.

The slice must render the five lanes:

- **Lane 1 — Scope.** Shows the release-in-scope from `exercise-01`, criterion-set version, assurance-case version, consumer-contract-set version, runbook version. Fail-state: any field unset shows red.
- **Lane 2 — Evidence freshness.** At least three rubric rows across at least two peer tracks. Each row shows criterion ID, owner peer, artefact ID / digest, freshness state, sign-off verification. Fail-states from chapter `06` are enforced.
- **Lane 3 — Pass criteria.** The same three-plus rubric rows with metric, threshold, measured value (from the fixture), pass state, hard/soft, 25059 dimension, MEASURE sub-category, EU AI Act article, and framework-citation-completeness. Rows are grouped by ISO/IEC 25059 dimension; the per-dimension summary is derived and displayed.
- **Lane 4 — Peer-track health.** One tile per peer track named in `exercise-03`. Contract version, signed-through date, renegotiation state, open challenges count.
- **Lane 5 — Runbook readiness.** Rollback contract state (with the last reverse-drill date), rollforward test-set freshness, notification-path reachability, deferred and exception counts (from the fixture), post-market handoff state.

### 2. `dashboard-design-notes.md`

Short (1–2 pages) explaining:

- The evidence-store shape the fixture models (path to fixture, schema references — SACM 2.2 / SPDX-AI / your program's schema of record).
- The source-of-truth per lane: what each field reads from, what heartbeat check the observer runs, what "stale" means for each field.
- Why the specific rubric rows were chosen for the slice (coverage of at least two 25059 dimensions and at least two peer tracks; illustrate a hard-fail path).
- The audience separation from chapter `06`: what this on-call board deliberately *does not* show, and where those fields live (release-owner board / program-owner board / audit board).

### 3. `silent-failure-red-team.md`

The red-team trace. Pick at least *three* observers in your slice and break each one in a specific way. Record the outcome.

For each breakage:

- **Observer.** Name the field(s) it feeds.
- **Breakage.** What you did (removed the artefact from the fixture, corrupted a digest, deleted the heartbeat, replaced the timestamp with a stale value).
- **Expected outcome.** What the dashboard should show per chapter `06`'s fail-state rules.
- **Observed outcome.** What the dashboard actually showed.
- **Disposition.** If the observed matches the expected, note it and move on. If it does not (defaulted-green, or the wrong colour), the slice has a silent-failure defect — describe the fix.

At least one breakage must target the **signature-verification** check in Lane 2. At least one must target the **freshness heartbeat** in Lane 4 or Lane 5.

### 4. `on-call-walk-through.md`

A short walk-through demonstrating how an on-call would use the slice at approval time. Two scenarios:

- **Scenario A: green board.** Every lane green. On-call reads the board, confirms the release-in-scope, signs the decision record. Note the specific decision-record fields the board makes it easy to fill.
- **Scenario B: hard-fail on Lane 3.** Modify one fixture value so a `GATE-*` criterion measured value falls below its threshold. Show the dashboard turning red. Show the on-call reading Lane 3 → identifying the criterion → jumping to the runbook (exercise `04`) → executing the disposition.

## Starter guidance

- **Wire, do not simulate.** The slice must be wired to a fixture that stands in for the evidence store. A dashboard whose fields are hard-coded is not the exercise; the whole point is that changing the fixture changes the dashboard state.
- **Heartbeats are the observation you cannot skip.** Every observer must publish a heartbeat (a "last-observed-at" timestamp), and every field must compare that heartbeat against its cadence. Defaulted-green is a bug you commit not to ship.
- **Do not overbuild.** The slice is a *proof-of-concept* — three rubric rows, two peer tracks, one release-in-scope. Better a small slice that is honestly wired than a full board that fakes the wiring.
- **Framework columns are visible on the board, not hidden.** Lane 3 has to display the 25059 dimension, the MEASURE sub-category, and the EU AI Act article per row; the on-call needs those citations at approval time.
- **Use your rubric.** The three-plus rows in Lane 3 are drawn from exercise `02`'s rubric — do not invent new criteria for the dashboard.
- **The red-team is not an afterthought.** A dashboard that has never been red-teamed for silent failure is a dashboard that will silently fail.

## Acceptance criteria

You have succeeded if:

- The `dashboard-slice/` renders (or can be rendered with a documented command) and shows all five lanes.
- Each lane's fail-state rules from chapter `06` are enforced (hard-fail rows visibly red; stale rows visibly yellow; unverified signatures red; overdue reverse-drill red at T2+).
- The evidence source-of-truth per field is documented and audit-able against the fixture.
- ISO/IEC 25059 dimension grouping is visible in Lane 3.
- Peer-track health tiles reflect the consumer-contract set from exercise `03`.
- The silent-failure red-team ran at least three breakages, including one signature-verification and one heartbeat breakage, and every observed outcome matches (or the slice has been patched and the fix documented).
- The on-call walk-through shows both a green sign-off and a red hard-fail disposition, and the red disposition explicitly jumps to a specific runbook section from exercise `04`.
- A colleague reading the walk-through and following it against the running slice can reproduce both scenarios.

## Stretch goals

- Add a **program-owner board** (chapter `06`'s audience 3) that consumes the same evidence store and shows gate throughput, exception counts, deferral counts, rollback events, and peer-track health across cycles. Make it clear which fields are the on-call board's *and* the program-owner board's vs. the program-owner board's only.
- Add an **audit board** (chapter `06`'s audience 4) that walks the trail — SOP versions, rubric versions, criterion-set versions, decision records with challenge logs, corrective-action closures.
- Wire the **post-market surveillance handoff** (mod-110 preview) — the online-eval slice's drift, coverage, and incident-detector configuration read from the same fixture, and the dashboard shows the handoff state in Lane 5.
- Author a **dashboard-schema SOP** — the standing document that governs how new fields are added, how fixtures are versioned, how observers register their heartbeats, and how the audit trail treats dashboard-config changes.
- Wire the dashboard to a real evidence store (SACM in JSON or XMI, SPDX-AI ML-BOM, a project's actual eval-report output). This is the largest stretch and the closest to production.
- Present the slice to a colleague not involved in the exercise and ask them to sign the mock decision record after using the dashboard. Capture where they hesitated; that is where the board needs more focus.
