# GSN for AI Release Decisions

## Motivation

GSN is the notation you will draw on the whiteboard when a release-gate meeting stalls. It fits a graphical medium, it is easy for reviewers to walk without reading prose, and every node is typed — so a reviewer can point at a specific goal, strategy, solution, context, or assumption and either accept it or open a hole. This chapter installs the notation, works through a concrete AI-release example, and pins down the failure modes that make a GSN case indefensible.

The reference standard is the [GSN Community Standard v3](https://scsc.uk/gsn), published by the [Safety-Critical Systems Club](https://scsc.uk/). Read the standard alongside this chapter; the standard is short, precise, and the source of truth for node shapes and link semantics.

## The seven core node types

GSN diagrams are directed graphs with typed nodes. The seven core types you must fluently draw and read are:

| Type          | Shape (per GSN v3) | Semantics                                                                                                                        |
| ------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| Goal          | Rectangle          | A claim about the system. Typically starts with "The system…" or "Release X…".                                                   |
| Strategy      | Parallelogram      | How a goal is decomposed into sub-goals. Names the argument, not the sub-goals.                                                  |
| Solution      | Circle             | Evidence discharging a leaf goal (e.g., an eval run, a red-team report, a signed model card).                                    |
| Context       | Rounded rectangle  | A definition or scope statement bound to a goal or strategy (e.g., "deployment tier: enterprise-internal, US + EU jurisdiction"). |
| Assumption    | Ellipse tagged `A` | Unproven premise made explicit (e.g., "the calibration set is representative of production traffic").                             |
| Justification | Ellipse tagged `J` | Rationale for the choice of strategy (e.g., "argument by discharge of each Article 15 requirement is chosen because…").          |
| Away-goal     | Rectangle with module identifier | Reference to a goal proven in another module or case — the target case is cited, not re-argued.                        |

Two link types connect them:

- **`SupportedBy`** (solid arrow) — inferential; used from Goal→Strategy→Goal→Solution, and from Goal→Away-goal.
- **`InContextOf`** (open arrow) — contextual; used to attach Context, Assumption, or Justification to a Goal or Strategy.

## Reading direction

By convention, top-level goals sit at the top of the page and evidence at the bottom. A GSN reviewer walks *downward* from the top-level goal, checking at each strategy that the sub-goals decompose the parent, and at each leaf that the solution discharges the goal. A reviewer also walks *sideways* into every `InContextOf` node, because a claim only holds inside its declared context — a goal removed from its context is meaningless.

## The GSN modularity extensions

GSN v3 formalises modular structure for large cases:

- **Module** — a self-contained sub-case with declared public interface (which goals are exposed, which are private).
- **Away-goal / Away-context / Away-solution** — references pointing to nodes owned by another module. This is how you avoid re-arguing the same claim in multiple release cases.
- **Contract** — the interface node describing what one module owes another. In an AI release, contracts are the fingerprints of chapter `06`'s evidence contracts.

For an AI-release program with several products, you will not build one enormous case. You will build one **release-gate case per product** whose leaf goals point via away-goal to reusable modules (a **safety-property module** per property, an **evaluation-methodology module** per methodology, a **jurisdiction module** per jurisdiction). Deep coverage of that pattern is in chapter `06`; this chapter names it so you can see it in the worked example.

## A worked release-case in GSN

We will walk through a small but realistic release-case for a fictional but concrete AI system.

**System.** `Aurelia-v3.2`, a document-triage assistant used inside a US-and-EU multinational bank to route incoming customer-service correspondence to the correct downstream workflow. Uses a fine-tuned foundation model with retrieval; runs on the bank's internal platform. The bank is a *deployer* under the EU AI Act (Article 26) and also a *provider* of the fine-tuned derivative into its own operations (Article 25). The system is high-risk per Annex III paragraph 5(b) (creditworthiness / financial services). SR 11-7 model-risk-management applies.

**Release decision.** Promote from limited pilot (200 users, US only) to production (all users, US + EU) at deployment tier `T2`.

### Top-level goal and its context

```
+-------------------------------------------------------------+
| G1 — The Aurelia-v3.2 T2 release discharges the applicable  |
| release-gate obligations, on the evidence available at      |
| time-of-decision (2026-07-10).                              |
+-------------------------------------------------------------+
             |                       |
    InContextOf              InContextOf
             v                       v
+-----------------------+   +-----------------------+
| C1 — Deployment tier: |   | C2 — Jurisdictions:   |
| T2 (US + EU, all users)|   | US (SR 11-7), EU     |
| Product owner: X       |   | (EU AI Act Annex III |
| Release RC: rc-2026-07 |   | §5(b))                |
+-----------------------+   +-----------------------+

             |
    InContextOf
             v
+-----------------------+   +-----------------------+
| A1 — The pilot        |   | J1 — Argument by      |
| traffic-mix is a fair |   | per-obligation +      |
| approximation of T2   |   | per-framework         |
| production traffic on |   | discharge is chosen   |
| the classes routed by |   | because both auditor  |
| the model.            |   | audiences require it. |
+-----------------------+   +-----------------------+
```

Note the pattern already:

- The top-level goal is *dated* and *scoped* — an assurance case is only ever valid at a moment in time and against a defined deployment.
- The context nodes carry the scope (tier, jurisdiction, product owner, release candidate hash).
- The **assumption** `A1` about pilot-to-production traffic is *declared* — GSN's discipline is that any premise you would not want an auditor to surface as a defeater has to be visible as an assumption from day one.
- The **justification** `J1` for the chosen strategy is present because "argument by discharge of each obligation" is one of several possible strategies (see chapter `01`, `S1`–`S4`) and the reviewer wants to know why *this* one was chosen.

### First-level strategy and sub-goals

```
                                     G1
                                     |
                          SupportedBy |
                                     v
                    +----------------------------+
                    | S1 — Argument by discharge |
                    | of each in-scope obligation|
                    | (per-obligation)           |
                    +----------------------------+
                          |         |       |         |         |
                    ______|______   |       |         |         |
                   v             v  v       v         v         v
+-----------------------+  +-----------+  +-------+  +-------+  +-------+
| G2 — EU AI Act Art. 9 |  | G3 — Art. |  | G4 —  |  | G5 —  |  | G6 —  |
| risk-management system|  |    10-15  |  | Art.  |  | Art.  |  | SR    |
| discharged.           |  | (per Art.)|  |  26   |  |  17   |  | 11-7  |
+-----------------------+  +-----------+  +-------+  +-------+  +-------+
```

`S1` says "we will discharge the top-level goal by showing that each obligation applicable to this release is discharged." Each sub-goal (`G2`, `G3`, …) is one obligation. In practice `G3` fans out further into six sibling sub-goals for Articles 10, 11, 12, 13, 14, and 15 — one per requirement.

### Leaf discharge with a solution

Zooming into one branch, `G3-Art15` (accuracy, robustness, cybersecurity):

```
                             G3-Art15
                                |
                    SupportedBy |
                                v
                +-------------------------------+
                | S2 — Argument by discharge of |
                | each Article 15 property      |
                +-------------------------------+
                    |          |          |
              ______|______    |          |
             v             v   v          v
+---------------------+ +---------+ +---------------+
| G3.1 — Accuracy on  | | G3.2 —  | | G3.3 —        |
| in-scope classes    | | Robust- | | Cybersecurity |
| meets the release-  | | ness    | | posture       |
| gate threshold      | | posture | | discharged    |
| within a 95% CI.    | | is docd.| |               |
+---------------------+ +---------+ +---------------+
             |
    SupportedBy
             v
+---------------------+   +-----------------------+
| Sn1 — Signed        |   | A2 — The eval set is  |
| eval report         |   | representative of T2  |
| eval-report-rc-2026 |   | production traffic on |
| -07-a3c1.pdf, with  |   | in-scope classes; the |
| bootstrap CI per    |   | representativeness    |
| MOD-EVAL evidence-  |   | statement lives in    |
| contract v1.        |   | dataset-card-v2.1.    |
+---------------------+   +-----------------------+
```

Two things to notice about the leaf structure:

- The **solution** `Sn1` is a *named, versioned artefact*, not a category. "Signed evaluation report" is not enough; the report's identifier, storage location, and the statistical warrant of the estimator are named. This is the interface to chapter `06`'s evidence contract.
- The **assumption** `A2` is attached at the leaf, not at the top. Assumptions are attached wherever they load-bear. A2's failure invalidates `G3.1` only; it does not necessarily invalidate `G3.2` or `G3.3`.

### Away-goals and modules

`G3.3` (cybersecurity posture) will typically be discharged not by a solution but by an away-goal into the `ai-infra-security` module that owns the cybersecurity assurance case:

```
                             G3.3
                                |
                    SupportedBy |
                                v
+---------------------------------------------------+
| AG-SEC-1 → Away-goal in module SEC-ARM-v2:        |
| "Aurelia-v3.2 cybersecurity posture discharges    |
|  EU AI Act Article 15(4) and NIST AI RMF          |
|  MANAGE-2.1 for tier T2 as of 2026-07-01."        |
+---------------------------------------------------+
```

Away-goals are how a release-case avoids owning craft it does not own. The `ai-infra-security` module has its own case, its own evidence, its own owner. The release-case cites it by identifier and does not re-argue. This is exactly the discipline chapter `06` will formalise as an evidence contract; here it lands as a graph structure.

## Choosing strategies well

A recurring failure mode of GSN cases is over-fanning a strategy and losing the reader in a graph too wide to walk. The GSN standard notes several common decomposition strategies; the four you will use most for AI release cases are:

- **Per-obligation discharge** — one sub-goal per applicable article / clause / sub-category. Best when the audience is a regulator or auditor and the case will be walked against a checklist.
- **Per-framework discharge** — one sub-goal per applicable framework (NIST AI RMF, ISO/IEC 42001, EU AI Act, SR 11-7). Best when the case has to serve multiple audiences with different literacy.
- **Per-property discharge** — one sub-goal per system property (accuracy, robustness, calibration, fairness, cybersecurity, privacy, transparency). Best when the underlying evidence pipeline is property-organised.
- **Per-risk discharge** — one sub-goal per residual risk from the harm inventory. Best when the release is *risk-limited* rather than *obligation-limited*, e.g., an internal deployment where the frame is "residual harm acceptable to the accountable executive" rather than a regulated obligation set.

All four are legitimate. All four require a **justification** node explaining *why* this decomposition was chosen for this case. A GSN case with no justification nodes is not a case; it is a diagram.

## Failure modes an experienced reviewer looks for

Deep coverage of assurance-case audit is in chapter `05`; the failure modes below are the ones that show up *in the GSN itself* and are worth catching at draft time before an auditor points them out.

- **Solutions with no identifier or version.** "Signed eval report" as a solution node means the case cannot survive an eval-report re-run.
- **Strategies that hide assumptions.** If a strategy says "argument by benchmark performance," the assumption "the benchmark is representative of production" is load-bearing and must be an explicit `A` node.
- **Goals restated as sub-goals.** A goal that decomposes into a rewording of itself has no decomposition. Every sub-goal must add information the parent did not carry.
- **Context that scopes the whole case invisibly.** If the context is only in a header slide, a reviewer skimming a leaf branch cannot see it. Every load-bearing context must be `InContextOf` a node inside the graph.
- **Missing away-goal identifiers.** An away-goal without a module and version identifier is functionally an assertion.
- **No dates.** A GSN case without a decision date and evidence dates cannot be re-argued at the next release cycle.

## Summary

- GSN's seven node types (goal, strategy, solution, context, assumption, justification, away-goal) and two link types (`SupportedBy`, `InContextOf`) are the whole notation you need for the module — everything else is v3 modular structure and diagram convention.
- An AI release-case's top-level goal is dated, scoped to a deployment tier and jurisdiction set, and decomposed by an *explicit* strategy — typically per-obligation, per-framework, per-property, or per-risk, chosen with a visible justification.
- Leaf solutions are named, versioned artefacts; assumptions are attached where they load-bear; away-goals cite modules owned elsewhere so the release-case does not re-argue peer craft.
- Chapter `03` shows the same case in CAE; chapter `04` persists it in SACM; chapters `05` and `06` audit and route it.
