# The Map Itself — Schema, Emission, Versioning, and Handoff

## Motivation

Chapters `02`–`07` were building the *content* of the map. This chapter builds the *artefact*: the machine-readable file (or files) that emits the map, the schema its rows validate against, the signing and versioning discipline that makes two versions diffable, and the review workflow that hands the map to the level-50 `senior-ai-governance-architect` for enterprise reconciliation.

The map is a first-class release-gate artefact. It has a content-addressed digest in the evidence pipeline (`mod-104`), a signature, a version number, and a review record. It is emitted at every release-gate run and stored alongside the release package.

## Design goals

The schema and emission format have to satisfy five properties simultaneously:

1. **Machine-parseable.** The architect at L50 runs aggregate queries across many maps. Every field is typed; free text is confined to `notes` fields the queries do not read.
2. **Human-readable.** A release-gate reviewer walks the map row-by-row in a code review interface. Rows fit on a screen; identifiers are readable.
3. **Diffable.** Two consecutive versions of the map for the same system produce a diff a reviewer can understand. Semantic diffs (obligation added, deliverable changed, status transitioned from `partial` to `covered`) are readable.
4. **Signed.** The map itself is signed by the release-assurance methodology owner; individual rows may carry additional signatures (legal countersign, L60 head-of-governance for elevated residuals).
5. **Content-addressed.** The map's digest is what other artefacts (assurance case, release-gate schema, card variants) point at, and what the L50 architect walks from.

The format decision that follows drops from those goals: YAML for authoring, JSON for emission and validation, JSON-Schema for the schema, in-band SPDX-AI / ML-BOM style manifest wrappers where the map is packaged for hand-off.

## Row schema

The row is the atomic unit. Every obligation on the map is one row.

```yaml
# One row from the map, in author-friendly YAML shape.
obligation_id: eu-ai-act.art15.robustness-report
schema_version: "1.2.0"                 # semver of this schema; validators check
map_id: assurance-map/hiring-tool/v2025-11-04
map_version: "2025-11-04"

# --- Provenance of the obligation itself ---
instrument: eu-ai-act-2024-1689           # canonical instrument identifier
instrument_version_pin: "OJ L 2024/1689 as published 2024-07-12"
article_or_clause: "Article 15(1)(4)(5)"
obligation_summary: >
  Robustness of the AI system, including resilience against attempts by
  unauthorised third parties to alter the use, outputs, or performance.
applies_when:
  - condition: "high-risk provider under Annex III point 4"
    determined_by: legal-counsel
    determination_date: 2025-06-14
    determination_evidence_ptr: sha256:aa11…

# --- The deliverable ---
deliverable: robustness-evaluation-report-v3.md
deliverable_kind: report                  # document|report|declaration|plan|card|manifest|log-attestation|cross-ref
evidence_pointer: sha256:1a2b3c…         # content-address into the pipeline
owner_role: model-evaluation-engineer
signing_role: ai-evaluation-engineer      # this role
signing_state:
  signed_at: 2025-10-22T14:03:17Z
  signature_ptr: sha256:9f8e…

# --- Cross-tag columns ---
sibling_nist_rmf: [MEASURE-2.6]
sibling_nist_ai_600_1:
  - risk: information-security
    suggested_actions: [MS-2.6-002]        # illustrative; pin Playbook version
nist_playbook_version: "2024-07-30"
sibling_iso_clauses:
  - "ISO/IEC 42001:2023 8.2"
  - "ISO/IEC 42001:2023 9.1"
  - "ISO/IEC 25059:2023 5.x robustness"
  - "ISO/IEC 24029-2:2023 clause 7"
iso_soa_status:
  "ISO/IEC 42001:2023 A.6.2.4": in-scope    # SoA declaration for Annex A tags

# --- Jurisdictional cross-references ---
sibling_jurisdictions:
  - instrument: co-sb24-205
    row: co-sb24-205.deployer.risk-management-program
    relation: contributes-to
  - instrument: au-vaiss
    row: au-vaiss.g4.testing-and-monitoring
    relation: contributes-to
  - instrument: cn-cac-genai
    row: cn-tc260-003.basic-security-checklist
    relation: overlaps-partially

# --- Interoperability (AI Verify) ---
interop_ai_verify_principles: [robustness, security]
interop_ai_verify_test_ids: [robust.perturb.001, robust.adversarial.003]
interop_mgf_building_block: operations-management
interop_ai_verify_report_ptr: sha256:be71…#/results/robustness
interop_gap: null                          # or a short string if the toolkit does not cover

# --- Release-gate wiring ---
tier_applicability: [tier-1, tier-2, tier-3]     # from mod-108
gate_dependency: blocking                        # blocking|informational|deferred-pass
status: covered                                  # covered|partial|open|waived-with-residual|not-applicable|pending-instrument
status_last_verified: 2025-10-22
status_next_verify_by: 2026-04-22

# --- Residual (only where status is waived-with-residual) ---
residual:
  description: null
  accepted_by: null
  accepted_at: null
  escalation_owner: null
  review_by: null

# --- Free text (author notes, not consumed by aggregate queries) ---
notes: |
  Robustness perturbation classes cover the L∞ / L2 ball radii from the
  ISO/IEC 24029-2 method reference. Adversarial-example evaluation uses
  the AI 100-2 evasion / extraction split.
```

Field-by-field constraints — the ones enforced by the JSON-Schema validator:

- `obligation_id` — kebab-case, dotted, unique within `map_id`. Regex enforced.
- `schema_version` — semver.
- `instrument` — enum drawn from the canonical instrument-identifier table (see §"Canonical identifiers" below).
- `instrument_version_pin` — free text, but required.
- `applies_when` — list of at least one entry with a determination trail.
- `deliverable_kind` — enum.
- `evidence_pointer` — SHA-256 content-address; regex enforced (`^sha256:[0-9a-f]{64}(#/.*)?$`).
- `owner_role` — enum drawn from the peer-role registry (defined in the track's role artefacts).
- `signing_role` — enum from the same registry.
- `signing_state.signed_at` — ISO-8601 UTC.
- `sibling_nist_rmf` — list; each entry validated against the RMF sub-category enumeration.
- `sibling_iso_clauses` — list; each entry validated against the format `<standard>:<year> <clause>`.
- `sibling_jurisdictions[].relation` — enum: `shares-deliverable | contributes-to | overlaps-partially | supersedes | superseded-by`.
- `status` — enum. Rows with `status: pending-instrument` require `applies_when[].condition` to include `"instrument-enacted"` or equivalent.
- `residual.*` — required when `status = waived-with-residual`.

The full JSON Schema lives at `schema/assurance-map/row.schema.json` in the release-assurance repository and is versioned alongside the code that consumes it.

## Map document shape

The map is a single document with a header and a body of rows. The document's canonical shape:

```yaml
schema_version: "1.2.0"
map_id: assurance-map/hiring-tool
system_id: hiring-tool
system_version: "2025.11.04"
map_version: "2025-11-04"
generated_at: 2025-11-04T09:22:41Z
generated_by:
  role: ai-evaluation-engineer
  identity: "Firstname Lastname <email>"
  identity_key_ptr: sha256:aa11…      # PGP / sigstore / OIDC binding
anchor: eu-ai-act-2024-1689
jurisdictional_scope:
  - jurisdiction: EU
    determination_evidence_ptr: sha256:11aa…
  - jurisdiction: US-CO
    determination_evidence_ptr: sha256:22bb…
  - jurisdiction: US-NY-NYC
    determination_evidence_ptr: sha256:33cc…
  - jurisdiction: UK
    determination_evidence_ptr: sha256:44dd…
  - jurisdiction: SG
    determination_evidence_ptr: sha256:55ee…
  - jurisdiction: AU
    determination_evidence_ptr: sha256:66ff…
notified_body_ref: null              # populated for Article 43 Annex VII paths
frameworks_pinned:
  eu-ai-act: "OJ L 2024/1689"
  nist-ai-rmf: "1.0"
  nist-ai-600-1: "2024-07-26"
  nist-ai-100-2: "2023"
  iso-iec-42001: "2023"
  iso-iec-23894: "2023"
  iso-iec-42005: "2025"
  iso-iec-25059: "2023"
  iso-iec-24029-2: "2023"
  ai-verify-framework: "0.10"        # pin the framework version
  mgf-genai: "2024-05"
prior_map_version: "2025-08-17"
prior_map_content_address: sha256:eeff…
rows:
  - # ... row entries as per row schema ...
attestations:
  - kind: methodology-owner-signature
    signer: "Firstname Lastname"
    signed_at: 2025-11-04T09:22:41Z
    signature_ptr: sha256:cc44…
  - kind: legal-countersign
    scope: [co-sb24-205.*, nyc-ll-144.*, cfpb-adverse-action.*]
    signer: "General Counsel"
    signed_at: 2025-11-04T09:22:41Z
    signature_ptr: sha256:dd55…
```

## Canonical identifiers

Cross-map interoperability collapses if two maps use different instrument identifiers. The programme maintains a **canonical instrument registry** — a small YAML file, versioned in the release-assurance repository, that establishes:

- Canonical instrument ID (e.g., `eu-ai-act-2024-1689`, `co-sb24-205`, `nyc-ll-144`, `iso-iec-42001:2023`).
- Human-readable title.
- Issuing authority.
- Canonical text URL (an authoritative host — EUR-Lex, Colorado General Assembly, ISO catalogue).
- Legal status enum (`in-force`, `pending`, `voluntary-guidance`, `regulator-supervisory`).
- Latest revision date and version pin format.

Every `instrument` and `sibling_jurisdictions[].instrument` value on a row must resolve into the registry. The validator enforces this.

`<!-- needs-research: consider whether to align the canonical registry with an emerging community list (OECD AI Policy Observatory has a catalogue; GPAI has one; a joint MLCommons / GPAI cross-index is possible) rather than maintain a bespoke one -->`

## Emission format

Authors edit YAML. The pipeline emits both YAML (for review) and canonical JSON (for validation, signing, storage).

The canonical JSON:

- Applies canonical field ordering (keys sorted lexicographically at every level).
- Uses UTF-8, no BOM, LF line endings.
- Numeric fields carry no trailing zeroes.
- ISO-8601 timestamps use `Z` for UTC.
- All string fields are trimmed.

The purpose of the canonicalisation is diff stability: two maps that are semantically identical produce byte-identical JSON.

## Signing

The map document is signed once its rows are complete. Signing options — pick one and pin per programme:

- **Sigstore (recommended for open-source-friendly programmes)** — the map document is signed with a short-lived Fulcio certificate bound to an OIDC identity, the signature is anchored in the public Rekor transparency log, and the entry is recorded in-band. This composes cleanly with the SLSA / Sigstore attestation approach from `mod-104` chapter `04`.
- **Enterprise CA + JWS** — the map is signed with a JWS (JSON Web Signature) whose header carries a key ID resolvable in the enterprise CA. Suitable for organisations that already have a mature enterprise key infrastructure.
- **X.509 + CMS** — for organisations aligned to standards-based document signing (regulatory audits sometimes prefer this).

The signature attests to *the canonical JSON's digest*. Verification is: (1) recompute the digest from the stored bytes, (2) verify the signature over the digest, (3) confirm the signer's key was valid at `generated_at`.

Individual rows can carry additional signatures (`signing_state.signature_ptr` on the row, `attestations[].signature_ptr` on the map header). Legal countersign is captured in the header `attestations[]` scoped to a row-glob.

## Versioning and diffs

The map is a *time series*. Two axes matter:

- **System-version axis.** As the system evolves (`system_version` changes), some obligations may re-trigger (substantial modification), some rows may retire (deprecated feature), some rows may be added (new deployment surface). A new map is emitted per release-gate run.
- **Instrument-version axis.** As instruments evolve — new Playbook version, new ISO revision, new statute — the map picks up the new pin without necessarily any change in the system. This produces "map churn" that is orthogonal to system-version churn.

The `prior_map_version` and `prior_map_content_address` fields on the header make the time-series walkable. A tool (`assurance-map diff <prev> <curr>`) computes the semantic diff:

- Rows added.
- Rows removed.
- Rows whose `deliverable` changed.
- Rows whose `evidence_pointer` changed.
- Rows whose `status` transitioned.
- Rows whose `applies_when` changed.
- Rows whose cross-tags (NIST / ISO / jurisdictional / interop) changed.
- Rows whose `residual.*` changed.
- Header `frameworks_pinned` changes.

The diff is what the release-gate reviewer inspects. It is what the L50 architect reads to spot drift. It is what an auditor consumes to walk from "what changed" to "why."

## Status semantics

The `status` field is the load-bearing summary. Its values:

- `covered` — the deliverable exists, is current, is signed, and its evidence resolves.
- `partial` — the deliverable exists but is incomplete for this row (missing sub-fields, expired signing, superseded evidence). Not release-gate-passable at blocking dependency; the row must be tracked to `covered`.
- `open` — no deliverable yet. Blocking rows in this state fail the gate.
- `waived-with-residual` — the release-assurance methodology owner has accepted the row is not met and recorded a residual. The residual has an escalation owner and a review-by date. Legal typically countersigns.
- `not-applicable` — the row has been determined not to apply. Requires `applies_when[].determination_evidence_ptr` and legal counsel countersign.
- `pending-instrument` — the instrument is not yet enacted (AIDA, Brazil PL 2338). Pre-populated for readiness; not gate-blocking until the instrument is in force.

Aggregate reporting (see §"L50 aggregate handoff") counts rows by status and by instrument.

## Review workflow

A map is reviewed twice at each release-gate run:

1. **Peer review (author-side).** The release-assurance methodology owner walks the map end-to-end with the peer roles owning the rows: `ai-risk-engineer` for Article 9 / MEASURE / MAP rows, `model-evaluation-engineer` for Article 15 rows, `ai-governance-analyst` for Article 10 rows, `ai-infra-security` for Article 12 integrity / cybersecurity rows, product for Article 13 / 14 / consumer-notice rows, legal for the substantive-content / notification / registration rows. Each peer signs off on their rows.
2. **Gate review (governance-side).** The release-gate itself walks the map row-by-row. A row without a green deliverable is either (a) blocked (`status: open`), (b) waived (`status: waived-with-residual`, requires signature), or (c) not applicable (`status: not-applicable`, requires determination evidence).

Reviews are recorded in the header `attestations[]`. A map without both reviews recorded is unsigned by the methodology owner.

## L50 aggregate handoff

The map is handed to the L50 `senior-ai-governance-architect` once per system-release. The architect consumes many maps together and runs aggregate queries. The queries the architect needs are the queries the schema is built to support.

Recurring aggregate queries:

- **Which deliverables recur across systems?** Rows whose `deliverable` field (once normalised across name templates) appears on ≥N systems are candidates for a common enterprise-wide control. Feeds control-library reconciliation.
- **Which obligations are consistently `open` or `waived-with-residual`?** A pattern across systems indicates either an unmet enterprise-wide capability (staffing / tooling gap) or an under-scoped obligation.
- **Which peer roles are chronically over-tasked?** Row counts by `owner_role` across systems flag capacity issues.
- **Which jurisdictions carry the largest incremental burden per system?** New-row counts per jurisdiction across systems inform market-entry decisions.
- **Where do sibling cross-tags disagree?** If two systems tag the same obligation to different `sibling_nist_rmf` sub-categories, one of them is wrong; the architect resolves.
- **Which frameworks are on a stale version pin?** A system pinned to `nist-ai-600-1: "2023"` when the current is `"2024-07-26"` is due for refresh.

The architect's tool consumes the maps as a directory of canonical JSON files, validates each against the schema, indexes by `system_id`, and answers the queries above. Its output is the enterprise control library and the programme-level dashboard reported to the L60 head of governance (`mod-112`).

## External-audience handoff

The map is *internal*. For external audiences the map is filtered and transformed:

- **Notified body / Article 43 Annex VII.** The notified body receives a subset filtered to EU AI Act rows plus the interoperability report pointers. `mod-109` covers the hand-off shape.
- **NYC LL 144 independent auditor.** The auditor receives the fairness-adjacent rows and the AI Verify report pointer.
- **Big Four assurance team.** The map is exported in the audit team's expected shape (typically an audit-workpaper CSV / XLSX plus the underlying JSON).
- **AISI-style third-party evaluator.** The map, plus the evaluation-battery configuration, plus the artefacts being evaluated, plus any red-team access grant.

The card-side of external-audience derivation lives in `mod-105`; the map contributes the underlying regime block a card variant reads from.

## Anti-patterns

Recurring failure modes to name:

- **The one-YAML-file monolith.** Maps for large systems can exceed a thousand rows. Splitting by `chapter` (anchor / RMF-crosswalk / ISO-crosswalk / jurisdictional / interop / GPAI) into files under a directory helps review; the emission still produces a single canonical JSON for signing.
- **The "we use the RMF" one-liner.** A `sibling_nist_rmf: [MAP-1]` tag is useless. Every RMF tag must reference the specific sub-category and the specific rationale for the tag; if the rationale is not obvious from the deliverable's content, the row is under-specified.
- **The status-as-decoration.** `status: covered` is not a self-report. It is verified: the evidence pointer resolves, the signature verifies, the retention date is future. Automated checks in the release-gate script enforce this at map-load time.
- **The instrument-version drift.** Instruments evolve; framework pins expire. A map that has not refreshed `frameworks_pinned` in a year is likely wrong somewhere. The map ages.
- **The unsigned map.** A map without a methodology-owner signature is a working draft, not a release-gate artefact. The gate rejects it.
- **The map as legal opinion.** The map records classifications and cites legal countersign — it does not *make* the classification calls. Confusing the two is the fastest way to lose the audit trail.
- **The row without a peer owner.** A row whose `owner_role` is "TBD" is an unowned obligation. The methodology owner does not own everything by default; the escalation is to name a peer.

## Worked example — a compact map for a small system

For an internal decision-support tool (medium tier, EU + US-CO scope, no GenAI, no LL 144 exposure), the map might be 40 rows: ~24 EU AI Act rows (Article 9 / 10 / 11 / 12 / 13 / 14 / 15 / 17 sub-rows plus Annex III typing), ~7 Colorado rows, ~4 UK-GDPR-adjacent rows (if the system is UK-available), ~3 AI Verify interop rows, plus 2 map-header attestations.

For a global GenAI system (high tier, EU + UK + US-national + US-CO + US-NY-NYC + SG + AU + JP + KR + CN + BR, LLM-based, deployer-and-provider both), the map might be 300+ rows. Splitting by chapter into files becomes essential.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — every row's argument node in the case cross-references the row's `obligation_id`.
- `mod-103` (release-gate architecture) — the gate schema's per-obligation field is exactly the row's `obligation_id`.
- `mod-104` (evidence pipeline) — every `evidence_pointer` resolves in the pipeline; the map itself is stored there.
- `mod-105` (cards for external audiences) — the card's `regime` block is a filtered projection of the map header and selected row summaries.
- `mod-108` (deployment-tier gating) — `tier_applicability` per row is what the tier decision reads.
- `mod-109` (third-party evaluator interface) — external-audience filtering pipes into the evaluator's expected hand-off shape.
- `mod-110` (post-market surveillance) — post-market row updates feed back into the map as new versions.
- `mod-111` (GPAI systemic-risk assurance) — GPAI-specific rows extend the schema with additional sub-fields (systemic-risk classification, Code of Practice adherence, model-evaluation report references).
- `mod-112` (owning an assurance program) — the aggregate map view is a programme-level KPI.

## Summary

- The map is a machine-readable, human-readable, diffable, signed, content-addressed artefact emitted at every release-gate run.
- Rows validate against a JSON Schema; the map document validates against a map-header schema. Both are versioned semantically.
- Emission is YAML for authoring, canonical JSON for validation / signing / storage.
- Signing is Sigstore (recommended), JWS, or CMS — pick one, pin per programme; the signature attests to the canonical JSON digest.
- Versioning is per release-gate run; two consecutive maps produce a semantic diff a reviewer or auditor walks.
- The map is reviewed twice per release: peer review by row owners, gate review by the governance side. Both reviews are recorded as header attestations.
- The map is handed to the L50 architect for enterprise reconciliation; recurring aggregate queries drive control-library reconciliation, capacity signal, framework-refresh calendar, and market-entry decisions.
- External-audience projections (notified body, LL 144 auditor, Big Four, AISI-style evaluator) are filtered variants of the same map; the card-side lives in `mod-105`.
- The exercises walk the schema: exercises 01–06 populate the rows layer by layer, and a mature programme executes the whole workflow at each release-gate run.
