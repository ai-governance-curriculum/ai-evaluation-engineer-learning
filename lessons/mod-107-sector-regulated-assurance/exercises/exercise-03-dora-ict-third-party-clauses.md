# exercise-03: DORA Article 30(3) Clauses for a Foundation-Model Arrangement

**Estimated effort:** 3 hours

## Objective

For one AI system that participates in a critical or important function of an EU financial-sector entity, produce the **DORA ICT-third-party artefact set** for one foundation-model arrangement supporting that system: a pre-contractual assessment, a register-of-information entry, a full Article 30(3) contractual-clause set, a sub-outsourcing map, a concentration-risk memo, and an exit-and-portability plan. The exercise is authoring, not solving — the artefact set is what the release-package for a DORA-in-scope AI system carries when it lands on the second-line reviewer's desk.

The centre of gravity is the Article 30(3) clause set. Article 30 prescribes the *minimum* contractual content for any ICT third-party arrangement; Article 30(3) adds the *extended* set required when the arrangement supports a critical or important function. Foundation-model providers are ICT third-party service providers, and — for critical-function AI systems — the extended set applies. Most of the exercise is drafting those clauses at a level a real contract lawyer could refine into executable language.

## Prerequisites

- Chapter [`04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md`](../04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md) — the DORA pillars, Article 30(3), the sub-outsourcing and concentration hazards, the RTS/ITS pointers.
- Chapter [`02-sr-23-4-third-party-relationships-and-foundation-models.md`](../02-sr-23-4-third-party-relationships-and-foundation-models.md) — the seven-item contract-clause fight list for a foundation-model provider is the U.S. sibling; the DORA clause set is a stronger, more statutory version of the same battle.
- [Regulation (EU) 2022/2554 — DORA](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) — read Articles 28, 29, 30, and 31 directly. They are the load-bearing articles for this exercise.
- [Delegated Regulation (EU) 2024/1502](https://eur-lex.europa.eu/eli/reg_del/2024/1502/oj) — the criteria for designation of critical ICT third-party service providers, if the arrangement is with a candidate for designation.
- [The ESAs' DORA landing page](https://www.esma.europa.eu/esmas-activities/digital-finance-and-innovation/digital-operational-resilience-act-dora) — for the current state of the ITS on the register of information and the RTS on contractual policies.
- Familiarity with the peer-role registry for the AI Evaluation Engineer track (`ai-risk-engineer`, `model-evaluation-engineer`, `ai-governance-analyst`, `ai-infra-security`, `platform-eng`, `product`, `legal`, procurement, CRO / risk committee).

## Problem statement

Invent the financial entity, the AI system it deploys, the critical function that system participates in, and the foundation-model arrangement that supports the system. Common patterns worth considering (pick one, or invent your own):

- **Retail bank — underwriting-assistance AI on a hosted foundation model.** Consumer-credit underwriting adjudication uses an LLM-based assistant to surface risk factors from unstructured broker or borrower documentation.
- **EU insurer — commercial-lines underwriting AI on a hosted foundation model.** The scenario from chapter `04` — the underwriting-assistance system for commercial-lines submissions, with a non-EU foundation-model provider and an EU-based cloud inference provider.
- **Payment institution — transaction-monitoring AI.** AI-based anomaly detection over payment flows; the AI participates in the entity's fraud-prevention critical function.
- **Investment firm — client-suitability-assessment AI.** MiFID-II-facing robo-advisor from chapter `05`'s worked shape; the AI participates in the investment-advice critical function.
- **CCP or trading venue — market-abuse-surveillance AI.** AI-based market-abuse anomaly detection over trading flows; the AI participates in a market-integrity critical function.
- **Asset manager — investment-research AI.** LLM-based research summariser used by portfolio managers as decision support; the AI participates in the investment-decision critical function.

Pin the scenario before authoring:

- The financial entity, its regulatory status, and its supervisory authority (which national competent authority and which ESA for DORA).
- The critical or important function the AI participates in.
- The foundation-model provider — jurisdiction, hosting model (public API, dedicated capacity, on-prem), and whether the provider is likely to be designated a *critical* ICT third-party service provider under DORA Article 31.
- The composition of the AI system (foundation model, retrieval components, fine-tuning, guardrails) and which components sit inside the entity versus at the provider.
- Any sub-outsourcing chain — the foundation-model provider's own cloud dependency in particular.

If the scenario is a natural fit for the credit-decisioning assistant from exercise `01`, feel free to reuse it and add the DORA layer; if not, invent afresh — the SR-11-7 side does not need to reappear here.

## Requirements

Produce seven artefacts in a single directory.

### 1. `scenario-scoping-brief.md`

A one-page brief that fixes:

- **Financial entity.** Named entity, regulatory status (bank, insurer, investment firm, CCP, etc.), primary national competent authority, primary ESA relationship under DORA.
- **AI system and its critical function.** The system's intended purpose and the specific critical or important function it participates in. The link between the AI system's failure and the function's disruption is stated concretely.
- **Foundation-model provider.** Named provider (real or hypothetical), jurisdiction, hosting mode, likely DORA Article 31 designation status (designated / candidate / clearly not designated / unknown).
- **Composition.** What runs at the provider, what runs at the entity, what runs at any other third party.
- **Sub-outsourcing chain.** Explicit list of the provider's own material sub-outsourcees relevant to the arrangement (typically at minimum the hyperscale cloud beneath the provider).
- **Criticality classification.** The entity's determination that the arrangement supports a critical or important function under DORA — with reasoning. This is the trigger for Article 30(3).
- **Concentration snapshot.** A one-paragraph read of the entity's overall foundation-model footprint and the concentration hazard the current arrangement contributes to.

### 2. `pre-contractual-assessment.md`

The Article 29 pre-contractual assessment. Cover:

- **Confirmation that the arrangement supports a critical or important function.** With reasoning.
- **Assessment of the third party's suitability.** Financial condition, business experience, operational and technology infrastructure, information security posture, incident-management capability, business-continuity capability, and reliance on subcontractors. For a foundation-model provider, this is where card-derived evidence sits — the provider's system card, preparedness / responsible-scaling framework, ISO/IEC 27001 status, SOC 2 status, published safety report.
- **Sub-outsourcing chain analysis.** Named material sub-outsourcees; the risks each introduces; the entity's plan for managing those risks (including how contractual protections cascade to sub-outsourcees).
- **Concentration-risk analysis.** Contribution of the arrangement to concentration risk at the entity level (across its foundation-model footprint) and — where relevant — at the sector level (where many downstream entities depend on the same provider).
- **Alternative-provider analysis.** Whether alternative providers exist that could deliver equivalent capability at the required tier; the substitutability assessment; the exit realism (which the exit plan artefact 7 develops).
- **Recommendation.** Enter into the arrangement / enter with conditions / do not enter. The reasoning that supports the recommendation. The sign-offs required (typically CRO, CTO or CIO, business owner, and — for the strongest arrangements — the management body).

### 3. `register-of-information-entry.md`

The Article 28(3) register of information entry for the arrangement. The ITS on the register of information specifies the exact schema; for this exercise, produce a YAML entry that covers at minimum:

- **Arrangement identifier.** Unique within the entity's register.
- **Third party identifier.** LEI where available; provider's legal name; jurisdiction of incorporation.
- **Contract identifier and effective / termination dates.** Which contract instantiates the arrangement.
- **ICT services description.** A structured description of the services (using the ITS's ICT-services taxonomy where the current ITS specifies one — cite `<!-- needs-research: … -->` where you need to check the current ITS categorisation).
- **Function supported.** The critical or important function the arrangement supports (with reference to the entity's functions inventory).
- **Criticality of the arrangement.** Categorical (supports-critical-or-important-function / other) with the entity's own reasoning.
- **Sub-outsourcing.** Named material sub-outsourcees with their own identifiers, jurisdictions, and services.
- **Data-processing and transfers.** Whether the arrangement processes personal data; where data are stored and processed; cross-border transfer mechanisms if applicable.
- **Governance and monitoring.** Business owner, contract owner, monitoring cadence, last due-diligence refresh date, next due-diligence refresh date.
- **Cost and criticality metrics.** Where the ITS requires financial or utilisation metrics, populate placeholders and note `<!-- needs-research: … -->` for the ITS-specific field list.

Note at the top of the file that a real programme's register-of-information entry conforms to the ITS's XBRL or CSV schema; the YAML in this exercise is a modelling proxy the release-package would round-trip into the compliant format.

### 4. `article-30-3-contractual-clauses.md`

The centre of gravity. Author the Article 30(3) contractual clause set for the arrangement, item by item. Article 30(3) adds an extended list of mandatory contractual provisions on top of Article 30(2). At minimum, cover:

- **Full service-level descriptions with quantitative performance targets.** For a foundation-model arrangement, this includes capability performance (not just uptime): throughput / latency SLA at named percentiles; behaviour-stability commitment for a pinned model version; response-quality commitment where quantifiable.
- **Notification of material changes.** Definition of *material change* (silent updates, deprecations, safety-classifier changes, serving-stack changes with behaviour impact); notification window; medium.
- **Contract termination rights and transition periods.** Termination for convenience, for cause, and on regulatory instruction; the transition period (realistic for AI-capability replacement, not boilerplate); exit-assistance obligations.
- **Data-protection and information-security obligations.** Data storage location; access control; encryption at rest and in transit; incident notification aligned to the entity's DORA reporting; no-training / no-retention commitment for entity inputs where negotiable; audit rights over the provider's information security.
- **Incident reporting obligations aligned to the entity's DORA reporting.** Provider-side incidents affecting the arrangement notified within a window compatible with the entity's own DORA reporting windows; content of the notification; escalation.
- **Business-continuity and disaster-recovery obligations.** RTO / RPO commitments; testing cadence; the provider's own resilience testing; scenarios that trigger provider-side BCDR.
- **Cooperation with competent authorities.** The provider's obligation to cooperate with the entity's supervisor and — where the provider is designated critical under Article 31 — with the Lead Overseer.
- **Audit rights (direct or pooled).** The entity's right to audit the provider directly; where a direct right is impractical, the pooled-audit mechanism; the audit scope (information security, ICT-risk-management practices, third-party arrangements at the provider); the cooperation-with-audit commitment.
- **Sub-outsourcing terms.** Approval or notification for sub-outsourcing changes; cascading of DORA-compliant contractual protections to sub-outsourcees; the entity's rights on sub-outsourcing-change refusal.
- **Governing law and jurisdiction.** Governing law; jurisdiction for disputes; recognition of the entity's supervisory jurisdiction.

For each clause, write:

- **Clause title.**
- **Rationale.** One-sentence justification citing the Article 30(3) requirement.
- **Draft text.** A short paragraph of contract-shaped language — precise enough that a real contract lawyer could refine it, not so long that the drafting distracts from the release-assurance perspective.
- **Fallback position.** What the release-assurance owner can accept if the provider will not agree to the primary draft. Some clauses may have no acceptable fallback ("no-training with a documented retention window is a hard requirement"); some may have graduated fallbacks ("12-month deprecation notice preferred; 6-month acceptable with mitigation; less than 6-month escalates to risk committee").
- **Verification.** How the release-package will verify the clause is executed and honoured over the arrangement lifetime — the audit or monitoring the on-going-monitoring plan carries.

### 5. `sub-outsourcing-map.md`

For the arrangement, a two-to-three-tier map:

- **Tier 0.** The entity itself and its own DORA-in-scope functions.
- **Tier 1.** The direct provider (the foundation-model provider). Named services, criticality of each to the arrangement.
- **Tier 2.** The provider's own material sub-outsourcees. Named services, jurisdictions, and known concentration or resilience hazards.
- **Tier 3+** if warranted (rare in practice for one arrangement, but possible).

For each edge (each dependency between tiers), note:

- The Article 29(2) and Article 30 protections applied.
- The failure-mode analysis — what happens to the arrangement if the sub-outsourcee fails.
- The mitigations — active mitigations (alternate providers, capacity elsewhere), passive mitigations (contract remedies).

The map is often best drawn — for this exercise, ASCII art, a mermaid diagram, or a simple table is fine.

### 6. `concentration-risk-memo.md`

The concentration-risk memo is the risk-committee-visible synthesis of concentration hazards for the arrangement. Cover:

- **Entity-level concentration.** How much of the entity's overall foundation-model footprint runs on this provider. How much of the entity's critical-function AI depends on this provider.
- **Sector-level concentration.** Where publicly known or reasonably estimable, how much of the sector depends on the same provider. The systemic hazard if the provider fails simultaneously across many entities.
- **Cloud-tier concentration.** The provider's own cloud dependency. Where multiple foundation-model providers share the same underlying hyperscale cloud, the cloud tier is where correlated failure lands.
- **Mitigation posture.** What the entity does now to mitigate concentration (alternate-provider readiness, capacity ceilings, tier-by-tier resilience testing).
- **Residual risk.** What the mitigations do not cover. The risk-committee decision to accept, mitigate further, or restrict the arrangement.

The memo is signed by the CRO and — for the largest arrangements — reviewed by the management body.

### 7. `exit-and-portability-plan.md`

The termination plan for the arrangement. Cover:

- **Exit triggers.** End of contract; termination for cause; opportunistic exit; regulatory instruction (including supervisory instructions under DORA Article 42 for critical designated providers).
- **Substitution options.** Named alternative providers (or a plausible substitution-analysis if no named alternative is realistic today); the capability gap analysis; the migration effort estimate.
- **Transition procedure.** Data-return procedure; access-transition procedure; documentation transition; customer-facing communication where applicable.
- **Transition timing.** Realistic RTO for the exit; how it fits inside the DORA impact-tolerance for the critical function; how the release-gate would authorise a planned or emergency exit.
- **Exit testing.** How the exit plan is tested — at what cadence, with what scope, with what remediation for defects found. Untested exit plans are widely acknowledged as the weakest link in third-party resilience; DORA's Article 30(3) exit obligations tighten the expectation.
- **Concentration-risk implications of exit.** If exit is triggered under stressed conditions where many entities exit simultaneously, the availability of alternative providers may be constrained. Address this concretely.

## Starter guidance

- **Fix scoping first.** Article 30(3) triggers only for critical-function arrangements. Get the criticality determination right on the scoping brief before drafting a single clause.
- **Article 30(3) is a *floor*, not a ceiling.** The Article specifies mandatory content; nothing prevents the entity from negotiating stronger terms. For a foundation-model arrangement, stronger terms on notification and exit are often worth the negotiation effort.
- **Fallback positions are load-bearing.** Article 30(3) is negotiated against a provider whose boilerplate does not natively include the extended clause set. The release-assurance owner works with procurement to identify what is negotiable, what is boilerplate-adjacent-and-graduatable, and what is a hard requirement. Fallbacks let the negotiation land somewhere real.
- **Silent updates are the defining foundation-model risk.** A pinned-version-with-silent-updates is not a real pin. Draft the material-change clause tightly and negotiate the notification window aggressively.
- **No-training / no-retention is negotiable at scale.** Large customers routinely get these terms; smaller customers may not. Where the customer's leverage is limited, the release-assurance owner escalates the concentration hazard and — where necessary — restricts the arrangement's use to lower-tier deployment surfaces where evaluation-set exfiltration is less consequential.
- **Audit rights are asymmetric.** Direct audit rights on a very large provider are rarely honoured in practice; pooled audits or third-party assurance reports (SOC 2 Type II, ISO 27001) fill the gap. Draft both options in the clause so the entity has a functional route to assurance.
- **Sub-outsourcing cascades.** DORA does not accept "we outsource to X; X handles its own subcontractors, not our problem." Article 29 and 30 protections cascade. The sub-outsourcing map is not decorative.
- **Exit realism matters.** Exit plans that assume seamless capability substitution are fiction. Real substitution takes months, involves re-fine-tuning, re-evaluation, and re-integration, and is bounded by the alternate provider's capacity. The exit plan states realism, not aspiration.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** Where you would need the current state of the ITS on the register of information, the current list of designated critical providers, or the current RTS on contractual policies, mark it rather than guessing. Level-2 DORA content moves.
- **The release-assurance owner is not the contract negotiator.** Procurement and legal own contract negotiation. The release-assurance owner authors the clause specifications, tracks negotiated outcomes against them, and — where negotiation fails to reach the minimum — refuses the arrangement's promotion to critical-function status.

## Acceptance criteria

You have succeeded if:

- `scenario-scoping-brief.md` fixes the seven scoping decisions with reasoning. The criticality classification for the arrangement (Article 30(3) trigger) is stated with reasoning.
- `pre-contractual-assessment.md` addresses all elements Article 29 requires, including the sub-outsourcing analysis and the concentration-risk analysis. The recommendation and required sign-offs are stated.
- `register-of-information-entry.md` is a YAML entry covering the required fields (arrangement identifier, third-party identifier, contract details, ICT services description, function supported, criticality classification, sub-outsourcing, data processing, governance and monitoring, cost / utilisation metrics). Fields where the ITS specifies a taxonomy not verified are marked `<!-- needs-research: … -->`.
- `article-30-3-contractual-clauses.md` covers each Article 30(3) element listed in the requirements. Every clause has a rationale, draft text, at least one fallback position (or an explicit "no acceptable fallback" note), and a verification approach.
- `sub-outsourcing-map.md` shows two to three tiers with the direct provider and its material sub-outsourcees. Failure-mode analysis is present per edge.
- `concentration-risk-memo.md` addresses entity-level, sector-level, and cloud-tier concentration with a mitigation posture and a residual-risk statement. Signer is named.
- `exit-and-portability-plan.md` names exit triggers, substitution options, transition procedure, timing (realistic), exit testing cadence, and concentration-under-stress implications.
- Every place a fact would need to be verified against DORA Level-2 content (RTS, ITS, current designated-critical-provider list) is marked `<!-- needs-research: … -->` rather than guessed.
- The artefact set is *consistent* — the criticality classification on the scoping brief matches the pre-contractual assessment, matches the register entry's criticality field, matches the Article 30(3)-applies decision, matches the concentration-risk memo's tier analysis.
- A reviewer walking the artefact set can see, for the arrangement, why it is in scope of DORA Article 30(3), what the extended clauses say, what the sub-outsourcing chain and concentration hazards are, and how the entity would exit if it had to.

## Stretch goals

- **Draft the resilience-testing plan for the arrangement.** In `resilience-testing-plan.md`, sketch the DORA Article 24-onward testing programme for the AI system supported by the arrangement — adversarial-input testing, prompt-injection testing, retrieval-corruption testing, end-to-end failure-injection simulating provider outage. Where the entity is significant enough to be in scope of Article 26 threat-led penetration testing (TLPT), name how the TLPT scope covers the AI system.
- **Author the incident-classification matrix.** In `incident-classification-matrix.md`, pre-map AI-specific incident types (silent-update behavioural change, hallucination cascade, evaluation-set exfiltration, judge-model drift, retrieval-corpus poisoning) against DORA Article 18 major-incident classification criteria. This is what the on-call reads when they need to know whether to fire the DORA-major process.
- **Draft the EU AI Act interaction memo.** In `dora-eu-ai-act-interaction-memo.md`, cover the interaction between DORA obligations and EU AI Act obligations for the same system — where they share artefacts, where they diverge, and where the release-package writes to the union. Cross-reference `mod-106` for the full cross-jurisdictional map.
- **Draft the Lead Overseer engagement posture.** If the foundation-model provider is designated (or plausibly to be designated) critical under DORA Article 31, sketch in `lead-overseer-engagement-posture.md` the entity's expected posture toward the Lead Overseer's oversight activity — how the entity would respond to a Lead Overseer information request, a joint on-site inspection, or a recommendation issued to the provider that affects the arrangement.
- **Add an evaluation-platform vendor arrangement.** Repeat a light version of the artefact set for a *second* ICT third-party arrangement — an evaluation-platform vendor that supplies release-package evidence (judge-model outputs, hosted red-team infrastructure). Chapter `04` names both categories as in-scope; the second arrangement's clause set is often overlooked and the exercise is instructive.
- **Draft the pooled-audit mechanism.** Where direct audit rights are impractical, draft in `pooled-audit-mechanism.md` the pooled-audit governance — the auditor selection, the audit scope, the report-distribution regime, the participating entities, the funding model. The Financial-services industry has begun to formalise pooled-audit mechanisms for hyperscale cloud providers; the equivalent for foundation-model providers is nascent.
