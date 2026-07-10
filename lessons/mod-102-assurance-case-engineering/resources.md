# Resources for mod-102-assurance-case-engineering

Primary sources first. Every URL below is to a primary organisation's own page, a published academic reference, or the OMG specification of record — so you can pin your understanding to text that survives editorial rewrites.

## The three assurance-case notations

- [Goal Structuring Notation (GSN) Community Standard v3](https://scsc.uk/gsn) — the community standard maintained by the Safety-Critical Systems Club. Read the standard cover-to-cover once; it is short. Then use it as reference for node shapes, link semantics, and modular structure.
- [Safety-Critical Systems Club (SCSC)](https://scsc.uk/) — hosts the GSN standard and publishes assurance-case working papers.
- [Adelard — Claims, Arguments, Evidence (CAE)](https://www.adelard.com/asce/choosing-asce/cae.html) — the practitioner introduction to CAE and its argument building blocks.
- [Adelard — ASCE (Assured Safety Arguments) tool](https://www.adelard.com/asce/) — the incumbent CAE and GSN tooling; also exports SACM.
- [OMG Structured Assurance Case Metamodel (SACM)](https://www.omg.org/spec/SACM/) — the OMG standards page. Latest published version at time of writing is SACM 2.2.
- [OMG XML Metadata Interchange (XMI)](https://www.omg.org/spec/XMI/) — SACM's XML interchange format.
- [ISO/IEC/IEEE 15026-2:2022 — Assurance case content](https://www.iso.org/standard/80625.html) — framework-agnostic content requirements that both GSN and CAE conform to. Read to understand the notation-independent baseline.
- ISO/IEC/IEEE 15026-1:2019 — Concepts and vocabulary — the companion vocabulary standard. Available via the ISO catalogue.

## Assurance-case methodology (background)

- Bishop, P. and Bloomfield, R. — Adelard's body of assurance-case work, including *Assurance Case Fundamentals* and the CAE Blocks methodology. See [Adelard publications](https://www.adelard.com/publications/) for the current list.
- Kelly, T. — the doctoral work behind GSN. *Arguing Safety – A Systematic Approach to Managing Safety Cases* (University of York, 1998). Kelly's subsequent GSN papers with Weaver are foundational; see the [University of York AAIP research pages](https://www.york.ac.uk/assuring-autonomy/) for pointers.
- Rushby, J. — *The Interpretation and Evaluation of Assurance Cases*, SRI Technical Report SRI-CSL-15-1 (2015). Available from the [SRI Computer Science Laboratory publications page](https://www.csl.sri.com/users/rushby/). The intellectual anchor for the confidence-in-argument framing used in chapter `05`.
- Rushby, J. — earlier work on *Formalism in Safety Cases* and related notes; also available from the SRI CSL page.
- Denney, E. and Pai, G. — NASA-led work on formalised assurance cases and the AdvoCATE tool; see [NASA Ames Robust Software Engineering group](https://ti.arc.nasa.gov/tech/rse/publications/) for the publications list.
- Habli, I. and colleagues — ongoing safety-case and ML-assurance work at the University of York. See the [Assuring Autonomy International Programme (AAIP)](https://www.york.ac.uk/assuring-autonomy/) publications list.

## ML- and AI-specific assurance cases

- Ashmore, R., Calinescu, R., and Paterson, C. — *Assuring the Machine Learning Lifecycle: Desiderata, Methods, and Challenges*. [arXiv:1905.04223](https://arxiv.org/abs/1905.04223). A survey that stakes out where assurance methods have to change to serve ML.
- Hawkins, R., Paterson, C., Picardi, C., Jia, Y., Calinescu, R., and Habli, I. — *Guidance on the Assurance of Machine Learning in Autonomous Systems (AMLAS)*. Published by the [Assuring Autonomy International Programme, University of York](https://www.york.ac.uk/assuring-autonomy/guidance/amlas/). The most-cited ML-safety-case methodology.
- Picardi, C., Paterson, C., Hawkins, R., Calinescu, R., and Habli, I. — Assurance-case work on ML at York; papers listed on the AAIP publications page above.
- Bloomfield, R., Khlaaf, H., Ryan Conmy, P., and Fletcher, G. — assurance-case work on AI systems from Adelard; see [Adelard publications](https://www.adelard.com/publications/).
- Khlaaf, H. — Trail of Bits and independent AI-safety publications on assurance and audit; see [Trail of Bits blog](https://blog.trailofbits.com/) and Khlaaf's public writing.

## Frameworks and regulations the case discharges into (background — deep coverage in adjacent mod-101, mod-106, mod-107, mod-108)

- [NIST AI Risk Management Framework 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework), the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook), and the [Generative AI Profile (AI 600-1)](https://doi.org/10.6028/NIST.AI.600-1). GOVERN / MAP / MEASURE / MANAGE and the sub-categories a release-case decomposes into.
- [ISO/IEC 42001:2023 — AI management system](https://www.iso.org/standard/81230.html). Clauses 4–10 are the auditable requirements; Annex A the AI-specific controls.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj). Articles 9–15 (per-obligation top of the release-case), 17 (QMS), 26 (deployer), 43 (conformity assessment), 47 (declaration of conformity), 49 (registration), 55 (GPAI with systemic risk), 61 (post-market), 72 (post-market monitoring plan).
- [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — operational reference for Article 55 discharge.
- [Federal Reserve SR 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and [OCC 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — sector-regulated model-risk shape.
- [FDA — Good Machine Learning Practice (GMLP) guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) and [FDA Predetermined Change Control Plans (PCCP) guidance](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions).

## Frontier-lab deployment-tier frameworks (background — deep coverage in mod-108, mod-111)

- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy).
- [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/).
- [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/).

## AISI-shape independent evaluators (background — deep coverage in mod-109)

- [UK AI Safety Institute](https://www.aisi.gov.uk/) and its [Inspect](https://inspect.aisi.org.uk/) evaluation framework.
- [US AI Safety Institute (NIST AISI)](https://www.nist.gov/aisi) and the [AISI Consortium](https://www.nist.gov/aisi/artificial-intelligence-safety-institute-consortium-aisic).
- [Singapore IMDA AI Verify Foundation](https://aiverifyfoundation.sg/).
- [METR](https://metr.org/), [Apollo Research](https://www.apolloresearch.ai/), [MLCommons AI Safety Working Group](https://mlcommons.org/working-groups/ai-safety/ai-safety/).

## Tooling

- [Adelard ASCE](https://www.adelard.com/asce/) — CAE and GSN authoring; SACM export.
- The University of York AAIP publishes tooling companions to AMLAS; see the AAIP page above.
- Open-source SACM tooling is fragmented; the OMG spec page above lists submitters and reference implementations.
- <!-- needs-research: verify current state of open-source GSN-to-SACM converters (Isabelle-based SACM libraries, community JSON schemas) and cite specific projects with active maintenance --> The chapters cite these as a category; author-of-record references land here on the next research cycle.

## Adjacent evidence-substrate (peer-owned, background)

- [OpenTelemetry Gen-AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the standard schema for the traces that discharge instrumentation claims.
- [OpenInference](https://github.com/Arize-ai/openinference) — vendor-neutral instrumentation library that emits OpenTelemetry-compatible spans for LLM applications.
- [Inspect (UK AISI)](https://inspect.aisi.org.uk/) — evaluation framework of record for AISI-shape assurance cases.
- [EleutherAI lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) — the community harness whose outputs land as evidence in many GenAI release-cases.

## Suggested reading order for this module

1. Chapter `01` of this module, then chapter 2 of the [GSN Community Standard v3](https://scsc.uk/gsn) — one sitting.
2. Chapter `02` of this module, then the rest of the GSN Community Standard v3 (modular extensions) — one sitting.
3. Chapter `03` of this module, then the [Adelard CAE](https://www.adelard.com/asce/choosing-asce/cae.html) piece plus ISO/IEC/IEEE 15026-2 content section — one sitting.
4. Chapter `04` of this module, then a walkthrough of the OMG SACM 2.2 spec's package summaries (Base / Argumentation / Terminology / Artifact) — one sitting.
5. Chapter `05` of this module, then Rushby's *The Interpretation and Evaluation of Assurance Cases* — one sitting.
6. Chapter `06` of this module, then the AMLAS guidance from AAIP and Ashmore et al. arXiv:1905.04223 — one sitting.

You are not expected to memorise SACM class names. You are expected to know which notation and which OMG package the release-case's content persists into, and to be able to look up the exact class or clause identifier confidently.
