# exercise-02: CAE Recast and Shape Choice

**Estimated effort:** 3 hours

## Objective

Recast the GSN case you authored in exercise `01` in **Claim, Argument, Evidence (CAE)** form, apply the **CAE Blocks + Defeaters** pattern to at least three arguments in the case, and then write a written **shape-choice rationale** defending which of GSN, CAE, or a hybrid you would deliver to each of your case's audiences.

This is the applied output of chapter `03`.

## Prerequisites

- Chapter `03-cae-and-shape-choice.md`.
- Exercise `01` output — the GSN case you will recast.
- Familiarity with the CAE building blocks (decomposition, substitution, concretion, calculation, evidence-incorporation) and the side-warrants (context, assumption, warrant / justification).

## Problem statement

You are the AI Evaluation Engineer preparing the case from exercise `01` for **two audiences** with different formats:

- **Audience 1 — Internal release-gate meeting.** The system's engineering leads, the risk-engineering lead, the AI-eval and model-eval peer leads, and the accountable executive. Format: whiteboard-and-slide-deck review; participants will walk the case top-down and ask questions at nodes.
- **Audience 2 — Regulator submission or external auditor package.** The EU AI Act notified body (scenario A / C), the FDA (scenario B), or the Big-Four assurance firm engaged by your organisation (any scenario). Format: structured prose in a technical documentation package; readers will walk the case as a document.

You have to decide which notation each audience gets, defend that decision in writing, and produce the CAE recast at minimum.

## Requirements

Produce a `cae-recast.md` (or equivalent) and a `shape-choice-rationale.md` containing:

### `cae-recast.md`

1. **CAE prose rendering of the top three levels of the case from exercise `01`.** Every claim numbered (`C1`, `C1.1`, `C1.1.15`, …); every argument named and labelled with a CAE block (`Argument A1.1 (Decomposition)`, `Argument A1.1.15.a (Concretion + Evidence-incorporation)`, etc.); every side-warrant (context, assumption, warrant) inline under the claim it attaches to.
2. **Full CAE rendering of the developed leaf branch from exercise `01`.** Every leaf claim has a stated evidence reference and warrant. Away-claims (equivalent to away-goals) name their target module and version.
3. **CAE Blocks + Defeaters at three arguments.** Choose three arguments — ideally spanning different CAE blocks (one decomposition, one concretion, one evidence-incorporation) — and for each write down:
   - The defeaters (rebutting and undercutting) a hostile-but-competent reviewer would raise.
   - The mitigation currently in place for each.
   - The residual defeaters, and how each residual is either declared as an assumption or blocks the case.
4. **A one-paragraph note on structural fidelity.** Confirm that the CAE and GSN cases are two renderings of the same underlying content — i.e., no claim in the CAE case is absent from the GSN case and vice versa, no context or assumption has been silently added or dropped. Chapter `03`'s warning against a single case in two notations kept out-of-sync applies here.

### `shape-choice-rationale.md`

1. **Which notation goes to which audience.** GSN, CAE, or a specified hybrid — one paragraph per audience.
2. **Why.** Reference chapter `03`'s decision criteria (whiteboard-vs-document, engineer-vs-regulator literacy, structural-complexity, defeater-prominence). Cite specifics from your scenario that push toward the chosen notation.
3. **How the two renderings stay in sync.** Chapter `03` recommends persisting a single source of truth (SACM — coverage in chapter `04` and exercise `03`) and *rendering* into each notation on demand. State how you will operationalise that in your organisation: which format is authoritative, which is a rendering, who owns keeping them in sync.
4. **What the hybrid would look like, if you chose one.** GSN skeleton + CAE prose at the leaves? CAE case + GSN module map alongside? Draw or sketch it.

## Starter guidance

- **Do not start the CAE recast from scratch.** The GSN graph *is* the CAE case's structure; you are re-rendering, not re-deriving. If you find yourself adding a new sub-claim during recast, go back and add it to the GSN case too — the two must stay one graph.
- **Every CAE argument names its block.** An unnamed argument is a hint the reasoning move has not been thought about. Even "Argument A (Decomposition)" is enough — the discipline is the labelling, not the sophistication.
- **Assumptions attach where they load-bear.** In CAE prose, an assumption reads as a sub-bullet under the specific claim it supports. Do not park all assumptions at `C1`; the reviewer needs to see which sub-claim each one holds up.
- **CAE Blocks + Defeaters is prompted, not imposed.** You are looking for defeaters a competent, motivated reviewer would raise. The point is to make them *visible* — one written-down defeater with a stated residual beats a hundred hand-waved ones.
- **The shape-choice rationale is a document you would actually send.** If your executive would not sign it, it is not done. Reference the audience's known preferences (a bank's chief model risk officer, an FDA reviewer, an EU notified body) explicitly — you are choosing per your audience, not per your preference.

## Acceptance criteria

You have succeeded if:

- Every claim, argument, side-warrant, and evidence reference in the CAE recast has a one-to-one counterpart in the GSN case from exercise `01`.
- Every argument in the CAE recast names a CAE block or a labelled hybrid.
- At least three arguments carry a CAE Blocks + Defeaters treatment with named rebutting and undercutting defeaters, mitigations, and residuals.
- Residual defeaters are either declared as assumption nodes in both the CAE and GSN cases or written up as blocking issues.
- The shape-choice rationale names both audiences, chooses a notation per audience, defends each choice against chapter `03`'s criteria, and defines a single-source-of-truth policy for keeping the two renderings in sync.
- The hybrid (if you chose one) is sketched concretely enough that a colleague could set it up in tooling without further explanation.

## Stretch goals

- Add a fourth argument's Blocks + Defeaters treatment covering an evidence-incorporation leaf whose evidence is authored by a peer track — this puts pressure on the routing exercise in `05`.
- Publish the CAE recast in a real CAE tool (e.g., ASCE) and export it — attach the export.
- Add a written **counter-audience note**: pick one audience you did not deliver to (e.g., an internal engineering IC not on the review committee) and describe what shape *they* would need and why it differs.
- Try a **three-notation experiment** — render a small slice of the case in [Structured Assurance Case Metamodel (SACM)](https://www.omg.org/spec/SACM/) JSON alongside the GSN and CAE renderings, then argue whether that slice's SACM version could serve as the single source of truth. (Exercise `03` develops this fully.)
