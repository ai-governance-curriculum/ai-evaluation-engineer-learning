# Evidence Contracts and Routing Claim-Branches to Peer Tracks

## Motivation

An assurance case does not produce its own evidence. Every leaf claim discharges to an artefact produced by a peer track — the AI-governance analyst, the risk engineer, the AI-eval engineer, the model-evaluation engineer, the MLSec peer, the third-party evaluator — and the release-assurance program's job is to *own the interface* into each of those parties, not to backfill their craft (chapter `01`, and mod-101's deferral contract).

This chapter closes the module by making the interface explicit: for each claim-branch in the case, name the owner peer track, write down what artefact is owed (name, version, format, storage), what statistical or procedural warrant the artefact must carry, and how the artefact's freshness is enforced. The persisted form of these interfaces is the **evidence contract** — one row per leaf claim in the case, one signed contract per peer.

An evidence contract is not paperwork. It is what makes the assurance case *diff-able across cycles* (chapter `04`), *auditable at leaves* (chapter `05`), and *survivable* when a peer track re-scopes or changes its methodology. Without a contract, every release cycle re-negotiates every leaf from scratch and the case cannot hold altitude.

## What an evidence contract contains

For each leaf claim in the case, the contract row names:

| Field                     | Content                                                                                                                            |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Claim identifier          | The SACM `Claim.id` in the case the contract discharges.                                                                            |
| Owner peer track          | The role that owns producing the artefact (analyst L15 / risk engineer L25 / AI-eval L30 / model-eval L30 / MLSec L35 / third-party). |
| Artefact                  | The named, versioned artefact (e.g., "signed eval report v1.0.0", "red-team engagement report v2", "harm inventory v3").             |
| Format and storage        | The file or registry format and the storage location (artefact registry URL, digest scheme, retention).                             |
| Warrant                   | The statistical or procedural warrant the artefact must carry (e.g., "95% bootstrap CI per-class F1"; "sign-off by risk-lead + peer-review"). |
| Freshness policy          | The maximum age of the artefact acceptable at release-gate (e.g., "≤ 30 days from decision date").                                  |
| Cadence                   | How often the artefact is regenerated (per-release, per-quarter, on-fine-tune, on-config-change).                                    |
| Sign-off party            | The named role who signs the artefact (typically the peer track's lead).                                                            |
| Framework citations       | The applicable NIST AI RMF sub-category, ISO/IEC 42001 clause, EU AI Act article, sector rule, etc.                                  |
| Escalation                | What the release-gate does if the artefact is missing, stale, or fails its warrant.                                                 |

The contract row is what the SACM `Artifact` element in chapter `04` persists (the `participants`, `events`, and `techniques` attributes are the contract's warrant, cadence, and sign-off recorded on the evidence side).

## Routing by owner track

The dominant question the contract answers is: *which peer track owes this evidence?* The routing is deterministic in most cases, but a few branches are contested and worth walking explicitly.

### To the AI-governance analyst (level 15)

The analyst owns intake, inventory, first-draft framework crosswalks, first-draft cards, and jurisdictional tracking (see mod-101 and the `ai-governance-analyst-learning` prerequisite). Leaves the assurance case routes to the analyst include:

- Inventory-linkage claims: "the system-under-release is registered in the AI inventory at row X."
- Jurisdictional-scope claims: "the applicable jurisdictions and their release-gate obligations are as identified in the current watchlist."
- First-draft card claims: "an initial model / system / dataset card was drafted per the analyst template and lives at storage-ref Y."

None of the analyst leaves are load-bearing on statistical warrants; they are *procedural* warrants. Warrant is "signed by analyst lead, dated ≤ 30 days from release decision, versioned." The release-assurance program then *elevates* these first-draft artefacts into the release-facing cards owned by mod-105.

### To the risk engineer (level 25)

The risk engineer owns harm modelling, LLM / adversarial-ML red-teaming, guardrail engineering, and AI-specific incident response. Leaves that route to the risk engineer:

- Harm-inventory claims: "the harms considered for this release are enumerated in harm-inventory v3, tied to jurisdictional obligations."
- Adversarial-evaluation claims: "the red-team suite covers the harm categories in scope for this deployment tier; findings and mitigations are in red-team-report v2."
- Guardrail-effectiveness claims: "the guardrail configuration in production discharges the residual-risk from harm-inventory v3; guardrail-eval-report v1 is signed."
- Incident-learning claims: "learnings from post-market incidents attributable to this system are incorporated in the current harm inventory."

Warrants here are a mix: harm inventories carry procedural warrant (signed by risk-lead + peer review), adversarial evaluations carry both procedural and statistical warrant (coverage against a documented threat model + attack success rate estimates with stated CIs). The specific statistical warrant lives in the risk-engineer track's methodology, not in the release-assurance program.

### To the AI-eval engineer (level 30, AI Engineering family)

The AI-eval engineer owns application-layer evaluation engineering: trace / trajectory / RAG / judge / online-eval / eval-gated CI/CD / eval-data-platform slice. Leaves that route here:

- Trace / instrumentation claims: "production traces from the pilot window are captured in the eval-data-platform per OpenTelemetry Gen-AI conventions, and are queryable by the release-gate reviewer."
- Trajectory / tool-call claims: "trajectory correctness on the tool-using tasks is measured at rate X on the online-eval slice."
- RAG grounding claims: "retrieved-context relevance and answer groundedness meet threshold Y on the calibration RAG set."
- Judge claims: "the LLM-as-judge in scope carries a documented judge-vs-human agreement rate; agreement is above threshold Z."
- Eval-gated CI/CD claims: "the release candidate passes the eval-gated CI/CD gates configured for tier T2."

Warrants here are the peer track's methodology. The evidence-contract row does *not* re-derive the methodology — it cites the AI-eval evidence-contract v1 (the peer track owns the contract's warrant clauses) and asserts the artefact conforms.

### To the model-evaluation engineer (level 30, ML Engineering family)

The model-evaluation engineer owns methodological depth: validity theory, bootstrap CIs, benchmark construction, calibration methodology, cross-modality harnesses, MLPerf-style methodology. Leaves that route here:

- Property-benchmark claims: "the model's performance on benchmark B for the properties in scope meets the release-gate threshold, within a documented CI computed by a documented estimator, on a benchmark whose construction is documented."
- Calibration claims: "predicted-probability calibration on the calibration set is measured under Brier score (or ECE, per the peer track's technique) and meets the threshold."
- Benchmark-integrity claims: "the benchmark used to discharge this property is not contaminated by the training corpus; disjointness is verified by the peer track."
- Cross-modality claims (if applicable): "the multimodal evaluation harness discharges the multimodal properties in scope."

The warrant is *always* statistical and *always* named. The release-assurance program does not choose the estimator; the model-evaluation engineer does. What the release-assurance program does is (a) verify that an estimator is named, (b) verify that the estimator's assumptions are declared, and (c) record the whole thing in the SACM `Technique` element.

### To the MLSec / infra-security peer (level 35)

The MLSec peer owns eval-set integrity, judge supply-chain security, adversarial-eval depth, model-extraction controls at platform scale, and general product security around the AI system. Leaves that route here:

- Eval-set exfiltration control claims: "the calibration set has not leaked to the model provider; exfiltration controls are in place per MLSec policy X."
- Judge-supply-chain claims: "the LLM-as-judge configuration and its underlying model are pinned by digest; provenance is per MLSec supply-chain policy."
- Adversarial-eval depth claims: "the adversarial evaluation covers threat model T with rigor consistent with the MLSec depth policy."
- Cybersecurity posture claims (EU AI Act Article 15(4)): "the system's cybersecurity posture is documented and discharges Article 15(4)"; typically this is a full away-claim to the SEC assurance case.

The warrant is procedural (policy conformance) plus artefact integrity (digest chains, signatures, provenance).

### To third-party evaluators (external, mod-109 coverage)

For higher deployment tiers or specific frameworks (GPAI systemic-risk under EU AI Act Article 55, RSP / Preparedness / FSF deployment tiers with independent-evaluator requirements), the leaf's evidence is produced by a third party — an AISI-shape evaluator, a notified body under EU AI Act Article 43, a Big-Four assurance firm, or an independent audit body. Leaves routed to third parties:

- Independent-evaluation claims at deployment tiers T3+.
- Notified-body conformity-assessment claims for EU AI Act Article 43 (Annex VI / Annex VII).
- Independent-audit claims for GPAI systemic-risk (Article 55) and sector-specific rules (SR 11-7 independent-validation expectation).
- Post-market surveillance evidence produced by third-party monitors (mod-110).

The contract to a third party is contractual in the legal sense as well as in the assurance-case sense. Deep coverage of the interface lives in mod-109; this module treats the third-party leaf as a special case of the routing pattern above.

## When routing is contested — the disambiguation rules

Three branches show up as contested often enough to be worth naming.

### "Fairness" evidence

Fairness is craft-owned by the risk engineer (bias / fairness engineering is inside their remit) but methodologically checked by the model-evaluation engineer (the estimator behind the fairness metric is theirs). The assurance case sub-branch typically has two leaves in parallel: one leaf discharged by risk-engineering evidence (harm-inventory row for a fairness harm; guardrail-eval-report reduced-harm measurement), the other by model-eval evidence (subgroup metric with a CI). Do *not* collapse them; the two peer tracks own different pieces.

### "Judge quality" evidence

Judge quality has two owners: the AI-eval engineer runs the judge inside the product pipeline and reports agreement; the model-evaluation engineer methodologises the judge-vs-human agreement estimator. Contract the AI-eval engineer for the artefact (judge-agreement report v1), and contract the model-evaluation engineer for the methodology the AI-eval artefact must conform to. Two rows, not one.

### "Threshold" derivation

Thresholds are almost always contested. Rule: the threshold's *value* is chosen by the release-assurance program (i.e., you) with input from the risk-engineer's harm inventory (what harm the threshold is protecting against) and the model-evaluation engineer's methodology (what statistical warrant the threshold's estimator carries). Contract the risk engineer for the harm-inventory tie-in; contract the model-evaluation engineer for the estimator; own the threshold value yourself with a written derivation traced to both. If the threshold's derivation is not traceable, the case's residual-risk pass (chapter `05`) will surface it as an unstated assumption.

## Freshness and cadence

An evidence contract is worth little if it does not say when the artefact goes stale. Three cadence patterns show up:

- **Per-release-candidate.** Regenerate the artefact for every release candidate. Common for eval reports, red-team reports on the current model, and judge-agreement reports whenever the judge is refreshed.
- **Per-quarter or per-interval.** Regenerate on a calendar cadence. Common for harm inventories (which do not shift as fast as models), for procedural artefacts (analyst-tier inventory linkage), and for platform-level MLSec attestations.
- **On-event.** Regenerate whenever a triggering event happens. Common for guardrail-eval reports (regenerate on guardrail config change), for judge reports (on judge change), for red-team reports (on fine-tune), and for incident-derived learnings (on post-market incident closure).

The contract must name the cadence and the release-gate must enforce it. A helpful pattern in the SACM instance (chapter `04`) is to attach a `freshness` metadata annotation to each `Artifact` with `maxAgeDays`, `regenerationTrigger`, and `lastVerifiedAt` — the release-gate walker then rejects the case if any leaf's evidence has an expired freshness.

## Escalation

For each contract row, an **escalation path** must be defined for the three failure modes:

- **Missing.** The artefact does not exist at release-gate time.
- **Stale.** The artefact exists but exceeds its freshness policy.
- **Warrant-failing.** The artefact exists and is fresh but does not meet the contracted warrant (e.g., CI is wider than the contract permits, sign-off party is missing, technique is not the contracted one).

Escalations do not go to the release-decision-maker in the first instance. They go to the peer track's lead, with a deadline. If the peer track cannot close the gap in time, the second-order escalation lands on the release-decision-maker with a documented residual and a proposed disposition (defer release, promote at lower tier, promote with rationale for accepting residual, etc.). The escalation matrix itself lives in mod-101's deferral contract and in the assurance program charter (mod-112); this module makes the per-leaf contract *point* to it.

## The contract as a governed artefact

The evidence contract is not free-form email. It is a governed artefact:

- **Owned by** the release-assurance program (i.e., you) — you write the contract, negotiate it with the peer track, and revise it as methodologies evolve.
- **Signed by** the peer track's lead and the release-assurance program lead — a contract with no signature is aspirational.
- **Versioned** — the contract has a version number, and the SACM `Artifact` elements cite the contract version they were produced under. This is what lets a release-cycle diff (chapter `04`) attribute an evidence change to a contract change vs. a data change.
- **Reviewed on a cadence** — at minimum annually, and whenever a peer track significantly updates its methodology, whenever a framework materially changes (e.g., EU AI Act GPAI Code of Practice revision), and whenever an audit finding (chapter `05`) targets an evidence-contract clause.

Store the contract set in the same repository as the case (Git-tracked, tagged). Each contract's version is referenced by the SACM `Artifact` elements it governs. The full evidence-contract repository is a program-level artefact worth showing to a regulator or auditor on its own — it demonstrates that the release-assurance program owns its interfaces and does not backfill peer craft.

## A worked contract row

Take the `C1.1.15.a` claim from chapters `02`–`04` (per-class F1 ≥ 0.85 on the calibration set with a 95% bootstrap CI). Its evidence-contract row:

```
Claim              : C1.1.15.a
Owner peer         : model-evaluation-engineer (level 30, ML Engineering)
Artefact           : eval-report v1.x for release candidate rc-YYYY-MM-<hash>
Format / storage   : signed PDF + machine-readable JSON summary
                     stored in artefact-registry://mod-eval/eval-report/
                     addressed by sha-256 digest, 7-year retention
Warrant            : per-class F1 with 95% bootstrap CI per
                     MOD-EVAL evidence-contract v1 §4;
                     training-set / eval-set disjointness verified
                     per MOD-EVAL evidence-contract v1 §5
Freshness          : ≤ 14 days from release-decision date
Cadence            : per-release-candidate
Sign-off party     : model-evaluation-engineer lead
Framework citations: EU AI Act Article 15(1)(a) accuracy; NIST AI RMF
                     MEASURE-2.5 (evaluation involving external sources);
                     ISO/IEC 42001 clause 8.3
Escalation         : missing → risk-engineer lead + release-owner within
                     2 business days;
                     stale → regenerate against current rc-hash within
                     5 business days or defer release;
                     warrant-failing → escalate to release-owner with
                     residual defeater documented
```

Read the row as: it is what the SACM `Artifact` element persists on the evidence side; it is what the audit ledger (chapter `05`) checks in the leaf-diversity pass and the residual-risk pass; and it is what the next release cycle diffs against.

## Summary

- An evidence contract is the persisted interface between the release-assurance case and the peer track that produces each leaf's evidence.
- One row per leaf claim: claim identifier, owner peer track, named-and-versioned artefact, format / storage, statistical or procedural warrant, freshness policy, cadence, sign-off party, framework citations, escalation.
- Routing follows the deferral contract in mod-101: analyst L15, risk engineer L25, AI-eval L30, model-eval L30, MLSec L35, third-party evaluator (mod-109). Contested branches (fairness, judge quality, threshold) fan across two peers, not one.
- Freshness and cadence are enforced at the release-gate; missing / stale / warrant-failing artefacts have a defined escalation.
- The contract set is a governed, signed, versioned, cited-by-SACM artefact — a program-level deliverable, not paperwork.
- With chapters `01`–`05` you have the notation and audit; this chapter closes the loop between the assurance case and the peer tracks that keep it fed.
