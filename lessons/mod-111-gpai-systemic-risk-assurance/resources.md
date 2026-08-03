# Resources for mod-111-gpai-systemic-risk-assurance (GenAI / GPAI Systemic-Risk Assurance)

Primary sources first. Every URL below points at the organisation that issues, hosts, or operates the instrument — the Regulation's consolidated text on EUR-Lex, the standards body, the frontier lab's own safety-framework landing page, the arXiv preprint, the AI Safety Institute's own publications hub — so your reading pins to text that survives editorial rewrites. Secondary reading and thematic commentary sit at the bottom.

The load-bearing reads for this module differ per chapter. Chapter `01`'s load-bearing reads are the consolidated text of Regulation (EU) 2024/1689 (Articles 3(65), 51, 52, 53, 55, 56, plus Annex XIII) and the current published version of the [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice). Chapter `02`'s are the four current published frontier frameworks (Anthropic RSP, OpenAI Preparedness, Google DeepMind FSF, Meta Frontier AI Framework) plus at least two [Frontier Model Forum](https://www.frontiermodelforum.org/) issue briefs. Chapter `03`'s are [NIST AI 600-1](https://doi.org/10.6028/NIST.AI.600-1) end-to-end and the UK AISI [Inspect](https://inspect.aisi.org.uk/) documentation. Chapter `04`'s are the arXiv preprints for each named benchmark plus the MLCommons AI Safety Working Group landing. Chapter `05`'s are the [C2PA technical specification](https://c2pa.org/specifications/specifications/) and the [NTIA Report on Dual-Use Foundation Models with Widely Available Model Weights](https://www.ntia.gov/programs-and-initiatives/artificial-intelligence/report-on-dual-use-foundation-models). If you read nothing else across the module, read the consolidated EU AI Act text for Articles 51, 52, and 55 end-to-end, the current Code of Practice safety-and-security chapter, and one of the four frontier frameworks straight through — those three primary sources carry the module's statutory-and-industry backbone.

## Chapter `01` — EU AI Act Article 55 and the GPAI Code of Practice

### EU AI Act primary sources

- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the consolidated Regulation text. Article 3(65) (definition of a GPAI model with systemic risk), Article 51 (classification criteria, including the 10^25-FLOP presumption), Article 52 (notification and designation procedure), Article 53 (obligations of GPAI providers baseline), Article 55 (obligations of GPAI providers with systemic risk), Article 56 (invitation to codes of practice), plus Annex XIII (criteria for the designation of GPAI models with systemic risk) are the specific citations this chapter uses.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office landing page; the enforcement counterparty for GPAI obligations.
- [European Commission — AI Act implementing acts and guidance](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the AI Act policy hub for implementing acts and Commission guidance. <!-- needs-research: verify whether the Commission has adopted a delegated act updating the Article 51(2) FLOP threshold since the Regulation was published -->

### GPAI Code of Practice

- [EU General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the operational discharge reference for Article 55 (and baseline Article 53) obligations for signatories. The Code is structured in three chapters: safety and security, transparency (including the Model Documentation Form), and copyright. <!-- needs-research: verify the current published version of the Code at drafting date -->
- [European Commission — GPAI Code of Practice signatories page](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — the signatories list. <!-- needs-research: verify the current URL for the signatories page and the current signatory set -->

### AI RMF and adjacent horizontal frameworks

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST AI RMF landing.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard whose clauses discipline the assurance case that Article 55 evidence lands in.

## Chapter `02` — Frontier-lab deployment-tier frameworks (comparative read)

### The four reference frameworks

- [Anthropic — Responsible Scaling Policy (RSP)](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — Anthropic's public commitment to AI Safety Levels (ASL) with paired deployment and security standards per level. Revised multiple times since 2023-09; verify the current version at reading time. <!-- needs-research: verify current RSP version and the ASL-4+ standards -->
- [OpenAI — Preparedness Framework](https://openai.com/safety/preparedness/) — OpenAI's public commitment to tracked risk categories (originally Cybersecurity, CBRN, Persuasion, Model Autonomy) with per-category thresholds. Substantively updated since first publication; verify the current version. <!-- needs-research: verify current Preparedness Framework version and tracked-category set -->
- [Google DeepMind — Frontier Safety Framework (FSF)](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — Google DeepMind's public commitment to Critical Capability Levels (CCLs) with separated deployment and security mitigations, periodic re-evaluation, and mitigation-effectiveness evaluation. <!-- needs-research: verify current FSF version and CCL category set -->
- Meta Frontier AI Framework — Meta's public frontier-model safety framework, structured around unique-and-material uplift toward severe outcomes with a high-risk and a critical-risk tier. <!-- needs-research: verify the canonical URL and current version of the Meta Frontier AI Framework at drafting date -->

### The Frontier Model Forum

- [Frontier Model Forum](https://www.frontiermodelforum.org/) — the industry body's landing page. Publishes issue briefs, working-group outputs, and reference-approach materials. <!-- needs-research: verify current publications page and highlight briefs relevant to Article 55 discharge -->
- [Frontier Model Forum — publications library](https://www.frontiermodelforum.org/updates/) — the publications feed. <!-- needs-research: verify the current publications-list URL structure -->

### Adjacent public safety-policy references

- [Microsoft — Responsible AI Standard](https://www.microsoft.com/en-us/ai/responsible-ai) — Microsoft's public Responsible AI framework; adjacent to the four references, useful as a fifth-framework contrast in the comparative read. <!-- needs-research: verify current version -->

## Chapter `03` — AISI TEVV and NIST AI 600-1 as the evaluator envelope

### NIST AI 600-1 and the AI RMF

- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) (2024-07) — the GenAI-specific profile of NIST AI RMF 1.0; twelve GenAI risk categories cross-referenced into GOVERN / MAP / MEASURE / MANAGE.
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the outer framework AI 600-1 profiles.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the operational elaboration of the framework.
- [NIST — Trustworthy and Responsible AI Resource Center (AIRC)](https://airc.nist.gov/) — the AIRC hub.
- [NIST AI 100-2 (Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations)](https://doi.org/10.6028/NIST.AI.100-2e2023) — the adversarial-ML taxonomy that many Article 55(1)(a) adversarial-testing methodologies map into.
- [NIST AI 100-4 (Reducing Risks Posed by Synthetic Content)](https://doi.org/10.6028/NIST.AI.100-4) — NIST's synthetic-content risk-reduction publication, adjacent to Article 50 and chapter `05`. <!-- needs-research: verify current NIST 100-4 status and successor documents -->

### UK AI Safety Institute

- [UK AI Safety Institute](https://www.aisi.gov.uk/) — the UK AISI landing page.
- [Inspect (open-source AI evaluation framework)](https://inspect.aisi.org.uk/) — the UK AISI's open-source Python library for authoring and running AI evaluations. Load-bearing for reproducibility bundles in AISI-shape TEVV engagements.
- [UK AISI — evaluations of frontier models](https://www.aisi.gov.uk/work) — the UK AISI's published evaluation reports. <!-- needs-research: verify the current publications URL and evaluation-report set -->
- [UK AISI — publications](https://www.aisi.gov.uk/) — the publications hub. <!-- needs-research: verify the current publications URL -->

### US AI Safety Institute (NIST)

- [US AI Safety Institute](https://www.nist.gov/aisi) — the US AISI landing page, hosted at NIST.
- [US AISI — publications and voluntary agreements](https://www.nist.gov/aisi) — the US AISI's published outputs. <!-- needs-research: verify the current publications URL and the current set of voluntary pre-deployment testing agreements with frontier developers -->

### TEVV framing (systems-engineering roots)

- [NIST — Testing, Evaluation, Verification, and Validation](https://www.nist.gov/programs-projects/testing-evaluation-verification-validation-tevv-technology-transfer) — the TEVV framing hub. <!-- needs-research: verify current TEVV publications URL -->

## Chapter `04` — Safety-benchmark evidence citation pack

### MLCommons AI Safety Working Group

- [MLCommons AI Safety Working Group](https://mlcommons.org/ai-safety/) — the AI safety working-group landing page.
- [MLCommons AILuminate](https://mlcommons.org/ai-safety/) — the AILuminate safety benchmark; per-hazard grades across categories. <!-- needs-research: verify AILuminate current version and dedicated landing URL if one exists -->

### Named benchmarks (arXiv-first)

- [AIR-Bench 2024 (arXiv:2407.17436)](https://arxiv.org/abs/2407.17436) — a safety benchmark whose taxonomy is derived from a survey of government AI regulations and company AI policies.
- [HarmBench (arXiv:2402.04249)](https://arxiv.org/abs/2402.04249) — a standardised evaluation framework for automated red-teaming of LLMs against harmful behaviours.
- [AgentDojo (arXiv:2406.13352)](https://arxiv.org/abs/2406.13352) — an evaluation framework for prompt injection and other attacks against tool-using LLM agents.
- [InjecAgent (arXiv:2403.02691)](https://arxiv.org/abs/2403.02691) — a benchmark for indirect prompt injection against tool-using LLM agents.
- [SafetyBench (arXiv:2309.07045)](https://arxiv.org/abs/2309.07045) — a multiple-choice benchmark for evaluating LLM safety understanding across categories.
- CyBench — an LLM cybersecurity capability benchmark including CTF challenges. <!-- needs-research: verify current arXiv identifier and landing page for CyBench -->
- [WMDP — Weapons of Mass Destruction Proxy (arXiv:2403.03218)](https://arxiv.org/abs/2403.03218) — multiple-choice hazardous-knowledge proxy for CBRN uplift and unlearning-effectiveness measurement.

### Peer-role registry references

The methodology depth on every benchmark is owned by peer roles, cited by reference from the release-assurance methodology owner:

- `model-evaluation-engineer` — depth on benchmark reading, scoring, and coverage claims.
- `ai-risk-engineer` — depth on adversarial red-team methodology, guardrail-evaluation methodology, and mitigation-effectiveness measurement.
- `agentic-safety-engineer` (level 40) — depth on frontier-agent red-team methodology, elicitation of tool-access-only capabilities, and agentic-mitigation effectiveness.

### Adjacent evaluation substrates

- [Inspect](https://inspect.aisi.org.uk/) — the UK AISI open-source evaluation library (repeated from chapter `03`; the same substrate that lands in the reproducibility bundle manifest).
- [OpenAI Evals](https://github.com/openai/evals) — OpenAI's public evaluation framework, useful as an adjacent substrate reference.

## Chapter `05` — C2PA provenance and NTIA obligations for GenAI

### C2PA and content-provenance

- [C2PA — Coalition for Content Provenance and Authenticity](https://c2pa.org/) — the C2PA landing page.
- [C2PA — technical specifications](https://c2pa.org/specifications/specifications/) — the technical specification for content-provenance manifests, assertions, hard binding, trust list, and redaction. <!-- needs-research: verify the current specification version at drafting date -->
- [Content Authenticity Initiative (CAI)](https://contentauthenticity.org/) — the industry initiative promoting C2PA adoption; maintains an implementation-focused resource set.
- [C2PA — public trust list](https://c2pa.org/) — the C2PA trust list. <!-- needs-research: verify the current URL and process for the C2PA trust list -->

### Watermarking (as the complement to C2PA)

- [Google DeepMind — SynthID](https://deepmind.google/technologies/synthid/) — the SynthID statistical watermarking scheme for text, image, and other modalities. Adjacent-mechanism reference from chapter `05`.

### EU AI Act — Article 50 (transparency obligations for GenAI)

- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Article 50 (transparency obligations for providers and deployers of certain AI systems). Article 50(2) covers machine-readable marking of synthetic outputs; Article 50(4) covers deep-fake disclosure. <!-- needs-research: reconfirm exact paragraph numbering of Article 50 in the current consolidated text -->

### NTIA report on dual-use foundation models

- [NTIA — Report on Dual-Use Foundation Models with Widely Available Model Weights](https://www.ntia.gov/programs-and-initiatives/artificial-intelligence/report-on-dual-use-foundation-models) (2024-07) — the reference US-government marginal-risk analysis of open-weights foundation-model trade-offs. <!-- needs-research: verify current URL and any successor documents from NTIA at drafting date -->
- [NTIA — AI hub landing page](https://www.ntia.gov/programs-and-initiatives/artificial-intelligence) — the wider NTIA AI landing.

### Supply-chain and signing substrate the C2PA credential lives inside

- [Sigstore project](https://www.sigstore.dev/) — the signing infrastructure the producer-credential chain frequently sits inside; cross-reference `mod-104` chapter `04`.
- [Sigstore — Fulcio](https://docs.sigstore.dev/certificate_authority/overview/) — the certificate authority whose Fulcio-issued certs the producer credential can chain to.
- [Sigstore — Rekor transparency log](https://docs.sigstore.dev/logging/overview/) — the transparency log the signing events can land in.

## Horizontal frameworks all chapters braid with

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST framework.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the horizontal EU AI regulation.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.

## Adjacent module cross-references

- [`mod-101-release-assurance-position`](../mod-101-release-assurance-position/) — the release-assurance role's outer position; Article 3(65) / 51 / 52 extend the Chapter III Section 2 walk from chapter `04` of that module.
- [`mod-102-assurance-case-engineering`](../mod-102-assurance-case-engineering/) — the assurance case whose top-level claims Article 55 obligations become; the Union-level systemic-risk assessment is a new claim-and-evidence surface.
- [`mod-103-release-gate-architecture`](../mod-103-release-gate-architecture/) — the release-gate criteria the Article 55 evidence set discharges through.
- [`mod-104-evaluation-evidence-pipeline`](../mod-104-evaluation-evidence-pipeline/) — the content-addressed store where every Article 55 evidence artefact lands; the reproducibility bundles the AISI-shape TEVV evaluator consumes; the signed assurance bundle at chapter `06`; supply-chain provenance (chapter `04`) as the C2PA producer-credential substrate.
- [`mod-105-cards-for-external-audiences`](../mod-105-cards-for-external-audiences/) — the Model Documentation Form (from the Code of Practice transparency chapter); the `provenance.c2pa` block at chapter `06` this module's chapter `05` cites into.
- [`mod-106-cross-jurisdictional-obligation-mapping`](../mod-106-cross-jurisdictional-obligation-mapping/) — the multi-jurisdiction shape (AI Office / UK AISI / US AISI) the evaluator envelope and Article 55 discharge coordinate across.
- [`mod-107-sector-regulated-assurance`](../mod-107-sector-regulated-assurance/) — where a systemic-risk GPAI is also sector-regulated (financial services, healthcare), the sector overlay attaches alongside the Article 55 overlay.
- [`mod-108-deployment-tier-gating`](../mod-108-deployment-tier-gating/) — the enterprise adaptation of the frontier-lab frameworks (chapter `02` reads the same frameworks with a different lens).
- [`mod-109-third-party-evaluator-and-auditor-interface`](../mod-109-third-party-evaluator-and-auditor-interface/) — the master evaluator interface (signed evaluation agreement, attack-payload non-disclosure, result-disclosure terms) the AISI-shape TEVV envelope inherits from.
- [`mod-110-post-market-surveillance`](../mod-110-post-market-surveillance/) — the Article 55(1)(c) serious-incident channel extends the Article 73 workflow; the openness-position re-assessment cadence interlocks with the post-market surveillance loop.
- [`mod-112-owning-an-assurance-program`](../mod-112-owning-an-assurance-program/) — running the Article 55 discharge across a portfolio and across model versions.

## Suggested reading order for this module

1. Chapter `01`, then read Regulation (EU) 2024/1689 Articles 3(65), 51, 52, 53, 55, and 56 in the consolidated text, plus Annex XIII, plus the current published version of the EU GPAI Code of Practice. Exercise `01` authors the Article 55 obligation map.
2. Chapter `02`, then read one of the four frontier frameworks straight through (RSP is a good first read), then skim the other three for structural contrasts, then read at least two Frontier Model Forum issue briefs. Exercise `02` builds the comparative-read table.
3. Chapter `03`, then read NIST AI 600-1 end-to-end and the UK AISI Inspect documentation. Exercise `03` designs the evaluator envelope.
4. Chapter `04`, then spend an hour on each named-benchmark arXiv preprint, prioritising the ones that map to your release's modality set. Exercise `04` builds the safety-benchmark citation pack.
5. Chapter `05`, then read the C2PA specification end-to-end (or the summary sections if time is short), read the NTIA report end-to-end, and read Article 50 of the consolidated EU AI Act. Exercise `05` overlays the C2PA-provenance and NTIA-openness sections.

You are not expected to memorise every framework's tier taxonomy, every benchmark's scoring convention, every C2PA assertion name, or every NTIA recommendation. You are expected to know which primary source owns each obligation, which peer-role registry entry produces the evidence for each claim, and to look up the specific citations confidently when the assurance case, the evaluator envelope, or the provenance-and-openness overlay needs to reference them.
