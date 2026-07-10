# exercise-03: SACM Persistence and Diff Across Release Cycles

**Estimated effort:** 3 hours

## Objective

Persist the case from exercises `01` and `02` in a valid **OMG SACM 2.2** instance (JSON is acceptable; XMI is a stretch), tag it as **version 1**, then produce a **version 2** representing the *next* release cycle after realistic changes and generate a diff between the two versions. The output is a working, versionable, diffable representation of the assurance case that a program repository could hold.

This is the applied output of chapter `04`.

## Prerequisites

- Chapter `04-sacm-persistence-and-diff.md`.
- The [OMG SACM 2.2 specification](https://www.omg.org/spec/SACM/2.2) — read the packages summary (Base / Argumentation / Terminology / Artifact) and the class reference for the subset in chapter `04`.
- Exercises `01` and `02` outputs — you will persist the same case.
- A text editor and (optionally) a JSON schema tool of your choice.

## Problem statement

The release-assurance program has to keep the release-case from exercises `01`–`02` in a form the next release cycle can build on rather than re-author. Two concrete requirements land on you this week:

- **Persistence.** Convert the case to a SACM instance that a program repository can Git-track. Every claim, argument, side-warrant, evidence reference, and away-claim must be a typed SACM element with a stable identifier and version.
- **Diff.** The next release cycle changes three specific things — you will apply those changes to the SACM instance as version 2 and produce a human-readable diff between v1 and v2. The diff has to explain, at each changed node, what changed and why.

## Requirements

Produce three artefacts:

### 1. `sacm-v1.json` (or `.xmi`)

A SACM 2.2 instance capturing the case at the initial release decision date (the one you used in exercise `01`). The instance must include, at minimum:

- One `ArgumentPackage` per case module (start with a single package if the case is small; split into modules if you followed the module map from exercise `01`'s stretch goal). Version `1.0.0`.
- Every claim from the CAE recast in exercise `02` as a `Claim` element, with `content`, `assumed`, and `toBeSupported` populated.
- Every argument in the CAE recast as an `ArgumentReasoning` element, with the CAE block name in `content`.
- `AssertedInference` elements linking sub-claims to their parent via the reasoning.
- `AssertedContext` elements linking contexts, assumptions, and warrants to the nodes they attach to.
- One `ArtifactPackage` for the evidence, with `Artifact` elements per leaf's evidence. Each `Artifact` must have at least one `ArtifactAsset` with a digest placeholder (a real `sha256` digest if you have artefacts on hand, otherwise a syntactically valid placeholder). `participants`, `events`, and `techniques` are populated from the peer-track routing recorded in exercise `01` (they will be formalised in exercise `05`).
- One `TerminologyPackage` capturing the deployment tier and jurisdiction scope from the case header.

The instance does not have to be schema-round-trippable in tooling (that is a stretch goal), but it must be *syntactically valid* JSON (or XMI) and *structurally valid* SACM — every reference resolves, every id is unique, every element carries a version.

### 2. `sacm-v2.json` (or `.xmi`)

Apply the following three changes to represent the next release cycle. Version `1.1.0` if the changes are non-structural (the SACM spec's semver interpretation); `2.0.0` if you consider a change materially structural.

1. **Content change on a threshold.** Move one leaf claim's threshold from its exercise-`01` value to a new value (e.g., per-class F1 threshold from `0.85` to `0.87`), with a stated reason (e.g., "risk-inventory row R-triage-3 upgraded the target harm's residual"). Update the leaf claim's `content` and record the reason in the audit ledger from exercise `04` (or a comment in the SACM if you prefer).
2. **Evidence-version change.** Replace one leaf's `ArtifactAsset` with a new version (new digest, new `lastVerifiedAt`, same technique). This models a re-run of the eval / red-team / audit for the next release candidate.
3. **Structural change.** Add one sub-claim under an existing argument that discharges an obligation you had previously overlooked or that a new framework revision has surfaced (e.g., a new EU AI Act GPAI Code of Practice clause). Add the new claim, wire it under the parent argument via a new `AssertedInference`, and add its evidence node.

### 3. `sacm-diff.md`

A human-readable diff between v1 and v2 that separates:

- **Structural diffs.** New / removed / restructured claims, arguments, inferences. One-line-per-change table plus the impact statement per row.
- **Content diffs.** Text-level diffs on `content` fields of claims that changed. Show old text and new text side-by-side, and name the reason for each change.
- **Evidence diffs.** Changes to `ArtifactAsset` version, digest, `lastVerifiedAt`, participants, or techniques. Show old / new digests and warrant deltas.

The diff must be walk-able by someone who has the case's SACM v1 open in a text editor — they should be able to find each cited node by identifier without your narration.

## Starter guidance

- **Author a small case first if the exercise `01` case is large.** SACM persistence is easier to get right on a small case with the full node zoo than on a large case with only a slice of node types. If exercise `01` produced a 30-goal case, pick a 6-goal slice for this exercise.
- **Use stable, human-readable identifiers.** `C1.1.15.a` beats `claim-uuid-42a3` for a document a human is going to read. Chapter `04` recommends this — machine tooling can layer UUIDs on top later.
- **Store the digest even if it is a placeholder.** The schema is what matters. `sha256:PLACEHOLDER-eval-report-v1-0-0` is fine so long as you use the same placeholder consistently between v1 and v2.
- **Keep the audit trail out-of-band.** The SACM instance is the case; the audit ledger and the release-cycle change log are separate artefacts stored alongside. Do not stuff prose reasons into the SACM `content` — use a separate change-log file.
- **When adding a sub-claim, remember to link its side-warrants.** A new claim without its context and assumptions is not merged; it is dangling.
- **Do not touch the identifiers of unchanged nodes.** The whole point of persistence is that unchanged identifiers survive across versions so the diff is stable.

## Acceptance criteria

You have succeeded if:

- `sacm-v1.json` (or `.xmi`) is syntactically valid, structurally valid SACM 2.2, and captures every claim / argument / context / assumption / warrant / evidence node from exercise `02`'s CAE recast.
- Every element has a stable identifier and a version.
- Every `AssertedInference` and `AssertedContext` resolves.
- Every `ArtifactAsset` has a digest (real or placeholder) and a `lastVerifiedAt`.
- `sacm-v2.json` reflects all three prescribed changes (threshold content, evidence version, structural addition) and keeps unchanged nodes' identifiers stable.
- `sacm-diff.md` separates structural, content, and evidence diffs, with old / new visible per row and a reason per change.
- A reader unfamiliar with the case can walk the diff top-to-bottom and understand what the next release cycle is being asked to re-argue vs. inherit unchanged.

## Stretch goals

- Publish v1 and v2 as **XMI** conforming to the OMG SACM 2.2 XMI schema, and validate against it with an XMI-capable tool.
- Build a small script (Python or your language of choice) that reads v1 and v2 JSON, produces the diff automatically, and emits `sacm-diff.md` in the shape above. Submit the script alongside the diff.
- Round-trip the SACM through a **case-tool import / export** ([ASCE](https://www.adelard.com/asce/), or an open-source GSN-to-SACM tool from `resources.md`). Note what the tool preserves and what it drops.
- Extend the diff to answer three machine queries against v2 (per chapter `04`): "which claims does artefact X support?", "which release-cases assume A?", "which evidence discharges obligation O?". Print the results and confirm they match the manual reading of the case.
