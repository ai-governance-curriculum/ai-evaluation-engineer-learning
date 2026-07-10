# CAE and Choosing Between GSN, CAE, and a Hybrid

## Motivation

If GSN is the whiteboard notation, **CAE (Claim, Argument, Evidence)** is the notation you reach for when the audience is reading rather than drawing — a regulator's technical documentation package, a Big-Four assurance letter, an internal-audit workpaper, or a legal-hold submission. CAE reads as structured prose whose skeleton is the same three-primitive graph GSN uses, plus a small library of *argument building blocks* that name the reasoning move being made.

This chapter installs the CAE vocabulary, recasts the release-case from chapter `02` in CAE, walks the CAE Blocks + Defeaters pattern that will feed the audit chapter (`05`), and closes with the criteria for choosing GSN, CAE, or a hybrid.

Primary references:

- [Adelard — Assurance Case Fundamentals (CAE)](https://www.adelard.com/asce/choosing-asce/cae.html) — the practitioner introduction.
- Bloomfield and Bishop, *Safety and Assurance Cases: Past, Present and Possible Future — an Adelard Perspective* — the intellectual history of the notation.
- [Assured Safety Arguments (ASCE) tool documentation](https://www.adelard.com/asce/) — the tooling most CAE cases are drafted in.
- [ISO/IEC/IEEE 15026-2:2022](https://www.iso.org/standard/80625.html) — assurance case content and structure (framework-agnostic; both GSN and CAE conform).

## The three CAE primitives

CAE names three node types:

- **Claim** — a proposition about the system. Equivalent to a GSN goal. A claim is a *declarative statement* whose truth-value is what the case establishes.
- **Argument** — how a claim is supported by sub-claims or by evidence. Equivalent to a GSN strategy, but with a *typed* set of argument building blocks (below) that name the reasoning move.
- **Evidence** — the artefact discharging a claim. Equivalent to a GSN solution.

A CAE case is a directed graph of these three, with a single top-level claim, arguments as intermediate nodes, sub-claims fanning out under arguments, and leaves discharged by evidence. Written in prose, the graph appears as a nested list of numbered claims where each claim carries the argument that supports it and either sub-claims or evidence references at its leaves.

## The CAE argument building blocks

The intellectual weight of CAE lives in a small catalogue of **argument building blocks**. The Adelard formulation names five; they are the moves you are allowed to make when moving from a claim to its supporting sub-claims. Every argument in a CAE case is one of these blocks (or an explicitly labelled hybrid). Naming the block forces the author to be precise about the reasoning move — and lets a reviewer disagree with the *move*, not just the sub-claims.

- **Decomposition (or *split*)** — decompose the claim into sub-claims whose conjunction implies the claim. Example: "The release discharges Article 15" is decomposed into "…discharges accuracy", "…discharges robustness", "…discharges cybersecurity."
- **Substitution** — replace the claim with an equivalent claim that is easier to establish. Example: substitute "the model is accurate on the in-scope classes" with "the model achieves ≥ X on benchmark B whose classes cover the in-scope classes per the mapping in dataset-card-v2.1."
- **Concretion (or *definition*)** — replace an abstract claim with a concrete, measurable one. Example: concretise "the system is accurate" as "the system achieves a per-class F1 ≥ 0.85 on the calibration set with a 95% bootstrap CI."
- **Calculation (or *derivation*)** — derive the claim from lower-level claims by a stated calculation. Example: derive "the top-level residual-risk is acceptable" by aggregating per-risk residuals with a stated weighting rule.
- **Evidence-incorporation** — attach evidence directly to a leaf claim. This is the block that lands on a leaf; every other block fans out into sub-claims.

Every argument node in a CAE case should carry the block name explicitly, e.g., `Argument A2.1 (Decomposition): decompose G3-Art15 into the three properties of Article 15(1)`. If an argument fits none of the five, name the hybrid explicitly (e.g., "concretion followed by decomposition") — do not hide it.

## Side-warrants: context, assumption, justification in CAE

CAE handles the same non-inferential nodes GSN uses (context, assumption, justification) with a slightly different terminology and shape. A CAE claim or argument carries three optional side-warrants:

- **Context / definitions** — the scope statement or definitions the claim is bound to. Equivalent to a GSN Context node.
- **Assumption** — an unproven premise attached to a claim or argument, always with a rationale for why the case can rest on it. Equivalent to a GSN Assumption node.
- **Warrant / justification** — the reason the chosen argument block applies. Equivalent to a GSN Justification node.

In the ASCE tool and in most CAE prose templates the side-warrants render as sub-bullets under the parent claim, prefixed `Context:`, `Assumption:`, or `Warrant:`. In a technical documentation package they render as footnotes or as explicit "Assumptions" and "Definitions" sub-sections under each claim.

## Recasting the release-case from chapter `02` in CAE

Take the same `Aurelia-v3.2` T2 release from chapter `02` and rewrite the top three levels in CAE prose.

```
C1  The release of Aurelia-v3.2 at deployment tier T2 into US+EU
    discharges the applicable release-gate obligations on the
    evidence available as of 2026-07-10.
    Context: Deployment tier T2 (US+EU, all users, release candidate
             rc-2026-07-a3c1).
             Jurisdictions in scope: US (SR 11-7), EU (AI Act Annex III
             §5(b)).
    Assumption: Pilot traffic-mix (200 users, US, 2026-05-01 → 2026-06-30)
             fairly approximates T2 production traffic on the classes
             routed by the model.
    Warrant: Per-obligation + per-framework discharge is chosen because
             the auditor and regulator audiences both require it.

    Argument A1 (Decomposition):
    Decompose C1 into per-obligation sub-claims and per-framework
    sub-claims, both required to hold jointly.

        C1.1  The release discharges each in-scope EU AI Act obligation.
        C1.2  The release discharges each in-scope NIST AI RMF sub-category.
        C1.3  The release discharges the ISO/IEC 42001 clauses relevant
              to release management.
        C1.4  The release discharges the SR 11-7 model-risk-management
              expectations applicable to the fine-tuned derivative.

    (C1.1 developed further below; C1.2 – C1.4 developed in their own
     numbered sections.)

C1.1  The release discharges each in-scope EU AI Act obligation.

      Argument A1.1 (Decomposition):
      Decompose C1.1 by article: 9, 10, 11, 12, 13, 14, 15, 17, 26,
      and where applicable 61 and 72.

          C1.1.9  Article 9 (risk-management system) is discharged.
          C1.1.10 Article 10 (data governance) is discharged.
          …
          C1.1.15 Article 15 (accuracy, robustness, cybersecurity)
                  is discharged.

C1.1.15  The release discharges Article 15 (accuracy, robustness,
         cybersecurity).

      Argument A1.1.15 (Decomposition, following Article 15(1)):
      Decompose Article 15 into its three properties.

          C1.1.15.a  Accuracy on in-scope classes meets the
                     release-gate threshold within a stated CI.
          C1.1.15.b  Robustness posture is documented and meets
                     the release-gate expectations.
          C1.1.15.c  Cybersecurity posture is documented and
                     discharged per Article 15(4).

C1.1.15.a  Per-class F1 ≥ 0.85 on the calibration set within a 95%
           bootstrap CI, on the classes routed by the model.

      Argument A1.1.15.a (Concretion + Evidence-incorporation):
      Concretise "accuracy on in-scope classes" as "per-class F1
      threshold on the calibration set" via the definition in
      dataset-card-v2.1 §3, and discharge with the eval report.
      Warrant: The calibration set's construction is described in
      dataset-card-v2.1 §2 and its representativeness for T2 traffic
      is separately claimed in C1.1.10 (Article 10 data governance);
      Article 15's accuracy obligation is a *properties* obligation,
      so a concretised threshold is legitimate under Article 15(3).
      Assumption: The pilot-to-production traffic assumption at C1
      is not additionally required at this leaf.

          Evidence E-eval-1: eval-report-rc-2026-07-a3c1.pdf, signed
          by the model-evaluation-engineer lead, with bootstrap CI
          per MOD-EVAL evidence-contract v1.

C1.1.15.c  Cybersecurity posture is discharged per Article 15(4).

      Argument A1.1.15.c (Evidence-incorporation by away-claim):
      Discharge via the AI-Infra-Security cybersecurity assurance
      case, which owns Article 15(4) for this platform.

          Away-claim SEC-ARM-v2 §C-2.3: "Aurelia-v3.2 cybersecurity
          posture discharges EU AI Act Article 15(4) and NIST AI RMF
          MANAGE-2.1 for tier T2 as of 2026-07-01."
```

A CAE case reads out as prose; the underlying graph is the same as the GSN case in chapter `02`. Every argument node names the block being used; every side-warrant (context, assumption, warrant) is attached at the level where it load-bears; every leaf is either an evidence reference or an away-claim into another case.

## CAE Blocks + Defeaters

CAE has a documented pattern — sometimes called **CAE Blocks + Defeaters** — that makes assurance-case audit tractable. Under this pattern, every argument node explicitly names two things beyond its block: the **defeaters** that would undermine the argument if true, and the **mitigations** in place to counter each defeater.

A defeater is a proposition whose truth would invalidate an argument or a claim. Two flavours matter:

- **Rebutting defeaters** — propositions that directly contradict the claim (e.g., "the eval set overlaps the training set, so the reported accuracy is inflated").
- **Undercutting defeaters** — propositions that break the argument without directly contradicting the claim (e.g., "the bootstrap CI is computed under an IID assumption that the pilot traffic mix violates").

Deep coverage of defeater identification is in chapter `05`. In this chapter, take the pattern as a prompt attached to every argument node:

- What defeaters would a hostile-but-competent reviewer raise here?
- What evidence or process do we have that mitigates each?
- What residual defeaters remain unaddressed, and are they declared as assumptions?

`A1.1.15.a` above becomes:

```
Argument A1.1.15.a (Concretion + Evidence-incorporation):
  …

  Defeater D1 (rebutting): The eval set overlaps the training corpus,
     so the reported F1 is inflated.
  Mitigation M1: Training-corpus / eval-set disjointness is verified
     under MOD-EVAL evidence-contract v1 §4 and confirmed in
     eval-report §Appendix B.

  Defeater D2 (undercutting): Bootstrap CI is computed under an IID
     assumption; production traffic is non-IID across US-vs-EU.
  Mitigation M2: Per-region CI additionally computed in
     eval-report §5.2; both intervals lie above threshold.

  Residual: A US-and-EU joint interval is not computed.
     Declared as Assumption A2': "US and EU per-region CIs are
     jointly sufficient given the mapping in dataset-card-v2.1 §3."
```

The residual — the defeater the case cannot yet mitigate — is declared as an assumption. That is the honest move; it puts the load-bearing premise into a reviewable node instead of hiding it in the tone of the prose.

## Choosing between GSN, CAE, and a hybrid

The three notations are semantically equivalent (they all conform to [ISO/IEC/IEEE 15026-2](https://www.iso.org/standard/80625.html) content requirements and all persist into SACM — see chapter `04`), so the choice is about audience and workflow, not about correctness.

### Reach for GSN when…

- The primary audience is engineers or a technical committee reviewing on a whiteboard.
- The case is *structurally complex* — many parallel branches, extensive modularity, heavy use of away-goals — because GSN's graphical form makes structure visible.
- The team already has GSN literacy from safety-critical background (rail, aviation, medical devices).
- The tool of record supports GSN natively (Sphinx-Assure, ASCE, or an in-house GSN editor).

### Reach for CAE when…

- The primary audience is a regulator, auditor, legal reviewer, or executive-level accountable person who will read the case as a document.
- The case will land inside a technical documentation package (EU AI Act Annex IV, SR 11-7 model documentation, FDA 510(k) submission) whose expectation is structured prose.
- The reasoning moves matter as much as the branching — because CAE's argument blocks force the author to name each move.
- Defeaters are prominent (safety-critical release, high-stakes deployment, contested residual risk) — the CAE Blocks + Defeaters pattern is tighter than GSN's implicit handling.

### Reach for a hybrid when…

Two hybrid patterns show up often in practice:

- **GSN skeleton, CAE prose for the leaves.** Draw the top three or four levels in GSN so the structure is visible; write out each leaf sub-tree in CAE prose so it can be dropped into the technical documentation package. This is the most common pattern for large enterprise release cases with mixed audiences.
- **CAE case with a GSN-style module map.** Write the case in CAE, but publish a GSN-style module map alongside it that shows the away-claim structure — which modules feed which claims. This is common for programs with many products (each product's case is CAE prose; the program-level map is GSN).

Both hybrids are legitimate under ISO/IEC/IEEE 15026-2 and both persist into the same SACM (chapter `04`).

### What to avoid

- **A single case in two notations kept out-of-sync.** If you draw a GSN diagram *and* write a CAE case for the same product, one of them will drift and reviewers will lose trust in both. Persist one source of truth (in SACM) and *render* into whichever notation each audience needs.
- **CAE prose without argument-block labels.** Prose that never names its reasoning move is a report, not a case. Every argument in the CAE case must name a block.
- **GSN diagrams without context nodes.** A GSN diagram whose top-level context lives only in an accompanying slide is not a stand-alone case.

## Summary

- CAE names three primitives (claim, argument, evidence), five argument building blocks (decomposition, substitution, concretion, calculation, evidence-incorporation), and three side-warrants (context, assumption, warrant).
- A CAE case reads as prose whose skeleton is the same graph as GSN — every notation is one rendering of the same underlying assurance-case content per ISO/IEC/IEEE 15026-2.
- The CAE Blocks + Defeaters pattern requires every argument to name its defeaters and the mitigation for each; unmitigated defeaters land as declared assumptions. Chapter `05` uses this pattern to structure the audit.
- Choose GSN for whiteboard-and-engineer audiences and structurally complex cases; choose CAE for regulator / auditor / legal audiences and defeater-prominent cases; hybrid patterns are legitimate and common — one source of truth persisted in SACM, rendered per audience.
