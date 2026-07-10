# Why an Assurance Case Is the Shape a Release Gate Needs

## Motivation

A release-gate decision has to *survive* three audiences at once. The internal decision-maker signing the release wants a defensible chain of reasoning; a third-party auditor arriving six months later wants to reconstruct the same chain from the evidence; a regulator asking a Question of the Day wants to walk from one obligation to one artefact and back. If the only thing on the desk is a slide deck, a table of eval scores, or a pass/fail from a CI job, none of those audiences can be discharged.

The safety-engineering tradition solved the same problem for aviation, rail, nuclear, and medical devices decades ago by writing an **assurance case**: a structured, reviewable argument that a top-level claim (the system is acceptably safe for its intended use, the release is defensible under the applicable regime, the AI system meets its stated properties) is supported by evidence, with the chain of reasoning between the claim and the evidence made explicit. That tradition is what this module borrows from.

The [GSN Community Standard v3](https://scsc.uk/gsn) frames the assurance case as "a reasoned and compelling argument, supported by a body of evidence, that a system, service or organisation will operate as intended for a defined application in a defined environment." The same shape works for an AI release. What changes is the character of the evidence (model / system / dataset artefacts, evaluations, red-team findings, monitoring plans) and the character of the argument (thresholds statistically warranted, evaluators independently sourced, obligations mapped to jurisdictions).

## What an assurance case is not

Three things get confused with an assurance case, and getting the distinction right is a prerequisite for the rest of the module.

- **An assurance case is not a report.** A report describes what happened. An assurance case argues why a claim holds, and structures that argument so a reviewer can walk it and disagree with any node. A model card is a report; an assurance case cites the model card as evidence.
- **An assurance case is not a compliance checklist.** A checklist enumerates obligations. An assurance case takes each obligation as a sub-claim and argues that the evidence discharges it. If the checklist has a green tick next to "Article 15 accuracy," the assurance case must show *how* the evidence supports that tick.
- **An assurance case is not a story.** A story is linear, editorial, and hard to review adversarially. An assurance case is a graph, with typed nodes (goals / claims, strategies / arguments, evidence / solutions, context, assumptions, justifications), and every link is either sound or unsound.

The mismatch between AI release evidence and any of these three lighter artefacts is why the assurance-case shape shows up in AI-governance frameworks. NIST AI RMF calls repeatedly for "documented rationale" for measurement decisions; ISO/IEC 42001 clauses 6, 8, and 9 assume a documented risk-based argument with linkable evidence; the EU AI Act, Articles 9 through 15 and Article 17, requires a technical documentation package whose shape a reviewer can walk.

## The three notations you have to fluently read

There are three notations you must be able to read, write, and translate between by the end of this module. Deep coverage of each is in chapters `02`, `03`, and `04`. This chapter previews them so the rest of the module has vocabulary to spend.

### GSN — Goal Structuring Notation

GSN is a graphical notation for assurance cases developed in the mid-1990s at the University of York and now maintained as a community standard. Its central primitives are the **goal** (a claim about the system), the **strategy** (the argument that decomposes a goal into sub-goals), the **solution** (the evidence that discharges a leaf goal), the **context** (the definitions or assumptions that scope a goal), the **assumption** (an unproven-but-declared premise), the **justification** (the rationale for choosing a strategy), and the **away-goal** (a reference to a goal proven elsewhere).

GSN is easy to read and to review. It is the default notation for regulator-facing safety cases in UK rail, aviation, and defence — and it is the notation most AI-assurance work in academia has adopted. When you draw a case on the whiteboard for a room of engineers, you will almost always be drawing GSN.

### CAE — Claim, Argument, Evidence

CAE is the notation Adelard developed for their assurance cases; the CAE building blocks are formalised in the [Assurance Case Fundamentals](https://www.adelard.com/asce/choosing-asce/cae.html) work by Bloomfield and Bishop. Its three primitives are the **claim** (equivalent to a GSN goal), the **argument** (how the claim is supported), and the **evidence** (what discharges a leaf claim). CAE adds five **argument building blocks** — decomposition, substitution, concretion, calculation, and evidence-incorporation — which is where its intellectual weight lives.

CAE is easier to write in prose than GSN, and it is the notation that regulators, safety authorities, and legal reviewers tend to be most fluent in. It also has a natural fit for defeaters (things that would undermine a claim if true) via a documented pattern called **CAE Blocks + Defeaters**. When you are writing the assurance case as a *document* for an auditor, CAE is often the better shape.

### SACM — Structured Assurance Case Metamodel

SACM is the OMG (Object Management Group) standard that gives GSN and CAE (and any other assurance-case notation) a single machine-readable metamodel. Its two packages, the **Argumentation Metamodel (ARM)** and the **Structured Assurance Evidence Metamodel (SAEM)**, express the argument and its evidence as typed objects with identifiers, relationships, and traceable versions. SACM is what lets you persist an assurance case, diff it between releases, and machine-check it against obligations.

You will not draw SACM. You will *persist* GSN or CAE cases as SACM, so that a repository can hold them, versioning tools can diff them, and downstream systems can query them.

## Where the argument for an AI release-gate lives

The rest of this track hangs everything off a single graph, so it is worth being explicit about what that graph typically claims.

The top-level goal (or claim) of an AI-release assurance case is almost always some form of:

> **G1** — The release of this AI system, at this deployment tier, into this jurisdiction, discharges the release-gate obligations that apply to it, on the evidence available at time-of-decision.

That top-level goal decomposes along a small number of standard strategies. A typical release-case for an EU AI Act Annex III high-risk system decomposes through:

- **S1** — Argument by discharge of each in-scope obligation (Articles 9–15, 17, 26, 43, 47, 49; Article 55 if GPAI-with-systemic-risk; Article 61 if post-market data has landed; Article 72 if a post-market plan is required).
- **S2** — Argument by discharge of each in-scope framework (NIST AI RMF sub-categories, ISO/IEC 42001 clauses, sector rules such as SR 11-7 or FDA GMLP).
- **S3** — Argument by soundness of the evidence chain (statistically warranted thresholds, reproducibility of the evidence, integrity of the artefact registry).
- **S4** — Argument by residual-risk acceptability (defeaters identified, mitigations in place, escalation paths named).

Under each of those strategies you decompose into sub-goals (per-obligation claims, per-clause claims, per-property claims). Under each sub-goal you either decompose further or discharge with evidence (a signed evaluation, a benchmark result with a CI, a red-team finding with a mitigation, a card version, a monitoring plan). Chapters `02`–`04` will make all of that concrete in each notation.

## Why an AI release needs the assurance-case shape more than a classical safety-critical system

Two things are different about the AI setting, and both push you deeper into the assurance-case shape rather than out of it.

1. **The evidence is less stable.** A control law in an autopilot admits closed-form verification; a language model's behaviour under a red-team suite does not. The AI-assurance case has to argue that a *statistical* body of evidence discharges the top-level goal, and that argument has to survive an evaluator who understands both statistics and the system. This is why the module ends on evidence contracts (chapter `06`) rather than on notation drills — where the argument bites is at the interface between the assurance case and the peer track that produced the evidence.
2. **The obligation graph is denser.** A commercial airliner discharges one certification framework (with local variants). An AI system in enterprise use might be in scope for the EU AI Act, NIST AI RMF, ISO/IEC 42001, a sector rule (SR 11-7 / GMLP / DORA), and a deployment-tier framework (RSP / Preparedness / FSF) *simultaneously*. The assurance case is the artefact that lets one release-gate decision discharge all of them without duplicating the underlying evidence.

Both properties are why the notation and persistence choices in this module matter. If the case is not versioned and diffable, the release cycle cannot re-argue the delta rather than rewriting from scratch. If the case cannot be audited for undermining evidence, it will drift into a report. If the evidence contracts are not clean, the case will collapse the first time a peer track re-scopes and the release-gate cannot backfill.

## Summary

- An assurance case is a reasoned, evidence-supported, adversarially-reviewable argument that a top-level claim holds — it is not a report, checklist, or story.
- The three notations you must read and write fluently by the end of this module are GSN (graphical, whiteboard default), CAE (prose-friendly, regulator-friendly), and SACM (machine-persistable, versionable, diffable).
- The top-level goal of an AI-release case is almost always "the release discharges the applicable release-gate obligations, on the evidence available at time-of-decision," and it decomposes along strategies of per-obligation discharge, per-framework discharge, evidence soundness, and residual-risk acceptability.
- The AI-release setting demands the assurance-case shape *more* than classical safety-critical settings, because evidence is statistical and the obligation graph is dense.
- The rest of the module walks GSN (`02`), CAE (`03`), SACM (`04`), audit / defeaters (`05`), and evidence-contract routing (`06`).
