# Interfaces Upward: Senior Architect, Head of AI Governance, and External Supervisors

## Motivation

Chapter `02` drew the six interfaces *downward* — into the peer tracks whose evidence the programme consumes. This chapter draws the three interfaces *upward and outward* — into the roles that consume the programme's output at institution scope and beyond it.

The distinction matters because the failure modes are opposite. Downward, the programme risks *absorbing* peer craft it should defer. Upward, the programme risks either *usurping* institution-scope decisions it should escalate (over-reach) or *withholding* signal the institution needs to make those decisions (under-report). Outward — into external supervisory bodies and independent auditors — the programme risks *speaking on behalf of* the institution in ways it lacks authority to.

The escalation-contract shape governing all three interfaces is the same three-line question the assurance owner must be able to answer for every case:

- **What may the programme decide?** — routine dispositions inside the risk-appetite envelope.
- **What must the programme escalate?** — cases whose disposition falls outside the envelope or whose signal is institution-scale.
- **What may the programme not decide alone?** — categorically institution-scope decisions (Article 55 GPAI classification, prohibited-practice edge cases, cross-institution reputational-risk cases, first-time supervisor communications).

Chapter `01` named these categories in passing. This chapter draws them at interface level with each counterparty.

## Interface with `senior-ai-governance-architect` (level 50)

The senior architect's remit is *cross-organisation* — the control library, the policy taxonomy, cross-jurisdiction reconciliation. The programme sits inside that architecture; it does not author it.

**Shape.** The architect draws the taxonomy of controls; the programme instantiates them. The architect reconciles overlapping obligations across jurisdictions; the programme discharges the reconciled set at the release-gate. The architect defines the policy taxonomy (accepted use, prohibited use, escalation-required); the programme enforces it.

### Inputs the programme owes the architect

- **Per-obligation coverage matrices.** For each in-scope framework (NIST AI RMF, ISO/IEC 42001, EU AI Act, sector rules), the current state of coverage across the systems the programme oversees — what obligations are covered by which criterion-set rows, what obligations are uncovered, what obligations are covered informally and need to be codified (drawn from `mod-106`).
- **Evidence-package templates.** The current assurance-bundle manifest template (`mod-104/06`), the card templates for external audiences (`mod-105`), the reproducibility-bundle template (`mod-104/03`) — so the architect can harmonise them across the institution's programmes.
- **Cross-jurisdictional exception log.** The subset of the exception log (chapter `01`) that has cross-jurisdictional implications — an exception granted in one market that would not survive in another, or an exception whose corrective action depends on a policy the institution has not yet published.
- **Control-library gap reports.** During operation, the programme discovers controls that are referenced in the release-gate but are not defined in the control library, or defined but unenforceable at release-gate scope. These flow to the architect as deprecation and addition requests.

### Inputs the programme consumes from the architect

- **Control-library entries** (Annex A-shape) that the release-gate criterion set references. The programme does not invent controls; it references the institution's library.
- **Policy-taxonomy updates** — accepted-use, prohibited-use, escalation-required. The programme's intake-stage scope assessment reads the taxonomy at each cycle.
- **Cross-jurisdiction reconciliation decisions** — where two markets impose overlapping obligations, the architect's reconciliation trims the release-gate's obligation list of duplicates and pins which authoritative rule governs.
- **Institution-scope standards** — the responsible-AI standard, the internal control catalogue, the model-risk-management standard (SR 11-7-shape where applicable). The programme discharges into these; it does not author them.

**Failure modes.** The programme invents a control the architect has not defined (institution-scope drift); the programme absorbs cross-jurisdiction reconciliation into case-level dispositions (loss of architecture); the architect publishes a control-library update that the programme does not adopt in the criterion set (release-gate misalignment).

**What good looks like.** A standing quarterly review between the programme lead and the architect covers coverage matrices, gap reports, and adoption of published updates. Adoption is a Git pull request against the criterion set with a citation to the architect's release; the programme cites the architect's clause number verbatim rather than paraphrasing (per `mod-103/04` cross-peer rule).

## Interface with `head-of-ai-governance` (level 60)

The head's remit is institution-scale: board reporting, regulator interface at institution scope, strategy, resourcing, risk-appetite. The programme reports upward on a fixed cadence with a fixed pack shape.

**Shape.** The head owns *what the institution is willing to ship*; the programme owns *whether each specific ship meets the risk-appetite statement*. When the risk-appetite is ambiguous for a case, the escalation is upward; when a case exceeds the risk-appetite, the escalation is also upward; when the head issues a board-level constraint or a reputational-risk override, it flows downward as a first-class input to the criterion set.

### Inputs the programme owes the head

- **Monthly release-decision summary.** Throughput (gates run, decisions made), disposition mix (pass / delayed / refused / promoted-at-lower-tier), exception counts, deferral counts, rollback events. One page; drawn from the decision log (chapter `01`).
- **Quarterly exception-log summary.** The full exception log for the quarter, grouped by criterion, with corrective-action closure rates and any exceptions nearing expiry without a revisit trigger. Feeds ISO/IEC 42001 clause 9.3 management review.
- **Incident summaries.** Every serious incident (EU AI Act Article 73), every material near-miss (per `mod-110`), every release-gate refusal, with a root-cause note and the corrective action taken. Cadence: on-event within the notification wall-clock; aggregated at the quarterly review.
- **Roadmap and resource asks.** The programme's own investment case for the next planning cycle (drawn from chapter `05`), plus any capacity-blocked escalations from the peer contracts (chapter `02`).
- **Annual methodology review.** A signed record of what changed in the criterion set, the peer contracts, the runbook, and the dashboard, with rationale.

### Inputs the programme consumes from the head

- **Institutional risk-appetite statement.** The head-signed statement of what deployments the institution is willing to ship at what tiers under what conditions. Referenced by every criterion set (per [NIST AI RMF GOVERN-1.3](https://www.nist.gov/itl/ai-risk-management-framework)).
- **Board-level constraints.** Any board-imposed constraint on deployment (a moratorium on a use-class, a maximum tier without board notification, a specific harm class the board has designated as non-tolerable). The programme's scope-assessment stage reads these first.
- **Reputational-risk overrides.** A head-issued veto on a specific release the programme would otherwise pass, or an approval to proceed on a specific release the programme would otherwise refuse. Rare, documented as an override with rationale in the decision log.
- **Resource allocation and top-management commitment** (ISO/IEC 42001 clauses 5.1 and 7.1). The programme's authorisation to run is the head's commitment.

**Failure modes.** The head cannot see the exception log until quarter-end (surprise incidents at board time); the programme escalates every case for reassurance (institutional over-load, loss of authority); the risk-appetite statement is stale and does not match current criterion sets (drift between what the institution says it will ship and what the release-gate approves).

**What good looks like.** Legible reports on a fixed cadence; a documented escalation-decision log for the cases upward; the risk-appetite statement is versioned and every criterion set cites it by version. The head does not read individual assurance cases; the head reads the summaries and drills into cases the programme flagged.

## Interface with external supervisory bodies

External supervisors sit outside the institution. The programme's interface with them is *tightly bounded*: the programme is the technical author of the evidence but not the institution's authorised spokesperson. Every external communication above the routine reporting cadence goes through the head of AI governance (or a delegate the head has named).

Four classes of external supervisor interact with the programme's evidence.

### The [European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office)

For providers of GPAI models (with or without systemic risk), the AI Office is the direct supervisory counterparty. Under EU AI Act Articles 55 and 56, GPAI-systemic-risk providers owe the Office notifications, model evaluations, and adversarial-testing records; the [GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) sets the shape (verify current URL). <!-- needs-research: confirm current GPAI Code of Practice publication URL and version -->

**Programme role.** Author the technical evidence set; assemble the notification pack; hand to the head for institutional transmission. The programme does not correspond directly with the Office on classification decisions or systemic-risk designations — those are institution-scope (`mod-111`).

### Competent Member State authorities

For each EU Member State the institution deploys into, the competent national authority handles market surveillance, Article 61 (post-market monitoring), Article 72 (post-market monitoring plan discharge), and Article 73 (serious-incident reporting).

**Programme role.** Author the post-market-monitoring plan (`mod-110`); assemble Article 72 records; assemble Article 73 incident notifications on-event within the wall-clock; hand to the head for transmission. Where the market-surveillance authority sends a documentation request under Article 74, the programme produces the assurance bundle (`mod-104/06`) plus the verification instructions plus the trust-root artefacts; transmission is head-authorised.

### Sector supervisors

Where the institution operates in a regulated sector, the sector supervisor's rules layer on top of horizontal AI regulation. Examples: ECB and EBA for banking (SR 11-7 / OCC 2011-12 / SR 23-4 model-risk lineage in the US context; EBA guidelines and DORA in the EU context); EIOPA for insurance; ESMA for capital markets; the FDA for medical AI/ML (GMLP, PCCP); sector-specific national authorities elsewhere.

**Programme role.** Discharge the sector-overlay evidence set (per `mod-107`) into the sector supervisor's expected format; hand to the head or the sector-compliance function (which may sit outside the AI-governance line) for transmission. The programme is authoritative on *whether the AI-specific evidence is defensible*; it is not authoritative on the sector rules themselves.

### Independent auditors

Independent evaluators (AISI-shape organisations, Big-Four assurance firms, sector notified bodies for CE-marking, city or state third-party auditors such as those required by NYC AEDT for automated employment decision tools) receive the programme's evidence and produce their own report.

**Programme role.** Assemble the audit pack (per `mod-109`); host the walkthrough sessions; respond to findings with corrective actions; register the auditor's report as an amendment to the assurance bundle. The programme does not negotiate the audit scope — that is contracted at institution scope by the head or a delegate.

### Notified bodies and CE-marking

Where the institution places a high-risk AI system on the EU market under Article 6 and Annex III, and where the applicable conformity-assessment route requires a notified body, the notified body becomes a formal counterparty for the CE-marking process. The programme's role is to author the technical documentation (Article 11 / Annex IV), the risk-management-system evidence (Article 9), the data-and-data-governance evidence (Article 10), the record-keeping (Article 12), the transparency-for-deployers evidence (Article 13), the human-oversight design (Article 14), and the accuracy-robustness-cybersecurity evidence (Article 15), and to assemble the assurance bundle (`mod-104/06`) as the primary document.

The notified body is not the same as an independent evaluator — it is designated under [ISO/IEC 42006](https://www.iso.org/standard/44546.html) or the sector-specific accreditation regime, and its findings drive the declaration of conformity under Article 47. First contact with a notified body is head-signed; ongoing conformity-assessment work is programme-executed with the notified body per the accreditation regime.

### The escalation-contract shape, restated

For every external counterparty:

- **May the programme decide alone?** No external communication is *decided* by the programme alone. Routine transmission on a pre-authorised cadence and shape is programme-signed; anything above routine is head-signed.
- **What must the programme escalate?** First-time contact with any external counterparty; any Article 73 serious-incident notification; any market-surveillance response under Article 74; any request that could shift the institution's classification status or its posture with the counterparty.
- **What may the programme not decide alone?** Institution-scope classification decisions (Article 55 systemic-risk; Article 6 high-risk classification where the boundary is contested); the interpretation of a supervisor's request; any settlement discussion; any waiver or extension of a regulatory deadline.

## Interface artefacts and their cadences

Each interface produces a small, fixed set of artefacts with a fixed cadence. The list below is what a programme running steady-state ships:

| Counterparty | Artefact | Cadence | Signer |
| ------------ | -------- | ------- | ------ |
| Senior architect | Coverage-matrix report | Quarterly | Programme lead |
| Senior architect | Control-library gap report | On-event + quarterly digest | Programme lead |
| Senior architect | Cross-jurisdiction exception subset | Quarterly | Programme lead |
| Head of AI governance | Monthly release-decision summary | Monthly | Programme lead |
| Head of AI governance | Quarterly exception-log summary | Quarterly | Programme lead |
| Head of AI governance | Incident summary | On-event within notification window | Programme lead |
| Head of AI governance | Roadmap and resource ask | Per planning cycle | Programme lead |
| Head of AI governance | Annual methodology review | Annual | Programme lead + assurance-team signatures |
| European AI Office (GPAI) | Notification packs, model-evaluation records | On-event and per Article 55 cadence | Head or delegate |
| Member State authority | PMM plan discharge | Per Article 72 cadence | Head or delegate |
| Member State authority | Article 73 serious-incident notification | On-event within statutory wall-clock | Head or delegate |
| Sector supervisor | Sector-overlay evidence pack | Per sector-supervisor cadence | Head or sector-compliance function |
| Independent auditor / notified body | Audit pack (assurance bundle + verification instructions + trust-root artefacts) | On engagement | Programme lead assembles; head-authorised transmission |

Every artefact above is Git-tracked, versioned, and cross-referenced by the AIMS controlled-document register (per `mod-104/06`). None of them is a PDF exported from a tool without a corresponding structured artefact behind it.

## Worked example — the six-person team from chapters `01`–`02`

Continuing the same organisation: six-person assurance team, forty AI systems in the inventory, one T3 system, one senior architect (a two-person team including a policy lead), one head of AI governance, three EU Member State deployments, and one US sector-regulated product line (a banking product under SR 11-7 lineage).

**Architect interface.** Monthly working session between the programme lead and the architect. Deliverables inbound this quarter: an updated control-library entry for chain-of-thought traceability at T3, adopted into the criterion set as `GATE-TRANS-04-v2`. Deliverables outbound this quarter: a coverage-matrix report showing that Article 15(4) cybersecurity has three uncovered rows the architect is asked to codify controls for.

**Head-of-governance interface.** Monthly release-decision summary (one page, twelve gate cycles). Quarterly exception-log summary (ten open exceptions, all with revisit triggers). One incident this quarter: a T2 chatbot mishandled a mental-health disclosure (see chapter `05`'s worked example); notification to the head within four hours, root-cause note within 48 hours, corrective action defined within the quarter, corrective-action closure by next quarter. Roadmap ask for the next planning cycle: 0.5 FTE for the online-eval slice buildout on the T3 system.

**External-supervisor interfaces this quarter.**

- One Article 72 post-market-monitoring plan submission for the T2 chatbot to the competent Member State authority (routine cadence, programme-signed, head-informed).
- One market-surveillance documentation request under Article 74 for the T3 system (first-of-kind; head-signed transmission; programme assembled the bundle plus verification instructions plus Fulcio and Rekor public roots; response window met).
- One SR 11-7-shape independent validation of the banking model performed by an external validator contracted by the sector-compliance function; the programme produced the audit pack; the validator's report registered as a bundle amendment (`mod-109`).
- No AI Office contact this quarter; the institution does not currently ship a GPAI-systemic-risk model.

## Where this shows up in the rest of the track

- `mod-101/06` — the deferral contract enumerates the higher-tracks (architect, head, CAIO); this chapter draws the interfaces in detail.
- `mod-106` — the cross-jurisdictional obligation mapping is the substrate for the coverage matrices the programme owes the architect.
- `mod-107` — the sector-overlay evidence set drives the sector-supervisor interfaces.
- `mod-109` — the third-party-evaluator and auditor interface is the tactical shape of the independent-auditor row in this chapter.
- `mod-110` — the post-market-monitoring plan discharges into Article 61, 72, and 73; the notification cadence is what the programme executes on-event.
- `mod-111` — the GPAI systemic-risk assurance is where the AI Office interface takes its most intensive form.
- Chapter `01` — the escalation-contract shape (may decide, must escalate, may not decide alone) is drawn here; the operating model executes it.
- Chapter `05` — incidents drive both the escalation events and the roadmap prioritisation the programme brings to the head.

## Summary

- Upward and outward interfaces mirror the downward peer interfaces of chapter `02`; the failure modes are opposite (over-reach and under-report versus over-absorb).
- The senior architect owns cross-organisation control-library architecture; the programme instantiates it, reports coverage and gaps, and adopts control-library and policy-taxonomy updates by pull request.
- The head of AI governance owns institution-scope decisions and risk-appetite; the programme reports on fixed cadences (monthly decision summary, quarterly exception summary, on-event incidents, annual methodology review) and escalates cases outside the appetite.
- External supervisors — the European AI Office, competent Member State authorities, sector supervisors, independent auditors — receive programme-authored evidence but head-authorised transmission for any above-routine communication.
- The escalation-contract shape governs all three interfaces: what the programme may decide, what it must escalate, what it may not decide alone (Article 55 GPAI classification, prohibited-practice edge cases, cross-institution reputational-risk cases, first-time supervisor communications, sector-supervisor above-routine).
- Cite [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) GOVERN sub-categories for the risk-appetite tie, [ISO/IEC 42001 clauses 5 and 9](https://www.iso.org/standard/81230.html) for the leadership and management-review tie, and the EU AI Act articles 55 / 61 / 72 / 73 / 74 / GPAI Code for the supervisor ties.
- Exercise-03 asks you to draft the interface specifications with your architect and head and rehearse the escalation contract for a first-time market-surveillance request.
