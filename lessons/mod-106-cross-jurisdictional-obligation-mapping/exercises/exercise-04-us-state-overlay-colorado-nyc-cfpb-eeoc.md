# exercise-04: US State and City Overlay — Colorado, NYC, CFPB, EEOC

**Estimated effort:** 2 hours

## Objective

Extend the map from exercises `01`–`03` with the **US-side overlay** — Colorado SB24-205 (developer + deployer), NYC Local Law 144 (AEDT bias audit), CFPB adverse-action-notice circulars (ECOA / Regulation B), and EEOC AI / ADA guidance (Title VII / UGESP / ADA). Where the US-side obligation shares a deliverable with an anchor row (frequently), record a cross-reference and do not duplicate the deliverable. Where the US-side adds a genuinely new obligation (consumer notice, AG disclosure, independent bias audit, reason-code fidelity, ADA screen-out, UGESP four-fifths analysis), add the new row with its own deliverable and owner.

## Prerequisites

- Chapter [`05-us-state-and-city-overlay.md`](../05-us-state-and-city-overlay.md).
- Exercises [`exercise-01`](exercise-01-eu-ai-act-obligation-to-deliverable-map.md), [`exercise-02`](exercise-02-nist-rmf-genai-profile-crosswalk.md), and [`exercise-03`](exercise-03-iso-clauses-crosswalk.md).
- [Colorado SB24-205 text](https://leg.colorado.gov/bills/sb24-205) — read at least the developer and deployer duty sections and the definitions (algorithmic discrimination, consequential decision, substantial factor, high-risk artificial intelligence system).
- [NYC Local Law 144 (AEDT) rules — DCWP final rule](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf) and the [DCWP AEDT FAQ](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page).
- [CFPB Circular 2022-03 (adverse-action notices in credit decisions based on complex algorithms)](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) and [CFPB Circular 2023-03 (adverse-action requirements with AI / complex predictive models)](https://www.consumerfinance.gov/compliance/circulars/circular-2023-03/).
- [EEOC — *Assessing Adverse Impact in Software, Algorithms, and AI Used in Employment Selection Procedures* (2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) and [EEOC — *The ADA and the Use of Software, Algorithms, and AI to Assess Job Applicants and Employees* (2022)](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence).

## Problem statement

Take the map from exercise `03` and add the US-side overlay rows. Before you author rows, produce a **scoping brief** that fixes the US-side classifications: is your system in scope of Colorado SB24-205 (developer, deployer, both, neither), of NYC LL 144 (employment position located in NYC), of CFPB Regulation B (credit decision, "substantial factor" in adjudication), of EEOC Title VII (adverse-impact analysis triggers), of ADA (screen-out analysis). Each classification is a legal call; note the reasoning and the required legal countersign.

Then extend the map with the overlay rows (using chapter `05`'s row shape), threading cross-references to anchor rows where the deliverable is shared, adding new deliverables where the obligation is genuinely new. Recognise the *enforcement-asymmetry* difference and adjust the `residual` posture where you have `waived-with-residual` rows.

If your exercise-`01` scenario deliberately has no US exposure, do not fabricate one — instead, pick one of the four instruments most closely relevant to the *shape* of your system (Colorado SB24-205 for a consequential-decision system, NYC LL 144 for an employment tool, CFPB circulars for a credit tool, EEOC for any employment tool) and produce the overlay *as if* you were extending to that US surface. The scoping brief must state this decision explicitly.

## Requirements

Produce four artefacts.

### 1. `us-scoping-brief.md`

A one-to-two page brief covering:

- **Colorado SB24-205 applicability.** Developer / deployer / dual-hat / not-in-scope. Cite the "high-risk AI system" definition, name your reasoning against the consequential-decision list, and note the "substantial factor" determination. Legal countersign required.
- **NYC LL 144 applicability.** Whether your system is an AEDT for a hiring / promotion decision of an NYC-located candidate or employee. Note the geographic scope determination.
- **CFPB / ECOA / Regulation B applicability.** Whether the system contributes to a credit decision within Regulation B's scope. Cite the "substantial factor" language from the circulars where applicable.
- **EEOC Title VII / UGESP applicability.** Whether the system is a "selection procedure" under UGESP. Note the vendor-immunity stance.
- **EEOC ADA applicability.** Whether the system is used to assess applicants or employees in ways that could raise a screen-out analysis.
- **Not-in-scope rows.** Rows you have determined do not apply, with reasoning and legal countersign. `not-applicable` is a valid map status; the reasoning has to be recorded.

### 2. `us-extended-map.yaml`

The exercise-`03` map, extended with the US-side rows. Every row (existing or new) that touches a US-side obligation gains:

- `sibling_us_state_or_federal` — list of overlay-row identifiers (e.g., `co-sb24-205.deployer.impact-assessment`, `nyc-ll-144.bias-audit`, `cfpb-adverse-action.specific-reasons`, `eeoc.title-vii.adverse-impact`).
- `relation` per sibling — `shares-deliverable | contributes-to | overlaps-partially | supersedes | superseded-by`.

Genuinely new US-side rows follow the full row shape from chapter `05` and the schema from chapter `08`. Required fields per new row:

- `obligation_id` — `co-sb24-205.*`, `nyc-ll-144.*`, `cfpb-adverse-action.*`, `eeoc.*` — as chapter `05` uses.
- `instrument` — canonical instrument ID (`co-sb24-205`, `nyc-ll-144`, `cfpb-circular-2023-03`, `eeoc-2023-adverse-impact-guidance`, `eeoc-2022-ada-guidance`).
- `instrument_version_pin` — version of record; for the CFPB circular the circular number and date; for EEOC the guidance publication date.
- `article_or_clause` — the section within the instrument.
- `obligation_summary` — one-sentence paraphrase.
- `applies_when` — per-row scoping condition with `determined_by: legal-counsel` and a determination date.
- `deliverable`, `deliverable_kind`, `owner_role`, `signing_role`, `tier_applicability`, `status`, `evidence_pointer`, `notes` — as before.
- `sibling_eu_ai_act` — cross-reference to the anchor row it shares a deliverable with, if any.
- `sibling_nist_rmf`, `sibling_iso_clauses` — extend the crosswalk into the RMF / ISO frames where applicable (fairness rows tag `MEASURE-2.11` and `ISO/IEC 42001:2023 A.7`; transparency rows tag `MEASURE-2.8` and `ISO/IEC 42001:2023 7.4`).
- `enforcement_route` — enum: `attorney-general-only | city-agency | federal-regulator | private-right-of-action | criminal | procurement-only`.
- `residual` — if `status: waived-with-residual`, note the enforcement route on the residual (a Colorado residual is a different exposure profile than an EEOC private-litigation residual).

The map header gains `frameworks_pinned.co-sb24-205`, `.nyc-ll-144`, `.cfpb-circulars`, `.eeoc-guidance` — each with the version-of-record.

### 3. `nyc-ll-144-audit-plan.md`

If NYC LL 144 is in scope, a short plan for the independent bias audit — the deliverable that closes the `nyc-ll-144.bias-audit` row. It must specify:

- The **independent auditor** you would engage (either name a real firm, or place a placeholder marker and note the selection criteria — no financial interest, no involvement in developing / using / distributing the tool).
- The **audit categories** (sex; race/ethnicity; intersectional sex × race/ethnicity — per LL 144's specified categorisation).
- The **data source** for the audit (historical data vs. test data; the DCWP rule permits either with restrictions).
- The **selection-rate impact-ratio table** shape the audit will produce.
- The **public summary** shape — how it will be published (deployer URL), what it will disclose, and how it will be dated.
- The **candidate / employee notice** shape — 10-business-day-prior notice, the medium, and the accommodation-notice pointer.

Where LL 144 is not in scope, a short `nyc-ll-144-not-in-scope.md` recording the determination is sufficient.

### 4. `cfpb-reason-code-methodology.md`

If CFPB adverse-action-notice rows are in scope, the methodology brief for reason-code derivation. It must specify:

- The **reason-code catalogue** — the specific reason codes your programme uses, keyed to model decision drivers (not vendor-list proxies).
- The **derivation method** — SHAP, LIME, counterfactual explanations, or another method; cite it. Note the method's fidelity limitations.
- The **fidelity evaluation** — how you evaluate whether the reason code matches the model's actual decision driver. What is measured; what threshold is acceptable.
- The **notice template** — how the reason code lands in the adverse-action notice consumer receives; the ECOA / Regulation B "specific and accurate" standard is what you are meeting.
- The **cross-reference to the credit-decision explainability policy** — the standing programme document.

Where CFPB is not in scope, a `cfpb-not-in-scope.md` recording the determination is sufficient.

## Starter guidance

- **Anchor cross-references are the *first* move.** Most US-side obligations share deliverables with anchor rows. Colorado deployer risk-management overlaps `eu-ai-act.art9.plan`. EEOC Title VII adverse-impact overlaps `eu-ai-act.art10.bias-report` in methodology (but not in specified categories). Author the cross-reference, then only add a new deliverable if the US-side truly is not covered.
- **Consumer-facing obligations are almost always net-new.** Colorado consumer notice, Colorado consumer appeal, CFPB adverse-action notice, EEOC ADA accommodation procedure — these have no EU AI Act analogue and require their own deliverables.
- **Enforcement asymmetry changes residual posture.** A Colorado waived residual is a regulator-facing exposure (AG-only enforcement); an EEOC waived residual is a private-litigation exposure (Notice of Right to Sue). Legal counsel will read these differently. Encode the enforcement route explicitly.
- **Independent means independent.** LL 144's independent-auditor requirement excludes in-house teams. Do not assign `nyc-ll-144.bias-audit` an `owner_role` of `ai-evaluation-engineer` — the auditor is external; this role coordinates the engagement (foreshadowing `mod-109`).
- **"Specific and accurate" is not decorative.** CFPB reason codes must correspond to the model's actual decision drivers. The reason-code catalogue + a fidelity-evaluation deliverable is the substantive artefact; a template alone is not enough.
- **UGESP is method-specified.** EEOC adverse-impact under UGESP has specific group definitions and specific ratio conventions. If you cross-reference your anchor bias report to `eeoc.title-vii.adverse-impact`, make sure the anchor report actually uses UGESP group definitions — otherwise the cross-reference is over-claiming.
- **Legal counsel signs scope calls.** Every `applies_when` and `not-applicable` determination on a US-side row countersigns to legal. Do not hide it in a comment; put `determined_by: legal-counsel` on the row.
- **Sector-specific US federal rules are not here.** SR 11-7 / SR 23-4 / OCC 2011-12 for banking, FDA GMLP / PCCP for medical devices, SEC-adjacent rules — those are `mod-107`. Do not add them in this exercise.

## Acceptance criteria

You have succeeded if:

- `us-scoping-brief.md` classifies your system against all four instruments (Colorado, NYC, CFPB, EEOC), with reasoning and legal-countersign notes.
- `us-extended-map.yaml` retains every prior row unchanged in its anchor / NIST / ISO fields and adds the US-side rows. Rows shared with anchor deliverables are cross-referenced, not duplicated. Genuinely new rows follow the full row shape.
- Every US-side row's `applies_when` is stamped `determined_by: legal-counsel` with a determination date.
- Rows carry `enforcement_route` from the enum. `residual` posture is annotated with the enforcement route where `waived-with-residual`.
- The map header pins the four US-side instruments.
- Where NYC LL 144 is in scope, `nyc-ll-144-audit-plan.md` names the independent auditor, the audit categories, the data source, the ratio-table shape, the public summary, and the candidate notice. Where out of scope, a determination file records the reasoning.
- Where CFPB is in scope, `cfpb-reason-code-methodology.md` names the reason-code catalogue, the derivation method, the fidelity evaluation, the notice template, and the policy cross-reference. Where out of scope, a determination file records the reasoning.
- Every genuinely new US-side row has a distinct owner and a distinct deliverable filename. No two rows point at the same generic "policy" without a specific artefact.
- The map validates against the schema from chapter `08`. `sibling_us_state_or_federal` fields resolve to existing overlay-row identifiers.
- A reviewer walking the extended map can see, for each obligation, which US-side rows it triggers, which are cross-references to anchor deliverables, and which are genuinely new artefacts the programme owes.

## Stretch goals

- **Draft the Colorado deployer impact assessment shape.** Colorado's deployer-impact-assessment requirement (annual + on substantial modification) is a specific artefact. In `co-deployer-impact-assessment-shape.md`, sketch the sections that would land there and cross-reference the 42005 method from exercise `03`. If a real impact-assessment already exists for another jurisdiction, note where the reuse is defensible and where Colorado-specific content is required.
- **Author the Colorado AG-disclosure procedure.** Colorado SB24-205 obliges deployers to disclose detected algorithmic discrimination to the AG. In `co-ag-disclosure-procedure.md`, produce the procedure — trigger, timeline, escalation, communication template, legal-review chain. Cross-reference the Article 61 serious-incident plan from the anchor map and note where the two procedures compose vs. where they are distinct.
- **Draft the ADA reasonable-accommodation procedure.** EEOC's ADA guidance requires that AI selection tools not screen out disabled candidates who could perform the essential functions with reasonable accommodation. In `eeoc-ada-accommodation-procedure.md`, produce the procedure — notice, request handling, alternative assessment, decision, appeal.
- **Draft the vendor-immunity policy.** EEOC's Title VII guidance is explicit that vendor conduct does not immunise the employer. In `eeoc-vendor-immunity-policy.md`, state the programme's policy position and cross-reference the SR 23-4 third-party risk-management shape (from `mod-107`, forward-looking).
- **Cross-reference the sector rules that will land in `mod-107`.** For each in-scope US-side row, note (in `us-to-mod-107-crossref.md`) which sector rule from `mod-107` (SR 11-7, SR 23-4, OCC 2011-12, FDA GMLP, DORA) would compose with it if the programme adds sector exposure. This is what `mod-107` picks up.
- **Add California CPRA rulemaking.** Where the CPRA automated-decision-making rulemaking has advanced, add a `us-ca-cpra.*` row block to the overlay. `<!-- needs-research: check current status of CPPA automated-decision-making rulemaking at authoring time and populate rows against the current draft / final rule -->`.
- **Draft the multi-tenant / multi-employer LL 144 posture.** Where your product ships to many NYC-based employers, the LL 144 audit obligation applies per employer. In `nyc-ll-144-multi-tenant-posture.md`, sketch how one audit could be re-used across employers (or explain why it cannot).
