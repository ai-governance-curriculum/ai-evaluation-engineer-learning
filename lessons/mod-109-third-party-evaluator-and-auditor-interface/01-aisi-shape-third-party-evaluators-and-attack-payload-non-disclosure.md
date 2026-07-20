# AISI-Shape Third-Party Evaluators and Attack-Payload Non-Disclosure

## Motivation

The AI Safety Institute shape — sovereign or quasi-sovereign technical evaluator, deep methodology bench, credentialed access to the deployed system, published high-level findings with low-level detail withheld — is a new addition to the release-assurance interface surface. Five years ago no release-assurance programme had to plan for it. Today, for any provider or deployer at the frontier or adjacent tier, the AISI handoff is a first-class artefact the programme must be able to produce on demand.

The interface is difficult in a very specific way. Unlike a notified body under the EU AI Act (chapter `02`) — which reviews *documented evidence* against a standards checklist — an AISI-shape evaluator runs the *system itself*, on their infrastructure or ours, with their evaluation harness and their attack payloads. The evaluation surface is live, the payloads are novel, and the whole exercise only produces useful signal if the payloads do not leak — back into the provider's training corpus, sideways into peer providers' systems via shared benchmarks, or forward into the public web where the next scrape cycle will absorb them. A payload that leaks has burned its evaluation utility for every subsequent round.

Handling this interface well is why the release-assurance programme owns the third-party surface (`mod-101` deferral contract, external row) rather than delegating it to procurement or legal. Procurement can sign an NDA; only the assurance programme knows which log stores need to be excluded from the training-data pipeline, which evaluation slices need to be sequestered from the online-eval telemetry (`mod-104`), and which reproducibility bundles can safely be exchanged (`mod-104` chapter `03`).

This chapter walks the AISI-shape evaluators that matter, what they typically ask for, the shape of the handoff envelope, and the attack-payload non-disclosure discipline the envelope has to enforce.

A note on scope. The chapter treats *AI-safety-institute-shape* as a category with clear boundaries — technical evaluator, capability-scoped, generally-confidential findings, methodology-preserving payload discipline. The category includes the sovereign institutes (UK, US), the sovereign-adjacent bodies (Singapore AI Verify), and the independent research organisations whose engagements follow the same interface pattern (METR, Apollo Research). It does *not* include notified bodies (chapter `02`), NYC-AEDT-style compliance auditors (chapter `03`), Big-Four attest firms (chapter `04`), or bug-bounty programmes; those interfaces are different enough in shape that grouping them here would obscure the specific disciplines the AISI shape requires.

## Who the AISI-shape evaluators are

### UK AI Security Institute (formerly UK AI Safety Institute)

**Who they are.** The UK AI Security Institute (formerly the UK AI Safety Institute — the rebrand landed in 2025) is a directorate of the UK Department for Science, Innovation and Technology, established after the November 2023 Bletchley AI Safety Summit. It maintains a technical evaluations team and publishes the `Inspect` open-source evaluation framework at [inspect.aisi.org.uk](https://inspect.aisi.org.uk/). Its institutional home page is [aisi.gov.uk](https://www.aisi.gov.uk/).

**What they ask for.** Credentialed access to a target model (typically pre-deployment or at a specific release candidate); a deployment-context statement (what the model is for, what surface it is exposed on, what safeguards sit around it in production); a deployment-tier framework document (the provider's internal deployment-tier framework — Anthropic's Responsible Scaling Policy, OpenAI's Preparedness Framework, Google DeepMind's Frontier Safety Framework, or the enterprise's internal equivalent); a draft safety case for the release; and reproducibility bundles for any capability elicitations the provider has already run (`mod-104` chapter `03` shape).

**Handoff envelope.** A sandboxed evaluation environment, or read-only API credentials against a pinned model version, with a bounded evaluation window; a shared secure workspace for reports and artefacts; a mutual non-disclosure agreement covering both the evaluator's attack payloads and the provider's internal safety-case detail; a return channel for the evaluator's findings that preserves provenance (signed report, digest-pinned to the model version tested).

**Release-assurance implication.** UK AI Security Institute engagements typically feed the release-gate at the highest deployment tier. Their findings become an evidence-contract row in the `mod-102` chapter `06` sense — an *external* leaf whose warrant is "signed by AISI, dated within the pre-deployment evaluation window, pinned to model digest X". The release-gate cannot pass the corresponding claim without the AISI report; the report cannot be produced without the handoff envelope this chapter specifies.

### US AI Safety Institute at NIST and the AISI Consortium

**Who they are.** The US AI Safety Institute sits inside the National Institute of Standards and Technology and coordinates the AI Safety Institute Consortium (AISIC), a multi-hundred-member consortium of AI providers, deployers, academic labs, and civil-society organisations. Its home page is [nist.gov/aisi](https://www.nist.gov/aisi). The Institute's remit includes red-team methodology, safety evaluations for advanced models, and pre-deployment testing agreements with major providers <!-- needs-research: verify current scope statement post-2025 executive-order changes -->.

**What they ask for.** Similar to the UK Institute — credentialed access to a target model, a deployment-context statement, and the provider's internal deployment-tier framework — with the addition (for AISIC members) of consortium-shared methodology contributions and cross-consortium benchmark participation. Where the US Institute has a pre-deployment testing agreement in place, the shape converges on the UK Institute's.

**Handoff envelope.** Consortium-shared secure workspace; per-engagement mutual NDA; pinned model access with a bounded evaluation window; provenance-preserving return channel.

**Release-assurance implication.** For US-headquartered providers, the US Institute engagement is often the primary AISI-shape leaf in the release-gate assurance case. For multinational providers, both UK and US engagements can appear as parallel leaves, each with its own evidence-contract row.

### Singapore AI Verify Foundation

**Who they are.** The AI Verify Foundation is a Singapore government-backed non-profit that stewards the AI Verify testing framework and toolkit. Its home page is [aiverifyfoundation.sg](https://aiverifyfoundation.sg/). The framework is oriented toward organisational and technical testing against a set of AI-governance principles; the Foundation is closer to a *methodology steward* than an operational red-team, but it acts as an evaluator-shape interface for organisations in the ASEAN region.

**What they ask for.** A completed AI Verify self-assessment (organisational + technical), documentary evidence for each principle, and — for the technical tests — access to a model or system under test in a form the AI Verify toolkit can drive.

**Handoff envelope.** Self-assessment upload, evidence-file exchange, and toolkit run against a sandboxed model instance. Non-disclosure is present but the surface is narrower than the AISI red-team surface because AI Verify's tests are largely open.

**Release-assurance implication.** For ASEAN-market releases, an AI Verify engagement often serves the analogous slot to a UK/US Institute engagement, though its evidentiary weight against a release-gate claim depends on the claim's specificity.

### METR (Model Evaluation and Threat Research)

**Who they are.** METR is an independent non-profit that develops methodology for evaluating dangerous autonomous capabilities of frontier AI systems. Its home page is [metr.org](https://metr.org/). METR has produced widely-referenced task suites (autonomous replication, self-exfiltration precursors, task-length capability curves) that AISI-shape institutes and providers increasingly reference or run.

**What they ask for.** Credentialed access to a target model (often via provider API or a fine-tuned research affordance), sufficient elicitation compute, and a research-collaboration agreement covering scope, publication rights, and attack-payload confidentiality.

**Handoff envelope.** Time-bounded credentialed access, shared secure workspace, mutual NDA on task specifications and elicitation prompts, and a return channel for METR's evaluation report.

**Release-assurance implication.** For the tier-3 agentic-capability leaf in the release-gate case, a METR-run or METR-methodology-aligned evaluation is often the anchor evidence. The `agentic-safety-engineer` peer (level 40, `mod-101` deferral contract) typically brokers the engagement and hands the resulting evidence to this programme.

### Apollo Research

**Who they are.** Apollo Research is an independent AI-safety research organisation focused on deceptive-alignment and scheming evaluations. Its home page is [apolloresearch.ai](https://www.apolloresearch.ai/). Apollo's methodology emphasises behavioural tests for deception and scheming across long-horizon and multi-turn interactions.

**What they ask for.** Similar to METR — credentialed model access, elicitation affordances, and a research-collaboration agreement.

**Handoff envelope.** Same shape as METR.

**Release-assurance implication.** Apollo-shape evaluations feed the deception / scheming leaf in the risk-engineer's harm inventory (`mod-101` deferral contract, risk-engineer row) and, for frontier deployments, appear as an external-evaluator leaf in the release-gate case.

The `agentic-safety-engineer` peer (level 40) is the natural craft owner for the Apollo interface; the release-assurance programme owns the evidence-contract row and the audit trail.

### MLCommons AI Safety Working Group

**Who they are.** The MLCommons AI Safety Working Group maintains benchmark suites (AILuminate is the anchor) for evaluating LLM safety across hazard categories. Its home page is [mlcommons.org/working-groups/ai-safety/ai-safety/](https://mlcommons.org/working-groups/ai-safety/ai-safety/).

**What they ask for.** Model access sufficient to run the benchmark suite, either directly or via a submitted-model workflow analogous to the classic MLPerf shape. The workflow is closer to *benchmark-shape evaluation* than to AISI-shape red-team, but the confidentiality discipline for the benchmark's held-out slices matters in the same way.

**Handoff envelope.** Submitted-model workflow with held-out slice sequestration; results are typically published with vendor identifiers.

**Release-assurance implication.** MLCommons AI Safety results feed the release-gate's `MEASURE-2.6` (safety) leaf and, because they are published, feed the external card (`mod-105`) as well.

### Adjacent shapes worth naming

Two adjacent evaluator shapes appear frequently enough at intake that the programme should be able to distinguish them from the AISI shape without a full engagement discussion. First, *academic red-team collaborations* — university-based safety-research groups run engagements that resemble AISI-shape engagements in method but do not carry the sovereign or quasi-sovereign standing of the institutes named above; findings are typically published as academic papers rather than as evaluator reports and payloads may enter the open literature. Second, *bug-bounty programmes* — vulnerability-disclosure programmes run against the AI system's product surface produce a stream of findings that overlap with red-team findings but under a very different disclosure regime (public disclosure on remediation, standardised triage, no bilateral NDA). The release-assurance programme handles both, but neither substitutes for an AISI-shape engagement at the highest deployment tiers.

## Why attack-payload non-disclosure matters

Every AISI-shape evaluation produces two classes of artefact: the *findings* (which the provider needs, the evaluator publishes at least in aggregate, and the release-gate consumes) and the *attack payloads* (the specific prompts, tool-use sequences, or elicitation techniques the evaluator used to produce the findings). The two classes have opposite disclosure profiles.

Findings must flow — into the release-gate, into the assurance case, and often into a published safety-case summary. Payloads must *not* flow. Three failure modes justify the discipline:

- **Training-corpus contamination.** If evaluator payloads land in provider log stores that feed the RLHF or SFT pipeline, the next model is trained to *refuse the specific payload* rather than to *generalise the harm class*. The payload's evaluation utility is destroyed; the underlying capability remains.
- **Peer-provider leakage.** If the payload set ends up in a shared benchmark or a jointly-hosted eval suite, every provider whose model touches the benchmark gets pre-training exposure. The AISI's ability to elicit the capability across the frontier drops to zero.
- **Public-web scrape.** If a payload lands in a report, blog post, or bug tracker that is later scraped into a training corpus, the same contamination occurs at internet scale.

Non-disclosure of payloads is therefore not an evaluator courtesy — it is a *methodology-preserving control* the release-assurance programme has to enforce at three points in its own infrastructure: the training-data pipeline (payloads excluded), the online-eval telemetry (`mod-104`, payloads excluded from any log that feeds back into fine-tune candidates), and the reproducibility-bundle exchange (payloads never included in provider-side reproducibility bundles, only in evaluator-side ones).

## The handoff envelope shape

The envelope is the persisted contract between the provider and the AISI-shape evaluator. Six components:

- **Read-only credentialed access.** A dedicated set of credentials, scoped to a pinned model version, with a bounded evaluation window (start / end timestamp), rate limits sized to the evaluator's expected volume, and observability that lets the provider confirm the credentials are not being used outside the window. No fine-tune access; no training-data write path from the eval traffic back to the pipeline.
- **Dedicated evaluation environment.** Either a sandboxed instance of the deployed system (production configuration but isolated from real users and from the production log store) or the evaluator's own infrastructure with API access. In both cases, evaluator traffic is *segregated* from production telemetry — it does not enter the online-eval slice (`mod-104`) and does not enter any log store the training-data pipeline consumes.
- **Reproducibility-bundle exchange, one-way.** The provider hands the evaluator the release candidate's reproducibility bundle (`mod-104` chapter `03`) — model digest, harness code, eval-set descriptors *of provider-side evaluations already run* — but *not* the evaluator's return bundle. The return channel carries the evaluator's report; the payload-carrying artefacts stay evaluator-side.
- **Mutual non-disclosure agreement.** Bilateral NDA covering (a) the evaluator's attack payloads and methodology, (b) the provider's internal safety case, unpublished harm inventory rows, and any commercially-sensitive deployment context. NDA has an explicit clause on *derivative artefacts* — payloads or findings reproduced in downstream reports still fall under the original disclosure profile.
- **Provenance-preserving return channel.** The evaluator's report arrives as a signed artefact, pinned to the model digest tested and the evaluation window. The release-assurance programme ingests the report into the assurance bundle (`mod-104` chapter `06`) as an external-evaluator leaf with its own DSSE signature and its own Rekor log entry, if the evaluator publishes to a transparency log.
- **Post-engagement dispositions.** A written procedure for what happens if the evaluator finds a capability that shifts the release's deployment tier — pause, mitigate, re-evaluate, or refuse the release. This is a `mod-103` release-gate hook: the engagement can produce a *hard-fail* the release-gate must honour.

Each of the six components has an owner. The credentialed access is owned jointly with `ai-infra-security` (level 35, per `mod-101` deferral contract). The evaluation environment is owned jointly with the platform team. The reproducibility-bundle exchange is owned by this programme (via `mod-104`). The NDA is owned jointly with legal. The return channel and post-engagement dispositions are owned by this programme. Ownership rows are documented in the engagement's charter so no component is orphaned when the on-call rotates.

## Worked example — handing a customer-support-agent frontier deployment to the UK AI Security Institute

A provider is releasing an internal-assistant tier-3 deployment: a customer-support agent with tool use over a knowledge base and a limited action surface (open ticket, look up customer record, schedule callback). The internal deployment-tier framework classifies the release at the highest bar because of tool-use surface and customer-data exposure.

The release-assurance programme prepares the handoff envelope:

1. **Deployment-context statement.** Two-page document naming the surface (customer chat), the tools exposed (three named tools with parameter shapes), the guardrails around each tool (`ai-risk-engineer` guardrail-eval report v3), and the deployment tier per the internal framework.
2. **Deployment-tier framework document.** The internal frontier-safety framework, marked confidential, shared under the mutual NDA.
3. **Draft safety case.** SACM `ArgumentPackage` at the current freeze (`mod-102` chapter `04`), redacted of any commercially-sensitive harm-inventory detail the evaluator does not need.
4. **Reproducibility bundles for provider-side evaluations.** The `mod-104` chapter `03` bundles for the release candidate's functional-adequacy, robustness, and safety measurements — model digest, harness code, eval-set descriptors, statistical warrant. This lets the evaluator triangulate their findings against what the provider has already measured.
5. **Credentialed access.** A dedicated API key against the pinned model digest, valid for an eight-week evaluation window, with a segregated log store the training pipeline does not consume from.
6. **Return channel.** A signed report from the UK AI Security Institute arrives at week nine, pinned to the model digest, ingested as an external-evaluator leaf with a DSSE signature.

The programme's non-disclosure discipline blocks three specific pipes for the duration of the engagement: the training-data pipeline drops the evaluator's log store from its ingestion set; the online-eval slice's drift-detector is filtered to exclude the evaluator's traffic; and the provider's incident-tracking system flags any bug ticket that quotes evaluator-supplied prompt content for legal review before it can be forwarded to peer teams or vendors.

## Common failure modes at the AISI interface

Four failure modes appear repeatedly in first-time AISI-shape engagements and are worth naming so the programme designs to prevent them.

- **Evaluator traffic contaminates the training pipeline.** The provider's log-ingestion pipeline treats all API traffic as training-candidate signal and absorbs the evaluator's attack payloads. Fix: segregate the evaluator's credentials at the log-store level, not only at the network level, and audit the training-data pipeline's ingestion allowlist explicitly against the evaluator's credential identifier.
- **The safety-case draft is over-redacted.** The provider redacts so much of the safety case that the evaluator cannot triangulate their findings against the provider's internal harm model, and produces an evaluation that reads as unrelated to the provider's actual concerns. Fix: redact commercially-sensitive detail but preserve the harm-inventory *shape* and the deployment-tier framework's substantive criteria.
- **The reproducibility bundle is inadequate.** The provider hands the evaluator a bundle that does not let them reproduce the provider's internal evaluations, so the evaluator cannot distinguish their new findings from re-discovery of what the provider already knew. Fix: use the `mod-104` chapter `03` bundle shape end-to-end, including harness code and eval-set descriptors, not just result summaries.
- **The return channel has no provenance.** The evaluator's report arrives as an unsigned PDF that cannot be pinned to the tested model version. Fix: require the evaluator to sign the report (DSSE envelope or equivalent) and to cite the model digest in the report's header; where the evaluator publishes to a transparency log, record the log entry in the assurance bundle (`mod-104` chapter `06`).

## The `Inspect` framework as a shared substrate

Worth naming separately: the UK AI Security Institute's open-source `Inspect` framework ([inspect.aisi.org.uk](https://inspect.aisi.org.uk/)) is increasingly the shared substrate on which multiple AISI-shape evaluations are authored. It gives evaluators a common way to express task suites, solvers, scorers, and eval logs; it gives providers a common way to *host* evaluations in their own infrastructure (for a self-hosted engagement variant) without having to invent the plumbing. The release-assurance programme should understand `Inspect` as an ecosystem-level artefact worth investing familiarity in — its adoption reduces per-engagement setup cost across the AISI-shape institutes, and its log format is a good starting point for the provider's own AISI-interface adapter (`mod-104` chapter `02`).

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the external row for third-party evaluators is the ancestor of this chapter's envelope.
- `mod-102` (assurance case) — AISI evidence appears as an external-evaluator leaf in the case; the evidence-contract row is negotiated by this programme.
- `mod-103` (release-gate) — the AISI report is a hard-gate criterion at the highest deployment tier; the engagement can produce a hard-fail.
- `mod-104` (evidence pipeline) — the reproducibility-bundle exchange is one-way, and the online-eval slice must be segregated from evaluator traffic.
- `mod-105` (cards) — the AISI finding summary feeds the safety-case section of the external card; payloads do not.
- `mod-110` (post-market surveillance) — if the evaluator flags a capability post-release, the surveillance plan has to incorporate the finding.
- `mod-111` (GPAI systemic-risk) — for EU AI Act Article 55 systemic-risk providers, an AISI-shape engagement is one of the anchor evidence streams.

## Summary

- The AISI shape (UK AI Security Institute, US AI Safety Institute and the AISI Consortium, Singapore AI Verify Foundation, METR, Apollo Research, MLCommons AI Safety Working Group) is a first-class interface the release-assurance programme owns.
- Each evaluator asks for a similar bundle: credentialed model access, deployment-context statement, deployment-tier framework, safety-case draft, reproducibility bundles for provider-side evaluations already run, and PII-scrubbed transcripts.
- Attack-payload non-disclosure is methodology-preserving, not courteous — payloads leaking into training corpora, peer providers' systems, or the public web destroys the payload's evaluation utility across the frontier.
- The handoff envelope has six components: read-only credentialed access with a bounded window, dedicated evaluation environment, one-way reproducibility-bundle exchange, mutual NDA covering payloads and provider safety-case detail, provenance-preserving return channel, and post-engagement disposition hooks into the release-gate.
- Exercise `01` has you design the handoff for a customer-support-agent frontier deployment and defend the non-disclosure discipline against the three specific leakage failure modes.
