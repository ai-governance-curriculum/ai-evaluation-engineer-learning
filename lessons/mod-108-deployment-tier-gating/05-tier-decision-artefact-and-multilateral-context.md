# The Tier-Decision Artefact and the Multilateral Context

## Motivation

Chapters `01`–`04` designed the pieces of the tier gate: the shape adopted from frontier labs, the capability-evidence side, the mitigation-obligation (cybersecurity attestation) side, and the reversal-side dispositions. This chapter closes the module by joining the pieces into a *single output* — the **tier-decision artefact** — and by setting the artefact in its multilateral context.

The artefact matters for two reasons. First, it is what the release-gate walker (`mod-103`) actually reads: without a single, versioned, digest-pinned artefact per candidate release, the tier gate's evaluation is a scavenger hunt across systems. Second, it is what the *outside world* eventually reads — auditors, notified bodies (`mod-109`), regulators, deployer counterparties, and, at the highest tiers, national safety institutes. The multilateral context — Bletchley, Seoul, Paris, the Frontier Model Forum — is why "the outside world" reads it in the *shape* they do, and why the enterprise's artefact benefits from mirroring the shape.

The methodology owner *composes* the artefact from the peer-produced evidence. They do not author the evidence; they do not sign for the peer specialists; they do not certify the mitigation effectiveness. They *join* the evidence into a defensible whole, name the disposition, sign for the methodology, and deliver the artefact into the release package (`mod-104`).

## The schema of the tier-decision artefact

The artefact has eight required sections. Each section has a specified content list; each section carries an owner and, where applicable, a signer.

### 1. System identity

Who and what is being tier-decided. Fields:

- **System name and version.** The release candidate identifier, resolvable back to a specific model version, prompt version, tool-set version, guardrail configuration, and infrastructure baseline.
- **Deployment identifier.** The product surface the tier decision applies to. Two products sharing a base model have distinct tier-decision artefacts (`04` — the "tier shopping" failure mode).
- **Assurance case reference.** Pointer into `mod-102`'s assurance case for this deployment.
- **Prior tier-decision reference (if any).** Pointer to the previous artefact this release supersedes.
- **Framework version references.** Which version of the internal tier scheme (`01`), which version of the threshold spec catalogue (`02`), which version of the cybersecurity attestation template (`03`), which version of the runbook (`04`, `mod-103` chapter `05`).

### 2. Deployment context

The permission envelope the tier admits and the surface the deployment lands on. Fields:

- **Tier landing.** The vector across the tier scheme's axes (`01`) — for example, `(data:Med, tools:High, reach:High, sector:none)`.
- **Population served.** Who is on the receiving end — internal users, authenticated external customers, unauthenticated external users, regulated end-users.
- **Tool set.** Named tools and their invocation modes (read-only, write, autonomous-chain).
- **Data access.** Which data sources the deployment may read or write, at what granularity, under what tenancy constraints.
- **Jurisdictions.** The jurisdictions in scope; the sector-rule map (`mod-107`) if applicable.
- **Contracted counterparties.** Any deployer whose contract commits the enterprise to specific tier configurations.

### 3. Capability-evidence set

The threshold specs (`02`) and their attached evidence. Fields, per spec:

- **Threshold-spec identifier.** From the threshold-spec catalogue.
- **Evidence artefact reference.** Pointer into the evidence pipeline (`mod-104`), with the artefact's cryptographic digest so the artefact is unambiguously referenced.
- **Measurement summary.** The point estimate, the confidence interval, the estimator, the pass / fail decision under the spec's decision rule.
- **Peer-track owner signature.** The `ai-eval-engineer` / `model-evaluation-engineer` / `ai-risk-engineer` role signature confirming the artefact.

### 4. Cybersecurity-attestation section

The four-framework attestation from chapter `03`. Sub-sections:

- **SAIF frame.** The enterprise-security programme context.
- **NCSC lifecycle attestation.** Per lifecycle stage (design / development / deployment / operation and maintenance), the guidelines addressed and the evidence pointers.
- **OWASP LLM Top 10 coverage table.** Per risk, the mitigation and evidence pointer.
- **MITRE ATLAS index for the adversarial-eval report.** The report's cross-reference to ATLAS techniques.

Each sub-section carries the `ai-infra-security` peer signature.

### 5. Kill-switch, rollback, downgrade, and do-not-deploy design

The reversal dispositions from `04`. Fields:

- **Kill-switch.** Named mechanism, authoriser, tested-cadence evidence, default-state under control-plane outage.
- **Rollback.** Named prior state to roll back to, RTO, tested-cadence evidence, authoriser per trigger class.
- **Downgrade.** Per axis in the tier scheme, the downgrade increment(s) and their triggers.
- **Do-not-deploy conditions.** The conditions that mandate this disposition and the escalation contract signer.

### 6. Decision, rationale, reviewers, and expiry

The methodology-owner half of the release-decision. Fields:

- **Disposition.** Promote at tier T; promote at tier T with deferred criterion X (expiry Y); do not promote; downgrade; do-not-deploy.
- **Rationale.** Prose citing the capability-evidence set, the cybersecurity attestation, and the residual-risk register.
- **Reviewers.** Named methodology owner, release-owner, peer-specialist signers (as required), head of AI governance (as required for tier-boundary crossings — `04`).
- **Expiry.** The wall-clock or milestone at which the tier decision must be re-evaluated. Capability-evidence expiry (`02`), post-market surveillance triggers (`mod-110`), and framework-version changes (any of `01`–`04`) are the typical expiry drivers.

### 7. Assurance-case join

Pointer into the assurance case (`mod-102`) where the tier decision lands. The artefact is *not* the assurance case — the assurance case is the argument, the artefact is one leaf-plus-summary of the argument's discharge at tier-decision time. The join names which claim in the case this artefact discharges and which evidence it aggregates.

### 8. Multilateral-context citation (optional but recommended)

The frameworks the artefact's shape mirrors and the industry publications the enterprise reads to keep the shape current. See the multilateral-context section below.

## How the artefact composes with the assurance case

The assurance case (`mod-102`) is the *argument* that the deployment discharges its obligations. The tier-decision artefact is a *concentrated* discharge of one particular claim in the case — the claim that the deployment sits at tier T with the required capability evidence and mitigation obligations.

In GSN terms, the tier-decision artefact is a solution node attached to a mid-level goal like "the release is safely promoted to tier T." In CAE terms (`mod-102` chapter `03`), the artefact is the evidence-incorporation leaf for an argument that decomposes the tier claim into capability, mitigation, and reversal sub-claims. The artefact's schema (above) is structured so a reviewer walking down the assurance case can hit the artefact and find every sub-claim's evidence in one hop.

The composition matters because it prevents *duplication* — the artefact should not restate what the assurance case already argues; it should *concentrate* the argument's leaves at the tier boundary. A tier-decision artefact that reads as a mini-assurance-case is a sign the wider assurance case is not doing its work.

## How the artefact slots into the release package

The release package (`mod-104`) is the bundle of artefacts the release-gate assembles for external consumption — technical documentation for the EU AI Act Article 11 obligation, notified-body dossier under Article 43 (`mod-109`), sector-regulated evidence sets (`mod-107`), external-audience cards (`mod-105`), and, for the tier gate specifically, this artefact.

The tier-decision artefact slots as one file in the package, versioned, digest-pinned, immutable once signed. The release-gate walker reads it as *the* tier decision — there is no second artefact that supersedes it. If the tier decision needs to be updated (a deferred criterion closes, a downgrade is enacted, an expiry is reached), a *new* artefact is authored referencing the previous one, and the previous one is marked superseded in the immutable pipeline. The prior artefact is *not* rewritten.

The immutability matters because the tier decision is a governance artefact. An audit two years after the release must be able to reconstruct exactly what evidence was in the artefact at the moment the disposition was signed. Mutability breaks reconstruction.

## The multilateral context

The enterprise programme does not sit in isolation. Since 2023, a series of intergovernmental and industry-body commitments has been building a shared vocabulary for frontier-AI safety, capability evaluation, and responsible deployment. The tier-decision artefact benefits from mirroring the shape these commitments call out.

### Bletchley Declaration (2023-11)

The [Bletchley Declaration](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration) was issued at the AI Safety Summit hosted at Bletchley Park in November 2023, and signed by 28 countries plus the EU. <!-- needs-research: verify current signatory count for the Bletchley Declaration and any subsequent additions. --> Its core substantive commitment is to a shared understanding of frontier-AI risk and to intensified international cooperation on frontier-AI safety research and evaluation.

For the enterprise programme, Bletchley is the *origin* declaration of the multilateral track. It does not impose obligations on the enterprise; it establishes the language and the mutual recognition among governments that shaped subsequent (and more concrete) commitments.

### Seoul Declaration and Ministerial Statement (2024-05)

The [Seoul Declaration for safe, innovative and inclusive AI](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) was issued at the second AI safety summit in May 2024. Two artefacts matter:

- The **Seoul Declaration** itself, a state-level commitment continuing the Bletchley process.
- The **Frontier AI Safety Commitments** signed by 16 frontier AI companies (Anthropic, Google, OpenAI, Meta, Microsoft, and others), committing to publish safety frameworks (i.e., commitments in the RSP / Preparedness / FSF shape from `01`), to define risk thresholds and mitigations, and, at extreme risk levels not adequately mitigated, not to develop or deploy the model at all. <!-- needs-research: verify the exact list of the 16 signatory companies of the Frontier AI Safety Commitments and any additions since. -->

For the enterprise programme, Seoul is the moment the frontier-lab shape became a *multilateral commitment* — the pattern of capability-threshold + mitigation + do-not-deploy is now a state-recognised shape, and the enterprise adopting it (`01`) is aligning with a recognised commitment structure.

### Paris AI Action Summit (2025-02)

The [Paris AI Action Summit](https://www.elysee.fr/en/sommet-pour-l-action-sur-l-ia) was held in February 2025, continuing the summit series with a broadened action-oriented agenda covering public interest AI, work and AI, innovation and culture, trust in AI, and global governance. <!-- needs-research: verify the exact URL for the Paris AI Action Summit and confirm its outcome documents (e.g., "Statement on Inclusive and Sustainable AI"); the signatory count and specific commitments diverged from the earlier summits. -->

For the enterprise programme, Paris expanded the vocabulary — beyond safety in the narrow frontier-risk sense — to include a wider set of AI governance concerns. The tier-decision artefact benefits from citing Paris where the enterprise's tier scheme addresses concerns Paris highlighted (labour impact, environmental impact, and public-interest AI concerns can shape the mitigation obligations at specific tiers).

### Frontier Model Forum

The [Frontier Model Forum](https://www.frontiermodelforum.org/) is the industry body co-founded in 2023-07 by Anthropic, Google, Microsoft, and OpenAI (with subsequent additions of further frontier developers). <!-- needs-research: verify current Frontier Model Forum membership beyond the four founding members; e.g., Amazon and Meta may have joined subsequently. -->

The Forum publishes cross-lab work on safety, security, evaluation methodology, and deployment practice. For the enterprise programme, the Forum is a *public library* — its publications on preparedness, on evaluation methodology, on early-warning systems, and on mitigation patterns are template patterns the enterprise reads and adapts. Citing the Forum's publications in the multilateral-context section of the tier-decision artefact grounds the enterprise's design choices in publicly-scrutinised patterns.

### Why the multilateral context matters for the artefact

Two reasons.

First, it *positions* the enterprise's tier-decision artefact in a recognised shape. An external reviewer opening the artefact sees a schema that mirrors the frontier-lab publications and the Seoul commitments, and can read it fluently. A completely bespoke shape would require the reviewer to first learn the vocabulary before evaluating the substance.

Second, it *anchors* the enterprise's justifications in a public commitment structure. When the artefact says "the tier scheme's do-not-deploy condition mirrors the shape of the Seoul Frontier AI Safety Commitments," the reviewer has a stable external referent for what "do-not-deploy" means. Without that anchor, the term is ambiguous.

The multilateral-context section of the artefact does not have to be long — a paragraph citing the applicable summits and the applicable Forum publications, with the URL and version, is enough.

## Worked example — the T-CS tier-decision artefact composition

Continuing the T-CS product from chapters `01`–`04`, the tier-decision artefact for the current release candidate composes as follows (representative excerpt).

**Section 1 — System identity.** System `T-CS-agent-v4.2`, release candidate `rc-2026-07-a3c1`, deployment identifier `product-cs-external`, assurance-case reference `case-cs-v3`, supersedes tier-decision artefact `td-cs-v4.1-2026-05`. Framework versions: tier-scheme v2.1, threshold-spec catalogue v3.0, cybersecurity-attestation template v1.5, runbook v2.7.

**Section 2 — Deployment context.** Tier landing `(data:Med, tools:High, reach:High, sector:none)`. Population: authenticated external customers, EU and US jurisdictions. Tool set: CRM read-write, ticketing read-write, knowledge-base read, no long-horizon autonomy beyond four sequential tool calls. Data access: per-tenant customer data. Counterparty: enterprise commercial customers under standard MSA; no notified-body involvement (product not in Annex III).

**Section 3 — Capability-evidence set.** Threshold specs `TIER-CE-SAFETY-01` (HarmBench, passing at CI upper 0.06), `TIER-CE-INJECT-01` (AgentDojo, passing at CI upper 0.04), `TIER-CE-CAP-01` (τ-bench, passing at CI lower 0.53), `TIER-CE-CAP-02` (GAIA Level-1, passing at CI lower 0.28). Each with digest-pinned artefact and signed by `ai-eval-engineer` and `ai-risk-engineer` peer roles.

**Section 4 — Cybersecurity attestation.** SAIF frame, NCSC per-stage attestation, OWASP LLM Top 10 coverage table with the LLM01 / LLM06 / LLM08 rows expanded (`03`), MITRE ATLAS index for the adversarial-eval report. All signed by `ai-infra-security`.

**Section 5 — Reversal design.** Kill-switch at the API-gateway layer, authoriser is on-call assurance engineer at T-CS-tier for cybersecurity triggers, escalates to head of AI governance for regulatory triggers; tested 2026-06-15. Rollback to `T-CS-agent-v4.1` in 15 minutes RTO, tested 2026-06-15. Downgrade paths named per axis. Do-not-deploy conditions include an escalation to head of AI governance for any confirmed cross-tenant leakage.

**Section 6 — Decision.** Disposition: promote at tier `(data:Med, tools:High, reach:High, sector:none)`. Rationale: cites section 3 evidence, section 4 attestation, and the residual-risk register position. Reviewers: methodology owner, T-CS release-owner, `ai-infra-security` peer lead, `ai-eval-engineer` peer lead, head of AI governance countersign (tier-boundary crossing from v4.1's `tools:Med`). Expiry: earlier of six months from decision, next quarterly re-gate, or any post-market surveillance trigger from `mod-110`.

**Section 7 — Assurance-case join.** Pointer into `case-cs-v3` claim `C-DEPLOY-TIER` and its supporting arguments.

**Section 8 — Multilateral context.** Cites the Seoul Frontier AI Safety Commitments shape as the model for section 5 do-not-deploy conditions; cites the current Frontier Model Forum publication on evaluation methodology as the reference for section 3 statistical framing.

The artefact is versioned, digest-pinned, signed, and lands in the immutable release package (`mod-104`).

## Where this shows up in the rest of the track

- `01`–`04` — every prior chapter of this module contributes a section to the artefact.
- `mod-102` — the assurance case is where the artefact hangs off; the join keeps the two coherent.
- `mod-103` — the release-gate walker consumes the artefact.
- `mod-104` — the immutable release package the artefact lives in.
- `mod-105` — the external-audience cards derive their tier-decision paragraphs from this artefact.
- `mod-106` — the cross-jurisdictional obligation map reads the artefact as evidence.
- `mod-107` — sector-regulated deployments add sector-specific sub-sections to the artefact.
- `mod-109` — third-party auditors and notified bodies read the artefact as part of their evidence.
- `mod-110` — post-market surveillance signals trigger re-authoring of the artefact when the expiry conditions fire.
- `mod-111` — for GPAI systemic-risk deployments, the artefact's capability-evidence and cybersecurity sections align to the EU AI Act Article 55 expectations.
- `mod-112` — the operating-model owns the artefact template and its versioning.

## Summary

- The tier-decision artefact is a single, versioned, digest-pinned, signed document per candidate release, composed of eight sections: system identity, deployment context, capability-evidence set, cybersecurity attestation, reversal design, decision (with reviewers and expiry), assurance-case join, multilateral context.
- The methodology owner *composes* the artefact from peer-produced evidence and signs for the methodology; peers sign for their evidence; head of AI governance countersigns for tier-boundary crossings.
- The artefact hangs off the assurance case as a concentrated discharge of the tier claim; it slots into the release package as an immutable file; updates are new artefacts referencing prior ones, never rewrites.
- The multilateral context — Bletchley Declaration (2023-11), Seoul Declaration and Frontier AI Safety Commitments (2024-05), Paris AI Action Summit (2025-02), Frontier Model Forum publications — positions the artefact in a recognised shape and anchors its justifications in public commitment structures.
- The tier-decision artefact is the tier gate's output; every prior chapter of this module contributes a section to it.
- Exercise 05 has you compose a full tier-decision artefact for a worked deployment, walking each of the eight sections.
