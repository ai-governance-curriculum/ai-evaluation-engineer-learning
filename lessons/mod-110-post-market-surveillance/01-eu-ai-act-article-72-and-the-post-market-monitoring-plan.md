# EU AI Act Article 72 and the Post-Market Monitoring Plan

## Motivation

A release-gate decision is a claim about a moment. At time `T`, the assurance case discharged its obligations against a specific evidence bundle (`mod-104` chapter `06`); the walker signed a decision record; the system was placed on the market or put into service. The claim only holds while its premise evidence is still true. Real deployments drift — the input distribution shifts, deployers use the system in ways the intended-purpose statement did not anticipate, the underlying foundation model gets a silent vendor update, an adversary discovers a new failure mode. Without a *live* surveillance loop, the release decision decays into an assertion about the past.

The EU AI Act (Regulation (EU) 2024/1689) codifies this loop for high-risk AI systems in **Article 72 — Post-market monitoring by providers, and post-market monitoring plan**. Article 72 is where the release-assurance programme's ongoing life shows up as a statutory obligation, not a hygiene practice. This chapter reads the article the way an assurance methodology owner has to read it — as a *design brief* for a plan that must be documented, proportionate, executable, and demonstrably wired into corrective action (Article 20) and incident reporting (Article 73).

## What Article 72 says

<!-- needs-research: reconfirm the exact wording of Article 72 paragraphs 1-3 and any Commission implementing act published on the post-market monitoring plan template as of 2026-07 -->

**What it says (paragraph 1).** Providers shall establish and document a post-market monitoring system in a manner that is proportionate to the nature of the AI technologies and to the risks of the high-risk AI system. The system shall actively and systematically collect, document, and analyse relevant data provided by deployers or collected through other sources on the performance of high-risk AI systems throughout their lifetime, and shall allow the provider to evaluate the continuous compliance of AI systems with the requirements set out in Chapter III, Section 2 (Articles 8–15).

**Release-assurance implication.** Four verbs bind: *actively*, *systematically*, *collect*, *analyse*. Passive log retention does not discharge Article 72 — the monitoring must be a *loop* with a review cadence, defined triggers, and a documented feedback into the risk-management system (Article 9) and technical documentation (Article 11). Under `mod-112`, this loop is the operational core of the release-assurance programme.

**What it says (paragraph 2).** The post-market monitoring system shall be based on a post-market monitoring plan. The post-market monitoring plan shall be part of the technical documentation referred to in Annex IV. The Commission shall adopt an implementing act laying down detailed provisions establishing a template for the post-market monitoring plan and the list of elements to be included in the plan.

**Release-assurance implication.** The plan is a *release-package artefact* — it ships inside the Annex IV bundle at gate time, not months later. The assurance programme's evidence pipeline (`mod-104`) stores the plan by content-address, cites its digest in the top-level assurance bundle manifest under `post_market_handoff_digest`, and versions it under change control. <!-- needs-research: check whether Commission has published implementing / delegated acts on the Article 72 template as of 2026-07; if published, the plan's structural shape becomes prescriptive rather than principle-based -->

**What it says (paragraph 3).** For high-risk AI systems covered by the Union harmonisation legislation listed in Section A of Annex I, where a post-market monitoring system and plan are already established under that legislation, the provider may integrate — where appropriate — the elements described in paragraphs 1 and 2 into the existing systems and plans, provided that an equivalent level of protection is achieved.

**Release-assurance implication.** For sector-regulated deployments (medical devices under MDR/IVDR, in-vitro diagnostics, machinery, radio equipment) the AI Act does not demand a *separate* plan — it demands *equivalence*. Chapter `04` in this module walks the FDA PCCP overlay; `mod-107` walks the wider sector overlay pattern. The assurance programme runs one unified monitoring runbook and tags each observation with the applicable authority.

## How Article 72 binds to Article 15's declared levels

Article 15 requires providers to declare the levels of accuracy, robustness, and cybersecurity that the high-risk system achieves, in the instructions for use and the technical documentation. Those declarations are *not* one-shot — they are the reference against which post-market signal is measured. The Article 72 plan is what verifies the declarations *remain true* over the system's lifetime.

Concretely, if the release-gate discharged a `GATE-FA-01` criterion at time `T` with "per-class F1 ≥ 0.85 (CI lower bound ≥ 0.83)" as the declared accuracy level, then the Article 72 plan owns:

- The online-eval slice that re-measures per-class F1 on production traffic on a stated cadence.
- The threshold below which the declared level is considered breached (the same 0.83 CI-lower-bound floor, or a pre-registered `epsilon` around it — see chapter `03`).
- The trigger that fires a re-review of the assurance case's `Article-15-accuracy` claim when the threshold is breached (chapter `03`).
- The corrective-action route under Article 20 when the re-review concludes the declared level is no longer supportable.

The plan therefore *closes the loop* Article 15 opens.

## Structure of a post-market monitoring plan

The plan is a controlled document (ISO/IEC 42001 clause 7.5) with the following sections. The exact template will be prescribed if and when the Commission implementing act lands; in the meantime, this shape maps every paragraph 1 verb to a named subsection.

### 1. System identification

- Provider identity and Article 49 registration reference (EU database entry).
- Product and release-candidate identifiers (`system_under_release` from the assurance bundle).
- Intended purpose statement (per Article 13 instructions for use).
- Annex III use-case classification and Article 6 high-risk determination.
- Notified body (if applicable under Article 43) and its identification number.

### 2. Monitoring objectives

- **Continuous compliance with Chapter III, Section 2.** The plan lists each of Articles 9–15 and names the monitoring evidence for each.
- **Detection of drift** — input, output, harm-signal, and fairness drift.
- **Detection of previously unforeseen risks** — new harms, new misuse patterns, new fundamental-rights impacts.
- **Verification of the risk-management system** (Article 9 loop closure).
- **Feed of learnings** into design of the next release cycle (`mod-103` chapter `01`).

### 3. Monitored characteristics

For each Chapter III, Section 2 obligation, the plan names the monitored characteristic, the metric, the threshold, and the review cadence:

| Obligation | Monitored characteristic | Metric | Threshold | Cadence |
| --- | --- | --- | --- | --- |
| Article 9 (risk management) | Reasonably-foreseeable-misuse register freshness | Days since last review | 90 days | Quarterly |
| Article 10 (data governance) | Input-distribution drift on named features | KL-divergence vs. release-time baseline | Pre-registered `d_max` | Weekly |
| Article 13 (transparency) | Deployer complaint volume against instructions clarity | Complaint rate per 10⁶ interactions | Pre-registered `c_max` | Monthly |
| Article 14 (human oversight) | Override rate by human overseer | Deviations from output per session | Pre-registered `o_max` | Monthly |
| Article 15 (accuracy) | Per-class F1 on production slice | 95% CI lower bound | ≥ 0.83 | Continuous (`mod-103` chapter `06`) |
| Article 15 (robustness) | Adversarial-attack success on refreshed threat model | Attack-success rate | ≤ 5% | Quarterly refresh, continuous production monitor |
| Article 15 (cybersecurity) | Supply-chain integrity of judge / model / dataset | BOM digest match | Match required | Per deployment |

The table is *illustrative* — every programme picks its own metrics, but the *shape* (obligation → characteristic → metric → threshold → cadence) is what makes the plan auditable.

### 4. Data-collection methods

The plan enumerates every source Article 72 admits and how the programme ingests each:

- **Telemetry from the deployed system.** Production traces (OpenTelemetry Gen-AI, OpenInference) captured by the peer AI-eval engineer (level 30) under the record-keeping obligation of Article 12; the assurance programme *consumes* pinned slices, does not own the observability substrate (`mod-104` chapter `01`).
- **Deployer channels.** A structured deployer-report intake (bug reports, complaint forms, escalations under Article 26(5), harm reports). Deployer feedback is a first-class evidence source under Article 72 paragraph 1.
- **End-user feedback.** Thumbs-down, complaint, appeal, or opt-out signal collected under Article 13's transparency obligation.
- **Internal red-team refresh.** Adversarial-eval refresh from the peer `ai-risk-engineer` (level 25) on a stated cadence.
- **External incident registries** — AI Incident Database, OECD.AI Incidents Monitor, MIT AI Risk Repository (chapter `05`).
- **Notified-body inspection findings** (Article 43 pathway).
- **Market-surveillance authority communications** — findings, requests, notices under Articles 74 and 79.

Each source is named with an owner peer track, an ingest cadence, and a store landing (`mod-104` chapter `02`).

### 5. Analysis methodology

- **Statistical procedure** — for each measured characteristic, the method (bootstrap CI, drift test, run-length control) is named and versioned.
- **Signal aggregation** — how many independent sources have to agree before a re-review trigger fires (chapter `03`).
- **Root-cause conservatism** — the assumption stance for ambiguous signal (default: conservative — treat as regression until disproven).
- **Human review** — which signals require human triage vs. automated disposition.

### 6. Review cadence and triggers

- **Standing cadence** — every measured characteristic gets a scheduled review; the review reads the current metric against the declared threshold and updates the assurance case's evidence pointers.
- **Event-triggered review** — a threshold breach, an external-incident-registry match (chapter `05`), a deployer escalation, a notified-body finding, or a serious incident (Article 73, chapter `02`) fires an out-of-cadence review.
- **Annual comprehensive review** — the whole plan is re-visited annually and at every major release; the review record lands in ISO/IEC 42001 clause 9.3 (management review).

### 7. Integration with Article 20 (corrective actions)

Article 20 obliges providers who consider or have reason to consider that a high-risk AI system placed on the market or put into service is not in conformity with the Regulation to take corrective actions — bringing the system into conformity, withdrawing it, disabling it, or recalling it — and to inform relevant deployers, distributors, importers, and the market-surveillance authority. The plan names the *decision procedure* that carries a monitoring finding into an Article 20 corrective action, the *authority contract* (who signs an Article 20 disposition), and the *evidence trail* the corrective action produces.

### 8. Integration with Article 73 (serious-incident reporting)

The plan cross-references chapter `02` of this module: which monitored characteristics can escalate into a serious incident, what triage carries the escalation, and what the notification wall-clock is.

### 9. Change control on the plan itself

The plan is versioned in the assurance store, superseded rather than edited, and reviewed on framework updates (Article 96 delegated acts, harmonised standards changes, Commission implementing acts). Every amendment carries a rationale, a signer, and a diff against the superseded version. The plan's history is the record of how the programme learned across its operating life.

## Proportionality is a design constraint, not a get-out

Paragraph 1's "proportionate to the nature of the AI technologies and to the risks" is the article's most-tested clause. It is *not* an invitation to under-monitor. Proportionality means the monitoring effort scales with the risk profile — a chest-X-ray triage AI carries a heavier monitoring plan than a customer-service intent classifier — but the *structural* obligations (documented plan, actively and systematically operated, feeding Article 20 corrective action, integrating Article 73 incident reporting) are non-negotiable regardless of scale. Programmes have tried to argue their systems are "too small to be worth a plan"; that argument does not survive an inspection.

A defensible proportionality argument reads: "the monitored characteristics are `{X, Y, Z}` because the harm inventory (`mod-102` chapter `06`) identifies `{H1, H2}` as the material risks; the cadence is `{C}` because signal-to-noise on the metrics resolves at that timescale; the analysis methodology is `{M}` because it detects the failure modes at the pre-registered significance in the pre-registered wall-clock." The argument cites the harm inventory, the intended-purpose statement, and the peer track's methodology. It does *not* read "the system is low-risk, so we do less"; that formulation collapses under adversarial reading by a market-surveillance authority.

## Deployer channels — a first-class source

Article 72 paragraph 1's specific mention of *data provided by deployers* is the point where the assurance programme has to solve a coordination problem outside its own team. The deployers are not always the programme's own colleagues — they are separate legal entities (hospitals, banks, retailers, government agencies) using the system under their own authority (Article 26). The programme has to design a *deployer channel* that is easy for the deployer to use, that produces machine-ingestible signal, and that survives friction.

Three shapes recur:

- **Contractual channel** — the deployment contract (Article 26 obligations flow through to Article 27 impact-assessment obligations for specified deployer categories) includes a schedule that names the deployer's reporting cadence, the report format, and the incident-notification wall-clocks. Contractual channels are enforceable but slow; they work best for structured periodic reports.
- **Platform channel** — the deployed system itself surfaces a "report an issue" affordance whose entries flow into the provider's observability substrate under an agreed schema. Platform channels are fast but require deployer engagement with the affordance.
- **Human channel** — a named point-of-contact at the provider receives deployer escalations. Human channels are the fallback and are essential for incidents; they are slow for standing signal.

A defensible plan carries all three, with a tiering: standing signal comes through the platform channel; periodic structured signal comes through the contractual channel; incident and out-of-band signal comes through the human channel. `mod-108` walks the tier-specific deployer contract patterns in more depth.

## Worked shape — customer-service RAG system

Consider a customer-service RAG assistant deployed by a European retail bank as a *deployer* of a *provider*'s foundation model, with the bank fine-tuning and integrating the assistant under its own name for its customers — the bank is therefore a provider of the derivative system under Article 25. The system is Annex III high-risk on the basis of its use in a service that materially affects access to essential private services (financial-services triage).

The Article 72 plan for this system reads, in outline:

- **Identification.** Provider = the bank; product = `customer-triage-assistant`; release-candidate = `rc-2026-05-07`; intended purpose = "route customer inquiries to the correct service line and draft a suggested response the human agent reviews before sending"; Annex III use-case = access to essential private services; Article 49 registration = `EU-DB-…-2026-000123`.
- **Monitoring objectives.** Continuous compliance with Articles 9–15; drift detection on the retrieval-relevance distribution and on the fine-tuning slice; detection of new misuse patterns (customers attempting to elicit account details from other customers); verification of the human-agent oversight loop under Article 14.
- **Monitored characteristics.** Per-intent classification accuracy (Article 15); retrieval-relevance drift (Article 10 / Article 15); hallucination rate on financial-fact statements (Article 15); complaint rate on drafted responses (Article 13); human-agent override rate on drafted responses (Article 14); refusal rate on policy-violating queries (Article 9); adversarial jailbreak-success rate (Article 15 cybersecurity).
- **Data-collection.** Telemetry via OpenTelemetry from the assistant surface (owner: platform team); deployer channel = internal branch feedback form (owner: retail-ops); end-user feedback = post-interaction survey (owner: retail-ops); red-team refresh quarterly (owner: `ai-risk-engineer`); external-registry scan weekly (owner: assurance programme).
- **Analysis methodology.** Per-characteristic control chart with a 7-day run-length trigger; two-source agreement rule (a signal fires re-review only if telemetry and one deployer / user channel agree); root-cause conservatism = assume regression until disproven.
- **Review cadence.** Weekly standing review of drift metrics; monthly review of complaint / override signal; quarterly comprehensive review; annual plan re-visit.
- **Article 20 integration.** A confirmed regression triggers a corrective-action ticket in the assurance programme; disposition options are retrain-and-redeploy, downgrade to human-only routing, or withdraw the system.
- **Article 73 integration.** A hallucination that causes a customer to act on materially wrong financial information can meet the "serious harm to property" threshold (chapter `02`); the plan cross-references the incident procedure.

The plan lands in the store as `postmarket-plan/customer-triage-assistant/v1` and is referenced from the assurance bundle for `rc-2026-05-07`.

## Where this shows up in the rest of the track

- `mod-101` chapter `04` — Article 72 named in the article set that shapes the release-gate.
- `mod-102` — the assurance case's `Article-15-*` claims are the anchors the plan's triggers reopen.
- `mod-103` chapter `05` — the runbook's incident-cutover and rollback triggers consume the plan's signals.
- `mod-104` chapter `06` — the plan is a manifest field (`post_market_handoff_digest`) in the assurance bundle.
- `mod-107` — sector overlays (SR 11-7 ongoing monitoring, FDA PCCP) integrate with the plan under Article 72(3).
- `mod-108` — deployment tier changes are one disposition the plan can trigger.
- `mod-112` — running the plan across a portfolio is the operational core of the programme.

## Summary

- Article 72 requires an *actively and systematically operated* post-market monitoring system, proportionate to the risks, documented as a plan that is part of the Annex IV technical documentation.
- The plan verifies that Chapter III, Section 2 obligations — in particular the Article 15 declared levels of accuracy, robustness, and cybersecurity — remain true across the system's lifetime.
- A defensible plan has nine sections: identification, objectives, monitored characteristics, data-collection methods, analysis methodology, review cadence and triggers, Article 20 integration, Article 73 integration, and change control.
- Article 72 paragraph 3 allows integration with sector-regulated monitoring plans (FDA PCCP, MDR post-market surveillance) provided equivalent protection is achieved — chapter `04` walks this overlay.
- Exercise 01 has you author the Article 72 post-market monitoring plan for a specific in-scope high-risk system, section by section, with triggers wired to the assurance case claims.
