# EU AI Act Article 55 and the GPAI Code of Practice

## Motivation

`mod-101` chapter `04` walked the EU AI Act articles that shape a high-risk release-gate. Article 55 was named at that walk — the systemic-risk overlay on top of the baseline GPAI obligations in Article 53 — but the article was not opened. This chapter opens it, together with the two neighbouring articles that decide *whether* Article 55 applies at all (Articles 51 and 52), and together with the operational reference most providers use to discharge the article's obligations in practice (the [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice)).

For a release-assurance methodology owner, the shift from the high-risk regime to the GPAI-systemic-risk regime is not cosmetic. The obligation set moves from *product* obligations (about a specific high-risk AI system placed on the market) to *model* obligations (about the general-purpose AI model itself, upstream of any specific product). The enforcement counterpart moves from Member-State market-surveillance authorities to the [European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) inside the European Commission. The evidence character moves from "does this system meet Articles 9–15?" to "have systemic risks at Union level been assessed and mitigated with state-of-the-art evaluation?"

This chapter walks the definition path (Articles 3(65), 51, 52), the Article 55 obligations themselves, and the Code of Practice as the operational discharge shape.

## The definition path — is this a GPAI model with systemic risk?

Before Article 55 applies, the model has to be *classified* as a GPAI with systemic risk. Three articles carry that classification path.

### Article 3(65) — the definition

**What it says.** Article 3 is the definitions article. Paragraph 65 defines a *general-purpose AI model with systemic risk* as a general-purpose AI model that has **high-impact capabilities** evaluated on the basis of appropriate technical tools and methodologies (including indicators and benchmarks), or that has been designated as such under Article 51 based on capabilities or impact equivalent to those with high-impact capabilities.

<!-- needs-research: reconfirm the exact wording of Article 3(65) in the current EUR-Lex text at https://eur-lex.europa.eu/eli/reg/2024/1689/oj, including how "high-impact capabilities" is glossed in the recitals. -->

**Release-assurance implication.** The definition is capability-driven, not use-case-driven. A GPAI can be systemic-risk-classified without any single high-risk downstream deployment; the classification attaches to the *model* on the basis of what it can do at the frontier. The release-assurance programme therefore has to know whether the *model artefact* it is shipping (or consuming from an upstream provider) falls inside the definition, independently of the products built on top.

### Article 51 — classification as GPAI with systemic risk

**What it says.** Article 51 sets out the criteria under which a GPAI model is classified as having systemic risk. A GPAI is *presumed* to have high-impact capabilities when the cumulative amount of compute used for its training, measured in floating-point operations (FLOP), is greater than **10^25 FLOP**. The AI Office may also designate a model as systemic-risk on the basis of capabilities or impact equivalent to that threshold, using criteria in Annex XIII (e.g., number of parameters, quality or size of the dataset, input and output modalities, benchmarks and evaluations of capabilities, reach, registered end-users).

<!-- needs-research: reconfirm the exact 10^25 FLOP threshold in Article 51(2) and the full Annex XIII criteria list in the current EUR-Lex text; also confirm whether the Commission has updated the threshold via delegated act since the original Regulation was published. -->

**Release-assurance implication.** The FLOP threshold is a *bright-line* criterion — a model above it is presumed in scope; the presumption can be rebutted only through a specific procedure. The Annex XIII criteria are the *equivalent-capability* path — a model below the FLOP threshold can still be designated systemic-risk if the AI Office judges its capability or impact to be equivalent. The release-assurance programme's intake step (`mod-102`) has to record training FLOP, parameter count, modality set, and reach as *classification-relevant* facts, not just as engineering trivia. The programme does not itself make the systemic-risk classification decision — the AI Office does — but it prepares the evidence the classification would rest on.

### Article 52 — procedure for notification and designation

**What it says.** Providers whose GPAI model meets or is likely to meet the Article 51(2) threshold shall notify the Commission without delay, and in any event within two weeks after that requirement is met or becomes known. The notification includes the information the Commission needs to assess the classification. The provider may present arguments alongside the notification for why, despite meeting the threshold, the model exceptionally does not present systemic risks. The Commission takes a decision; models may also be designated *ex officio* by the Commission on the basis of Annex XIII criteria.

<!-- needs-research: verify the two-week notification window and the current notification form / template hosted on the AI Office website. -->

**Release-assurance implication.** The notification is a *release-gate-adjacent* obligation. The release-assurance programme cannot ship a candidate model that crosses the threshold without confirming the Article 52 notification has been filed (or, for a rebuttal case, the rebuttal has been submitted and its rationale documented in the assurance bundle — `mod-104` chapter `06`). This is a `mod-102`-style intake gate: an Article 52 notification reference goes into the assurance case as a discharged obligation before any downstream Article 55 evidence is even collected.

## Article 55 — the systemic-risk provider obligations

Article 55 layers four obligations on top of the baseline Article 53 obligations that apply to any GPAI provider. The article's text uses "in addition to the obligations listed in Article 53" as its lead-in; the release-assurance programme discharges both sets, with Article 55 as the systemic-risk overlay.

### Article 55(1)(a) — state-of-the-art model evaluation, including adversarial testing

**What it says.** Providers of GPAI models with systemic risk shall perform model evaluation in accordance with standardised protocols and tools reflecting the state of the art, including conducting and documenting *adversarial testing* of the model with a view to identifying and mitigating systemic risks.

**Release-assurance implication.** This is where the assurance-bundle content set expands. The bundle (`mod-104` chapter `06`) already carries robustness, accuracy, and security evidence for the high-risk product regime; the Article 55(1)(a) overlay adds:

- **Standardised-protocol citation.** The programme names the protocol used for each capability domain — MLCommons AILuminate, HarmBench, WMDP, AgentDojo, etc. (chapter `04`) — and cites the version and configuration.
- **Adversarial-testing evidence.** Red-team reports from an internal team, a peer team (`agentic-safety-engineer` at level 40 for agentic capabilities), and, increasingly, a third-party evaluator (`mod-109`). The report set is signed and lands in the bundle under the `mlsec_manifest_digest` extension.
- **State-of-the-art documentation.** A justification of *why* the chosen protocols reflect the state of the art at the time of release — cited into the Frontier Model Forum's public library, the AISI-published evaluation guidance, the GPAI Code of Practice references. State-of-the-art is a moving target; the assurance case has to record the reference set as of the release date.

### Article 55(1)(b) — systemic-risk assessment and mitigation at Union level

**What it says.** Providers shall assess and mitigate possible systemic risks at Union level, including their sources, that may stem from the development, the placing on the market, or the use of general-purpose AI models with systemic risk.

**Release-assurance implication.** "At Union level" is the critical phrase. The assessment is not confined to a single downstream deployer or a single Member State's population — it looks at aggregate risk across the Union, including cross-border cascades, information-integrity effects on Union-wide public discourse, and cross-sector uplifts (biosecurity, cybersecurity, CBRN, and — increasingly — model-autonomy risks in agentic deployments). The assurance bundle carries a *Union-level systemic-risk assessment* as a distinct artefact from the product-level risk register (`mod-102`), with its own harm inventory, mitigation register, and residual-risk narrative.

### Article 55(1)(c) — serious-incident tracking and reporting to the AI Office

**What it says.** Providers shall keep track of, document, and report to the AI Office and, as appropriate, to national competent authorities, without undue delay, relevant information about serious incidents and possible corrective measures.

**Release-assurance implication.** The Article 61 / Article 73 serious-incident-reporting shape from the high-risk product regime (`mod-101` chapter `04`, `mod-110`) is extended to the GPAI-systemic-risk regime with the AI Office as the primary counterparty. The assurance bundle's post-market handoff (`mod-104` chapter `06`) references a *Union-level serious-incident procedure* that names the AI Office point of contact, the notification format, and the interlock with the post-market surveillance loop (`mod-110`).

### Article 55(1)(d) — adequate cybersecurity of the model and physical infrastructure

**What it says.** Providers shall ensure an adequate level of cybersecurity protection for the general-purpose AI model with systemic risk and the physical infrastructure of the model.

**Release-assurance implication.** Model-weight security, training-cluster security, inference-cluster security, and the operational security of the release-signing pipeline itself (`mod-104` chapter `04` for supply-chain provenance, chapter `05` for eval-set exfiltration) all attach here. The assurance bundle carries a *model-and-infrastructure cybersecurity attestation* signed by the `ai-infra-security` peer, with the same clause-mapped shape as the high-risk product regime's Article 15 evidence but scaled up: the threat model includes state-level model-exfiltration actors, and the attestation cites frameworks the Code of Practice references (see below).

## The GPAI Code of Practice — the operational discharge reference

Article 56 of the AI Act invites the drawing up of codes of practice at Union level to contribute to the proper application of the Regulation, taking into account international approaches. For GPAI, the [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) is the operational discharge reference. Signatories of the Code benefit from a **presumption of conformity** with the corresponding Article 53 and Article 55 obligations — the Code is not the only way to discharge the obligations, but it is the reference path.

<!-- needs-research: verify the exact clause of the AI Act that grants the "presumption of conformity" for Code signatories, and confirm which version of the Code (First Version, published 2025-07 per public reporting) is current at the time this chapter is read. -->

The Code is structured into three chapters, each of which carries a set of commitments and, per commitment, more granular measures:

### The safety and security chapter

**What it says.** The safety and security chapter operationalises Article 55 for signatories. It carries commitments on systemic-risk assessment (the frontier framework the signatory publishes), on model-evaluation shape (state-of-the-art evaluation with adversarial testing), on internal governance for safety decisions, on serious-incident tracking and reporting to the AI Office, and on cybersecurity of the model and infrastructure. The chapter is intentionally shaped so that a signatory's public frontier framework (Anthropic RSP, OpenAI Preparedness, Google DeepMind FSF — see chapter `02`) can be cited as the mechanism through which the commitments are met.

**Release-assurance implication.** The safety-and-security chapter is where the assurance programme lands the bulk of its Article 55 discharge evidence. The programme's assurance bundle carries, per Code commitment, a citation to the internal artefact (the frontier framework the enterprise or upstream provider follows, the evaluation report set, the incident procedure, the cybersecurity attestation) that discharges it.

### The transparency chapter

**What it says.** The transparency chapter operationalises the Article 53(1)(a)–(b) baseline GPAI obligations — the technical documentation for the model itself, and the information provided to downstream providers who integrate the model into their AI systems. It includes a **Model Documentation Form** shape that structures the disclosure.

**Release-assurance implication.** This chapter is where the model card (`mod-105`) and the downstream-provider integration documentation land. The assurance programme cites the Model Documentation Form as the shape and the model card as the derived public-audience view.

### The copyright chapter

**What it says.** The copyright chapter operationalises Article 53(1)(c)–(d) — the copyright policy and the training-content summary. It carries commitments on respecting text-and-data-mining opt-outs under Directive (EU) 2019/790, on internal copyright compliance procedures, and on the training-content summary template.

**Release-assurance implication.** This chapter interfaces with the dataset cards (`mod-105`) and with the training-data-summary artefact the assurance bundle carries. It is *not* a systemic-risk-specific chapter — it applies to all GPAI providers — but a systemic-risk provider carries the same obligations and the assurance bundle carries the same citations.

### The Code as living reference, not statute

The Code of Practice is *not statute*. Its authority derives from Article 56's invitation to codes of practice and from the presumption-of-conformity mechanism the Regulation provides for signatories. Two implications follow.

First, the Code is *revisable*. The AI Office and the signatories can (and are expected to) revise the Code as the state of the art evolves — evaluation methodology improves, capability categories are refined, incident-reporting patterns settle. The assurance case cites the Code by version; a later version does not retroactively invalidate a discharge that was compliant with the version-at-release, but it does reset the expectation for subsequent releases.

Second, the Code is *not the only discharge path*. A GPAI-systemic-risk provider is free to discharge Article 55 obligations through other means — bespoke evaluation methodology, an alternative frontier framework, an independent audit — as long as the discharge is defensible under the article. The Code's advantage is the presumption of conformity; the alternative discharge paths carry higher evidentiary burden. Enterprises typically pick a specific position (sign the Code, or explain in the assurance case why the alternative discharge equals or exceeds the Code's shape).

## The European AI Office

The European AI Office (established inside DG CNECT of the European Commission) is the *enforcement counterpart* for GPAI obligations, including Article 55. Its remit includes:

- Contributing to the coherent application of the Act across the Union, in particular for GPAI.
- Monitoring the implementation and application of the GPAI rules, and of the Code of Practice.
- Receiving notifications under Article 52 and taking classification decisions.
- Receiving serious-incident reports under Article 55(1)(c).
- Issuing guidance, standardised documentation templates (including the Model Documentation Form), and, over time, further technical detail.

**Release-assurance implication.** The AI Office is *the* counterparty the assurance bundle is written for on the GPAI side. Where a high-risk product's bundle is written for a Member-State market-surveillance authority (`mod-101` chapter `04`), a GPAI-systemic-risk bundle is written for the AI Office. The programme's third-party interface (`mod-109`) has to include the AI Office among its listed counterparties, with the AI Office's expected verification walk (`mod-104` chapter `06`) documented against the bundle's shape.

## Worked example — assurance package for a general-purpose LLM with systemic risk

Suppose the enterprise trains a general-purpose LLM whose training compute crosses 10^25 FLOP, intends to place it on the market inside the Union, and files an Article 52 notification. Concretely, the assurance package extends the baseline bundle as follows:

- **Intake (`mod-102`).** The assurance case records Article 3(65), Article 51(2) FLOP crossing, Article 52 notification reference, and the AI Office's classification decision (or, if the provider is rebutting the presumption, the rebuttal submission reference and its rationale).
- **Frontier framework citation.** The signatory publishes (or adopts) a frontier framework in the shape of chapter `02` (RSP-like, Preparedness-like, or FSF-like). The framework is cited in the assurance bundle as the mechanism through which the Code of Practice safety-and-security commitments are met.
- **State-of-the-art evaluation set (Article 55(1)(a)).** MLCommons AILuminate, WMDP, HarmBench, AgentDojo, plus internal red-team runs — each cited with version, configuration, and result (chapter `04`). The state-of-the-art justification (why *this* set at *this* release) is a distinct artefact.
- **Union-level systemic-risk assessment (Article 55(1)(b)).** A separate assessment document, structured under NIST AI 600-1's GenAI risk categories (chapter `03`), with each risk assessed at Union level.
- **Serious-incident procedure (Article 55(1)(c)).** A procedure referencing the AI Office as counterparty, with notification templates, timelines, and interlock into `mod-110`.
- **Cybersecurity attestation (Article 55(1)(d)).** Weight-storage security, training-cluster security, inference-cluster security, insider-risk controls — signed by `ai-infra-security`.
- **Model Documentation Form.** A completed Model Documentation Form per the Code of Practice's transparency chapter, plus the derived public-audience model card (`mod-105`).
- **Training-content summary and copyright policy.** Per the Code of Practice's copyright chapter.

The bundle is signed and persisted per `mod-104` chapter `06`, with the additional Article 55 evidence extending the manifest.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — the assurance case carries Article 55 claims and cites their evidence in one hop.
- `mod-104` chapter `06` (signed assurance bundle) — the bundle is extended with Article 55 evidence for systemic-risk-tier releases.
- `mod-105` (cards for external audiences) — the Model Documentation Form is the shape of the transparency-chapter disclosure.
- `mod-108` (deployment-tier gating) — chapter `02` of this module reads frontier frameworks that the deployment-tier gate typically adopts.
- `mod-109` (third-party evaluator interface) — the AI Office and AISI-shape evaluators are counterparties to the Article 55 evidence set.
- `mod-110` (post-market surveillance) — the serious-incident procedure interlocks with the post-market loop.

## Summary

- Article 55 of the EU AI Act carries four systemic-risk-specific provider obligations: state-of-the-art model evaluation including adversarial testing, systemic-risk assessment and mitigation at Union level, serious-incident tracking and reporting to the AI Office, and adequate cybersecurity of the model and infrastructure.
- The classification path runs through Article 3(65) (definition), Article 51 (10^25 FLOP presumption plus Annex XIII equivalent-capability criteria), and Article 52 (notification and designation procedure). The provider notifies within two weeks of meeting the threshold; the AI Office decides.
- The [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) is the operational discharge reference, structured in safety-and-security, transparency, and copyright chapters. Signatories benefit from a presumption of conformity with the corresponding Article 53 / 55 obligations.
- The European AI Office is the enforcement counterparty for GPAI obligations, including receiving notifications and serious-incident reports.
- The assurance bundle (`mod-104` chapter `06`) is extended with Article 55 evidence — the state-of-the-art evaluation set, the Union-level systemic-risk assessment, the serious-incident procedure with the AI Office as counterparty, and the model-and-infrastructure cybersecurity attestation.
- Exercise 01 has you build the Article 55 + Code of Practice obligation map for a worked GPAI-systemic-risk release, obligation by obligation, with the discharge artefact per row.
