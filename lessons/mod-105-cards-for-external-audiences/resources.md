# Resources for mod-105-cards-for-external-audiences

Primary sources first. Every URL below points at the organisation that owns the artefact — the paper's authoritative host, the standards body, the tool project, the vendor's own documentation — so your reading pins to text that survives editorial rewrites. Secondary and background reading lives at the bottom.

## The card lineage — Mitchell, Gebru, Hugging Face (chapter `01`)

- Mitchell et al., *Model Cards for Model Reporting* — [arXiv:1810.03993](https://arxiv.org/abs/1810.03993). Published at ACM FAT\* 2019. The nine section headers, the disaggregation move, and the intended-use / out-of-scope discipline.
- Gebru et al., *Datasheets for Datasets* — [arXiv:1803.09010](https://arxiv.org/abs/1803.09010), *Communications of the ACM* December 2021 ([CACM DOI](https://doi.org/10.1145/3458723)). The seven datasheet sections and the provenance / maintenance moves.
- [Hugging Face Model Cards documentation](https://huggingface.co/docs/hub/model-cards) — field-by-field guide to the YAML frontmatter (`license`, `language`, `base_model`, `pipeline_tag`, `library_name`, `datasets`, `metrics`, `tags`, `model-index`, `co2_eq_emissions`).
- [Hugging Face Model Card Guidebook](https://huggingface.co/docs/hub/model-card-guidebook) — Ozoani, Gerchick, and Mitchell's operationalisation of Mitchell / Gebru into a hosted-model template.
- [Hugging Face `modelcard_template.md`](https://github.com/huggingface/huggingface_hub/blob/main/src/huggingface_hub/templates/modelcard_template.md) — the annotated template shipped with the `huggingface_hub` library.
- [`ModelCard` and `DatasetCard` Python APIs](https://huggingface.co/docs/huggingface_hub/en/guides/model-cards) — programmatic surface for reading, writing, and validating the YAML frontmatter.

### Card / datasheet variants worth recognising

- Pushkarna, Zaldivar, and Kjartansson, *Data Cards Playbook* (Google Research, 2022) — [arXiv:2204.01075](https://arxiv.org/abs/2204.01075) and [datacardsplaybook.org](https://sites.research.google/datacardsplaybook/). Data cards tailored for downstream deployers rather than researchers.
- Holland et al., *The Dataset Nutrition Label* (2018) and follow-up work at [datanutrition.org](https://datanutrition.org/) — rapid at-a-glance summary format.
- [MLCommons Croissant](https://mlcommons.org/working-groups/data/croissant/) — machine-readable dataset metadata format built on schema.org.
- Arnold et al., *FactSheets: Increasing Trust in AI Services through Supplier's Declarations of Conformity* (IBM, 2019) — [arXiv:1808.07261](https://arxiv.org/abs/1808.07261). Supplier declaration-of-conformity shape.
- Gilbert, Dean, Zick, and Lambert, *Reward Reports for Reinforcement Learning* — [arXiv:2204.10817](https://arxiv.org/abs/2204.10817). RL / RLHF reward-function reporting.
- Crisan, Drouhard, Vig, and Rajani, *Interactive Model Cards* (FAccT 2022) — [arXiv:2205.02894](https://arxiv.org/abs/2205.02894). User-research findings on how card readers actually use them.

## Assurance-card shape and worked examples (chapters `02` and `03`)

### Published system / model cards worth reading end-to-end

- OpenAI system cards:
  - [GPT-4 System Card (PDF)](https://cdn.openai.com/papers/gpt-4-system-card.pdf).
  - [GPT-4o System Card](https://openai.com/index/gpt-4o-system-card/).
  - [o1 System Card](https://openai.com/index/openai-o1-system-card/).
- Anthropic model cards:
  - [Claude 3 Model Card (PDF)](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf).
  - Claude 3.5 Sonnet and Claude 4 model-card family — links published on the [Anthropic news / research pages](https://www.anthropic.com/news).
- Google Gemini:
  - [Gemini model cards on the Gemini docs](https://ai.google.dev/gemini-api/docs/models) and the Vertex AI Model Garden pages.
- Meta Llama:
  - [Llama 3 model card on GitHub](https://github.com/meta-llama/llama-models/blob/main/models/llama3/MODEL_CARD.md).
  - [Meta Responsible Use Guide](https://ai.meta.com/static-resource/responsible-use-guide/).
  - [Llama 3.1 announcement](https://ai.meta.com/blog/meta-llama-3-1/) — Llama Guard, Prompt Guard, Code Shield references.

### Frontier-safety frameworks the tier-decision section reads to

- [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/) — the four tracked categories (cybersecurity, CBRN, persuasion, model autonomy) and tier decisions.
- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — the AI Safety Level (ASL) tiers.
- [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — Critical Capability Levels.
- [Meta Frontier AI Framework](https://ai.meta.com/static-resource/meta-frontier-ai-framework/) — release-decision framing for critical risk assessments.

### Adversarial / safety taxonomies chapter `03` §5 cites

- [MITRE ATLAS](https://atlas.mitre.org/) — adversarial threat landscape for AI systems.
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — LLM01 (Prompt Injection) through LLM10 (Unbounded Consumption).
- [NIST AI 100-2 E2023 — Adversarial Machine Learning Taxonomy](https://doi.org/10.6028/NIST.AI.100-2e2023).
- [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/) — safety-benchmark taxonomies and shared eval work.

## ISO/IEC 42005 impact assessment (chapter `04`)

- [ISO/IEC 42005:2025 — *Information technology — Artificial intelligence — AI system impact assessment*](https://www.iso.org/standard/42005) — the authoritative standard. The abstract on the ISO page is the first read; the standard text is the required reference for the section shape.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — clause 8.1 (operational planning) references the impact-assessment obligation the 42005 output discharges.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Article 27 (fundamental-rights impact assessment, FRIA) and Article 9 (risk management system). Article 27 is the specialisation for deployers of high-risk systems and public authorities that the stretch goal on exercise `03` covers.
- [European Commission FRIA guidance page](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the Commission's implementation guidance as it develops; watch for updates.

### Related risk-management / impact-assessment reading

- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — GOVERN / MAP / MEASURE / MANAGE functions; the MAP and MEASURE functions cover impact-assessment terrain.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — GenAI-specific risk categories that show up in impact-assessment findings.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally aligned principle set; a common vocabulary for stakeholder-facing findings.

## ISO/IEC 25059 quality-attribute spine (chapter `05`)

- [ISO/IEC 25059:2023 — *Software engineering — SQuaRE — Quality model for AI systems*](https://www.iso.org/standard/80655.html) — the AI-specific quality-model extension.
- [ISO/IEC 25010:2011 (rev. 2023) — *SQuaRE — System and software quality models*](https://www.iso.org/standard/78176.html) — the base quality model 25059 extends.
- [ISO/IEC 25012:2008 — *Data quality model*](https://www.iso.org/standard/35736.html) — data-quality characteristics referenced from the data section.
- [ISO/IEC 5259 series — *Data quality for analytics and ML*](https://www.iso.org/standard/81088.html) — the data-quality series aligned with modern ML pipelines.
- [ISO/IEC TR 24028:2020 — *Overview of trustworthiness in AI*](https://www.iso.org/standard/77608.html) — the trustworthiness terminology that many 25059 sub-attributes draw from.
- [ISO/IEC TR 24029-1:2021 — *Assessment of the robustness of neural networks — Part 1*](https://www.iso.org/standard/77609.html) — robustness assessment methodology.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance the quality-attribute thresholds bind risk positions to.

## C2PA content provenance and adjacent watermarking (chapter `06`)

### C2PA and Content Credentials

- [C2PA specification landing](https://spec.c2pa.org/) — technical specifications for the manifest, assertion, claim, and signature structure. Pin the version you cite in card body copy.
- [C2PA technical specification, v2.1](https://spec.c2pa.org/specifications/specifications/2.1/) — the current published revision at time of writing; check the landing page for later revisions.
- [Coalition for Content Provenance and Authenticity (C2PA)](https://c2pa.org/) — the coalition site, member list, and governance.
- [Content Authenticity Initiative (CAI)](https://contentauthenticity.org/) — the Adobe-led implementation initiative that operationalises C2PA into product tooling.
- [Content Credentials](https://contentcredentials.org/) — the consumer-facing brand for C2PA-signed content and the [verify page](https://contentcredentials.org/verify).
- [C2PA `c2patool`](https://github.com/contentauth/c2patool) — command-line tool for signing and verifying manifests. Rust and pre-built binaries.
- [`c2pa-rs`](https://github.com/contentauth/c2pa-rs) — the Rust SDK. Language bindings for other stacks are linked from the CAI repos.
- [Joint Development Foundation](https://www.jointdevelopment.org/) — the Linux Foundation subsidiary that hosts C2PA.

### Watermarking and complementary provenance

- [Google DeepMind SynthID](https://deepmind.google/technologies/synthid/) — statistical watermarking for image, audio, and text.
- [SynthID Text (blog post)](https://deepmind.google/discover/blog/watermarking-ai-generated-text-and-video-with-synthid/) — text-watermarking overview.
- [Kirchenbauer et al., *A Watermark for Large Language Models*](https://arxiv.org/abs/2301.10226) — foundational academic work on token-level LLM watermarking.
- [Aaronson, *Watermarking of Large Language Models* (2023 talk / notes)](https://scottaaronson.blog/?p=6823) — background reading on cryptographic watermarking approaches.
- [invisible-watermark](https://github.com/ShieldMnt/invisible-watermark) — an open-source image-watermarking implementation, useful for the stretch goal on exercise `04`.
- [IPTC Photo Metadata standard](https://iptc.org/standards/photo-metadata/) and the [`digitalSourceType` values](https://cv.iptc.org/newscodes/digitalsourcetype/) — upstream photo-metadata schema; the C2PA fallback often cites the IPTC `digitalSourceType` field for AI-generated imagery.

### EU AI Act disclosure obligations for GenAI

- [EU AI Act, Article 50 (transparency obligations for providers and deployers of certain AI systems)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — sub-paragraphs 1 (natural-person interaction), 2 (AI-generated content watermarking), 3 (deepfake disclosure), 4 (public-interest text disclosure).
- [EU AI Act, Article 53 (obligations for providers of general-purpose AI models)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — training-data disclosure summary requirements.
- [EU AI Act, Article 55 (obligations for providers of GPAI models with systemic risk)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — deep coverage in mod-111.

## Audience variants, third-party evaluators, and disclosure practice (chapter `07`)

- [UK AI Safety Institute](https://www.aisi.gov.uk/) — accredited independent evaluator; publishes evaluation methodology and reports.
- [US AI Safety Institute at NIST](https://www.nist.gov/aisi) — the US counterpart, hosted at NIST.
- [METR (Model Evaluation and Threat Research)](https://metr.org/) — third-party evaluator focused on autonomous-capability elicitation.
- [Apollo Research](https://www.apolloresearch.ai/) — third-party evaluator focused on deceptive-capability evaluation.
- [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/) — industry-consortium safety-benchmark work.
- [EU AI Act, Article 74 (market surveillance and control of AI systems on the Union market)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the market-surveillance authority's access rights the regulator variant reads to.
- [EU AI Act, Article 43 (conformity assessment)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — notified-body assessment; the notified-body variant of the regulator submission reads to this article.

## Regulated-product frameworks the exercises anchor to

### FDA / medical device

- [FDA Good Machine Learning Practice (GMLP) guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles).
- [FDA Predetermined Change Control Plan (PCCP) guidance](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial) — the change-envelope shape scenarios reference.
- [21 CFR Part 820 — Quality System Regulation](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfcfr/CFRSearch.cfm?CFRPart=820) — device-quality record-keeping.

### Banking / financial model risk

- [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) — the model-inventory / annual-validation / independent-review / ongoing-monitoring shape.
- [OCC 2011-12 — Sound Practices for Model Risk Management](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — OCC's counterpart guidance.
- [DORA — Digital Operational Resilience Act](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) — financial-sector operational-resilience regime (mod-107 has deep coverage).

## Data protection and consent frames the disclosure discipline reads to

- [GDPR — Regulation (EU) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj) — Articles 5 (principles), 6 (lawful basis), 22 (automated decision-making), 25 (data protection by design), 35 (data protection impact assessment).
- [CCPA / CPRA (California)](https://oag.ca.gov/privacy/ccpa) — the US-state counterpart with automated decision-making rulemaking underway.

## Adjacent methodology and background reading

- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — per-sub-category suggested actions.
- [NIST AI 100-4 — Reducing Risks Posed by Synthetic Content](https://doi.org/10.6028/NIST.AI.100-4) — provenance and watermarking guidance.
- [ISO/IEC 27001:2022](https://www.iso.org/standard/27001) and [ISO/IEC 27002:2022](https://www.iso.org/standard/75652.html) — the information-security management vocabulary many redaction rationales cite.
- [ISO/IEC 5338:2023 — *AI system life cycle processes*](https://www.iso.org/standard/81118.html) — life-cycle-process vocabulary the change-control section reads to.
- [ISO/IEC 42006:2025 — *Requirements for bodies providing audit and certification of AI management systems*](https://www.iso.org/standard/44546.html) — the accreditation regime the regulator / notified-body variant contemplates.

## Suggested reading order for this module

1. Chapter `01`, then Mitchell et al. (2019) and Gebru et al. (2021) end-to-end in one sitting. If you have not internalised the nine and the seven, the rest of the module will float.
2. Chapter `02`, then read *one* real system card from OpenAI, Anthropic, Google Gemini, or Meta Llama end-to-end. Draft the head shape for your own chosen scenario as YAML before opening exercise `01`.
3. Chapter `03` alongside the public system card you chose above. Then start exercise `01` (model card) and exercise `02` (system card).
4. Chapter `04` after `03`, plus the ISO/IEC 42005 abstract and — for the FRIA specialisation — EU AI Act Article 27. Exercise `03` executes the section against your worked scenario.
5. Chapter `05` alongside the ISO/IEC 25059 landing page. The quality-attribute vocabulary rewards a single careful pass and then shows up in exercises `01` and `02`.
6. Chapter `06` after chapter `05`. Read the C2PA specification landing page and one Article 50 sub-paragraph in one sitting. Exercise `04` produces a working manifest.
7. Chapter `07` after chapters `03`–`06`. Then execute exercise `05` — the four-variant derivation and the audit walk. If the audit walk fails, do not paper over it in the manifest; fix upstream in the public variant.

You are not expected to memorise every clause number or spec field. You are expected to know which standards body owns each artefact, which article of the EU AI Act shapes which disclosure obligation, and to be able to look up the exact identifier confidently when the card body needs to cite it.
