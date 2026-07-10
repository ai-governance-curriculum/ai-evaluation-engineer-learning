# The Card Lineage: Mitchell, Gebru, and the Hugging Face Guidebook

## Motivation

Every card an AI Evaluation Engineer will ever ship — model card, dataset card, system card, regulator submission, third-party evaluator handoff, board briefing — descends from three primary sources: Mitchell et al.'s *Model Cards for Model Reporting* (FAT\* 2019), Gebru et al.'s *Datasheets for Datasets* (CACM 2021), and the Hugging Face model-cards guidebook / template that operationalised both into a standard `README.md` form on the Hub. You cannot skip these; the vocabulary the regulator uses in Article 11 Annex IV of the EU AI Act ("intended purpose," "known limitations," "foreseeable misuse"), the taxonomy the ISO/IEC 42001 clause 7.5 documented-information requirements draw from, and the shape a downstream deployer expects when they open a page on the Hub or on Vertex Model Garden are all downstream of these three artefacts.

This chapter reads all three at the level a card author has to be able to argue from. The next chapter (`02`) then names precisely where they stop being enough for a regulator, notified body, third-party evaluator, or board audience — and what the enterprise-scale *assurance card* shape has to add.

## Mitchell et al., 2019 — Model Cards for Model Reporting

Mitchell, Wu, Zaldivar, Barnes, Vasserman, Hutchinson, Spitzer, Raji, and Gebru published *Model Cards for Model Reporting* at ACM FAT\* 2019 ([arXiv:1810.03993](https://arxiv.org/abs/1810.03993)). The paper's shape is what every downstream card template imitates.

The central move is deceptively small. Take any trained model as a *reporting unit* and require it to carry a short, structured document that answers a fixed set of questions. The paper enumerates nine section headers:

1. **Model Details** — organisation, version, date, model type, training algorithm, parameters, features, license, and where feedback goes.
2. **Intended Use** — the intended users, the intended primary use cases, and out-of-scope use cases explicitly listed.
3. **Factors** — the demographic, phenotypic, and environmental factors that meaningfully change model behaviour and that the card claims to have measured.
4. **Metrics** — the model performance measures reported, with explicit choice of thresholds and any relevant approaches to decision thresholds.
5. **Evaluation Data** — the datasets used to evaluate the model, why they were chosen, and any pre-processing done for evaluation.
6. **Training Data** — the same three points, at whatever level of disclosure the provider chooses (Mitchell et al. explicitly allow "same as evaluation data" or a partial disclosure).
7. **Quantitative Analyses** — reported metrics disaggregated by factors *and* by intersections of factors.
8. **Ethical Considerations** — the risks the model raises and how they were considered, including data-sensitive fields (medical, legal), use in a decision that meaningfully affects human life, and mitigations shipped alongside the model.
9. **Caveats and Recommendations** — anything else the reviewer needs to interpret the numbers correctly.

Three moves from the paper survive into every regulator template and are worth naming outright.

- **The disaggregation move.** Metrics are not just top-line; the card asks the author to report *disaggregated* metrics along the factors it names, and the intersections of those factors. This is what makes a model card auditable rather than merely descriptive. A card that reports overall accuracy but not per-subgroup accuracy is *not* a Mitchell card.
- **The intended-use move.** The card asks the author to enumerate not only the intended primary use cases but also the **out-of-scope** use cases. The out-of-scope list is what a downstream deployer, a regulator, or a third-party evaluator will bind an appropriate-use claim to. Its absence is a defeater. The EU AI Act Article 13 (transparency and provision of information) reads as a stricter, legally binding version of this same move.
- **The mitigation-is-part-of-the-card move.** Section 8 (ethical considerations) is not a disclaimer. It is a section where the model's shipping context — guardrails, sensitive-data notices, decision-affecting-humans notes — is documented at the same version as the model itself. That is the seed of the *system card* the module returns to in chapter `03`.

Mitchell et al. also fix a stance the card author has to internalise. They frame model cards as *reporting for accountability*, not as a marketing artefact. A card is written for someone who might refuse to use the model, not for someone whose decision is already made. The reader is presumed adversarial in the mild sense — willing to walk away, willing to press for evidence.

The paper deliberately does *not* fix a machine-readable schema, does not specify how factor lists interact with the underlying data-generating process, does not name any specific regulatory regime, and does not talk about immutability, versioning, or content-provenance. All four of those gaps are what later chapters of this module will fill.

## Gebru et al., 2018 / 2021 — Datasheets for Datasets

Gebru, Morgenstern, Vecchione, Vaughan, Wallach, Iii, and Crawford's *Datasheets for Datasets* appeared as a workshop paper at FAT/ML 2018 and was published in *Communications of the ACM* in December 2021 ([arXiv:1803.09010](https://arxiv.org/abs/1803.09010) / [CACM DOI](https://doi.org/10.1145/3458723)). Where a Mitchell model card is the model's reporting unit, a Gebru datasheet is the dataset's.

The datasheet is longer than a model card because a dataset raises more questions. Gebru et al. propose seven sections, each with a list of questions the datasheet author is asked to answer:

1. **Motivation** — why was the dataset created, who created it, who funded its creation, and what any specific tasks it was intended to support.
2. **Composition** — what the instances are; how many; whether they are a sample of a larger set; what data each instance contains; whether labels are associated; missingness; relationships between instances; recommended splits; errors, noise, redundancies; whether the dataset is self-contained or links out to external sources; any data confidential or subject to legal protections; anything a data subject would consider sensitive.
3. **Collection process** — how the data was acquired, what mechanisms or procedures were used, sampling strategy, who was involved in collection, over what timeframe, whether an ethical review process was conducted, whether individuals were notified, whether they consented, whether they can revoke, whether an analysis of potential impact of the dataset and its use on data subjects has been conducted.
4. **Preprocessing / cleaning / labelling** — what was done, whether the raw data was saved, whether the software used is available, and any other information.
5. **Uses** — what tasks the dataset has been used for; is there a repository that links to any/all papers or systems that use it; what other tasks it could be used for; anything about its composition or its collection that might impact future uses; are there tasks the dataset should *not* be used for.
6. **Distribution** — how it is or will be distributed, when, under what license, are there export controls or regulatory restrictions, any warranties.
7. **Maintenance** — who is supporting / hosting / maintaining, contact, updates plan, deprecation, retention limits, and how consumers should communicate errors.

Three moves survive from the datasheet into the regulator-facing world.

- **The provenance move.** Every question about the dataset ultimately drives to a provenance chain: who collected, from whom, under what consent, under what license, under what preprocessing. This is what the EU AI Act Article 10 (data and data governance) and NIST AI RMF's MAP-4.1 (data provenance) read as a legally binding form of. The datasheet is the shape the regulator expects the answers to arrive in.
- **The "should not be used for" move.** Section 5 explicitly asks whether there are tasks the dataset should not be used for. This is the dataset-side twin of the model card's out-of-scope-use list, and just like on the model side its absence is a defeater. Regulators reading a dataset card without this section will assume the author has not thought hard about downstream misuse.
- **The maintenance move.** Section 7 forces the dataset's *lifecycle* onto the page. When a card names a dataset by version and cites a maintainer, the reader knows there is someone accountable for the dataset over time, and can trace the retention horizon. This is the seed of post-market surveillance (mod-110) applied at the dataset layer.

As with Mitchell, Gebru et al. deliberately do not fix a machine-readable schema, do not specify how the datasheet interacts with content-provenance manifests (chapter `06`), and do not distinguish between what a public consumer sees and what a regulator sees. Those are the gaps this module fills.

## The Hugging Face Model Card Guidebook

Between Mitchell/Gebru and the enterprise-scale assurance card, there is one artefact almost every practitioner has actually held in their hands: the Hugging Face model card. The Hub represents every hosted model with a `README.md` at the repo root; that README carries **YAML metadata** at the top (the *card metadata*) followed by structured Markdown sections that closely follow Mitchell et al.

Hugging Face publishes the guidebook, an annotated template, and a `metadata.json` schema. The three artefacts to know:

- The [**Model Cards documentation**](https://huggingface.co/docs/hub/model-cards) on the Hub docs — the field-by-field guide to what the YAML frontmatter carries (`license`, `language`, `base_model`, `pipeline_tag`, `library_name`, `datasets`, `metrics`, `tags`, `model-index` for benchmark results, and `co2_eq_emissions`) and how the Markdown sections align with Mitchell/Gebru's headers.
- The [**Model Card Guidebook**](https://huggingface.co/docs/hub/model-card-guidebook) — Ozoani, Gerchick, and Mitchell's operationalisation, with worked examples, an annotated template ([`modelcard_template.md`](https://github.com/huggingface/huggingface_hub/blob/main/src/huggingface_hub/templates/modelcard_template.md)), and prompts that push the author toward disaggregated evaluation and out-of-scope-use lists.
- The [**`ModelCard` and `DatasetCard` Python APIs**](https://huggingface.co/docs/huggingface_hub/en/guides/model-cards) in `huggingface_hub` — the programmatic surface for reading, writing, and validating the YAML frontmatter.

Two things the Hub does that Mitchell / Gebru do *not* are worth naming, because both foreshadow the assurance-card shape.

- **YAML frontmatter as machine-readable head.** The Hub separates *what a downstream tool needs to parse* (license, base model, datasets used, benchmark results in `model-index` shape) from *what a human needs to read*. This is the same separation the regulator submission will have to draw (chapter `07`): a machine-readable core the notified body's tooling can ingest, a human-readable body a reviewer can walk. The Hub is the first place most practitioners see this pattern; the assurance card generalises it.
- **`model-index` benchmark results.** The Hub's `model-index` field carries structured (task, dataset, metric, value) tuples that render as a leaderboard row. It is the closest thing the open-source ecosystem has to a machine-checked benchmark section, and it is the ancestor of the ISO/IEC 25059 quality-attribute spine chapter `05` builds on.

The gaps are also worth naming. The Hugging Face guidebook is written for a hosted-model publication context. It does not carry a threat model. It does not carry an eval-set integrity attestation. It does not carry a residual-risk narrative that a regulator can bind to Article 9. It does not distinguish between the version a public consumer sees and the version a market-surveillance authority sees. All four are what the enterprise-scale assurance-card shape has to add.

## Datasheet variants worth being aware of

Beyond the base Gebru datasheet, three variants have emerged that a card author should be able to recognise on sight.

- **Data Cards (Google Research, 2022).** Pushkarna, Zaldivar, and Kjartansson's *Data Cards Playbook* ([arXiv:2204.01075](https://arxiv.org/abs/2204.01075); [datacardsplaybook.org](https://sites.research.google/datacardsplaybook/)) reworks the Gebru template into a more structured, transparency-oriented artefact intended for downstream deployers rather than researchers, with explicit *audience adaptation* — a foreshadow of chapter `07`.
- **Dataset Nutrition Labels (Data Nutrition Project).** Holland, Hosny, Newman, Joseph, and Chmielinski's *The Dataset Nutrition Label* (2018) and the follow-up work at [datanutrition.org](https://datanutrition.org/) trade some of the datasheet's exhaustiveness for a rapid, at-a-glance summary. Regulator submissions rarely use this shape directly, but board narratives (chapter `07`) often adopt it.
- **Croissant metadata (MLCommons, 2024).** [ML Commons Croissant](https://mlcommons.org/working-groups/data/croissant/) is a machine-readable dataset metadata format built on schema.org that MLCommons intends as the interchange layer between dataset hosts and downstream tools. It is not a datasheet in Gebru's prose sense but it *is* the ancestor of the machine-readable dataset-card head an assurance card carries.

## Model-card variants worth being aware of

Three model-card variants extend or specialise the Mitchell base and are cited widely enough that a card author should recognise them.

- **FactSheets (IBM Research, 2018 / 2020).** Arnold et al.'s *FactSheets: Increasing Trust in AI Services through Supplier's Declarations of Conformity* ([arXiv:1808.07261](https://arxiv.org/abs/1808.07261)) frames the model card as a *supplier's declaration of conformity* — the closest early precursor to the EU AI Act's Article 47 declaration of conformity. The FactSheet vocabulary ("purpose," "target audience," "training / testing methodology," "domain," "known limitations") maps almost one-to-one onto Article 13.
- **Reward Reports (2022–2023).** Gilbert, Dean, Zick, and Lambert's *Reward Reports for Reinforcement Learning* ([arXiv:2204.10817](https://arxiv.org/abs/2204.10817)) extends the model-card idea for RL and RLHF systems, where the *reward function* is a first-class reporting object. The vocabulary shows up when a card has to describe post-training alignment interventions.
- **Interactive Model Cards.** Crisan, Drouhard, Vig, and Rajani's *Interactive Model Cards* (FAccT 2022, [arXiv:2205.02894](https://arxiv.org/abs/2205.02894)) study how card readers actually use them, and argue for interactivity where the reader can query the card's underlying evidence directly. The user-research findings inform the reviewer-experience choices chapter `07` returns to.

None of these are the required primary source — Mitchell et al. is — but the vocabulary shows up in enterprise cards often enough that a card author who cannot place them will be reading someone else's card without the right context.

## What the three primary sources fix — and what they leave for this module

By the end of this chapter you should be able to say, without notes:

- What Mitchell et al.'s nine sections are, what the disaggregation move is, and why the out-of-scope-use list is a first-class field rather than a footnote.
- What Gebru et al.'s seven sections are, why the provenance chain is what regulators expect, and why the maintenance section is what turns the datasheet into a lifecycle artefact.
- What the Hugging Face YAML frontmatter separates from the Markdown body, why that separation foreshadows the machine-readable core / human-readable body split, and where the `model-index` field sits relative to a benchmark result.
- What Data Cards, Nutrition Labels, Croissant, FactSheets, Reward Reports, and Interactive Model Cards add on top of the base.

What none of the three primary sources fix — and what the rest of this module will:

- **Traceability to an assurance case.** A Mitchell card does not point at a GSN case (mod-102) or an evidence node (mod-104). Chapter `02` names what fields the assurance-card shape has to add.
- **Regulator-facing structure.** A Mitchell card is not organised around Article 11 Annex IV, ISO/IEC 42001 clause 7.5, or ISO/IEC 42005 impact assessment. Chapters `02`, `04`, and `05` fix this.
- **System-level composition.** A model card describes a model. A regulator, notified body, or board reads the *system*. Chapter `03` composes model + dataset + eval + safety + tier-decision into one artefact and walks worked examples from OpenAI, Anthropic, Google, and Meta.
- **Content-provenance for GenAI outputs.** No card in the Mitchell / Gebru lineage carries a C2PA manifest attesting to the provenance of the model's outputs. Chapter `06` picks this up.
- **Audience variance.** Mitchell et al. write for "the reader"; a real card has four readers (public, regulator, third-party evaluator, board), and they cannot see the same disclosure. Chapter `07` closes this out.

## Summary

- Mitchell et al. (2019) fix the model-card shape: nine sections, disaggregated metrics, explicit out-of-scope-use lists, mitigations shipped alongside the model. Written *for accountability*, not for marketing.
- Gebru et al. (2021) fix the dataset-card shape: seven sections that force a provenance chain, an explicit "should not be used for" list, and a maintenance narrative.
- The Hugging Face model-card guidebook operationalises both into a `README.md` shape with YAML frontmatter that separates a machine-readable head from a human-readable body — the ancestor of the machine-readable / human-readable split every enterprise card has.
- Variants (Data Cards, Nutrition Labels, Croissant, FactSheets, Reward Reports, Interactive Model Cards) extend the base for particular audiences and modalities.
- What these three sources deliberately do not fix — traceability into an assurance case, regulator-facing structure, system-level composition, content-provenance, audience variance — is exactly what the remaining chapters of this module do.
