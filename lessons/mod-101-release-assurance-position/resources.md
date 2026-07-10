# Resources for mod-101-release-assurance-position

Primary sources first. Secondary and community references at the bottom. Every URL below is to a primary organisation's own page — not to a third-party summary — so you can pin your understanding to text that survives editorial rewrites.

## NIST AI RMF and companions

- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the framework itself. Read cover-to-cover once; then keep as a reference to walk sub-categories.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the day-to-day companion. Per-sub-category suggested actions, transparency clauses, and cross-references to other frameworks.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — profile of AI RMF 1.0 for generative AI. Read after AI 100-1 if your systems include GenAI.
- [NIST AI 100-2 — Adversarial-ML Taxonomy](https://doi.org/10.6028/NIST.AI.100-2e2023) — reference for the MEASURE-2.7 (security / resilience) attack categories.
- [NIST AI Resource Center (AIRC)](https://airc.nist.gov/) — hub for the above and related NIST AI materials.

## ISO/IEC standards

- [ISO/IEC 42001:2023 — AI management system](https://www.iso.org/standard/81230.html) — the AIMS standard. Clauses 4–10 are the auditable requirements; Annex A lists the AI-specific controls.
- [ISO/IEC 23894:2023 — AI risk-management guidance](https://www.iso.org/standard/77304.html) — method behind clause 6 risk assessment.
- [ISO/IEC 42005:2025 — AI system impact assessment](https://www.iso.org/standard/44545.html) — method behind clause 6 impact assessment.
- [ISO/IEC 25059:2023 — SQuaRE for AI systems](https://www.iso.org/standard/80655.html) — software-quality-model extension for AI.
- [ISO/IEC 24029-2:2023 — Robustness of neural networks (methodology)](https://www.iso.org/standard/79804.html) — method for robustness measurement.
- [ISO/IEC 42006 — Requirements for bodies certifying AIMS](https://www.iso.org/standard/44546.html) — accreditation shape for AIMS certification bodies.
- ISO/IEC 5259 series — data quality for analytics and ML; see the ISO catalogue for the current parts.
- [ISO/IEC 8183](https://www.iso.org/standard/83628.html) — data life-cycle framework for AI. Complements the 5259 series.

## EU AI Act and instruments

- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — official text on EUR-Lex. Read Chapter III (Section 2) for high-risk requirements; Chapter V for GPAI; Chapter IX for post-market monitoring and reporting.
- [European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the Commission body overseeing GPAI obligations.
- [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — operational reference for Article 55 discharge by GPAI providers.
- [Annex III high-risk domains, unofficial navigable version](https://artificialintelligenceact.eu/annex/3/) — read alongside the official EUR-Lex text.

## International values baseline

- [OECD AI Principles (2019, updated 2024)](https://oecd.ai/en/ai-principles) — the anchor values instrument.
- [OECD AI Classification Framework](https://oecd.ai/en/classification) — categorisation for AI systems by context, data, model, task, and impacts.
- [Council of Europe Framework Convention on AI (2024)](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — first binding international treaty on AI.
- [UNESCO Recommendation on the Ethics of AI (2021)](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics) — most widely subscribed values instrument.
- UNESCO Readiness Assessment Methodology (RAM) and Ethical Impact Assessment (EIA) tool — see the UNESCO AI ethics page above for current links.

## Adjacent sector-regulated shape (background reading; deep coverage in mod-107)

- [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm)
- [OCC 2011-12 — Sound practices for model risk management](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html)
- [SR 23-4 — Interagency guidance on third-party relationships](https://www.federalreserve.gov/supervisionreg/srletters/SR2304.htm)
- [FDA Good Machine Learning Practice (GMLP) guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles)
- [FDA Predetermined Change Control Plans (PCCP) for AI-enabled device software](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions)
- [DORA — Regulation (EU) 2022/2554](https://eur-lex.europa.eu/eli/reg/2022/2554/oj)

## Adjacent frontier-lab deployment-tier frameworks (background reading; deep coverage in mod-108, mod-111)

- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy)
- [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/)
- [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/)
- [Frontier Model Forum](https://www.frontiermodelforum.org/)

## AISI-shape independent evaluators (background reading; deep coverage in mod-109)

- [UK AI Safety Institute](https://www.aisi.gov.uk/) and its [Inspect](https://inspect.aisi.org.uk/) evaluation framework
- [US AI Safety Institute (NIST AISI)](https://www.nist.gov/aisi) and the [AISI Consortium](https://www.nist.gov/aisi/artificial-intelligence-safety-institute-consortium-aisic)
- [Singapore IMDA AI Verify Foundation](https://aiverifyfoundation.sg/)
- [METR](https://metr.org/), [Apollo Research](https://www.apolloresearch.ai/), [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/)

## Assurance-case methodology (background reading; deep coverage in mod-102)

- [Goal Structuring Notation (GSN) Community Standard v3](https://scsc.uk/gsn)
- [Adelard CAE (Claims, Argument, Evidence)](https://www.adelard.com/asce/choosing-asce/cae.html)
- [OMG SACM (Structured Assurance Case Metamodel)](https://www.omg.org/spec/SACM/)

## Cards and provenance (background reading; deep coverage in mod-105)

- Mitchell et al., *Model Cards for Model Reporting* — [arXiv:1810.03993](https://arxiv.org/abs/1810.03993)
- Gebru et al., *Datasheets for Datasets* — [arXiv:1803.09010](https://arxiv.org/abs/1803.09010)
- [Hugging Face Model Card Guidebook](https://huggingface.co/docs/hub/model-card-guidebook)
- [C2PA content provenance](https://c2pa.org/)

## Incident registries (background reading; deep coverage in mod-110)

- [AI Incident Database (AIID)](https://incidentdatabase.ai/)
- [OECD.AI Incidents Monitor](https://oecd.ai/en/incidents)
- [MIT AI Risk Repository](https://airisk.mit.edu/)

## Suggested reading order for this module

1. Chapter `01` of this module, then the top-level NIST AI RMF (AI 100-1) — one sitting.
2. Chapter `02` of this module, then the Playbook and NIST AI 600-1 — one sitting.
3. Chapter `03` of this module, then a full read of ISO/IEC 42001:2023 clauses 4–10 — one sitting.
4. Chapter `04` of this module, then EU AI Act Articles 5, 6, 8–15, 17, 26, 43, 47, 49, 55, 61, 72 and Annexes III, IV, V — one sitting.
5. Chapter `05`, then the three values instruments (OECD, CoE, UNESCO) — one sitting.
6. Chapter `06`, then the exercises.

You are not expected to memorise sub-category or article numbers. You are expected to know which framework and which article shape a given release-gate obligation, and to be able to look up the specific identifier confidently.
