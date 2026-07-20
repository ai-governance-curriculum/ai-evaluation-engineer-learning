# DORA and ICT Third-Party Risk When AI Carries a Critical Function

## Motivation

Chapters `01` and `02` covered the U.S. banking sector's shape (SR 11-7, SR 23-4). For a release-assurance methodology owner working on any AI system that participates in a critical function of an EU financial-sector entity — a bank, an investment firm, an insurer, a pension fund, a trading venue, a CCP, a payment institution, an e-money institution, a fund manager — the anchor is different. It is the [**Digital Operational Resilience Act (DORA, Regulation (EU) 2022/2554)**](https://eur-lex.europa.eu/eli/reg/2022/2554/oj), which entered into force on 2023-01-16 and became applicable on 2025-01-17.

DORA is a *Regulation* — directly applicable in EU Member States without national transposition — that harmonises the operational-resilience shape across the EU financial sector. It layers on top of sector-specific regulation (CRR/CRD, MiFID, Solvency II, MiFIR, PSD2, and their siblings) rather than replacing any of them. For AI systems, DORA matters for one specific reason: when an AI system participates in the delivery of a critical or important function of a financial-sector entity, the AI system and its supporting arrangements fall inside DORA's **ICT risk management** and **ICT third-party risk management** obligations. That drags foundation-model providers, hosted-inference vendors, judge-model providers, evaluation-platform vendors, and cloud inference providers into scope as ICT third-party service providers under a legally binding regime — one significantly stronger than the equivalent U.S. guidance from chapter `02`.

The [European Supervisory Authorities (ESAs) — EBA, EIOPA, ESMA — jointly maintain the DORA implementation](https://www.esma.europa.eu/esmas-activities/digital-finance-and-innovation/digital-operational-resilience-act-dora) through Regulatory Technical Standards (RTS) and Implementing Technical Standards (ITS) that specify the details. Where DORA's Level-1 text is written at a regulation's altitude, the RTS/ITS give the release-assurance methodology owner the specific artefact and cadence expectations. This chapter reads DORA at the article level for the parts that shape a release-gate, and then walks the adaptation for AI-carrying critical functions. Exercise-03 asks you to author the DORA ICT-third-party contractual clauses for a foundation-model arrangement.

## What DORA says, at the pillar level

DORA is organised into five pillars: **ICT risk management**, **ICT-related incident management, classification, and reporting**, **digital operational resilience testing**, **management of ICT third-party risk**, and **information and intelligence sharing**. Each has its own article set and each has RTS/ITS filling out the specifics. For the release-assurance owner, all five pillars have release-gate implications; three pillars — ICT risk management, ICT third-party risk, and digital operational resilience testing — carry most of the weight.

### Pillar 1 — ICT risk management (Articles 5–16)

**What it says.** Financial entities must have an ICT risk management framework, approved by the management body, that identifies and documents ICT-supported business functions, information assets and ICT assets, ICT risks, and the impact tolerances for disruptions. The framework covers protection and prevention, detection, response and recovery, learning and evolving, and communication. It is reviewed at least annually and after any major ICT-related incident.

**Release-assurance implication.** An AI system that participates in a critical function is an ICT asset supporting that function. The release-gate consumes the entity's ICT risk management framework as *context* — the release cannot approve a system whose criticality classification and impact tolerances have not been recorded. It emits evidence into the ICT risk-management inventory (this is the DORA sibling of SR 11-7's model inventory: both are living registers of the assets in scope). Article 16 for smaller entities is a lighter regime; the release-assurance owner reads the entity's proportionality determination and calibrates the release-package accordingly.

### Pillar 2 — ICT-related incident management (Articles 17–23)

**What it says.** Financial entities must have an ICT-related incident management process that logs, classifies, and responds to incidents. Incidents crossing the **major** threshold (per the classification criteria in Article 18 and specified further in RTS) are reported to the competent authority within specified timelines using specified templates. Voluntary reporting of significant cyber threats is enabled.

**Release-assurance implication.** The release-gate includes an **incident-response readiness** criterion for any AI system in scope. The release-package attaches the incident classification methodology (how does the entity decide an AI-caused disruption is *major*?), the notification-window commitments, and the connection to `mod-110`'s post-market surveillance. For AI-specific failure modes — silent foundation-model updates that trigger downstream anomalies, hallucination cascades that surface as customer complaints — the incident classification needs to be pre-mapped so the on-call knows whether to fire the DORA-major process.

### Pillar 3 — Digital operational resilience testing (Articles 24–27)

**What it says.** Entities perform a testing programme proportionate to their size, business, and risk profile, covering vulnerability assessments, source-code reviews, penetration tests, and — for entities identified as significant — **threat-led penetration testing (TLPT)** conducted at least every three years, aligned with the TIBER-EU framework. Testing scope covers ICT systems supporting critical or important functions and their ICT third-party service providers.

**Release-assurance implication.** For an AI-carrying critical function, the resilience-testing programme has to include the AI system's failure modes: adversarial-input testing, prompt-injection testing against the deployed surface, data-integrity testing on the retrieval or feature-store layer, and end-to-end failure-injection exercises that simulate provider outages. The release-gate consumes the testing outputs as evidence and requires the testing scope declaration to name AI-specific vectors explicitly. `mod-108` (deployment-tier gating) and `mod-110` (post-market surveillance) both integrate with the DORA testing cadence.

### Pillar 4 — Management of ICT third-party risk (Articles 28–44)

**What it says.** This is the pillar that most reshapes AI vendor relationships. Its core elements:

- **Strategy on ICT third-party risk** (Article 28) — the management body approves a strategy that includes a policy for use of ICT services supporting critical or important functions and considers concentration risk.
- **Register of information** (Article 28(3)) — entities maintain and update a register of all contractual arrangements on the use of ICT services provided by ICT third-party service providers, with a specific data schema (specified in ITS). The register distinguishes arrangements supporting critical or important functions from other arrangements.
- **Pre-contractual assessment** (Article 29) — before entering into a contractual arrangement for ICT services supporting a critical or important function, the entity assesses whether the arrangement covers such a function, considers the sub-outsourcing chain, and assesses concentration risk.
- **Contractual provisions** (Article 30) — DORA prescribes a *minimum content* for contractual arrangements. For arrangements supporting critical or important functions, Article 30(3) adds an *extended* list of mandatory contractual provisions, including full service-level descriptions, service quality levels and quantitative and qualitative performance targets, notification obligations for material changes, incident-reporting obligations aligned to the entity's own DORA reporting, cooperation with competent authorities, exit strategies with transition periods, and audit rights.
- **Sub-outsourcing** (across Article 30 and Article 29) — sub-outsourcing arrangements that are material must be named, subject to the same contractual protections at each tier, and factored into the concentration analysis.
- **Oversight of critical ICT third-party service providers** (Articles 31–44) — the ESAs designate ICT third-party service providers as *critical* on the basis of systemic-impact criteria specified in Article 31 and further specified by [Delegated Regulation (EU) 2024/1502](https://eur-lex.europa.eu/eli/reg_del/2024/1502/oj). Designated critical providers are subject to direct EU-level oversight by a Lead Overseer (an ESA), with recommendation powers, information-gathering powers, and — ultimately — the power to require financial entities to suspend or terminate arrangements. <!-- needs-research: verify current list of designated critical ICT third-party service providers under DORA once ESAs publish the first designations -->

**Release-assurance implication.** For every AI arrangement in scope, the release-package carries: the register-of-information entry, the pre-contractual assessment memo, the contractual-clause set (with Article 30(3) items enumerated for critical-function arrangements), the sub-outsourcing map, and the concentration-risk analysis. The release-gate cannot approve a T3/T4 promotion built on an ICT third-party arrangement whose Article 30(3) contractual provisions are missing or incomplete. Chapter `02`'s SR-23-4 due-diligence package is the U.S. sibling — some of the same evidence discharges both; DORA's specificity is stronger.

### Pillar 5 — Information and intelligence sharing (Article 45)

**What it says.** Financial entities may exchange amongst themselves cyber threat information and intelligence, subject to safeguards. Participation is voluntary but encouraged.

**Release-assurance implication.** Where the entity participates in intelligence-sharing arrangements, the release-package acknowledges them and the incident-response procedure connects to them. This is a lighter release-gate concern than the other four pillars.

## Where AI stresses the DORA shape

DORA was drafted with a broad ICT footprint in mind — cloud infrastructure, software vendors, data providers, network services. AI arrangements fit inside its definitions but produce a few sharp edges the release-assurance owner has to disposition explicitly.

### Foundation-model providers under Article 30(3)

A hosted foundation-model provider supplying inference for a critical-function AI system is an ICT third-party service provider supporting a critical or important function, so Article 30(3)'s extended contractual list applies. Several items in that list are non-trivial to negotiate with a large foundation-model provider:

- **Full service-level descriptions** with quantitative performance targets — for capability performance, not just uptime. What is the SLA for token throughput at a given latency percentile? What is the SLA for retention of the *behaviour* of a pinned model version?
- **Notification of material changes** — silent updates to a nominally-pinned version have to be defined as material changes; deprecation windows have to be aligned to the entity's own risk-appetite for migration.
- **Cooperation with competent authorities** — a provider whose customer base spans many EU financial entities may face aggregated supervisory cooperation demands; the arrangement should acknowledge these.
- **Exit strategies with realistic transition periods** — for AI capability replacement, exit transitions can be long and technically demanding; the transition period specified in the contract must reflect that reality, not a boilerplate 30 days.
- **Audit rights** — the entity's right to audit the provider's ICT-risk-management posture, its own third-party arrangements (sub-outsourcing), and — where relevant — its model-risk practices, either directly or through pooled audits.

### Judge-model providers and evaluation-platform vendors

Both categories qualify as ICT third-party service providers when they participate in the delivery of release-gate evidence for a critical-function AI system. If the release decision depends on a judge model's output, and the judge-model provider fails, the release decision's evidentiary basis is compromised. The Article 28(3) register-of-information entry for the entity should therefore include these secondary providers, and — depending on materiality — Article 30(3) provisions may apply.

### Concentration risk in the foundation-model market

Article 28's concentration-risk assessment forces the entity to consider what happens when many downstream systems rely on the same upstream provider. In the current foundation-model market, concentration is high across three tiers: a few frontier-model providers, a few cloud inference providers underneath them, and — for many entities — a small number of internal integration platforms. Each tier is a concentration hazard the release-assurance owner has to disposition, and the release-package carries the concentration memo as an artefact. `mod-111` covers systemic-risk framing for the provider side of this arrangement.

### Cross-border and cross-regulator alignment

An EU financial entity running a foundation-model provider based outside the EU triggers DORA's requirements on cross-border data flows, cooperation with authorities, and — indirectly — GDPR interfaces. The release-package documents these interfaces and cites the relevant transfer safeguards. The release-gate does not resolve GDPR questions itself, but it must record that the required cross-referencing has been done.

### The interaction with EU AI Act obligations

DORA and the EU AI Act apply to the same AI system independently — DORA on the operational-resilience axis, the AI Act on the risk-management-and-transparency axis. There is no formal precedence rule between them; the entity has to discharge both. In practice, several DORA and AI Act obligations shape the same release-package artefacts: incident-reporting timelines braid Article 61 of the AI Act with DORA's Article 19; risk-management-framework language braids Article 9 of the AI Act with DORA's Article 6. The release-assurance methodology owner authors the crosswalk that shows which artefacts discharge which obligations, and where a shared artefact needs to be written to the more-demanding of the two obligation sets. `mod-106` teaches the shape.

## Worked shape — an underwriting-assistance system at an EU insurer

Take a concrete system: an **underwriting-assistance AI** at an EU insurer, used by underwriters to score commercial-lines submissions and surface risk factors from unstructured broker documentation. It participates in the delivery of a critical function (underwriting for a regulated line of business). It uses a hosted foundation model from a non-EU provider for the document-understanding component, an EU-based cloud inference provider for embedding computation, and an internal fine-tuned scoring head.

Plugged into DORA:

- **Register-of-information entries**: three — the foundation-model provider, the cloud inference provider, and the internal integration platform. Each entry names its supporting function, its criticality classification, and its sub-outsourcing chain (the foundation-model provider itself runs on a hyperscale cloud that is separately registered).
- **Pre-contractual assessment**: the foundation-model arrangement supports a critical function; concentration risk is documented against the insurer's overall foundation-model footprint; sub-outsourcing chain traced through the provider's cloud dependency.
- **Article 30(3) contractual clauses**: model-version pin with 12-month deprecation notice; silent-update definition; capability-SLA including latency and behaviour-stability commitments; incident-notification aligned to the insurer's DORA reporting window; audit rights (directly, and pooled through an audit consortium where directly-executed audits are impractical); exit strategy with a documented transition period, tested annually.
- **Sub-outsourcing map**: two-tier map with the cloud provider named; both tiers covered by Article 30 provisions per Article 29(2).
- **Resilience testing (Article 24 onward)**: annual adversarial-input testing on the deployed surface; TLPT within the entity's TLPT programme if the insurer is designated as significant; failure-injection exercise simulating provider outage with the fallback-provider migration runbook.
- **Incident classification**: pre-mapped classification for AI-specific incidents (silent-update behavioural change, hallucination cascade, evaluation-set exfiltration event, judge-model drift affecting release-gate evidence).
- **Release-gate criteria**: register entries current; Article 30(3) clauses executed; sub-outsourcing map current; concentration memo signed by risk committee within the last 12 months; resilience-testing evidence within currency window; incident-response readiness confirmed.

That is a DORA-shaped release-package for an EU-financial-sector AI system with a foundation-model dependency. Exercise-03 asks you to develop the Article 30(3) contractual-clause set for one such arrangement, article-by-article.

## RTS, ITS, and where to find current specifics

DORA's Level-1 text sets the shape; the specifics come from the Regulatory Technical Standards (RTS) and Implementing Technical Standards (ITS) developed by the European Supervisory Authorities and adopted through Commission delegated regulations. For the release-assurance methodology owner, the RTS/ITS matter for the exact schemas and templates:

- The **RTS on ICT risk management framework** (Article 15) specifies the elements of the framework and its documentation.
- The **RTS on classification of ICT-related incidents and cyber threats** (Article 18(3)) specifies the classification criteria and the thresholds for major incidents.
- The **ITS on the register of information** (Article 28(9)) specifies the exact data schema for the register — the fields, their allowed values, and the reporting-format specifications.
- The **RTS on the harmonisation of conditions enabling the conduct of the oversight activities** (Article 41) and the **Delegated Regulation on the criteria for designation of critical ICT third-party service providers** ([Delegated Regulation (EU) 2024/1502](https://eur-lex.europa.eu/eli/reg_del/2024/1502/oj)) specify the designation process and the oversight regime.
- The **RTS on the specification of policy on ICT services performed by ICT third-party service providers supporting critical or important functions** (Article 28(10)) specifies the mandatory content of the entity's own third-party policy.

The release-assurance methodology owner does not hand-carry each RTS/ITS into the release-package; instead, the RTS/ITS shape the entity's own DORA-implementation policy (typically owned by the ICT-risk function or the CRO), and the release-package cites that policy. The release-assurance owner's job is to make sure the citation is live and the entity's policy remains current with the applicable RTS/ITS.

## Where this shows up in the rest of the track

- `mod-101` — DORA is the EU-financial-sector statutory sibling of NIST AI RMF's GOVERN-6 and MANAGE-3 (third-party risk), rendered as directly-applicable law.
- `mod-102` — the assurance case for an EU-financial-sector AI system carries a DORA branch alongside its EU AI Act, ISO/IEC 42001, and NIST AI RMF branches.
- `mod-103` — the release-gate schema's `sector_rule_citation` field can point at a DORA article and — for critical-function arrangements — at Article 30(3) items individually.
- `mod-104` — the evidence pipeline carries register-of-information entries, pre-contractual assessment memos, and contractual-clause summaries as first-class artefacts.
- `mod-106` — the cross-jurisdictional obligation map places DORA alongside the EU AI Act, GDPR, and sector-specific EU financial regulation as a column of its own.
- `mod-108` — deployment-tier gating for EU-financial-sector systems uses the critical-function classification as one of its tier inputs.
- `mod-109` — the third-party evaluator interface uses DORA Article 30(3) as its template for evaluator arrangements when the entity is EU-financial-sector.
- `mod-110` — DORA's incident-management and resilience-testing pillars braid with post-market surveillance.
- `mod-111` — the designation of *critical* ICT third-party service providers under DORA Articles 31–44 is the systemic-risk sibling for the provider side of a foundation-model arrangement.

## Summary

- DORA (Regulation (EU) 2022/2554) is a directly-applicable EU regulation on digital operational resilience for the financial sector, applicable from 2025-01-17. It has five pillars: ICT risk management, ICT-related incident management, digital operational resilience testing, ICT third-party risk management, and information sharing.
- When an AI system participates in a critical or important function of an EU financial entity, DORA obligations attach to the AI system and to its ICT third-party service providers (foundation-model providers, hosted-inference vendors, judge-model providers, evaluation-platform vendors, cloud inference providers).
- Article 28(3) requires a register of information for all ICT third-party arrangements; Article 29 requires a pre-contractual assessment; Article 30(3) prescribes an extended contractual-clause set for arrangements supporting critical or important functions.
- The ESAs designate certain ICT third-party service providers as *critical* under Articles 31–44 and subject them to direct EU-level oversight.
- The release-package for a DORA-in-scope AI system carries the register entry, the pre-contractual assessment, the Article 30(3) contractual clauses, the sub-outsourcing map, the concentration-risk memo, and the resilience-testing evidence for each in-scope arrangement.
- Exercise-03 asks you to author the Article 30(3) contractual clause set for a foundation-model arrangement supporting a critical function.
