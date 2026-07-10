# SACM Persistence, Versioning, and Diffing

## Motivation

GSN and CAE are notations. A release program has more than one release — often more than one release per week — and the release-gate case needs to survive across releases: last release's case has to be diff-able against this release's case, evidence has to be traceable to its version, and the argument's structure has to be queryable so that a change in one obligation surfaces every case that relied on it.

That is what the [OMG Structured Assurance Case Metamodel (SACM)](https://www.omg.org/spec/SACM/) is for. SACM is not a *drawing* format; it is a **metamodel** that captures the *content* of any assurance case (in GSN, CAE, or another notation) as typed, identified, related objects that a repository can hold. Persist your GSN or CAE case as SACM, and you gain versioning, diffing, and machine queryability without giving up the notation your audiences read.

This chapter installs the SACM structure, walks a small SACM instance for the release-case we have been developing, and shows the concrete pattern for versioning and diffing across release cycles.

Primary reference: [OMG SACM 2.2](https://www.omg.org/spec/SACM/) (the standard document, XMI schema, and package structure). This chapter follows SACM 2.2's names; older SACM literature (2.0 / 2.1) uses slightly different casing but the same shape.

## SACM at a glance

SACM defines a metamodel — a description of the classes and relationships an assurance case's content must be expressible in. It is packaged into three parts:

- **SACM::Base** — foundational classes (identifiers, artefact packages, taggable elements, description elements). Everything in SACM inherits from `Base`.
- **SACM::Argumentation** (the Argumentation Metamodel, ARM) — the classes for the *argument*: claims, argument-reasoning, argument-packages, references. This is where a GSN goal or CAE claim persists.
- **SACM::Terminology** — the vocabulary and definition classes that scope a claim's meaning.
- **SACM::Artifact** — the classes for evidence: artefact assets, artefact packages, participants (the people or bodies who signed), events (production of the artefact), technique (the method that produced it).

Two things follow from the packaging.

1. The **argument** and the **evidence** live in different packages so a claim can be re-argued or re-cited without moving the underlying evidence, and evidence can be re-referenced by other cases without duplication.
2. Every element in a SACM instance has an **identifier** and a **version**; every relationship is directional and typed; every element has a **content** attribute where the human-readable statement lives.

Serialisation is via [OMG XMI](https://www.omg.org/spec/XMI/) (the OMG-standard XML interchange for metamodels). Practitioner tools and the OMG published sample instances also render SACM as JSON for ease of scripting; both round-trip through the same metamodel.

## The classes you will use most

The full SACM specification defines dozens of classes. The subset you will exercise for a typical AI-release case is small.

- **`ArgumentPackage`** — the container for a case (or a module of a case). One `ArgumentPackage` per release-case module.
- **`Claim`** — a single claim, equivalent to a GSN goal or a CAE claim. Has `content` (the human-readable statement), `assumed` (boolean, `true` if this claim is an assumption), and `toBeSupported` (boolean, `true` if the claim is decomposed further).
- **`ArgumentReasoning`** — the reasoning that connects a parent claim to its supporting sub-claims. This is where the GSN strategy or CAE argument block sits, with the block name in `content`.
- **`AssertedInference`** — the relationship element linking a set of premise claims to a conclusion claim via an `ArgumentReasoning`. GSN's `SupportedBy` from a Strategy to child Goals persists here.
- **`AssertedContext`** — the relationship linking a claim (or `ArgumentReasoning`) to a scoping element. GSN's `InContextOf` persists here.
- **`ArtifactPackage`** — the container for evidence.
- **`Artifact`** — a piece of evidence. Has `content`, and one or more `ArtifactAsset` children.
- **`ArtifactAsset`** — the concrete asset (e.g., a signed PDF, a JSON blob, an OCI-registry digest). Has a version and a storage reference.
- **`Participant`** — the person or body responsible for producing the artefact (the risk-engineer lead, the model-evaluation-engineer lead, the third-party evaluator).
- **`Event`** — the event that produced the artefact (the evaluation run, the red-team engagement, the sign-off meeting).
- **`Technique`** — the technique the artefact was produced by (bootstrap CI, HELM subset, GSN peer review, etc.).
- **`TerminologyPackage`** — the vocabulary the case is scoped in.

The **argument** side is the graph you already drew in chapter `02`; the **evidence** side is what chapter `06` will formalise as the evidence contract.

## A small SACM instance for the release-case

The snippet below persists a slice of the `Aurelia-v3.2` release-case from chapters `02` and `03` in JSON. The JSON is illustrative; the same content in XMI is one-to-one with the metamodel and is what a SACM-conformant tool would emit.

```json
{
  "sacm": "2.2",
  "argumentPackages": [
    {
      "id": "AP-Aurelia-v3.2-T2",
      "version": "1.0.0",
      "content": "Release-case for Aurelia-v3.2 at deployment tier T2, decision date 2026-07-10.",
      "claims": [
        {
          "id": "C1",
          "content": "The release of Aurelia-v3.2 at deployment tier T2 into US+EU discharges the applicable release-gate obligations on the evidence available as of 2026-07-10.",
          "assumed": false,
          "toBeSupported": true
        },
        {
          "id": "A1",
          "content": "Pilot traffic-mix (200 users, US, 2026-05-01 → 2026-06-30) fairly approximates T2 production traffic on the classes routed by the model.",
          "assumed": true,
          "toBeSupported": false
        },
        {
          "id": "C1.1.15.a",
          "content": "Per-class F1 >= 0.85 on the calibration set within a 95% bootstrap CI, on the classes routed by the model.",
          "assumed": false,
          "toBeSupported": true
        }
      ],
      "reasonings": [
        {
          "id": "R1",
          "content": "Argument by per-obligation + per-framework discharge (decomposition)."
        },
        {
          "id": "R1.1.15.a",
          "content": "Concretion of 'accuracy on in-scope classes' via dataset-card-v2.1 §3, then evidence-incorporation."
        }
      ],
      "assertedInferences": [
        {
          "id": "AI-1",
          "premises": ["C1.1", "C1.2", "C1.3", "C1.4"],
          "conclusion": "C1",
          "reasoning": "R1"
        },
        {
          "id": "AI-2",
          "premises": ["E-eval-1"],
          "conclusion": "C1.1.15.a",
          "reasoning": "R1.1.15.a"
        }
      ],
      "assertedContexts": [
        {
          "id": "AC-1",
          "context": "TP-Deployment-T2",
          "target": "C1"
        },
        {
          "id": "AC-2",
          "context": "A1",
          "target": "C1"
        }
      ]
    }
  ],
  "artifactPackages": [
    {
      "id": "AP-Aurelia-v3.2-T2-Evidence",
      "version": "1.0.0",
      "artifacts": [
        {
          "id": "E-eval-1",
          "content": "Eval report for rc-2026-07-a3c1, per MOD-EVAL evidence-contract v1.",
          "assets": [
            {
              "id": "asset-eval-report-pdf",
              "version": "v1.0.0",
              "storageRef": "artefact-registry://mod-eval/eval-report-rc-2026-07-a3c1.pdf",
              "digest": "sha256:c3a9e5..."
            }
          ],
          "participants": ["model-evaluation-engineer-lead@bank.example"],
          "events": ["EV-eval-run-2026-07-05"],
          "techniques": ["bootstrap-ci-95pct-per-class-f1"]
        }
      ]
    }
  ],
  "terminologyPackages": [
    {
      "id": "TP-Deployment-T2",
      "content": "Deployment tier T2: US+EU, all users, release candidate rc-2026-07-a3c1. Jurisdictions in scope: US (SR 11-7), EU (AI Act Annex III §5(b))."
    }
  ]
}
```

Read this as: the release-case is one `ArgumentPackage` whose top claim `C1` is contextualised by `TP-Deployment-T2` and by assumption `A1`; its reasoning is decomposition (`R1`); its leaf claim `C1.1.15.a` is contextualised by the concretion argument (`R1.1.15.a`) and discharged by evidence `E-eval-1` whose concrete asset is stored under the artefact registry with a content digest.

Everything you saw drawn in GSN in chapter `02` and written in CAE prose in chapter `03` is here as typed objects. That is the win: one source of truth, many renderings.

## From GSN or CAE to SACM

You will not usually author SACM directly. The workflow is:

1. **Draft** the case in GSN or CAE (whichever notation the audience wants) using a case editor or a text template.
2. **Export** to SACM via the tool of record or via a script that walks the source model.
3. **Store** the SACM in a case repository (Git-tracked, tagged per release, digested).
4. **Render** from SACM back into GSN and CAE views on demand for the audiences that need each.

The [Assured Safety Arguments (ASCE)](https://www.adelard.com/asce/) tool exports SACM 2.2 natively. Open-source tooling for GSN-to-SACM includes the [Isabelle-based SACM libraries](https://github.com/isaqs/sacm-isabelle) and community JSON tools listed in `resources.md`. If you write a lightweight tool in-house, keep three properties: (a) every SACM element has a stable identifier that survives re-render, (b) every artefact digest is captured so the SACM instance is verifiable against the registry, (c) the export is idempotent so a no-op edit does not produce a diff.

## Versioning

The version story lives at three levels.

- **`ArtifactAsset` version.** Each concrete evidence artefact carries a version and a content digest. When the risk engineer re-runs the red-team, the resulting artefact is a *new asset version* referenced by the case.
- **`Artifact` version.** The evidence node itself carries a version if its meaning has changed (e.g., "Eval report v1 covered 12 classes; Eval report v2 covers 14 classes"). Multiple asset versions can live under one artefact version if the underlying artefact is being iteratively signed.
- **`ArgumentPackage` version.** The case module itself is versioned. A new release-gate decision is a new version of the case, referencing the artefact versions it decided against.

The recommended pattern for AI release programs is to version the `ArgumentPackage` per release-gate decision (`AP-Aurelia-v3.2-T2` v1.0.0 for the 2026-07-10 decision, v1.1.0 for a subsequent T2 re-decision after a fine-tune, v2.0.0 for a T3 promotion). Store the SACM instance in Git with a tag matching the version; store the artefact assets in an artefact registry addressed by digest. This keeps diffs cheap (Git handles the argument side) while keeping the evidence integrity guarantee (digests are checked at load).

## Diffing between release cycles

The whole point of persisting into SACM is that the *next* release cycle does not re-argue the case from scratch. It diffs. A useful diff between two case versions surfaces three classes of change:

- **Structural diff.** New claims added, old claims removed, sub-claim decompositions restructured. This is a graph diff: which nodes changed, which edges changed, which contexts moved.
- **Content diff.** A claim's `content` field changed (e.g., a threshold moved from `0.85` to `0.87`). This is a text diff on the claim's `content`.
- **Evidence diff.** An artefact's asset was replaced with a new version, or the evidence-contract technique changed (e.g., the CI methodology moved from parametric to bootstrap).

A tractable diff tool renders these three classes separately. Structural diffs surface as a two-column graph view; content diffs surface as line-level text diffs on the claim `content`; evidence diffs surface as an asset-manifest diff (old digest → new digest, old technique → new technique, old participant → new participant).

The pattern to internalise: **a well-diff-able assurance case is one where every load-bearing statement lives in exactly one node**. If the same threshold appears in three claims, the diff will lie; if the same evidence is duplicated across two artefacts, the diff cannot tell you which version is authoritative.

## Machine queryability

Because SACM is a metamodel, standard queries become one-liners against the persisted instance. Three queries you will run every release cycle:

- **"Which claims does artefact X support?"** — walk `AssertedInference` with `X` in `premises`. Useful when the evidence registry retires an artefact and you need to know which release-cases now have a hole.
- **"Which release-cases assume A?"** — walk `assumed=true` claims across `ArgumentPackages` and grep `content`. Useful when a pilot-to-production assumption changes and the program needs to re-argue every case that used to rest on it.
- **"Which evidence discharges obligation O?"** — walk from the claim whose `content` maps to `O`, follow inferences down to leaves, list the artefacts. Useful for regulator questions of the form "show me every artefact behind Article 15(1)(a) for this system this release."

## What SACM does not solve

SACM persists the case. It does not check the case. Undermining evidence, unstated assumptions, insufficient diversity of evidence, and defeaters are *audit* questions — coverage in chapter `05`. SACM makes the audit *tractable* by giving each finding a stable identifier and a diffable target; it does not replace the audit.

Similarly, SACM does not check the *evidence contract* to the peer track that produced the artefact — that is chapter `06`. What SACM lets you do is *record* the evidence contract as `Artifact` participants, events, and techniques so the contract's discharge is traceable.

## Summary

- SACM is the OMG metamodel that persists a GSN or CAE assurance case's content as typed, identified, related objects across three packages: base, argumentation, terminology, artefact.
- Author your case in GSN or CAE, export to SACM (via a tool or a scripted walker), store the SACM instance in Git alongside artefact digests, and render back into the audience's notation on demand.
- Version at three levels: `ArtifactAsset` (concrete evidence), `Artifact` (evidence node meaning), and `ArgumentPackage` (the case module). Tag SACM in Git per release-gate decision.
- Diffs between release cycles surface structurally, in content, and in evidence, and are only meaningful if every load-bearing statement lives in exactly one node.
- SACM makes audit and evidence-contract discharge *tractable*; chapters `05` and `06` do the audit and the contract.
