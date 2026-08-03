# exercise-04: PCCP and Article 72 Interaction

**Estimated effort:** 3 hours

## Objective

Author the **unified monitoring runbook and evidence-tagging discipline** for one AI-enabled medical device that is both FDA-cleared under a **Predetermined Change Control Plan (PCCP)** and CE-marked as an Annex III high-risk AI system under the EU AI Act. Produce the crosswalk that maps AI-Act obligations to PCCP sections (defending the Article 72(3) equivalence argument per obligation), the unified monitored-characteristics table with regulatory-scope tags, the tagged evidence-store schema with max-across-regimes retention, the corrective-action register with dual sign-off routes, and the single incident-triage that emits multi-clock notifications from one incident identifier.

The PCCP itself is drafted by the manufacturer's regulatory-affairs function — the exercise wires the *assurance surface* around it. The load-bearing artefact is the crosswalk: it is the controlled document that a market-surveillance authority (AI Act) and an FDA inspector both consume when they walk the programme.

## Prerequisites

- Chapter [`04-fda-pccp-and-continuous-change-control-alongside-article-72.md`](../04-fda-pccp-and-continuous-change-control-alongside-article-72.md) — the PCCP three components, the four divergences, the unification pattern, the crosswalk as a controlled document, the worked chest-X-ray triage example, five anti-patterns.
- Chapter [`01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md`](../01-eu-ai-act-article-72-and-the-post-market-monitoring-plan.md) — the nine-section plan structure the crosswalk maps into.
- Chapter [`02-eu-ai-act-article-73-serious-incident-workflow.md`](../02-eu-ai-act-article-73-serious-incident-workflow.md) — the Article 73 triage that the incident-triage-with-two-clocks artefact extends.
- Familiarity with `mod-104` chapter `01` (`retention_class` and `regulatory_scope` fields on evidence artefacts), `mod-107` (SR 11-7, GMLP, and the wider sector-overlay pattern PCCP is a specific case of), and ISO/IEC 42001 clause 7.5 (the crosswalk is a controlled document).
- FDA guidance on [Predetermined Change Control Plans for Artificial Intelligence-Enabled Device Software Functions (2024)](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions).
- 21 CFR Part 803 (Medical Device Reporting), 21 CFR Part 820 (Quality System Regulation) with QMSR final rule effective 2026-02-02, and 21 CFR Part 801 (Labeling).
- Regulation (EU) 2024/1689 Article 72(3) equivalence clause, plus Regulation (EU) 2017/745 (MDR) as the sector-parallel post-market-surveillance regime.

## Problem statement

Pin one AI-enabled medical device software function that is (a) FDA-cleared with a PCCP and (b) CE-marked and placed on the EU market as an Annex III high-risk AI system (medical devices are Annex III high-risk under the Regulation via the intersection with EU sector legislation). The choice must:

- **Have a plausible PCCP envelope.** The manufacturer has plausibly named specific modifications the PCCP authorises — retraining on refreshed data on a stated cadence, tightening / loosening of decision thresholds within pre-specified bounds, expansion to additional imaging-device manufacturers under a pre-specified compatibility protocol, or similar.
- **Have a plausible FDA classification.** A 510(k), De Novo, or PMA pathway is named; the class II or class III device-classification is stated.
- **Have a named notified body for the CE-marking pathway.** Article 43 pathway (Annex VII) with a notified-body identifier placeholder.
- **Have named deployers.** Hospitals or hospital networks in the US and in the EU.

Common shapes worth considering (pick one — do not reuse chapter `04`'s chest-X-ray triage example verbatim):

- **Continuous-glucose-monitor closed-loop insulin-dose recommender** — the PCCP envelope covers retraining on refreshed cohort data; the AI Act monitored characteristics span accuracy on target-glucose-range percentage plus subgroup parity across paediatric and adult populations.
- **Radiology-workflow prioritisation model** — the PCCP envelope covers threshold tightening as clinical validation accumulates; the AI Act monitored characteristics span sensitivity on urgent findings plus fairness on rural-versus-urban imaging-device populations.
- **In-hospital deterioration-prediction scoring model** (early-warning-score augmentation) — the PCCP envelope covers retraining on refreshed EHR data; the AI Act monitored characteristics span sensitivity/specificity plus subgroup parity across race and age.
- **Retinal-imaging diabetic-retinopathy classifier** — the PCCP envelope covers expansion to additional retinal-imaging camera manufacturers; the AI Act monitored characteristics span sensitivity/specificity plus fairness on skin-tone and race.

Pin the device shape, the FDA classification, the PCCP envelope's three components (at summary level — the exercise does not require full PCCP authoring), the notified body, and the deployer set before drafting.

## Requirements

Produce five artefacts in a single directory.

### 1. `unified-crosswalk.md`

The crosswalk chapter `04` names as a controlled document under ISO/IEC 42001 clause 7.5. One row per obligation-and-regime combination. At least 15 rows. Columns:

- **Obligation identifier** — the specific citation (e.g., "Article 72 section 3 monitored characteristic: per-class sensitivity", "PCCP modification-protocol activity: performance verification", "21 CFR 820.100 corrective and preventive action", "ISO 13485 clause 8.5.2 corrective action", "MDR Article 83 post-market surveillance system").
- **Regime** — AI Act / PCCP / FDA QSR (or QMSR) / ISO 13485 / MDR.
- **Evidence artefact class that discharges it** — the specific artefact class in the store (per `mod-104` chapter `02`).
- **Owner peer track** — the peer whose methodology produces the evidence.
- **Cadence** — how often the evidence is refreshed.
- **Applicable-authority tag** — which authority reads this row's evidence (FDA, EU market-surveillance authority, notified body, sector-specific).
- **Equivalence argument** — for AI Act obligations discharged through a PCCP or sector activity under Article 72(3), the specific argument that the sector activity provides equivalent protection. For AI Act obligations not covered by any sector activity, an explicit "gap; discharged separately by Article 72 monitor" note. For sector obligations not covered by any AI-Act activity, an explicit "sector-only; discharged separately" note.

Coverage requirements:

- All nine Article 72 plan sections are represented in at least one row.
- The PCCP three components (description of modifications; modification protocol; impact assessment) are each represented.
- 21 CFR Part 803 (MDR reporting), 21 CFR Part 820 (QSR / QMSR), and ISO 13485 are each represented.
- At least one MDR (Regulation (EU) 2017/745) row where the AI Act's Article 72(3) equivalence with the MDR post-market-surveillance regime is defended.
- At least one *gap* row where the AI Act obligation is not equivalent to any sector activity and must be discharged separately (e.g., the fundamental-rights framing chapter `04` names — sector rules do not carry fundamental-rights language; the AI Act monitor must).

### 2. `unified-monitored-characteristics-table.md`

Extend chapter `04`'s illustrative table to at least 10 rows for the picked device. Columns:

- **Monitored characteristic** — the concrete characteristic observed.
- **Metric** — the specific measurable quantity.
- **AI Act obligation** — the Chapter III Section 2 Article (or Annex III cross-reference).
- **FDA / PCCP obligation** — the PCCP modification-protocol activity or the 21 CFR reference the metric discharges.
- **Sector-rule obligation** — the ISO 13485 clause or the 21 CFR 820 / QMSR reference the metric additionally discharges (where applicable).
- **Regulatory-scope tag set** — the multi-valued tag (e.g., `["eu-ai-act-article-72", "fda-pccp", "iso-13485-8.2.6"]`).
- **Source peer** — the peer track that produces the evidence.
- **Cadence** — refresh cadence.

Coverage requirements:

- At least one row where the characteristic discharges *both* Article 15 (accuracy) and PCCP performance verification.
- At least one row where the characteristic discharges *both* Article 10 (data governance) and PCCP modification-protocol data-management.
- At least one row where the characteristic is *fundamental-rights framed* (subgroup parity) and does NOT collapse into an FDA framing — this is the chapter `04` divergence chapter is explicit about.
- At least one row where the characteristic is a cybersecurity supply-chain check (Article 15 cybersecurity + FDA cybersecurity guidance).
- At least one row where the characteristic is an *adverse-event rate* that could escalate to Article 73 and to FDA MDR reporting in parallel.

### 3. `evidence-store-tagging-schema.md`

The store schema chapter `04` sketches, formalised.

- **Artefact-level fields**:
  - `regulatory_scope` — multi-valued list drawn from a controlled vocabulary (`eu-ai-act-article-72`, `eu-ai-act-article-73`, `fda-pccp`, `fda-mdr`, `iso-42001-9.3`, `iso-13485-8.2.6`, `mdr-article-83`, `gdpr-article-33`, and so on for the deployment's applicable regimes).
  - `retention_class` — multi-valued list, one entry per applicable regime; the store applies the *maximum* retention across regimes. Include the AI Act 10-year retention under Article 18 and the FDA device-life-plus-2-year retention; state the max-across-regimes rule explicitly.
  - `applicable_authority_tags` — the authority views the artefact is exposed under (FDA / EU market-surveillance authority / notified body / DPO).
- **Separable audit-views** — the query that produces each view:
  - `fda_inspector_view` — artefacts tagged `fda-*` or `iso-13485-*` or `mdr-*`.
  - `eu_market_surveillance_view` — artefacts tagged `eu-ai-act-*` or `mdr-*` (MDR is EU sector legislation feeding into AI Act's Article 72(3) equivalence).
  - `notified_body_view` — artefacts referenced by the Annex VII conformity-assessment file or by the ISO 13485 QMS documentation.
  - `dpo_view` — artefacts tagged `gdpr-*`.
- **Content-address discipline** — every artefact carries a `sha256:…` digest and a producer signature (DSSE per `mod-104` chapter `01`); every scope-tag change is a supersession, not an edit.
- **Max-retention worked example** — one artefact worked through: e.g., an evidence artefact tagged both `eu-ai-act-article-72` (10y) and `fda-pccp` (device-life + 2y); if the device-life is 15 years, the max is 17 years, and the artefact expires no earlier than that.
- **Cross-reference** to `mod-104` chapter `01`'s content-addressed store discipline; note that the tagging discipline extends but does not replace the base store.

### 4. `corrective-action-register-with-dual-signoff.md`

The corrective-action register with dual sign-off routes. Schema and worked example rows.

**Schema fields** (per row):

- Proposed change — natural-language description.
- PCCP-envelope determination — one of `in-envelope`, `out-of-envelope`, `new-envelope-required`. Co-signed by manufacturer's regulatory-affairs function.
- Article 20 disposition — one of `bring-into-conformity`, `withdraw`, `disable`, `recall`. Co-signed by release-owner and second-line signer.
- Discharging evidence artefact — the artefact class and digest the change produces as evidence of implementation.
- Sign-off routes per regime — AI Act (release-owner + second-line + head-of-AI-governance for withdrawal or T3+); FDA (QMS quality-manager + PCCP-owner regulatory-affairs); notified body notification where change is a substantial modification.
- Notification obligations triggered — AI Act market-surveillance authority notice (if any), FDA notice (submission required, or Section 806 correction/removal report, or none), notified-body notification of substantial modification (if any).
- Wall-clocks — one wall-clock per notification obligation.

**Worked example rows** — at least three:

1. **In-envelope** — the drift shown in the picked device's monitored-characteristics table triggers a retraining that is within the PCCP-authorised envelope. Retraining is executed under the PCCP modification protocol; verification evidence discharges both the Article 20 corrective action (AI Act — bringing declared Article 15 accuracy back into conformity) and the PCCP verification obligation. One evidence artefact; two authority scopes. No new FDA submission; no market-surveillance-authority notice; possible notified-body notice depending on Article 43 substantial-modification test.
2. **Out-of-envelope requiring new FDA submission** — a subgroup regression (e.g., paediatric under-performance) is proposed to be fixed by adjusting the intended patient-population statement; the change is *not* in the PCCP envelope (which anticipated retraining, not intended-population changes). A new FDA marketing submission is required; concurrently the Article 72 plan is amended to reflect the narrower intended purpose; the Article 13 instructions for use are updated; the notified body is notified of the substantial modification.
3. **Labelling-only update** — a wording clarification in the deployer-facing user manual that the FDA guidance treats as a labelling update under 21 CFR Part 801 and the AI Act treats as an Article 13 transparency update. One workflow, two regimes' labelling requirements discharged. No submission required in either regime; the deployer distribution is coordinated with the manufacturer's regulatory-affairs function.

### 5. `single-incident-two-clocks-triage.md`

The incident-triage extension of chapter `02`, showing how one triage produces multiple notifications on independent wall-clocks from one shared incident identifier.

**Triage extension** — the additional determinations the triage runs when the incident implicates a device under this exercise:

- AI Act Article 73 classification against Article 3(49) — usually the *health-harm* disjunct for medical devices, occasionally the *fundamental-rights* disjunct where subgroup regression at scale, occasionally the *serious-and-irreversible critical-infrastructure disruption* disjunct where the device supports critical clinical infrastructure.
- FDA MDR reportability under 21 CFR Part 803 — is the event *reportable* under 21 CFR 803.50 (30-day report for events involving death or serious injury, or events that could contribute); is it reportable under 21 CFR 803.53 (5-working-day report for events requiring remedial action to prevent unreasonable risk of substantial harm). Mark `<!-- needs-research: verify the current wall-clocks in 21 CFR 803.50 and 803.53 as of 2026-07 -->`.
- GDPR Article 33 breach reportability — is personal health data involved? If yes, 72-hour clock runs to the supervisory authority.
- Notified-body notification obligation — does the incident indicate a substantial modification will be required (feeding into artefact 4's out-of-envelope path)?

**Shared incident identifier** — one identifier tags every notification, every corrective-action record, every re-review, and every superseding-assurance-bundle entry.

**Notification chain** — one row per notification, columns: authority, regime, wall-clock, content-template reference (from exercise-02 artefact 3), signer.

**Worked example** — a pneumothorax-sensitivity drift (or the equivalent for the picked device) that meets multiple thresholds:

- Article 3(49) *serious harm to health* disjunct — Article 73 15-day outer clock (no death → not the 10-day inner clock; no widespread infringement → not the 2-day).
- FDA MDR reportable event — 30-day report under 21 CFR 803.50.
- PCCP-envelope excursion (the fix requires a change outside the envelope, triggering artefact 4's out-of-envelope route) — new FDA marketing submission needed; timing coordinated with the FDA MDR chain.
- GDPR Article 33 — 72-hour clock if the drift involved processing of identifiable personal health data at scale.

Walk the notification chain hour-by-hour, showing all four notifications lodged under the shared identifier with consistent facts.

## Starter guidance

- **PCCP is not a shield against Article 72.** Chapter `04` is emphatic — Article 72(3)'s equivalence clause requires the equivalence to be *demonstrated per obligation*, not asserted. The crosswalk (artefact 1) is the demonstration.
- **One runbook, one store, tagged.** Not two runbooks side-by-side, not two stores. The tagging discipline is what carries the dual regime.
- **Envelope inflation is a documented anti-pattern.** Chapter `04` names it — the manufacturer treats every new signal as within the PCCP envelope to avoid new-submission overhead; regulators eventually catch a modification that materially expanded intended use without a submission. The envelope determination in artefact 4 is co-signed with regulatory-affairs; borderline cases escalate to a formal FDA pre-submission discussion.
- **Deployer-channel signal must not get lost.** Signal from hospital deployers reaches the manufacturer's medical-safety function and must also reach the assurance runbook. Chapter `04` names this as an anti-pattern.
- **Retention is max-across-regimes plus margin.** An artefact that expires while the longer-retention regime still requires it is a compliance failure in the longer regime. Artefact 3's max-retention rule is non-negotiable.
- **One triage produces multiple notifications.** Article 73 + FDA MDR + GDPR + notified-body notification all run in parallel from one shared incident identifier. Divergent notifications on the same event are an audit finding in every regime.
- **Fundamental-rights framing does not collapse into FDA framing.** Chapter `04` names this divergence explicitly. Artefact 2 must carry at least one row that is fundamental-rights framed and does not have an FDA counterpart.
- **`<!-- needs-research: … -->` markers are legitimate.** The exact wall-clocks in 21 CFR 803, the QMSR final-rule transition-period considerations as of 2026-07, and specific PCCP-guidance clause numbers may drift. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `unified-crosswalk.md` has at least 15 rows covering all nine Article 72 sections, the PCCP three components, 21 CFR Part 803, 21 CFR Part 820 (QSR / QMSR), ISO 13485, and MDR Article 83; every row names an owner peer track, a cadence, and an applicable-authority tag; the equivalence argument is explicit per row (either equivalence-defended, gap-flagged, or sector-only-flagged); at least one gap row exists.
- `unified-monitored-characteristics-table.md` has at least 10 rows with every column populated; at least one Article-15-plus-PCCP-performance row, one Article-10-plus-PCCP-data-management row, one fundamental-rights row without FDA counterpart, one cybersecurity row, and one adverse-event row.
- `evidence-store-tagging-schema.md` covers artefact-level fields (`regulatory_scope`, `retention_class`, `applicable_authority_tags`), all four separable audit-views, the content-address discipline, and one worked max-retention example.
- `corrective-action-register-with-dual-signoff.md` has schema fields for every dual-regime consideration and at least three worked rows (in-envelope, out-of-envelope requiring new FDA submission, labelling-only). Sign-off routes are correct per chapter `04` and chapter `05`.
- `single-incident-two-clocks-triage.md` extends chapter `02`'s triage with the FDA MDR / GDPR Article 33 / notified-body determinations; the shared incident identifier binds all notifications; the worked example walks the notification chain hour-by-hour with all four notifications correctly routed.
- Every artefact is internally consistent — the same regulatory-scope tags in the crosswalk (artefact 1) and the store schema (artefact 3); the same incident identifier in the triage extension (artefact 5) and the corrective-action register (artefact 4).
- Every place a fact would need to be verified against the current FDA guidance clause numbering, the current 21 CFR wall-clocks, the QMSR transition-period rules, or the enterprise's own PCCP text is marked `<!-- needs-research: … -->` rather than guessed.

## Stretch goals

- **Extend the pattern to a device also under IVDR.** In `ivdr-overlay.md`, add the EU IVDR (Regulation (EU) 2017/746) obligations to the crosswalk for a device that is also an in-vitro diagnostic. The sector-clause set expands with performance-evaluation and clinical-performance-study obligations.
- **PCCP-envelope-borderline escalation path.** In `envelope-borderline-escalation.md`, walk the specific case where a proposed modification borderline-fits the PCCP envelope. Involve an FDA pre-submission meeting; document the pre-submission request package; walk the FDA feedback into the PCCP-versus-new-submission determination. Cite chapter `04`'s envelope-inflation anti-pattern.
- **Joint labelling-update workflow.** In `joint-labelling-workflow.md`, design the workflow so Article 13 instructions-for-use and FDA device labelling under 21 CFR Part 801 update as one workflow with two regulatory-scope tags. Include the deployer distribution coordination.
- **FDA GMLP guiding-principles alignment.** In `gmlp-alignment.md`, extend the crosswalk with rows that map to the FDA / Health Canada / MHRA Good Machine Learning Practice guiding principles. GMLP is not enforceable in itself but is cited by the FDA in evaluating PCCPs.
- **Tabletop rehearsal on a subgroup-parity finding.** In `subgroup-parity-tabletop.md`, author a tabletop-exercise script the release-assurance function runs against a subgroup-parity regression finding — showing the fundamental-rights framing (AI Act route) and the clinical-safety framing (FDA route) running in parallel from one triage.
