# Auditing an Assurance Case: Defeaters, Undermining Evidence, and Diversity

## Motivation

An assurance case earns its keep only if it can be *reviewed adversarially*. A case that no reviewer knows how to poke at is decorative; a case that a hostile-but-competent reviewer walked away from without shaking is defensible. This chapter is the audit companion to chapters `02`–`04`: given a submitted GSN or CAE case (persisted in SACM), what do you look for, in what order, and how do you record the findings so the case can be repaired without re-doing the audit next release cycle.

Two intellectual anchors carry the chapter.

- **Rushby's confidence-in-argument work.** [John Rushby's *The Interpretation and Evaluation of Assurance Cases*](https://www.csl.sri.com/users/rushby/papers/sri-csl-15-1-assurance-cases.pdf) frames an assurance case as an argument whose *epistemic* soundness is what a reviewer is checking. Read the paper once — it is short and cuts a lot of noise out of the field.
- **CAE Blocks + Defeaters** (chapter `03`). The pattern gives you a working prompt for each argument node: what defeaters would a reviewer raise here, what mitigates each, what residual remains.

The chapter proceeds in five audit passes, from the shallowest checks (structural) to the deepest (residual-risk acceptability).

## Pass 1 — Structural well-formedness

Before you can audit the *argument*, the case has to be structurally sound.

Walk the case (in whichever notation was submitted; a SACM persistence makes this a script) and check:

- **Every claim has a unique identifier and version.** Duplicate identifiers, missing versions, or floating claims not tied into the graph are structural failures.
- **Every argument node names its reasoning move.** GSN strategies without a rationale, CAE arguments without a block name (decomposition, substitution, concretion, calculation, evidence-incorporation), and SACM `ArgumentReasoning` elements with empty `content` all block audit.
- **Every leaf is discharged.** A leaf claim that has no evidence and no away-claim is either an unfinished branch or an unstated assumption. Both are structural failures — repair the branch or mark the leaf `assumed=true`.
- **Every context is `InContextOf` a specific node.** A context that lives only in a header slide has no scope in the graph.
- **Every away-claim resolves.** An away-goal in GSN or an away-claim in CAE must point to a module and a version that the reviewer can open. Broken references are structural failures.
- **Every artefact has an asset with a digest.** An evidence node with no version and no digest cannot survive the next release cycle's diff (chapter `04`).

Structural failures do not require judgement; they require repair before the argumentative audit begins. Do not let a structurally malformed case eat a session's audit budget.

## Pass 2 — Unstated assumptions

Every assurance case rests on premises the reviewer would like to see declared. The audit's job is to make the tacit explicit.

For each argument in the case, walk the CAE Blocks + Defeaters prompt: what would have to be true for this argument to hold? Compare the answer against the assumption nodes attached to the argument or claim. If the argument relies on a premise that is not among its assumption nodes, that premise is *unstated* and either needs an assumption node or needs to be discharged by a sub-claim.

Classes of unstated assumptions that show up in AI-release cases most often:

- **Representativeness assumptions.** The evaluation set is representative of production traffic; the calibration set is representative of the population the system will decide on; the red-team suite is representative of the adversary the system will face. Every one of these is load-bearing and every one is often unstated.
- **Independence assumptions.** The judge is independent of the model being judged; the test set is disjoint from the training corpus; the third-party evaluator is contractually independent of the deployer. Named at the point where the argument depends on them.
- **Stationarity assumptions.** Training-time properties still hold at inference-time; the data distribution has not shifted since the eval was run; the guardrail configuration has not changed since the eval was run.
- **Monotonicity assumptions.** A pass at a lower deployment tier implies a pass at a higher tier (this one is almost always *wrong* and must be flagged); a pass on a benchmark subset implies a pass on the full benchmark.
- **Threshold-derivation assumptions.** The threshold was chosen against a benchmark whose statistical warrant is documented elsewhere; the threshold's chosen level has a rationale that ties to the harm inventory.

Every unstated assumption you surface is either:

- **Repaired** — an assumption node is added at the argument or claim where it load-bears, with a rationale for why the case can rest on it; or
- **Escalated** — the case is *incorrect* to rest on this premise, and the argument has to be reshaped.

Both outcomes are audit *wins*. A case whose audit surfaced no unstated assumptions was probably not audited at depth.

## Pass 3 — Defeaters and mitigations

For every argument, apply the defeater / mitigation prompt.

A **defeater** is any proposition whose truth would invalidate the argument or the claim. Two flavours, from chapter `03`:

- **Rebutting** — the defeater directly contradicts the claim. "The eval set overlaps the training corpus, so accuracy is inflated" rebuts "the model is accurate."
- **Undercutting** — the defeater breaks the argument without contradicting the claim. "The bootstrap CI is computed under an IID assumption that pilot traffic violates" undercuts the *inference* from CI to fitness.

Every argument in the case should carry, at a minimum, the *serious* rebutting and undercutting defeaters and a documented mitigation for each. In an AI-release setting, the defeaters that show up most often are:

- **Evaluation-set contamination.** Test contamination, benchmark leakage, judge-in-the-training-data. Mitigation is disjointness verification and, for GenAI, a contamination-check technique documented in the model-eval evidence-contract (chapter `06`).
- **Judge failure.** LLM-as-judge disagrees with human raters at high stakes; judge biased toward the model under evaluation; judge stale versus the current system. Mitigation is judge-vs-human validation with a defined agreement metric, and periodic judge refresh.
- **Distribution shift between eval and production.** Pilot traffic mix ≠ production traffic mix; region A ≠ region B; time-t ≠ time-(t+3 months). Mitigation is stratified evaluation, ongoing monitoring (chapter `04`), or an explicit assumption declared at C1.
- **Threshold gaming.** Threshold chosen so the current release passes rather than because a harm-model or SLA demands it. Mitigation is documented threshold derivation, ideally traced to a harm inventory or a regulatory requirement.
- **Confounded metrics.** A metric that trades off two properties reported as a single number (a common failure mode with "safety score"). Mitigation is decomposition into the underlying properties.
- **Evaluator conflict of interest.** The party producing the evidence is the party under evaluation; the third-party evaluator has an ongoing commercial relationship with the deployer. Mitigation is independence attestation and, at higher deployment tiers, a genuinely independent evaluator (chapter `mod-109`).
- **Evidence age.** The evidence pre-dates the current release candidate; the red-team was run against a prior model version. Mitigation is evidence-freshness policy stated in the evidence-contract and enforced at release-gate.

For each defeater surfaced, record: the defeater, its flavour (rebutting / undercutting), the argument node it targets, the mitigation in place, and the residual. Residuals that cannot be mitigated in this release cycle either land as declared assumptions (chapter `03`) or block the release.

## Pass 4 — Diversity of evidence

A single kind of evidence — no matter how strong — is a weaker discharge than multiple kinds of evidence pointing the same direction. This is the assurance-case analogue of the [defence-in-depth](https://csrc.nist.gov/glossary/term/defense_in_depth) argument in security. Rushby calls this *epistemic diversity* in the confidence-in-argument work above.

For each leaf claim, ask whether the evidence is *diverse* along the axes that matter for the claim:

- **Methodological diversity.** Is the accuracy claim supported *only* by an offline benchmark, or also by an online-eval slice and a red-team probe? Is the fairness claim supported *only* by a summary metric, or also by a slice audit? A leaf leaning on one methodological base is a leaf with one point of failure.
- **Party diversity.** Is the evidence produced *only* by the model provider, or also by an internal risk engineer and, at higher tiers, an independent third-party evaluator? A single-party claim is weaker than a multi-party claim; regulators know this.
- **Temporal diversity.** Is the evidence a single-shot measurement, or a series across time (pre-training, post-training, post-fine-tune, in production)? A single-shot measurement is fragile against distribution shift.
- **Dataset diversity.** Is the evidence measured *only* on the calibration set, or on multiple sets whose construction differs? A single-set evaluation is weaker against selection bias.

Diversity is not a checklist item and there is no obligation-driven threshold; it is a *proportion* argument. Higher-stakes claims need more diversity. A T1 internal-pilot release can rest on a single methodology and party; a T3 external release cannot.

Record diversity gaps as *audit findings*, not as failures. The disposition is either "acceptable at this deployment tier" (with rationale) or "add evidence before promotion." The peer track that owed the evidence (chapter `06`) is the one asked to close the gap.

## Pass 5 — Residual-risk acceptability and confidence-in-argument

The last pass takes a step back from the argument and asks: given everything the earlier passes surfaced, does the reviewer *believe* the top-level claim?

This is where Rushby's confidence-in-argument framing carries the weight. The reviewer is estimating a *confidence* in the top-level claim conditional on:

- the argument's structure (does the reasoning move from evidence to top-level claim actually apply?),
- the evidence's quality (does each leaf's evidence discharge its leaf claim under scrutiny?),
- the residual defeaters (are the remaining defeaters small enough that a hostile-but-competent reviewer would accept them?),
- the assumptions (are the load-bearing premises credible?), and
- the diversity (does the whole case rest on one narrow base or on several converging ones?).

Two failure modes to record explicitly at this pass:

- **Cascading assumptions.** The case's top-level claim rests on a chain of assumptions each of which rests on the next. If the reviewer would not sign each assumption in isolation, the case cannot rest on their conjunction — this is the assurance-case analogue of the classical "chain of five 90%-confident links has 60% confidence." Rushby's paper cited above discusses this pathology at length.
- **Argument-evidence mismatch.** The evidence discharges *something*, but not the leaf claim under it. Common example: the eval report discharges "model accuracy on benchmark B" but the leaf claim reads "model accuracy on the in-scope production classes." The evidence supports a *neighbouring* claim, not the one it is attached to.

The output of this pass is a written *confidence rationale* the release-decision-maker signs alongside the case. The rationale names, at minimum: what confidence the reviewer has in the top-level claim; what specifically load-bears; what would move confidence up or down; what evidence would be needed to lift a low-confidence branch. A release-gate approver signing without a confidence rationale is signing a report, not a case.

## Recording the audit

Every finding across the five passes lands in an **audit ledger** attached to the case's SACM instance. Recommended minimum fields per finding:

| Field                | Content                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------ |
| Finding ID           | Stable identifier, unique within the case.                                                       |
| Pass                 | Structural / Unstated assumption / Defeater / Diversity / Residual-risk.                         |
| Target               | The SACM identifier of the claim, argument, or evidence node the finding targets.                |
| Statement            | One-sentence description of the issue.                                                           |
| Severity             | Blocking / Elevate / Note.                                                                       |
| Disposition          | Repair / Escalate / Accept-as-assumption / Accept-with-rationale.                                |
| Owner                | Party responsible for closing (release-owner, peer track producing the evidence, external body). |
| Deadline             | Date by which the disposition is due; typically before the release decision.                     |
| Confidence delta     | For pass 5 findings: how much this finding moves reviewer confidence in the top-level claim.     |

Every audit finding recorded this way persists into the next cycle. If the case is diff-able (chapter `04`) and the audit ledger is persisted alongside, the *next* audit inherits the closed-findings list and only re-opens what changed.

## Common failure modes an audit surfaces

Compact list you can turn into a checklist for your own reviews:

- Solutions are named categories, not identified artefacts.
- Assumptions are stated in prose but not attached as nodes.
- Sub-claims re-word the parent claim without adding information.
- Threshold rationales resolve to "chosen to match the previous release's threshold."
- Judge or evaluator is the same party as the entity being judged.
- Evidence's date pre-dates the current release candidate.
- CI methodology is unstated ("95% CI" with no estimator named).
- A claim is discharged by a benchmark whose leakage / contamination status is unclear.
- An away-goal points to a module that no longer exists at the referenced version.
- The top-level claim carries no date or deployment-tier scope.

Every one of these is common in practice. Every one is repairable if the case is versioned in SACM and the audit ledger persists.

## Summary

- Audit an assurance case in five passes: structural well-formedness → unstated assumptions → defeaters and mitigations → diversity of evidence → residual-risk acceptability and confidence-in-argument.
- The CAE Blocks + Defeaters pattern (chapter `03`) is the working prompt for the defeater pass; Rushby's confidence-in-argument work is the frame for the residual pass.
- Every finding lands in an audit ledger with a SACM-linked target, severity, disposition, owner, and confidence delta.
- Diversity of evidence (method, party, time, dataset) is a proportion argument scaled to deployment tier — not a checklist.
- The release-decision-maker signs a written *confidence rationale* alongside the case; signing without one collapses the case back into a report.
- Chapter `06` closes the loop by formalising the evidence contract to the peer tracks that produce each leaf's evidence.
