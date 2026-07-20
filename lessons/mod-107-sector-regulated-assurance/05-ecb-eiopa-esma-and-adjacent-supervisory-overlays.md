# ECB, EIOPA, ESMA, and Adjacent Supervisory Overlays

## Motivation

Chapters `01`–`04` covered the anchor instruments: SR 11-7 / OCC 2011-12 (U.S. banking model risk), SR 23-4 (U.S. banking third-party), FDA GMLP + PCCP (U.S. medical devices), and DORA (EU financial-sector operational resilience). These are the *hard* instruments — statute, formal supervisory guidance, or agency guidance with clear applicability. The release-assurance methodology owner in a regulated sector also has to track a second, softer layer: **supervisory expectations** that European sectoral authorities and their U.S. equivalents publish through opinions, discussion papers, thematic reviews, guides, and speeches. This layer is fast-moving. It has real teeth in the sense that a supervisor's expectations show up as findings at the next inspection, but it is not the same as statute — it is the way statute is being interpreted, and the interpretation shifts.

For a release-assurance owner running a programme at a European bank, insurer, or investment firm, the supervisory-overlay landscape at time of writing includes: **ECB Banking Supervision** expectations on model risk and — increasingly — on AI-specific risks in supervised banks; **EIOPA** opinions and consultation papers on AI in insurance; **ESMA** statements on AI in investment services and market conduct; and, on the U.S. side, adjacent **FDIC / OCC / Federal Reserve interagency** guidance that supplements SR 11-7 and SR 23-4. None of these overlays carries the release-gate weight of the anchor instruments. All of them shape *what a supervisor will look for* at the next inspection, and any of them can escalate to statute or to formal guidance without notice.

This chapter reads the overlays at the level of *what a release-assurance owner has to track*, not at the level of a full-text paraphrase — because the primary sources shift and any full paraphrase authored today will be stale before the next review cycle. Where the current state of a piece of guidance matters for a release-package artefact, this chapter says so, and marks details that need verification with `<!-- needs-research: ... -->`. Exercise-04 asks you to draft the supervisory-overlay row of the release-package for one European-financial-sector AI system.

## ECB Banking Supervision — model risk and AI expectations

The [European Central Bank's Banking Supervision function](https://www.bankingsupervision.europa.eu/) supervises significant institutions in the Single Supervisory Mechanism (SSM) and coordinates with national competent authorities for less-significant institutions. Its model-risk expectations grew out of the **Targeted Review of Internal Models (TRIM)**, a multi-year exercise that ran through 2015–2020 and produced the ECB [Guide to internal models](https://www.bankingsupervision.europa.eu/) covering credit, market, and counterparty-credit risk. <!-- needs-research: verify current title, version, and publication date of the ECB Guide to internal models (successor edition since the 2019 general topics chapter) -->

**What it says (at the level relevant to AI systems).** The ECB expects significant institutions to have a robust model risk management framework covering the full lifecycle, an inventory, independent validation, and effective governance. Where AI/ML models are used in supervised functions, they are expected to fit inside this framework and to receive rigour commensurate with their materiality. The ECB has published thematic communications and speeches on AI risks in banking (including on generative AI); these are not formal guides but they signal what supervisors will ask about.

**Release-assurance implication.** For a significant institution, the release-gate for an AI system in a supervised function must operate inside the bank's ECB-facing model risk management framework. Where the AI system participates in an internal-model activity (credit risk, market risk, counterparty-credit risk), the release-package additionally cites the relevant chapter of the ECB Guide and the bank's own gap analysis against it. The release-assurance owner tracks ECB communications on AI and updates the release-package template when the ECB's expectations shift. This is more a *watch-list obligation* than a static one.

The interface between the ECB expectations and the release-gate is typically operationalised through the bank's own MRM policy, which cites the ECB Guide and the local supervisor's expectations as feeders and treats the release-assurance programme as the second-line implementation. That means the release-package rarely cites ECB documents directly — it cites the bank's own MRM policy, which cites the ECB.

## EIOPA — AI in insurance

The [European Insurance and Occupational Pensions Authority](https://www.eiopa.europa.eu/) has published a sequence of documents on AI in insurance, including the 2021 report on AI governance principles from its Consultative Expert Group on Digital Ethics in Insurance, and subsequent opinions and consultation papers on AI use in specific insurance functions (underwriting, pricing, claims handling, fraud detection). <!-- needs-research: verify current EIOPA landing page URL for AI, and the latest opinion or consultation paper reference; the AI-in-insurance workstream is active and titles/URLs shift -->

**What it says (at the level relevant to AI systems).** EIOPA's overlay emphasises proportionality (rigour matches the impact of the AI use case on the policyholder), fairness in pricing (particular attention to indirect discrimination and to explainability of pricing outcomes), consumer protection (transparency to the policyholder about AI use), and — for cross-cutting risk — governance and human oversight. The 2021 report's six principles of ethical and trustworthy AI in insurance function as a soft-baseline that EIOPA references in later work.

**Release-assurance implication.** For an insurance AI system, the release-package carries a **proportionality determination** citing the EIOPA framing, a **fairness-in-pricing analysis** where the system touches pricing or underwriting (with sensitivity analysis across protected characteristics as reasonably practicable under data-availability constraints), and a **consumer-facing transparency artefact** that discharges the disclosure expectations. Where DORA (chapter `04`) covers operational resilience of the same system, the EIOPA overlay covers conduct-oriented expectations that DORA does not touch. The two are complementary rather than overlapping. The release-assurance owner has to run *both* rows in the release-package for an EU insurer's AI system.

## ESMA — AI in investment services

The [European Securities and Markets Authority](https://www.esma.europa.eu/) has taken a supervisory-convergence stance on AI use in investment services, coordinating national competent authorities in applying MiFID II and MiFIR obligations to AI-enabled activities. ESMA has published statements on the applicability of existing conduct-of-business rules to AI use, thematic communications on AI-generated content and market conduct, and — in coordination with the other ESAs under DORA — technical standards for the financial sector. <!-- needs-research: verify current ESMA statements on AI in investment services and any subsequent public statements on generative AI in investment advisory; ESMA also acts as a Lead Overseer under DORA Article 32 for designated critical ICT third-party service providers, and the release-assurance owner tracks any published expectations from that role -->

**What it says (at the level relevant to AI systems).** ESMA's overlay emphasises that existing conduct-of-business, best-execution, product-governance, and suitability obligations apply *unchanged* to AI-enabled investment services. Where AI is used in client-facing activities, firms are expected to demonstrate that the AI's outputs are consistent with these obligations. Where AI is used in market-facing activities (algo-trading, market-making), the existing MiFID II algorithmic-trading requirements (RTS 6 and the associated ESMA guidelines) apply.

**Release-assurance implication.** For an investment-services AI system, the release-package carries an **existing-obligation applicability memo** — the analysis showing which existing MiFID II / MiFIR obligations apply to the AI-enabled activity and how the AI's design supports them. For an algorithmic-trading AI, the release-package additionally carries the RTS-6-shaped controls (self-assessment, testing, monitoring, stress testing, kill functionality) with AI-specific elements added. The release-gate cannot approve an investment-services AI system whose existing-obligation applicability memo has not been signed off by the compliance function.

## FDIC and OCC — U.S. interagency adjacent guidance

On the U.S. side, chapter `02` covered the joint 2023 Interagency Guidance on Third-Party Relationships (SR 23-4 / OCC 2023-17 / FDIC FIL-29-2023). The three federal banking agencies also periodically issue [**joint statements**](https://www.occ.gov/news-issuances/bulletins/index-bulletins.html) and thematic communications on adjacent topics that touch AI risk management, including on model risk, cyber and operational resilience, and consumer-compliance risk. <!-- needs-research: verify the current inventory of interagency statements touching AI use in banks, particularly any subsequent joint guidance or requests-for-information following the June 2021 RFI on financial institutions' use of AI -->

**What it says (at the level relevant to AI systems).** The interagency posture at time of writing is that existing supervisory expectations (SR 11-7, SR 23-4, sector consumer-protection rules) apply to AI use, and that firms are expected to adapt those expectations to AI-specific characteristics rather than to await new AI-specific rules. Individual agency communications (OCC Semiannual Risk Perspective, FDIC risk reviews) periodically call out AI risks the agencies are focused on.

**Release-assurance implication.** For a U.S.-supervised bank, the release-package carries the SR-11-7 and SR-23-4 artefacts from chapters `01` and `02`; the interagency overlay is what the release-assurance owner watches for signals about *what supervisors will ask about next*. Where an OCC Semiannual Risk Perspective calls out a specific AI-related concern (for example, generative-AI-enabled fraud, model-risk-management for foundation models), the release-package template is updated to ensure the release-gate has visibility on that concern.

## The overlay is *watch-list* work, not point-in-time work

The single most important thing to internalise about supervisory overlays is that they change. A EIOPA opinion published today becomes an EIOPA guideline in eighteen months. An ECB thematic communication becomes a Guide chapter within two supervisory cycles. An ESMA supervisory-convergence statement becomes a Q&A that supervisors then apply as expectations. The release-assurance methodology owner therefore runs a **watch-list process** that periodically re-reads the sectoral authorities' landing pages, checks for new publications, updates the release-package template, and — where a change is material — re-releases affected AI systems' assurance cases against the updated shape.

A typical watch-list cadence:

- **Monthly** — scan the landing pages of ECB Banking Supervision, EIOPA, ESMA, the U.S. federal banking agencies, and any sector-specific supervisor the entity is subject to; note new publications; triage.
- **Quarterly** — deep-read any publication triaged as material; update the release-package template if warranted; brief the assurance function and the compliance function.
- **Annually** — walk the release-package templates for each in-scope AI system against the current state of the overlays; identify systems whose assurance cases now materially lag the state of expectations; queue re-releases as needed.
- **Ad-hoc** — on any inspection communication (a Draft Findings letter, an information request, a thematic review announcement), map the communication onto affected release-packages within a stated window.

This watch-list process is itself an ISO/IEC 42001 clause-9 (performance evaluation) activity for the assurance programme and shows up in the programme's own management-review agenda (`mod-112`).

## Worked shape — a robo-advisor at a mid-sized EU investment firm

Take a concrete system: a **robo-advisor** at an EU investment firm, providing MiFID-II-suitable investment advice to retail clients on a subscription basis. It uses a portfolio-optimisation engine built in-house, an LLM-based client-interaction layer using a hosted foundation model, and an automated suitability-assessment component.

Plugged into the supervisory overlays:

- **ESMA overlay**: existing-obligation applicability memo covering MiFID II suitability (Article 25), best interests of clients (Article 24), product governance (Article 16(3), ESMA product-governance guidelines), and the ESMA supervisory-convergence expectations on AI in investment services; the memo names each obligation and points at the release-gate criterion that discharges it.
- **DORA overlay** (chapter `04`): register-of-information entry for the foundation-model provider; Article 30(3) clauses; concentration-risk memo.
- **National-competent-authority overlay**: the local NCA's own supervisory expectations on robo-advice (many EU NCAs have published such expectations); tracked in the watch-list; cited where applicable.
- **EIOPA overlay**: not applicable directly (the firm is an investment firm, not an insurer), but tracked in the watch-list because the firm's parent group is an insurance-adjacent group and cross-sectoral communications sometimes matter.
- **ECB overlay**: not applicable (the firm is not a credit institution), but the watch-list still notes ECB SSM communications where relevant to group-level considerations.

The release-package carries: the ESMA-anchored applicability memo, the DORA artefacts (chapter `04`), the local-NCA overlay memo, and an assurance-function statement on the watch-list currency. Exercise-04 asks you to draft the applicability memos and the watch-list-currency statement for one European-financial-sector AI system of your own choosing.

## Interfaces with the AI-specific overlay set

The supervisory overlays discussed above are the *sectoral* overlays — they come from the authorities that supervise the financial or insurance or investment sector. There is a parallel *AI-specific* overlay set that the release-assurance methodology owner also tracks: the European AI Office and its GPAI Code of Practice work (`mod-111`); the European Data Protection Board's guidance where AI processing engages GDPR (in particular the EDPB's 2024 opinion on AI models trained on personal data <!-- needs-research: verify current EDPB opinion numbering and any subsequent guidance on AI and GDPR -->); and the network of national data-protection authorities whose expectations on automated decision-making under GDPR Article 22 apply to consumer-facing AI systems.

These AI-specific overlays interact with the sectoral overlays in ways the release-package has to disposition. Where a sectoral authority's expectation and an AI-specific authority's expectation cover the same ground with different vocabulary — for instance, on transparency to affected persons in credit decisions, where EIOPA and CFPB (for insurance-adjacent products at cross-jurisdictional firms) and GDPR Article 22 all have views — the release-package writes to the union of the expectations, cites all applicable primary sources, and lets the compliance function determine whether any hard release-gate criteria need to be added beyond what each individual overlay would require.

## National competent authorities and the local overlay

Above the EU-level authorities sit the national competent authorities (NCAs) that supervise entities on the ground: the BaFin in Germany, the AMF and ACPR in France, the CNMV and Banco de España in Spain, the FCA and PRA in the UK (outside the SSM but still a major reference), the Bank of Italy, the Central Bank of Ireland, and their sibling authorities across other Member States. Each NCA maintains its own supervisory expectations on AI in the sectors it supervises, and each NCA can publish thematic communications, dear-CEO letters, or Q&As that materially shape what an entity's release-package needs to contain.

For a release-assurance methodology owner running a programme at a single-jurisdiction entity, the local NCA is often the most immediately load-bearing overlay — more so than ECB Banking Supervision or ESMA at times, because the NCA is the entity that runs the inspections. The watch-list process (below) therefore has an NCA row for each jurisdiction the entity operates in.

For a release-assurance owner running a programme at a cross-border entity — a bank operating in multiple EU Member States, an insurer with authorisations in several — the NCA row multiplies, and the watch-list has to track each jurisdiction's local overlay separately. Where NCAs' expectations diverge, the release-package documents the divergence and — where possible — writes to the more-demanding of the applicable expectations for each release surface.

## Speculative synthesis and how to mark it

Several claims in this chapter — especially ones about the *current* state of supervisory expectations — will be out of date within a supervisory cycle. Where the release-assurance owner is drafting release-package content that cites this material, the discipline is:

- Cite from the sectoral authority's own landing page or from a specific numbered document.
- If a specific fact (a URL, a document number, a publication date) is not verifiable from a primary source at the time of drafting, mark the claim `<!-- needs-research: describe what needs verification -->` inline and route it to the compliance function for confirmation before the release-package is signed.
- Do not paraphrase a supervisor's public statement into hard release-gate criteria; instead, cite the statement, describe how the release-package acknowledges it, and let the compliance function determine whether harder criteria are warranted.

The tone of the release-package on the overlay row is: *the assurance function tracks the current state of supervisory expectations, has read them, has captured them in the release-gate design where appropriate, and can point at the primary source on request*.

## Where this shows up in the rest of the track

- `mod-101` — the supervisory-overlay work is one instance of the deferral-contract shape from `mod-101` chapter `06`: the compliance function owns the primary reading of overlays; the assurance function owns their reflection in the release-package.
- `mod-102` — the assurance case's context nodes cite the applicable overlays as declared premises; the case does not carry them as claims because they are not falsifiable in the same way.
- `mod-103` — the release-gate schema carries an `overlays_current_as_of` field with a timestamp; a stale overlay currency is a soft-gate that must be dispositioned.
- `mod-104` — the evidence pipeline carries watch-list scan records and overlay applicability memos as artefact types.
- `mod-106` — the cross-jurisdictional obligation map places the supervisory overlays as feeders into the applicable column per jurisdiction.
- `mod-109` — external auditors and third-party evaluators are often the ones who catch overlay drift the internal watch-list missed; the interface (`mod-109`) is where these signals arrive.
- `mod-112` — the watch-list is a management-review agenda item for the assurance programme.

## Summary

- Supervisory overlays — ECB Banking Supervision, EIOPA, ESMA, and adjacent U.S. interagency guidance — are the *soft* layer of expectations that sit alongside statute and formal supervisory guidance. They are fast-moving and mostly interpretive rather than binding.
- ECB expects AI/ML models in supervised functions to fit inside the bank's model-risk-management framework; EIOPA emphasises proportionality, fairness in pricing, and consumer transparency in insurance AI; ESMA emphasises that existing MiFID II conduct obligations apply unchanged to AI-enabled investment services.
- U.S. federal banking agencies periodically publish interagency communications signalling AI-related supervisory focus; these do not create new obligations but shape what supervisors will ask about at the next inspection.
- The release-assurance owner runs a **watch-list process** (monthly / quarterly / annual / ad-hoc) that periodically re-reads the sectoral authorities' landing pages, updates release-package templates, and queues re-releases where a change is material.
- Speculative synthesis in release-package content is marked `<!-- needs-research: ... -->` and routed to the compliance function for confirmation before sign-off; the release-package cites primary sources and does not paraphrase supervisor statements into hard release-gate criteria.
- Exercise-04 asks you to draft the applicability memos and the watch-list-currency statement for one European-financial-sector AI system.
