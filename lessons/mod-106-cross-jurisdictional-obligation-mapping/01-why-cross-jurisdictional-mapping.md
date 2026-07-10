# Why a Cross-Jurisdictional Obligation Map

## Motivation

By the time this role is running the release-assurance methodology at scale, one AI system is almost never governed by a single instrument. A hiring-tool product ships to European employers under the EU AI Act, to Illinois and NYC employers under state and city AEDT rules, to UK employers under the ICO's AI guidance, to Canadian employers under provincial human-rights instruments (and eventually AIDA), and to Singapore employers under the Model AI Governance Framework — while the same model card, the same evaluation evidence, and the same post-market plan have to hold up against all of them.

If the assurance program authors a separate release-gate for each instrument, the release cadence collapses under duplication and each map drifts. If it authors a single release-gate and *hopes* the mapping across instruments is right, an in-scope obligation eventually goes uncovered and the program cannot answer an auditor.

The way out is a **cross-jurisdictional obligation map**: one canonical inventory of obligations, produced per system, where every row is *one obligation from one instrument* and the columns identify the deliverable that discharges it, the peer role that owns the deliverable, and the sibling framework clauses that carry the same obligation. The map is a working artefact of the release-assurance methodology; it is also the hand-off contract to the level-50 `senior-ai-governance-architect`, who consumes it and reconciles obligations *across* systems at institution scope.

This module teaches how to build that map — starting from the EU AI Act as the statutory anchor and layering NIST AI RMF, ISO/IEC standards, US state and city rules, non-EU jurisdictional overlays, and Singapore's AI Verify testing framework onto it.

## What the map is (and what it is not)

The map is:

- **Per-system** — every AI system with a release-gate has its own map. Two systems with different intended purpose, deployment surface, and affected populations get two maps, even if the model behind them is the same. The architect reconciles *across* maps.
- **Obligation-normal** — one row per obligation from one instrument. If two instruments carry the same-shape obligation (e.g. EU AI Act Article 12 record-keeping and ISO/IEC 42001 clause 7.5.3 documented information), each gets its own row, and both rows point at the same deliverable and cross-reference each other.
- **Deliverable-linked** — every row names a concrete deliverable: a document, a signed artefact, a passing evaluation report, a card section, a signed declaration. "Policies are in place" is not a deliverable; "policy `SEC-AIRM-v3` signed by the CISO on 2025-11-04, stored at `assurance/policies/SEC-AIRM-v3.pdf` with digest `sha256:…`" is.
- **Owned per row** — the peer role that produces the deliverable is named on the row. Not "someone on the platform team." One role.
- **Static enough to diff** — the map is versioned. Two consecutive versions produce a diff that the architect can review as a change control.

The map is **not**:

- A legal opinion. It is an engineering artefact. Legal counsel signs off on the classification and interpretation calls; the map records those calls and cites where they came from.
- A control library. The control library lives at the L50 architect layer (`senior-ai-governance-architect`) and is *derived from* aggregating many maps. Do not try to author the control library from inside one system's map.
- A substitute for the underlying frameworks. It is a *cross-reference* into them. The reader is expected to open the primary text — the EU AI Act at EUR-Lex, NIST AI 100-1 at NIST, the ISO clauses in the ISO catalogue — for the authoritative language.

## Why the EU AI Act is the anchor

Every jurisdictional map has to pick an anchor: the reference frame the other columns are aligned against. In 2026 the natural anchor is the EU AI Act, for four reasons.

1. It is the only horizontal AI **regulation** currently in force with statutory obligations that are concrete enough to enumerate row-by-row. Its Chapter III, Section 2 (Articles 9–15) covers risk management, data governance, technical documentation, record-keeping, transparency, human oversight, and accuracy / robustness / cybersecurity; its Chapter V covers GPAI; Chapter IX covers post-market monitoring and reporting.
2. Its obligation shape (technical documentation, human oversight, post-market monitoring, serious-incident reporting, conformity assessment) is the pattern other jurisdictions are converging on. Anchoring on it minimises rework as new instruments come online.
3. It carries a formal **notified-body** interface for a subset of high-risk cases (Article 43, Annex VII), which forces the map into a shape a third-party auditor can consume — the same shape any independent evaluator (AISI-style) or Big Four assurance team will expect.
4. The associated primary artefacts — the **EU declaration of conformity** (Article 47 / Annex V), the **technical documentation** dossier (Article 11 / Annex IV), the **post-market monitoring plan** (Article 72) — are already deliverables the release-gate is producing under other names. Making them the columns of the map avoids inventing new artefacts.

The anchor choice is deliberate — but it is also fragile. If the release-gate is for a system with *no* EU exposure, the anchor should be re-picked (typically NIST AI RMF for a US-only footprint, ISO/IEC 42001 for an institution certifying its management system, or a sector rule like SR 11-7 for a US-regulated bank). Chapter `02` walks the EU AI Act anchor; chapters `03`–`07` layer the other frames on top.

## The four layers of the map

The map has four layers, and each subsequent chapter of this module builds one:

1. **Statutory anchor** — EU AI Act. Chapter `02` turns each in-scope article into a concrete deliverable.
2. **Cross-framework spine** — NIST AI RMF (with the GenAI Profile / AI 600-1) and ISO/IEC standards (42001, 23894, 42005, 25059, 24029-2). Chapters `03` and `04` cross-tag each deliverable to the sub-category or clause that carries the same obligation.
3. **Jurisdictional overlays** — US state/city rules (Colorado AI Act, NYC Local Law 144, CFPB adverse-action-notice circulars, EEOC AI / ADA guidance) and non-EU overlays (UK ICO, Australia VAISS, Canada AIDA, Japan METI, South Korea AI Framework Act, PRC CAC GenAI Interim Measures, Brazil PL 2338/2023). Chapters `05` and `06` add these on top of the anchor.
4. **Interoperability reference** — Singapore IMDA AI Verify Foundation's testing framework and Model AI Governance Framework, treated as the interoperability layer that lets one evaluation battery satisfy overlapping obligations from multiple jurisdictions. Chapter `07` walks this.

Chapter `08` closes the module by writing the map itself — the schema, the emission format, and the review workflow that hands it to the L50 architect.

## Who consumes the map and how

Three consumers matter, and the map is shaped for all three.

- **The release-gate itself (this role).** During a gate, the map is walked row-by-row: for each obligation, is the deliverable present, signed, and current? Any row without a green deliverable is either a fail, a deferred pass with an accepted residual, or an in-flight blocker.
- **The L50 senior architect.** The architect reads *many* maps together and asks: which deliverables are shared across systems (candidates for a common control), which obligations are consistently uncovered (control-library gaps), which peer roles are chronically over-tasked (staffing signal), which jurisdictions carry the largest incremental burden per system (regulatory-strategy signal). The map format therefore has to be **machine-parseable**, and its column shape has to be identical across systems.
- **External audiences.** A notified body, a third-party evaluator, or a Big Four auditor consumes the map (or a filtered variant of it) as the top-level index into the release package. This is a light audit path: an auditor points at a row, asks "show me the deliverable," and the row's pointer resolves.

The map is not shown to end-users or to the general public. Card production for external audiences (`mod-105`) filters and rewrites; the map is an *internal-facing* engineering artefact.

## Where this shows up in the rest of the track

- `mod-101` established the four bodies of literature (NIST / ISO / EU AI Act / values baseline). This module is the operational cross-tab of those four, plus the jurisdictional overlays.
- `mod-102` (assurance-case engineering) — each obligation row on the map is discharged by an argument in the assurance case. The map is the outer index; the case is the argument.
- `mod-103` (release-gate architecture) — the gate schema carries the same obligation IDs the map does, so a gate fail on obligation `X` and a map row `X` refer to the same thing.
- `mod-104` (evidence pipeline) — the deliverable pointer on each row resolves into the pipeline's content-addressed store.
- `mod-105` (cards for external audiences) — the card's `regime` block is the audience-safe projection of the map.
- `mod-107` (sector-regulated assurance) — sector rules (SR 11-7, DORA, FDA GMLP) layer on top of this map. The sector map inherits the row shape from here.
- `mod-108` (deployment-tier gating) — the map carries a "tier applicability" column; the same obligation may be waived at tier 0 and required at tier 3.
- `mod-109` (third-party evaluator interface) — the map is the first artefact shipped to the third-party evaluator; the notified-body pathway (Article 43 / Annex VII) consumes it directly.
- `mod-110` (post-market surveillance) — Articles 61 and 72 rows on the map cite into the surveillance plan and back.
- `mod-111` (GPAI systemic-risk assurance) — Article 55 rows are joined with the GPAI Code of Practice commitments in a dedicated section.
- `mod-112` (owning an assurance program) — aggregate map reporting is one of the program-level dashboards.

## The chapter shape you will see in `02`–`07`

Each of the next six chapters follows a common shape:

1. **The instrument** — what it is, who issued it, its legal status, its scope.
2. **The obligations that touch a release-gate** — the specific articles, sections, or clauses that translate to release-gate evidence.
3. **The deliverable-mapping table** — for each obligation, the concrete deliverable this program produces and the peer role that owns it.
4. **The cross-reference back to the anchor** — how each row maps back to the EU AI Act (or, where the instrument *is* the anchor, how the anchor maps out to the other frames).
5. **Overlay-specific traps** — the parts of the instrument that look like they duplicate an EU obligation but do not, or that add a genuinely new obligation the anchor does not cover.

Chapter `08` then walks the schema of the map itself — what a row looks like, how it is versioned, how the machine-readable emission is signed, and how the architect consumes it.

## Summary

- A release-assurance program that ships across jurisdictions cannot maintain a separate release-gate per instrument; it maintains **one cross-jurisdictional obligation map per system**, with columns for the deliverable and the peer owner and rows for each obligation.
- The EU AI Act is the anchor because it is the only in-force horizontal AI regulation with concrete enough obligations to enumerate, and its obligation shape is what other jurisdictions are converging on.
- Layered on top: NIST AI RMF (with the GenAI Profile), ISO/IEC 42001 / 23894 / 42005 / 25059 / 24029-2, US state / city rules, non-EU jurisdictional overlays, and Singapore AI Verify as an interoperability reference.
- The map is consumed by the release-gate (internally), by the L50 architect (across systems for control-library reconciliation), and by third-party auditors and notified bodies (as the top-level index into the release package).
- Chapters `02`–`07` build the map layer by layer; chapter `08` writes the machine-readable schema.
