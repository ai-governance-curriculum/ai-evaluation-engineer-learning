# Eval-Set Exfiltration, Contamination, and the MLSec Boundary

## Motivation

Every previous chapter in this module has treated the eval-set as a trusted input: the store hashes it (chapter `01`), the adapter binds it into a record (chapter `02`), the bundle ships it (chapter `03`), and provenance attests where it came from (chapter `04`). None of that is worth much if the eval-set has already leaked *into* the model, or is leaking *out of* the pipeline.

Two failure modes shape this chapter.

The first is **eval-set contamination**: the eval-set (or portions of it) is already inside the model's training corpus, either directly (the eval-set was scraped by the pretraining crawler) or indirectly (a paraphrase of the eval-set was in the corpus; the eval-set was recycled through a benchmark meta-set the model providers all indexed). The eval numbers are optimistic — the model is not evaluating on novel data, it is retrieving from memorised data. Under NIST AI RMF MEASURE-2.13 (effectiveness of measurement) a contaminated benchmark is not a measurement. Under EU AI Act Article 15(1)(a) (accuracy), the number the provider ships to the market-surveillance authority under Article 74 is one whose warrant has been silently invalidated.

The second is **eval-set exfiltration**: the eval-set leaks *out of* the pipeline — through a hosted-provider API call whose contents the provider retains and uses for future training, through an evaluator container that emits inputs to a telemetry endpoint, through a judge model that is itself the "next generation" of the model under test and quietly memorises what it scored, or through an insider or a leaky log. Once the eval-set has leaked, its value as a hidden reference collapses — future runs on that eval-set are contaminated by construction.

Both failure modes are peer-owned. The `ai-infra-security` track (peer, level 35) owns the deep MLSec view — the threat modelling, the compartment design, the depth adversarial coverage, the exfiltration-control policy. The release-assurance program does not backfill that craft. What the release-assurance program owns is: the *evidence contract* into that peer, the *supply-chain-security clauses* threaded into the assurance bundle, and the *audit trail* that a market-surveillance authority can follow when a contamination or exfiltration incident is later suspected. This chapter draws that ownership boundary.

## The threat model in one page

Enough of the threat model to reason about it — depth lives in the `ai-infra-security` track.

### Contamination — how eval-sets leak *into* models

- **Direct pretraining scrape.** The eval-set (or its source, e.g., a public benchmark) is on the open web; the pretraining crawler ingests it. Common with public benchmarks (MMLU, GSM8K, HELM tasks, MATH) that are widely known; less common but not impossible with programs' internal eval-sets that are accidentally leaked.
- **Paraphrase / cross-lingual leakage.** The eval-set is not verbatim in the pretraining corpus, but a paraphrase (English → French → English) or a semantic near-duplicate is. Detection is harder; the model's grip on the eval-set is still stronger than it should be.
- **Meta-benchmark or aggregation leakage.** A public aggregator (a benchmark of benchmarks, a leaderboard export, a Hugging Face dataset that reindexes many evaluation sets) republishes eval-set entries the pretraining crawler then ingests as if they were novel.
- **Chain-of-thought contamination.** A public LLM answering a benchmark question emits an answer with its reasoning; the answer is scraped as text, and later pretraining runs learn *the reasoning path* the model produced. The next model's eval performance on the benchmark reflects the earlier model's chain of thought rather than novel reasoning.
- **Fine-tune leakage.** The model was fine-tuned on data that includes a benchmark (or an internally reused eval-set). The provider intended fine-tune data to be "clean" but the pipeline that gathered fine-tune data pulled from a source that included the benchmark.
- **RAG-side contamination.** For RAG systems, the retriever's index contains the eval-set answers verbatim, and the "eval" is really testing whether the retriever finds the eval-set entry.

### Exfiltration — how eval-sets leak *out of* pipelines

- **Hosted-provider retention.** The eval calls a hosted API; the provider retains user data for training. The eval-set is now in the provider's next training corpus. Mitigations: opt-out from training (where the provider offers it), zero-data-retention endpoints, on-prem deployment for high-stakes runs.
- **Evaluator telemetry.** The evaluator container ships a telemetry SDK that phones home eval-inputs to an observability vendor whose retention terms allow the eval-inputs to enter the vendor's own dataset pool. Mitigations: telemetry-off images, network-egress ACLs, air-gapped runs.
- **Judge-side memorisation.** The judge is an LLM that (a) processes every eval-set example as part of its normal invocation and (b) is later re-trained on production traffic that included the judge's own inputs. The eval-set enters the next judge's training corpus.
- **Log-based exfiltration.** Container-runtime logs, application logs, or ci-system logs capture eval-inputs; the logs land in a log-aggregator whose access policy is broader than the eval-set's.
- **Insider or overbroad access.** The eval-set is on a share whose ACLs include people or systems that are not authorised to see it. Insider misuse or credentials-leak is enough to move it out.

Each of these has a peer-owned mitigation. The release-assurance program's job is to make sure the mitigation is *contracted and verified*, not to invent it.

## The contract with `ai-infra-security`

The `ai-infra-security` peer owns MLSec depth. From the mod-102 chapter `06` evidence-contract shape, the release-assurance program contracts three artefact classes from this peer:

### Class A — Contamination attestation

For each release-cycle eval-set that discharges a hard release-gate criterion (mod-103 chapter `01`), the `ai-infra-security` peer produces a **contamination attestation** — a signed artefact that says: "as of release-candidate `rc-YYYY-MM-<hash>`, we have run the contamination-detection methodology described in `mlsec-contamination-methodology-vN.md` against dataset digest `sha256:9ff2…` and model digest `sha256:aa11…`, and the outcome is either (a) no contamination detected under thresholds T, or (b) contamination detected in exactly these examples, with the following mitigation."

What the attestation contains:

- The dataset digest and model digest under test.
- The methodology reference (peer-track-owned; the release-assurance program cites it but does not author it). Typical methodologies include *n-gram overlap* (Brown et al. and later refinements), *canary tokens* (Carlini-style unique markers seeded into eval-sets), *paraphrase detection*, *log-probability signature* checks (the model assigns anomalously high probability to eval-set continuations vs. a control), and — for public benchmarks — cross-checks against known-contamination catalogues (e.g., the `data-contamination` public tracking effort where it exists).
- The numeric result and its statistical warrant. Estimator, CI, threshold.
- The disposition. Either "no finding" or the finding-and-mitigation record: which examples are compromised, whether they can be re-authored, and whether the eval-set version has to be rotated.

The freshness of the attestation is per-release-candidate for high-tier releases and per-quarter for low-tier internal work. The attestation's digest lands in the reproducibility bundle at `data/security/contamination-attestation.json` and is signed as its own DSSE envelope.

### Class B — Exfiltration-control attestation

For each release-cycle where the eval-set is exercised through a hosted provider, an evaluator that has network egress, or a judge model that is external to the pipeline's compartment, the `ai-infra-security` peer produces an **exfiltration-control attestation** — a signed artefact that says: "the eval-set at digest `sha256:9ff2…` was exercised under exfiltration-control policy `mlsec-exfil-policy-vN.md`; the control set was in place at run time; audit-log lookups confirm no exfiltration event during the run window."

What the attestation contains:

- The eval-set digest.
- The exfiltration-control policy reference (peer-track-owned). Typical control classes:
  - **Provider-side data-retention controls.** Zero-data-retention endpoints (where offered), opt-out-from-training toggles, provider contractual clauses. The attestation records the provider identity, the endpoint URL, the data-retention posture at run time, and the contractual reference.
  - **Network-egress ACLs.** The evaluator container's network policy (Kubernetes NetworkPolicy, Envoy egress ACL, an on-prem firewall rule). The attestation records the policy digest and evidence that the policy was in effect during the eval run.
  - **Log-scrub / log-restrict.** The logging pipeline scrubs eval-inputs from persistent logs; the attestation records the scrubber's version and its scan results over the run window.
  - **Compartment isolation.** The eval runs in a compartment with its own credentials, its own network segment, and its own storage; the attestation records the compartment's identity.
  - **Judge-side controls.** If a hosted judge is used, the same provider-side controls apply; if the judge is internal, its training-data governance record is what the attestation cites.
- Run-window observability. Which time window the eval ran in; audit logs from the compartment; anomaly-detection results over that window.
- The disposition. Either "no exfiltration observed" or the observed finding + mitigation.

Freshness is per-release-candidate. Digest lands in the bundle at `data/security/exfiltration-attestation.json`.

### Class C — Supply-chain-security clauses

For each provenance attestation (chapter `04`), the `ai-infra-security` peer signs a **supply-chain-security clause** that binds the attestation to the peer track's own supply-chain-security policy:

- **Model-supply-chain clause.** "The model at digest `sha256:aa11…` has provenance conforming to peer supply-chain policy `mlsec-model-supply-vN.md`; the SLSA attestation, ML-BOM, SPDX-AI, safetensors, and ModelScan / picklescan artefacts satisfy the policy's Section §3 acceptance criteria."
- **Evaluator-supply-chain clause.** Same shape for the evaluator container image.
- **Judge-supply-chain clause.** Same shape for the judge model (or a documented deferral to the model-supply-chain clause when they are the same artefact).
- **Dataset-supply-chain clause.** For eval-sets acquired from outside the pipeline (public benchmarks, licensed datasets), the acquisition path, the licensing, and the integrity checks are attested. The clause records the peer's authorisation-of-acquisition step, so an auditor can trace back to the person who signed for pulling the dataset in.

The four clauses together are what the release-gate's `GATE-SUPPLY-*` criteria (chapter `04`) resolve to. Without the peer's signatures, the criteria are self-referential — the assurance program is attesting to its own supply-chain, which is not a check.

## Where the release-assurance program stops

The clean way to draw the boundary is: **the release-assurance program owns the interface into the peer track; the peer track owns the depth**.

Concretely, the release-assurance program:

- **Owns.** The evidence-contract row that names the artefact, its warrant, its freshness, and its escalation. The threading of that row's clauses into the assurance bundle. The release-gate criterion set that consumes the artefacts. The audit trail that runs from a market-surveillance query all the way to the peer's signature.
- **Does not own.** The methodology behind contamination detection. The compartment-design behind exfiltration controls. The threat model that decides which controls are load-bearing. The peer-track red-team and adversarial-eval methodology depth.

An assurance-program engineer who writes their own contamination-detection code without the peer's methodology behind it is out over their skis, and an assurance case that discharges MLSec claims to a leaf produced by the assurance program itself has zero diversity of evidence (mod-102 chapter `05`) on that branch.

## Public-benchmark contamination — the special case

Public benchmarks (MMLU, GSM8K, HumanEval, MATH, HELM tasks, LMSYS Chatbot Arena questions where applicable, MMLU-Pro, and their derivatives) are contaminated *by default* — enough of them are on the open web that any modern pretraining run has ingested some of them. Release-assurance programs relying on public-benchmark evidence need to name this in the assurance case:

- **The benchmark's contamination status is an assumption.** Mod-102 chapter `05`'s unstated-assumptions audit catches an assurance case that treats a public benchmark score as if the benchmark were fresh. The assumption has to be stated: "we are treating this public-benchmark score as evidence of *retention on a known set* rather than *generalisation to novel examples*, and the case's warrant reflects that."
- **Complement public-benchmark evidence with held-out evidence.** The release-gate never rests solely on a public-benchmark score for a hard criterion; the peer `model-evaluation-engineer` produces a held-out companion (a bespoke internal benchmark, a canary-marked private set, a versioned rotation of the public set that has been perturbed) whose contamination status is verifiable. The release-gate's hard-criterion warrant is on the companion; the public-benchmark score is corroborating soft evidence.
- **Refresh, don't reuse.** Held-out eval-sets are refreshed on a cadence tied to the eval-set exfiltration risk. If a set has been exercised through a provider that retains data, or if it has been shipped in a bundle that was later distributed under an agreement whose enforcement is weaker than the eval-set's confidentiality warrants, the peer track rotates the set. Rotation is documented; the old set's digest and the new set's digest are both in the store; the release-cycle's criterion set (mod-103 chapter `01`) is updated to reference the new digest.

## Canary tokens and detection

A cheap, well-attested contamination-detection technique is *canary tokens*: unique, high-entropy identifiers that are seeded into the eval-set at construction time. If the model, at inference, ever emits the canary in response to unrelated prompts, it has memorised the eval-set. Canaries are cheap for the peer to seed, cheap to test against a hosted model (one probe per canary), and defensible in an assurance case because their construction is verifiable.

The release-assurance program does not choose the canary methodology, but it *does* contract for the canary attestation. A typical row in the mod-102 chapter `06` evidence contract:

- **Claim:** "eval-set `harm-eval-set/v3.2` (`sha256:9ff2…`) has not been memorised by the release-candidate model."
- **Owner peer:** `ai-infra-security`.
- **Artefact:** canary-attestation.json signed with peer key, referencing methodology `mlsec-canary-methodology-v2.md`.
- **Warrant:** procedural — canary construction, seeding, and probe run; statistical — probe FAR/FRR reported.
- **Freshness:** per-release-candidate.
- **Escalation:** finding → peer + release-owner within 1 business day; rotate eval-set or defer release.

The canary attestation lands in the bundle at `data/security/canary-attestation.json`.

## Threading the clauses into the bundle

Pulling the whole layer together, the assurance bundle's `data/security/` directory typically looks like:

```
data/security/
├── contamination-attestation.json      # Class A
├── exfiltration-attestation.json       # Class B
├── supply-chain-clauses/               # Class C — one per artefact
│   ├── model.clause.json
│   ├── evaluator.clause.json
│   ├── judge.clause.json
│   └── dataset.clause.json
├── canary-attestation.json             # canary probe result
└── mlsec-methodology-refs/             # peer-owned methodology docs, cited by digest
    ├── contamination-methodology.md
    ├── exfil-policy.md
    └── canary-methodology.md
```

The bundle manifest (chapter `03`) references each of these under `security.*`, and the release-gate walker (mod-103 chapter `06`) cross-checks:

- Every clause's referenced artefact digest matches the reproducibility bundle's digest for the same artefact.
- Every clause is signed by the `ai-infra-security` peer's key (not by the release-assurance program's key — self-signing here is meaningless).
- Every referenced methodology is versioned and its version is one the mod-102 chapter `06` contract permits.
- Freshness across all four classes is within the release-gate's freshness policy.

Any failure escalates through the mod-102 chapter `06` path.

## The peer runbook interlock

Where the mod-102 chapter `06` freshness / cadence / escalation shape gets specific for MLSec:

- **Missing attestation.** The peer track's on-call is notified within the mod-102 chapter `06` window; if the attestation cannot be produced in time, the release either defers or promotes at a lower tier per mod-103 chapter `05`'s runbook. In no case does the release proceed to a tier where the missing attestation was a hard criterion.
- **Finding, resolved before release.** The peer's disposition and mitigation are recorded and the release proceeds with the mitigation on the record.
- **Finding, unresolved at release.** The release either defers, promotes at a lower tier without the affected criterion, or the release-owner accepts the residual — always with a written justification tied to the harm inventory (mod-102 chapter `06` risk-engineer branch). A hard-criterion finding accepted without a residual justification is an audit finding by construction.
- **Post-release finding.** Post-market surveillance (mod-110) catches a contamination or exfiltration signal after release. The reproduction bundle (chapter `03`) is what the peer runs on to establish whether the finding was already present at release; if so, the release-gate decision is retro-flagged and an incident-response loop opens.

## What the assurance case is arguing here

For every hard release-gate criterion whose warrant rests on an eval-set, the assurance case (mod-102) has a matching sub-argument that discharges to three MLSec leaves in parallel:

- Contamination-attestation leaf (Class A).
- Exfiltration-control leaf (Class B).
- Supply-chain-clause leaf (Class C).

Losing any of the three collapses the sub-argument; a case that only carries one of the three is arguing from one side. Diversity of evidence (mod-102 chapter `05`) is what makes the sub-argument survive.

The three leaves' digests, together with the primary eval evidence's digest, are what the market-surveillance authority under EU AI Act Article 74 receives when they ask for the accuracy / robustness / cybersecurity discharge (Article 15). Article 15(4) specifically calls out cybersecurity and resilience against adversarial manipulation — the exfiltration-control leaf is where the assurance program discharges the "resilience against exfiltration" cut of Article 15(4), *pointing at the peer's ownership*. The case does not backfill the peer's craft.

## Summary

- Eval-set contamination (data leaked *into* the model) and eval-set exfiltration (data leaked *out of* the pipeline) are peer-owned failure modes. `ai-infra-security` (peer, level 35) owns the depth; the release-assurance program owns the interface.
- The release-assurance program contracts three MLSec artefact classes: contamination attestation (Class A), exfiltration-control attestation (Class B), and supply-chain-security clauses (Class C — one per model / evaluator / judge / dataset).
- All three classes are signed by the peer's key, land in the bundle at `data/security/`, and are referenced by the manifest.
- Public benchmarks are contaminated by default; the assurance case states this as an assumption and complements public-benchmark scores with held-out companion evidence produced by the model-evaluation engineer.
- Canary tokens are a cheap, defensible detection technique; the peer produces canary attestations that land in the bundle.
- The release-gate walker cross-checks digest agreement between MLSec clauses and the reproducibility bundle, cross-checks signatures against the peer's key, and enforces freshness. Missing / stale / warrant-failing attestations escalate through the mod-102 chapter `06` path.
- The assurance case's MLSec sub-argument discharges to three leaves in parallel; losing any of the three collapses the sub-argument.
- Chapter `06` closes the module by signing the whole assurance bundle and mapping the release-gate output artefact into ISO/IEC 42001 clause 7.5 / 8 / 9 / 9.2 / 10 records.
