# The Assurance-Card Shape for External Audiences

## Motivation

Chapter `01` closed with a list of gaps in the Mitchell / Gebru / Hugging Face lineage — no assurance-case traceability, no regulator-facing structure, no system-level composition, no content-provenance, no audience variance. This chapter names what fills those gaps: the **assurance-card** shape. An assurance card is not a new notation. It is the base card plus the *fields, structure, and machine-readable bindings* the regulator, notified body, third-party evaluator, and board audience need to walk from a claim on the page to a signed evidence node in the store (mod-104) and back.

Two failure modes justify the extension.

The first is the **defensibility failure**. A base Mitchell card ships with metrics but not with an argument that the metrics were produced by an independent evaluator against an integrity-checked eval set with statistically warranted thresholds. A regulator reading the card cannot bind a claim to Article 15 (accuracy, robustness, cybersecurity) — the card asks them to take the metric on faith. Under EU AI Act Article 11 Annex IV (technical documentation) and Article 47 (declaration of conformity), faith is not enough; the card has to point at an assurance case that a reviewer can walk.

The second is the **audience failure**. The Hub-shaped model card assumes a single reader (a developer downstream). The four external audiences an enterprise card actually has — the public, the regulator, the third-party evaluator, and the board — need overlapping-but-not-identical disclosures. A single monolithic card either overshares (leaking attack payloads, PII, decontamination canary tokens) or underserves (a board reader who needs a residual-risk narrative gets a table of eval metrics). The assurance-card shape names how to derive audience variants from one canonical case; chapter `07` returns to the derivation rule.

## The assurance-card definition

An **assurance card** is a versioned, signed artefact that:

1. Carries a machine-readable **head** (structured metadata) and a human-readable **body** (prose).
2. Names the artefact it describes (model, dataset, system) by content-address into the evidence store (mod-104 chapter `01`).
3. Binds every reported claim in the body to at least one **evidence pointer** (a digest into the store, or a citation to a signed external evaluator report).
4. Names the **assurance-case node** the card discharges (a GSN goal or CAE claim identifier, per mod-102) so a reviewer walking the case reaches the card and vice versa.
5. Carries an **audience tag** that identifies which variant this is (public, regulator, third-party, board) and — for redacted variants — a `redaction-manifest` that names what was omitted and why.
6. Ships with a **signature** from the producer (chapter `06` of mod-104, and chapter `06` of this module) and, where applicable, a **C2PA content-provenance manifest** for GenAI outputs.

Every one of the six is a superset of what Mitchell et al. asked for. The rest of this chapter walks each and names where it comes from.

## The head: machine-readable metadata

The head is a canonicalised structured document (JSON, YAML, or JSON-LD; the head format is a program choice — pin it once and version it). Its job is to give any downstream tool — the release-gate walker, a regulator's compliance-management platform, a third-party evaluator's harness, a board-reporting dashboard — a machine-parseable summary of what the card describes.

A minimum viable head carries:

```yaml
card:
  schema_version: "assurance-card-v1"
  card_id: "card:internal-assistant/v2026-04-11:regulator"
  audience: "regulator"          # public | regulator | third-party | board
  supersedes: "card:internal-assistant/v2026-03-02:regulator"  # optional; prior version this replaces
  produced_at: "2026-04-11T14:22:00Z"
  producer: "assurance-team@example.corp"
subject:
  kind: "system"                 # model | dataset | system
  system_id: "internal-assistant/v2026-04-11"
  content_address: "sha256:74a1..."   # digest of the described artefact
  components:                    # for kind: system, the constituent model + dataset + eval bundles
    - kind: "model"
      id: "internal-assistant-base/v2026-04-09"
      content_address: "sha256:9ff2..."
    - kind: "dataset"
      id: "harm-eval-set/v3.2"
      content_address: "sha256:012c..."
    - kind: "eval-bundle"
      id: "rc-2026-05-07:release-gate-bundle"
      content_address: "sha256:47da..."
assurance_case:
  case_id: "case:internal-assistant/rc-2026-05-07"
  case_content_address: "sha256:6a1e..."
  discharges:                    # which case nodes this card supports
    - "goal:G1"
    - "goal:G1.S1.G-15-accuracy"
    - "goal:G1.S1.G-15-cybersecurity"
regime:                          # applicable regulatory / framework overlays
  eu_ai_act:
    system_category: "high-risk-annex-III-3(a)"
    articles: ["9", "10", "11", "13", "15", "17"]
  iso_iec_42001:
    clauses: ["6.1", "7.5", "8.1", "8.2", "9.1", "9.2"]
  iso_iec_42005:
    impact_assessment_id: "iai:internal-assistant/rc-2026-05-07"
    impact_assessment_content_address: "sha256:88af..."
  iso_iec_25059:
    quality_attributes_covered: ["functional-adequacy", "robustness", "user-controllability",
                                 "societal-and-ethical-risk-mitigation", "transparency"]
evidence_pointers:               # map claim-id -> evidence content-addresses
  claim:accuracy-primary:
    metric: "macro-F1"
    value: 0.912
    ci_95: [0.897, 0.926]
    evidence_content_address: "sha256:74a1..."
    sacm_artifact_id: "art:eval-report:rc-2026-05-07:gate-fa-01"
  claim:robustness-adversarial:
    metric: "attack-success-rate"
    value: 0.031
    ci_95: [0.019, 0.049]
    evidence_content_address: "sha256:c33d..."
    sacm_artifact_id: "art:redteam-report:rc-2026-05-07:gate-rb-02"
  # ... one entry per body-side claim
redaction_manifest:              # only present on non-public audience variants
  omitted_fields: []             # for the public variant
  # For a non-public variant, e.g.:
  # - path: "safety.attack_payloads"
  #   reason: "operational-security"
  #   available_to: ["regulator", "third-party"]
provenance:
  producer_signature:
    key_id: "assurance-team@example.corp"
    algorithm: "ed25519"
    signature: "..."
  rekor_log_index: 8123491
  c2pa_manifest:                 # for GenAI-output cards, chapter 06
    manifest_content_address: "sha256:d4e0..."
```

Six invariants the head has to hold, and that the release-gate walker will check at ingest:

- **`card.card_id` is unique per (subject, audience, version).** Two different audiences of the same version are two cards, not one card with a mode switch.
- **`subject.content_address` resolves in the evidence store.** A card that names a subject the store does not carry is not a card; it is a claim about a subject.
- **Every `evidence_pointers.*.evidence_content_address` resolves in the store**, and each is signed by a producer whose identity matches the evidence-contract routing (mod-102 chapter `06`; mod-104 chapter `01`).
- **`assurance_case.discharges` maps only to case nodes the assurance case itself carries.** If the case has no goal `G1.S1.G-15-accuracy`, the card cannot discharge it; the ingest fails.
- **`redaction_manifest` is complete on non-public variants.** Every difference between the public variant and this variant is enumerated. Chapter `07` returns to this rule.
- **The producer signature is over the canonicalised head + body pair.** Editing either invalidates the signature; there is no in-place edit primitive (see mod-104 chapter `01`).

The head is small on purpose. Everything the reviewer needs to do byte-level verification lives here; the body is where the reviewer reads the prose that explains what those digests mean.

## The body: human-readable sections, extended

The body extends the Mitchell / Gebru sections rather than replacing them. A reviewer who knows the base sections should be able to open an assurance card and find their bearings within the first minute; what has been added is *why* the section holds, not *what* the section claims. The extensions:

- **Intended purpose (extends Mitchell §2).** In addition to the intended users and use cases, name the deployment tiers permitted (mod-108), the jurisdictions this variant covers (mod-106), and the *appropriate-use boundary* — the set of use cases that the assurance case affirmatively demonstrates the system is fit for. Under the EU AI Act Article 3(12), "intended purpose" is a legally binding term; the section reads to that definition.
- **Foreseeable misuse (extends Mitchell §2 out-of-scope-use).** Enumerate the foreseeable misuse pathways drawn from the risk-engineering peer's harm inventory (mod-102 chapter `06`; the peer is `ai-risk-engineer`). Each misuse pathway names the mitigations shipped against it and the residual-risk position after mitigation.
- **Training and evaluation data (extends Gebru).** Under a regulator submission, the section carries the datasheet content-address, the eval-set integrity attestation content-address, and the contamination-attestation content-address (mod-104 chapter `05`). Under a public disclosure, the section may redact the eval-set names but must still declare that an integrity attestation exists — the redaction manifest names what was withheld.
- **Quality attributes (new).** A section structured around ISO/IEC 25059 quality dimensions (functional adequacy, reliability, robustness, user controllability, societal and ethical risk mitigation, transparency; chapter `05` walks these). Every quality attribute reports at least one metric with a threshold and a CI, and every threshold is bound to a case node.
- **Impact assessment (new).** The ISO/IEC 42005 impact assessment output summary, with pointers into the underlying impact-assessment artefact (chapter `04` walks this).
- **Safety-evidence summary (new).** A summary of red-team findings, guardrail evaluations, and residual-risk position. Written to survive an adversarial reviewer asking "what would falsify this claim?" Chapter `03` returns to this section when composing the system card.
- **Deployment-tier decision (new).** For frontier systems: the tier (per RSP / Preparedness / FSF, mod-108) the release has been assigned to, the evaluations that drove the assignment, and the operational constraints the tier imposes. For non-frontier systems: the deployment-mode decision (staff-only, controlled deployer set, general availability) and its rationale.
- **Post-market surveillance plan (new).** The Article 72 (EU AI Act) or GMLP / PCCP (FDA) post-market plan: what is monitored, what triggers escalation, who owns response. Mod-110 has the deep coverage; the assurance card carries the pointer.
- **Change-control commitments (new).** How the model / system / dataset is updated, what changes require re-issuing the card, and the retention horizon for the current version. For FDA-regulated systems, the PCCP boundary.
- **Provenance and disclosure discipline (new).** For GenAI systems: what content-provenance manifests are attached to outputs, how they are verified, and the disclosure position (which fields are omitted in which audience variant and why). Chapter `06` walks this.

The body is where the reviewer *reads*. The head is where the reviewer *verifies*. Every claim in the body has an `evidence_pointers.*` entry in the head. If the reviewer wants to check that a claim is defensible, they follow the pointer.

## The audience-variant contract

An assurance card is always a variant of a canonical case. Four audiences are worth naming outright; chapter `07` returns to the derivation.

- **Public.** The variant the world sees. Redactions favour disclosure — the presumption is that a field is present unless there is a named operational-security, personal-data, or trade-secret reason to omit it. The public variant is the *default template* against which every other variant is a diff.
- **Regulator submission.** The variant a market-surveillance authority (EU AI Act Article 74), a notified body (Article 43 conformity assessment), or an FDA reviewer sees. Redactions favour completeness — attack payloads, decontamination canaries, PII in eval sets are handled under confidentiality agreements rather than by omission. The variant carries every pointer the public variant redacts.
- **Third-party evaluator handoff.** The variant a UK AISI, NIST AISI, METR, Apollo, or an accredited notified body's evaluator receives. Redactions favour reproducibility — the reproducibility bundle (mod-104 chapter `03`) is available, but the evaluator is bound by an evaluation agreement not to leak canaries or PII. Chapter `07` and mod-109 walk this.
- **Board narrative.** The variant an internal board audience reads. Redactions favour brevity and interpretability — metrics are presented against thresholds and against the residual-risk position, not as raw eval outputs. The variant is short (often 8–15 pages) and structured around business decisions (whether to release, whether to pause, whether to escalate).

The invariant across all four: the *claims* in each variant are consistent with the same case; only the *level of disclosure* differs. If a public variant says "macro-F1 = 0.912" and a regulator variant says "macro-F1 = 0.897," the card is broken, or one of the variants is drawn from a different case. Chapter `07` treats the audience-variant derivation as a mechanical operation over the canonical case, not as separate authoring.

## Traceability to the assurance case (mod-102) and the evidence store (mod-104)

Every assurance-card claim is a leaf of the assurance case. Every leaf is a digest in the evidence store. The three-way binding is what makes the card defensible:

```
assurance case (mod-102)          assurance card (this module)          evidence store (mod-104)
────────────────────────          ──────────────────────────            ────────────────────────
Goal G1                                                                 
  └── Strategy S1 (per-Article)                                         
        └── Goal G1.S1.G-15-accuracy   ←→   body §quality-attributes   
                                              ↳ claim:accuracy-primary  ─── sha256:74a1... (eval record)
              └── Solution (evidence)   ←──────────────────────────────── sha256:74a1...
```

Read left to right, the case says "goal G1.S1.G-15-accuracy is discharged by an evidence node." Read right to left, the store says "digest `sha256:74a1…` was signed by the model-evaluation-engineer producer and records macro-F1 = 0.912 on `harm-eval-set/v3.2`." The card is the *human-readable middle* that a reviewer walks: they read the claim in the body, they follow the `evidence_pointers` entry to the digest, they verify the digest resolves in the store, and they cross-check the store's signature against the producer named in `evidence_contracts` (mod-102 chapter `06`). If any of the three legs breaks, the card is not defensible.

The rest of the module makes this concrete. Chapter `03` composes model + dataset + eval evidence + safety summary + tier decision into a single system card that walks this same three-way binding. Chapter `04` shows the same binding for an ISO/IEC 42005 impact-assessment output section. Chapter `05` walks it for the ISO/IEC 25059 quality-attribute spine. Chapter `06` extends it to C2PA content-provenance manifests for GenAI outputs. Chapter `07` closes with the audience-variant derivation.

## What the assurance card is *not*

Three things it is worth naming that the assurance card is not, because programs routinely conflate them.

- **The assurance card is not the assurance case.** The case is the *argument* (mod-102). The card is the *external-audience view* of the argument, specialised per reader. A card is derived from the case; the case is the load-bearing artefact.
- **The assurance card is not the release-gate decision.** The gate (mod-103) is the *decision* — a pass / fail with a signed bundle. The card is the *disclosure* of what the bundle contains. A card cannot make a release-gate decision; it can only report one.
- **The assurance card is not the compliance report.** A compliance report enumerates obligations discharged. The card carries claims about the system; the compliance report cross-tabulates those claims against a jurisdiction's obligations (mod-106). One card can feed many compliance reports.

Keeping these boundaries clean is what lets the card stay short enough to be readable and grounded enough to be defensible.

## Summary

- The assurance card is the base Mitchell / Gebru / HF card *plus* audience-tagged head/body separation, evidence-pointer bindings into the store, discharges-mapping into the assurance case, redaction-manifest discipline, producer signature, and — for GenAI — a C2PA manifest.
- The head is machine-readable and small; the body is human-readable and extends the Mitchell / Gebru sections with intended-purpose, foreseeable-misuse, quality-attributes, impact-assessment, safety-evidence, deployment-tier, post-market, change-control, and provenance-discipline sections.
- Four audiences (public, regulator, third-party evaluator, board) are variants of one canonical case; claims are consistent across variants and only disclosure levels differ.
- Every card is a three-way binding: claim in the body ↔ pointer in the head ↔ digest in the store ↔ solution in the case. Any leg missing is a defeater.
- The card is not the case, not the gate, not the compliance report. Chapters `03`–`07` walk each part of the shape in depth.
