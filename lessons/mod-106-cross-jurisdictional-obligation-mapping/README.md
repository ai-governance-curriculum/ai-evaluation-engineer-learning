# mod-106-cross-jurisdictional-obligation-mapping: Cross-Jurisdictional Evaluation-Obligation Mapping

Builds the per-system **obligation map** the release-assurance methodology uses to keep one release-gate honest across many overlapping instruments. Anchors on the EU AI Act, cross-tags each obligation into NIST AI RMF (with the GenAI Profile / AI 600-1) and ISO/IEC 42001 / 23894 / 42005 / 25059 / 24029-2 clauses, layers US state / city rules (Colorado SB24-205, NYC Local Law 144, CFPB adverse-action-notice circulars, EEOC AI / ADA guidance) and non-EU jurisdictional rules (UK ICO, Australia VAISS, Canada AIDA + Quebec Law 25, Japan METI, South Korea AI Framework Act, PRC CAC GenAI Interim Measures, Brazil PL 2338/2023), and adopts Singapore AI Verify as the interoperability reference so one evaluation battery can discharge many overlapping obligations. Closes with the machine-readable schema and the L50 hand-off shape.

**Estimated effort:** 16 hours

## Learning objectives

- Translate EU AI Act evaluation obligations into concrete deliverables — Articles 9 (risk-management system), 10 (data governance), 11 (technical documentation, Annex IV), 12 (record-keeping), 13 (transparency), 14 (human oversight), 15 (accuracy / robustness / cybersecurity), 26 (deployer obligations), 43 (conformity assessment), 47 (declaration of conformity), 49 (registration), 61 (post-market obligations), 72 (post-market monitoring plan), and Annex III high-risk domains.
- Cross-tag the same deliverables against NIST AI RMF 1.0 (with the Generative AI Profile / AI 600-1) and ISO/IEC 42001, 23894, 42005, 25059, 24029-2 clauses.
- Add US state-level and city-level rules on top of the federal / EU baseline: Colorado AI Act (SB24-205), NYC Local Law 144 (AEDT), CFPB adverse-action-notice circulars, EEOC AI / ADA guidance.
- Add non-EU jurisdictional overlays: UK ICO AI guidance, Australian Voluntary AI Safety Standard, Canada AIDA (proposed), Japan METI Guidelines, South Korea AI Framework Act, PRC CAC GenAI Interim Measures, Brazil AI Bill (PL 2338/2023).
- Adopt Singapore IMDA AI Verify Foundation testing framework as an interoperability reference for cross-jurisdictional evaluation obligations.
- Emit a per-obligation coverage matrix that a senior architect (level 50) can consume for enterprise reconciliation.

## Lecture chapters

1. [`01-why-cross-jurisdictional-mapping.md`](01-why-cross-jurisdictional-mapping.md) — Why a per-system cross-jurisdictional obligation map is the artefact one release-gate maintains instead of a gate-per-instrument. The four-layer map (statutory anchor, cross-framework spine, jurisdictional overlays, interoperability reference). What the map is and is not. The three consumer audiences: release-gate, L50 architect, external auditors.
2. [`02-eu-ai-act-obligations-to-deliverables.md`](02-eu-ai-act-obligations-to-deliverables.md) — Article-by-article translation from statutory text to concrete deliverables for Articles 9, 10, 11 (Annex IV items 1–8), 12, 13, 14, 15 (with Article 15(5) attack-category sub-rows), 17, 26, 43, 47 (Annex V), 49, 61, 72, plus Annex III typing. The row shape used throughout the module. Recurring traps (substantial modification, reasonably foreseeable misuse, state of the art, placing on the market vs. putting into service, provider vs. deployer split).
3. [`03-nist-ai-rmf-crosswalk-with-genai-profile.md`](03-nist-ai-rmf-crosswalk-with-genai-profile.md) — Cross-tag each EU AI Act row into NIST AI RMF 1.0 sub-categories (MAP / MEASURE / MANAGE / GOVERN) with per-row rationales. Add the AI 600-1 GenAI-Profile risk categories (confabulation, information integrity, IP, information security, harmful bias, value-chain integration, obscene / degrading content, environmental impact) as a distinct row block for GenAI systems. Overlay NIST AI 100-2's adversarial-ML taxonomy on Article 15 cybersecurity sub-rows.
4. [`04-iso-clauses-crosswalk.md`](04-iso-clauses-crosswalk.md) — Cross-tag each row against ISO/IEC 42001 clauses 4–10 and Annex A controls (with Statement of Applicability status), ISO/IEC 23894 risk-management method clauses, ISO/IEC 42005 impact-assessment method clauses, ISO/IEC 25059 SQuaRE quality-attribute vocabulary, and ISO/IEC 24029-2 neural-network robustness method. The audit-trail discipline: from row to clause to method to deliverable.
5. [`05-us-state-and-city-overlay.md`](05-us-state-and-city-overlay.md) — Colorado SB24-205 (developer + deployer duties, consumer notice + appeal, AG disclosure), NYC Local Law 144 (independent bias audit, public summary, candidate notice), CFPB adverse-action-notice circulars 2022-03 / 2023-03 (specific and accurate reasons, reason-code fidelity), EEOC Title VII AI / UGESP four-fifths analysis + ADA screen-out and reasonable-accommodation. Enforcement asymmetries (AG-only, city civil penalty, private-litigation, criminal) that change residual-risk posture per row.
6. [`06-non-eu-jurisdictional-overlay.md`](06-non-eu-jurisdictional-overlay.md) — UK ICO AI guidance under UK GDPR (Article 22 explainability, Article 35 DPIA), Australian VAISS ten guardrails + Privacy Act APPs, Canada AIDA (pending) + Quebec Law 25 + PIPEDA, Japan METI AI Guidelines + APPI + AI Promotion Act 2025 + Hiroshima Code of Conduct, South Korea AI Framework Act + PIPA, PRC CAC GenAI Interim Measures + PIPL + DSL + CSL + GB/T 45654-2025, Brazil PL 2338/2023 + LGPD. Where each overlay shares a deliverable and where it adds genuinely new rows (individual rights, substantive content, jurisdiction-specific filings).
7. [`07-singapore-ai-verify-interoperability.md`](07-singapore-ai-verify-interoperability.md) — Singapore AI Verify Foundation's eleven principles as an interoperability reference. The AI Verify Toolkit's technical tests + process checks. Model AI Governance Framework and MGF-GenAI as the process spine. The one-run-many-rows discipline — how a single AI Verify report attaches to many rows across jurisdictions — and where it cannot (LL 144 independent audit, CFPB reason-code fidelity, ISO/IEC 42001 certified-body audit, PRC substantive content). Project Moonshot as the LLM-specific evaluation-battery reference.
8. [`08-map-schema-and-emission.md`](08-map-schema-and-emission.md) — The row schema, the map document header, the canonical instrument registry, YAML-for-authoring / canonical-JSON-for-emission split, Sigstore / JWS / CMS signing options, the versioning-and-diff protocol, the six status enum values, the two-phase review workflow (peer review + gate review), the L50 aggregate-handoff queries, external-audience filtered projections, and the anti-patterns to avoid.

## Structure

- `01-…md` … `08-…md`: lecture chapters (above).
- [`exercises/`](exercises/): six per-exercise prompts, each extending the map produced by the previous exercise. Solutions live in the paired `ai-evaluation-engineer-solutions` repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Exercises

The six exercises are cumulative — each picks up the map the previous exercise emitted and extends it one layer:

1. [`exercise-01-eu-ai-act-obligation-to-deliverable-map.md`](exercises/exercise-01-eu-ai-act-obligation-to-deliverable-map.md) — Invent one system, fix the scoping decisions, produce the EU AI Act anchor slice of the map (one row per in-scope article, each with a named deliverable and peer owner).
2. [`exercise-02-nist-rmf-genai-profile-crosswalk.md`](exercises/exercise-02-nist-rmf-genai-profile-crosswalk.md) — Extend every row with NIST AI RMF sub-categories, AI 600-1 GenAI-Profile risk categories and Playbook suggested actions, and AI 100-2 attack-taxonomy branches on Article 15 sub-rows. Add the GenAI-Profile row block.
3. [`exercise-03-iso-clauses-crosswalk.md`](exercises/exercise-03-iso-clauses-crosswalk.md) — Extend every row with ISO/IEC 42001 clauses and Annex A controls, plus 23894 / 42005 / 25059 / 24029-2 method-standard references. Draft the Statement of Applicability fragment.
4. [`exercise-04-us-state-overlay-colorado-nyc-cfpb-eeoc.md`](exercises/exercise-04-us-state-overlay-colorado-nyc-cfpb-eeoc.md) — Overlay Colorado SB24-205, NYC LL 144, CFPB circulars, and EEOC Title VII / ADA guidance. Draft the NYC LL 144 audit plan and the CFPB reason-code methodology.
5. [`exercise-05-non-eu-overlay-uk-au-ca-jp-kr-cn-br.md`](exercises/exercise-05-non-eu-overlay-uk-au-ca-jp-kr-cn-br.md) — Overlay the seven non-EU jurisdictions. Handle pending-instrument (AIDA, Brazil PL 2338) and gate-preceding (PRC algorithm filing, Korean in-country representative) rows honestly.
6. [`exercise-06-ai-verify-interoperability-mapping.md`](exercises/exercise-06-ai-verify-interoperability-mapping.md) — Add the AI Verify interoperability layer to every row. Author the toolkit configuration from the map's evaluation demand, run the coverage audit, and record the interop-gap register for obligations AI Verify cannot discharge. Hand the map to the L50 architect.

## Suggested pace

- **Chapter `01`** — read once. It fixes the vocabulary (map, row, obligation-normal, deliverable-linked, sibling frames) that the rest of the module presumes.
- **Chapter `02`** — read alongside the [EU AI Act text at EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), particularly Chapter III Section 2 (Articles 8–15). Exercise `01` walks this chapter into a working map.
- **Chapters `03` and `04`** — read as a pair. The RMF and ISO crosswalks are structurally analogous — RMF gives analytical vocabulary; ISO gives audit vocabulary. Exercises `02` and `03` extend the map with each.
- **Chapter `05`** — read alongside the [Colorado SB24-205 text](https://leg.colorado.gov/bills/sb24-205) and the [NYC DCWP LL 144 rule](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf) at hand. Exercise `04` extends the US-side overlay.
- **Chapter `06`** — read once, then re-read the specific sub-section for each jurisdiction your system actually touches. Do not try to master all seven at once. Exercise `05` walks a scoped subset.
- **Chapter `07`** — read alongside the [AI Verify Foundation site](https://aiverifyfoundation.sg/) and (for GenAI systems) the [MGF-GenAI PDF](https://aiverifyfoundation.sg/wp-content/uploads/Model-AI-Governance-Framework-for-Generative-AI-May-2024-1-1.pdf). Exercise `06` closes the module.
- **Chapter `08`** — read at the end, after the crosswalk chapters. The schema falls into place once you know what the columns are carrying.

## Dependencies

- Requires `mod-101` (release-assurance position — the four bodies of literature this module cross-tabs), `mod-102` (assurance-case engineering — each row's obligation is discharged by an argument in the case), `mod-103` (release-gate architecture — the gate schema carries the same obligation IDs), `mod-104` (evaluation evidence pipeline — every `evidence_pointer` on a row resolves in the pipeline), and `mod-105` (cards for external audiences — the card's `regime` block is a filtered projection of the map).
- Consumed by `mod-107` (sector-regulated assurance — sector rules like SR 11-7, DORA, FDA GMLP layer on top of this map), `mod-108` (deployment-tier gating — the `tier_applicability` column decides which rows apply per tier), `mod-109` (third-party evaluator interface — the notified-body pathway consumes the map directly), `mod-110` (post-market surveillance — Articles 61 and 72 rows cite into the surveillance plan), `mod-111` (GPAI systemic-risk assurance — Article 55 rows and Hiroshima commitments join here), and `mod-112` (owning an assurance program — aggregate map reporting is a programme-level dashboard).
- The `senior-ai-governance-architect` (level 50) consumes the emitted map artefact for enterprise reconciliation; this role is one level below and one map-per-system upstream of the architect.
