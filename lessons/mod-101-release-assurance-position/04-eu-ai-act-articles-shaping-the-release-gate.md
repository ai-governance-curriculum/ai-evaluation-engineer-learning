# EU AI Act — Articles That Shape a Release Gate

## Motivation

The EU AI Act (Regulation (EU) 2024/1689) is the world's first horizontal AI regulation. Where NIST AI RMF is voluntary framework and ISO/IEC 42001 is a certifiable management-system standard, the EU AI Act is **law** — Regulation, directly applicable, with enforcement through Member State authorities and, for GPAI, through the European AI Office.

For a release-assurance program the Act matters in two ways.

First, if the AI system in scope falls under one of the Act's regulated categories (in particular high-risk AI systems per Annex III or Annex I, or GPAI models — especially those with systemic risk), then the release-gate is *carrying* a set of statutory obligations, not just internal ones. The release-gate architecture (`mod-103`) has to name each obligation, cite the article, and attach the evidence that discharges it.

Second, even for systems that are not in scope of the Act, the Act is the pattern that regulators in other jurisdictions are converging on — its shape (risk-management system, technical documentation, human oversight, accuracy / robustness / cybersecurity, post-market monitoring) is now the reference shape for release-assurance evidence globally.

This chapter reads the specific articles that shape a release-gate: Articles 8–15 (obligations on high-risk AI systems), Article 17 (QMS), Article 26 (deployer obligations), Article 43 (conformity assessment), Article 47 (EU declaration of conformity), Article 49 (registration), Article 55 (systemic-risk GPAI), Article 61 (post-market obligations), Article 72 (post-market monitoring plan).

> **Note on terminology.** The Act distinguishes *providers* (who place an AI system on the market or put it into service under their own name) from *deployers* (who use an AI system under their authority, formerly "users" in earlier drafts). Many release-assurance programs run for a provider *or* a deployer, and the obligation set differs. Read each article with the relevant actor's hat on.

## The article set that shapes the release-gate

### Article 8 — Compliance with the requirements

**What it says.** High-risk AI systems shall comply with the requirements laid down in Chapter III, Section 2 (Articles 9–15), and compliance shall take into account the AI system's intended purpose, generally acknowledged state of the art, and the risk-management system in Article 9.

**Release-gate implication.** Article 8 is the top of the requirements pyramid for high-risk systems. The release-gate does not carry Article 8 evidence directly; it carries evidence for each of Articles 9–15 individually, and the release decision itself is the operationalisation of "the system is compliant with Chapter III, Section 2."

### Article 9 — Risk-management system

**What it says.** A risk-management system shall be established, implemented, documented, and maintained across the entire lifecycle. It must (a) identify and analyse known and reasonably foreseeable risks; (b) estimate risks that may emerge from intended purpose and reasonably foreseeable misuse; (c) evaluate other risks arising from post-market monitoring data; (d) adopt appropriate targeted risk-management measures.

**Release-gate implication.** Article 9 is the statutory sibling of NIST AI RMF's MAP and MANAGE. The release-gate carries: the risk-management system document (from `mod-102`/`mod-103`), the harm inventory produced by `ai-risk-engineer`, the reasonably-foreseeable-misuse register, and the post-market feedback loop (`mod-110`).

### Article 10 — Data and data governance

**What it says.** Training, validation, and testing data sets shall be subject to data-governance and data-management practices appropriate for the intended purpose — including relevant design choices, data collection processes, data preparation, and examination of possible biases, gaps, and shortcomings.

**Release-gate implication.** Article 10 is where the release-gate consumes the peer analyst's data-governance work and the peer risk-engineer's bias analysis, and where dataset cards (`mod-105`) become statutory evidence. It also cross-links to ISO/IEC 5259 and ISO/IEC 8183 for data-quality method.

### Article 11 — Technical documentation

**What it says.** Technical documentation for a high-risk AI system shall be drawn up before it is placed on the market or put into service, kept up-to-date, and shall demonstrate that the AI system complies with the requirements of Chapter III, Section 2. Annex IV specifies the minimum contents.

**Release-gate implication.** Article 11's technical documentation is the *release package* — the artefact bundle that the release-gate assembles and that the auditor / notified body / market-surveillance authority reads. It is *not* the same as the model card for external audiences (`mod-105`); it is the internal-facing statutory dossier the model card is derived from.

Annex IV's shape (system description, elements of the AI system and process for development, monitoring, functioning, control, standards applied, EU declaration of conformity, post-market monitoring plan) is directly the shape of the release-package template.

### Article 12 — Record-keeping

**What it says.** High-risk AI systems shall technically allow automatic recording of events (logs) throughout their lifecycle, appropriate to the intended purpose, to trace functioning and support post-market monitoring. Retention periods must be appropriate.

**Release-gate implication.** Article 12 is the statutory backing for the evidence pipeline (`mod-104`). The release-gate cannot pass unless the system's runtime logging design (owned upstream by `ai-eval-engineer` and `ai-infra-mlops` peers) has been threaded through — the release-assurance program specifies what is logged, retention, and how logs feed into post-market monitoring.

### Article 13 — Transparency and provision of information to deployers

**What it says.** High-risk AI systems shall be designed and developed such that their operation is sufficiently transparent to enable deployers to interpret the system's output and use it appropriately. They shall be accompanied by instructions for use containing concise, complete, correct, and clear information relevant to the deployer.

**Release-gate implication.** Article 13 is the statutory backing for the *system card* (`mod-105`). Instructions-for-use content is specified: identity of the provider, characteristics of the AI system, human-oversight measures, expected lifetime, maintenance measures. The release-gate has to attach the instructions-for-use draft and verify its adequacy against the article.

### Article 14 — Human oversight

**What it says.** High-risk AI systems shall be designed such that they can be effectively overseen by natural persons during the period they are in use. Human-oversight measures must enable the person to (among other duties) properly understand the AI system's capacities and limitations, remain aware of the possible tendency of automation bias, correctly interpret the output, decide not to use the output in a particular situation, override the output, and interrupt operation.

**Release-gate implication.** Human-oversight design is a release-gate concern because it is *evaluated* as evidence — that a human overseer can actually meet these duties given the interface. The release-gate reviews the human-oversight design document and any usability / calibration evidence for it.

### Article 15 — Accuracy, robustness, and cybersecurity

**What it says.** High-risk AI systems shall achieve, and their design shall enable, appropriate levels of accuracy, robustness, and cybersecurity. Levels shall be declared in accompanying instructions for use, tested, and maintained across the lifecycle. Systems shall be resilient to errors, faults, or inconsistencies, and against attempts by unauthorised third parties to alter their use, outputs, or performance by exploiting vulnerabilities (data poisoning, model poisoning, adversarial examples, model evasion, confidentiality attacks).

**Release-gate implication.** Article 15 is where MEASURE evidence lands. Accuracy, robustness, and cybersecurity thresholds are declared (in the technical documentation and in the instructions for use), the release-gate verifies the peer evidence discharges each, and the online-eval / post-market surveillance keeps the declarations alive.

### Article 17 — Quality management system

**What it says.** Providers of high-risk AI systems shall put a quality management system in place, documented in written policies, procedures, and instructions, covering (among a numbered list): strategy for regulatory compliance, techniques for design / design control / verification, examination / test / validation procedures, technical specifications, systems for data management, the risk-management system in Article 9, post-market monitoring per Article 72, procedures for reporting serious incidents per Article 73, communication with authorities, record-keeping, resource management, accountability framework.

**Release-gate implication.** Article 17 is the statutory sibling of ISO/IEC 42001 (AIMS). Where clauses 4–10 of ISO/IEC 42001 are audited, Article 17 is the QMS the notified body inspects. The release-assurance program's methodology *is* the operational core of the Article 17 QMS. `mod-112` teaches how to run the program at that level.

### Article 26 — Obligations of deployers of high-risk AI systems

**What it says.** Deployers shall (a) take appropriate technical and organisational measures to ensure use in accordance with instructions; (b) assign human oversight to natural persons who have the necessary competence, training, authority, and support; (c) ensure input data is relevant and sufficiently representative; (d) monitor the operation of the AI system on the basis of the instructions for use; (e) keep logs generated by the AI system for an appropriate period; and more. Article 26 also refers to the fundamental-rights impact assessment (FRIA) in Article 27 for specified deployer categories.

**Release-gate implication.** If the release-assurance program is running for a *deployer* rather than a provider, this article is the top of its release-gate obligation pyramid. The evidence set is different — human-oversight competence, input-data governance, monitoring configuration, log retention — but the shape is the same. Many enterprise release-gates run for both hats simultaneously (deployer of a provider's foundation model, provider of a fine-tuned or system-integrated derivative).

### Article 43 — Conformity assessment

**What it says.** Depending on the Annex III area, the provider follows one of two conformity-assessment procedures before placing the system on the market: internal control (Annex VI) or involvement of a notified body (Annex VII). Some Annex III use-cases (biometrics categorisations, remote biometric identification) require notified-body involvement.

**Release-gate implication.** Article 43 decides who ultimately signs the CE-marking dossier — internal or a notified body. The release-assurance program produces the dossier either way; the notified-body pathway adds the third-party interface obligations covered in `mod-109`.

### Article 47 — EU declaration of conformity

**What it says.** The provider shall draw up a written machine-readable EU declaration of conformity for each high-risk AI system and keep it at the disposal of the national competent authorities for 10 years after placing on the market. Contents are specified in Annex V.

**Release-gate implication.** The EU declaration of conformity is one of the release-package outputs (`mod-104`). It is a specific artefact with a specific content list; the release-gate cannot pass for a high-risk system without it.

### Article 49 — Registration

**What it says.** Before placing a high-risk AI system on the market or putting it into service, providers (and, for certain Annex III use-cases, public-authority deployers) shall register the AI system in the EU database referred to in Article 71.

**Release-gate implication.** Registration is a gate-preceding action — the release-gate confirms it has happened, records the registration reference, and threads it into the release notes.

### Article 55 — Obligations for providers of general-purpose AI models with systemic risk

**What it says.** In addition to the baseline GPAI obligations (Article 53), providers of GPAI models with systemic risk shall (a) perform model evaluation in accordance with standardised protocols reflecting state of the art, including adversarial testing, to identify and mitigate systemic risks; (b) assess and mitigate possible systemic risks at Union level; (c) keep track of, document, and report serious incidents to the AI Office; (d) ensure an adequate level of cybersecurity protection for the model and its physical infrastructure.

**Release-gate implication.** For GPAI models with systemic risk, the release-gate is scaled up: the systemic-risk assessment, adversarial-evaluation evidence, serious-incident procedure, and cybersecurity of the model artefacts all become gate criteria. `mod-108` and `mod-111` teach the full shape.

The EU AI Office's GPAI Code of Practice is the operational reference for many providers here — it details how the Article 55 obligations are typically discharged.

### Article 61 — Reporting of serious incidents

**What it says.** Providers of high-risk AI systems placed on the Union market shall report any serious incident to the market-surveillance authorities of the Member States where that incident occurred. Reporting timelines are specified.

**Release-gate implication.** Incident-response and reporting are release-gate concerns because the release-package attaches the serious-incident procedure (`mod-110`). The gate cannot pass without a documented, tested procedure.

### Article 72 — Post-market monitoring by providers

**What it says.** Providers shall establish and document a post-market monitoring system in a manner that is proportionate to the nature of the AI technologies and the risks of the high-risk AI system. The system shall actively and systematically collect, document, and analyse relevant data provided by deployers or collected through other sources on the performance of the AI system throughout its lifetime.

**Release-gate implication.** Article 72 requires a *post-market monitoring plan* as a release-package artefact. `mod-110` is dedicated to this artefact and to running the loop that keeps release-gate decisions alive after ship.

## Beyond these articles

A release-assurance program will also touch other parts of the Act in specific situations:

- **Article 5** — prohibited AI practices. Not a release-gate obligation per se; instead, an intake-time disqualification the analyst/legal counsel typically catches before the system reaches the release-gate.
- **Article 6 + Annex III** — high-risk classification. Governs whether Articles 8–15 apply at all. Analyst legwork.
- **Article 27** — fundamental-rights impact assessment (FRIA) for specified deployer categories. Interfaces to the impact assessment under ISO/IEC 42005.
- **Article 53** — baseline GPAI obligations for any GPAI provider (technical documentation, information to downstream providers, copyright policy, training-content summary).
- **Article 71** — the EU database.
- **Article 73** — reporting of serious incidents, complementary to Article 61.
- **Annex III** — the current list of high-risk use-cases.

The release-assurance program tracks the *set* of articles that apply per system, not just the ones in this chapter.

## The Act is the pattern globally

Regulators in other jurisdictions are converging on similar obligation shapes: technical documentation, risk-management system, transparency to deployers and end-users, human oversight, accuracy / robustness / security, incident reporting, post-market monitoring. Even a release-gate for a system that will never touch EU deployment will typically be easier to defend elsewhere if it discharges the Act's shape. `mod-106` teaches the cross-jurisdictional map explicitly.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — the assurance case's claims cite EU AI Act articles as the top-level obligation source.
- `mod-103` (release-gate architecture) — the release-gate schema carries an explicit `eu_ai_act_article` field per obligation.
- `mod-104` (evidence pipeline) — Article 12 (record-keeping) is the statutory backing for the pipeline.
- `mod-105` (cards for external audiences) — the system card is derived from the Article 11 technical documentation and the Article 13 instructions for use.
- `mod-107` (sector-regulated assurance) — sector rules (SR 11-7, DORA, FDA GMLP) layer *on top of* the Act for regulated deployers.
- `mod-109` (third-party interface) — the notified-body pathway under Article 43 is one shape of the third-party interface.
- `mod-110` (post-market surveillance) — Articles 61, 72, and 73 are the statutory backing.
- `mod-111` (GPAI systemic-risk assurance) — Article 55 is the top of the pyramid, with the GPAI Code of Practice as the operational reference.

## Summary

- The EU AI Act is a Regulation — directly applicable law with statutory obligations that a release-gate for an in-scope system must discharge article by article.
- Articles 8–15 are the requirements for high-risk AI systems: overall compliance, risk-management system, data governance, technical documentation, record-keeping, transparency, human oversight, accuracy / robustness / cybersecurity.
- Article 17 requires a QMS; Article 26 sets deployer obligations; Article 43 governs conformity assessment; Article 47 is the EU declaration of conformity; Article 49 is registration.
- Article 55 layers systemic-risk GPAI obligations on top; the GPAI Code of Practice is the operational reference.
- Articles 61 and 72 govern serious-incident reporting and post-market monitoring — the surveillance loop that keeps release-gate decisions alive after ship.
- Exercise 04 has you map a release-gate for a specific high-risk system to the article set, article by article, with the evidence artefact that discharges each.
