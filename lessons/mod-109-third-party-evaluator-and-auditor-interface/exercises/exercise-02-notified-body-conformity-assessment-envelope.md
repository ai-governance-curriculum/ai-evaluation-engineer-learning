# exercise-02: Notified-Body Conformity Assessment Envelope

**Estimated effort:** 3 hours

## Objective

Assemble the **notified-body Annex VII dossier** for one worked high-risk AI system and design the **surveillance-audit calendar** that carries the certificate across its validity window. Produce the Annex IV technical documentation set, the Article 17 QMS documentation map, the internal-testing evidence index, the notified-body selection memo, and the substantial-modification handling procedure that keeps the certificate live release-to-release.

The exercise is design and authoring, not solving. Placeholder pointers and `<!-- needs-research: … -->` markers are legitimate answers where a fact would need to be verified against the consolidated Regulation text, an accredited notified body's current NANDO listing, or a specific harmonised standard's current published version.

## Prerequisites

- Chapter [`02-notified-body-conformity-assessment-under-eu-ai-act-article-43.md`](../02-notified-body-conformity-assessment-under-eu-ai-act-article-43.md) — the notified-body regime under Articles 30–31 and 43; the three dossier components (Annex IV, Article 17, internal-testing evidence); the audit-visit workflow; the interaction with ISO/IEC 42001 certification.
- Chapter [`06-delivery-timing-envelope-and-evidence-hardening-playbook.md`](../06-delivery-timing-envelope-and-evidence-hardening-playbook.md) — the engagement-charter template and the four evidence-hardening practices (digest-pin, sample-by-query, redact-per-audience, sign-the-envelope) that the notified-body dossier applies at scale.
- Familiarity with `mod-104` chapter `06` (assurance bundle) and `mod-104` chapter `05` (MLSec attestations) — the assurance bundle is the primary source; the Annex IV items are *views* onto the bundle.
- Familiarity with `mod-107` (sector-regulated assurance) where the deployment picked here has a sector overlay (medical device under EU MDR, financial services under DORA, etc.).
- Skim access to the consolidated text of Regulation (EU) 2024/1689 at [eur-lex.europa.eu/eli/reg/2024/1689/oj](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — specifically Articles 11, 17, 30, 31, 43, 47, and 72; Annex IV; and Annex VII.
- Skim access to the NANDO register at [ec.europa.eu/growth/tools-databases/nando/](https://ec.europa.eu/growth/tools-databases/nando/) <!-- needs-research: verify current NANDO URL for AI Act notified bodies -->.

## Problem statement

Pick one high-risk AI system for which the notified-body route is either mandatory or elected. Two constraints on the choice:

- **The choice must land in Annex III of the AI Act.** The notified-body route is a feature of the high-risk regime; low-risk systems do not require it.
- **The choice should exercise either the mandatory Annex VII route or an informed election of Annex VII over Annex VI.** Common shapes worth considering:
  - **Mandatory Annex VII.** A biometric-categorisation product (Annex III point 1) — the biometric category triggers the notified-body-mandatory subset <!-- needs-research: verify the exact biometric sub-points under the final consolidated text -->.
  - **Elected Annex VII with harmonised-standards divergence.** A CV-based ATS scoring tool for hiring (Annex III point 4) where the provider has partly diverged from a specific harmonised standard and elects Annex VII to discharge the divergence risk.
  - **Elected Annex VII with a sector overlay.** A creditworthiness scoring model (Annex III point 5) where the provider elects Annex VII because a Big-Four attest engagement (chapter `04`) already runs on the AIMS but a notified-body certificate is a customer-contract requirement.

Pin the system, the Annex III point, and the route election (mandatory vs elected) before you begin the artefact set.

## Requirements

Produce five artefacts in a single directory.

### 1. `system-and-route-brief.md`

A one-page brief that fixes:

- **System identity.** Named provider, named product, one-sentence position; the release candidate the initial dossier will cover; the model digest and the underlying foundation-model version (if the product is a downstream deployment of a third-party model).
- **Annex III classification.** The specific Annex III point and sub-point the system falls under. Concise legal-shape reasoning (one paragraph) — why the system meets the definition rather than sitting outside it.
- **Route selection.** Article 43 Annex VI (internal control) versus Annex VII (notified-body involvement). If mandatory, cite the specific biometric-category or other trigger. If elected, name the reason (harmonised-standards divergence, customer-contract requirement, prior-engagement reuse, board-visibility upgrade).
- **Harmonised standards claimed.** The specific harmonised standards the provider claims application of — ISO/IEC 42001, ISO/IEC 23894, ISO/IEC 24029-2, ISO/IEC 25059, and adjacent — with a note on any partial-application or divergence the dossier will need to defend.
- **Sector overlays.** Where a sector rule attaches (medical device MDR, financial services DORA, employment-context Colorado / NYC LL144 overlays per `mod-107`), the sector overlay is named. The notified-body's designated scope must accommodate the overlay's implications.
- **Assurance-programme context.** The `mod-104` chapter `06` assurance bundle's identifier for the release candidate, the `mod-102` chapter `04` assurance-case identifier, and the peer-role registry rows whose evidence will populate the dossier.

### 2. `notified-body-selection-memo.md`

A short memo (three to five pages) that documents the notified-body selection. Sections:

- **Shortlist.** Three notified bodies whose designated scope covers the release. For each, cite the NANDO identifier (four-digit number), the designating Member State, the specific harmonised standards the body is designated for, and one link into the body's public profile <!-- needs-research: verify current NANDO listings for AI Act notified bodies; the register is still stabilising -->.
- **Comparison table.** Columns: designated scope fit, competence-roster depth (AI-domain assessors and QMS assessors), geographic reach and working language, engagement-partner track record with providers of similar shape, indicative fees and timelines, surveillance-regime shape.
- **Selection.** The selected body and the reason. Score the selection on scope-fit and competence rather than on price (per chapter `02`'s selection guidance).
- **Contract touchpoints.** Fees, timelines, confidentiality of provider-internal data, the auditor's right to describe the audit methodology in the surveillance summary, the certificate's validity window, and the surveillance cadence during the window.
- **Backup-body plan.** Where the selected body cannot deliver (unavailability, loss of accreditation, scope contraction), the shortlist's second choice with the shortest re-engagement lead time.

### 3. `annex-iv-technical-documentation.md`

The Annex IV technical documentation set, structured section-by-section against the Annex IV items. For each Annex IV item:

- **Section title.** The Annex IV item as it appears in the consolidated Regulation (e.g., "general description of the AI system", "detailed description of the elements of the AI system and its development").
- **Content summary.** A short paragraph describing what the section covers for this system. Not the section's full text — enough for the notified body's assessor to see what is present.
- **Underlying assurance-bundle citations.** The specific `mod-104` chapter `06` assurance-bundle leaves the section cites, with digest pins. Cite `mod-104` chapter `03` reproducibility bundles for the internal-testing sections and `mod-104` chapter `04` ML-BOM entries for the data-provenance sections.
- **Harmonised-standards mapping.** The specific harmonised standards' clauses the section discharges (e.g., "risk-management system per Article 9 → ISO/IEC 23894:2023 clauses 5.2–5.5").
- **Peer-role owner.** Which peer role (`ai-risk-engineer`, `ai-eval-engineer`, `model-evaluation-engineer`, `ai-infra-security`, this programme) owns the underlying evidence.
- **Redaction pass.** Where any content is redacted for the notified-body audience versus the full internal bundle, note the redaction and its reason. Chapter `02`'s discussion of dossier assembly and chapter `06`'s redact-per-audience heuristic both apply.

Cover every Annex IV item; where an item is genuinely not applicable to the system, mark "not applicable — reasoning" rather than omitting it. The notified body reads the dossier's *completeness* as a signal about the QMS's operating maturity.

### 4. `article-17-qms-map.md`

The Article 17 QMS documentation map. This artefact maps every Article 17 requirement (strategy for regulatory compliance, techniques and procedures for design and design-control, techniques for development and quality control, examination and testing procedures, data-management procedures, risk-management system, post-market monitoring system, procedures for reporting serious incidents (Article 73), procedures for handling communications with authorities, record-keeping, and resource-management procedures) onto:

- **The AIMS clause it satisfies.** Where the provider maintains an ISO/IEC 42001 AIMS, the corresponding clauses 4–10 (and Annex A control(s) where applicable) that carry the substantive content.
- **The controlled-document identifier.** The AIMS controlled-documents register entry the notified body will inspect.
- **The peer-role owner.** Which peer role authors and maintains the document (usually the AI-governance analyst peer at level 15, per `mod-101` deferral contract).
- **The re-narration note.** Where the AIMS clause and the Article 17 requirement do not use the same terminology, a one-line re-narration note that maps the terminology so the notified-body assessor can cross-walk between them without re-authoring.

Where the provider does not maintain an ISO/IEC 42001 AIMS, this artefact is a bespoke QMS documentation index; the exercise's discipline is the same but the substrate is different. Note the trade-off in the memo (Article 17 versus AIMS clauses 4–10 converge on the same content, per chapter `02`'s interaction section).

### 5. `surveillance-and-substantial-modification-plan.md`

The plan for keeping the certificate live across its validity window. Sections:

- **Certificate lifecycle calendar.** The certificate's validity window (assume the maximum length permitted <!-- needs-research: verify current maximum certificate validity under the Act -->); the scheduled surveillance-audit dates (typically annual within the window); the certificate-renewal engagement-decision date (envelope-ready lead time — chapter `06` calibration — subtracted from the expiry).
- **Surveillance-audit envelope preview.** What the surveillance-audit envelope looks like at each surveillance interval — the sampled subset of the initial Annex IV / Article 17 evidence, plus evidence of any material changes since the previous audit. The evidence pipeline (`mod-104` chapter `06`) must be able to produce the sampled subset on demand.
- **Substantial-modification test.** The specific test the release-gate applies on every release candidate between certifications, per Article 43(4). Concrete triggers: material change to intended purpose, material change to training-data provenance, material change to the model architecture, material change to the deployment surface, material change to the guardrail set. For each trigger, the release-gate's disposition — pass, notify notified body, re-engage for supplementary assessment, block release pending re-certification.
- **Substantial-modification runbook.** The runbook the release-assurance on-call follows when a trigger fires: the immediate notification to the notified body, the evidence package the notification includes, the release-gate hold pending the notified body's confirmation of whether the modification is substantial, and the disposition based on the notified body's response.
- **Corrective-action integration.** How any surveillance-audit finding integrates with ISO/IEC 42001 clause 10.2 (nonconformity and corrective action) — the finding becomes an AIMS corrective-action entry, the entry is discharged by the peer-role owner, and the discharge evidence is available at the next surveillance interval.
- **Certificate-suspension or -withdrawal contingency.** What the programme does if the notified body suspends or withdraws the certificate — the immediate release-gate implication (block all in-scope release candidates), the escalation path (`head-of-ai-governance`, level 60), the remediation plan template, and the re-certification lead time.

## Starter guidance

- **Pin the Annex III point precisely.** Annex III's categories are structured; a system that lands in the wrong point will be reviewed by a notified body whose scope does not cover it. The one-paragraph legal-shape reasoning is where the point-fit is defended.
- **Route election is a decision, not a default.** Where Annex VI is available (most Annex III categories other than the biometric-mandate subset), electing Annex VII is a defensible choice for divergence-risk, customer-contract, or board-visibility reasons — but the choice should be documented, not assumed. The notified body reads the election reasoning as context.
- **The Annex IV dossier is a *view* onto the assurance bundle.** Chapter `02` is emphatic — where the `mod-104` chapter `06` bundle is well-instrumented, the Annex IV dossier is produced by transformation, not by re-authoring. The dossier's citations back to the bundle are the audit trail the notified body will walk in stage 1.
- **Harmonised-standards divergence is where the notified body earns their fee.** Where the provider claims application in full, Annex VI would suffice. Annex VII pays off when there is divergence to defend. The Annex IV dossier's harmonised-standards mapping should show the divergences explicitly.
- **The AIMS is the substrate that makes Article 17 tractable.** If the provider maintains an ISO/IEC 42001 AIMS, Article 17 is re-narration. If the provider does not, Article 17 is authoring from scratch — plan lead time accordingly (per chapter `06`'s envelope-ready lead-time calibration for notified-body engagements).
- **Surveillance is not one-and-done.** The programme designs the surveillance-audit envelope at initial certification, not at first surveillance. The `mod-104` evidence pipeline's ability to produce the sampled subset on demand is the primary determinant of surveillance cost.
- **The substantial-modification test is a release-gate criterion, not an occasional review.** Chapter `02` is emphatic — every release candidate is evaluated against the test. The exercise's discipline is designing the test explicitly, with concrete triggers and dispositions.
- **`<!-- needs-research: … -->` markers are legitimate.** The AI Act's implementing acts and harmonised standards are still stabilising; the NANDO register is still being populated for AI-Act-scope notified bodies. Where you would need the current published version of a specific instrument, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `system-and-route-brief.md` fixes the six scoping decisions (identity, Annex III classification, route selection, harmonised standards, sector overlays, assurance-programme context). A reviewer can decide, from the brief alone, whether Annex VII is mandatory or elected, and which harmonised standards the dossier's mapping will cite.
- `notified-body-selection-memo.md` presents a defensible shortlist of three notified bodies with NANDO identifiers, a comparison table, the selection and its reasoning, contract touchpoints, and a backup-body plan.
- `annex-iv-technical-documentation.md` covers every Annex IV item; each section names its content summary, assurance-bundle citations with digests, harmonised-standards mapping, peer-role owner, and redaction pass. Items genuinely not applicable are marked with reasoning.
- `article-17-qms-map.md` maps every Article 17 requirement onto its AIMS clause (where an AIMS exists) or its bespoke QMS document, with the controlled-document identifier, peer-role owner, and re-narration note.
- `surveillance-and-substantial-modification-plan.md` covers the certificate lifecycle calendar, the surveillance-audit envelope preview, the substantial-modification test with concrete triggers and dispositions, the substantial-modification runbook, the corrective-action integration, and the certificate-suspension contingency.
- The Annex IV dossier's citations resolve to specific `mod-104` chapter `06` assurance-bundle leaves rather than placeholder references — the dossier is a *view* onto the bundle, not a re-authored document.
- No peer-role dependency is anonymous — every underlying evidence source names the peer role (from the `mod-101` deferral contract) that owns it.
- Every place a fact would need to be verified against the consolidated Regulation text, a specific harmonised standard's current version, or a current NANDO listing is marked `<!-- needs-research: … -->`.
- The engagement charter template from chapter `06` is either present as an appended section or explicitly referenced from `surveillance-and-substantial-modification-plan.md` so a reviewer can see the timing discipline in operation.

## Stretch goals

- **Draft the stage-1 clarification exchange.** In `stage-1-clarification-exchange.md`, author two plausible stage-1 clarification requests the notified body might issue (a missing risk-management evidence citation; an ambiguity in the intended-purpose statement) and the programme's response.
- **Draft the stage-2 audit-walkthrough script.** In `stage-2-audit-walkthrough.md`, sketch the two-day remote audit's walkthrough script — which parts of the release-gate walker (`mod-103` chapter `01`), the evidence pipeline (`mod-104` chapter `01`), and the assurance-case store (`mod-102` chapter `04`) the QMS assessor is walked through, and which release-gate output artefacts are sampled.
- **Author the ISO/IEC 42001 crosswalk.** In `iso-42001-crosswalk.md`, produce the crosswalk between the Article 17 requirements and the ISO/IEC 42001 clauses 4–10 and Annex A controls, showing where the two converge and where the AI Act's requirements are additional.
- **Compose the EU declaration of conformity.** In `eu-declaration-of-conformity.md`, draft the Article 47 declaration the provider issues after the certificate is in hand — the specific fields (product identifier, harmonised-standards claim, notified body's identifier and certificate number, provider's signatory).
- **Add the post-market monitoring plan pointer.** In `post-market-monitoring-pointer.md`, sketch the Article 72 post-market monitoring plan for the same system — the specific signals monitored, the peer-role owner (foreshadowing `mod-110`), and the escalation trigger. Cross-reference `mod-110` where the surveillance-audit surface intersects with post-market monitoring.
- **Extend the substantial-modification test to a real release-gate criterion.** In `release-gate-substantial-modification-criterion.md`, express the substantial-modification test as a machine-checkable criterion in the release-gate walker's format from `mod-103` chapter `02` — the input signals, the disposition logic, and the artefact the criterion emits.
