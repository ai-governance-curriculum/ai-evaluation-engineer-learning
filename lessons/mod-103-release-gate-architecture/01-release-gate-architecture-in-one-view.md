# The Release-Gate, In One View

## Motivation

A release-gate is not a checkbox. It is a *standing procedure* that turns evaluation evidence into a defensible decision to promote a candidate to a stated deployment surface, and to write down what happens if that decision has to be reversed. The assurance case (mod-102) is the argument the gate consumes; the evidence pipeline (mod-104) is where the argument's leaves live; the cards, obligation crosswalks, and post-market loop (mod-105–mod-110) are downstream artefacts the gate emits. This module owns the gate itself.

Two failure modes motivate the shape.

The first is **soft-collapse**: every criterion is aspirational, all failures are "advisory," and the gate becomes a ceremony that never blocks a release. Regulators and internal-audit read this as an unfired control and treat the whole program as ornamental. NIST AI RMF's MANAGE function is not discharged by an unfired gate.

The second is **hard-brittle**: the gate is defined at one deployment surface (say, an internal pilot), pass criteria are decided after the run, and every real production incident is retrofitted into a new criterion. There is no rollback contract, so any regression triggers a scramble, and the assurance case cannot be reconstructed after the fact. EU AI Act post-market monitoring (Article 72) cannot attach to this shape, and ISO/IEC 42001 clause 8 auditors will read documentation-after-the-fact as absent.

The rest of this chapter draws the standing shape that avoids both.

## What a release-gate *is*

Concretely, one release-gate is a tuple of six elements:

1. **A scope** — the AI system-under-release, the model version, the config, the deployment surface, and the deployment tier.
2. **A pre-registered decision criterion set** — every criterion is written down before the run, marked hard or soft, with an explicit pass threshold, an evidence pointer, and a framework citation.
3. **An evidence bundle** — the immutable set of artefacts produced by the peer tracks (chapter `04`), pinned by digest and versioned. The assurance case (mod-102) is the argument; the bundle is what the argument's leaves resolve to.
4. **A decision record** — the go / no-go / defer / promote-at-lower-tier disposition, with signers named per RACI, timestamps, and a written rationale that cites the criteria that passed and those that were waived.
5. **A rollback / rollforward contract** — the pre-committed triggers, the pre-tested procedure, and the RTO (recovery-time objective) for reversing the promotion.
6. **A post-market handoff** — the online-eval slice, incident-detection thresholds, and the review cadence the gate hands to mod-110.

None of the six is optional. A "release-gate" missing any one of them is either a checklist (missing 2 or 5), a report (missing 4), or a ceremony (missing all six).

## Hard gates vs. soft gates

The single-most-important design decision in a gate is *which criteria are hard*.

A **hard gate** blocks the release. Its threshold is pre-registered, its evidence is auditable at the leaf, and there is no informal path around it. The only path around a hard-gate failure is a formal, signed **exception approval** (chapter `05`) with a written residual and a bounded expiry. Exception approvals are rare, tracked, and reviewed by the second line.

A **soft gate** is measured, recorded, and required to be *dispositioned* — but does not by itself block. Soft-gate failures are flagged in the decision record, tied to a corrective action, and re-examined at the next gate. Soft is not "advisory" — soft is "reviewed, dispositioned, tracked." An untracked soft-gate failure is a program defect.

Roughly the split is:

- **Hard.** Criteria tied to a statute the program has to discharge (EU AI Act Articles 9–15 obligations, sector rules like SR 11-7 independent-validation for the highest-risk models, FDA GMLP principles for regulated medical devices). Criteria tied to a *contractual* obligation to a deployer or a regulator. Criteria tied to a *safety* threshold whose exceedance would trigger post-market notification (Article 73) or an equivalent obligation. Criteria whose failure would cause an incident type the program has already committed to preventing (mod-110 loop).
- **Soft.** Criteria tied to internal quality goals that improve the product but do not by themselves discharge a statute (functional-adequacy targets above the hard-floor, transparency polish, adaptability metrics used for internal tracking). Criteria whose failure indicates a *trend* rather than a *breach*.

The taxonomy is not automatic. Every gate design has to argue, criterion by criterion, why a criterion is hard or soft, citing the framework or the harm inventory that fixes the answer. This *pre-registration* — the criterion, the threshold, and the hard/soft classification — is written down *before* the release candidate is evaluated. Choosing the threshold after the run to make the candidate pass is the release-gate equivalent of p-hacking, and is an audit finding.

## Pre-registered pass criteria

Every criterion in the gate has five fields:

| Field                 | Content                                                                                                                       |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Criterion identifier  | A stable ID the assurance case (mod-102) claim references, e.g. `GATE-FA-01` for "functional-adequacy criterion 01."           |
| Threshold             | The pass level as a number *and* the estimator. "Per-class F1 ≥ 0.85 (95% bootstrap CI lower-bound ≥ 0.83) on calibration-set v3." |
| Hard / soft           | With a one-line justification citing the statute, harm-inventory row, or internal-goal that fixes the classification.          |
| Evidence pointer      | Which peer track owns the artefact (chapter `04`), and the SACM `Artifact` ID the gate walker resolves.                       |
| Framework citation    | ISO/IEC 25059 quality dimension (chapter `02`), NIST AI RMF MEASURE sub-category, EU AI Act article, ISO/IEC 42001 clause.     |

The criterion set is versioned as a whole. `gate-criteria-vN.md` lands in the same repo as the assurance case, tagged before the release candidate is exercised. A gate walker (tooling, or a checklist for the low-tier case) reads `gate-criteria-vN.md`, resolves each evidence pointer against the bundle, evaluates the threshold, and produces the decision record.

Pre-registration matters because it is what makes the gate *falsifiable*. Without it, "the gate passed" is a claim with no counterfactual.

## Rollback and rollforward hooks

Every promotion carries a *reversal contract*. Two components:

- **Rollback.** The pre-tested procedure to revert to the previous known-good version if a trigger fires. The gate records: the previous version's digest, the reversal procedure (config swap, model-swap, feature-flag flip, traffic-shift back to canary-0), the tested RTO, and the signer authorised to invoke it. Rollback triggers themselves are written into the runbook (chapter `05`).
- **Rollforward.** The pre-committed path to a *fix-forward* — a small patch that addresses the trigger without reverting the whole promotion. Rollforward is not a substitute for rollback; it is a second option the on-call has when rollback would itself be disruptive (long-running sessions, cached state, side-effects on downstream systems). The gate names: which classes of trigger admit rollforward, the maximum time-to-patch, and the recorder who audits post-hoc.

A gate without both hooks is not a gate; it is a release announcement. Both hooks are tested at least once per quarter against the actual production surface — an untested rollback is a rollback that will not work. Testing the rollback (a "reverse drill") is a documented event under ISO/IEC 42001 clause 8.

## Deployment-surface-specific gate variants

The same system-under-release passes through multiple deployment surfaces during its life: internal-only pilot, canary to a limited user population, staged rollout to a broader population, full production, on-prem embedded copy at a deployer's site. Each surface has its own *risk profile*, its own *evidence-availability profile*, and its own *reversibility profile*. So the gate variant differs.

A typical taxonomy:

- **T0 — internal-only pilot.** Limited to signed-off internal users; no external effect. Gate is thin: only the safety-floor criteria are hard; functional and transparency criteria are soft. Reversibility is trivial (flip access off).
- **T1 — restricted external canary.** Small external population, opt-in, with monitoring on. Adds hard gates on safety metrics measured on the canary population, on transparency criteria required by the deployer contract, and on incident-detection thresholds. Reversibility is high (feature-flag flip).
- **T2 — staged rollout to majority production.** Adds hard gates on robustness, on statistical-warrant criteria from the model-eval track (bootstrap CI on the primary benchmark(s)), and on cross-jurisdictional obligations that trigger at production scope (EU AI Act deployer obligations, sector rules). Reversibility is medium (traffic-shift back; may involve cached state).
- **T3 — full production, all populations.** All criteria hard. Adds gates on independent-evaluator evidence, third-party sign-off, and post-market surveillance readiness (mod-110). Reversibility is medium-to-low.
- **T4 — regulated-sector deployment or on-prem at a deployer.** Adds gates on sector-rule evidence (SR 11-7 independent validation, FDA GMLP, DORA operational-resilience). Adds gates on the notified-body relationship (mod-109). Reversibility is often only via *deployer-side* action, so the gate has to include a deployer-notification contract (Article 26).

The T taxonomy is not the only one, and the *exact* levels a program uses will be shaped by its own deployment tiering (mod-108). What matters is that the gate variants are named, that the *delta* between them is written down criterion-by-criterion, and that a candidate cannot skip a tier without a signed exception. Deployment-tiered gating shows up again in mod-108 with the deeper safety-frontier framing (RSP, Preparedness, FSF); this module gives the general shape.

## Where the gate sits relative to the rest of the program

Draw one picture. Inputs into the gate on the left; outputs on the right.

```
                     ┌───────────────────────────────────┐
   ai-eval-engineer  ─▶│ Trace / trajectory / RAG /       │
   (level 30)          │ judge / online-eval evidence      │
                       │                                   │
   model-evaluation   ─▶│ Statistical-warrant, benchmark,  │
   -engineer (L30)      │ calibration evidence              │
                                                            │
   ai-risk-engineer   ─▶│ Harm inventory, adversarial /    │
   (level 25)           │ red-team, guardrail-eval evidence │
                                                            │
   ai-infra-security  ─▶│ Eval-set integrity, judge         │
   (level 35)           │ supply-chain, cybersecurity       │
                                                            │──┐
   analyst-produced   ─▶│ Inventory, jurisdictional         │  │
   inputs (level 15)    │ crosswalks, first-draft cards     │  │
                                                            │  │
                       └───────────────┬───────────────────┘  │
                                       │                       │
                       ┌───────────────▼───────────────────┐   │
                       │   RELEASE-GATE — criteria vN       │   │
                       │   walker + decision record         │   │
                       └───────────────┬───────────────────┘   │
                                       │                       │
       ┌───────────────┬───────────────┼───────────────┬──────┘
       ▼               ▼               ▼               ▼
   Assurance      Rollback /       External       Post-market
   case update    rollforward      cards          surveillance
   (mod-102)      contract         (mod-105)      handoff
                  (this module)                   (mod-110)
```

The gate is the join point. On the left are the peer tracks that produce evidence; on the right are the artefacts the assurance program owns. The gate is what turns the left into the right.

## What the on-call assurance engineer actually does

On the day of a release, the on-call reads a dashboard (chapter `06`) that surfaces the gate's state at a glance: which criteria are pre-registered, which have fresh evidence attached, which are trending, and which have opened issues that would trip the runbook (chapter `05`). Then the on-call walks the gate, records the disposition, and signs — with the second-line's effective-challenge convention observed (chapter `05`). The on-call is not the release-decision-maker; the on-call is the signer for the *assurance* half of the release, in a role RACI that has the release-owner accountable elsewhere.

Everything else in this module fleshes out that day-of-release loop:

- Chapter `02` — how the rubric that produces the criteria is structured around ISO/IEC 25059 quality dimensions and cross-mapped to NIST AI RMF MEASURE sub-categories.
- Chapter `03` — how the gate's outputs feed ISO/IEC 42001 clauses 8 (operation) and 9 (performance evaluation), so that the AIMS auditor sees the trail.
- Chapter `04` — the consumer-side of the peer-track evidence contracts introduced in mod-102 chapter `06`, made specific to what a gate consumes.
- Chapter `05` — the runbook the on-call keeps at hand.
- Chapter `06` — the dashboard the on-call reads.

## Summary

- A release-gate is a six-part standing procedure: scope, pre-registered criteria, evidence bundle, decision record, rollback/rollforward contract, post-market handoff.
- Criteria are marked hard or soft *before* the run; hard criteria block, soft criteria are dispositioned and tracked. Choosing the threshold after the run is an audit finding.
- Every promotion carries a tested rollback and a named rollforward path; reverse-drills are documented events under ISO/IEC 42001 clause 8.
- Gate variants are surface-specific (T0 pilot → T4 regulated on-prem); criterion deltas between variants are written down; skipping a tier requires an exception approval.
- The gate consumes evidence from four peer tracks and the analyst; it emits decision records, rollback contracts, external cards, and the post-market handoff.
- The next chapters build the rubric (`02`), map into the AIMS (`03`), specify the peer contracts (`04`), draft the runbook (`05`), and design the dashboard (`06`).
