# NIST AI RMF Crosswalk (with the GenAI Profile / AI 600-1)

## Motivation

Chapter `02` produced a set of deliverables anchored to EU AI Act articles. This chapter cross-tags each of those deliverables to the **NIST AI RMF 1.0** sub-category that carries the same obligation, and — for GenAI systems — to the additional **GenAI Profile** (NIST AI 600-1) suggested actions that layer on top.

The value of this cross-tag is not that NIST AI RMF is a duplicate framework the release-gate must independently satisfy. It is that a large fraction of the assurance program's audience (US federal, US enterprise, and multinational deployers who have made NIST alignment a procurement condition) speaks in RMF sub-category IDs. If the same deliverable that discharges EU AI Act Article 15 also carries a `MEASURE-2.7` tag, the release-gate can answer both audiences from the same evidence.

`mod-101` chapter `02` walked the four functions and the Playbook. This chapter assumes that vocabulary and moves directly to the crosswalk.

## The cross-tag row extension

Every EU AI Act row on the map picks up two additional fields:

| Field | Content |
| --- | --- |
| `sibling_nist_rmf` | One or more sub-category references (e.g. `MAP-1.1`, `MEASURE-2.7`, `MANAGE-1.3`). Not a single ID — an obligation frequently plugs into several |
| `sibling_nist_ai_600_1` | GenAI-Profile risk category and suggested-action reference — only where the system includes generative capabilities |

The Playbook (published at `airc.nist.gov`) is the reference for which sub-categories cover which suggested actions. The mapping below is the recurring pattern the release-assurance program uses; individual programs adjust the tags per system.

## Article-to-sub-category mapping

### Article 9 (risk-management system) → MAP-1, MAP-2, MAP-5, MANAGE-1, MANAGE-4

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art9.plan` | `MAP-1.1`, `MAP-1.5`, `MAP-2.1`, `MAP-2.2`, `MAP-2.3` | Context and system categorisation are pre-requisites to the risk-management plan |
| `eu-ai-act.art9.harms` | `MAP-5.1`, `MAP-5.2` | Impact characterisation on individuals, groups, communities |
| `eu-ai-act.art9.residuals` | `MANAGE-1.2`, `MANAGE-1.3` | Prioritisation of risks and decisions to accept / mitigate / avoid |
| `eu-ai-act.art9.feedback-loop` | `MANAGE-4.1`, `MANAGE-4.2` | Post-deployment monitoring and communication |

**GenAI Profile overlay.** For a GenAI system, the harm inventory picks up the GenAI-Profile risk categories: confabulation, harmful bias, information integrity, information security, IP, obscene / degrading content, value-chain and component integration, and more. The `sibling_nist_ai_600_1` field on `eu-ai-act.art9.harms` lists the applicable categories.

### Article 10 (data governance) → MAP-4, MEASURE-2.11, GOVERN-1.6

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art10.governance-plan` | `GOVERN-1.6`, `MAP-4.1` | Standing policy on third-party data and lineage |
| `eu-ai-act.art10.bias-report` | `MEASURE-2.11` | Fairness with harmful bias managed |
| `eu-ai-act.art10.dataset-cards` | `MAP-4.1`, `GOVERN-1.4` | Documentation of data provenance |
| `eu-ai-act.art10.lineage-manifest` | `GOVERN-6.1`, `MAP-4.2` | Third-party dependency tracking |

**GenAI Profile overlay.** GenAI-Profile pulls IP (from the training data) and information integrity (whether training data is authentic) into MAP-4 and MEASURE-2.6.

### Article 11 (technical documentation / Annex IV) → GOVERN-1.4, MAP-1.1, transverse

The Annex IV dossier is a *superset* container — it points at every article's evidence. The map's Article 11 sub-rows therefore cross-reference many sub-categories:

- Annex IV section 1 (general description) → `MAP-1.1`
- Annex IV section 2 (development process) → `MAP-3.1`, `MAP-3.3`
- Annex IV section 3 (monitoring, functioning, control) → `MANAGE-4.1`
- Annex IV section 4 (risk-management system) → cross-ref to Article 9 rows
- Annex IV section 5 (changes over lifecycle) → `GOVERN-1.4`, `MANAGE-2.4`
- Annex IV section 6 (standards applied) → `GOVERN-1.1`
- Annex IV section 7 (declaration) → cross-ref to Article 47 row
- Annex IV section 8 (post-market plan) → cross-ref to Article 72 row

### Article 12 (record-keeping) → MEASURE-3.1, MANAGE-4.1, GOVERN-1.7

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art12.logging-design` | `MEASURE-3.1`, `GOVERN-1.7` | Mechanisms for tracking identified AI risks over time; incident-management readiness |
| `eu-ai-act.art12.retention-policy` | `GOVERN-1.7`, `GOVERN-4.3` | Documentation retention and continuous improvement |
| `eu-ai-act.art12.completeness-report` | `MEASURE-4.1`, `MEASURE-4.2` | Measurement efficacy — do we know the logging works? |
| `eu-ai-act.art12.integrity-plan` | `MEASURE-2.7`, `GOVERN-6.1` | Tamper-evidence sits under security / resilience |

### Article 13 (transparency) → MEASURE-2.8, GOVERN-5

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art13.instructions-for-use` | `MEASURE-2.8`, `GOVERN-5.1` | Transparency and accountability; engagement with AI actors |
| `eu-ai-act.art13.deployer-card` | `MEASURE-2.8`, `GOVERN-5.2` | Cards are the audience-facing transparency artefacts |
| `eu-ai-act.art13.adequacy-review` | `MEASURE-4.1` | Measurement of transparency adequacy |

### Article 14 (human oversight) → MEASURE-2.9, MEASURE-3.3, GOVERN-3

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art14.oversight-design` | `MEASURE-2.9` | Explainability and interpretability characteristic |
| `eu-ai-act.art14.usability-report` | `MEASURE-3.3` | Feedback about efficacy of measurement — the automation-bias evaluation |
| `eu-ai-act.art14.training-log` | `GOVERN-3.2` | Workforce training on AI risk |

### Article 15 (accuracy, robustness, cybersecurity) → MEASURE-2.5, MEASURE-2.6, MEASURE-2.7

| EU AI Act row | NIST AI RMF sub-categories | Rationale |
| --- | --- | --- |
| `eu-ai-act.art15.accuracy-declaration` | `MEASURE-2.3`, `MEASURE-2.5` | Validity and reliability; performance evaluation |
| `eu-ai-act.art15.robustness-report` | `MEASURE-2.6` | Safety characteristic — robustness under stress |
| `eu-ai-act.art15.cybersecurity-report` | `MEASURE-2.7` | Security and resilience — the anchor for AI 100-2 taxonomy |
| Sub-row: adversarial examples | `MEASURE-2.7` + NIST AI 100-2 | Attack category from Article 15(5) |
| Sub-row: data / model poisoning | `MEASURE-2.7` + NIST AI 100-2 | Attack category |
| Sub-row: model evasion | `MEASURE-2.7` + NIST AI 100-2 | Attack category |
| Sub-row: confidentiality attacks | `MEASURE-2.7` + NIST AI 100-2 | Attack category |

**GenAI Profile overlay.** AI 600-1 adds prompt-injection, jailbreak, and hallucination-in-safety-critical-outputs risks to MEASURE-2.7 and MEASURE-2.6.

### Article 17 (QMS) → GOVERN-1, GOVERN-2

Article 17's numbered content list closely tracks the GOVERN function of RMF and the clause 4–10 shape of ISO/IEC 42001. On the map, the QMS row is a *deliverable-set* row — the QMS itself is not a single artefact but the union of the policies and procedures that GOVERN-1 through GOVERN-6 name.

### Article 26 (deployer obligations) → GOVERN-6, MAP-4, MANAGE-2, MANAGE-4

Deployer rows are heavier on GOVERN-6 (third-party governance — the deployer is a downstream user of a provider's system) and MANAGE-2 / MANAGE-4 (response strategy and communication).

### Article 43 (conformity assessment) → GOVERN-4, MANAGE-2.4

The conformity-assessment decision-record row picks up GOVERN-4 (accountability) and MANAGE-2.4 (documentation of risk treatment).

### Article 47 (declaration of conformity) → GOVERN-1.4

The declaration is a documentation artefact; GOVERN-1.4 is the corresponding sub-category.

### Article 49 (registration) → GOVERN-4.1

Registration is an accountability action.

### Article 61 (serious-incident reporting) → MANAGE-4.3, GOVERN-1.7

The response plan and drill log both cite MANAGE-4.3 (communication and continuous improvement) and GOVERN-1.7 (incident-response readiness).

### Article 72 (post-market monitoring plan) → MANAGE-4.1, MEASURE-3.1

The plan and the review report both cite MANAGE-4.1 (post-deployment monitoring) and MEASURE-3.1 (mechanisms for tracking risks over time).

## GenAI Profile — the additional row block

For GenAI systems, the map picks up a distinct **GenAI Profile row block** carrying the AI 600-1 risk categories that do not have a one-to-one Article number but which the RMF-aligned audience will expect to see. The block sits alongside the article rows and typically covers:

- Confabulation (hallucination) — evidence of hallucination-rate measurement and mitigation
- Harmful bias — for GenAI outputs specifically, distinct from Article 10 dataset-side bias
- Human-AI configuration — evidence that human-oversight design accounts for GenAI-specific overreliance patterns
- Information integrity — provenance / watermarking / C2PA evidence (cross-references `mod-105`)
- Information security — jailbreak / prompt-injection resilience (cross-references Article 15 rows)
- Intellectual property — evidence of training-data licensing posture and copyright policy (cross-references Article 53 for GPAI providers)
- Value chain and component integration — evidence of downstream deployer-facing controls and supplier attestations
- Obscene / degrading / abusive content — evidence of content filtering evaluation
- Environmental impact — evidence of compute-cost and carbon posture (release-gate consumes but does not author)

Each row has an owner peer role (predominantly `ai-risk-engineer` for the first six, `ai-infra-security` for information security, `ai-governance-analyst` for value chain, platform-eng for environmental).

## AI 100-2 — the adversarial-ML taxonomy overlay

Under Article 15's cybersecurity row (and its sub-rows), the AI 100-2 taxonomy provides the vocabulary the row's evidence uses. The taxonomy breaks attacks by capability (evasion, extraction, inference, poisoning), knowledge (white-box, grey-box, black-box), goal, and specificity. The map's cybersecurity sub-rows should identify which taxonomy branch each evaluation covers, so a reader can spot gaps (e.g. "we evaluated evasion and inference, but not extraction").

## Worked example — one obligation cross-tagged end-to-end

Take Article 15 accuracy for a GenAI-augmented CV-screening system:

```yaml
obligation_id: eu-ai-act.art15.accuracy-declaration
instrument: eu-ai-act-2024-1689
article_or_clause: Article 15(1)(2)(3)
obligation_summary: Declare accuracy metrics, thresholds, and rationale
applies_when: high-risk provider under Annex III point 4
deliverable: accuracy-threshold-declaration-v3.md
deliverable_kind: declaration
owner_role: model-evaluation-engineer
signing_role: ai-evaluation-engineer  # this role
sibling_nist_rmf: [MEASURE-2.3, MEASURE-2.5]
sibling_nist_ai_600_1:
  - risk: confabulation (screening reasons contain hallucinated citations)
    suggested_actions: [MS-2.3-002, MS-2.5-005]  # illustrative Playbook references
sibling_iso_clauses: [ISO/IEC 42001 clause 8.3, ISO/IEC 25059 5.2]  # filled in chapter 04
tier_applicability: [tier-1, tier-2, tier-3]
status: covered
evidence_pointer: sha256:d3f9…
```

This single row is now readable by four audiences: an EU market-surveillance authority (via `article_or_clause`), a US enterprise procurement team (via `sibling_nist_rmf` and `sibling_nist_ai_600_1`), an ISO 42001 audit team (via `sibling_iso_clauses`, coming next chapter), and a downstream deployer procuring the system (via `deliverable_kind` and `owner_role`).

## Where the crosswalk breaks down

- **Some Article rows have no natural sub-category.** Article 49 (registration) plugs into GOVERN-4.1 only weakly; it is primarily a filing action, not a risk-management action. The map should mark the sub-category as `citation-only` on such rows.
- **Some sub-categories are populated by multiple articles.** MEASURE-2.7 attracts Article 12, Article 15, and Article 55 evidence for a systemic-risk GPAI provider. The `sibling_nist_rmf` field is many-to-many.
- **Playbook references are the Playbook's own IDs.** The `sibling_nist_ai_600_1` example above uses `MS-2.3-002` as a synthetic ID; when authoring, use the actual Playbook / AI 600-1 IDs current at authoring time.
- **RMF 1.0 is stable; the Playbook is continuously updated.** The map should carry a `nist_playbook_version` field per row and refresh it when a suggested-action reference changes.

## Where this shows up in the rest of the track

- `mod-102` — assurance-case argument nodes cite the same sub-categories.
- `mod-103` — release-gate schema carries `nist_ai_rmf_subcategory` on every obligation.
- `mod-104` — evidence artefacts are tagged with sub-category IDs for retrieval.
- `mod-105` — cards carry a NIST AI RMF crosswalk section derived from these rows.
- `mod-107` — sector rules cite RMF sub-categories where applicable (SR 11-7 model-risk activities align with MAP-3 / MEASURE-2 / MANAGE-1).
- `mod-108` — deployment-tier gating uses sub-category coverage as one of the tier criteria.
- `mod-109` — third-party evaluators (particularly US NIST AISI consortium participants) expect the sub-category tags on hand-off artefacts.
- `mod-111` — the GPAI systemic-risk assurance module leans hard on AI 600-1 rows and MEASURE-2.7 for adversarial evaluation.

## Summary

- Each EU AI Act row on the map picks up a `sibling_nist_rmf` field (one-to-many sub-categories) and, for GenAI systems, a `sibling_nist_ai_600_1` field (GenAI-Profile risk category and suggested actions).
- The GenAI Profile also generates a *distinct* row block for risks (confabulation, information integrity, IP, value-chain integration) that do not have a one-to-one Article number.
- AI 100-2 provides the adversarial-ML taxonomy that cybersecurity sub-rows are labelled with.
- The crosswalk is many-to-many; the Playbook version has to be pinned per row because Playbook suggested actions evolve.
- Exercise 02 walks you through building a NIST-RMF cross-tag for a scenario worked in exercise 01; chapter `04` adds the ISO clause spine.
