# exercise-04: Supervisory-Overlay Applicability Memos and Watch-List Currency Statement

**Estimated effort:** 3 hours

## Objective

For one AI system deployed by a European financial-sector entity, produce the **supervisory-overlay row of the release-package** — an applicability memo per relevant EU sectoral supervisor (ECB Banking Supervision, EIOPA, ESMA), a national-competent-authority overlay memo for the entity's home jurisdiction, an interfaces-with-AI-specific-overlays note (European AI Office, EDPB, national DPAs), and a **watch-list-currency statement** signed by the assurance function. The overlay row is what a supervisor first opens at inspection to see whether the entity is even *aware* of the current state of expectations; the row is not the release-gate criterion set, but a stale or missing overlay row is itself an inspection finding.

The exercise is authoring, not solving. Supervisory-overlay content shifts often; the exercise emphasises the discipline of citing primary sources, distinguishing what is binding from what is interpretive, and marking `<!-- needs-research: … -->` for facts that would need to be verified against the current state of each supervisor's landing page at time of submission.

## Prerequisites

- Chapter [`05-ecb-eiopa-esma-and-adjacent-supervisory-overlays.md`](../05-ecb-eiopa-esma-and-adjacent-supervisory-overlays.md) — the sectoral supervisors' current shape, the watch-list process (monthly / quarterly / annual / ad-hoc), the interface with AI-specific overlays.
- Chapter [`04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md`](../04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md) — DORA sits alongside the supervisory overlays and the release-package cross-references between them.
- Landing pages for the relevant supervisors — [ECB Banking Supervision](https://www.bankingsupervision.europa.eu/), [EIOPA AI](https://www.eiopa.europa.eu/browse/regulation-and-policy/artificial-intelligence_en), [ESMA AI](https://www.esma.europa.eu/esmas-activities/investors-and-issuers/artificial-intelligence), and — where the entity is UK-based or has UK exposure — the [FCA AI page](https://www.fca.org.uk/firms/artificial-intelligence-ai) and the [PRA's SS1/23 model-risk-management supervisory statement](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss123).
- Familiarity with the peer-role registry — the release-assurance owner works alongside compliance, legal, regulatory affairs, and — for the watch-list — the second-line function that maintains the entity's supervisory-relations posture.

## Problem statement

Invent the financial entity, the AI system, and the entity's supervisory footprint. The scenario must involve at least one EU sectoral supervisor (ECB, EIOPA, or ESMA); a national competent authority is always in scope; the AI-specific overlays interface where applicable. If exercise `03`'s scenario is a natural fit, reuse it and add the supervisory-overlay layer; otherwise invent afresh.

Common patterns worth considering (pick one, or invent your own):

- **A significant credit institution supervised in the ECB SSM** deploying a credit-decisioning-support AI. ECB Banking Supervision + national competent authority (BaFin, ACPR, or another Member-State supervisor).
- **A mid-sized EU insurer** deploying an underwriting AI in a regulated line. EIOPA overlay + national competent authority (BaFin's insurance function, ACPR, or another Member-State supervisor).
- **An EU investment firm** deploying a client-suitability robo-advisor. ESMA overlay + national competent authority (AMF, BaFin, or another).
- **A UK-authorised bank with EU branches** deploying an AI in a supervised function. PRA + FCA on the UK side + ECB / national supervisor(s) on the EU side, all interacting.
- **A cross-border insurer** deploying a fraud-detection AI across multiple EU jurisdictions. EIOPA + several national supervisors, with divergent local expectations.

Pin the scenario before authoring:

- The entity's regulatory status and its regulatory footprint (which supervisors interact with it).
- The AI system's intended purpose and the supervised function(s) it participates in.
- The likely sectoral supervisor(s) whose overlay attaches (ECB, EIOPA, ESMA — or a subset).
- The national competent authority (or authorities) for the entity's operations.
- Any AI-specific overlays that interface (European AI Office for GPAI-Code-of-Practice reference; EDPB for GDPR-side AI opinions; national DPAs for GDPR Article 22 automated-decision-making).

## Requirements

Produce six artefacts in a single directory.

### 1. `scenario-scoping-brief.md`

A one-page brief that fixes:

- **Entity and regulatory footprint.** Named entity, regulatory status, primary sectoral supervisor, primary national competent authority, and any secondary supervisors (cross-border, cross-sectoral).
- **AI system and supervised function.** The system's intended purpose and the specific supervised function it participates in. The link between the AI system's outputs and the supervised function is stated concretely.
- **Overlay scope.** Which sectoral supervisor overlays apply and which do not, with reasoning. An overlay is *out of scope* if the entity is not supervised by that authority; a plain not-applicable determination on the overlay memo is a valid answer as long as the reasoning is on the record.
- **AI-specific overlay interfaces.** Whether the European AI Office (GPAI provider status, GPAI Code of Practice reference), the EDPB (any AI-related opinions that reach the entity's use case), and the national DPA (GDPR Article 22 automated-decision-making) attach. Not-applicable determinations here are also valid.
- **Anchor-instrument cross-references.** For each anchor instrument in scope from earlier chapters — DORA (chapter `04`), SR 11-7 (chapter `01`) if the entity has US operations, EU AI Act (from `mod-106`) — the release-package rows the overlay memos cross-reference.

### 2. `ecb-banking-supervision-overlay-memo.md`

If the entity is supervised by the ECB SSM, or if the entity's supervisor coordinates through the SSM, produce a short applicability memo covering:

- **Applicability.** Whether ECB Banking Supervision expectations attach to the entity, and — inside the entity — to the AI system.
- **Framework citations.** The ECB Guide to internal models and any current ECB thematic communications on AI in banking (marked `<!-- needs-research: … -->` where you need to verify the current publication list at time of drafting).
- **Model-risk-management interface.** Where the AI system participates in an SR-11-7-shaped process — because European significant institutions typically have a model-risk-management framework built to SR 11-7's shape as adapted for the EU — the memo names the interface with the entity's own MRM policy.
- **Internal-models interaction.** If the AI system participates in an internal-models activity (credit, market, counterparty-credit risk) that is subject to ECB model approval, the memo names the interaction and the additional release-gate evidence.
- **Watch-list currency.** The last date the ECB Banking Supervision landing page and thematic-communications inventory were scanned; the reviewer who signed the scan.
- **Release-gate reflection.** How the memo's content maps into release-gate criteria — typically as cross-references to the bank's MRM policy rather than as direct ECB citations.

If the entity is not ECB-supervised, produce a short `ecb-not-in-scope.md` recording the determination with reasoning. Silence is not an option.

### 3. `eiopa-overlay-memo.md`

If the entity is an insurance or occupational-pensions entity subject to EIOPA-coordinated supervision, produce a memo covering:

- **Applicability.** Whether EIOPA opinions and consultation-paper expectations attach to the AI system's use case.
- **Framework citations.** The 2021 EIOPA six-principles report on AI governance in insurance, any current EIOPA opinion or consultation paper on AI in the specific insurance function (underwriting, pricing, claims, fraud detection), and any current thematic work (`<!-- needs-research: … -->` for current URL / title verification).
- **Proportionality determination.** The scaling of rigour to policyholder impact for the AI use case.
- **Fairness-in-pricing analysis.** If the AI touches pricing or underwriting, the memo names the fairness-in-pricing analysis (subgroup sensitivity, indirect-discrimination analysis, explainability of pricing outcomes) that the release-package carries.
- **Consumer-facing transparency artefact.** For any AI use case touching the policyholder, the transparency artefact the entity provides.
- **Watch-list currency.** As for the ECB memo.
- **Release-gate reflection.** Where the memo's content maps into release-gate criteria — often overlapping with DORA (chapter `04`) on operational-resilience matters and with EU AI Act on transparency and human oversight.

If the entity is not EIOPA-relevant, produce a short `eiopa-not-in-scope.md` recording the determination.

### 4. `esma-overlay-memo.md`

If the entity is an investment firm, trading venue, CCP, or otherwise subject to ESMA-coordinated supervision, produce a memo covering:

- **Applicability.** Whether ESMA statements on AI in investment services attach to the AI system's use case.
- **Framework citations.** The current ESMA public statements on AI (`<!-- needs-research: … -->` for the current inventory), any relevant supervisory-convergence Q&As, and — for algorithmic-trading AI systems — MiFID II RTS 6 and the associated ESMA guidelines.
- **Existing-obligation applicability memo.** The core artefact this memo produces — which existing MiFID II / MiFIR obligations apply to the AI-enabled activity, and how the AI's design supports them (best execution, suitability, product governance, best interests of the client).
- **Algorithmic-trading additions.** For algo-trading AI systems, the RTS-6-shaped controls (self-assessment, testing, monitoring, stress testing, kill functionality) with AI-specific elements.
- **DORA cross-reference.** Where ESMA acts as Lead Overseer under DORA Article 32 for a designated critical ICT third-party service provider on which the entity depends, the interaction is noted.
- **Watch-list currency.** As above.
- **Release-gate reflection.** Where the memo's content maps into release-gate criteria — typically compliance-function sign-off on the existing-obligation applicability memo as a hard-gate criterion.

If the entity is not ESMA-relevant, produce a short `esma-not-in-scope.md` recording the determination.

### 5. `national-competent-authority-overlay-memo.md`

Regardless of ECB / EIOPA / ESMA applicability, the national competent authority is *always* in scope. Produce a memo covering:

- **Authority identification.** Which national competent authority (or authorities) supervise the entity for the relevant function. Where cross-border operations trigger multiple authorities, name each and its scope of supervision.
- **NCA-published expectations.** Any NCA supervisory expectations on AI in the sector — dear-CEO letters, Q&As, thematic-review publications, sandbox activities. This section is where the NCA-specific content lands (BaFin has one set of expectations; AMF has another; the FCA is often cited as a reference even outside its formal remit).
- **Local overlays over EU-level frameworks.** Where the NCA's expectations layer on top of an EU-level framework (a national interpretation of EU AI Act obligations, a national transposition of Solvency II conduct obligations, a specific supervisory expectation the ECB does not carry), name the layering.
- **Cross-border divergence.** Where the entity operates in multiple jurisdictions, the memo notes the most-demanding-of-applicable stance the release-package takes for each release surface.
- **Inspection posture.** How the entity engages with the NCA on AI-related supervisory activity — designated contacts, communication channels, notification obligations for material AI incidents (which typically fold into DORA reporting).
- **Watch-list currency.** As above.
- **Release-gate reflection.** Where the memo's content maps into release-gate criteria — typically NCA-facing communication artefacts and NCA-cited framework references.

Multiple NCA memos are acceptable for a cross-border entity; one per jurisdiction is preferred for clarity.

### 6. `watch-list-currency-statement.md`

The watch-list-currency statement is the assurance function's own attestation that the supervisory-overlay row is current. It carries:

- **Scan cadences.** Named cadences (monthly for landing-page scans; quarterly for triaged publications deep-read; annual for release-package template refresh; ad-hoc for inspection communications).
- **Last-scan dates per authority.** For each authority tracked (ECB, EIOPA, ESMA, national competent authorities, European AI Office, EDPB, national DPAs), the last date the authority's landing page was scanned and the last date any triaged publication was deep-read.
- **Reviewer name(s).** Who signed each scan.
- **Material changes since last release-package refresh.** Any changes in supervisor expectations since the release-package template was last refreshed — new publications, changed positions, initiated consultations.
- **Actions taken.** Where a material change triggered a template refresh or an affected-system re-release, the actions and their status.
- **Currency assessment.** The signer's own read of whether the release-package template is current with the supervisory-overlay state at the sign-off date. Where currency is deficient, the remediation plan and expected completion date.
- **Signer.** The assurance function's designated overlay-owner. Not the model developer. Not the first-line business owner.

The statement is dated. It is signed. It is the artefact the release-gate reads first when the release-package touches supervisory-facing evidence.

## Starter guidance

- **Fix the scoping first.** Which supervisors attach is a question of the entity's regulatory footprint, not of the AI system's technical shape. Get the footprint right before authoring memos.
- **Not-in-scope memos are legitimate answers.** A short memo that records a considered determination — with reasoning — is exactly what the release-package needs for a supervisor whose overlay does not attach. Silence is not equivalent to a not-in-scope determination.
- **Cite primary sources.** Every memo cites the supervisor's own landing page or numbered document. Do not paraphrase a speech into a hard release-gate criterion; do not quote an opinion as if it were a directive. Cite the source and describe how the release-package acknowledges it.
- **Distinguish binding from interpretive.** The ECB Guide is *interpretive*; the CRD/CRR are *binding*. A EIOPA opinion is *interpretive*; Solvency II is *binding*. An ESMA statement is *interpretive*; MiFID II is *binding*. Where an interpretive text hardens into supervisory expectation, note that; where it is interpretation of a binding text, cite the binding text alongside.
- **The overlay row is not a release-gate criterion set.** It is context and cross-reference. A supervisor asks "are you aware?" first; the overlay row answers that question. Hard release-gate criteria live in the anchor-instrument artefacts (SR 11-7, DORA, GMLP/PCCP) and in the CRO's / compliance function's determinations that add or waive.
- **Watch-list currency is a signer question.** The watch-list-currency statement is not a summary of what has been scanned; it is a signer's attestation that the release-package is current. Sign it (or mark as a simulation artefact if the exercise scenario names no real signer).
- **Cross-border entities have multiple NCA rows.** Do not compress them. Where NCAs' expectations diverge, name the divergence and the most-demanding-of-applicable stance the release-package takes for each release surface.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** The state of supervisory expectations shifts; the exercise emphasises the discipline of marking-for-verification rather than guessing.

## Acceptance criteria

You have succeeded if:

- `scenario-scoping-brief.md` fixes the entity's regulatory footprint, the AI system's supervised function, the overlay scope, and the AI-specific overlay interfaces with reasoning.
- Every applicable sectoral supervisor has an overlay memo (`ecb-*`, `eiopa-*`, `esma-*`); every not-applicable supervisor has a not-in-scope memo with reasoning. Silence on any of ECB / EIOPA / ESMA is not acceptable.
- `national-competent-authority-overlay-memo.md` covers at least one NCA (the entity's home NCA); multiple NCAs for cross-border entities.
- Each memo cites primary sources for the framework references and marks `<!-- needs-research: … -->` where a specific URL, title, or publication date would need to be verified.
- Each memo names how its content reflects into release-gate criteria — typically as cross-references to bank / entity policy artefacts or to compliance-function sign-offs.
- `watch-list-currency-statement.md` names scan cadences, last-scan dates per authority, reviewer names, material changes since last refresh, actions taken, currency assessment, and signer. The statement is dated.
- The interface memo (or a note inside one of the supervisor memos) addresses the AI-specific overlays — European AI Office, EDPB, national DPAs — where they interact with the sectoral overlays.
- Every place a fact would need to be verified against the current state of a supervisor's landing page is marked `<!-- needs-research: … -->` rather than guessed.
- The memo set is *consistent* — the overlay scope on the scoping brief matches which supervisor memos are present and which are not-in-scope; the currency-statement's authority list covers every memo produced.
- A reviewer walking the memo set can see, for the entity, which supervisors' expectations reflect into the release-package, where the primary sources sit, when the watch-list was last refreshed, and who owns the refresh.

## Stretch goals

- **Author the inspection-response playbook.** In `inspection-response-playbook.md`, sketch how the assurance function responds to an inspection communication touching the AI system — the intake procedure, the material-request routing (to the model developer, MRM, product, compliance), the response drafting chain, the review-and-approve routing before response goes to the supervisor. Include a walkthrough for a Draft Findings letter that names an AI-related finding.
- **Draft the parent-company / cross-sectoral communication memo.** If the entity is a subsidiary of a cross-sectoral group (a bank inside a bancassurance group; an investment firm inside a wider financial-services holding), draft in `cross-sectoral-communication-memo.md` how the entity's overlay row coordinates with parent-company / sibling-entity overlays. Cross-sectoral supervisors sometimes ask for consolidated positions.
- **Author the sandbox engagement brief.** If the local NCA operates a regulatory sandbox for AI (several EU NCAs do — FCA, BaFin, ACPR, others), draft in `nca-sandbox-engagement-brief.md` what a sandbox application would say — the AI system, the specific supervisory questions the sandbox would answer, the entity's expected commitments.
- **Draft the joint-supervisor briefing document.** For a system that crosses multiple supervisors (e.g., a bank-adjacent investment product), draft in `joint-supervisor-briefing.md` a briefing pack that a joint supervisory team would read — one narrative, cross-referenced to the applicable overlay memos, so the joint team does not have to synthesise from disparate memos.
- **Add a UK-PRA-SS1/23 crosswalk.** If the entity has UK exposure or your organisation compares against UK guidance, add `uk-pra-ss123-crosswalk.md` — a table mapping the ten PRA SS1/23 model-risk-management principles against the SR-11-7 artefact set from exercise `01`. The exercise reveals which SS1/23 principles are covered by the SR-11-7 shape and which are UK-specific.
- **Extend the watch-list to AI-specific overlays.** In `ai-specific-watch-list.md`, produce the parallel watch-list for AI-specific overlays — European AI Office, EDPB, national DPAs, Hiroshima AI Process work, G7 code developments. These are separate scans on separate cadences and the currency of each affects different release-package rows.
