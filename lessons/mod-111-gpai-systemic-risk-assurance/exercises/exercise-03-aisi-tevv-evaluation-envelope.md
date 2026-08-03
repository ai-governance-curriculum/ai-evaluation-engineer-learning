# exercise-03: AISI TEVV Evaluation Envelope

**Estimated effort:** 2 hours

## Objective

Design the **AISI-shape TEVV evaluator envelope** — the self-contained, content-addressed handoff the release-assurance programme prepares so a third-party evaluator (UK AI Safety Institute, US AI Safety Institute, or a broadly-similar independent evaluator) can attach to the assurance case *cleanly*, walk from any risk claim to a specific evidence artefact in one hop, and independently reproduce a chosen subset of the evaluations. The envelope is indexed both by [NIST AI 600-1](https://doi.org/10.6028/NIST.AI.600-1)'s GenAI risk categories (the *what*) and by the four TEVV verbs (the *how*), and it cites — without duplicating — the peer-owned methodology depth of `model-evaluation-engineer`, `ai-risk-engineer`, and `agentic-safety-engineer`.

The exercise is envelope design and authoring, not solving. Placeholder evidence artefact IDs, evaluator API keys, and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the current AI 600-1 text, a specific evaluator's current access-model documentation, or the enterprise's own evidence store contents.

## Prerequisites

- Chapter [`03-aisi-tevv-and-nist-ai-600-1-generative-ai-profile-as-the-evaluator-envelope.md`](../03-aisi-tevv-and-nist-ai-600-1-generative-ai-profile-as-the-evaluator-envelope.md) — the AI 600-1 GenAI risk categories, the TEVV umbrella, the UK AISI + [Inspect](https://inspect.aisi.org.uk/) substrate, the US AISI + NIST portfolio, the evaluator-handoff structure, the pre-/at-/post-deployment timing distinctions, and the "what the programme does NOT hand over" discipline.
- Chapter [`01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md`](../01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md) — the Article 55 obligations the evaluator's report contributes evidence toward.
- Chapter [`02-frontier-lab-deployment-tier-frameworks-comparative-read.md`](../02-frontier-lab-deployment-tier-frameworks-comparative-read.md) — the frontier-framework citation the envelope carries.
- Skim access to [NIST AI 600-1](https://doi.org/10.6028/NIST.AI.600-1) end-to-end, plus the [UK AISI](https://www.aisi.gov.uk/) publications page, the [Inspect](https://inspect.aisi.org.uk/) documentation, and the [US AISI](https://www.nist.gov/aisi) landing page.
- Familiarity with `mod-104` (evidence pipeline — the content-addressed store, the reproducibility bundle shape, the assurance bundle at chapter `06`), `mod-102` (the assurance case's claim shape), and `mod-109` (third-party evaluator interface — the signed evaluation agreement, attack-payload non-disclosure).

## Problem statement

Continue from exercise `01`'s pinned release. The envelope must:

- **Be designed for a specific evaluator engagement timing.** Pick pre-deployment, at-deployment, or post-deployment (chapter `03` distinguishes the three). Pre-deployment is the default for a first-time systemic-risk release; a follow-up release may run at- or post-deployment.
- **Name the specific evaluator.** Pick UK AISI, US AISI, or a broadly-similar independent evaluator with a stated methodology and reporting convention. If you pick an independent evaluator without a public methodology, note this and provide the reference methodology `<!-- needs-research: … -->` markers.
- **Cover the AI 600-1 risk categories that apply to the release's modality set.** For a text-only LLM, essentially all twelve apply; for a text-to-image model, some categories (e.g., Confabulation for factual generation) may apply differently. State which categories are in-scope and why.
- **Cite the peer methodology owners without duplicating their content.** The envelope points at peer artefacts; it does not carry the peer artefacts inline.

## Requirements

Produce five artefacts in a single directory.

### 1. `evaluator-engagement-brief.md`

A one-page brief that pins the engagement scope:

- **Evaluator identity.** The specific evaluator (UK AISI, US AISI, or a named independent evaluator), the engagement channel, and the point-of-contact role on both sides. Cross-reference `mod-109` chapter `01` for the evaluator-relationship management.
- **Engagement timing.** Pre-deployment / at-deployment / post-deployment, with the wall-clock — engagement start date, expected report delivery, publication or embargo terms.
- **Access model.** Which access mode the evaluator is granted — model checkpoint + local runtime, hosted API with elevated rate limits, structured-access API with tool-use environment, or a combination. Cross-reference the signed evaluation agreement (`mod-109` chapter `01`).
- **Scope of evaluation.** Which capability categories and which risk categories the engagement covers. Where the engagement is a subset of the release's full risk surface, state which categories are in-scope for *this* engagement and which are covered elsewhere.
- **Reporting convention.** Whether the evaluator publishes independently, publishes with provider response, or reports internally-only to the provider (with subsequent disclosure to the AI Office where required). `<!-- needs-research: verify current UK / US AISI publication conventions -->` where necessary.
- **Article 55 tie-in.** Which Article 55(1)(a)–(d) sub-obligations the engagement's outputs directly contribute evidence toward. Cross-reference exercise `01`'s obligation map.

### 2. `ai-600-1-crosswalk.md`

The AI 600-1 crosswalk — the *what-is-evaluated* index. Structured as a table with the following columns.

| Column | Content |
| --- | --- |
| AI 600-1 risk category | The category number and name (chapter `03` enumerates the twelve). Mark `<!-- needs-research: verify against current published AI 600-1 text -->` where the category set has drifted. |
| In-scope for this engagement? | Yes / No / Partial, with a one-line reason. |
| Release-gate criterion | The specific release-gate criterion (or set of criteria) from `mod-103` that addresses the category. |
| Discharging evidence | The evidence-artefact class(es) from the store (`mod-104` chapter `02`) that discharge the criterion. |
| AI RMF sub-category cross-references | The specific `FUNCTION-CATEGORY.SUBCATEGORY` sub-categories from AI RMF 1.0 that AI 600-1 cross-references for this category. |
| Peer-role owner | Which peer track owns the methodology for the evidence (`model-evaluation-engineer`, `ai-risk-engineer`, `agentic-safety-engineer` at level 40, `ai-alignment-engineer`, or `ai-infra-security`). |
| Evaluator handoff pointer | The store-digest reference the evaluator receives for this category, or a `<!-- needs-research: … -->` marker if the reproducibility bundle for this category is not yet finalised. |

At minimum, the crosswalk includes one row per AI 600-1 risk category:

1. CBRN Information or Capabilities.
2. Confabulation.
3. Dangerous, Violent, or Hateful Content.
4. Data Privacy.
5. Environmental Impacts.
6. Harmful Bias or Homogenisation.
7. Human-AI Configuration.
8. Information Integrity.
9. Information Security.
10. Intellectual Property.
11. Obscene, Degrading, and/or Abusive Content.
12. Value Chain and Component Integration.

Rows marked "Out-of-scope" for the specific engagement must still state where the category *is* addressed elsewhere in the assurance programme, so the evaluator understands the boundary.

### 3. `tevv-artefact-index.md`

The *how-is-evaluated* index. For each in-scope AI 600-1 risk category from artefact 2, name the four TEVV-verb artefacts:

- **Testing artefacts.** Which capability-elicitation runs, benchmark runs, or red-team probes cover the category. Cite by name and store digest. Foreshadow exercise `04` — the benchmark-citation pack is what populates most of this column for safety-relevant categories.
- **Evaluation artefacts.** How the test outputs are scored against criteria — the scoring rubric, the threshold rationale, the peer-owned reading of the score. Cite the peer artefact.
- **Verification artefacts.** How the results verify against the provider's stated capability envelope — the assurance-case claim node (`mod-102`), the frontier-framework tier landing (chapter `02` / exercise `02`), and the tier-landing evidence.
- **Validation artefacts.** How the results validate against the intended real-world need — deployment-context evaluation, red-team-in-context runs, third-party audit reports (if available), post-market signal from prior releases (cross-reference `mod-110`).

The index is dual-navigable: a row can be reached from the AI 600-1 crosswalk (via risk-category link) or from a TEVV-verb view (all Testing artefacts across categories, all Evaluation artefacts across categories, etc.). Present both views.

### 4. `reproducibility-bundle-manifest.md`

The manifest of reproducibility bundles the evaluator receives access to (per `mod-104` chapter `03`'s reproducibility-bundle discipline). For each bundle, the manifest carries:

- **Bundle name and digest.** The reproducibility bundle's canonical name (e.g., `harmbench-v1-2-configured-2026-05-07`) and its content-addressed digest.
- **Bundle contents summary.** What the bundle contains — evaluation definition (Inspect script for UK AISI engagements, or equivalent for other evaluators), pinned model checkpoint reference, pinned dataset digest, pinned dependency lockfile, run instructions, and the recorded result.
- **Environment specification.** The runtime environment the bundle expects — Inspect version, Python version, GPU / TPU requirements, memory requirements, expected wall-clock, expected cost.
- **Reproduction instructions.** Step-by-step commands the evaluator runs to reproduce the result independently, or a pointer to a `README.md` in the bundle that carries them.
- **AI 600-1 category link.** The category (or categories) the bundle's result feeds evidence to, per artefact 2.
- **Peer-owner methodology reference.** The peer-owned artefact that carries the methodology reading of the result. The evaluator escalates methodology questions there, not to the release-assurance programme.

At minimum, the manifest includes reproducibility bundles for:

- One capability-elicitation run per in-scope AI 600-1 category with a safety-benchmark citation (foreshadow exercise `04`).
- The internal red-team report bundle for the release (owned by `ai-risk-engineer`).
- The agentic-safety red-team report bundle (owned by `agentic-safety-engineer` at level 40) if the release is agentic-capable.
- The guardrail-evaluation report bundle (owned by `ai-risk-engineer` or `model-evaluation-engineer`).
- The mitigation-effectiveness measurement bundle (owned by `ai-risk-engineer`).

For each bundle, the manifest is *content-addressed* — the digest resolves to a specific commit at bundle-generation time, and the evaluator can verify the digest end-to-end.

### 5. `handoff-package-composition.md`

The composition of the *handoff package* itself — the self-contained, signed archive the evaluator receives. Structured as a directory listing plus a description.

The package contains:

- `assurance-case.sacm.json` — the SACM `ArgumentPackage` at engagement start (per `mod-102`).
- `ai-600-1-crosswalk.md` — artefact 2.
- `tevv-artefact-index.md` — artefact 3.
- `reproducibility-bundle-manifest.md` — artefact 4.
- `frontier-framework-citation.md` — the enterprise-framework citation from exercise `02`, with the tier landing for the release.
- `article-55-obligation-map.md` — exercise `01`'s obligation map (or an evaluator-appropriate subset).
- `state-of-the-art-justification.md` — the justification narrative for why the evaluation set cited under Article 55(1)(a) is state-of-the-art at release date. Cite the [Frontier Model Forum](https://www.frontiermodelforum.org/) briefs, AISI publications, and any other shared references from exercise `02`.
- `access-artefacts/` — the API keys, model-checkpoint references, evaluation-dataset digests, and canary tokens the evaluator uses. Cross-reference `mod-104` chapter `05` for the eval-set-security regime governing canaries.
- `evaluation-agreement.pdf` — the signed evaluation agreement per `mod-109` chapter `01` (attack-payload non-disclosure, IP protection, result-disclosure terms).
- `README.md` — the package's own README, with the pointer graph the evaluator walks first.

The package is signed as a whole (a top-level `dsse-envelope.json` or equivalent, per `mod-104` chapter `06`) so the evaluator can verify integrity end-to-end. The signing role is the release-assurance methodology owner, with co-signing by the head-of-AI-governance role for the state-of-the-art justification.

Include a two-paragraph *reviewer walkthrough* at the top of the composition — the numbered sequence an evaluator uses on receipt: verify the top-level signature, read `README.md`, read `evaluator-engagement-brief.md`, read `article-55-obligation-map.md`, read `ai-600-1-crosswalk.md`, pick a category, resolve to a reproducibility bundle from `reproducibility-bundle-manifest.md`, reproduce the result.

## Starter guidance

- **The envelope is *the interface*, not the content.** Chapter `03` names the discipline: the release-assurance programme owns *plumbing*, not methodology. The envelope points at peer artefacts. If the envelope inlines a red-team methodology, the boundary between roles has slipped.
- **Both indices resolve to the same artefacts.** The AI 600-1 crosswalk and the TEVV-verb view are two navigations of the same underlying set. If they resolve to different artefacts, the envelope is either double-storing evidence or mis-indexing it.
- **The reproducibility bundle is what makes the envelope credible.** An envelope that cites results but does not give the evaluator a path to reproduce them independently is not doing the work Article 55(1)(a)'s "adversarial testing" language requires. Every result cited has a reproducibility bundle behind it, or the citation is flagged as un-reproducible with a rationale.
- **Inspect is a shared substrate for UK AISI engagements.** If the evaluator is UK AISI, the reproducibility bundle for a capability evaluation is an Inspect script, an Inspect version, a pinned dependency lockfile, and the checkpoint reference. This is what makes the reproduction one-command for the evaluator side.
- **Pre-deployment / at-deployment / post-deployment change the handoff shape.** Pre-deployment carries the assurance-case-at-freeze and can influence release. At-deployment carries the assurance-case-at-release and informs the post-market plan. Post-deployment carries the assurance-case-at-current-state and drives re-evaluation. State which and design the manifest accordingly.
- **The Article 55 tie-in is one-to-many.** A single reproducibility bundle can contribute evidence to more than one Article 55 sub-obligation (a WMDP-run bundle contributes to (1)(a) state-of-the-art evaluation and to the CBRN portion of (1)(b) Union-level systemic-risk assessment). The AI 600-1 crosswalk carries the multi-obligation contribution; the manifest carries the direct reproducibility path.
- **Handoff timing changes the access artefacts.** Pre-deployment access to a checkpoint may need a specially-provisioned inference environment; at-deployment access may be identical to the production API; post-deployment access may be a snapshotted checkpoint. State which and provision the `access-artefacts/` directory accordingly.
- **`<!-- needs-research: … -->` is a legitimate answer.** The AI 600-1 category set, the current UK / US AISI publication conventions, the current Inspect version, and the current independent-evaluator methodology all drift on faster cadences than a curriculum chapter can pin. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `evaluator-engagement-brief.md` names the specific evaluator, the engagement timing, the access model, the scope, the reporting convention, and the Article 55 tie-in. A reviewer can decide from the brief alone what the engagement covers.
- `ai-600-1-crosswalk.md` has one row per AI 600-1 risk category. In-scope rows carry release-gate criteria, discharging evidence, AI RMF cross-references, peer-role owner, and evaluator handoff pointer. Out-of-scope rows state where the category is addressed elsewhere.
- `tevv-artefact-index.md` covers the four TEVV verbs per in-scope category. Both AI 600-1-indexed and TEVV-verb-indexed views are present.
- `reproducibility-bundle-manifest.md` lists at least one capability-elicitation bundle per in-scope safety category, plus the internal red-team bundle, the agentic-safety bundle (if the release is agentic), the guardrail-evaluation bundle, and the mitigation-effectiveness bundle. Each bundle carries name, digest, contents summary, environment specification, reproduction instructions, AI 600-1 category link, and peer-owner methodology reference.
- `handoff-package-composition.md` lists every file in the package, describes the sign-and-verify pathway end-to-end, and carries the two-paragraph reviewer walkthrough.
- The envelope cites peer artefacts by store digest; no peer artefact's methodology is inlined.
- Every place a fact would need to be verified against the current AI 600-1 text, the current UK / US AISI convention, or a specific reproducibility-bundle digest is marked `<!-- needs-research: … -->` rather than guessed.
- The handoff timing (pre / at / post-deployment) is stated and drives the access-artefact provisioning.
- The signed evaluation agreement is present in the package (or referenced by digest to `mod-109` chapter `01`'s master).

## Stretch goals

- **Author the Inspect-expressed evaluation stub.** In `inspect-evaluation-stub/`, write a short Inspect script for one AI 600-1 category (e.g., an information-security prompt-injection probe drawing on AgentDojo-style patterns) that a UK AISI evaluator could run against a hosted checkpoint. `<!-- needs-research: verify Inspect API stability -->` where the Inspect API surface is uncertain.
- **Design the multi-evaluator engagement.** In `multi-evaluator-plan.md`, sketch an engagement where UK AISI and US AISI both attach concurrently — how the shared reproducibility-bundle manifest serves both, where the reporting conventions diverge, and how the assurance bundle records both engagements without collision. Cross-reference `mod-106`.
- **Draft the evaluator-response integration procedure.** In `evaluator-response-integration.md`, sketch how the evaluator's report — once received — lands back into the assurance bundle as a new evidence node, is signed by the evaluator, and is cited from the assurance case as new claim-supporting evidence. Cross-reference `mod-104` chapter `06`.
- **Author the post-deployment re-evaluation package.** In `post-deployment-envelope.md`, adapt the envelope for a post-deployment engagement — the same crosswalk with an added *change-since-release* column (deployment signals from `mod-110`, incident reports, new benchmark releases) and an updated reproducibility-bundle manifest that reflects any model or infrastructure changes since the initial release.
- **Cross-reference `mod-109`.** In `mod-109-alignment-note.md`, describe how the envelope's evaluation agreement, attack-payload non-disclosure clauses, and result-disclosure timing align with `mod-109` chapter `01`'s master evaluator interface. The envelope inherits from the master; state any deltas.
