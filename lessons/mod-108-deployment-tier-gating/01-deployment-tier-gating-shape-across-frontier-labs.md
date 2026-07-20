# Deployment-Tier Gating: the Shape Across Frontier Labs

## Motivation

The release-gate architecture in `mod-103` gave the general shape of surface-specific gate variants (T0 pilot → T4 regulated on-prem). That taxonomy is *coarse* — it slices by deployment surface, not by the *capabilities of the model being deployed*. For an enterprise deploying a general-purpose model, or a fine-tuned derivative of one, that coarseness is a problem: two systems on the same surface can carry very different capability profiles, and the release-gate has to reason about the *capability envelope* separately from the *deployment surface*.

Frontier labs — Anthropic, OpenAI, Google DeepMind — hit this problem earlier than most enterprise deployers, because they are the ones producing the frontier capabilities in the first place. Their response was a specific pattern: a *tier* is a bounded set of deployment permissions coupled to *capability evidence* and *mitigation obligations*. Cross a capability threshold, and the deployment permissions have to change (or the deployment has to stop) unless the mitigation obligations at the higher tier are demonstrably met.

The release-assurance methodology owner adapts *the shape* of this pattern into the enterprise release-gate. The enterprise is not a frontier lab — it does not train frontier models, it does not sit at the capability frontier itself — but it *does* deploy those models, and it *does* carry the deployment-side responsibility for the consequences of doing so at scale. The frontier-lab shape gives the enterprise a defensible pattern for that responsibility.

This chapter walks the three reference frameworks — Anthropic Responsible Scaling Policy (RSP), OpenAI Preparedness Framework, Google DeepMind Frontier Safety Framework (FSF) — as the source pattern, and closes with the reason the enterprise adopts *the shape* rather than the labels.

## What a tier is

A **tier** in this pattern is a tuple of three things:

- **A bounded set of deployment permissions.** Which populations may the system serve? Which tool set may it invoke? Which data may it access? Which product surfaces may it reach? Which jurisdictions may it be offered in? A tier is a permission envelope.
- **A capability-evidence set.** What must be true, evidentially, about the model's capabilities for the deployment to sit in this tier? The evidence is produced by peer specialists (`ai-eval-engineer`, `model-evaluation-engineer`, `ai-risk-engineer`); the tier gate *consumes* it.
- **A set of mitigation obligations.** Given the capability evidence, what mitigations must be in place at the deployment surface for the tier to be permissible? Guardrails, red-team results, monitoring detectors, human-oversight design, cybersecurity attestations (`03`), kill-switch design (`04`).

A tier gate fires when a candidate release either enters the tier for the first time, or when new capability evidence arrives that suggests the current tier is no longer supported by the evidence (`04`).

## Why the frontier labs adopted the shape

Two forces drove the shape.

First, **irreducible uncertainty about frontier capabilities**. At the frontier, a model's capability profile is not fully known at training time. It has to be *elicited* through evaluations, red-teaming, and observed use. The gate cannot assume a stable capability envelope; it has to be structured around *the point at which the envelope is re-evaluated*. A tier is that point.

Second, **the cost of an over-permissive deployment**. If a model with capabilities exceeding the mitigations in place is deployed to a broad population, the downside is severe (biosecurity uplift, cyber-offensive uplift, autonomous-replication uplift, or, more mundanely, misuse at scale). A tier gate is the pre-commitment device that keeps deployment permissions bounded to the mitigations demonstrably in place.

The pattern is not unique to frontier labs. It shows up wherever irreducible uncertainty about a capability envelope meets a broad deployment surface — pharmaceutical Phase-I / Phase-II / Phase-III trials, aviation type-certification tiers, nuclear-plant operating envelopes. What is *new* in the AI setting is the pace of capability change and the fact that the capability envelope can shift with a fine-tune, a system-prompt change, or a tool-set addition.

## Anthropic Responsible Scaling Policy — AI Safety Levels

The Anthropic Responsible Scaling Policy (RSP) was first published in 2023-09, and has been updated since. <!-- needs-research: verify the current RSP version and its exact ASL bandings, e.g., the 2024-10 update introduced changed ASL-3 deployment/security standards; confirm current published version. --> The RSP is structured around **AI Safety Levels** (ASL), an escalating series roughly analogous to BSL (BioSafety Level) in laboratory biosecurity:

- **ASL-1** — models that manifestly do not pose meaningful catastrophic risk (small models, non-frontier baselines).
- **ASL-2** — models that show early signs of dangerous capabilities but where the current mitigations are considered adequate (the current frontier at the time of the original policy).
- **ASL-3** — models with substantially higher risk of catastrophic misuse, requiring hardened deployment and security standards (misuse-hardening on the deployment side; weight-security on the training / storage side).
- **ASL-4** (and above) — models whose capabilities require standards not yet fully specified at the time of writing; the policy commits to specifying them before an ASL-4 model is trained.

The RSP couples each ASL to (a) **capability thresholds** that trigger transition to the next level, described in terms of measurable capability categories (biosecurity uplift, cyber-offensive uplift, autonomous-replication, and more), (b) **deployment standards** (misuse-hardening obligations, red-team obligations, monitoring), and (c) **security standards** (weight-storage, access control, insider risk). <!-- needs-research: confirm current published capability threshold categories and whether "autonomous-replication" remains a distinct category in the latest version. -->

The RSP is a *pre-commitment device*. Anthropic commits to *not deploy* or *not train* at a higher ASL without the corresponding standards in place. That commitment is publishable, revisable on a published cadence, and reviewable.

**Adaptation-to-enterprise implication.** The enterprise release-gate does not sit at the frontier, and does not deploy across ASLs in the RSP sense. But the *shape* — capability threshold → deployment standard → security standard, pre-committed and publishable — is directly the shape of the enterprise tier gate. The enterprise substitutes its own capability categories (data-access blast-radius, tool-invocation autonomy, decision-authority level over enterprise workflows) and its own deployment / security standards.

## OpenAI Preparedness Framework — tracked-risk-category thresholds

The OpenAI Preparedness Framework was first published in 2023-12, with subsequent revisions in 2025. <!-- needs-research: verify the current Preparedness Framework version (e.g., "Preparedness Framework 2.0" or later), publication date, and current tracked risk categories — the original set was Cybersecurity, CBRN, Persuasion, Model Autonomy; some later revisions restructured this set. -->

The Preparedness Framework is structured around a bounded set of **tracked risk categories** — the original set was Cybersecurity, CBRN, Persuasion, and Model Autonomy — and, per category, a set of **capability-level thresholds** (originally Low / Medium / High / Critical) with associated deployment- and development-side obligations:

- **Low** — no meaningful uplift for the risk in the category; standard practice applies.
- **Medium** — non-trivial uplift; standard mitigations apply.
- **High** — substantial uplift; hardened mitigations required; some deployments not permitted without additional review.
- **Critical** — the deployment or continued development of the model without further safety work would be unacceptable; specific commitments (e.g., not-deploy, not-train-further) apply.

The framework commits OpenAI's Safety Advisory Group (and, in later revisions, additional review bodies) to reviewing the evidence for the tier a candidate model sits in, with a documented decision process. <!-- needs-research: verify the current review body naming (Safety Advisory Group, Safety and Security Committee, Preparedness team) as of the current published framework. -->

**Adaptation-to-enterprise implication.** The Preparedness Framework's contribution to the enterprise pattern is the **tracked-risk-category** structure: rather than a single tier ladder, use a small set of *orthogonal* risk axes and land a candidate in a level per axis. For an enterprise deployment, the axes might be *data-access blast-radius*, *autonomous-action authority*, *external-user reach*, *regulated-sector exposure* — each with its own Low / Medium / High / Critical banding and its own mitigation obligations. A single candidate may be Low on three axes and High on one; the tier gate reasons about the vector.

## Google DeepMind Frontier Safety Framework — Critical Capability Levels

The Google DeepMind Frontier Safety Framework (FSF) was first published in 2024-05, with subsequent updates. <!-- needs-research: verify current FSF version and the specific CCL categories in the latest published revision (initial version included Autonomy, Biosecurity, Cybersecurity, and Machine-Learning R&D categories). -->

The FSF is structured around **Critical Capability Levels** (CCLs) — specific capability thresholds, per risk domain, whose crossing triggers additional evaluation, deployment mitigation, and security mitigation. The FSF names its capability domains explicitly and, per domain, describes the CCL at which mitigation obligations escalate.

The FSF also introduces two useful primitives the other frameworks handle less explicitly:

- **Early-warning evaluations.** The FSF commits to *periodic* re-evaluation of models against the CCLs (rather than only at training-time or release-time), so a capability that emerges post-deployment can trigger the framework.
- **Mitigation-effectiveness evaluation.** A mitigation is not credited unless it has been *evaluated* for effectiveness — a guardrail with an unmeasured block rate does not discharge the mitigation obligation.

**Adaptation-to-enterprise implication.** The FSF's contribution to the enterprise pattern is the pair of primitives: periodic re-evaluation (the enterprise tier gate does not evaluate once at release; it re-evaluates on a cadence, when new evidence arrives, and on triggering events — `mod-110`) and mitigation-effectiveness measurement (the enterprise tier gate does not credit a mitigation without evidence that it works — `03`).

## Comparing the three shapes

| Framework | Structure | Escalation trigger | Mitigation coupling |
| --- | --- | --- | --- |
| Anthropic RSP | Single ladder (ASL-1..ASL-4+) | Capability threshold on a fixed set of dangerous-capability categories | Deployment standard + security standard per ASL |
| OpenAI Preparedness | Vector of categories × levels (Low / Med / High / Critical) | Per-category threshold | Per-category mitigation + deployment / development commitment |
| Google DeepMind FSF | Vector of domains × Critical Capability Levels | Per-domain CCL crossing | Mitigation coupled + effectiveness evaluation required |

The three shapes are variants on the same underlying pattern: capability evidence → tier / level → mitigation obligation. RSP presents it as a single ladder; Preparedness and FSF present it as a vector across axes. All three commit publicly to the pattern being followed and to review of the evidence.

Two differences matter for enterprise adaptation.

- **Single ladder vs. vector.** The RSP's single ladder is easy to communicate but forces the highest-risk axis to dominate the overall tier — a model with a moderate cyber uplift and a low bio uplift sits at whichever ASL the cyber uplift triggers. The Preparedness / FSF vector preserves the per-axis reading and lets the mitigation obligations be per-axis-specific. For an enterprise programme whose risk axes (`01`) are heterogeneous — data blast-radius is unrelated to sector exposure, and both are unrelated to tool autonomy — the vector shape is usually the more honest fit.
- **Mitigation-effectiveness measurement.** The FSF's explicit "mitigations are not credited without effectiveness measurement" is the sharpest version of a principle the other frameworks imply. The enterprise programme adopting the shape should adopt this principle explicitly; without it, the tier gate becomes a paper exercise (`03`).

The **Frontier Model Forum** is the industry body that publishes cross-lab work on safety, security, and evaluation methodology — the enterprise programme reads its publications as a public library of pattern templates. <!-- needs-research: verify current Frontier Model Forum membership beyond the founding members (Anthropic, Google, Microsoft, OpenAI) and any recent additions. -->

## Why the enterprise adopts the shape, not the labels

The frontier labs' labels — ASL-3, "High" on CBRN, CCL-N on Autonomy — are calibrated to *model-producing* organisations sitting at the capability frontier. An enterprise deploying a foundation-model API, or a fine-tuned derivative, is *downstream* of that frontier. It does not train the frontier capabilities; it *consumes* them under a provider's terms of service, and it carries the deployment-side consequences of how it uses them.

Two implications follow.

**First, the enterprise inherits the provider's tier assessment as a floor, not as a ceiling.** If the provider deploys the model at ASL-2 with a specific deployment standard, the enterprise cannot deploy at a *lower* mitigation level than the provider requires. But the enterprise's own deployment context — its user population, its tool set, its data access — may impose *higher* mitigation obligations than the provider's baseline. The enterprise tier gate has to reason about the enterprise-specific delta.

**Second, the enterprise's capability categories are enterprise-specific.** "Cyber-offensive uplift on the open internet" is a frontier-lab category; "cross-tenant data exfiltration via tool-use in the enterprise's customer-support workflow" is the enterprise adaptation. The enterprise tier gate uses the frontier-lab category structure as inspiration and substitutes categories that match its own risk surface.

The shape is what transfers. The labels are indicative.

## Worked shape — a bounded enterprise tier scheme

Consider a professional-services firm deploying a general-purpose foundation-model API under two products: an *internal-facing coding-assistant deployment* (T-CA) and a *customer-support agent with tool-use* (T-CS). The enterprise tier scheme, adapted from the frontier-lab shape:

**Axes** (Preparedness-style):

- **Data-access blast-radius.** From `read-only-public-docs` up to `read-write-across-tenants`.
- **Tool-invocation autonomy.** From `no-tools` up to `long-horizon-autonomous-tool-chains`.
- **External-user reach.** From `internal-only` up to `unauthenticated-external-users`.
- **Regulated-sector exposure.** From `none` up to `regulated-decision-support` (e.g., financial advice, medical triage).

**Bandings per axis:** `Low / Med / High / Critical`, adapted from Preparedness. Each banding names concrete deployment permissions (what the tier admits) and mitigation obligations (what must be true at the deployment surface to sit there).

**Capability evidence** (`02`) at the transition point per axis: safety-benchmark results, agent-benchmark results, red-team results, adversarial-eval results — all consumed from peer specialists.

**Mitigation obligations** (`03`) per tier: guardrail set, monitoring detectors, human-oversight design, cybersecurity attestations, kill-switch and rollback design (`04`).

**Tier landing:**

- T-CA lands as `(data:Low, tools:Med, reach:Low, sector:none)` — internal users, IDE-scoped tools, internal repositories. Its tier gate requires safety and coding-benchmark evidence, a modest guardrail set, and internal-facing monitoring.
- T-CS lands as `(data:Med, tools:High, reach:High, sector:none)` — customer data access, tool-chain including CRM and ticketing writes, unauthenticated external users. Its tier gate requires a broader safety-benchmark set, agent-benchmark evidence, red-team results specifically on prompt-injection into tool calls, a stricter guardrail set, and a tested kill-switch.

The two products *share* the enterprise tier scheme; each *lands* at a specific vector; each pulls the mitigation set the vector implies.

## Where this shows up in the rest of the track

- `02` — the capability-evidence side of the tier gate: which peer-produced benchmarks discharge which thresholds.
- `03` — the mitigation-obligation side: cybersecurity attestation clauses that stack onto the tier gate.
- `04` — the reversal side: kill-switch, rollback, downgrade, and do-not-deploy pathways.
- `05` — the artefact side: how a single tier-decision artefact composes and how it slots into the wider release package.
- `mod-102` — the assurance case cites the tier as a top-level context node and its axes as sub-claims.
- `mod-103` — the surface-specific gate variants (T0..T4) and the capability-specific tier vector combine in the gate walker.
- `mod-104` — the evidence pipeline pins the capability-evidence artefacts by digest so the tier gate is auditable.
- `mod-110` — post-market surveillance is the periodic re-evaluation channel the FSF pattern requires.
- `mod-111` — for GPAI systemic-risk deployments, the tier gate composes with the EU AI Act Article 55 obligation set.

## Summary

- A tier is a bounded set of deployment permissions coupled to capability evidence and mitigation obligations. Cross a threshold, and either the permissions change or the mitigations escalate.
- Frontier labs adopted the shape to handle irreducible uncertainty about frontier capabilities and the cost of over-permissive deployment.
- Anthropic RSP: single ladder (ASL-1..ASL-4+), capability threshold → deployment standard + security standard.
- OpenAI Preparedness: vector of tracked risk categories × Low/Med/High/Critical, per-category mitigation and deployment / development commitments.
- Google DeepMind FSF: vector of domains × Critical Capability Levels, with periodic re-evaluation and mitigation-effectiveness measurement made explicit.
- The Frontier Model Forum publishes cross-lab work the enterprise programme reads as a public library.
- The enterprise adopts *the shape* (capability evidence → tier → mitigation obligation, pre-committed and publishable) not the labels. The provider's tier is a floor; the enterprise's deployment context may impose a stricter tier.
- Exercise 01 has you author an enterprise tier scheme in the RSP shape, adapted to a two-product enterprise deployment.
