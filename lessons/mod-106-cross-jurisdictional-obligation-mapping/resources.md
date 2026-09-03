# Resources for mod-106-cross-jurisdictional-obligation-mapping

Primary sources first. Every URL below points at the organisation that owns the artefact — the regulator's authoritative host, the standards body, the tool project's own repository — so your reading pins to text that survives editorial rewrites. Secondary and background reading lives at the bottom.

Statutes and bills in this module move quickly. Where a URL points at a bill in flight (AIDA / Bill C-27, Brazil PL 2338, Korea's enforcement decrees, California CPPA rulemaking), check for a more recent revision before you cite the text into a live map.

## The EU AI Act anchor (chapter `02`)

### The Regulation itself and its official documentation

- [Regulation (EU) 2024/1689 — the EU Artificial Intelligence Act, on EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj). The authoritative text. Chapter III Section 2 (Articles 8–15) covers risk management, data governance, technical documentation, record-keeping, transparency, human oversight, accuracy / robustness / cybersecurity; Chapter III Section 3 (Articles 16–27) covers provider and deployer obligations; Chapter IX (Articles 72–86) covers post-market monitoring, information sharing, and market surveillance.
- [Annex III — high-risk domains list](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the eight high-risk-use-case categories that the classification row on the map cites.
- [Annex IV — technical documentation content list](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the eight numbered items each becoming a row on the map under Article 11.
- [Annex V — EU declaration of conformity content list](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the content fields each becoming a row / sub-field under Article 47.
- [Annexes VI and VII — conformity-assessment procedures](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the internal-control (Annex VI) vs. notified-body (Annex VII) procedures Article 43 chooses between.

### Institutional guidance and implementation documents

- [European Commission AI Act implementation page](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — current implementing acts, delegated acts, guidance, and Commission communications as they publish.
- [European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the Commission body coordinating GPAI supervision and general implementation. The AI Office publishes the Article 72(3) post-market-monitoring plan template referenced in chapter `02`.
- [European AI Board](https://digital-strategy.ec.europa.eu/en/policies/ai-board) — Member-State-level coordination body.
- [ENISA — European Union Agency for Cybersecurity — AI reports](https://www.enisa.europa.eu/topics/iot-and-smart-infrastructures/artificial-intelligence) — cybersecurity guidance relevant to Article 15(5) attack categories.
- [FRA — European Union Agency for Fundamental Rights — AI publications](https://fra.europa.eu/en/themes/artificial-intelligence-and-big-data) — fundamental-rights guidance relevant to Article 27 FRIA.

### Harmonised standards and their references

- [CEN-CENELEC JTC 21 work programme](https://www.cencenelec.eu/areas-of-work/cen-cenelec-topics/artificial-intelligence/) — the joint technical committee developing harmonised standards under the AI Act's Article 40. Watch for standards giving presumption of conformity for Articles 9, 10, 12, 13, 14, 15.
- [European Commission standardisation request C(2023) 3215](https://ec.europa.eu/growth/tools-databases/enorm/mandate/593_en) — the standardisation request to CEN-CENELEC covering the required deliverables.

## NIST AI RMF crosswalk (chapter `03`)

### AI RMF 1.0 and the GenAI Profile

- [NIST AI Risk Management Framework 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the four functions (GOVERN, MAP, MEASURE, MANAGE), the sub-category structure, and the trustworthy-characteristic vocabulary.
- [NIST AI 100-1 PDF direct](https://doi.org/10.6028/NIST.AI.100-1) — the published document, versioned.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the per-sub-category suggested actions. The Playbook version-of-record is pinned per row on the map.
- [NIST AI 600-1 — Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific risk categories (confabulation, harmful bias, information integrity, information security, IP, obscene / degrading / abusive content, value-chain and component integration, human-AI configuration, environmental impact, dangerous or violent recommendations, data privacy) and suggested actions.
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — the umbrella portal for RMF-adjacent resources, Playbook updates, and profile publications.

### Adversarial ML taxonomy — the AI 100-2 tags on Article 15 sub-rows

- [NIST AI 100-2 E2023 — Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations](https://doi.org/10.6028/NIST.AI.100-2e2023). Second edition of the ML attack-taxonomy the map's Article 15(5) attack-category sub-rows are labelled with.

### Adjacent NIST publications the module references

- [NIST AI 100-4 — Reducing Risks Posed by Synthetic Content](https://doi.org/10.6028/NIST.AI.100-4) — provenance and watermarking guidance the GenAI-Profile information-integrity rows cross-tag.
- [US AI Safety Institute at NIST](https://www.nist.gov/aisi) — evaluation methodology publications relevant to MEASURE-2 rows on GenAI; the AISI stretch goal on exercise `02` cross-tags to these.
- [NIST AI Standards Zero Drafts pilot](https://www.nist.gov/artificial-intelligence/nist-ai-standards-zero-drafts-pilot) — pre-standard drafts NIST is co-developing that eventually land in the map as sibling-clauses.

## ISO/IEC crosswalk (chapter `04`)

### The five ISO/IEC standards the module crosswalks

- [ISO/IEC 42001:2023 — *Information technology — Artificial intelligence — Management system*](https://www.iso.org/standard/81230.html). The AIMS clauses 4–10 and Annex A controls; the audit spine of the ISO crosswalk.
- [ISO/IEC 23894:2023 — *Information technology — Artificial intelligence — Guidance on risk management*](https://www.iso.org/standard/77304.html). The method-of-record for the AIMS clause 6.1.2 / 6.1.3 risk activities.
- [ISO/IEC 42005:2025 — *Information technology — Artificial intelligence — AI system impact assessment*](https://www.iso.org/standard/44545.html). The method-of-record for the AIMS clause 6.1.4 / 8.3 impact activities.
- [ISO/IEC 25059:2023 — *Software engineering — SQuaRE — Quality model for AI systems*](https://www.iso.org/standard/80655.html). The quality-attribute vocabulary the Article 13 / 14 / 15 rows are labelled with.
- [ISO/IEC 24029-2:2023 — *Assessment of the robustness of neural networks — Part 2: Methodology for the use of formal methods*](https://www.iso.org/standard/79804.html). The method-of-record for the Article 15 robustness deliverable.

### Adjacent ISO/IEC standards worth naming (light cross-tags)

- [ISO/IEC 24029-1:2021 — *Assessment of the robustness of neural networks — Part 1: Overview*](https://www.iso.org/standard/77609.html) — the overview companion to 24029-2.
- [ISO/IEC 5259 series — *Data quality for analytics and ML*](https://www.iso.org/standard/81088.html) — cross-tagged onto Article 10 dataset-facing rows.
- [ISO/IEC 8183:2023 — *AI data lifecycle framework*](https://www.iso.org/standard/83194.html) — cross-tagged onto dataset-card rows and lineage manifests.
- [ISO/IEC 42006:2025 — *Requirements for bodies providing audit and certification of AI management systems*](https://www.iso.org/standard/44546.html) — the accreditation regime the ISO/IEC 42001 certificate presumes.
- [ISO/IEC TR 24028:2020 — *Overview of trustworthiness in artificial intelligence*](https://www.iso.org/standard/77608.html) — the trustworthiness terminology many downstream ISO AI documents draw from.
- [ISO/IEC 5338:2023 — *AI system life cycle processes*](https://www.iso.org/standard/81118.html) — life-cycle process vocabulary the change-control rows read against.
- [ISO 31000:2018 — *Risk management — Guidelines*](https://www.iso.org/standard/65694.html) — the base risk-management framework 23894 adapts to AI.
- [ISO/IEC 27001:2022 — *Information security management systems*](https://www.iso.org/standard/27001) and [ISO/IEC 27002:2022 — *Information security controls*](https://www.iso.org/standard/75652.html) — the cybersecurity management-system reference Article 15 cybersecurity rows cross-tag to.

## US state and city overlay (chapter `05`)

### Colorado SB24-205

- [Colorado SB24-205 — *Consumer Protections for Artificial Intelligence* — bill page](https://leg.colorado.gov/bills/sb24-205). Text as enacted, with the developer / deployer duties, the "high-risk artificial intelligence system" definition, and the "consequential decision" scope list.
- [Colorado Attorney General's Office — enforcement page](https://coag.gov/) — announcements on the AG's enforcement stance and any subsequent rulemakings.
- [Colorado General Assembly session materials](https://leg.colorado.gov/sessions) — check for amendments in later sessions.

### NYC Local Law 144 (Automated Employment Decision Tools)

- [NYC Local Law 144 of 2021 — full text](https://legistar.council.nyc.gov/LegislationDetail.aspx?ID=4344524&GUID=B051915D-A9AC-451E-81F8-6596032FA3F9). The AEDT statute the bias-audit obligation flows from.
- [DCWP final rule on AEDTs (April 2023)](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf) — the operative rule specifying audit methodology, independence, categories, and enforcement.
- [DCWP AEDT information page](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — plain-language FAQ, notice templates, and enforcement guidance.

### CFPB adverse-action-notice circulars

- [CFPB Circular 2022-03 — *Adverse action notification requirements in connection with credit decisions based on complex algorithms*](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/). The "no black-box exception" clarification.
- [CFPB Circular 2023-03 — *Adverse action notice requirements when relying on artificial intelligence or complex predictive decision-making models*](https://www.consumerfinance.gov/compliance/circulars/circular-2023-03/). The "specific and accurate" reason-code standard.
- [Equal Credit Opportunity Act (ECOA), 15 U.S.C. § 1691](https://www.law.cornell.edu/uscode/text/15/1691) — the underlying statute.
- [Regulation B, 12 CFR Part 1002](https://www.consumerfinance.gov/rules-policy/regulations/1002/) — the implementing regulation whose adverse-action provisions the circulars interpret.
- [CFPB Consumer Compliance Circulars page](https://www.consumerfinance.gov/compliance/circulars/) — check for later circulars refining AI-adjacent adverse-action guidance.

### EEOC AI / ADA guidance

- [EEOC — *Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence Used in Employment Selection Procedures Under Title VII of the Civil Rights Act of 1964* (May 2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial). Four-fifths rule and UGESP applicability to AI selection tools.
- [EEOC — *The Americans with Disabilities Act and the Use of Software, Algorithms, and Artificial Intelligence to Assess Job Applicants and Employees* (May 2022)](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence). Screen-out analysis and reasonable-accommodation.
- [Uniform Guidelines on Employee Selection Procedures (UGESP), 29 CFR Part 1607](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607) — the 1978 baseline for selection-procedure adverse-impact analysis.
- [Title VII of the Civil Rights Act of 1964, 42 U.S.C. § 2000e](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964) — the underlying statute.
- [Americans with Disabilities Act of 1990, 42 U.S.C. § 12101 et seq.](https://www.ada.gov/law-and-regs/ada/) — the underlying statute.
- [EEOC AI initiative landing page](https://www.eeoc.gov/ai) — check for further Technical Assistance Documents.

### Adjacent US federal / state instruments worth naming

- [California Privacy Rights Act (CPRA)](https://oag.ca.gov/privacy/ccpa) and [California Privacy Protection Agency (CPPA) rulemaking page](https://cppa.ca.gov/regulations/) — watch the automated-decision-making rulemaking for a California overlay row set.
- [Illinois Artificial Intelligence Video Interview Act](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=4015) — an earlier state-level AI statute the map may cross-reference.
- [White House Executive Order 14110 — *Safe, Secure, and Trustworthy Development and Use of Artificial Intelligence* (2023)](https://www.federalregister.gov/documents/2023/11/01/2023-24283/safe-secure-and-trustworthy-development-and-use-of-artificial-intelligence) — the standing federal reference frame (revoked / superseded status shifts across administrations; check the [Federal Register EO list](https://www.federalregister.gov/presidential-documents/executive-orders) for the current posture).

## Non-EU jurisdictional overlay (chapter `06`)

### United Kingdom

- [ICO — *Guidance on AI and data protection*](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/). The umbrella document covering lawful basis, fairness, transparency, and accountability for AI under UK GDPR.
- [ICO and The Alan Turing Institute — *Explaining decisions made with AI*](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/explaining-decisions-made-with-ai/). Operational guidance on Article 22 UK GDPR explanation obligations.
- [ICO AI and data protection risk toolkit](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/ai-and-data-protection-risk-toolkit/).
- [ICO regulatory sandbox](https://ico.org.uk/for-organisations/advice-and-services/regulatory-sandbox/).
- [UK Government white paper — *A pro-innovation approach to AI regulation* (March 2023)](https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach). The principles-based framework the sector regulators translate into their own guidance.
- [UK Data Protection Act 2018](https://www.legislation.gov.uk/ukpga/2018/12/contents/enacted). The substantive statute alongside UK GDPR.
- [UK AI Safety Institute (AISI UK)](https://www.aisi.gov.uk/). Third-party evaluation methodology and reports; see also chapter `07`'s cross-references and `mod-109`.
- [FCA publications and consultations](https://www.fca.org.uk/publications) and [Bank of England / PRA DP5/22 on AI in financial services](https://www.bankofengland.co.uk/prudential-regulation/publication/2022/october/artificial-intelligence). Sector-specific supervisory expectations for AI in UK financial services.
- [MHRA Software and AI as a Medical Device change programme](https://www.gov.uk/government/publications/software-and-ai-as-a-medical-device-change-programme). Sector-specific for medical devices.

### Australia

- [Voluntary AI Safety Standard (VAISS)](https://www.industry.gov.au/publications/voluntary-ai-safety-standard). The ten guardrails.
- [Government interim response — *Safe and responsible AI in Australia*](https://www.industry.gov.au/publications/safe-and-responsible-ai-australia-consultation). Direction on mandatory guardrails and future regulation.
- [Privacy Act 1988 (as amended)](https://www.legislation.gov.au/C2004A03712/latest) and the [Australian Privacy Principles (APPs)](https://www.oaic.gov.au/privacy/australian-privacy-principles). The data-protection floor.
- [OAIC — Office of the Australian Information Commissioner](https://www.oaic.gov.au/). Supervisor.
- [OAIC AI guidance](https://www.oaic.gov.au/privacy/privacy-guidance-for-organisations-and-government-agencies/artificial-intelligence) — Privacy Act and AI intersection.

### Canada

- [Bill C-27 — *Digital Charter Implementation Act, 2022* (containing AIDA)](https://www.parl.ca/legisinfo/en/bill/44-1/c-27). The bill in flight. Check for status updates and any amended text.
- [ISED companion document to AIDA](https://ised-isde.canada.ca/site/innovation-better-canada/en/artificial-intelligence-and-data-act). The government's plain-language framing of AIDA.
- [Personal Information Protection and Electronic Documents Act (PIPEDA)](https://laws-lois.justice.gc.ca/eng/acts/p-8.6/). The federal data-protection floor.
- [Quebec Law 25 (formerly Bill 64) — *Act to modernise legislative provisions as regards the protection of personal information*](https://www.legisquebec.gouv.qc.ca/en/document/cs/P-39.1). Automated-decision-notice under Article 22.
- [Ontario Bill 194 — *Strengthening Cyber Security and Building Trust in the Public Sector Act, 2024*](https://www.ola.org/en/legislative-business/bills/parliament-43/session-1/bill-194). Public-sector AI use rules.
- [Office of the Privacy Commissioner of Canada — AI page](https://www.priv.gc.ca/en/privacy-topics/technology/artificial-intelligence/).
- [Commission d'accès à l'information du Québec](https://www.cai.gouv.qc.ca/). Quebec supervisor.
- [Directive on Automated Decision-Making (Government of Canada)](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592). Federal-government AI use rules; a reference frame for public-sector deployment.

### Japan

- [METI AI Guidelines for Business](https://www.meti.go.jp/policy/mono_info_service/geniai/ai_guideline.html). The current version-of-record (v1.0 published April 2024; check for updates).
- [Cabinet Office — Social Principles of Human-Centric AI (2019)](https://www8.cao.go.jp/cstp/english/humancentricai.pdf). The principle set underlying the METI guidelines.
- [Act on the Protection of Personal Information (APPI) — PPC English resources](https://www.ppc.go.jp/en/legal/). The data-protection floor.
- [Personal Information Protection Commission (PPC)](https://www.ppc.go.jp/en/). Supervisor.
- [Hiroshima AI Process Code of Conduct](https://www.mofa.go.jp/ecm/ec/page5e_000076.html). G7-endorsed voluntary code of conduct for advanced AI system developers.
- [G7 Hiroshima AI Process International Guiding Principles](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-international-guiding-principles-advanced-ai-system) — the underlying international principles set.
- [Japan Financial Services Agency (JFSA) publications page](https://www.fsa.go.jp/en/index.html). Sector-specific supervisory expectations for financial-services AI.

### South Korea

- [Act on the Development of Artificial Intelligence and Establishment of Trust (AI Framework Act) — MSIT summary page](https://www.msit.go.kr/eng/) — check for the current status, enforcement decrees, and MSIT sub-regulations.
- [Personal Information Protection Act (PIPA)](https://www.pipc.go.kr/eng/user/lgp/lawInfo.do). The data-protection floor, with AI-specific supplementary provisions after 2023 amendments.
- [Personal Information Protection Commission (PIPC)](https://www.pipc.go.kr/eng/). Supervisor.
- [Ministry of Science and ICT (MSIT)](https://www.msit.go.kr/eng/). The lead ministry for AI Framework Act implementation.

### People's Republic of China

- [CAC — *Interim Measures for the Management of Generative Artificial Intelligence Services* (2023)](http://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm). Original Chinese text; unofficial English translations available via [DigiChina](https://digichina.stanford.edu/) at Stanford.
- [CAC — *Provisions on the Administration of Deep Synthesis Internet Information Services* (2022)](http://www.cac.gov.cn/2022-12/11/c_1672221949318230.htm). Deepfake / synthetic-content provider obligations.
- [CAC — *Provisions on the Administration of Algorithmic Recommendations of Internet Information Services* (2022)](http://www.cac.gov.cn/2022-01/04/c_1642894606364259.htm). Algorithmic-recommendation registration and transparency.
- [Personal Information Protection Law (PIPL, 2021) — official text](http://www.npc.gov.cn/npc/c30834/202108/a8c4e3672c74491a80b53a172bb753fe.shtml). The data-protection floor.
- [Data Security Law (DSL, 2021) — official text](http://www.npc.gov.cn/npc/c30834/202106/7c9af12f51334a73b56d7938f99a788a.shtml).
- [Cybersecurity Law (CSL, 2017) — official text](http://www.cac.gov.cn/2016-11/07/c_1119867116.htm).
- [GB/T 45654-2025 — *Basic security requirements for generative artificial intelligence services* (SAC / TC260)](https://www.tc260.org.cn/). The technical-standard companion to the CAC Interim Measures.
- [DigiChina (Stanford Cyber Policy Center)](https://digichina.stanford.edu/) — high-quality analysis and unofficial English translations of PRC AI regulation.

### Brazil

- [Projeto de Lei nº 2338 de 2023 — Senado Federal do Brasil](https://www25.senado.leg.br/web/atividade/materias/-/materia/157233). The current AI bill; check for the Chamber of Deputies' amendments.
- [Lei Geral de Proteção de Dados (LGPD, Lei nº 13.709/2018)](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm). The data-protection floor.
- [Autoridade Nacional de Proteção de Dados (ANPD)](https://www.gov.br/anpd/pt-br). Supervisor; publishes AI-adjacent regulatory documents.

## Singapore AI Verify (chapter `07`)

### AI Verify Foundation and the Framework

- [AI Verify Foundation](https://aiverifyfoundation.sg/). The umbrella site — mission, publications, and current framework versions.
- [AI Verify Framework](https://aiverifyfoundation.sg/what-is-ai-verify/) — the eleven principles and their category grouping.
- [AI Verify Toolkit — GitHub repository](https://github.com/aiverify-foundation/aiverify). The open-source Python toolkit; technical-test catalogue and process-check list.
- [Project Moonshot](https://aiverifyfoundation.sg/project-moonshot/). LLM evaluation toolkit — adversarial red-teaming, prompt-injection resilience, jailbreak resistance, harmful-content classification. `aiverify-foundation/moonshot` on GitHub houses the code.
- [AI Verify Foundation crosswalks and mapping documentation](https://aiverifyfoundation.sg/resources/) — Foundation-published crosswalks to EU AI Act, NIST AI RMF, and ISO/IEC 42001.

### Model AI Governance Framework and companions

- [Model AI Governance Framework, 2nd Edition (2020)](https://www.pdpc.gov.sg/-/media/files/pdpc/pdf-files/resource-for-organisation/ai/sgmodelaigovframework2.pdf). The four building blocks the map's process spine reads to.
- [Model AI Governance Framework for Generative AI (May 2024)](https://aiverifyfoundation.sg/wp-content/uploads/Model-AI-Governance-Framework-for-Generative-AI-May-2024-1-1.pdf). The nine GenAI-specific dimensions.
- [Compendium of use cases — Model AI Governance Framework](https://www.pdpc.gov.sg/-/media/files/pdpc/pdf-files/resource-for-organisation/ai/sg-model-ai-governance-framework-use-case-volume-2.pdf). Illustrative applied examples.

### Singapore data protection and sector guidance

- [PDPA — Personal Data Protection Act 2012](https://sso.agc.gov.sg/Act/PDPA2012). The data-protection floor.
- [PDPC — Personal Data Protection Commission](https://www.pdpc.gov.sg/). Supervisor.
- [PDPC Advisory Guidelines on the Use of Personal Data in AI Recommendation and Decision Systems](https://www.pdpc.gov.sg/Guidelines-and-Consultation). AI-specific personal-data guidance.
- [Singapore Cybersecurity Act 2018](https://sso.agc.gov.sg/Act/CA2018). CII operator obligations.
- [MAS — Monetary Authority of Singapore FEAT principles](https://www.mas.gov.sg/publications/monographs-or-information-paper/2018/FEAT). Sector-specific fairness / ethics / accountability / transparency principles for financial-services AI. See also the [Veritas Consortium](https://www.mas.gov.sg/schemes-and-initiatives/veritas) work on operationalising them.

## The map artefact — schema and emission (chapter `08`)

### Signing, transparency, and content addressing

- [Sigstore project](https://www.sigstore.dev/). Fulcio short-lived certificates + Rekor transparency log; the recommended signing option for open-source-friendly programmes.
- [Rekor transparency log](https://docs.sigstore.dev/logging/overview/). Public-good transparency ledger for signed artefacts.
- [SLSA — Supply-chain Levels for Software Artefacts](https://slsa.dev/). Complementary supply-chain integrity framework the map's evidence pipeline (see `mod-104`) hooks into.
- [in-toto attestations spec](https://github.com/in-toto/attestation/blob/main/spec/README.md). The attestation shape SLSA / Sigstore emit; the map's per-row signing wraps compatibly.
- [RFC 8785 — JSON Canonicalisation Scheme (JCS)](https://www.rfc-editor.org/rfc/rfc8785). The canonicalisation rules that keep the emitted JSON diff-stable.
- [RFC 7515 — JSON Web Signature (JWS)](https://www.rfc-editor.org/rfc/rfc7515). The JWS alternative signing shape.
- [RFC 5652 — Cryptographic Message Syntax (CMS)](https://www.rfc-editor.org/rfc/rfc5652). The X.509 + CMS alternative for standards-based signing.
- [SPDX-AI and ML-BOM work at Linux Foundation SPDX](https://spdx.dev/). AI-BOM extensions the manifest wrappers on the emitted map compose with.

### Schema languages and validation

- [JSON Schema — 2020-12 draft](https://json-schema.org/specification.html). The row schema and map-header schema draft against.
- [YAML 1.2.2 specification](https://yaml.org/spec/1.2.2/). Reference for the author-side YAML shape.

## GPAI-adjacent and interoperability catalogues

- [OECD AI Policy Observatory](https://oecd.ai/en/). Cross-country catalogue of AI policies and instruments — a candidate community reference for the map's canonical instrument registry.
- [OECD AI Principles](https://oecd.ai/en/ai-principles). The international principle set many of the frameworks in this module align to.
- [Global Partnership on AI (GPAI)](https://gpai.ai/). GPAI reports and working-group outputs.
- [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/). Cross-industry safety-benchmark work.
- [MLCommons AILuminate benchmark](https://mlcommons.org/benchmarks/ailuminate/). Shared safety benchmark that composes with AI Verify / Moonshot for LLM evaluation.

## Suggested reading order for this module

1. Chapter `01`. Fix the vocabulary. Read the EU AI Act preamble (recitals) and Chapter III Article 8–15 titles once at EUR-Lex; you do not need the full text yet.
2. Chapter `02`, then read Articles 9, 10, 11, 12, 13, 14, 15 in EUR-Lex end-to-end. Annex III, IV, V immediately after. This is the *anchor* — every other chapter refers back to it. Start exercise `01` when you can walk the article-by-article deliverable table from memory.
3. Chapters `03` and `04` as a pair. NIST AI 100-1 in one sitting; the Playbook is a lookup reference, not a read-through. ISO/IEC 42001 clauses 4–10 in one sitting; the method-standards (23894, 42005, 25059, 24029-2) are opened per row as you cross-tag. Exercises `02` and `03` execute the crosswalks.
4. Chapter `05` alongside the Colorado SB24-205 text and the NYC DCWP LL 144 rule. The CFPB circulars are short — read them end-to-end. The EEOC guidance documents are also short — read at least the 2023 Title VII AI guidance end-to-end. Exercise `04` extends the map with the US-side rows.
5. Chapter `06`. Do *not* try to master all seven jurisdictions at once — read the sections for the ones your invented system actually touches, and skim the rest. Exercise `05` walks a scoped subset.
6. Chapter `07` alongside the AI Verify Foundation site and (for GenAI systems) the MGF-GenAI PDF. Look at the AI Verify Toolkit repository at least once to understand what a technical-test entry looks like. Exercise `06` closes the module.
7. Chapter `08` at the end. The schema falls into place once you know what every column is carrying. This chapter is also the reference to return to when you author your own map's schema in a real programme.

You are not expected to memorise every clause number or article sub-paragraph. You are expected to know which body owns each artefact, which article of the EU AI Act shapes which obligation, and to be able to look up the exact identifier confidently when the map cites it.
