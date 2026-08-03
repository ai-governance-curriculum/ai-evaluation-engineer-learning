# Resources for mod-109-third-party-evaluator-and-auditor-interface

Primary sources first. Every URL below points at the organisation that issues, hosts, or operates the instrument — the safety institute's home page, the standards body, the regulator's rule text, the accountancy standard-setter's publications, the benchmark's canonical URL — so your reading pins to text that survives editorial rewrites. Secondary reading, thematic commentary, and vendor documentation sit at the bottom.

The load-bearing reads for this module differ per chapter. Chapter `01`'s load-bearing reads are the sovereign AI-safety-institute home pages and the `Inspect` framework; chapter `02`'s is the consolidated Regulation (EU) 2024/1689 text and ISO/IEC 42006:2025; chapter `03`'s is the NYC DCWP rule text and guidance; chapter `04`'s is ISAE 3000 (Revised); chapter `05`'s is the current FRVT/FRTE round; chapter `06`'s cites the reference materials from the four interface-specific chapters. If you read nothing else, read one AISI-shape institute's home page end-to-end plus either the EU AI Act Article 43 / Annex VII text or the DCWP AEDT rule text — the two together give the interface range this module covers.

## Chapter `01` — AISI-shape third-party evaluators

### The sovereign and quasi-sovereign institutes

- [UK AI Security Institute (formerly UK AI Safety Institute)](https://www.aisi.gov.uk/) — the UK AISI landing page. <!-- needs-research: verify current site content post-2025 rebrand from AI Safety Institute to AI Security Institute. -->
- [UK AISI — `Inspect` framework](https://inspect.aisi.org.uk/) — the open-source evaluation framework increasingly used as the shared substrate across AISI-shape engagements.
- [UK AISI — `Inspect` GitHub organisation](https://github.com/UKGovernmentBEIS/inspect_ai) — the `Inspect` framework's source repository. <!-- needs-research: verify current canonical GitHub org / repo path post-DSIT reorganisation. -->
- [US AI Safety Institute (NIST)](https://www.nist.gov/aisi) — the US AISI landing page.
- [US AISI — AI Safety Institute Consortium (AISIC)](https://www.nist.gov/aisi/artificial-intelligence-safety-institute-consortium-aisic) — the AISIC coordination page. <!-- needs-research: verify current AISIC membership scope and any 2025-2026 changes to the consortium's operational scope. -->
- [International Network of AI Safety Institutes — Commerce announcement](https://www.commerce.gov/news/press-releases/2024/11/first-ever-international-network-ai-safety-institutes-set-launch-san) — the multilateral network's launch announcement.
- [Singapore AI Verify Foundation](https://aiverifyfoundation.sg/) — the AI Verify Foundation home page.
- [Singapore AI Verify Foundation — testing framework and toolkit](https://aiverifyfoundation.sg/ai-verify/) — the framework and toolkit page. <!-- needs-research: verify current URL structure for the AI Verify framework page. -->

### The independent research organisations

- [METR (Model Evaluation and Threat Research)](https://metr.org/) — METR's home page.
- [METR — research publications](https://metr.org/research) — METR's methodology publications. <!-- needs-research: verify current URL for the METR research index. -->
- [Apollo Research](https://www.apolloresearch.ai/) — Apollo Research's home page.
- [Apollo Research — publications](https://www.apolloresearch.ai/research) — Apollo's evaluations publications page. <!-- needs-research: verify current URL for the Apollo Research publications index. -->
- [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/) — the working-group home.
- [MLCommons AI Safety benchmark (AILuminate)](https://mlcommons.org/benchmarks/ai-safety/) — the AILuminate benchmark home. <!-- needs-research: verify current URL structure for AILuminate and any 2025-2026 versioning. -->

### Frontier-lab publications the AISI-shape interface interlocks with

- [Anthropic — Responsible Scaling Policy](https://www.anthropic.com/rsp) — the current RSP landing page.
- [OpenAI — Safety and Preparedness](https://openai.com/safety/preparedness/) — the Preparedness Framework landing page.
- [Google DeepMind — Frontier Safety Framework announcement](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — the FSF announcement blog.
- [Frontier Model Forum](https://www.frontiermodelforum.org/) — the FMF landing page.
- [UK Government — Frontier AI Safety Commitments (Seoul Summit)](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — the 16-company Frontier AI Safety Commitments text.

## Chapter `02` — Notified-body conformity assessment

### EU AI Act primary sources

- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the consolidated Regulation text. Articles 11 (technical documentation), 17 (QMS), 30 (designating authorities and notified bodies), 31 (requirements relating to notified bodies), 43 (conformity assessment procedures), 47 (EU declaration of conformity), 55 (GPAI systemic-risk), 72 (post-market monitoring), Annex III (high-risk AI systems), Annex IV (technical documentation), and Annex VII (conformity assessment based on assessment of QMS and technical documentation) are the specific citations this chapter uses.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office landing page.
- [European Commission — NANDO register](https://ec.europa.eu/growth/tools-databases/nando/) — the New Approach Notified and Designated Organisations register. <!-- needs-research: verify current NANDO URL and confirm AI Act notified bodies are listed there rather than under a separate register. -->
- [European Commission — AI Act implementing acts and guidance](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the AI Act policy hub for implementing acts and guidance.

### ISO/IEC standards the notified-body regime cross-references

- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard whose clauses 4–10 the Article 17 QMS documentation converges on.
- [ISO/IEC 42006:2025 — *Requirements for bodies providing audit and certification of AI management systems*](https://www.iso.org/standard/44546.html) — the certification-body standard the notified body's AIMS-scope accreditation is against. <!-- needs-research: verify published status and current version of ISO/IEC 42006:2025. -->
- [ISO/IEC 17065 — *Conformity assessment — Requirements for bodies certifying products, processes and services*](https://www.iso.org/standard/46568.html) — the horizontal certification-body standard.
- [ISO/IEC 17020 — *Conformity assessment — Requirements for the operation of various types of bodies performing inspection*](https://www.iso.org/standard/52994.html) — the inspection-body standard, referenced by some notified-body accreditations.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance the Article 9 risk-management system frequently applies.
- [ISO/IEC 24029-2:2023 — *AI — Assessment of the robustness of neural networks*](https://www.iso.org/standard/79804.html) — the neural-network robustness assessment standard. <!-- needs-research: verify current status of Part 2 publication. -->
- [ISO/IEC 25059:2023 — *SQuaRE — Quality model for AI systems*](https://www.iso.org/standard/80655.html) — the AI-system quality model.

### Adjacent EU frameworks

- [European Accreditation](https://european-accreditation.org/) — EA is the accreditation bodies' coordinating body; its publications inform how national accreditation bodies designate notified bodies.
- [European Commission — CE marking landing page](https://single-market-economy.ec.europa.eu/single-market/ce-marking_en) — the horizontal CE-marking framework the AI Act's conformity-assessment regime imports its shape from. <!-- needs-research: verify current URL for the CE-marking landing page. -->

## Chapter `03` — NYC Local Law 144 (AEDT) independent bias audit

### DCWP primary sources

- [NYC DCWP — Automated Employment Decision Tools hub](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the DCWP AEDT information hub for employers, employment agencies, candidates, and auditors.
- [NYC Rules — Automated Employment Decision Tools rule text](https://rules.cityofnewyork.us/rule/automated-employment-decision-tools-updated/) — the DCWP final rule text. <!-- needs-research: verify current published rule URL and any post-2024 amendments. -->
- [NYC Council — Local Law 144 of 2021 (Int. 1894-2020)](https://legistar.council.nyc.gov/LegislationDetail.aspx?ID=4344524) — the enacting Local Law. <!-- needs-research: verify current URL on NYC Council Legistar. -->

### Related US and international regimes the AEDT shape prefigures

- [Colorado Consumer Protections for Artificial Intelligence (SB 24-205)](https://leg.colorado.gov/bills/sb24-205) — the Colorado AI Act (Consumer Protections for Artificial Intelligence). <!-- needs-research: verify current status, effective date, and any 2025-2026 amendments; effective-date has been amended. -->
- [Illinois Artificial Intelligence Video Interview Act (820 ILCS 42)](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=4015) — Illinois's AI-in-video-interview statute, a US antecedent to LL144's use-case-scoped shape.
- [EEOC — Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence Used in Employment Selection Procedures Under Title VII](https://www.eeoc.gov/laws/guidance/assessing-adverse-impact-software-algorithms-and-artificial-intelligence-used) — the EEOC technical assistance document on adverse-impact assessment for AI in employment selection.
- [Uniform Guidelines on Employee Selection Procedures (29 CFR Part 1607)](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607) — the horizontal Uniform Guidelines, source of the "four-fifths rule" heritage the LL144 impact ratio inherits.
- [EU AI Act — Annex III point 4 (employment, workers' management and access to self-employment)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the EU high-risk hiring category adjacent to the AEDT-shape audit.

### Statistical-methodology background

- [EEOC — Adverse Impact Analysis / Four-Fifths Rule (Questions and Answers)](https://www.eeoc.gov/laws/guidance/questions-and-answers-clarify-and-provide-common-interpretation-uniform-guidelines) — the Q&A document that clarifies the four-fifths rule's application. <!-- needs-research: verify current URL for the Q&A document. -->

## Chapter `04` — Big-Four AI-assurance engagements

### Assurance-engagement standards

- [IAASB — International Standard on Assurance Engagements (ISAE) 3000 (Revised)](https://www.iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or) — the IAASB standard for non-financial assurance engagements outside the US.
- [IAASB — International Standards on Assurance Engagements landing page](https://www.iaasb.org/standards-pronouncements) — the IAASB standards hub.
- [AICPA — Statements on Standards for Attestation Engagements (SSAEs)](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-standards-and-statements) — the AICPA attestation-standards hub. <!-- needs-research: verify current URL under the merged AICPA-CIMA site and confirm SSAE 21 remains current for direct examination engagements. -->
- [AICPA — SOC 2 examination framework](https://www.aicpa-cima.com/resources/landing/system-and-organization-controls-soc-suite-of-services) — the SOC-suite landing page, relevant background for the SOC 2-adjacent AI-control examinations chapter `04` references. <!-- needs-research: verify current AICPA-CIMA URL for the SOC-suite landing. -->

### Big-Four AI-assurance product pages

Vendor product naming shifts frequently; the following pages are the most-stable entry points as of authoring, but confirm current naming before citing.

- [Deloitte — Trustworthy AI](https://www2.deloitte.com/us/en/pages/deloitte-analytics/solutions/ethics-of-ai-framework.html) — Deloitte's Trustworthy AI framework page. <!-- needs-research: verify current URL and confirm product naming for the Deloitte AI Assurance practice. -->
- [PwC — Responsible AI](https://www.pwc.com/gx/en/services/consulting/technology/responsible-ai.html) — PwC's Responsible AI page. <!-- needs-research: verify current URL and confirm Responsible AI is the current umbrella brand. -->
- [EY — Trusted AI and EY.ai](https://www.ey.com/en_gl/ai) — EY's AI page. <!-- needs-research: verify current URL and confirm EY.ai / Trusted AI branding is current. -->
- [KPMG — Trusted AI](https://kpmg.com/xx/en/what-we-do/services/kpmg-trusted-ai.html) — KPMG's Trusted AI page. <!-- needs-research: verify current URL and confirm the KPMG AI in Control naming for the associated framework. -->
- [Accenture — Responsible AI](https://www.accenture.com/us-en/services/applied-intelligence/ai-ethics-governance) — Accenture's Responsible AI page. <!-- needs-research: verify current URL and confirm Accenture's positioning as advisory-only vs any attest offering. -->

### Criteria sets the attest opinions typically reference

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST AI RMF landing.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific profile.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard for control-effectiveness attest engagements against ISO/IEC 42001.

## Chapter `05` — FRVT / FRTE as precedent

### NIST FRVT / FRTE

- [NIST — Face Recognition Vendor Test (FRVT)](https://www.nist.gov/itl/iad/image-group/face-recognition-vendor-test-frvt) — the FRVT programme landing page. <!-- needs-research: verify current NIST URL structure and confirm the FRVT-to-FRTE naming transition. -->
- [NIST FRVT ongoing-results publication](https://pages.nist.gov/frvt/) — the ongoing-results publication page. <!-- needs-research: verify current results-publishing URL and the current track structure. -->
- [NIST — FRVT Part 3: Demographic Effects (NISTIR 8280, 2019)](https://doi.org/10.6028/NIST.IR.8280) — the 2019 demographic-differentials report that reshaped the vendor market.
- [NIST — Face Recognition Technology Evaluation (FRTE) programme continuation](https://www.nist.gov/programs-projects/face-analysis-technology-evaluation-fate) — the FRTE / FATE programme continuation. <!-- needs-research: verify current URL and confirm the naming convention. -->

### Adjacent NIST biometric-recognition evaluations (the portfolio)

- [NIST — Speaker Recognition Evaluation (SRE)](https://www.nist.gov/itl/iad/mig/speaker-recognition) — the speaker-recognition analogue.
- [NIST — Iris Exchange (IREX)](https://www.nist.gov/programs-projects/iris-exchange-irex-overview) — the iris-recognition analogue.
- [NIST — Fingerprint Vendor Technology Evaluation lineage](https://www.nist.gov/programs-projects/fingerprint-vendor-technology-evaluation-fpvte-2012) — the fingerprint analogue. <!-- needs-research: verify current programme naming and status. -->

## Chapter `06` — Delivery timing, envelope, and evidence hardening

Chapter `06` is a synthesis of chapters `01`–`05`; its citations are largely to the reference materials in the four interface-specific chapters. Additional references for the operating-procedure content:

- [`in-toto` attestation framework](https://in-toto.io/) — the attestation framework the four hardening practices reference.
- [Sigstore project — DSSE (Dead Simple Signing Envelope)](https://github.com/secure-systems-lab/dsse) — the signing-envelope format.
- [Sigstore project — Rekor transparency log](https://docs.sigstore.dev/logging/overview/) — the transparency-log the return-artefact ingestion cites where evaluators publish to a log.
- [SLSA — Supply-chain Levels for Software Artifacts](https://slsa.dev/) — the SLSA framework the ML-BOM packaging aligns with.
- [SPDX — Software Package Data Exchange](https://spdx.dev/) — the SPDX package-metadata format the ML-BOM packaging uses.

## Horizontal frameworks all chapters braid with

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST framework.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the horizontal EU AI regulation.

## Adjacent module cross-references

- [`mod-101-release-assurance-position`](../mod-101-release-assurance-position/) — the release-assurance methodology owner's position and the deferral contract that names the external-parties row.
- [`mod-102-assurance-case-engineering`](../mod-102-assurance-case-engineering/) — the assurance case that third-party reports enter as external-evaluator leaves with validity windows.
- [`mod-103-release-gate-architecture`](../mod-103-release-gate-architecture/) — the release-gate the third-party report has to arrive in time to inform.
- [`mod-104-evaluation-evidence-pipeline`](../mod-104-evaluation-evidence-pipeline/) — the evidence pipeline whose maturity determines the cost and feasibility of every third-party engagement.
- [`mod-105-cards-for-external-audiences`](../mod-105-cards-for-external-audiences/) — the derived external-facing paragraphs that cite the third-party reports.
- [`mod-106-cross-jurisdictional-obligation-mapping`](../mod-106-cross-jurisdictional-obligation-mapping/) — the per-jurisdiction obligation map that pins which third-party engagement types are mandated where.
- [`mod-107-sector-regulated-assurance`](../mod-107-sector-regulated-assurance/) — the sector-regulated overlays where a sector-specific third-party engagement adds obligations to the AISI / notified-body / AEDT / Big-Four base.
- [`mod-108-deployment-tier-gating`](../mod-108-deployment-tier-gating/) — the tier-decision artefact that is one of the seven envelope components.
- [`mod-110-post-market-surveillance`](../mod-110-post-market-surveillance/) — the surveillance plan that carries the certificate-validity re-engagement reminders and the post-market signal feed the third-party reports contribute to.
- [`mod-111-gpai-systemic-risk-assurance`](../mod-111-gpai-systemic-risk-assurance/) — the AI Office's direct supervision of Article 55 GPAI systemic-risk providers, a distinct interface shape.
- [`mod-112-owning-an-assurance-program`](../mod-112-owning-an-assurance-program/) — the operating model that owns the engagement charter as a standing artefact across cycles.

## Suggested reading order for this module

1. Chapter `01`, then read one sovereign AI-safety institute's landing page end-to-end (UK AI Security Institute is the easiest entry point) and the `Inspect` framework page. Exercise `01` designs the AISI handoff envelope.
2. Chapter `02`, then read the consolidated text of Regulation (EU) 2024/1689 for Articles 11, 17, 30, 31, 43, 47, and 72, Annex IV, and Annex VII, plus the ISO/IEC 42006:2025 abstract. Exercise `02` assembles the notified-body Annex VII dossier.
3. Chapter `03`, then read the DCWP AEDT hub and the current published rule text. Exercise `03` prepares the AEDT input-dataset envelope.
4. Chapter `04`, then read the IAASB ISAE 3000 (Revised) landing page and one Big-Four firm's current AI-assurance product page. Exercise `04` scopes the ISAE 3000 (Revised) engagement and defends the attest-vs-advisory split.
5. Chapter `05` alongside the current FRVT/FRTE ongoing-results publication. Exercise `05` reads a current round and designs the next-generation AISI-shape engagement with the five shape lessons applied.
6. Chapter `06` after `01`–`05`. It is the synthesis. It has no dedicated exercise — its content is exercised through the engagement-charter deliverable inside each of exercises `01`–`04`.

You are not expected to memorise every institute's evaluation-track catalogue, every notified body's designated scope, every criteria set's clause numbering, or every FRVT round's methodology annex. You are expected to know which primary source owns each interface's shape, which peer-role registry entries feed each envelope's components, and to look up the specific citations confidently when the engagement's charter needs to reference them.
