# Non-EU Jurisdictional Overlay — UK, Australia, Canada, Japan, South Korea, PRC, Brazil

## Motivation

Chapter `05` added the US-side overlay: state statutes, city rules, and federal civil-rights and consumer-protection guidance stacked on top of the EU AI Act anchor. This chapter does the equivalent for the seven other jurisdictions the release-assurance program most often has to answer to in 2026.

The pattern is the same as chapter `05`. Each jurisdictional overlay:

1. Names the instrument, its legal status (statute in force, statute pending, principles-based guidance, cross-sector regulator guidance), the issuing body, and the enforcement route.
2. Enumerates the obligations that touch a release-gate.
3. Cross-references the EU AI Act row where the deliverable is shared and enumerates the genuinely new rows the overlay adds.
4. Flags the *traps* — the parts of the instrument that look like a duplicate of an EU obligation but are not, and the parts that add a genuinely new obligation the anchor does not carry.

The seven instruments covered here:

- **UK — ICO AI and data protection guidance** (principles-based supervisory guidance)
- **Australia — Voluntary AI Safety Standard** (voluntary, from the Department of Industry, Science and Resources)
- **Canada — Artificial Intelligence and Data Act (AIDA), Bill C-27** (proposed; still in parliamentary process as of authoring)
- **Japan — METI AI Guidelines for Business** (voluntary, from METI, with related Cabinet Office AI Strategy)
- **South Korea — AI Framework Act** (Act on the Development of Artificial Intelligence and Establishment of Trust)
- **PRC — CAC Interim Measures for the Management of Generative AI Services** (in force; from the Cyberspace Administration of China with joint ministerial issuance)
- **Brazil — AI Bill (PL 2338/2023)** (bill in the National Congress)

A programme that ships globally will typically face a subset of these, not all seven. The map still has to enumerate the applicable instruments and their obligations. A "no exposure" determination is itself a row on the map (see chapter `08`'s `applies_when` treatment).

`<!-- needs-research: statutes and bills in this chapter are moving quickly; every applies-when determination in a real release-gate must be re-verified against current legal counsel and the currently published text, not against this chapter -->`

## UK — ICO AI and data protection guidance

**Instrument.** The UK does not have a horizontal AI statute as of 2026. It has a sector-regulator-driven regime: the Information Commissioner's Office (ICO) supervises data-protection-adjacent obligations under UK GDPR and the Data Protection Act 2018, and other regulators (FCA, Ofcom, MHRA, CMA) supervise AI use inside their own remits. The white paper *A pro-innovation approach to AI regulation* (March 2023) established the principles-based framework the regulators translate into their own guidance.

For the release-gate, the ICO's guidance is the load-bearing artefact. The relevant publications are:

- **Guidance on AI and data protection** (ICO, most recently updated 2023) — the umbrella document covering lawful basis, fairness, transparency, data minimisation, individual rights, and accountability under UK GDPR for AI systems.
- **Explaining decisions made with AI** (ICO with The Alan Turing Institute) — the operational guidance on Article 22 UK GDPR explanation obligations for solely automated decisions with legal or similarly significant effects.
- **AI risk toolkit** and the **AI and data protection risk toolkit** — practical checklists that map onto ICO enforcement expectations.

The [ICO regulatory sandbox](https://ico.org.uk/for-organisations/advice-and-services/regulatory-sandbox/) is a supervisory-engagement channel that many programmes use for pre-deployment consultation on novel AI use cases; the sandbox output is not a formal approval but is a defensible artefact on the map.

**Obligations that touch the release-gate.** UK GDPR Articles 5 (principles), 22 (automated decision-making), 25 (data protection by design), 35 (DPIA), plus the *Data Protection Act 2018* substantive provisions for law-enforcement / intelligence-services processing.

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `uk-gdpr.art22.explainability` | Meaningful explanation for solely automated decisions with legal / similarly significant effects | `uk-explainability-report-v<N>.md` following ICO / Turing methodology | `model-evaluation-engineer` + this role |
| `uk-gdpr.art35.dpia` | Data protection impact assessment where processing is likely to result in high risk | `uk-dpia-v<N>.md` — cross-ref to `iso/42005` shape where alignable | this role + data-protection officer (DPO) |
| `uk-ico.ai-guidance.lawful-basis` | Documented lawful basis for AI processing | `uk-lawful-basis-record-v<N>.md` | legal + DPO |
| `uk-ico.ai-guidance.fairness-review` | ICO fairness assessment applied to the AI system | `uk-fairness-review-v<N>.md` | `ai-risk-engineer` + this role |
| `uk-ico.ai-guidance.transparency-notice` | Article 13 / 14 UK GDPR privacy notice adapted for the AI system | cross-ref to `eu-ai-act.art13.instructions-for-use` + `uk-privacy-notice-v<N>.md` | product + legal |
| `uk-ico.sandbox-engagement` (optional) | Sandbox output where the programme has engaged the ICO | `uk-ico-sandbox-report-v<N>.md` | legal + this role |

**Trap — "solely automated" is a narrow test.** UK GDPR Article 22 applies only where there is no meaningful human involvement in the decision and the effect is legal or similarly significant. A human-oversight design under EU AI Act Article 14 that adds meaningful review typically takes the system out of Article 22's ambit for that decision path — but the release-gate cannot rely on that assertion without producing the oversight-usability evidence. The map's UK Article 22 row therefore is often *not-applicable-with-evidence*, not *waived*.

**Trap — the FCA / Ofcom / MHRA remits.** The UK's regulator-led approach means that in-scope FCA / Ofcom / MHRA use cases inherit their own regulator's expectations on top of the ICO baseline. Financial firms overlay [FCA CP24-9 / DP5/22 (AI in financial services)](https://www.fca.org.uk/publications), medical devices overlay MHRA software-as-medical-device guidance, and online platforms overlay Ofcom's Online Safety Act code. The map cross-references these but does not enumerate them here — they are `mod-107` territory.

**Trap — UK vs. EU divergence.** UK GDPR is aligned but not identical to EU GDPR; the reforms in the Data Protection and Digital Information Bill (as it moves through parliament) may widen the gap. The map should carry the *UK* GDPR article, not the EU GDPR article, even when the wording is identical, so downstream diff analysis catches divergences.

## Australia — Voluntary AI Safety Standard

**Instrument.** The [Australian Voluntary AI Safety Standard (VAISS)](https://www.industry.gov.au/publications/voluntary-ai-safety-standard) was published by the Department of Industry, Science and Resources in September 2024. It comprises ten guardrails covering accountability, risk management, data governance, testing, human oversight, transparency, contestability, supply chain, records, and stakeholder engagement. It is voluntary — but the Government has signalled that mandatory guardrails for high-risk AI settings will follow, likely tracking the voluntary shape closely. The [interim response to *Safe and responsible AI in Australia*](https://www.industry.gov.au/publications/safe-and-responsible-ai-australia-consultation) sets the direction.

Australia's *Privacy Act 1988* (as amended, and with a further reform tranche in progress) supplies the data-protection floor; the OAIC (Office of the Australian Information Commissioner) is the supervisor.

**Obligations that touch the release-gate.** The ten VAISS guardrails plus Privacy Act Australian Privacy Principles (APPs) where personal information is processed.

**Overlay rows — VAISS guardrails.**

| Row | Guardrail | Deliverable | Owner |
| --- | --- | --- | --- |
| `au-vaiss.g1.accountability` | Establish accountability | cross-ref to `eu-ai-act.art17.qms` + `au-accountability-map-v<N>.md` | this role |
| `au-vaiss.g2.risk-management` | Risk-management process | cross-ref to `eu-ai-act.art9.plan` | this role |
| `au-vaiss.g3.data-governance` | Data-governance measures | cross-ref to `eu-ai-act.art10.governance-plan` | `ai-governance-analyst` |
| `au-vaiss.g4.testing-and-monitoring` | Testing, evaluation, and monitoring | cross-ref to `eu-ai-act.art15.*` + `eu-ai-act.art72.post-market-plan` | `model-evaluation-engineer` |
| `au-vaiss.g5.human-oversight` | Human oversight and intervention | cross-ref to `eu-ai-act.art14.oversight-design` | this role |
| `au-vaiss.g6.transparency` | Transparency to end-users | cross-ref to `eu-ai-act.art13.instructions-for-use` + `au-end-user-notice-v<N>.md` | product + legal |
| `au-vaiss.g7.contestability` | Contestation and escalation | `au-contestation-mechanism-spec-v<N>.md` | product + this role |
| `au-vaiss.g8.supply-chain` | AI supply chain transparency | cross-ref to `eu-ai-act.art10.lineage-manifest` + `au-supply-chain-attestation-v<N>.md` | `ai-governance-analyst` |
| `au-vaiss.g9.records` | Records for stakeholder verification | cross-ref to `eu-ai-act.art11.annex-iv.*` | this role |
| `au-vaiss.g10.stakeholder-engagement` | Stakeholder engagement | `au-stakeholder-engagement-log-v<N>.md` | this role |

**Overlay rows — Privacy Act.**

- `au-privacy.app6.use-and-disclosure` — use / disclosure consistent with the primary purpose collected for
- `au-privacy.app11.security` — reasonable security steps for personal information
- `au-privacy.notifiable-data-breaches` — 30-day notification of eligible data breaches to OAIC and affected individuals

**Trap — voluntary does not mean absent.** VAISS is voluntary but is being used as the reference frame for procurement, tender responses, and enterprise-risk questionnaires. A programme that "does not do VAISS" cannot answer an Australian government tender question. The map should carry VAISS rows even when the *statutory* trigger is missing.

**Trap — the mandatory guardrails, when they land, may re-scope this section.** The Government's [interim response](https://www.industry.gov.au/publications/safe-and-responsible-ai-australia-consultation) commits to mandatory guardrails for high-risk AI settings. Programmes that have already adopted VAISS will convert quickly; those that have not will face a compressed adoption window. `<!-- needs-research: verify current status of the mandatory guardrails legislation and update this chapter -->`.

**Trap — the "reasonable steps" pattern.** APP 11 and several VAISS guardrails use a "reasonable steps" standard. This is not "no steps" — it is a standard the release-gate must be able to *show*. Every row using this pattern needs an evidence pointer, not a policy assertion.

## Canada — AIDA (Bill C-27)

**Instrument.** Canada's proposed *Artificial Intelligence and Data Act* is part of Bill C-27 (the *Digital Charter Implementation Act, 2022*), which also contains the *Consumer Privacy Protection Act* and the *Personal Information and Data Protection Tribunal Act*. The bill has moved through committee but is not enacted as of authoring. AIDA is expected to impose obligations on those who make available for use, manage the operations of, or design or develop for use "high-impact" AI systems, with obligations including risk-assessment and mitigation plans, monitoring, transparency, and record-keeping. The [ISED companion document](https://ised-isde.canada.ca/site/innovation-better-canada/en/artificial-intelligence-and-data-act) sketches the enforcement mechanism (Ministerial powers, an AI and Data Commissioner, private penalties, and criminal offences for reckless / knowingly deploying certain AI to cause serious harm).

Provincial regimes are already in force:

- **Quebec — Law 25 (formerly Bill 64)** — imposes obligations on decisions based *exclusively* on automated processing, including notification and human intervention on request, effective 2023-09-22.
- **Ontario — Bill 194 (Strengthening Cyber Security and Building Trust in the Public Sector Act, 2024)** — public-sector AI use rules.

The federal *Personal Information Protection and Electronic Documents Act (PIPEDA)* supplies the data-protection floor federally, with provincial equivalents (Quebec Law 25, Alberta PIPA, British Columbia PIPA) where applicable.

**Obligations that touch the release-gate (AIDA, if enacted).**

- Assess whether the system is a "high-impact" system.
- Establish measures to identify, assess, and mitigate risks of harm and biased output.
- Publish a plain-language description of the system, its intended use, mitigation measures, and monitoring.
- Notify the Minister of harms or biased output that result in serious material harm.
- Keep records to demonstrate compliance.

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `ca-aida.high-impact.classification` | High-impact classification decision | `ca-high-impact-classification-v<N>.md` | legal + `ai-governance-analyst` |
| `ca-aida.risk-mitigation.plan` | Measures to identify, assess, mitigate risks (once in force) | cross-ref to `eu-ai-act.art9.plan` | this role |
| `ca-aida.public-description` | Plain-language description published for the intended user | cross-ref to `eu-ai-act.art13.deployer-card` + `ca-public-description-v<N>.md` | product + this role |
| `ca-aida.monitoring.plan` | Monitoring plan post-deployment | cross-ref to `eu-ai-act.art72.post-market-plan` | this role |
| `ca-aida.serious-harm-notice` | Notification of serious material harm to Minister | `ca-aida-notification-procedure.md` | legal + this role |
| `ca-quebec-law-25.art22.automated-decision-notice` | Notice + human intervention for exclusively automated decisions | `qc-law-25-automated-decision-notice.md` | product + legal |
| `ca-pipeda.principle-consent` | Meaningful consent for AI-adjacent personal-information use | cross-ref to `eu-ai-act.art10.governance-plan` + `ca-pipeda-consent-record.md` | legal + DPO |
| `ca-ontario-bill-194.public-sector-ai` | Public-sector AI use rules (only for public-sector deployers) | `on-bill-194-public-sector-record.md` | legal + this role |

**Trap — AIDA is *not enacted*.** The map must record AIDA rows as `applies_when: "AIDA enacted"` and mark `status: pending-instrument`. A row that reads as covered before the instrument is law over-claims. The programme still may wish to *pre-populate* the row so the gate is ready — but the classification must be honest.

**Trap — Quebec is in force *now*.** Law 25 Article 22 applies to exclusively automated decisions producing legal effects or affecting the person concerned. This is stricter in some respects than PIPEDA and applies immediately for organisations doing business in Quebec.

**Trap — bilingual disclosures.** Quebec disclosures must be available in French. The `qc-law-25-*` rows should carry a language sub-field on the deliverable.

## Japan — METI AI Guidelines for Business

**Instrument.** Japan's approach is voluntary-guidance-heavy. The load-bearing artefact is the [*AI Guidelines for Business* (METI, MIC, joint publication)](https://www.meti.go.jp/policy/mono_info_service/geniai/ai_guideline.html), most recently published in version 1.0 (April 2024) with updates tracked publicly. It consolidates the earlier *Social Principles of Human-Centric AI* (Cabinet Office, 2019), the METI *Governance Guidelines for Implementation of AI Principles*, and MIC / METI AI-utilisation and development guidelines.

Related regulatory instruments include:

- **Act on the Protection of Personal Information (APPI)** — the data-protection floor, with amendments introducing pseudonymised information and cross-border transfer requirements.
- **AI Promotion Act (2025)** — Japan enacted a lighter-touch AI framework act in 2025 emphasising promotion, transparency, and voluntary guideline adherence. `<!-- needs-research: confirm exact citation of the AI Promotion Act (Diet number and short title) and its effective date -->`.
- **Financial Services Agency (JFSA)** and **Personal Information Protection Commission (PPC)** sector guidance where applicable.

The [Hiroshima AI Process Code of Conduct](https://www.mofa.go.jp/ecm/ec/page5e_000076.html) — endorsed at the 2023 G7 — is an international commitment shape Japanese practitioners cite alongside the METI guidelines.

**Obligations that touch the release-gate.** The METI guidelines phrase obligations as *matters to be undertaken* by developers, providers, and business users, aligned with ten common principles (human-centric, safety, fairness, privacy, security, transparency, accountability, education, fair competition, innovation).

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `jp-meti.developer.safety` | Developer safety-consideration record | cross-ref to `eu-ai-act.art9.plan` + `jp-meti-safety-record.md` | this role |
| `jp-meti.developer.fairness` | Developer fairness / bias review | cross-ref to `eu-ai-act.art10.bias-report` | `ai-risk-engineer` |
| `jp-meti.developer.transparency` | Developer transparency (functions, limitations, uses) | cross-ref to `eu-ai-act.art13.deployer-card` + `jp-meti-transparency-supplement.md` | product + this role |
| `jp-meti.provider.instructions-for-use` | Provider instructions for use (business-facing) | cross-ref to `eu-ai-act.art13.instructions-for-use` | this role |
| `jp-meti.provider.post-market-response` | Provider post-market response and update procedures | cross-ref to `eu-ai-act.art72.post-market-plan` | this role |
| `jp-meti.business-user.human-oversight` | Business-user human-oversight commitment | cross-ref to `eu-ai-act.art14.oversight-design` + `jp-meti-oversight-record.md` | this role |
| `jp-appi.cross-border-transfer` | APPI cross-border transfer safeguards where applicable | `jp-appi-transfer-record.md` | legal + DPO |
| `jp-appi.pseudonymised-processing` | Pseudonymised-information processing record | `jp-appi-pseudonymised-record.md` | legal + `ai-governance-analyst` |
| `jp-ai-promotion-act.registration` | Registration / cooperation obligations under the Act | `jp-ai-promotion-act-record.md` | legal + this role |

**Trap — the guidelines split the actor.** METI's guidelines are explicit about the three actor types (developer, provider, business user) and their differing obligations. A single organisation with all three hats produces three sub-row-sets and cross-references them. This mirrors — but is not identical to — the EU AI Act provider / deployer split.

**Trap — Hiroshima AI Process commitments are voluntary but *cited*.** For frontier / general-purpose models the Hiroshima Code of Conduct commitments are the reference frame Japanese regulators expect providers to have adopted. The map's GPAI rows (from `mod-111`) should cross-reference the Code of Conduct even though it is not statute.

**Trap — the JFSA sector overlay.** Financial-services AI use in Japan comes with JFSA supervisory expectations that are not in the METI guidelines. Where in scope, the sector map (`mod-107`) picks it up.

## South Korea — AI Framework Act

**Instrument.** The Republic of Korea's *Act on the Development of Artificial Intelligence and Establishment of Trust* (colloquially the AI Framework Act or AI Basic Act) was passed by the National Assembly in December 2024 and takes effect on 2026-01-22. It establishes a comprehensive framework covering national AI strategy, high-impact AI, generative AI, and cross-border providers.

The [*Personal Information Protection Act (PIPA)*](https://www.pipc.go.kr/eng/) supplies the data-protection floor and, uniquely, has AI-specific supplementary provisions after 2023 amendments. The [Personal Information Protection Commission (PIPC)](https://www.pipc.go.kr/eng/) is the supervisor.

`<!-- needs-research: the AI Framework Act's enforcement decrees and Ministry of Science and ICT sub-regulations are being drafted in 2025-2026; confirm current status and cite exact article numbers of the Act rather than the summary below when authoring a real map -->`

**Obligations that touch the release-gate.** As enacted, the Act includes obligations for high-impact AI operators (risk-management, transparency, human oversight, safety measures, record-keeping), for generative-AI operators (labelling of AI-generated content, notification to users of AI interaction), and for foreign providers (in-country representative).

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `kr-ai-framework.high-impact.classification` | High-impact AI classification | `kr-high-impact-classification-v<N>.md` | legal + `ai-governance-analyst` |
| `kr-ai-framework.high-impact.risk-management` | Risk-management measures for high-impact AI | cross-ref to `eu-ai-act.art9.plan` | this role |
| `kr-ai-framework.high-impact.safety-measures` | Safety and reliability measures | cross-ref to `eu-ai-act.art15.*` | `model-evaluation-engineer` |
| `kr-ai-framework.high-impact.human-oversight` | Human oversight | cross-ref to `eu-ai-act.art14.oversight-design` | this role |
| `kr-ai-framework.high-impact.user-notification` | Notification of AI use to end-users | `kr-user-notification-template.md` | product + legal |
| `kr-ai-framework.generative-ai.labelling` | Labelling of AI-generated output | cross-ref to `eu-ai-act.art50.*` (from `mod-105`) + `kr-genai-labelling-spec.md` | product + this role |
| `kr-ai-framework.foreign-provider.representative` | In-country representative for foreign providers | `kr-in-country-representative-appointment.md` | legal |
| `kr-pipa.automated-decision-refusal` | Right to refuse fully-automated decisions (after 2023 amendment) | `kr-pipa-automated-decision-procedure.md` | product + legal |
| `kr-pipa.ai-processing-record` | Personal-information processing record for AI processing | `kr-pipa-processing-record.md` | DPO + `ai-governance-analyst` |

**Trap — the enforcement decrees are still being drafted.** The Act sets the frame; the operative detail comes in Presidential Decrees and MSIT (Ministry of Science and ICT) sub-regulations. The map's `kr-*` rows must cite the enforcement decree once published and be re-verified.

**Trap — the labelling obligation is broad.** The Act's labelling obligation for generative-AI outputs applies to a wider surface than EU AI Act Article 50(2) — it can capture outputs the EU regime treats as out-of-scope. The map's cross-reference to Article 50 must be qualified.

**Trap — the foreign-provider representative.** Where the release-assurance program's organisation is not established in Korea and its service is available to Korean users, the in-country representative appointment is a *pre-release* action. The gate cannot proceed without it.

## PRC — CAC Interim Measures for Generative AI Services

**Instrument.** The [Interim Measures for the Management of Generative Artificial Intelligence Services](http://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm) were issued by the Cyberspace Administration of China (CAC) jointly with six other ministries and took effect on 2023-08-15. They apply to the provision of generative AI services to the public within the territory of the People's Republic of China.

Related instruments:

- **Provisions on the Administration of Deep Synthesis Internet Information Services** (CAC, 2022) — deepfake-adjacent labelling and provider obligations for synthetic content.
- **Provisions on the Administration of Algorithmic Recommendations of Internet Information Services** (CAC, 2022) — algorithmic-recommendation registration and transparency.
- **Personal Information Protection Law (PIPL, 2021)** — the data-protection floor, with cross-border transfer requirements and impact-assessment obligations.
- **Data Security Law (DSL, 2021)** — data-classification and security requirements.
- **Cybersecurity Law (CSL, 2017)** — the cybersecurity floor.
- Model / Foundation-model relevant technical standards: **GB/T 45654-2025** (formerly TC260-003) on basic security requirements for generative AI services.

**Obligations that touch the release-gate.** The Interim Measures require providers to adhere to core socialist values, to prevent generation of prohibited content, to conduct security assessments and to file algorithmic registration (where the service has public-opinion attributes or social-mobilisation capacity), to label AI-generated content, to safeguard personal information, and to provide user complaint channels.

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `cn-cac-genai.security-assessment` | CAC security assessment for services with public-opinion attributes | `cn-cac-security-assessment-record-v<N>.md` | legal + `ai-infra-security` |
| `cn-cac-genai.algorithm-filing` | Algorithm filing with the CAC algorithm registry | `cn-cac-algorithm-filing-record.md` | legal + this role |
| `cn-cac-genai.content-labelling` | Labelling of AI-generated content per Deep Synthesis Provisions | cross-ref to `eu-ai-act.art50.2` + `cn-content-labelling-spec.md` | product + this role |
| `cn-cac-genai.training-data-lawfulness` | Lawful, legitimate source of training data | cross-ref to `eu-ai-act.art10.governance-plan` + `cn-training-data-lawfulness-record.md` | `ai-governance-analyst` + legal |
| `cn-cac-genai.content-policy` | Content policy meeting substantive requirements | `cn-content-policy-v<N>.md` | product + legal |
| `cn-cac-genai.user-complaint-channel` | User complaint channel and handling record | `cn-user-complaint-procedure.md` | product + this role |
| `cn-pipl.cross-border-transfer` | PIPL cross-border transfer mechanism | `cn-pipl-cross-border-record.md` | legal + DPO |
| `cn-pipl.pipia` | Personal information protection impact assessment | cross-ref to `iso/42005` + `cn-pipia-v<N>.md` | DPO + `ai-governance-analyst` |
| `cn-dsl.data-classification` | Data classification and important-data protection | `cn-dsl-data-classification.md` | `ai-governance-analyst` + `ai-infra-security` |
| `cn-tc260-003.basic-security-checklist` | GB/T 45654-2025 (TC260-003) basic security assessment | `cn-tc260-003-checklist-v<N>.md` | `ai-infra-security` + `model-evaluation-engineer` |

**Trap — territorial scope.** The Interim Measures apply to services *provided to the public within the territory of the PRC*. A model available globally but not offered to PRC users may be out of scope; a service that is nominally global but is available to PRC users is in scope. The map's `applies_when` for `cn-cac-genai.*` rows should record the operational determination and its evidence (geo-fencing, terms-of-service exclusion, market-entry decision).

**Trap — the substantive content requirements.** The Interim Measures include substantive content policy requirements (core socialist values, prevention of subversive content, etc.) that have no EU AI Act analogue. This is not merely a technical safety obligation — it is a substantive content-policy obligation, and it will typically require a purpose-built content-policy layer for the PRC market. Legal counsel signs.

**Trap — cross-border evidence.** Evidence pointers on `cn-*` rows may themselves have cross-border transfer implications if the evidence store lives outside the PRC. The evidence pipeline (`mod-104`) may need a PRC-local mirror; the map should record the storage location per row.

**Trap — algorithm filing timing.** Algorithm filing is *pre-service-launch* for in-scope services. The gate cannot proceed until the filing receipt is present. This mirrors EU AI Act Article 49 registration in shape but is a distinct regulator and a different content list.

## Brazil — AI Bill (PL 2338/2023)

**Instrument.** Brazil's *Projeto de Lei nº 2338 de 2023* is the Senate-originating comprehensive AI bill. As of authoring it has passed the Senate (December 2024) and is under consideration by the Chamber of Deputies. It follows a risk-based approach closely aligned with the EU AI Act: prohibited-risk systems, high-risk systems (with a defined list similar to Annex III), and general obligations for all AI systems, plus specific rules for generative AI and copyright.

The [Lei Geral de Proteção de Dados (LGPD, Lei nº 13.709/2018)](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) supplies the data-protection floor. The [Autoridade Nacional de Proteção de Dados (ANPD)](https://www.gov.br/anpd/pt-br) is the supervisor and has issued AI-relevant guidance.

**Obligations that touch the release-gate (as passed by the Senate; the Chamber may modify).**

- Prohibited-risk identification and non-deployment.
- High-risk classification and, for high-risk, risk-management, algorithmic-impact assessment, transparency, human oversight, and record-keeping.
- Generative-AI training-data disclosure requirements.
- Copyright rules for training on copyrighted works.
- Deployment notification and, for public-sector deployment, additional obligations.

**Overlay rows.**

| Row | Obligation summary | Deliverable | Owner |
| --- | --- | --- | --- |
| `br-pl-2338.prohibited-risk.check` | Prohibited-risk exclusion record | `br-prohibited-risk-check-v<N>.md` | legal + `ai-governance-analyst` |
| `br-pl-2338.high-risk.classification` | High-risk classification decision | `br-high-risk-classification-v<N>.md` | legal + `ai-governance-analyst` |
| `br-pl-2338.high-risk.aia` | Algorithmic impact assessment | cross-ref to `iso/42005` + `br-aia-v<N>.md` | this role + DPO |
| `br-pl-2338.high-risk.transparency` | Transparency and information to affected persons | cross-ref to `eu-ai-act.art13.instructions-for-use` + `br-transparency-notice-v<N>.md` | product + legal |
| `br-pl-2338.high-risk.human-oversight` | Human oversight measures | cross-ref to `eu-ai-act.art14.oversight-design` | this role |
| `br-pl-2338.high-risk.records` | Record-keeping | cross-ref to `eu-ai-act.art12.logging-design` | platform-eng |
| `br-pl-2338.genai.training-data-summary` | GPAI-style training-data summary | cross-ref to `eu-ai-act.art53` (from `mod-111`) + `br-training-data-summary-v<N>.md` | `ai-governance-analyst` |
| `br-pl-2338.copyright.disclosure` | Copyright disclosure and rights-holder mechanisms | `br-copyright-disclosure-v<N>.md` | legal + `ai-governance-analyst` |
| `br-lgpd.art20.automated-decision-review` | Right to review of decisions made solely by automated processing | `br-lgpd-automated-decision-procedure.md` | product + legal |
| `br-lgpd.dpia` | LGPD data-protection impact assessment | cross-ref to `iso/42005` + `br-dpia-v<N>.md` | DPO + this role |

**Trap — the text is not final.** The Chamber of Deputies may amend the Senate text. The map's `br-pl-2338.*` rows must cite the version-of-record (as passed by the Senate on <date>, or as amended by the Chamber on <date>) and be re-verified once enacted. Deliverables can be pre-drafted, but the *classification* rows should not be locked until enacted.

**Trap — LGPD is in force.** Article 20 LGPD's right to review of solely-automated decisions is already enforceable. Even before AI legislation lands, LGPD rows are live.

**Trap — ANPD guidance.** ANPD has been publishing AI-adjacent regulatory documents (regulatory sandbox regulations, generative-AI impact-assessment guidance). The `br-lgpd.*` rows should cross-reference the current ANPD guidance and be refreshed when new documents are published.

## Consolidated overlay pattern

Across the seven overlays, the same patterns recur:

- **Most obligations share a deliverable with an EU AI Act row.** Risk-management, human oversight, transparency, record-keeping, post-market monitoring, and impact-assessment obligations map onto the same deliverables the anchor produces. The overlay row is a cross-reference, not a new deliverable.
- **Consumer-facing / individual-rights obligations are almost always net-new.** UK GDPR Article 22 explanation, Quebec Law 25 automated-decision-notice, Korean PIPA automated-decision-refusal, LGPD Article 20 review, Colorado consumer notice and appeal, CFPB adverse-action notice — these are jurisdiction-by-jurisdiction and often have no EU AI Act analogue.
- **Substantive content requirements are jurisdiction-specific.** The PRC CAC content-policy row and the Korean labelling row are the clearest examples. The map records them as own-row obligations with legal countersign.
- **Registration / filing / notification obligations are gate-preceding.** EU Article 49, PRC algorithm filing, Korean foreign-representative appointment. These block the gate rather than being verified inside it.
- **"Not yet enacted" is a legitimate status.** AIDA and Brazil PL 2338 are not yet law. The map represents the pending status honestly and pre-populates the row against the current published text.
- **Sector overlays (financial, medical, online-platform) sit outside this map.** They land in `mod-107`.

## Cross-reference map — which non-EU rows share which EU AI Act rows

| Non-EU row | Shared EU AI Act row |
| --- | --- |
| `uk-gdpr.art35.dpia` | `eu-ai-act.art9.impact-assessment` (via ISO/IEC 42005 shape) |
| `au-vaiss.g2.risk-management` | `eu-ai-act.art9.plan` |
| `au-vaiss.g5.human-oversight` | `eu-ai-act.art14.oversight-design` |
| `ca-aida.risk-mitigation.plan` | `eu-ai-act.art9.plan` |
| `ca-aida.monitoring.plan` | `eu-ai-act.art72.post-market-plan` |
| `jp-meti.developer.fairness` | `eu-ai-act.art10.bias-report` |
| `jp-meti.provider.instructions-for-use` | `eu-ai-act.art13.instructions-for-use` |
| `kr-ai-framework.high-impact.risk-management` | `eu-ai-act.art9.plan` |
| `kr-ai-framework.generative-ai.labelling` | `eu-ai-act.art50.2` |
| `cn-cac-genai.content-labelling` | `eu-ai-act.art50.2` |
| `cn-cac-genai.training-data-lawfulness` | `eu-ai-act.art10.governance-plan` |
| `br-pl-2338.high-risk.aia` | `eu-ai-act.art9.impact-assessment` |
| `br-pl-2338.genai.training-data-summary` | `eu-ai-act.art53` |

Cross-references make one row's evidence discharge many rows' obligations — but the *cross-tag audit* (chapter `08`) must still walk from every overlay row to a live deliverable, not to a promise.

## Genuinely new rows the overlays add

Rows without a shared EU AI Act deliverable, that must be authored as own-artefacts:

- `uk-gdpr.art22.explainability`, `uk-ico.sandbox-engagement`
- `au-vaiss.g7.contestability`, `au-privacy.notifiable-data-breaches`
- `ca-aida.serious-harm-notice`, `ca-quebec-law-25.art22.automated-decision-notice`, `ca-ontario-bill-194.public-sector-ai`
- `jp-appi.cross-border-transfer`, `jp-appi.pseudonymised-processing`
- `kr-ai-framework.foreign-provider.representative`, `kr-pipa.automated-decision-refusal`
- `cn-cac-genai.security-assessment`, `cn-cac-genai.algorithm-filing`, `cn-cac-genai.content-policy`, `cn-cac-genai.user-complaint-channel`, `cn-tc260-003.basic-security-checklist`
- `br-lgpd.art20.automated-decision-review`, `br-pl-2338.copyright.disclosure`

Each of these deserves its own peer-role owner and its own evidence artefact on the map.

## Enforcement asymmetries worth flagging

- **UK.** ICO fines (up to £17.5M or 4% of global turnover under UK GDPR) plus regulator-specific fines from FCA, Ofcom, MHRA, CMA where applicable. No private right of action for GDPR breach, but tort claims are possible.
- **Australia.** APP breaches have OAIC enforcement (civil penalties reformed upwards recently) plus individual complaint route. VAISS is voluntary but influences procurement.
- **Canada.** AIDA (if enacted) contemplates Ministerial administrative penalties and criminal offences for the most egregious cases. Quebec Law 25 has strong administrative-penalty regime enforced by the Commission d'accès à l'information.
- **Japan.** APPI enforced by PPC with orders and criminal penalties. METI guidelines are voluntary — non-compliance is a reputational / procurement issue, not a fine.
- **South Korea.** AI Framework Act penalties for high-impact-AI non-compliance; PIPA fines are administrative and can be substantial. PIPC actively investigates.
- **PRC.** CAC has extensive enforcement authority; non-compliance with Interim Measures can result in service suspension, fines, and criminal referral. PIPL fines can reach 5% of prior year's turnover for serious breaches.
- **Brazil.** LGPD fines are substantial (up to 2% of Brazilian revenue with a cap); PL 2338 will bring additional AI-specific enforcement if enacted.

The residual-risk register per row records both the *enforcement severity* and the *enforcement route* (regulator, private, criminal, procurement-only), because each is a different risk shape.

## Where this shows up in the rest of the track

- `mod-105` — Colorado disclosure, Quebec French disclosure, and PRC labelling each generate distinct card variants.
- `mod-107` — sector-regulated overlays (JFSA, FCA, MHRA, provincial financial regulators) land here.
- `mod-108` — deployment-tier gating uses jurisdictional coverage as a tier criterion (a global-tier deployment picks up more overlays).
- `mod-109` — third-party evaluators in the UK (AISI UK) and elsewhere are named here.
- `mod-110` — post-market surveillance obligations from AU VAISS G4, CA AIDA monitoring, and PRC user-complaint channel resolve here.
- `mod-111` — GPAI systemic-risk assurance picks up the Hiroshima Code of Conduct commitments and the PRC training-data lawfulness rows for foundation-model providers.
- `mod-112` — programme-level dashboards report per-jurisdiction coverage across all systems.

## Summary

- The non-EU overlay adds seven jurisdictions to the map: UK (ICO), Australia (VAISS), Canada (AIDA + Quebec Law 25), Japan (METI guidelines), South Korea (AI Framework Act + PIPA), PRC (CAC Interim Measures + PIPL + DSL + CSL + TC260-003), Brazil (PL 2338 + LGPD).
- Most obligations share deliverables with EU AI Act rows and are recorded as cross-references. Individual-rights obligations, substantive content requirements, and jurisdiction-specific filings are the net-new rows.
- Not-yet-enacted instruments (AIDA, Brazil PL 2338) are represented as `applies_when: instrument-enacted` with `status: pending-instrument`.
- Registration and filing obligations (PRC algorithm filing, Korean in-country representative, EU Article 49 registration, Colorado AG disclosure) are gate-preceding actions.
- Enforcement asymmetries mean residual-risk-register posture per row varies substantially by jurisdiction.
- Exercise 05 walks a multi-jurisdictional scenario across the seven overlays; chapter `07` adds Singapore AI Verify as the interoperability reference.
