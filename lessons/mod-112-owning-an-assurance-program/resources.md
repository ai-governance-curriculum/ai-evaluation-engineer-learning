# Resources for mod-112-owning-an-assurance-program (Owning an Enterprise AI-Evaluation-Assurance Program)

Primary sources first. Every URL below points at the organisation that issues, hosts, or operates the instrument — the standards body's landing page, the regulator's own site, the vendor's product page, the enterprise's public responsible-AI documentation — so your reading pins to text that survives editorial rewrites. Secondary reading and thematic commentary sit at the bottom.

The load-bearing reads for this module differ per chapter. Chapter `01`'s load-bearing reads are [Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) end-to-end (the effective-challenge convention), [ISO/IEC 42001](https://www.iso.org/standard/81230.html) clauses 5 (leadership) and 9.3 (management review), and one framework's public risk-management-programme document (COSO ERM or ISO 31000) as shape reference for the intake-to-decision cycle. Chapter `02`'s are the peer-track role registries the assurance programme contracts with plus the [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) that discipline the AI-eval row. Chapter `03`'s are the [European AI Office landing page](https://digital-strategy.ec.europa.eu/en/policies/ai-office) and the EU AI Act consolidated text (Articles 55, 61, 72, 73, 74) end-to-end, plus [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) GOVERN sub-categories for the risk-appetite tie. Chapter `04`'s are the seven vendor landing pages plus Microsoft's, Google's, and AWS's public responsible-AI standards straight through as shape references. Chapter `05`'s are the [AI Incident Database](https://incidentdatabase.ai/) and the [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents) plus the [MIT AI Risk Repository](https://airisk.mit.edu/) for the categorisation pass. If you read nothing else across the module, read SR 11-7 straight through, then read the current Microsoft Responsible AI Standard, then walk one AIID incident record end-to-end — those three carry the module's governance-methodology backbone.

## Chapter `01` — The operating model and the effective-challenge convention

### The second-line-of-defence pattern

- [Federal Reserve SR 11-7 — *Guidance on Model Risk Management*](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) (2011-04) — the load-bearing reference for the effective-challenge convention this chapter's rotation borrows from. Read the sections on effective challenge, validation independence, and the three-lines-of-defence model straight through.
- [OCC Bulletin 2011-12 — *Sound Practices for Model Risk Management*](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) (2011-04) — the OCC's parallel guidance jointly issued with SR 11-7; the sound-practices language is often read alongside.
- [Federal Reserve SR 23-4 — *Interagency Guidance on Third-Party Relationships: Risk Management*](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm) (2023-06) — extends the SR 11-7 discipline into third-party model risk; relevant when the assurance programme's peer-track contracts include external evaluators or vendor-hosted models.

### AI management-system standards

- [ISO/IEC 42001:2023 — *Information technology — Artificial intelligence — Management system*](https://www.iso.org/standard/81230.html) — the AIMS standard whose clauses discipline the operating-model artefacts. Clause 5 (leadership), clause 7 (support, including 7.5 documented information), clause 8 (operation), clause 9 (performance evaluation, including 9.1 monitoring and 9.3 management review), and Annex A (control objectives) are the specific citations.
- [ISO/IEC 23894:2023 — *Artificial intelligence — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the AI-specific risk-management-process guidance the operating-model handbook's risk-treatment stages sit inside.
- [ISO/IEC 42006:2025 — *Information technology — Artificial intelligence — Requirements for bodies providing audit and certification of artificial intelligence management systems*](https://www.iso.org/standard/44546.html) — the accreditation-body standard the notified-body row in chapter `03` cites into.
- [ISO/IEC 5338:2023 — *AI system life cycle processes*](https://www.iso.org/standard/81118.html) — a companion lifecycle standard useful for pinning the intake-to-decision cycle against a recognised process shape.

### Horizontal risk-management shape

- [COSO — *Enterprise Risk Management: Integrating with Strategy and Performance*](https://www.coso.org/enterprise-risk-management) — the horizontal ERM framework whose *risk-response* language shapes many enterprise assurance programmes' escalation vocabulary. <!-- needs-research: verify current publication URL and the specific COSO ERM update version -->
- [ISO 31000:2018 — *Risk management — Guidelines*](https://www.iso.org/standard/65694.html) — the horizontal risk-management standard whose process shape is the substrate ISO/IEC 23894 profiles for AI.

### Governance-by-record shape

- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the operational elaboration of NIST AI RMF's four functions (GOVERN / MAP / MEASURE / MANAGE), useful as the source of specific sub-category IDs when the operating-model handbook cites the framework by ID.
- [NIST — *Trustworthy and Responsible AI Resource Center* (AIRC)](https://airc.nist.gov/) — the AIRC hub for the framework and profile documents.

## Chapter `02` — The peer-track contract matrix

### Peer-track role registries in this track

Peer-track contracts are with roles the wider AI-governance / AI-engineering / ML-engineering / AI-infrastructure organisation carries. For each peer, read the peer's own role registry (in the paired role-content repository), then read the peer's methodology-of-record documents so the freshness cadence and artefact schema in the matrix are grounded.

- `ai-governance-analyst` (level 15, AI Governance) — intake, inventory, first-draft cards, jurisdictional scoping.
- `ai-risk-engineer` (level 25, AI Governance) — harm models, adversarial evaluation, guardrails, incident-response playbook.
- `ai-eval-engineer` (level 30, AI Engineering) — application-layer eval evidence, online-eval, eval-gated CI/CD, trace-based evidence.
- `model-evaluation-engineer` (level 30, ML Engineering) — statistical framing, benchmarks, calibration, reproducibility bundles.
- `ai-infra-security` (level 35, AI Infrastructure) — eval-set-security, judge supply-chain, model-extraction risk, ML-BOM / SPDX / SLSA / Sigstore.
- `agentic-safety-engineer` (level 40, AI Governance) — frontier-agent capability evidence, autonomy envelope, systemic-risk feed.

### Peer-track methodology substrates

- [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the semantic conventions the AI-eval-engineer row's trace-based evidence conforms to (or documents divergence from). Pin against the current published version at reading time.
- [NIST AI 100-2 — *Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations*](https://doi.org/10.6028/NIST.AI.100-2e2023) — the taxonomy the risk-engineer's adversarial-eval methodology maps into.
- [NIST AI 600-1 — *Generative AI Profile*](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific profile whose twelve categories the harm-inventory and adversarial-eval rows are structured against.
- [MITRE ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems)](https://atlas.mitre.org/) — the MITRE-published knowledge base of adversary tactics against ML systems; complementary to NIST AI 100-2 for the risk-engineer's threat-modelling row.
- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — the OWASP LLM Top 10, useful as a starter checklist for the AI-infra-security row's eval-set-security and prompt-injection attestations. <!-- needs-research: verify current published version at reading time -->

### Supply-chain and signing substrate

- [CycloneDX — *ML-BOM (Machine Learning Bill of Materials)*](https://cyclonedx.org/capabilities/mlbom/) — the ML-BOM specification the infra-security row's supply-chain provenance uses.
- [SPDX — *SPDX-AI profile*](https://spdx.dev/) — the SPDX AI profile the supply-chain provenance row cites into. <!-- needs-research: verify current publication URL and version of the AI profile -->
- [SLSA — *Supply-chain Levels for Software Artifacts*](https://slsa.dev/) — the SLSA framework's provenance-and-verification requirements.
- [Sigstore project](https://www.sigstore.dev/), [Fulcio](https://docs.sigstore.dev/certificate_authority/overview/), and [Rekor transparency log](https://docs.sigstore.dev/logging/overview/) — the signing infrastructure the assurance-bundle signature chain depends on.
- [DSSE — *Dead Simple Signing Envelope*](https://github.com/secure-systems-lab/dsse) — the envelope format signed attestations use.

### Bundle-serialisation substrate

- [RO-Crate specification](https://www.researchobject.org/ro-crate/) — the research-object packaging convention the reproducibility-bundle row often uses.
- [BagIt File Packaging Format (RFC 8493)](https://datatracker.ietf.org/doc/html/rfc8493) — the archival-packaging standard for evidence bundles.
- [OCI Image Format Specification](https://github.com/opencontainers/image-spec) — the OCI substrate that lets bundles ride the same distribution rails as container images.

## Chapter `03` — Interfaces upward and outward

### European AI Office and EU AI Act primary sources

- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office landing page; the enforcement counterparty for GPAI obligations and the coordinating body for the market-surveillance authorities.
- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the consolidated Regulation text. Article 5 (prohibited practices), Article 6 (high-risk classification), Article 9 (risk-management system), Article 11 and Annex IV (technical documentation), Article 22 (authorised representatives), Articles 47 and 48 (declaration of conformity and CE marking), Article 55 (obligations of GPAI providers with systemic risk), Article 56 (invitation to codes of practice), Article 61 (post-market monitoring by providers), Article 72 (post-market monitoring plan), Article 73 (serious-incident reporting), and Article 74 (market-surveillance documentation requests) are the specific citations this module uses.
- [European Commission — AI Act implementing acts and guidance](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the AI Act policy hub for implementing acts and Commission guidance. <!-- needs-research: verify current implementing-acts publication status at reading time -->
- [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the Code of Practice the AI Office / GPAI provider interface is anchored on. <!-- needs-research: verify the current published version -->

### Competent-authority coordination

- [European Commission — list of national competent authorities under the AI Act](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the reference for competent Member State market-surveillance authorities. <!-- needs-research: verify the current publication URL and the current list of Member State competent authorities -->
- [European AI Board](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the coordinating body for national competent authorities; relevant when the assurance programme's interfaces span multiple Member States. <!-- needs-research: verify current publication URL for the AI Board -->

### NIST horizontal framework — GOVERN for the risk-appetite tie

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST AI RMF landing. The GOVERN sub-category GOVERN-1.3 (accountability and risk-tolerance criteria) is the specific tie for the head-of-governance risk-appetite statement.
- [NIST AI RMF Playbook — GOVERN function](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook/GOVERN) — the operational elaboration of GOVERN sub-categories. <!-- needs-research: verify current URL structure for the GOVERN function page -->

### Sector-supervisor primary sources (for the sector-supervisor row)

- [European Central Bank (ECB) — banking supervision](https://www.bankingsupervision.europa.eu/) — the ECB / SSM landing.
- [European Banking Authority (EBA) — guidelines on internal governance](https://www.eba.europa.eu/) — the EBA landing; specific model-risk-management guidance is issued periodically. <!-- needs-research: verify current EBA guidelines on ICT and model risk relevant to AI systems -->
- [European Insurance and Occupational Pensions Authority (EIOPA)](https://www.eiopa.europa.eu/) — the EIOPA landing; relevant when the pinned organisation carries insurance-sector products.
- [European Securities and Markets Authority (ESMA)](https://www.esma.europa.eu/) — the ESMA landing.
- [US Food and Drug Administration (FDA) — Software as a Medical Device (SaMD) / GMLP / PCCP](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-aiml-enabled-medical-devices) — the FDA's AI/ML-enabled medical devices hub; relevant when the pinned organisation carries a healthcare-AI product. <!-- needs-research: verify current URL structure and the current PCCP guidance publication status -->

### DORA and third-party ICT risk

- [Regulation (EU) 2022/2554 — *Digital Operational Resilience Act (DORA)*](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) — the horizontal EU financial-services regulation on ICT and third-party risk, relevant where the assurance programme's peer-contract matrix's supply-chain provenance row interlocks with DORA obligations.

### Independent-auditor and notified-body substrate

- [ISO/IEC 42006:2025 — *Requirements for bodies providing audit and certification of artificial intelligence management systems*](https://www.iso.org/standard/44546.html) — the accreditation-body standard for AIMS certification bodies.
- [ISO/IEC 17021-1:2015 — *Requirements for bodies providing audit and certification of management systems*](https://www.iso.org/standard/61651.html) — the horizontal management-system-audit accreditation standard.

### Sector-adjacent US city / state auditor pathways

- [New York City — Automated Employment Decision Tools (AEDT) — Local Law 144 of 2021](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the reference for independent-auditor engagement in the NYC employment-decisioning context. <!-- needs-research: verify current URL and rule text version -->
- [Colorado SB 24-205 — Artificial Intelligence Consumer Protection Act](https://leg.colorado.gov/) — the Colorado horizontal state AI law with independent-audit implications. <!-- needs-research: verify current URL and effective-date status -->

## Chapter `04` — Build vs buy: the vendor landscape

### The seven vendors named in the chapter

- [Credo AI](https://www.credo.ai/) — governance platform positioning around policy attestation, use-case intake, and multi-framework crosswalking. <!-- needs-research: verify current product surface at reading time -->
- [Holistic AI](https://www.holisticai.com/) — governance platform with bias-and-explainability tooling, inventory, and audit-preparation features. <!-- needs-research: verify current product surface at reading time -->
- [ModelOp Center](https://www.modelop.com/) — model-operations platform with governance overlays, positioned around model inventory, lifecycle workflow, and SR 11-7-shape model-risk management. <!-- needs-research: verify current product surface at reading time -->
- [ServiceNow AI Control Tower](https://www.servicenow.com/) — Now-Platform-native governance surface for AI inventory, risk assessment, and workflow. <!-- needs-research: verify current product name and feature set at reading time -->
- [IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance) — IBM-stack governance product tied into watsonx for lifecycle governance, model-risk workflow, and factsheet generation. <!-- needs-research: verify current product surface at reading time -->
- [Fiddler AI](https://www.fiddler.ai/) — AI observability platform with governance-adjacent features around monitoring, explainability, and evaluation. <!-- needs-research: verify current positioning between observability and governance at reading time -->
- [Monitaur Governance OS](https://www.monitaur.ai/) — governance product positioned around model-risk workflow and evidence capture. <!-- needs-research: verify current product surface at reading time -->

### Hyperscaler-native governance surfaces (adjacent references)

- [AWS SageMaker — model governance](https://aws.amazon.com/sagemaker/ai-governance/) — the SageMaker AI-governance surface. <!-- needs-research: verify current URL structure at reading time -->
- [Azure Machine Learning — Responsible AI dashboard](https://learn.microsoft.com/en-us/azure/machine-learning/concept-responsible-ai-dashboard) — the Azure ML responsible-AI dashboard. <!-- needs-research: verify current URL at reading time -->
- [Google Cloud Vertex AI — Model Registry and Model Cards](https://cloud.google.com/vertex-ai) — the Vertex AI governance surface. <!-- needs-research: verify current governance-specific URLs at reading time -->

### Enterprise responsible-AI reference standards

Read as shape references, not as prior-art to be copied.

- [Microsoft — Responsible AI Standard](https://www.microsoft.com/en-us/ai/principles-and-approach) — Microsoft's public responsible-AI documentation, with impact-assessment templates, fit-for-purpose evaluation, and deployment-readiness checkpoints. <!-- needs-research: verify current version and canonical URL at reading time -->
- [Microsoft — *Impact Assessment Template and Guide*](https://www.microsoft.com/en-us/ai/tools-practices) — the impact-assessment template referenced by the Standard. <!-- needs-research: verify current URL at reading time -->
- [Google — Responsible AI practices](https://ai.google/responsibility/) — Google's public documentation of responsible-AI practices, including the model card and dataset card conventions, evaluation frameworks, and safety-review processes. <!-- needs-research: verify current documentation surface at reading time -->
- [Google — *People + AI Research (PAIR) Guidebook*](https://pair.withgoogle.com/guidebook/) — the PAIR guidebook covering responsible-AI design patterns Google's public documentation cites into.
- [AWS — Responsible AI overview](https://aws.amazon.com/ai/responsible-ai/) — AWS's public documentation of responsible-AI practices. <!-- needs-research: verify current overview surface at reading time -->
- [AWS — AI Service Cards](https://aws.amazon.com/ai/responsible-ai/resources/) — the AWS AI Service Cards convention. <!-- needs-research: verify current URL at reading time -->

### Open-source substrates worth reading against the matrix

- [Inspect (UK AI Safety Institute)](https://inspect.aisi.org.uk/) — the UK AISI's open-source Python library for authoring and running AI evaluations. Load-bearing for reproducibility bundles the evidence-store row consumes.
- [OpenAI Evals](https://github.com/openai/evals) — OpenAI's public evaluation framework, useful as an adjacent open-source substrate reference.
- [LangFuse / Arize Phoenix / Braintrust](https://langfuse.com/) — open or open-core observability platforms in the AI-eval space, useful as adjacent references against Fiddler's observability positioning. <!-- needs-research: verify current URLs and product surfaces for each -->
- [Aequitas (Center for Data Science and Public Policy, University of Chicago)](https://github.com/dssg/aequitas) — an open-source fairness-audit toolkit, useful as an adjacent reference against Holistic AI's bias tooling.

## Chapter `05` — Incident-driven roadmap prioritisation

### Incident-signal sources

- [AI Incident Database (AIID)](https://incidentdatabase.ai/) — the community-maintained database of publicly-reported AI incidents. Documented at [incidentdatabase.ai/research](https://incidentdatabase.ai/research/) with a public API.
- [AI Incident Database — Goals, Methods, and Failures (GMF) taxonomy](https://incidentdatabase.ai/taxonomies/) — the GMF taxonomy the categorisation pass uses. <!-- needs-research: verify current taxonomy URL structure and current published taxonomies -->
- [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents) — the OECD's incident monitor. <!-- needs-research: verify current scope and update cadence at reading time -->
- [MIT AI Risk Repository](https://airisk.mit.edu/) — a repository of AI-risk taxonomies, incident sources, and academic risk categorisations.
- [Partnership on AI — AI Incident Database contributors](https://partnershiponai.org/) — PAI's coordination role in the incident-database ecosystem. <!-- needs-research: verify current URL for PAI's incident-database work -->

### Adjacent incident-response and near-miss substrates

- [MITRE ATLAS](https://atlas.mitre.org/) — attack-technique catalogue useful as a categorisation lens for security-flavoured incidents.
- [CVE program](https://cve.mitre.org/) and [NIST NVD](https://nvd.nist.gov/) — the CVE and NVD substrates for security-CVE-adjacent AI incidents.
- [CISA — Cybersecurity and Infrastructure Security Agency alerts](https://www.cisa.gov/news-events/cybersecurity-advisories) — CISA advisories relevant when AI incidents cross into critical-infrastructure exposure. <!-- needs-research: verify current advisory URL structure at reading time -->

### Post-market surveillance substrate

- [FDA MAUDE — Manufacturer and User Facility Device Experience](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfmaude/search.cfm) — the FDA's post-market device-experience database; relevant analogue for the pinned organisation's own near-miss-log discipline when the organisation carries healthcare-AI products.
- [EudraVigilance — pharmacovigilance](https://www.ema.europa.eu/en/human-regulatory/research-development/pharmacovigilance/eudravigilance) — the EU pharmacovigilance system; another shape-reference for post-market signal capture.

### Adjacent research on incident-response programme design

- [Charette (RAND) and related — *The Risks Digest*](https://catless.ncl.ac.uk/Risks/) — the ACM SIGSOFT-hosted Risks Forum digest, long-running catalogue of software / systems incidents worth reading as prior art for categorical incident thinking.
- [Woods and Cook — resilience engineering literature](https://www.taylorfrancis.com/) — the resilience-engineering literature (Hollnagel, Woods, Leveson) whose *fault-in-context* framing shapes incident-analysis rigour. <!-- needs-research: pin specific canonical papers -->

## Horizontal frameworks all chapters braid with

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST framework.
- [NIST AI 600-1 — *Generative AI Profile*](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific profile of the AI RMF.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the AI-specific risk-management guidance.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the horizontal EU AI regulation.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.
- [Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the second-line-of-defence pattern grounding chapter `01`'s effective-challenge convention.

## Adjacent module cross-references

- [`mod-101-release-assurance-position`](../mod-101-release-assurance-position/) — the release-assurance role's outer position and the deferral contract that the operating model discharges.
- [`mod-102-assurance-case-engineering`](../mod-102-assurance-case-engineering/) — the assurance-case authoring surface the differentiated-core row of the build-vs-buy analysis defends; the audit passes the incident-driven ritual applies at programme scope.
- [`mod-103-release-gate-architecture`](../mod-103-release-gate-architecture/) — the release-gate walker the operating model's stage 5 runs; the on-call dashboard the effective-challenge convention hangs off; the consumer-contract-set the peer-contract matrix mirrors.
- [`mod-104-evaluation-evidence-pipeline`](../mod-104-evaluation-evidence-pipeline/) — the evidence pipeline, the reproducibility bundle, the supply-chain provenance substrate, the signed assurance bundle; the differentiated-core row of the build-vs-buy analysis.
- [`mod-105-cards-for-external-audiences`](../mod-105-cards-for-external-audiences/) — the card templates the analyst row's first-draft cards feed into.
- [`mod-106-cross-jurisdictional-obligation-mapping`](../mod-106-cross-jurisdictional-obligation-mapping/) — the coverage matrices the programme owes the senior architect; the substrate for the cross-jurisdictional exception log.
- [`mod-107-sector-regulated-assurance`](../mod-107-sector-regulated-assurance/) — the sector-overlay evidence set the external-supervisor interface drives.
- [`mod-108-deployment-tier-gating`](../mod-108-deployment-tier-gating/) — the deployment-tier map the scope-assessment stage classifies against; the freshness cadences the peer-contract matrix varies per tier.
- [`mod-109-third-party-evaluator-and-auditor-interface`](../mod-109-third-party-evaluator-and-auditor-interface/) — the third-party-evaluator interface layered on top of the peer contracts at tiers requiring independent evidence; the audit-pack shape the notified-body row consumes.
- [`mod-110-post-market-surveillance`](../mod-110-post-market-surveillance/) — the post-market signals feeding the same incident-driven prioritisation queue; the Article 61 / 72 / 73 discharge the external-supervisor interface transmits.
- [`mod-111-gpai-systemic-risk-assurance`](../mod-111-gpai-systemic-risk-assurance/) — the GPAI systemic-risk assurance surface where the AI Office interface takes its most intensive form; the escalation classes that leave team-scope authority under Article 55.

## Suggested reading order for this module

1. Chapter `01`, then read SR 11-7 straight through, then read ISO/IEC 42001 clauses 5 and 9.3. Exercise `01` authors the operating-model handbook.
2. Chapter `02`, then read the OpenTelemetry Gen-AI semantic conventions and one peer's methodology-of-record document (start with the risk-engineer's NIST AI RMF Playbook or NIST AI 600-1 read). Exercise `02` authors the peer-contract matrix.
3. Chapter `03`, then read Regulation (EU) 2024/1689 Articles 55, 61, 72, 73, and 74 end-to-end, then read the European AI Office landing page. Exercise `03` authors the interfaces upward and outward.
4. Chapter `04`, then read one of Microsoft's, Google's, or AWS's public responsible-AI standards straight through, then skim the seven vendor product surfaces. Exercise `04` authors the build-vs-buy fit-vs-gap analysis.
5. Chapter `05`, then walk one AIID incident record end-to-end, including the community post-mortem and any provider corrective statements. Exercise `05` runs the ritual against that incident.

You are not expected to memorise every vendor's feature matrix, every EU AI Act article number, every ISO clause, or every incident-database taxonomy row. You are expected to know which primary source owns each obligation, which peer-role registry produces the evidence for each claim, and to look up the specific citations confidently when the operating-model handbook, the peer-contract matrix, the upward interfaces, the build-vs-buy analysis, or the incident-driven roadmap pack needs to reference them.
