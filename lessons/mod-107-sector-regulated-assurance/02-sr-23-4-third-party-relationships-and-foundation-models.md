# SR 23-4, Third-Party Relationships, and Foundation Models

## Motivation

Chapter `01` closed on a joint: SR 11-7's third-party-model paragraph assumes a vendor supplies a per-model validation package, which is exactly what a foundation-model provider does *not* supply. Between 2011 and 2023, the U.S. banking supervisors published a series of updates on third-party risk management, culminating in the [Interagency Guidance on Third-Party Relationships: Risk Management](https://www.federalreserve.gov/newsevents/pressreleases/files/bcreg20230606a1.pdf) issued jointly by the Federal Reserve, OCC, and FDIC on 2023-06-06. The Federal Reserve announced the guidance through [SR 23-4](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm) on the same date, rescinding the older SR 13-19 / CA 13-21 and aligning U.S. banking-agency expectations on third-party risk under a single shape.

For a release-assurance methodology owner in banking, SR 23-4 is the shape that governs **foundation-model providers, hosted-inference vendors, judge-model providers, and evaluation-platform vendors** — every third party whose product participates in a released AI system. It sits alongside SR 11-7 rather than replacing it: SR 11-7 still governs the *model* inside the bank's inventory; SR 23-4 governs the *relationship* the bank has with the vendor supplying that model or supplying capacity around it. In practice the two shapes braid together, and the release-gate has to carry both.

This chapter reads the SR 23-4 lifecycle stages, walks the adaptation to foundation-model providers where the traditional vendor-model validation package does not exist, and then names the concentration-risk and sub-outsourcing hazards specific to the small set of foundation-model providers on which large swathes of the industry now depend. It is background for exercise-01 and exercise-03, not a standalone exercise.

## What SR 23-4 says, in one paragraph per lifecycle stage

The Interagency Guidance is organised as a lifecycle: **planning, due diligence and third-party selection, contract negotiation, on-going monitoring, and termination**, all framed by governance (board and senior management oversight) and by independent reviews. Two ideas cut across the lifecycle: risk-based rigour (higher-risk relationships receive more intensive management at every stage) and end-to-end accountability (the banking organisation remains responsible for its activities regardless of who performs them).

### Planning

**What it says.** Before entering into a third-party relationship, the banking organisation identifies and assesses the potential benefits and risks, aligns the relationship with the strategic plan and risk appetite, and considers whether the activity is *critical* — one whose failure could disrupt operations, cause significant customer harm, or otherwise materially affect the organisation. Planning outputs feed the due-diligence scope.

**Release-assurance implication.** For a foundation-model relationship, the planning stage produces the answer to: is this relationship critical? For most released AI systems at scale, the answer is yes — a hosted-inference-provider outage or a silent model change can immediately affect customer-facing surfaces. That answer sets the rigour for everything downstream, and the release-gate cannot approve a T3/T4 release built on a third-party foundation model whose criticality assessment is missing or contradicts the deployment profile.

### Due diligence and third-party selection

**What it says.** Due diligence covers the third party's strategies and goals, legal and regulatory compliance, financial condition, business experience and qualifications, operational and technology infrastructure, incident-reporting and management, resilience, information security (including cybersecurity), management of information systems, insurance coverage, conflicts of interest, and reliance on subcontractors. Depth is proportionate to criticality.

**Release-assurance implication.** For a foundation-model provider, due diligence produces an *evidence package* that becomes an artefact in the release bundle (mod-104). Its contents differ from a classical vendor package: it includes the provider's **system card** or **model card**, the provider's **deployment-tier or preparedness framework** review, the provider's **incident-response commitments** (SLAs, notification windows, breach-notification triggers), the provider's **security certifications** (ISO/IEC 27001, SOC 2 Type II, FedRAMP where applicable), and — increasingly — the provider's **usage-data commitments** (no-training-on-your-inputs undertakings, data-residency guarantees, evaluation-set-exfiltration protections). Where the provider publishes an [NIST AI RMF Generative AI Profile](https://www.nist.gov/itl/ai-risk-management-framework) alignment or a comparable governance narrative, that document is part of the package too.

### Contract negotiation

**What it says.** Contracts should reflect the nature, scope, and complexity of the activities; specify performance measures, incident-response and reporting expectations, audit and remediation rights, subcontracting terms, data confidentiality and security requirements, business-continuity and disaster-recovery provisions, dispute resolution, and termination and default provisions. Higher-risk relationships require more specific and enforceable terms.

**Release-assurance implication.** For a foundation-model provider, contract terms the release-assurance owner cares about include: **model-version pinning** (can the bank pin to a specific model version, and for how long?), **deprecation notification windows** (how much notice does the bank get before a pinned version is retired?), **silent-update notification** (does the bank get notified of behavioural updates to a nominally-pinned version?), **evaluation-set confidentiality** (does the provider commit that inputs are not used for training or retained for benchmarking?), **incident-notification windows** aligned with the bank's own regulatory notification obligations, and **audit rights** — including any right to audit the provider's own model-risk practices. A contract missing any of these is a release-gate deficiency that has to be dispositioned before T3/T4 promotion.

### On-going monitoring

**What it says.** On-going monitoring covers the third party's performance, compliance, and risk profile throughout the relationship, with escalation of deficiencies. Monitoring intensity aligns with the criticality of the relationship and the third party's risk profile. Documentation of monitoring activities and outcomes is expected.

**Release-assurance implication.** For a foundation-model provider, on-going monitoring extends the post-market surveillance loop (mod-110) with **vendor-side signals**: provider status pages, published model updates, provider incident disclosures, and — where the provider publishes them — evaluation-result changes and safety-report updates. The release-gate reversal contract (mod-103) includes a **vendor-change trigger** that fires when any of these signals crosses a threshold.

### Termination

**What it says.** Termination arrangements — whether at end of contract, for cause, or opportunistic — must be planned in advance, including transition of data, notification of customers, and continuity of any dependent activities. Exit costs and exit-time are part of the risk assessment.

**Release-assurance implication.** For a foundation-model provider, termination planning is where **portability** and **substitutability** are pre-tested. The release-gate for a critical AI system does not approve a system whose foundation-model relationship has no tested exit plan. Where the provider is *the only* provider that offers the required capability at the required tier, the release-package documents this concentration risk and escalates to the risk committee.

### Governance and independent reviews

**What it says.** The board and senior management oversee the third-party risk management framework. Independent reviews — typically Internal Audit or an equivalent second-line function — periodically review the framework, its execution across the relationship lifecycle, and its outputs. Findings feed the aggregate reporting the board receives.

**Release-assurance implication.** The release-assurance methodology owner works with Internal Audit to ensure the release-package artefacts (due-diligence packages, contract summaries, on-going monitoring plans) are structured to be readable in an Internal Audit workpaper. Where Internal Audit finds gaps in the release-assurance treatment of a third-party AI arrangement, the finding lands in the release-assurance programme's own management-review agenda (`mod-112`).

## Where foundation-model providers stress the SR 23-4 shape

SR 23-4 is a more modern and more flexibly-written guidance than SR 11-7, but it too was drafted with a broader vendor population in mind than the small oligopoly of frontier-model providers that dominates the current market. Three stress points matter for the release-assurance owner.

### The vendor-supplied validation package does not exist in the classical shape

A traditional vendor model comes with a validation package a bank's MRM can review: model description, training data description, test results on the vendor's own benchmarks, and — often — a client-executable validation harness. Foundation-model providers do not supply this. They supply a system card, a set of published benchmark results, and — for their most capable models — a safety report and a deployment-tier framework. These are cards, not validation packages, and they discharge different obligations. The release-assurance owner has to write down explicitly *what the vendor's cards discharge and what still requires internal validation*, because the bank cannot outsource the SR-11-7 second-line effective challenge to a card.

### Evaluation-set exfiltration risk

Sending a proprietary evaluation set to a hosted-inference API is, without contractual and technical protection, an exfiltration event: the evaluation set may be logged, retained, used for provider-side quality analysis, or — worst case — folded into the next training corpus. This class of risk was not contemplated in SR 23-4's data-confidentiality paragraph. The mitigation is contractual (no-training and no-retention terms), technical (private endpoints, dedicated capacity), and procedural (evaluation-set canary strings, benchmark-refresh cadence). The release-assurance owner writes the policy that requires the mitigation; the evidence pipeline (mod-104) discharges it.

### Concentration and sub-outsourcing

At the time of writing, a handful of foundation-model providers underpin a very large share of enterprise AI. When a bank runs a critical AI system on one such provider, and dozens of other banks do too, the failure of that provider becomes a systemic event, and the individual bank's SR-23-4 concentration-risk assessment has to acknowledge that its exit plans are only as good as the sector's ability to absorb a simultaneous migration. Sub-outsourcing compounds this: many foundation-model providers themselves depend on a small set of cloud infrastructure providers, so the "sub-outsourced" leg of the arrangement introduces its own concentration risk that the SR-23-4 subcontracting paragraph asks the bank to trace and to disposition. `mod-104` chapter `04` covers this concentration mapping as an evidence artefact; DORA (chapter `04` of this module) treats the same phenomenon in the EU financial-sector context and provides the stronger statutory hook.

## Worked shape — foundation-model provider as an ICT third-party arrangement

Take the same credit-decisioning assistant from chapter `01`. Its foundation-model provider is a hosted-inference vendor. Plugged into SR 23-4:

- **Planning**: relationship is classified *critical* because the assistant participates in an adverse-action-relevant workflow; T3/T4 release requires a critical-relationship due-diligence package.
- **Due diligence package**: system card and safety report for the pinned model version; provider's ISO/IEC 27001 and SOC 2 Type II reports; provider's deployment-tier or preparedness framework document; provider's incident-response commitments; provider's usage-data commitments.
- **Contract terms**: model-version pin with 12-month deprecation notice; no-training / no-retention commitment for API inputs; incident-notification within 72 hours aligned with the bank's own supervisory notification window; right to audit provider's model-risk practices at minimum annually; termination-for-cause on material silent-update failure.
- **On-going monitoring**: subscription to provider status page and safety-report updates; monthly review of provider announcements; vendor-change trigger wired into the release-gate reversal contract.
- **Termination**: two alternative providers pre-tested with a fallback-migration runbook; exit RTO documented; concentration-risk memo naming the residual dependence on a small provider set.

The release-package artefact bundle carries the due-diligence package, the executed contract (or contract-summary memo for the release-gate), the on-going monitoring plan, and the termination plan. Together with the SR-11-7-shaped model documentation from chapter `01`, this is the full sector-shaped evidence set for a U.S. banking AI system with a hosted foundation-model dependency.

## Contract-clause library — the seven items to fight for

Contract negotiation with a large foundation-model provider is asymmetric: the provider has a boilerplate MSA and a limited appetite for bespoke terms. Where the release-assurance owner works with procurement and legal to negotiate a contract that supports SR-23-4-shaped due diligence, seven items are typically load-bearing and worth negotiating hard on. Missing any one of them creates a release-package gap that has to be dispositioned by another mechanism.

1. **Model-version pin.** The customer can pin to a specific model identifier and version. The provider commits to make that version available for a specified minimum period (12 months is a common floor for critical arrangements).
2. **Silent-update definition and notification.** Any change to a nominally-pinned version's behaviour — whether via a supporting-model swap, a safety-classifier update, or a serving-stack change — is a *silent update*, and the customer receives written notification within a stated window (72 hours is a common target).
3. **Deprecation notice window.** When a pinned version is scheduled for retirement, the customer receives notice at least N months before the effective date, where N is proportionate to the customer's migration complexity.
4. **No-training / no-retention commitment.** Customer inputs, prompts, and outputs are not used to train or fine-tune the provider's models, and are retained only as necessary for operational service delivery (typically with a documented retention window).
5. **Incident notification aligned to the customer's regulatory obligations.** Provider-side incidents that could affect customer service are notified within a window compatible with the customer's own supervisory-notification windows (which for DORA-in-scope customers can be tight — see chapter `04`).
6. **Audit rights, direct or pooled.** Either a direct audit right the customer can exercise, or a pooled-audit mechanism where an independent auditor performs audits on behalf of a defined customer group.
7. **Termination and exit assistance.** Termination-for-convenience, termination-for-cause triggers, and a documented exit-assistance package the provider will supply on termination (documentation, transitional access, data return where applicable).

Where any item cannot be negotiated on the master contract, the release-assurance owner records the gap and dispositions it: either the arrangement is downgraded from *critical* (with the release-package's criticality determination revised), or the gap is accepted as a residual with the risk-committee-approved rationale on file.

## Judge-model providers and evaluation-platform vendors

SR 23-4 does not care whether a third party supplies inference, evaluation, or something else — its lifecycle applies to any critical relationship. Two adjacent categories often get missed:

- **Judge-model providers.** If the release-assurance evidence includes LLM-judge outputs, the judge-model provider is a third party whose failure mode (silent model change) can invalidate the evidence that the release-gate depends on. The release-package documents the judge-model provider under SR 23-4, pins the judge-model version, and treats a judge-model change as an evidence-refresh trigger.
- **Evaluation-platform vendors** (e.g. hosted eval platforms, red-team-as-a-service providers). These vendors sit between the peer eval engineer and the release-gate; their availability, integrity, and data-handling are covered under SR 23-4, and their outputs enter the evidence pipeline (mod-104) with the vendor identifier as part of the artefact metadata.

Both categories interface with `mod-109` (third-party evaluator and auditor interface); the SR-23-4 arrangement is what makes the interface durable.

## The interaction between SR 23-4 and internal MRM

SR 23-4 does not replace SR 11-7 for the *model* inside a third-party arrangement — it wraps the *relationship* around the model, and the SR-11-7 shape from chapter `01` still applies to the model itself. Practically, this means the release-package for a foundation-model-backed AI system carries *two* artefact sets that reference each other:

- The **SR-11-7 model artefacts** (Model Description Document, development-test report, implementation-test report, model-use section, independent-validation report, on-going-monitoring plan, Model Performance Report) — for each model in the composition, including the foundation model where its performance is separately measurable inside the bank's environment.
- The **SR-23-4 relationship artefacts** (due-diligence package, contract summary, on-going monitoring plan for the relationship, termination plan, concentration-risk memo) — for each third-party arrangement.

The two artefact sets have overlaps but different signers, different review cadences, and different escalation paths. The release-assurance methodology owner maintains the crosswalk that shows, for each artefact, which review answers which sector obligation. Without the crosswalk, a supervisor asking "who signed off on the foundation model?" gets an ambiguous answer, and the release-package looks incomplete.

## What the SR 23-4 register actually looks like in practice

Banks running under SR 23-4 typically maintain a register of third-party arrangements as a structured artefact — a database or a well-formed spreadsheet — that supervisors can request in one hop. For each arrangement the register carries at minimum: the vendor identifier, the arrangement identifier, the supporting business function, the criticality classification, the risk tier, the on-going monitoring cadence, the last due-diligence refresh date, the contract-renewal date, and the responsible business owner. AI arrangements sit alongside other technology arrangements in the register, distinguished by an AI-arrangement flag or an AI-arrangement category.

The release-assurance methodology owner's programme feeds the register: every release-gate approval that involves a third-party AI arrangement produces a register entry or an updated register entry, and the release-package pins the register entry's identifier as one of its outputs. This is the tightest coupling between the release-assurance programme and the bank-wide third-party function — the two functions share a register and share a cadence for reviewing it.

## Where this shows up in the rest of the track

- `mod-101` — GOVERN-6 (third-party governance) is the NIST AI RMF category that SR 23-4 discharges in the U.S. banking sector.
- `mod-103` — the release-gate reversal contract includes a vendor-change trigger; the criterion set includes a "vendor-package-current" hard-gate for critical relationships.
- `mod-104` — the evidence pipeline carries vendor artefacts (system cards, contract summaries, monitoring reports) as first-class artefact types.
- `mod-105` — the system card for the released AI system names the foundation-model dependency and the pinned version.
- `mod-108` — deployment-tier gating uses the vendor-package status as one of its tier-gate inputs.
- `mod-109` — the third-party evaluator interface uses the SR-23-4 due-diligence shape as its template for evaluator onboarding.
- `mod-110` — post-market surveillance includes vendor-side signal collection as a scheduled activity.
- `mod-111` — GPAI systemic-risk assurance for a provider maps to the *provider-side* of an SR-23-4 arrangement viewed from the deployer.

## Summary

- The Interagency Guidance on Third-Party Relationships (2023-06-06), announced by SR 23-4, is the U.S. banking-agency shape for governing third-party relationships across their lifecycle: planning, due diligence, contract negotiation, on-going monitoring, and termination.
- SR 23-4 sits *alongside* SR 11-7 for AI systems: SR 11-7 governs the model in the inventory; SR 23-4 governs the relationship with the vendor supplying that model or supplying capacity around it.
- Foundation-model providers, hosted-inference vendors, judge-model providers, and evaluation-platform vendors all fall under SR 23-4 when their arrangement is critical.
- Three stress points with foundation-model providers: the vendor-supplied validation package does not exist in the classical shape (cards, not validation packages); evaluation-set exfiltration is a new class of confidentiality risk; and concentration plus sub-outsourcing hazards concentrate at a handful of providers and their cloud sub-outsourcees.
- The release-package carries a due-diligence package, a contract summary, an on-going monitoring plan, and a termination plan for each critical third-party AI arrangement. Chapter `04` (DORA) is the EU statutory sibling of this shape.
- No exercise is direct; this chapter is prerequisite background for exercise-01 (SR 11-7 adaptation) and exercise-03 (DORA ICT third-party clauses).
