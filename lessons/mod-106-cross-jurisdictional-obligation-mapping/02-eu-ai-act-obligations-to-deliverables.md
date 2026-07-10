# EU AI Act — From Article Text to Concrete Deliverable

## Motivation

Chapter `01` picked the EU AI Act as the map's anchor. This chapter turns each in-scope article into a **concrete deliverable** — the document, the signed artefact, the signed evaluation report, the machine-readable declaration — that the release-gate produces and that the map row points at.

`mod-101` already walked *what the articles say* and their release-gate implication. The value this chapter adds is the mechanical translation from statutory text to a named artefact you can attach to a row. Where `mod-101` says "Article 12 is the statutory backing for the evidence pipeline," this chapter says: "Article 12 discharges as `logging-design-spec.md` v-N plus `retention-policy.yaml` v-N, signed by the platform-eng lead, digest-anchored in the pipeline, with a passing `log-completeness-report.json` produced by the eval pipeline at each release."

The chapter walks Articles 9, 10, 11 (with Annex IV), 12, 13, 14, 15, 26, 43, 47 (with Annex V), 49, 61, 72, and touches Annex III's high-risk-domain typing.

## The row shape used in this chapter

Every article below produces one or more map rows in the shape:

| Field | Content |
| --- | --- |
| `obligation_id` | Short stable ID unique within the map (e.g. `eu-ai-act.art9`, `eu-ai-act.art11.annex-iv.7`) |
| `instrument` | `eu-ai-act-2024-1689` |
| `article_or_clause` | Article and sub-paragraph reference |
| `obligation_summary` | One-sentence paraphrase — the map is not the primary text |
| `applies_when` | Scope condition ("high-risk provider," "high-risk deployer," "GPAI with systemic risk," "high-risk deployer that is a public authority") |
| `deliverable` | Named artefact (path or content-addressed digest) |
| `deliverable_kind` | `document` / `report` / `declaration` / `plan` / `card` / `log-attestation` |
| `owner_role` | Peer role responsible for producing the deliverable |
| `signing_role` | Role whose signature closes the deliverable |
| `sibling_nist_rmf` | Sub-category reference — filled in chapter `03` |
| `sibling_iso_clauses` | Clause references — filled in chapter `04` |
| `tier_applicability` | Deployment tiers on which the row applies (from `mod-108`) |
| `status` | `covered` / `partial` / `open` / `waived-with-residual` |
| `evidence_pointer` | Content-addressed digest into the evidence store (`mod-104`) |

The rows below are shown in a compressed form. Chapter `08` gives the full JSON / YAML schema.

## Deliverable mapping, article by article

### Article 9 — Risk-management system

**Deliverables.**

- `risk-management-plan-v<N>.md` — the standing document. Its shape is dictated by `mod-102` (assurance-case engineering); the plan is the outer envelope of the case.
- `harm-inventory-v<N>.yaml` — machine-readable inventory of identified and reasonably-foreseeable harms, tagged by intended purpose, misuse scenarios, and affected populations. Produced by `ai-risk-engineer`.
- `residual-risk-register-v<N>.yaml` — residuals accepted at the gate, each with an escalation owner. Signed by the assurance-methodology owner (this role) and countersigned by the L60 head of AI governance for anything above tier 2.
- `post-market-feedback-loop-spec.md` — the loop that lets Article 72 data update Article 9. Cross-references the post-market plan under Article 72.

**Owner:** `ai-risk-engineer` for the harm inventory; this role for the plan, register, and loop spec.

**Row count in the map:** at least three (`eu-ai-act.art9.plan`, `eu-ai-act.art9.harms`, `eu-ai-act.art9.residuals`), because the assurance-case discharge is different for each.

**Trap.** Article 9 is *continuous*, not one-shot. A release-gate that produces a v-1 plan and never updates it is out of compliance. The map's `status` for the Article 9 rows must be re-verified per release, not per system.

### Article 10 — Data and data governance

**Deliverables.**

- `dataset-cards/` — one card per training, validation, testing, and (where applicable) evaluation dataset. Cards follow Gebru et al. plus ISO/IEC 8183 lifecycle framing (see `mod-105`).
- `data-governance-plan-v<N>.md` — the standing plan covering collection processes, preparation, purpose-appropriateness, and bias / gap / shortcoming examination.
- `bias-and-shortcoming-report-v<N>.md` — the examination result, produced by `ai-risk-engineer` with input from `model-evaluation-engineer`.
- `data-lineage-manifest.json` — SPDX-AI / ML-BOM tagged data-lineage manifest, produced by the evidence pipeline (`mod-104`).

**Owner:** `ai-governance-analyst` and `ai-risk-engineer` on the substantive content; this role signs off that the deliverable set discharges the article.

**Trap.** Article 10(5) allows processing of special categories of personal data *only* to the extent strictly necessary for bias detection and correction, and subject to safeguards. The map must flag whether the deliverables invoke Article 10(5); if so, the safeguards themselves become a sub-row, and legal counsel signs.

### Article 11 — Technical documentation (Annex IV)

Annex IV is a **numbered content list**, and each numbered item is one map row.

| Annex IV section | Deliverable | Owner |
| --- | --- | --- |
| 1. General description | `sysdoc/01-general-description.md` | this role |
| 2. Detailed description of the elements and process of development | `sysdoc/02-elements-and-process.md` | `ai-eval-engineer` + platform-eng |
| 3. Monitoring, functioning, control | `sysdoc/03-monitoring-and-control.md` | this role |
| 4. Risk-management system per Article 9 | pointer to Article 9 rows above | this role |
| 5. Changes made through the lifecycle | `sysdoc/05-change-log.md`, signed diffs | platform-eng release owner |
| 6. Standards applied and description of solutions | `sysdoc/06-standards-applied.md` (harmonised standards / ISO clause references) | this role |
| 7. Copy of the EU declaration of conformity | pointer to Article 47 row below | this role |
| 8. Post-market monitoring plan per Article 72 | pointer to Article 72 row below | this role |

**Owner:** this role assembles and signs the dossier; substantive content comes from named peers.

**Row count in the map:** eight, one per Annex IV item. Rows 4, 7, 8 are pointers to other rows and should be typed as `deliverable_kind: cross-ref`.

**Trap.** Annex IV is the *internal* dossier. The publicly-facing system card (`mod-105`) is derived from it but is not the same document. A map that collapses them into one row loses the audit trail.

### Article 12 — Record-keeping (logs)

**Deliverables.**

- `logging-design-spec-v<N>.md` — what is logged, at what granularity, with what identifiers. Owned by platform-eng; cross-signed by `ai-eval-engineer` for eval-adjacent events.
- `retention-policy-v<N>.yaml` — machine-readable retention windows per log class.
- `log-completeness-report-v<N>.json` — passing evaluation of the logging surface (recording is actually occurring; retention is actually enforced). Produced by `ai-eval-engineer`.
- `log-signing-and-integrity-plan-v<N>.md` — how logs are made tamper-evident (append-only store, transparency log, notarisation). Owned by `ai-infra-security`.

**Owner:** platform-eng and `ai-infra-security` on the substantive content; this role signs off on the release-gate discharge.

**Trap.** Article 12(2) and 12(3) impose different retention floors depending on the system category. The retention policy must state which paragraph applies and cite it.

### Article 13 — Transparency and information to deployers

**Deliverables.**

- `instructions-for-use-v<N>.md` — the article-specified content list (provider identity, characteristics, performance, human-oversight measures, expected lifetime, maintenance). This is a specific artefact, distinct from the internal Annex IV dossier and distinct from the public card.
- `deployer-facing-card.md` — the deployer-audience variant of the system card from `mod-105`, derived from Article 11 dossier + instructions-for-use.
- `transparency-adequacy-review-v<N>.md` — a signed statement that the transparency deliverables discharge the article, with review notes.

**Owner:** this role produces the instructions-for-use and the transparency-adequacy review; the card variant comes from the card pipeline in `mod-105`.

**Trap.** "Instructions for use" is not "release notes." It has a statutory content list (Article 13(3)); the map's row for Article 13 should enumerate each of the (a)–(f) content items as sub-rows.

### Article 14 — Human oversight

**Deliverables.**

- `human-oversight-design-v<N>.md` — the standing design document: who oversees, at what step, with what interface, what authority to override / interrupt / not-use. Must address the article's specified duties (understanding capacities and limitations, awareness of automation bias, correct interpretation, decide not to use, override, interrupt).
- `human-oversight-usability-report-v<N>.md` — evaluated evidence that the design *actually enables* the overseer to meet those duties. Produced jointly by `ai-eval-engineer` (interaction traces) and a UX specialist; this role signs off.
- `automation-bias-training-log-v<N>.md` — record of the training given to overseers, cross-referenced with Article 26 obligations for deployer-facing systems.

**Owner:** this role signs off on the design and the usability report; UX and `ai-eval-engineer` produce the substantive content.

**Trap.** Human-oversight adequacy is *evaluated*, not asserted. A design document with no usability evidence is a red-flag row. Where the system is Annex III point 1 (biometric identification), Article 14(5) adds the two-natural-persons rule; the map must flag this as a sub-row.

### Article 15 — Accuracy, robustness, cybersecurity

**Deliverables.**

- `accuracy-threshold-declaration-v<N>.md` — declared accuracy metrics, thresholds, and rationale. Threshold rationale must cite the methodology from `model-evaluation-engineer`.
- `robustness-evaluation-report-v<N>.md` — evaluated evidence against ISO/IEC 24029-2 methodology (see chapter `04`).
- `cybersecurity-evaluation-report-v<N>.md` — evaluated evidence against NIST AI 100-2 taxonomy and ISO/IEC 27001-aligned controls for the model artefacts and eval sets.
- `accuracy-in-instructions-for-use.md` — the declared thresholds as they appear in the Article 13 instructions for use. Must match the declaration.

**Owner:** `model-evaluation-engineer` for accuracy methodology; `ai-risk-engineer` and `ai-infra-security` for robustness / cybersecurity substantive content; this role for the declaration and the cross-consistency.

**Row count in the map:** three at minimum (accuracy, robustness, cybersecurity), with sub-rows per attack category (data poisoning, model poisoning, adversarial examples, model evasion, confidentiality attacks) from Article 15(5).

**Trap.** Article 15(4) obliges systems that continue learning after deployment to be resilient against biased outputs influencing input; this creates a specific evaluation obligation the map must flag if the system supports online learning.

### Article 26 — Deployer obligations

Applies **only if** this role's system is being released as a deployer (or dual-hat). Deliverables track article sub-paragraphs:

| Sub-paragraph | Deliverable | Owner |
| --- | --- | --- |
| 26(1)(a)/(b) — appropriate technical and organisational measures | `deployer-tom-plan-v<N>.md` | this role |
| 26(2) — assign human oversight | `human-oversight-competence-record-v<N>.yaml` | HR + this role |
| 26(4) — input data governance | `input-data-representativeness-report-v<N>.md` | `ai-governance-analyst` |
| 26(5) — monitoring per instructions | `deployer-monitoring-plan-v<N>.md` | this role |
| 26(6) — log retention | pointer to Article 12 row | (cross-ref) |
| 26(7) — inform employees before use in workplace | `workplace-use-notice-v<N>.md` | HR + legal |
| 26(11) — inform natural persons subject to decision | `decision-subject-notice-v<N>.md` | product + legal |

**Trap.** Article 26(7) and 26(11) are not "nice-to-have" — they are statutory notice obligations. The map must carry them as distinct rows with legal countersign.

### Article 43 — Conformity assessment

**Deliverables.**

- `conformity-assessment-decision-record-v<N>.md` — which procedure was chosen (internal control per Annex VI vs. notified-body involvement per Annex VII) and why. Cites Annex III sub-point and Article 43 sub-paragraph.
- `notified-body-engagement-record-v<N>.md` — only where Annex VII applies. Named body, engagement letter, evidence-of-independence letter. Owned by legal + this role, cross-references the third-party interface in `mod-109`.
- `internal-control-audit-record-v<N>.md` — only where Annex VI applies. Evidence that internal-control conditions were met.

**Owner:** this role produces the decision record; legal signs the notified-body engagement.

**Trap.** Article 43 is not a per-release deliverable if the system is unchanged. It becomes re-triggered when a "substantial modification" occurs (Article 3(23)); the map must carry a rule for when the row is stale.

### Article 47 — EU declaration of conformity (Annex V)

**Deliverables.**

- `eu-declaration-of-conformity-v<N>.md` — machine-readable, following the Annex V content list. Signed by the provider's authorised signatory. Retained 10 years per Article 47(3).

Annex V requires: system name, provider name and address, statement of sole responsibility, references to the Act's relevant provisions and standards applied, place and date of issue, and signature. Each is a sub-field on the row.

**Owner:** this role produces; the authorised signatory (typically a corporate officer named in the QMS) signs.

**Trap.** A machine-readable declaration is required. The `.md` variant above should be paired with a `.json` (or XML) variant carrying the same content.

### Article 49 — Registration

**Deliverables.**

- `eu-database-registration-record-v<N>.yaml` — the registration reference number (once the EU database at Article 71 is populated) and the metadata submitted.

**Owner:** this role coordinates; the authorised representative in the EU submits.

**Trap.** Article 49 is a gate-*preceding* action for high-risk systems: the release-gate does not proceed until the registration reference is present. For public-authority deployers registering an Annex III use-case, the row applies at the deployer's release-gate too.

### Article 61 — Reporting of serious incidents

**Deliverables.**

- `serious-incident-response-plan-v<N>.md` — the standing plan: what qualifies as a serious incident under Article 3(49) and Article 61(1), the reporting-timeline table (Article 61 has different windows for different incident severities), the market-surveillance authority contact list, the internal escalation chain.
- `incident-drill-report-v<N>.md` — evidence that the plan has been drilled at least once per release cycle. Produced by `ai-risk-engineer`.

**Owner:** this role produces the plan; `ai-risk-engineer` runs the drill; legal signs the reporting-timeline table.

**Trap.** Article 61 timelines are strict and different from those in NIS2, DORA, and other EU incident regimes. The plan cannot re-use a generic incident SOP; it must cite Article 61 sub-paragraphs and state its stance where multiple regimes fire simultaneously.

### Article 72 — Post-market monitoring plan

**Deliverables.**

- `post-market-monitoring-plan-v<N>.md` — the plan itself. Its content is dictated by `mod-110`.
- `post-market-data-collection-configuration.yaml` — the machine-readable configuration of the data sources feeding the plan.
- `post-market-loop-review-report-v<N>.md` — at each release cycle, evidence that the loop is running, the data is being reviewed, and the risk-management system (Article 9) is receiving the input.

**Owner:** this role for the plan and the review report; platform-eng for the collection configuration.

**Trap.** The Article 72 template that the AI Office is expected to publish (per Article 72(3)) determines the plan's content shape. Until published, the plan follows the article's own text and is redrafted on publication. The map must carry the plan version and cite Article 72(3) explicitly.

### Annex III — High-risk-domain typing

Annex III is not an obligation per se; it is the *scoping* input that determines whether the Article 8–15 obligations apply. The map carries an Annex III row per applicable point:

| Row | Content |
| --- | --- |
| `eu-ai-act.annex-iii.<n>.<sub>` | Which Annex III point and sub-point the system falls under |
| `applies_when` | Empty (Annex III is scoping) |
| `deliverable` | `annex-iii-classification-decision-v<N>.md` |
| `owner_role` | `ai-governance-analyst` + legal |

The Annex III classification is signed by legal counsel and reviewed at each substantial modification.

## Consolidated view — what the deliverables set looks like

For a canonical high-risk provider system, the article set produces roughly these deliverable classes:

- **Standing documents** — risk-management plan, data-governance plan, logging design, retention policy, human-oversight design, serious-incident plan, post-market monitoring plan.
- **Reports** — bias-and-shortcoming, robustness, accuracy, cybersecurity, log-completeness, transparency-adequacy, oversight-usability, post-market-loop-review, incident-drill.
- **Declarations** — EU declaration of conformity, conformity-assessment decision, Annex III classification.
- **Cards** — dataset cards, deployer-facing system card (derived from `mod-105`), instructions for use.
- **Manifests** — data-lineage manifest (SPDX-AI / ML-BOM).
- **Records** — EU-database registration record, notified-body engagement record, workplace-use notice, decision-subject notice.

Every deliverable is content-addressed in the evidence pipeline (`mod-104`) and pointed to from its row on the map.

## Recurring traps across articles

- **"Substantial modification" (Article 3(23))** re-triggers most obligations. The map's `status` field is not durable — it must be re-verified per release, and per substantial modification.
- **"Reasonably foreseeable misuse" (Article 9(2)(b))** cannot be discharged only by intake documentation. The harm inventory has to be tested against the intended-purpose statement in the technical documentation.
- **"State of the art" (Article 8(2), Article 9(3), Article 15(1))** is a moving reference frame. The map must carry a "state-of-the-art snapshot" pointer per release, so a later auditor can see what was believed to be state of the art at gate time.
- **"Placing on the market" vs. "putting into service"** differ (Article 3(9) / (11)) and the applying obligations differ. The map's `applies_when` field must distinguish.
- **Provider vs. deployer hats** split the row set. A single organisation with both hats maintains two sets of rows and cross-references them.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — each Article 9 / 14 / 15 obligation on the map is discharged by a GSN / CAE / SACM argument.
- `mod-103` (release-gate architecture) — the gate schema carries a mandatory `eu_ai_act_article` field per obligation, matching the row IDs above.
- `mod-104` (evidence pipeline) — `evidence_pointer` on each row resolves here.
- `mod-105` (cards for external audiences) — dataset cards, deployer-facing card, and instructions-for-use variants are produced here.
- `mod-108` (deployment-tier gating) — the `tier_applicability` column decides which rows apply at which tier.
- `mod-109` (third-party evaluator interface) — Article 43 notified-body row hands off here.
- `mod-110` (post-market surveillance) — Articles 61 and 72 rows resolve into the surveillance plan.
- `mod-111` (GPAI systemic-risk assurance) — Article 55 rows are covered in `mod-111` and cross-cited from here.

## Summary

- Every in-scope EU AI Act article produces one or more concrete deliverables on the map: standing documents, reports, declarations, cards, manifests, and records.
- Article 11 (with Annex IV) and Article 47 (with Annex V) are content-listed — one row per numbered item, with an owner.
- Article 12 (record-keeping), Article 15 (accuracy / robustness / cybersecurity), and Article 14 (human oversight) are the highest-density rows and require passing reports, not just design documents.
- Annex III typing is the scoping input; without it, the Article 8–15 rows have no `applies_when`.
- Provider and deployer hats split the row set; a single organisation with both maintains two sub-maps and cross-references them.
- The map's status is per-release, not per-system; substantial modification (Article 3(23)) re-triggers most rows.
- Exercise 01 walks a fictional system through the article-to-deliverable table row by row; chapter `03` starts cross-tagging these rows into NIST AI RMF sub-categories.
