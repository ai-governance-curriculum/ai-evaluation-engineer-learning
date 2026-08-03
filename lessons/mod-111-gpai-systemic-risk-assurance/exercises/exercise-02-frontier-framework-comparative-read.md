# exercise-02: Frontier-Lab Framework Comparative Read

**Estimated effort:** 3 hours

## Objective

Read the four reference frontier-lab frameworks — Anthropic Responsible Scaling Policy, OpenAI Preparedness Framework, Google DeepMind Frontier Safety Framework, Meta Frontier AI Framework — *comparatively*, and produce the artefact set a GPAI-systemic-risk assurance case cites when it names one of them (or an enterprise adaptation) as the mechanism through which the [EU GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) safety-and-security-chapter commitments are met. The output is a table plus supporting artefacts that show the four-part shape holding across the frameworks, name where they diverge on specifics, and pin the enterprise's choice-and-adaptation to a specific pre-commitment set an AI Office reviewer can walk.

The exercise is comparative reading and authoring, not solving. Placeholder-tier landings and `<!-- needs-research: … -->` markers are legitimate answers where a threshold, category, or governance-body name would need to be verified against the current published version of a framework.

## Prerequisites

- Chapter [`02-frontier-lab-deployment-tier-frameworks-comparative-read.md`](../02-frontier-lab-deployment-tier-frameworks-comparative-read.md) — the four-part shape, the four reference frameworks, the two shared primitives (pre-commitment as governance device; elicitation-based evaluation), and the three columns of the comparative read (where they agree, where they diverge, where the enterprise adapts).
- Chapter [`01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md`](../01-eu-ai-act-article-55-and-the-gpai-code-of-practice.md) — the Code-of-Practice safety-and-security commitments the framework citation discharges.
- Skim access to the four current published frameworks:
  - [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy).
  - [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/).
  - [Google DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/).
  - Meta Frontier AI Framework (Meta's frontier-model safety framework; `<!-- needs-research: verify the canonical URL and current version at drafting date -->`).
- Skim access to at least two [Frontier Model Forum](https://www.frontiermodelforum.org/) issue briefs.
- Familiarity with `mod-108` (enterprise adaptation of deployment-tier gating) — this exercise reads the *same* frameworks with a different lens (Article 55 discharge, not enterprise deployment scheme).

## Problem statement

Continue from exercise `01`'s pinned release (or pin one afresh if you have not worked exercise `01`). The comparative read must:

- **Cover all four reference frameworks.** No skipping. A GPAI-systemic-risk assurance case that cites only one framework without a comparative read against the alternatives cannot honestly claim the "state-of-the-art" position that Article 55(1)(a) requires — the state of the art is what the industry publishes together, not what one lab publishes alone.
- **Pin to specific published versions.** Frameworks are revised; a comparative read against a version that has been superseded is stale before it is authored. Every framework cited names its version (and its publication date), or is marked `<!-- needs-research: … -->` if the version pin is uncertain.
- **Name the enterprise's choice and pre-commitments.** The output includes a specific *citation-into-a-pre-commitment* — not "we follow RSP-shaped tiering" but "we follow FSL-3 pre-commitments PC-3.1 through PC-3.5 per version 2.1 of our internal framework, published 2026-04-17". Placeholder specifics are legitimate; hand-waving is not.

## Requirements

Produce five artefacts in a single directory.

### 1. `framework-version-pinning-brief.md`

A one-page brief that pins the reading substrate. For each framework:

- **Canonical URL and title.** The specific landing page the reading is against.
- **Version and publication date.** The version identifier the framework carries (RSP has been revised multiple times; Preparedness has been substantively updated; FSF is on iterative revision; Meta's framework was first published in early 2025). Mark `<!-- needs-research: verify the current version at drafting date -->` where uncertain.
- **Framework scope.** One sentence on which models the framework applies to at the publisher (all frontier models, models above a stated compute or capability threshold, deployed models only, etc.).
- **Governance body.** The internal body accountable for tier decisions at the publisher (Anthropic's Responsible Scaling Officer function; OpenAI's Safety Advisory Group and Safety and Security Committee; DeepMind's internal review structure; Meta's internal structure). `<!-- needs-research: … -->` where the current naming is uncertain.
- **Publication cadence commitment.** The publisher's stated cadence for revising the framework (annually, on demand, on capability crossings) — if stated.

At the bottom of the brief, include a *shared-substrate note*: two to three sentences on where the four frameworks share substrate — capability categories that appear in all four (biosecurity / CBRN, cyber-offensive, model autonomy / autonomous replication are the recurring ones); pause-and-strengthen as the shared pre-commitment shape; the Frontier Model Forum as the shared publication surface. This note grounds the comparative read that follows.

### 2. `comparative-read-table.md`

The four-column comparative table. Structured with one row per structural element the four frameworks share.

Header row:

| Structural element | Anthropic RSP | OpenAI Preparedness Framework | Google DeepMind FSF | Meta Frontier AI Framework |
| --- | --- | --- | --- | --- |

At minimum, the table has rows for:

- **Ladder shape.** Single-ladder (RSP-style ASL) vs. per-category ladder (Preparedness-style banding) vs. per-domain thresholds (FSF-style CCLs) vs. outcome-tier (Meta-style high-risk / critical-risk). One sentence per cell.
- **Capability categories tracked.** The specific categories the framework names, in the current version. Mark `<!-- needs-research: … -->` where the category set has changed and the current set is uncertain.
- **Threshold operationalisation.** How thresholds are stated per category — narrative capability descriptions, quantitative benchmark thresholds, elicitation-triggered thresholds, or a combination.
- **Deployment-mitigation vs. security-mitigation separation.** RSP pairs a deployment standard and a security standard per ASL. FSF explicitly separates deployment mitigations and security mitigations. Preparedness and Meta's treatment of this separation. One sentence per cell.
- **Escalation and pre-commitment shape.** The specific commitment at threshold crossing — pause deployment, pause training, restrict scope, invoke additional review. One sentence per cell.
- **Governance body / escalation authority.** The named body responsible for tier decisions (see the framework-version-pinning brief) and the escalation authority above it (board committee, executive, etc.). `<!-- needs-research: … -->` where uncertain.
- **Third-party evaluator involvement.** The claimed proportion and shape of third-party evaluation, and any AISI-relationship commitments. Cross-reference chapter `03` and `mod-109`.
- **Periodic re-evaluation cadence.** The FSF's early-warning-evaluation primitive; the equivalent in each other framework (if stated).
- **Mitigation-effectiveness measurement.** The FSF's mitigation-effectiveness primitive; the equivalent in each other framework (if stated).
- **Framework-revision procedure.** How the framework itself is revised — publication of a superseding version, a change-log, a stated review cadence.

Where a cell would require guessing, mark `<!-- needs-research: … -->`.

Under the table, include a two-to-three-paragraph *interpretation note* that names:

- Which two or three structural elements the frameworks agree on most tightly (typically ladder shape as a family — capability evidence → tier → mitigation obligations → pre-commitment — plus the pause-and-strengthen commitment).
- Which two or three structural elements the frameworks diverge on most sharply (typically capability-category naming, threshold operationalisation, and third-party-evaluator involvement).
- Which specific rows carry the highest *reviewer-visible signal* — the rows an AI Office reviewer would open first when comparing the enterprise's cited framework against alternatives.

### 3. `frontier-model-forum-reading-list.md`

The Frontier Model Forum publishes issue briefs and working-group outputs as a *shared industry reference surface* (chapter `02`). Pick at least two current issue briefs and:

- **Cite each brief with its title, publication date, and URL.** `<!-- needs-research: verify current publication list at [frontiermodelforum.org](https://www.frontiermodelforum.org/) -->` where the specific brief's current URL is uncertain.
- **State the reading purpose.** For each brief, one to two sentences on how it informs a specific row in the comparative-read table (e.g., a brief on third-party-evaluator engagement informs the third-party-evaluator-involvement row; a brief on capability-elicitation methodology informs the threshold-operationalisation row).
- **Note the citation-in-assurance-case value.** For each brief, whether and how the enterprise cites it in the assurance case's state-of-the-art justification (chapter `01`, Article 55(1)(a)).

The reading list is short but load-bearing — it is what the state-of-the-art justification uses to anchor the enterprise's evaluation methodology against a shared industry reference.

### 4. `enterprise-framework-citation.md`

The specific citation the enterprise carries in its assurance bundle. Given the release from artefact 1 (and exercise `01` if you continued it), the citation names:

- **Framework choice.** Which of the four frameworks the enterprise adopts *shape from* (RSP-shape, Preparedness-shape, FSF-shape, or Meta-shape). Where the choice is a hybrid (elements of two or more), name each element and its source. `mod-108` chapter `01` is a foreshadow of the enterprise-adaptation discipline; this artefact is that adaptation for the *Article 55 discharge* citation.
- **Framework version identifier.** The enterprise's own version identifier for its adopted framework — a version number, a content-addressed digest, or both — with the publication date and the signer. Placeholder version identifiers are legitimate.
- **Capability-category set.** The categories the enterprise tracks. Often the source framework's set unchanged; if modified, the diff is stated (which categories added, which removed, which renamed, why).
- **Tier landing for the release.** The tier the release candidate sits at (e.g., FSL-3, ASL-3-equivalent, "critical-risk-adjacent"), with the capability-evidence artefacts that place it there.
- **Pre-commitments discharged.** The specific pre-commitments the enterprise binds itself to at this tier — enumerated as PC-3.1, PC-3.2, PC-3.3, etc. (adopting the framework's own numbering or an enterprise numbering, but *specific*). Each pre-commitment states the action (pause deployment, restrict tool set, require third-party evaluation before scale-up, etc.) and the trigger (capability-evidence threshold crossing, elicitation surfacing a hidden capability, a serious-incident report).
- **Escalation authority.** The internal body accountable for tier decisions and pre-commitment invocation. Placeholder role names (`head-of-ai-governance`, `chief-safety-officer`) are legitimate.
- **Re-evaluation cadence.** The commitment to re-evaluate the framework, the tier, and the pre-commitments — with the cadence, the responsible role, and the interlock into `mod-110`'s post-market surveillance loop.

### 5. `code-of-practice-discharge-mapping.md`

The final artefact ties the framework citation back to the Code-of-Practice discharge from exercise `01`.

For each safety-and-security-chapter commitment (per chapter `01` and exercise `01`'s `article-55-obligation-map.md`), state:

- **The commitment.** As paraphrased from the current Code of Practice.
- **The framework mechanism.** Which specific pre-commitment (PC-3.1, PC-3.2, etc.) from `enterprise-framework-citation.md` operationalises the commitment.
- **The evidence set.** The specific evidence-artefact classes that discharge the pre-commitment, cited from exercise `01`'s obligation map (foreshadow — exercise `04`'s safety-benchmark citation pack).
- **The signer.** Who signs the discharge for this commitment — the framework's governance body (from artefact 1), the release-owner, or a peer sign-off.

The mapping is the *bridge* between the industry-shape reading (this exercise) and the statute-shape reading (exercise `01`). An AI Office reviewer walks from a Code commitment → framework mechanism → evidence set in one hop.

## Starter guidance

- **Read the four frameworks in a fixed order.** Read RSP first (it is the most detailed on ladder shape), then Preparedness (for the per-category banding contrast), then FSF (for the periodic-re-evaluation and mitigation-effectiveness primitives), then Meta (for the outcome-tier contrast). Reading in this order lets each framework's contribution stand out against the ones you have already read.
- **Version-pin as you go.** Frameworks are revised. If you cannot pin the version cleanly, the reading is against a moving target and the comparative table cannot converge. Mark `<!-- needs-research: … -->` and move on rather than guessing.
- **The comparative read is not a ranking.** Do not conclude that one framework is "better" than another. The frameworks are calibrated to different publisher contexts (foundation-model producers with different portfolios and different risk appetites); a comparative read that ranks them mistakes the exercise for a benchmark.
- **Pre-commitment specificity is non-negotiable.** Chapter `02` is emphatic — "we follow RSP-shaped tiering" is not a citation. The enterprise-framework citation names PC-3.1, PC-3.2, etc., or equivalent specifics. Placeholder pre-commitment numbers are legitimate; hand-waving is not.
- **Read the Frontier Model Forum publications as *shared reference*, not statute.** They are what the industry publishes together. The state-of-the-art justification in the assurance case leans on them as the *shared* reference against which the enterprise's evaluation methodology is placed.
- **The enterprise adopts the shape, not the labels.** If you copy the RSP's ASL labels into the enterprise framework, the reviewer will see the copy. Use the enterprise's own tier labels; the shape is what carries the discharge, not the naming.
- **The FSF's two primitives (periodic re-evaluation, mitigation-effectiveness measurement) belong in the enterprise adaptation.** Chapter `02` calls them out explicitly; regardless of which framework you cite as the primary shape, adopt these two primitives. They are what turn the framework from a publication into a governance device.
- **`<!-- needs-research: … -->` is a legitimate answer.** The frameworks' version histories, the current governance-body naming, the current AISI-relationship claims, the current Frontier Model Forum publication list — all of these change on a cadence faster than a curriculum chapter can pin. Mark rather than guess.

## Acceptance criteria

You have succeeded if:

- `framework-version-pinning-brief.md` covers all four frameworks with URL, version, publication date, scope, governance body, and revision cadence. The shared-substrate note is present and grounded.
- `comparative-read-table.md` has one row per structural element (at least the ten enumerated above), with a cell per framework. The interpretation note names the two-to-three tightest agreements, the two-to-three sharpest divergences, and the highest-signal rows for an AI Office reviewer.
- `frontier-model-forum-reading-list.md` cites at least two current issue briefs with the reading purpose and the citation-in-assurance-case value for each.
- `enterprise-framework-citation.md` names the framework choice (with any hybridisation stated), the framework-version identifier, the capability-category set (with diff if modified), the tier landing for the release, the pre-commitments enumerated with specific numbering, the escalation authority, and the re-evaluation cadence.
- `code-of-practice-discharge-mapping.md` maps every safety-and-security-chapter Code commitment (from exercise `01`) to a specific pre-commitment from artefact 4 and to the evidence set that discharges it. The signer is named per commitment.
- No framework is ranked; the comparative read stays comparative.
- Every place a fact would need to be verified against a current published framework version, a current AISI-relationship claim, or a current Frontier Model Forum publication is marked `<!-- needs-research: … -->` rather than guessed.
- The FSF primitives (periodic re-evaluation, mitigation-effectiveness measurement) appear in `enterprise-framework-citation.md` regardless of which framework is cited as the primary shape.

## Stretch goals

- **Add a fifth-framework reading.** In `additional-framework-reading.md`, pick one additional publicly-published safety framework (Microsoft's Responsible AI Standard, an academic proposal, an industry-consortium output beyond the Frontier Model Forum) and read it against the same ten structural elements. Note where it converges with the four references and where it introduces novel structure. `<!-- needs-research: … -->` where the framework's current publication is unclear.
- **Author the framework-revision-tracking discipline.** In `framework-revision-tracking.md`, describe how the enterprise tracks the four (or five) source frameworks' revisions after adopting a shape — the review cadence, the responsible role, the decision routine when a source framework's revision surfaces a new primitive the enterprise's framework does not carry.
- **Draft the AI-Office-visible framework summary.** In `ai-office-framework-summary.md`, write the one-page summary of the enterprise's cited framework the assurance bundle carries — publication date, version, capability categories, tier taxonomy, escalation authority, pre-commitments at the release's tier, and the citation into the Code-of-Practice discharge mapping. This is what a reviewer at the AI Office reads first at the framework layer.
- **Cross-reference `mod-108`.** In `mod-108-alignment-note.md`, sketch how the framework citation in this exercise aligns with (or diverges from) the enterprise deployment-tier scheme from `mod-108`. The two are *not* the same artefact — `mod-108`'s scheme lands enterprise deployment products at tiers; this exercise's citation lands the *model* at a framework tier — but they interlock and the alignment note makes the interlock explicit.
- **Author the elicitation-based-evaluation stance.** In `elicitation-stance.md`, write the two-paragraph stance on elicitation-based evaluation for the release — how the enterprise commits to *look for* capabilities the model may be hiding, who is accountable for the elicitation, and how the elicitation evidence lands in the assurance bundle. Chapter `02` frames elicitation as one of the two shared primitives cutting across all four frameworks; the stance names how the enterprise operationalises it.
