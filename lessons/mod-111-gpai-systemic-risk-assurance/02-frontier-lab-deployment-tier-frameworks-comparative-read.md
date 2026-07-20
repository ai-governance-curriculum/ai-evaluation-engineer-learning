# Frontier-Lab Deployment-Tier Frameworks — a Comparative Read

## Motivation

`mod-108` walked the *enterprise adaptation* of deployment-tier gating — the shape an enterprise release-gate takes when it deploys a foundation model or its derivative at scale. That module's first chapter opened three of the reference frontier-lab frameworks (Anthropic Responsible Scaling Policy, OpenAI Preparedness Framework, Google DeepMind Frontier Safety Framework) as the source pattern.

This chapter reads the *same* frameworks with a different lens: as the industry-shape template that a GPAI-systemic-risk provider's Article 55 discharge (chapter `01`) most often overlays with. A signatory of the EU GPAI Code of Practice usually cites its own frontier framework as the mechanism through which the Code's safety-and-security commitments are met. A release-assurance methodology owner therefore has to be able to read these frameworks *comparatively* — where they agree on shape, where they diverge on operationalisation, and where the differences change what an Article 55 assurance case can honestly claim.

The reading is deliberately shallow on capability specifics (those move too fast to bake into a curriculum chapter) and deep on structural shape (which is stable across versions). The concrete versions and thresholds are marked with `<!-- needs-research: ... -->` so the reader confirms against the current published texts.

## The shape every framework carries

Before diving into the individual frameworks, note the four-part structure they all carry, in one form or another:

1. **Capability evidence.** What must be true, evidentially, about the model's capabilities in a given risk domain, at a given point in the model's life cycle?
2. **Tier / level decision.** Given the capability evidence, which deployment (and sometimes development) tier is the model in?
3. **Mitigation obligations.** Given the tier, what deployment-side and security-side mitigations must be in place?
4. **Escalation and pre-commitment.** If the capability evidence at re-evaluation supports a higher tier but the mitigations for that tier are not in place, what does the provider commit to do (pause deployment, pause training, restrict scope, invoke additional review)?

The four parts are the *shape*. Individual frameworks differ on which capability categories they name, how they quantise thresholds, who signs off on tier decisions, and how the escalation commitment is worded.

## Anthropic Responsible Scaling Policy

**Structure.** The [Anthropic Responsible Scaling Policy (RSP)](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) is structured around **AI Safety Levels (ASL)**, an escalating series (ASL-1, ASL-2, ASL-3, ASL-4+) with each level coupling capability evidence to two matched standards — a **deployment standard** (misuse-hardening for released models) and a **security standard** (weight storage, access control, insider risk on model artefacts). Crossing a capability threshold triggers transition to a higher ASL, and the RSP commits Anthropic to *not deploy* or *not further train* at the higher ASL without the corresponding standards in place — a *pause-and-strengthen* commitment.

<!-- needs-research: verify the current published RSP version (the policy has been revised multiple times since its 2023-09 first publication, e.g., a substantive revision in 2024-10); confirm the current set of dangerous-capability categories the RSP tracks, and whether the ASL-4 standard has been specified since. -->

**Capability categories.** The original RSP named biosecurity, cyber-offensive, and autonomous-replication uplift among the dangerous-capability categories driving level transitions; later revisions have refined the category set and, in some cases, split or renamed axes. Each category has a set of *evaluation-based indicators* — capability elicitations whose success (or the model's near-success) marks a threshold crossing.

**Evaluator independence.** The RSP describes third-party evaluator involvement in capability evaluation, and Anthropic has published information on relationships with the UK AISI and US AISI. The specific independence claims (which evaluations are third-party, which are internal, what pre-deployment access is granted) evolve with the framework version.

**Governance.** A named internal body (the Responsible Scaling Officer function, plus a board-level committee) is accountable for tier decisions and for the pause commitment. The framework carries a *policy revision procedure* — a documented process for how the RSP itself is updated.

## OpenAI Preparedness Framework

**Structure.** The [OpenAI Preparedness Framework](https://openai.com/safety/preparedness/) is structured around a bounded set of **tracked risk categories** and, per category, a set of **capability-level thresholds** with associated obligations. The original 2023-12 framework named four tracked categories — Cybersecurity, CBRN, Persuasion, and Model Autonomy — with a Low / Medium / High / Critical banding per category. Later published revisions have restructured this set.

<!-- needs-research: verify the current published Preparedness Framework version, its publication date, and its current set of tracked risk categories and thresholds — the framework has been substantively revised at least once since the 2023-12 first version (some public reporting names a "Preparedness Framework 2.0" but the exact naming and content should be reconfirmed from openai.com/safety/preparedness). -->

**Capability categories.** The tracked-category structure is the framework's most distinctive design choice: rather than a single ladder, a candidate model is landed in a *level per category*, producing a vector. A model may be Medium on three categories and High on one; the deployment and development obligations at the vector's high-water-mark drive decisions.

**Evaluator independence.** OpenAI has similarly published information on evaluator relationships with the US AISI and UK AISI. The Preparedness Framework describes internal evaluation by the Preparedness team, with escalation to an internal review body.

**Governance.** A named internal body is accountable for reviewing evidence, approving tier landings, and endorsing deployment / training decisions at higher tiers. In earlier versions this was the Safety Advisory Group; later revisions reference additional bodies including the Safety and Security Committee. <!-- needs-research: verify the current review body naming as of the current published version. -->

## Google DeepMind Frontier Safety Framework

**Structure.** The [Google DeepMind Frontier Safety Framework (FSF)](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) is structured around **Critical Capability Levels (CCLs)** — specific capability thresholds, per risk domain, whose crossing triggers additional evaluation, deployment mitigation, and security mitigation. The FSF distinguishes between *deployment mitigations* (applied to model use in production) and *security mitigations* (applied to model weights and infrastructure).

<!-- needs-research: verify the current published FSF version and its exact CCL categories in the latest published revision; the initial 2024-05 version named autonomy, biosecurity, cybersecurity, and machine-learning R&D domains. -->

**Capability categories.** The FSF names its capability domains explicitly and, per domain, describes the CCL at which mitigation obligations escalate. The domain set is smaller and more explicit than either the RSP's or the Preparedness Framework's, with less category ambiguity but also less flexibility for capabilities that fall outside the named domains.

**Distinctive primitives.** The FSF adds two primitives that the other two frameworks either handle implicitly or only recently:

- **Early-warning evaluations.** The FSF commits to *periodic* re-evaluation of models against the CCLs — capability evaluation is not a one-time event at training or release, but a cadence.
- **Mitigation-effectiveness evaluation.** A mitigation is not credited unless it has been *evaluated* for effectiveness. A guardrail with an unmeasured block rate does not discharge the mitigation obligation.

**Governance.** DeepMind names an internal review structure for CCL landings and for the deployment / security mitigation decisions.

## Meta Frontier AI Framework

<!-- needs-research: Meta published a Frontier AI Framework in early 2025; verify the current version, its capability threshold structure (public reporting describes "high risk" and "critical risk" tiers with unique-and-material-uplift criteria), and whether Meta continues to publish updates. Cite the framework from Meta's public safety pages once the URL is confirmed. -->

**Structure (as reported).** The Meta Frontier AI Framework carries a *risk-outcome* framing — rather than levelling on abstract capabilities, it levels on the *uplift* the model provides toward specified severe outcomes (mass-casualty CBRN attack, mass-scale cyber attack), with a *high-risk* tier and a *critical-risk* tier. Deployment restrictions at the critical-risk tier are strong (limiting or ceasing deployment); the framework's stated approach places heavy weight on the *unique-and-material* nature of the uplift the model would provide beyond baseline attacker capability.

**Comparative note.** Meta's framing is a useful counterpoint because it *inverts* the capability-first ordering: the primary object is the harmful outcome, and the capability evidence is landed against uplift toward that outcome. The RSP, Preparedness Framework, and FSF all lead with capability categories and derive harm implications; Meta leads with harm outcomes and derives capability implications. Both orderings show up in enterprise adaptations.

## The Frontier Model Forum

The [Frontier Model Forum](https://www.frontiermodelforum.org/) is an industry body founded by Anthropic, Google, Microsoft, and OpenAI (with subsequent additions), focused on the safe and responsible development of frontier AI models. It publishes:

- **Issue briefs** on specific frontier-safety questions (evaluation methodology, model-weight security, third-party evaluator interfaces, and more).
- **Working-group outputs** on shared technical and governance topics.
- **Convening and coordination** across signatories and with external bodies (including AISIs and the AI Office).

**Release-assurance implication.** The Forum's publications are a *public library* the enterprise programme reads for shared vocabulary and reference approaches. They are not statutory; they are not the enterprise's own framework; they are the industry's public reasoning surface. A GPAI-systemic-risk assurance bundle that cites a Forum issue brief for a specific evaluation-methodology choice is anchoring that choice against a shared industry reference, which strengthens the state-of-the-art justification (chapter `01`, Article 55(1)(a)).

## Two shared primitives worth naming explicitly

Two primitives cut across all four frameworks and deserve to be named on their own before the comparative read.

### Pre-commitment as a governance device

None of the four frameworks derives its authority from a specific evaluation methodology or a specific capability threshold. Each derives its authority from the *pre-commitment* — the publisher commits, in advance, to specific actions (pause deployment, pause training, restrict scope) if capability evidence outruns mitigation. The pre-commitment is publishable, revisable on a stated cadence, and reviewable by external parties. This is the same governance shape as pharmaceutical Phase-I/II/III trial commitments, aviation type-certification tiers, or nuclear operating envelopes: pre-committed behaviour under specified evidence is what makes the framework a governance device rather than an aspirational statement.

**Release-assurance implication.** A citation into a frontier framework in the assurance case must resolve to a *specific pre-commitment*, not to the framework's general shape. "We follow RSP-shaped tiering" is not a citation; "we follow FSL-3 pre-commitments PC-3.1 through PC-3.5 per version 2.1 of our internal framework, published 2026-04-17" is.

### Elicitation-based evaluation

All four frameworks assume that frontier capability is not fully knowable at training time and must be *elicited* through structured evaluation, capability probes, and red-teaming that actively try to surface capabilities the model has but has not been asked to demonstrate. This is a stronger assumption than "we ran benchmarks and the scores were within limits" — it requires an evaluator with the mandate and skill to *look for* capabilities the model may be hiding (through refusal training, through under-elicitation, through misalignment of the eval prompt to the underlying capability). Chapter `03` connects this back to the AISI-shape TEVV envelope, which is the third-party institutional embodiment of the same primitive.

## Reading the frameworks comparatively

The reason the release-assurance methodology owner reads all four frameworks is to build a *comparison table* the assurance bundle can cite. The table has three columns.

### Where they agree — the shape

All four frameworks agree on the four-part shape at the top of this chapter: capability evidence → tier / level decision → mitigation obligations → escalation and pre-commitment. All four commit to some form of pause-and-strengthen when the capability evidence outruns the mitigations at the current level. All four describe an internal governance body accountable for tier decisions. All four publish enough to be publicly readable.

This agreement is what makes it defensible for a release-assurance programme to cite *any* of the four as the mechanism through which the Code of Practice safety-and-security commitments are met. The shape is the industry consensus; the specific labels are the individual providers' choices.

### Where they diverge — the specifics

- **Capability categories.** RSP tracks dangerous-capability categories that have evolved over versions (biosecurity, cyber-offensive, autonomous-replication have all appeared, with refinements). Preparedness originally named Cybersecurity, CBRN, Persuasion, and Model Autonomy; the current version's set should be reconfirmed. FSF names autonomy, biosecurity, cybersecurity, and ML R&D. Meta leads with mass-casualty CBRN and mass-scale cyber. The overlap is substantial (biosecurity / CBRN, cyber-offensive, autonomy / model-autonomy) but the boundaries and definitions differ.
- **Threshold operationalisation.** RSP uses an ASL ladder with named standards per level. Preparedness uses a Low/Medium/High/Critical banding per category (a per-category ladder). FSF uses per-domain CCLs. Meta uses high-risk and critical-risk outcome tiers. The four thresholds are not directly translatable; a "High" on Preparedness's Model Autonomy is not obviously the same as an ASL-3 capability trigger on RSP or a CCL crossing on FSF.
- **Evaluator-independence claims.** All four describe some form of external evaluation, but the *proportion* of evaluation that is third-party, the *timing* of third-party access (pre-deployment, at-deployment, post-deployment), and the *scope* of what third parties can independently reproduce differ across frameworks and versions. `mod-109` chapter `01` walks the AISI-shape evaluator interface as the emerging convergence point.
- **Escalation counterparties.** RSP names Anthropic-internal bodies and, publicly, the Responsible Scaling Officer function. Preparedness names OpenAI-internal review bodies. FSF names DeepMind-internal structures. Meta names Meta-internal structures. None of the four defers escalation authority to an external body by default — though all four describe cooperation with AISIs and, for EU-scope models, with the AI Office.

### Where the enterprise adapts — the assurance-bundle citation

An enterprise release-assurance programme running for a GPAI-systemic-risk provider (or for a downstream deployer of one) typically does not invent a fifth framework. It picks a shape (usually one of the four, plus its own adaptations for the enterprise context — `mod-108`) and cites the source in the assurance bundle. The bundle's frontier-framework citation carries:

- The specific framework version referenced.
- The specific capability categories the enterprise adopts (which may be the source framework's set unchanged, or a modified set with a diff explained).
- The specific mitigation obligations at each tier, and how they map to the enterprise's release-gate criteria (`mod-103`).
- The escalation commitment — what the enterprise commits to do when the capability evidence outruns the mitigations, and who has authority to invoke the commitment.
- The re-evaluation cadence — how often the framework's evidence is refreshed (`mod-110`).

## Worked example — a signatory citing its own RSP-shape framework

Suppose a GPAI provider has published an RSP-shape framework with four levels (their internal naming: FSL-1 through FSL-4, "Frontier Safety Levels") and has signed the EU GPAI Code of Practice. Concretely, the safety-and-security-chapter discharge cites its own framework as follows:

- **Commitment: "State-of-the-art model evaluation including adversarial testing."** Discharged by FSL evaluation reports for the current release, produced against the framework's capability categories, plus a red-team report from an internal team and a third-party evaluator engagement (`mod-109`).
- **Commitment: "Systemic-risk assessment at Union level."** Discharged by an FSL-level assessment supplemented with a Union-level risk report structured against NIST AI 600-1 (chapter `03`).
- **Commitment: "Serious-incident tracking and reporting."** Discharged by the framework's internal incident procedure extended with an AI Office notification interlock.
- **Commitment: "Adequate cybersecurity of the model and infrastructure."** Discharged by the framework's security-standard evidence at the current FSL, with the `ai-infra-security` peer's attestation.

The assurance bundle carries all of this as citations into the frontier-framework artefact set, plus the framework document itself as a signed reference. A reviewer at the AI Office who receives the bundle can walk from Code-of-Practice commitment to framework citation to specific evidence artefact in one hop.

## Where this shows up in the rest of the track

- `mod-108` (deployment-tier gating) — chapter `01` opens the enterprise adaptation of these frameworks; this chapter reads them as the GPAI-Article-55 discharge shape.
- `mod-109` (third-party evaluator interface) — AISI-shape evaluators show up as the shared external counterparty across all four frameworks.
- `mod-110` (post-market surveillance) — the re-evaluation cadence a framework commits to becomes a post-market surveillance schedule.
- Chapter `01` of this module — Article 55 obligations and Code of Practice signatory citations rest on the framework citation.
- Chapter `04` of this module — the benchmark suites named as capability-evidence sources across the frameworks.

## Summary

- All four reference frameworks — Anthropic RSP, OpenAI Preparedness Framework, Google DeepMind FSF, Meta Frontier AI Framework — share a four-part shape: capability evidence, tier decision, mitigation obligations, escalation and pre-commitment.
- They diverge on capability-category naming, threshold operationalisation, evaluator-independence claims, and escalation-body naming; none of the four sets translates directly into another.
- The Frontier Model Forum publishes issue briefs and working-group outputs that constitute a shared industry reference surface.
- A GPAI-systemic-risk assurance bundle typically cites one of these four frameworks (or an enterprise-adapted variant) as the mechanism through which the EU GPAI Code of Practice safety-and-security commitments are met.
- Reading the frameworks *comparatively* — same shape, different specifics — is what the release-assurance methodology owner does to place their own citation defensibly.
- Exercise 02 has you build the comparative-read table for the current published versions of the four frameworks, per capability category and per threshold operationalisation, with the diff to a hypothetical enterprise adaptation.
