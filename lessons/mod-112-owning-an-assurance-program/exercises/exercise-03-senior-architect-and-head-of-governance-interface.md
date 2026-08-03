# exercise-03: Senior Architect and Head of Governance Interface

**Estimated effort:** 2 hours

## Objective

Author the **upward and outward interface specifications** for the assurance programme pinned in exercises `01` and `02`. Three interfaces need drafting: (a) with the `senior-ai-governance-architect` (level 50) at institution scope, (b) with `head-of-ai-governance` (level 60), and (c) with external supervisory bodies (European AI Office, competent Member State authorities, sector supervisors, independent auditors and notified bodies where applicable). The exercise finishes by rehearsing the escalation contract for a *first-time market-surveillance documentation request* under [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) Article 74 — the failure mode most likely to expose an under-drafted interface.

This exercise is design and authoring, not solving. `<!-- needs-research: … -->` markers are legitimate answers where an article number, template, or authority contact would need to be verified against the current EUR-Lex text or the current European Commission / competent-authority guidance.

## Prerequisites

- Chapter [`03-senior-architect-head-of-governance-and-external-supervisor-interfaces.md`](../03-senior-architect-head-of-governance-and-external-supervisor-interfaces.md) — the escalation-contract shape restated at each interface; the senior-architect interface; the head-of-governance interface; the four classes of external supervisor; the compact cadence table.
- Exercise [`exercise-01`](exercise-01-operating-model-and-effective-challenge-convention.md) — the reporting-line contract with the head of AI governance authored there is the basis for artefact 2 below.
- Exercise [`exercise-02`](exercise-02-peer-track-contract-matrix.md) — the escalation paths from the peer contracts terminate at these upward interfaces.
- Familiarity with [`mod-106-cross-jurisdictional-obligation-mapping`](../../mod-106-cross-jurisdictional-obligation-mapping/) (the coverage matrices the programme owes the architect), [`mod-107-sector-regulated-assurance`](../../mod-107-sector-regulated-assurance/) (the sector-supervisor overlay), [`mod-109-third-party-evaluator-and-auditor-interface`](../../mod-109-third-party-evaluator-and-auditor-interface/) (independent auditors and notified bodies), and [`mod-110-post-market-surveillance`](../../mod-110-post-market-surveillance/) (Article 61 / 72 / 73 discharge).
- Skim access to the [European AI Office landing page](https://digital-strategy.ec.europa.eu/en/policies/ai-office), the [EU AI Act consolidated text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) (Articles 55, 61, 72, 73, 74 in particular), and [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) GOVERN sub-categories for the risk-appetite tie.

## Problem statement

Carry the pinned organisation from exercises `01` and `02`. The interfaces must be defensible against that specific organisation's jurisdictional and sector posture — an organisation with no EU exposure does not carry an AI Office row but still carries a lead-jurisdiction-authority row of some shape; an organisation with no sector-regulated products does not carry a sector-supervisor row but should still carry the row's *placeholder* so the interface is easy to activate when a sector-regulated product is added.

Three complications to consider when drafting:

- **First-time contact with an external authority.** The interface must handle the case where the organisation has *never* corresponded with a specific external counterparty. Rehearsal artefact 4 (below) walks this case in detail.
- **A head-of-governance who has less AI-technical depth than the programme lead.** The reporting artefacts must be *legible* to a reader whose expertise is governance and regulatory strategy rather than evaluation methodology. Narrative summaries, not raw dashboards.
- **A senior architect whose control library is under active revision.** At least one input from the architect (a control-library update, a policy-taxonomy revision, a cross-jurisdiction reconciliation) should be in flight during the drafting date; the interface must accommodate the adoption workflow (a pull request against the criterion set with a citation to the architect's release).

## Requirements

Produce five artefacts in a single `interfaces/` directory.

### 1. `interfaces/senior-architect-interface.md`

The interface with `senior-ai-governance-architect` (level 50).

- **Shape.** State that the architect owns the control library, the policy taxonomy, and cross-jurisdiction reconciliation; the programme instantiates. Reference chapter `03`.
- **Inputs the programme owes the architect.** Enumerate at least the four inputs chapter `03` names — per-obligation coverage matrices (drawn from `mod-106`), evidence-package templates, cross-jurisdictional exception log (a subset of the operating-model exception log), control-library gap reports. For each, name the artefact, the cadence, the signer, and the transmission channel.
- **Inputs the programme consumes from the architect.** Enumerate at least the four inputs chapter `03` names — control-library entries, policy-taxonomy updates, cross-jurisdiction reconciliation decisions, institution-scope standards. For each, name the adoption workflow (a pull request against the criterion set citing the architect's release verbatim per `mod-103` chapter `04`).
- **Failure modes.** Enumerate the three failure modes chapter `03` names — programme inventing a control, programme absorbing reconciliation, architect update not adopted — and for each, the observable signal and the fix.
- **Cadence.** State the standing quarterly review's shape (attendees, agenda, output), plus any on-event triggers for interim contact (a control-library update the programme is asked to review pre-release, a first-of-kind cross-jurisdiction reconciliation).

### 2. `interfaces/head-of-governance-interface.md`

The interface with `head-of-ai-governance` (level 60), extending the reporting-line contract from exercise `01` artefact 5.

- **Shape.** State the head-owns / programme-owns split at institution vs release scope. Reference chapter `03`.
- **Cadence table.** Compact table with columns *artefact*, *cadence*, *signer*, *transmission channel*. At minimum, rows for: monthly release-decision summary, quarterly exception-log summary, on-event incident summaries, per-planning-cycle roadmap and resource ask, annual methodology review.
- **Pack templates.** For each of the four packs (monthly, quarterly, on-event, annual), state the sections, the page length target, the data source per section (which register or dashboard), and the reading discipline (the head reads the summaries; the head does not read individual assurance cases; the head drills into cases the programme flagged).
- **Head-of-governance inputs.** Enumerate the four inputs chapter `03` names — institutional risk-appetite statement, board-level constraints, reputational-risk overrides, resource allocation and top-management commitment. For each, name the incorporation workflow into the operating model (which criterion sets cite the risk-appetite by version, which register carries board-level constraints, how reputational-risk overrides land in the decision log).
- **Failure modes.** Enumerate the three failure modes chapter `03` names — head cannot see the exception log until quarter-end, programme escalates for reassurance, risk-appetite statement stale — and for each, the observable signal and the fix.

### 3. `interfaces/external-supervisor-interface.md`

The interface with each class of external supervisor relevant to the pinned organisation. Structured as one section per class:

- **[European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office).** For providers with GPAI models or systemic-risk GPAI models. State the programme's role (author the technical evidence; assemble the notification pack; hand to the head for institutional transmission), the escalation route, the counterparty for classification decisions (institution scope, per `mod-111`), and the specific artefact classes the AI Office consumes. Where the organisation is not currently in scope for AI Office contact, mark the row as *placeholder* with the activation trigger.
- **Competent Member State authorities.** For each EU Member State the organisation deploys into. State the market-surveillance authority's identity (or `<!-- needs-research: pin the current competent authority for market X -->` where the authority is not stable), the Article 61 / 72 / 73 / 74 discharge role, the wall-clock windows (Article 73 serious-incident notification within the statutory window — verify against the current consolidated text and cite the article), and the head-authorised transmission workflow.
- **Sector supervisors.** For each sector-regulated product line the organisation carries — ECB / EBA for banking, EIOPA for insurance, ESMA for capital markets, FDA for medical AI/ML, or the sector-specific authority elsewhere. State the sector-overlay evidence pack (per `mod-107`), the transmission counterparty (the head, or the sector-compliance function if that function sits outside the AI-governance line), and the escalation route.
- **Independent auditors and notified bodies.** For engagements with AISI-shape organisations, Big-Four assurance firms, sector notified bodies for CE-marking (per [ISO/IEC 42006](https://www.iso.org/standard/44546.html)), and city / state third-party auditors (NYC AEDT, Colorado SB 24-205 auditor pathways, etc.). State the audit-pack shape (per `mod-109`), the walkthrough discipline, and the corrective-action-response cadence.

For every row, state the escalation-contract shape: what the programme may decide alone, what it must escalate, what it may not decide alone.

### 4. `interfaces/first-market-surveillance-request-rehearsal.md`

A rehearsal of the escalation contract for a first-time market-surveillance documentation request under EU AI Act Article 74. The scenario:

> A competent Member State authority (name a specific plausible one for the pinned organisation's EU deployments) sends the organisation a written documentation request under Article 74 for one of the T2 or T3 systems in the inventory. The request cites specific Article 11 / Annex IV documentation, the risk-management-system evidence (Article 9), and the technical documentation for the system-under-question. The request specifies a response window (verify the statutory maximum against the current consolidated text — `<!-- needs-research: reconfirm Article 74 response window in the current text -->`).

Walk the response as a numbered timeline, from receipt to transmission:

1. **Receipt.** Who receives the request (the head of AI governance's function, the legal department, the programme lead directly?), how the request is registered in the programme's incident / correspondence log, the escalation notification within the first business hours.
2. **Classification.** Whether the request is routine (a documentation pull the programme has pre-authorised transmission for), above-routine (head-signed transmission), or exceptional (a request that would shift the institution's classification status or its posture — legal-department involvement required, senior-architect notification).
3. **Bundle assembly.** The programme's role: assemble the assurance bundle (per `mod-104` chapter `06`) plus the verification instructions plus the trust-root artefacts (Fulcio, Rekor public roots) plus the Article 11 / Annex IV mapping. State the operating-model handbook section that governs the assembly.
4. **Head-of-governance review.** The head-authorised transmission workflow — the head reviews the bundle, the cover letter, and the transmission channel; the head signs.
5. **Transmission.** The specific channel to the competent authority (secure filing portal, encrypted mail, a designated regulatory-liaison function inside the institution). Wall-clock target relative to the statutory maximum.
6. **Follow-up.** The response-handling workflow — how the authority's follow-up questions are handled, how the programme's bundle is amended if the authority requests specific artefacts, how the deferral log captures any request-derived deferral of a downstream release.
7. **Post-event review.** The programme's own retrospective — what the response revealed about the assurance bundle's fitness for mechanical walkthrough by a first-time external reader, what the interface artefacts revealed about gaps in the escalation contract, what corrective actions land in the roadmap (foreshadow exercise `05`).

The rehearsal is the *acceptance test* for the interfaces: if the timeline reveals a decision the programme could not make and no interface artefact routes it, the interface is under-drafted.

### 5. `interfaces/cadence-table.md`

The consolidated cadence table combining artefacts from artefacts 1–3, with columns *counterparty*, *artefact*, *cadence*, *signer*, *transmission channel*. The table should reconcile against the chapter `03` cadence table but be *specific to the pinned organisation* — an organisation with no GPAI-systemic-risk model does not carry an AI Office row; an organisation with no CE-marked high-risk system does not carry a notified-body row.

Include, for each row:

- Which operating-model register / dashboard is the data source.
- Which register the transmission event lands in (typically the correspondence log or the escalation-decision log stub from exercise `01`).
- The specific handbook section governing preparation and transmission.

## Starter guidance

- **The escalation-contract shape is the through-line.** Every interface — architect, head, external — reads the same three-line contract: what the programme may decide, what it must escalate, what it may not decide alone. If an interface has no *may not decide alone* row, it is under-scoped.
- **Institution-scope vs release-scope.** The head owns *what the institution is willing to ship*; the programme owns *whether each specific ship meets the risk-appetite*. The interfaces must make the boundary visible so no one on either side has to guess.
- **The head does not read individual assurance cases.** The reporting artefacts are summaries with drill-down pointers into the assurance-bundle store, not narrative accounts of individual cases. A head who has to read 40 cases per month cannot govern.
- **External transmission is head-authorised above routine.** Every external counterparty row states the routine-versus-above-routine split; every above-routine transmission is head-signed. The programme's authority is *team scope*; the interfaces make that scope visible.
- **First-time contact is a *category* of external event, not a per-authority workflow.** The rehearsal artefact (artefact 4) walks a specific Article 74 case, but the timeline shape applies to any first-time contact with any external counterparty — an AI Office initial request, a first-time notified-body onboarding, a first-of-kind sector-supervisor query.
- **The programme is the technical author, not the institutional spokesperson.** Every artefact in the external-supervisor interface makes this line explicit. Rows where the programme signs an external transmission alone are governance defects.
- **`<!-- needs-research: … -->` is a legitimate answer** for EU AI Act article numbers (verify against the current consolidated text), for the current published Member State competent-authority list, for the current AI Office notification templates, and for organisation-specific channel details (secure portals, regulatory-liaison functions).

## Acceptance criteria

You have succeeded if:

- `interfaces/senior-architect-interface.md` covers inputs owed to the architect (at least four), inputs consumed from the architect (at least four) with adoption workflow, three failure modes with signal and fix, and cadence (quarterly review plus on-event triggers).
- `interfaces/head-of-governance-interface.md` extends exercise `01` artefact 5 with pack templates per cadence (sections, page length, data source, reading discipline), the four head-of-governance inputs and their incorporation workflow, and three failure modes with signal and fix.
- `interfaces/external-supervisor-interface.md` carries one section per class of external supervisor relevant to the pinned organisation (European AI Office, competent Member State authorities per deployment, sector supervisors per sector-regulated product, independent auditors / notified bodies). Every row states the escalation-contract shape.
- `interfaces/first-market-surveillance-request-rehearsal.md` walks the timeline in numbered steps from receipt to post-event review; each step names an owner, a wall-clock target, and the handbook / register that governs it. The rehearsal exposes at least one gap in the interface (an under-drafted decision, a missing pre-authorised transmission channel, an ambiguous signer) — the exercise's job is to *surface* the gap, not gloss over it.
- `interfaces/cadence-table.md` reconciles against chapter `03`'s cadence table but is specific to the pinned organisation's jurisdictional and sector posture. Rows for external supervisors that do not apply are marked *placeholder* with the activation trigger.
- Every EU AI Act article number is either verified against the current consolidated text or marked `<!-- needs-research: … -->`.
- Every external counterparty's row makes the routine-versus-above-routine split explicit; every above-routine transmission is head-signed.
- Every interface's *may not decide alone* class is enumerated (Article 55 GPAI classification, prohibited-practice edge cases, cross-institution reputational-risk cases, first-time supervisor communications, sector-supervisor above-routine).

## Stretch goals

- **Author the correspondence-log schema.** In `correspondence-log-schema.md`, formalise the append-only log the programme keeps of every external correspondence — inbound and outbound — with columns for counterparty, artefact reference, transmission channel, signer, and any regulatory-deadline exposure.
- **Draft the head-of-governance briefing-note template.** In `head-briefing-note-template.md`, produce the template for the on-event briefing note the programme prepares when an incident, deferral, or escalation requires ad-hoc head attention outside the standing cadence. Include the section headings, the target reading time, and the sign-off block.
- **Draft the senior-architect standing-review agenda.** In `architect-standing-review-agenda.md`, produce the recurring agenda for the quarterly senior-architect review — coverage-matrix reading, control-library gap reading, adoption-decision block, cross-jurisdiction reconciliation block.
- **Rehearse an Article 73 serious-incident notification.** In `article-73-rehearsal.md`, walk a plausible serious-incident scenario for a system in the pinned inventory — the wall-clock notification window (verify against the current consolidated text and cite the article), the bundle-assembly workflow, the head-of-governance sign-off, the AI Office / competent-authority transmission (as applicable), the post-event review, and the roadmap follow-up.
- **Draft the notified-body engagement pack.** In `notified-body-engagement-pack.md`, for an organisation whose CE-marking pathway requires a notified body, produce the initial engagement pack — the audit scope, the Annex IV / Article 11 documentation index, the risk-management-system evidence index (Article 9), the data-governance evidence index (Article 10), the record-keeping index (Article 12), the transparency evidence (Article 13), the human-oversight design (Article 14), and the accuracy-robustness-cybersecurity evidence (Article 15). Verify article numbers against the current consolidated text.
