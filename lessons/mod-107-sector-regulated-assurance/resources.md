# Resources for mod-107-sector-regulated-assurance

Primary sources first. Every URL below points at the organisation that issues or hosts the instrument — the federal register, the supervisor's own page, the standards body, the agency's guidance library — so your reading pins to text that survives editorial rewrites. Secondary reading, thematic communications, and vendor documentation sit at the bottom.

## U.S. banking model risk (chapter `01`)

### The anchor guidance

- [Federal Reserve SR 11-7 — *Guidance on Model Risk Management*](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — 2011-04-04. The originating U.S. supervisory letter; the joint OCC/Fed reference.
- [OCC Bulletin 2011-12 — *Sound Practices for Model Risk Management*](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — 2011-04-04. OCC's identical-in-substance companion.
- [FDIC FIL-22-2017 — *Model Risk Management*](https://www.fdic.gov/news/financial-institution-letters/2017/fil17022.html) — FDIC's 2017 adoption of the same guidance for FDIC-supervised institutions.

### Related supervisory background on model risk

- [Federal Reserve *Supervision and Regulation Report* (semiannual)](https://www.federalreserve.gov/publications/supervision-and-regulation-report.htm) — periodic reporting on supervisory focus, including on model risk.
- [OCC *Semiannual Risk Perspective*](https://www.occ.gov/publications-and-resources/publications/semiannual-risk-perspective/index-semiannual-risk-perspective.html) — periodic OCC statement of emerging risks, with recent editions calling out AI/ML risks in banks.
- [Basel Committee on Banking Supervision — *Newsletter on artificial intelligence and machine learning*](https://www.bis.org/publ/bcbs_nl30.htm) — Basel-level thematic communication on AI/ML in prudential supervision.
- [Bank of England / PRA — *Model risk management principles for banks* (SS1/23)](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss123) — the UK PRA's supervisory statement on MRM, useful as a cross-Atlantic comparator.

## U.S. banking third-party risk (chapter `02`)

- [*Interagency Guidance on Third-Party Relationships: Risk Management* (2023)](https://www.federalreserve.gov/newsevents/pressreleases/files/bcreg20230606a1.pdf) — 2023-06-06 joint Fed / OCC / FDIC guidance. The lifecycle text.
- [Federal Reserve SR 23-4 — announcement letter](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm) — 2023-06-06. The Fed's SR letter announcing the joint guidance and rescinding SR 13-19 / CA 13-21.
- [OCC Bulletin 2023-17](https://www.occ.gov/news-issuances/bulletins/2023/bulletin-2023-17.html) — OCC's announcement.
- [FDIC FIL-29-2023](https://www.fdic.gov/news/financial-institution-letters/2023/fil23029.html) — FDIC's announcement.
- [OCC — *Community Bank Guide to the Interagency Third-Party Risk Management Guidance* (2024)](https://www.occ.gov/publications-and-resources/publications/community-affairs/community-developments-insights/pub-insights-community-bank-guide-to-the-interagency-third-party-risk-management-guidance.html) — the proportionality read for smaller institutions.
- [Federal Reserve June 2021 *Request for Information on Financial Institutions' Use of Artificial Intelligence*](https://www.federalreserve.gov/newsevents/pressreleases/files/bcreg20210331a1.pdf) — the interagency RFI whose responses informed subsequent guidance direction.

### Foundation-model vendor documentation the SR 23-4 due-diligence package reads to

- [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/) — the four tracked risk categories and tier decisions the customer-side due diligence reads.
- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — the AI Safety Level (ASL) tier framework.
- [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — Critical Capability Levels.
- [Meta Frontier AI Framework](https://ai.meta.com/static-resource/meta-frontier-ai-framework/) — release-decision framing.
- [SOC 2 (Trust Services Criteria) at AICPA](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2) — the assurance report the due-diligence package expects for a critical vendor.
- [FedRAMP](https://www.fedramp.gov/) — the U.S. federal-government cloud authorisation programme; increasingly a due-diligence input for critical arrangements even outside federal use.
- [ISO/IEC 27001:2022 — *Information security management systems*](https://www.iso.org/standard/27001) — the ISMS certification the due-diligence package typically references.

## FDA — AI/ML medical devices (chapter `03`)

### GMLP guiding principles

- [FDA — *Good Machine Learning Practice for Medical Device Development: Guiding Principles*](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the joint FDA / Health Canada / MHRA October 2021 publication. The 10 principles landing page.
- [Health Canada — *Good Machine Learning Practice*](https://www.canada.ca/en/health-canada/services/drugs-health-products/medical-devices/artificial-intelligence-machine-learning/good-machine-learning-practice.html) — the Health Canada companion landing page.
- [MHRA — Software and AI as a Medical Device](https://www.gov.uk/government/publications/software-and-ai-as-a-medical-device-change-programme) — the UK regulator's SaMD programme, including its GMLP alignment.
- [FDA / Health Canada / MHRA — *Predetermined Change Control Plans for Machine Learning-Enabled Medical Devices: Guiding Principles*](https://www.fda.gov/medical-devices/software-medical-device-samd/predetermined-change-control-plans-machine-learning-enabled-medical-devices-guiding-principles) — the joint 2023 principles supplement.
- [FDA / Health Canada / MHRA — *Transparency for Machine Learning-Enabled Medical Devices: Guiding Principles*](https://www.fda.gov/medical-devices/software-medical-device-samd/transparency-machine-learning-enabled-medical-devices-guiding-principles) — joint transparency principles.

### PCCP final guidance

- [FDA — *Predetermined Change Control Plans for Artificial Intelligence-Enabled Device Software Functions*](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions) — the December 2024 final guidance landing page.
- [FDA — *Marketing Submission Recommendations for a Predetermined Change Control Plan*](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial) — earlier FDA guidance recommending PCCP content in marketing submissions.
- [Food and Drug Omnibus Reform Act of 2022 — FD&C Act §515C](https://www.congress.gov/bill/117th-congress/house-bill/2617/text) — the statute authorising PCCP.

### Device pathways and adjacent standards

- [FDA — *Software as a Medical Device (SaMD)*](https://www.fda.gov/medical-devices/digital-health-center-excellence/software-medical-device-samd) — the SaMD framework landing page.
- [FDA — Digital Health Center of Excellence](https://www.fda.gov/medical-devices/digital-health-center-excellence) — DHCoE landing page.
- [FDA — AI/ML-Enabled Medical Devices list](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-aiml-enabled-medical-devices) — the running list of authorised AI/ML-enabled devices.
- [IMDRF — *Software as a Medical Device: Possible Framework for Risk Categorization and Corresponding Considerations*](https://www.imdrf.org/documents/software-medical-device-possible-framework-risk-categorization-and-corresponding-considerations) — the SaMD risk categorisation IMDRF publication.
- [IMDRF — *Machine Learning-enabled Medical Devices — A subset of Artificial Intelligence-enabled Medical Devices: Key Terms and Definitions*](https://www.imdrf.org/documents/machine-learning-enabled-medical-devices-key-terms-and-definitions) — IMDRF terminology.
- [ISO 14971:2019 — *Medical devices — Application of risk management to medical devices*](https://www.iso.org/standard/72704.html) — the device risk-management standard.
- [IEC 62304:2006+AMD1:2015 — *Medical device software — Software life cycle processes*](https://www.iec.ch/publications/international-standard-medical-device-software-software-life-cycle-processes) — the device software lifecycle standard.
- [IEC 81001-5-1:2021 — *Health software and health IT systems safety, effectiveness and security — Activities in the product life cycle*](https://www.iec.ch/publications/international-standard-part-5-1-security-activities-in-the-product-life-cycle) — the security-activities standard often cited alongside IEC 62304.
- [21 CFR Part 820 — *Quality System Regulation*](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfcfr/CFRSearch.cfm?CFRPart=820) — the U.S. device quality-system regulation.
- [Regulation (EU) 2017/745 — *Medical Device Regulation (MDR)*](https://eur-lex.europa.eu/eli/reg/2017/745/oj) — the EU medical-device regulation.
- [Regulation (EU) 2017/746 — *In Vitro Diagnostic Regulation (IVDR)*](https://eur-lex.europa.eu/eli/reg/2017/746/oj) — the EU IVD regulation.

## EU financial-sector operational resilience — DORA (chapter `04`)

### The regulation

- [Regulation (EU) 2022/2554 — *Digital Operational Resilience Act (DORA)*](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) — the Level-1 text. Entered into force 2023-01-16; applicable 2025-01-17.
- [Delegated Regulation (EU) 2024/1502 — criteria for designation of critical ICT third-party service providers](https://eur-lex.europa.eu/eli/reg_del/2024/1502/oj) — the Article 31 designation criteria delegated act.

### The ESAs' DORA implementation

- [ESMA — Digital Operational Resilience Act (DORA)](https://www.esma.europa.eu/esmas-activities/digital-finance-and-innovation/digital-operational-resilience-act-dora) — the ESAs' landing page for DORA implementation, RTS/ITS, and Q&A.
- [EBA — DORA landing page](https://www.eba.europa.eu/regulation-and-policy/digital-operational-resilience-act) — the EBA's DORA workstream.
- [EIOPA — DORA landing page](https://www.eiopa.europa.eu/browse/regulation-and-policy/digital-operational-resilience-act-dora_en) — the EIOPA's DORA workstream.
- [Joint Committee of the ESAs](https://www.esma.europa.eu/esmas-activities/joint-committee) — the ESAs' joint work on cross-sectoral topics, including DORA RTS/ITS.

### Adjacent EU financial-sector references

- [Directive 2013/36/EU (CRD IV)](https://eur-lex.europa.eu/eli/dir/2013/36/oj) and [Regulation (EU) 575/2013 (CRR)](https://eur-lex.europa.eu/eli/reg/2013/575/oj) — the EU capital-requirements regime whose internal-models approach interfaces with model risk.
- [Directive 2014/65/EU (MiFID II)](https://eur-lex.europa.eu/eli/dir/2014/65/oj) and [Regulation (EU) 600/2014 (MiFIR)](https://eur-lex.europa.eu/eli/reg/2014/600/oj) — the EU investment-services regime whose conduct rules the ESMA overlay applies to AI.
- [Directive 2009/138/EC (Solvency II)](https://eur-lex.europa.eu/eli/dir/2009/138/oj) — the EU insurance solvency regime the EIOPA overlay sits inside.

## Supervisory overlays (chapter `05`)

### European sectoral supervisors

- [ECB Banking Supervision](https://www.bankingsupervision.europa.eu/) — the ECB SSM landing page.
- [ECB — *Guide to internal models*](https://www.bankingsupervision.europa.eu/ecb/pub/pdf/ssm.guidetointernalmodels_consolidated_202310~ac89c7cb2f.en.pdf) — the current consolidated version of the ECB Guide to internal models. <!-- needs-research: confirm this URL points at the current consolidated edition; the ECB updates the Guide periodically -->
- [EIOPA — Artificial Intelligence workstream](https://www.eiopa.europa.eu/browse/regulation-and-policy/artificial-intelligence_en) — the EIOPA's AI-in-insurance publications and consultations.
- [EIOPA — *Artificial Intelligence Governance Principles: Towards Ethical and Trustworthy Artificial Intelligence in the European Insurance Sector* (Consultative Expert Group on Digital Ethics in Insurance, 2021)](https://www.eiopa.europa.eu/document/download/e7c4dfc9-25be-4bd9-95e6-9c9c7f8c4d1f_en) — the 2021 six-principles report. <!-- needs-research: confirm exact URL; EIOPA occasionally moves PDFs when reorganising its documents library -->
- [ESMA — Artificial Intelligence landing page](https://www.esma.europa.eu/esmas-activities/investors-and-issuers/artificial-intelligence) — the ESMA's AI-in-investment-services publications.
- [ESMA — *Public statement on the use of Artificial Intelligence in the provision of retail investment services*](https://www.esma.europa.eu/document/public-statement-use-artificial-intelligence-provision-retail-investment-services) — a representative ESMA supervisory-convergence statement on AI. <!-- needs-research: verify current title/URL; ESMA statements on AI are updated periodically -->
- [European Data Protection Board (EDPB)](https://www.edpb.europa.eu/edpb_en) — for GDPR-side AI opinions and guidance the release-package cross-references.

### U.S. federal banking agencies — thematic communications

- [OCC — Bulletins index](https://www.occ.gov/news-issuances/bulletins/index-bulletins.html) — OCC bulletin index for interagency and OCC-specific communications.
- [FDIC — Financial Institution Letters](https://www.fdic.gov/news/financial-institution-letters/index.html) — FDIC FIL index.
- [Federal Reserve — Supervision and Regulation Letters](https://www.federalreserve.gov/supervisionreg/srletters/srletters.htm) — Fed SR letters.
- [Federal Financial Institutions Examination Council (FFIEC)](https://www.ffiec.gov/) — the interagency coordinating body; publishes joint booklets that include IT and third-party topics.

### National competent authorities — representative pointers

- [BaFin — Artificial Intelligence topic page](https://www.bafin.de/EN/DieBaFin/AktivitaetenAusUndInland/InternationaleZusammenarbeit/KuenstlicheIntelligenz/kuenstliche_intelligenz_node_en.html) — the German BaFin's AI page. <!-- needs-research: confirm current URL; BaFin's page structure changes -->
- [AMF — Fintech and Innovation](https://www.amf-france.org/en/professionals/fintech) — French AMF fintech and innovation.
- [ACPR — Innovation](https://acpr.banque-france.fr/en/innovation) — French ACPR innovation.
- [FCA — Artificial Intelligence](https://www.fca.org.uk/firms/artificial-intelligence-ai) — UK FCA AI page.
- [Bank of Italy — Innovation and payments](https://www.bancaditalia.it/compiti/vigilanza/normativa/index.html?com.dotmarketing.htmlpage.language=1) — Bank of Italy supervisory-guidance landing.

## Consumer-facing overlays (chapter `06`)

### CFPB circulars and adjacent guidance

- [CFPB Circulars series](https://www.consumerfinance.gov/compliance/circulars/) — the circulars index.
- [CFPB Circular 2022-03 — *Adverse action notification requirements in connection with credit decisions based on complex algorithms*](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/).
- [CFPB Circular 2023-03 — *Adverse action notification requirements and the proper use of the CFPB's sample forms provided in Regulation B*](https://www.consumerfinance.gov/compliance/circulars/circular-2023-03/).
- [CFPB Circular 2022-06 — *Unfair and Deceptive Acts or Practices in connection with the use of consumer data*](https://www.consumerfinance.gov/compliance/circulars/circular-2022-06-unfair-and-deceptive-acts-or-practices-that-impede-consumer-reviews/). <!-- needs-research: verify the 2022-06 circular URL and title -->
- [Equal Credit Opportunity Act (ECOA), 15 U.S.C. §1691](https://www.law.cornell.edu/uscode/text/15/chapter-41/subchapter-IV) — the underlying statute.
- [Regulation B, 12 CFR Part 1002](https://www.consumerfinance.gov/rules-policy/regulations/1002/) — ECOA's implementing regulation.

### EEOC and ADA / Title VII

- [EEOC — Artificial Intelligence and Algorithmic Fairness Initiative](https://www.eeoc.gov/ai) — the EEOC AI landing page.
- [EEOC — *The Americans with Disabilities Act and the Use of Software, Algorithms, and Artificial Intelligence to Assess Job Applicants and Employees* (2022)](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence) — the 2022 ADA technical assistance.
- [EEOC — *Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence Used in Employment Selection Procedures Under Title VII of the Civil Rights Act of 1964* (2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) — the 2023 Title VII technical assistance.
- [Uniform Guidelines on Employee Selection Procedures (UGESP), 29 CFR Part 1607](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607) — the interagency selection-procedures guidelines EEOC's adverse-impact analysis reads to.
- [Americans with Disabilities Act (ADA), 42 U.S.C. §12101](https://www.ada.gov/law-and-regs/ada/) — the ADA landing page.
- [Title VII of the Civil Rights Act of 1964, 42 U.S.C. §2000e](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964) — Title VII on the EEOC page.

### Adjacent U.S. consumer and state law

- [HUD — Fair Housing Act guidance on algorithmic tenant-screening](https://www.hud.gov/program_offices/fair_housing_equal_opp) — the HUD Fair Housing landing page. <!-- needs-research: verify current specific HUD guidance URLs on algorithmic tools in tenant screening; HUD reorganises its guidance library periodically -->
- [NYC Department of Consumer and Worker Protection — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — LL 144 landing page.
- [Illinois Artificial Intelligence Video Interview Act (820 ILCS 42)](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=4015) — IL AIVIA text.
- [Colorado SB 24-205 — *Consumer Protections for Artificial Intelligence*](https://leg.colorado.gov/bills/sb24-205) — Colorado's high-risk AI act.
- [California Privacy Rights Act (CPRA / CCPA)](https://oag.ca.gov/privacy/ccpa) — CCPA / CPRA landing; the CPPA's automated-decision-making rulemaking is tracked here.

## Vendor platforms cited in chapter `06`

Every vendor claim from chapter `06` is provisional and should be re-verified against the vendor's own current documentation before it is cited in a release-package.

- [ModelOp](https://www.modelop.com/) — model operations and governance platform.
- [Monitaur](https://www.monitaur.ai/) — Governance OS.
- [Fiddler AI](https://www.fiddler.ai/) — model observability and monitoring.
- [Domino Data Lab — Model Monitor / Governance](https://domino.ai/) — an adjacent MLOps + governance platform commonly evaluated alongside the three named platforms.
- [DataRobot — MLOps and AI Governance](https://www.datarobot.com/) — adjacent MLOps + governance platform.
- [Credo AI](https://www.credo.ai/) — AI governance and compliance platform.
- [Arize AI](https://arize.com/) — ML observability platform.
- [WhyLabs](https://whylabs.ai/) — ML monitoring and observability.

Read each vendor's own current documentation for the sector-specific templates (SR 11-7 tiering, DORA register-of-information entries, PCCP components) they support, and confirm the current state of the AI-specific extensions (foundation-model tracking, prompt-versioning, judge-model management) they claim.

## Adjacent standards the release-package cites in passing

- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal U.S. framework the sector-regulated shape braids with.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — GenAI-specific risk categories.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS management-system standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance.
- [ISO/IEC 42005:2025 — *AI system impact assessment*](https://www.iso.org/standard/42005) — the impact-assessment standard.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the EU horizontal AI regulation; sector obligations braid with it for EU deployments.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.

## Suggested reading order for this module

1. Chapter `01`, then read SR 11-7 and OCC 2011-12 end-to-end in one sitting. If you have not internalised the three-lines-of-defence shape and the six SR-11-7 elements, the rest of the module will float.
2. Chapter `02`, then read the 2023 Interagency Guidance on Third-Party Relationships. Skim SR 23-4 alongside. Draft the seven-item contract-clause fight list against a foundation-model provider you know.
3. Chapter `03`, then read the FDA GMLP guiding-principles page and the PCCP final guidance December 2024. Skim IMDRF SaMD risk categorisation if the medical-device space is new to you. Exercise `02` executes the shape.
4. Chapter `04`, then read DORA Articles 5–16 and 28–44 directly. The RTS/ITS remain reference; you do not need to memorise their content. Exercise `03` produces the Article 30(3) clause set.
5. Chapter `05` alongside the ECB, EIOPA, ESMA landing pages. The overlays shift often; the chapter is written to survive that. Exercise `04` produces the applicability memos and the watch-list-currency statement.
6. Chapter `06`, then read the CFPB Circulars 2022-03 and 2023-03 and the EEOC 2022 and 2023 technical-assistance documents directly. Skim one vendor platform's own current documentation. Exercise `05` produces the consumer-facing-overlay row and the vendor-coverage map.

You are not expected to memorise every article number or bulletin identifier. You are expected to know which sector regulator owns each instrument, what the release-package artefacts look like against each, and to be able to look up the exact identifier confidently when a release-package body needs to cite it.
