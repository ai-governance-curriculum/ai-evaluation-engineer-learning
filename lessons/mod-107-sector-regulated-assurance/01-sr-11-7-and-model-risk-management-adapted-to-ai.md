# SR 11-7 and Model Risk Management, Adapted to AI

## Motivation

For a release-assurance methodology owner working on any AI system that touches a U.S. bank, broker-dealer, insurer, or federally-supervised financial services function, the ground under the release-gate is not NIST AI RMF and it is not the EU AI Act. It is **SR 11-7 / OCC 2011-12** — the [Federal Reserve's Supervisory Letter SR 11-7 on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm), issued 2011-04-04, and its companion [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) issued the same day. This joint guidance replaced the older OCC 2000-16 and became — for practical purposes — the U.S. banking sector's constitution for how *any* quantitative model must be governed. Fifteen years later, it is still what a U.S. supervisor examines against, and it is still the shape a bank's Model Risk Management (MRM) function is built to.

Two facts matter for this module. First, SR 11-7 pre-dates the modern AI/ML wave by more than a decade; its authors were thinking about credit scorecards, market-risk VaR, ALLL provisioning models, and pricing engines. Every AI-specific rough edge you find in it — foundation-model reuse, prompt-based systems, evaluation-set contamination, agentic behaviour — is an *adaptation*, not a native fit. Second, despite that vintage, its shape holds up remarkably well: an inventory, a risk-tiering, an effective-challenge convention, developmental evidence, on-going monitoring, and an accountable governance chain. The release-assurance methodology owner's job in a regulated-sector context is to run the AI release-gate *inside* that shape, not alongside it — because supervisors will not accept "AI is different, so we run a parallel programme."

This chapter paraphrases the SR 11-7 shape in the language a release-assurance owner already speaks, threads it against NIST AI RMF and EU AI Act obligations from `mod-101`, and then walks the joints where AI stresses the 2011 shape and requires deliberate adaptation. The exercise (exercise-01) has you author an SR-11-7-shaped document set for one concrete AI model.

## What SR 11-7 says, in one paragraph per element

The guidance is short by regulatory standards (roughly 21 pages) and reads as prose rather than as a numbered rulebook. Its substantive content clusters into six elements, each of which becomes a release-gate concern.

### Model definition and scope

**What it says.** SR 11-7 defines a *model* as a "quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates." Anything that fits — regardless of whether it is called a model by its developer — is in scope. The definition is deliberately broad: spreadsheets, rule engines with statistically-tuned parameters, third-party vendor tools, and champion/challenger frameworks all count. Model risk is defined as the potential for adverse consequences from decisions based on incorrect or misused model outputs, arising principally from fundamental errors and from incorrect or inappropriate use.

**Release-assurance implication.** Every AI system a U.S. bank deploys is a model in SR-11-7's sense — and often several models composed. A RAG system with an LLM, a retriever, and a re-ranker is at least three models. A fine-tuned foundation model plus an inference-time guardrail classifier is at least two. The release-gate scope statement (mod-103) must enumerate each model in the composition, because MRM inventory (below) tracks each individually. Reasoning "the LLM is not a model, it's a general capability" does not survive first contact with a supervisor.

### Model inventory

**What it says.** Firms must maintain a comprehensive model inventory identifying every model in use or recently retired, along with information sufficient to describe the model, its purpose, its input and output data, its use, and its risk tier. Ownership and validation status must be recorded. The inventory is a live artefact, refreshed on a stated cadence, and reconciled at least annually.

**Release-assurance implication.** The release-assurance methodology owns *entry to and update of* the MRM inventory for AI systems. Every release-gate pass emits an inventory record or an inventory update; the release package (mod-104) carries the inventory-diff as an artefact. Where an enterprise runs a model-catalogue tool alongside the release pipeline, the release-gate is what promotes an inventory record from "candidate" to "in production."

### Risk tiering

**What it says.** Models are tiered by materiality of the decisions they inform, complexity, and the extent of exposure to model error. Higher-tier models receive more rigorous development testing, independent validation, and monitoring; lower-tier models can be governed more lightly. The firm's own tiering methodology is a documented artefact and is itself subject to review.

**Release-assurance implication.** Tiering is where SR 11-7 meets `mod-108` (deployment-tier gating) most directly. A bank's model-risk tier and this programme's deployment tier are two different taxonomies serving related purposes; the release-gate design must state the mapping between them and cite it in every release decision. A T2/T3 deployment on the assurance side almost always corresponds to a Tier-1 or Tier-2 MRM designation on the bank side, but the mapping is not automatic and needs to be pre-registered.

### Effective challenge

**What it says.** Development and use of a model must be subject to *effective challenge* — critical analysis by objective, informed parties who can identify model limitations and produce appropriate changes. Effective challenge requires the challengers to be independent of model development, competent to assess the model, and empowered to influence outcomes. This is the concept the industry structures its **three lines of defence** around: the first line is the business function that owns the model and its outcomes; the second line is Model Risk Management (independent validation, model-risk policy, aggregate reporting); the third line is Internal Audit (assurance over the second line).

**Release-assurance implication.** The release-gate operates in the *second line* for AI systems — the assurance methodology is the effective-challenge instrument for MRM. Every release decision is second-line effective challenge on record. Where the release-gate signs off, it does so *as a second-line function*, not as an extension of development. This has RACI consequences: the signer of the assurance decision cannot be the model developer, cannot report to the model developer, and cannot have a compensation link to the model's business outcomes. Internal Audit's periodic review of the release-assurance programme itself is the third-line loop.

### Model development, implementation, and use

**What it says.** Firms must document the design, theory, and logic underlying each model; the data used in development; the assumptions; the testing performed (including outcomes analysis, benchmarking, and sensitivity analysis); and the results. Implementation controls (change management, access control, environment reproducibility) are part of the documentation. Model use — including the business decisions the model informs and any overrides — is documented.

**Release-assurance implication.** This is the SR-11-7 sibling of EU AI Act Article 11 (technical documentation) and NIST AI RMF MEASURE. The release-package template for a U.S. banking AI system carries: a **Model Description Document (MDD)** covering theory, assumptions, data, and design; a **Model Development Testing report** covering outcomes analysis, benchmarking, and sensitivity analysis; an **Implementation Testing report** covering change management and environment reproducibility; and a **Model Use** section describing the intended use and the human-override design. These four artefacts are the developer-side inputs the release-gate consumes; independent validation (below) is the second-line output.

### Independent validation and on-going monitoring

**What it says.** All models are subject to validation performed by staff independent of model development. Validation covers evaluation of conceptual soundness, on-going monitoring (process verification and benchmarking), and outcomes analysis (comparison of model outputs to actual outcomes). Validation is repeated on a stated cadence and after material changes. Deficiencies are tracked to remediation.

**Release-assurance implication.** Independent validation is the artefact the release-gate consumes as its second-line input. For a Tier-1 model, an independent-validation report signed by an MRM validator is a hard-gate criterion. For a Tier-2 model, a validation-scope memo plus targeted validation testing suffices. On-going monitoring becomes a release-gate emission (mod-110) — the release-gate does not close on ship, it hands off to a monitoring cadence that will re-open the gate at the next material change or at the next scheduled revalidation.

### Governance, policies, procedures, and controls

**What it says.** Board and senior management establish a strong model-risk-management framework, including a written policy setting out roles and responsibilities, a risk-appetite statement for model risk, escalation procedures, and independence of the MRM function. Policies are refreshed and demonstrably applied.

**Release-assurance implication.** The release-assurance methodology *is* an operationalisation of the model-risk policy for AI systems. The methodology document (mod-112) has to name where it sits under the MRM policy, cite the policy's authority for its criteria, and route material dispositions (waivers, high-risk-model exceptions, incident-triggered re-validations) up the same governance chain the rest of MRM uses.

## Model risk tiering — a closer look

Because tiering decides how much rigour each downstream artefact receives, it is worth reading the SR 11-7 tiering paragraph carefully. The guidance does not prescribe a specific taxonomy; it prescribes the *factors* the taxonomy must consider (materiality of decisions, model complexity, extent of exposure to model error) and requires the firm's own methodology to be documented, applied consistently, and reviewed.

Most U.S. banks operate a three-tier or four-tier scheme. A typical shape:

- **Tier 1** — highest materiality: models whose outputs directly drive regulatory-capital calculations, consumer-facing credit decisions, or other externally-consequential judgements. Highest rigour of validation, most frequent revalidation cadence, standing MRM oversight.
- **Tier 2** — significant materiality: models whose outputs materially inform business decisions but not with the same regulatory or consumer stakes as Tier 1. Full validation with a lighter revalidation cadence.
- **Tier 3** — limited materiality: models whose outputs inform internal operational decisions with limited external effect. Streamlined validation and lower-frequency monitoring.
- **Tier 4** (where used) — de minimis: models whose failure would have negligible effect. Inventory tracking only.

For AI systems the tiering has to consider factors that SR 11-7's drafters did not name: reversibility (how easily can a bad output be caught and corrected before it affects a customer?), scale (how many decisions does the model influence per unit time?), and composability (is this model on its own, or is it one of several composed to produce a downstream decision?). The release-assurance methodology owner works with MRM to include these factors in the tiering methodology and to document how AI-specific characteristics map onto tiers.

## Where AI stresses the SR 11-7 shape

SR 11-7 works well for a credit scorecard whose input schema is fixed, whose training data is your own, whose behaviour is stationary between refreshes, and whose failures show up in tractable outcome metrics. AI systems — especially foundation-model-based ones — depart from this profile in ways the 2011 guidance did not contemplate. Four departures matter most.

### Foundation-model reuse and the "third-party model" problem

An SR-11-7 inventory row historically named a *model that the bank owns end-to-end*. A foundation model is a shared upstream artefact used by hundreds of downstream systems, with training data the bank does not see, capabilities the bank cannot fully enumerate, and updates the bank does not control. SR 11-7's own §VI covers third-party models but assumes an inventory row per third-party model with a validation package supplied by the vendor. For a foundation-model provider, there is no such package in the classical shape, and vendor documentation is a card, not a validation report. The adaptation covered in chapter `02` maps foundation-model providers onto the newer [SR 23-4 third-party-relationships shape](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm) and treats the foundation model as an ICT third-party arrangement, not as a classical vendor model.

### Prompt-based and agentic systems

An SR 11-7 model has a well-defined input schema (borrower attributes → PD estimate) and a well-defined output. A prompt-based LLM has an input surface of *free text*, an output space of *free text*, and — for agentic systems — an action space that includes tool calls with side-effects. Development testing has to cover a much larger surface, on-going monitoring has to include semantic drift and behaviour drift (not just statistical drift of a scalar output), and outcomes analysis has to reconstruct sequences of interactions rather than point predictions. None of this is impossible under SR 11-7 — but the *evidence contracts* between the developer and the second-line validator (mod-102 chapter `06`) have to be re-negotiated for these surfaces.

### Evaluation-set contamination as an integrity risk

In 2011, an evaluation set was your own held-out data and integrity meant training/validation/test disjointness. For AI models, especially those built on public foundation models, an evaluation set can be *contaminated* if it appears in the foundation model's training corpus — the model has seen the answers, and the reported performance overstates capability. This class of integrity risk was not contemplated in SR 11-7's model-development-testing paragraph and requires deliberate treatment: evaluation-set provenance, canary strings, benchmark-refresh cadence, and — for high-tier systems — private evaluation sets that never leave a controlled environment. The release-assurance methodology owns the *policy* that requires this treatment; `mod-104` owns the evidence pipeline that discharges it.

### On-going monitoring against a moving upstream

SR 11-7 on-going monitoring assumes the model is stable and the world drifts. Foundation-model-backed AI systems have the opposite problem: the *model* may drift as the vendor pushes silent updates, deprecations, or fine-tune-cycle changes. Monitoring cadence has to fire on *vendor announcements* as well as on outcome-metric drift, and the release-gate has to include a **vendor-change trigger** in the reversal contract (mod-103). Chapter `02` develops this into a full-shape SR 23-4 mapping.

### Three lines of defence, restated for AI

The three-lines-of-defence structure that SR 11-7 crystallised deserves a paragraph of its own because it is the load-bearing organisational shape a supervisor will ask about first, and it is the shape most easily eroded by AI-native product organisations that grew up without it.

- **First line — the business function that owns the model and its outcomes.** For AI systems this typically includes the product team, the ML engineering team, and the operational team running the deployment. The first line owns model performance and is accountable for its use.
- **Second line — Model Risk Management (or an equivalent independent function).** MRM sets policy, maintains the inventory, tiers models, performs independent validation, and reports aggregate model risk to senior management. The release-assurance methodology sits *inside* the second line for AI systems; the release-gate is the second-line's operational instrument.
- **Third line — Internal Audit.** Internal Audit provides periodic independent assurance over the second line, including over the release-assurance methodology itself. The third line does not itself validate individual models; it validates that the second line does.

When an AI product organisation is set up without this structure — a common pattern in AI-native startups that later acquire a regulated deployment surface — the release-assurance owner's first job is to name the missing lines, propose the structure, and get an accountable senior-management sign-off on the RACI. Without that sign-off, the release-gate has no defensible authority to block a release, and the supervisor's first question at inspection ("show us your three lines") produces a finding.

### Model performance report — the standing artefact

SR 11-7 also introduces, implicitly through its on-going-monitoring and outcomes-analysis paragraphs, the standing artefact most banks call the **Model Performance Report (MPR)**. The MPR is the periodic document that consolidates, per tiered model, the on-going monitoring metrics, the outcomes-analysis results, any material events (revalidations, exceptions, incidents), and the model's disposition for the coming period. It is produced on a cadence proportionate to the model's tier (monthly for Tier-1, quarterly for Tier-2, annually for Tier-3 in a typical scheme) and is the single artefact that the second-line function reviews and signs.

For AI systems the MPR extends to cover items that SR 11-7's original drafters did not have language for: vendor-side signals from the foundation-model provider (silent updates, deprecations, published incidents), semantic drift measurements on generative outputs, evaluation-set integrity refresh events, and guardrail-classifier performance. The release-assurance methodology owner authors the MPR template for AI systems and threads the release-package into it — every release-gate decision becomes an entry in the next MPR, and every MPR is a re-opening of the release-gate for the systems it covers.

## Worked shape — a credit-decisioning assistant at a mid-sized U.S. bank

Take a concrete system: an LLM-based **credit-decisioning assistant** used by adjudicators at a U.S. bank to summarise borrower documentation and surface anomalies for adverse-action review. It does *not* make the credit decision — an adjudicator does — but its outputs materially shape the adjudicator's attention. It uses a hosted foundation model, a retrieval layer over a proprietary loan-file corpus, and a fine-tuned re-ranker owned by the bank.

Plugged into SR 11-7:

- **Inventory rows**: three — the hosted foundation model (SR 23-4 shape, chapter `02`), the retrieval layer, and the fine-tuned re-ranker. Each has its own risk tier and its own validation status.
- **Risk tier**: the composite system is Tier-1 for MRM purposes because it influences a fair-lending-relevant decision (chapter `06` overlay applies).
- **Effective challenge**: MRM's second-line validation covers each of the three models, plus the *composition* — the emergent behaviour of the pipeline that no single-model validation catches.
- **Development testing (MDD)**: the fine-tuned re-ranker has a classical MDD; the foundation-model MDD is a *card-derived* artefact citing the vendor's system card and the bank's own capability-evaluation results; the retrieval layer's MDD covers embedding choice, index construction, and coverage evaluation.
- **Implementation testing**: change management on the retrieval index, prompt-template versioning under configuration control, and vendor-version pinning discipline for the foundation model.
- **Model use**: intended use is *decision support for adjudicators*, not autonomous decisioning; the human-override design is documented and reviewed under [CFPB adverse-action-notice expectations](https://www.consumerfinance.gov/compliance/circulars/) (chapter `06`).
- **On-going monitoring**: quarterly outcomes analysis against actual adjudication outcomes; monthly semantic-drift monitoring on the summarisation output; vendor-change alerts wired into the release-gate reversal contract.
- **Independent validation**: signed by MRM Validation lead before T3 promotion; revalidation triggered by any material change to the foundation-model version, the retrieval corpus, or the prompt template.
- **Model Performance Report**: monthly, consolidating all four monitoring dimensions plus vendor-side signals, signed by MRM Validation, reviewed by the model-risk committee, and referenced in the next release-gate cycle.

That is the SR-11-7-shaped document set for one AI model — and it is what exercise-01 asks you to author for a system of your own choosing.

## A note on internal-model regulation and AI

For U.S. banks that use models for regulatory-capital purposes (internal-models-approach under the U.S. implementations of Basel-derived rules), an additional layer sits alongside SR 11-7: the model-approval process the primary federal supervisor runs before an internal model can be used for regulatory-capital calculations. AI/ML models in this space are rare at time of writing — the supervisors have been cautious about approving them for capital purposes — but they are not prohibited, and where they are used, the release-gate carries the additional supervisor-approval evidence as an artefact. The EU sibling is the ECB's model-approval process under the CRR/CRD for internal models, covered lightly in chapter `05`. In both jurisdictions, the release-assurance methodology owner treats the supervisor-approval package as a first-class release-package artefact and does not promote the model to the supervised deployment surface until the approval is on file.

## Where this shows up in the rest of the track

- `mod-101` — SR 11-7 is one of the four bodies of literature the release-assurance programme maps to; the effective-challenge convention here is the second-line convention from `mod-101` chapter `01`.
- `mod-102` — the assurance case for a U.S. banking AI system carries an SR-11-7 branch alongside its NIST AI RMF, ISO/IEC 42001, and EU AI Act branches.
- `mod-103` — the release-gate schema's `sector_rule_citation` field points at SR 11-7 paragraphs by section; the criterion tier map cites SR 11-7 tiering as one of the two feeders (deployment tier being the other).
- `mod-104` — the evidence pipeline carries MDD, development-test, implementation-test, model-use, and independent-validation report as artefact types.
- `mod-108` — deployment-tier gating names its mapping to MRM risk tier explicitly.
- `mod-109` — MRM Validation is one of the "independent-review" audiences whose interface `mod-109` covers.
- `mod-110` — on-going monitoring is the SR-11-7 sibling of post-market surveillance; the surveillance cadence is scheduled per MRM tier and per assurance tier.
- `mod-112` — the release-assurance methodology document names its subordination to the bank's model-risk-management policy.

## Summary

- SR 11-7 (Federal Reserve, 2011-04-04) and OCC 2011-12 together define the U.S. banking sector's model risk management shape: an inventory, risk-tiering, effective challenge, development testing, independent validation, on-going monitoring, and a governance chain.
- Effective challenge is operationalised as the **three lines of defence**: business (first), MRM (second), Internal Audit (third). The release-assurance programme sits in the second line for AI systems and is the effective-challenge instrument.
- Every AI system a U.S. bank deploys is a *model* in SR-11-7's sense — often a composition of several models. Inventory, tiering, and validation apply to each.
- The 2011 shape holds up but stresses at four joints: foundation-model reuse (chapter `02` mapping to SR 23-4), prompt-based/agentic surfaces, evaluation-set contamination as a new integrity risk, and on-going monitoring against a moving upstream.
- The release-package artefact set — MDD, development-test report, implementation-test report, model-use section, independent-validation report, on-going-monitoring plan — is the SR-11-7-shaped document set the release-gate consumes and emits.
- Exercise-01 has you author the SR-11-7-shaped document set for one AI model of your choosing, with the four stress-points explicitly addressed.
