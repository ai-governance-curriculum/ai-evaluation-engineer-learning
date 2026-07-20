# Notified-Body Conformity Assessment Under EU AI Act Article 43

## Motivation

The EU AI Act's high-risk conformity-assessment regime imports a well-established piece of EU product-safety machinery — the *notified body* — into AI governance. For most high-risk AI systems the provider can perform conformity assessment internally against Annex VI; but for a specific set of categories, and for any provider that chooses to use a harmonised-standards route with third-party involvement, a notified body is in the loop. When the notified body is in the loop, the release-assurance programme is producing evidence not for an AISI-shape technical evaluator (chapter `01`) nor for an internal auditor (`mod-104` chapter `06`) but for a *conformity-assessment body* whose competence, independence, and impartiality are themselves accredited under ISO/IEC 17065 and ISO/IEC 42006:2025.

The interface shape is different from AISI's in three concrete ways. First, the notified body reviews *documented evidence* against a standards checklist — Article 11 technical documentation, Article 17 QMS documentation, results of the provider's own internal testing — rather than running the system itself with novel payloads. Second, the notified body issues a *conformity certificate* whose lifecycle (issue, surveillance, renewal, suspension, withdrawal) has to be tracked by the release-assurance programme across the certificate's validity window, not just at engagement time. Third, the notified body's scope is bounded by their *notification* — the specific Annex III categories and standards they are competent to assess against — and the programme has to pick a notified body whose notification covers the release's scope.

This chapter walks what a notified body is, when the notified-body route is mandatory, what the notified body reviews, and what the release-assurance dossier and audit-visit workflow look like.

## What a notified body is

**Who they are.** Under the EU AI Act Article 30 (designating authorities and notified bodies), a notified body is a conformity-assessment body designated by an EU Member State's notifying authority to perform third-party conformity assessment under the Act. To be designated, the body must satisfy Article 31 (requirements relating to notified bodies) — competence, independence, impartiality, absence of conflict of interest — and must be accredited by a national accreditation body against ISO/IEC 17065 (requirements for bodies certifying products, processes and services). For AI-management-system certification against ISO/IEC 42001, the relevant certification-body standard is ISO/IEC 42006:2025 ([iso.org/standard/44546.html](https://www.iso.org/standard/44546.html)) — *Requirements for bodies providing audit and certification of artificial intelligence management systems*.

The Member State that designates the notified body assigns it a four-digit identification number and notifies the European Commission and the other Member States via the NANDO (New Approach Notified and Designated Organisations) system ([ec.europa.eu/growth/tools-databases/nando/](https://ec.europa.eu/growth/tools-databases/nando/)) <!-- needs-research: verify current NANDO URL and that AI Act notified bodies are listed there rather than under a separate register -->. The NANDO register lists each notified body's designated scope — the specific harmonised standards and Annex III categories they can assess against.

The European AI Office ([digital-strategy.ec.europa.eu/en/policies/ai-office](https://digital-strategy.ec.europa.eu/en/policies/ai-office)) is the Commission-level authority that coordinates the notified-body regime, publishes guidance, and (for GPAI systemic-risk providers under Article 55) handles supervision directly.

**What they ask for.** The notified body's dossier request follows the Article 43 procedure the provider has chosen and always includes Article 11 / Annex IV technical documentation, Article 17 QMS documentation, and evidence of the internal testing regime the provider ran before requesting third-party involvement.

**Handoff envelope.** A structured technical dossier (see below), a QMS documentation set, on-site or remote audit access to the QMS-relevant systems, and a per-engagement contract with the notified body covering fees, timelines, confidentiality, and the surveillance regime after certificate issue.

**Release-assurance implication.** Notified-body engagements produce a *certificate* that is itself an evidence-contract row in the assurance case (`mod-102` chapter `06`) with a validity window. The release-assurance programme has to track the certificate's lifecycle across every subsequent release cycle in the window — surveillance-audit outcomes, scope changes, substantial-modification notifications — and re-engage the notified body when the scope of a release exceeds the certificate's scope.

## When the notified-body route is mandatory

Article 43 (conformity assessment procedures) offers two tracks for high-risk AI systems in Annex III:

- **Annex VI — Internal control.** The provider performs conformity assessment internally: they draw up the technical documentation, apply their QMS, run internal testing, and issue an EU declaration of conformity themselves under Article 47.
- **Annex VII — Involvement of a notified body.** A notified body assesses the QMS and the technical documentation; on success, they issue an EU technical-documentation assessment certificate; the provider then issues the EU declaration of conformity.

For most Annex III categories, the provider *may choose* between Annex VI and Annex VII. Where the provider has applied the harmonised standards in full, Annex VI is available; where the provider has partly diverged from the harmonised standards, Annex VII is often the safer route because the notified body's certificate discharges the divergence risk.

For a specific set of categories the Annex VII route is *mandatory*. The categories where a notified body must be involved are the biometric-categorisation and remote-biometric-identification categories within Annex III — specifically the biometric use cases in Annex III point 1 (biometric identification and biometric categorisation of natural persons, and emotion recognition) <!-- needs-research: verify the exact Annex III sub-points that mandate notified-body involvement under the final consolidated text of Regulation (EU) 2024/1689 -->. For providers building in these categories, chapter `02` is not optional reading.

For GPAI systemic-risk providers (Article 55) the regime is different — supervision runs through the AI Office directly, with a different set of obligations covered in `mod-111`.

The consolidated text of the Regulation lives at [eur-lex.europa.eu/eli/reg/2024/1689/oj](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) and is the primary source for the article numbers used in this chapter.

## What the notified body reviews

The dossier the notified body reviews under Annex VII has three principal components:

### Article 11 / Annex IV technical documentation

**Who they are.** The notified body's assessors — a mix of AI-domain assessors and QMS assessors, per the body's competence roster.

**What they ask for.** The technical documentation set specified in Annex IV, which includes:

- General description of the AI system (intended purpose, versions, hardware requirements, deployment forms).
- Detailed description of the elements of the AI system and its development (methods and tools used, computational resources, training / validation / testing data provenance and characteristics, data-governance procedures, model-architecture description).
- Detailed description of the monitoring, functioning, and control of the AI system (performance metrics chosen, foreseeable unintended outcomes, human-oversight measures, technical measures to facilitate deployer interpretation).
- Detailed description of the risk-management system per Article 9.
- Description of any change made to the system through its lifecycle.
- List of harmonised standards applied in full or in part; where standards are not applied, description of solutions adopted to meet the requirements.
- Copy of the EU declaration of conformity.
- Detailed description of the post-market monitoring system per Article 72.

**Handoff envelope.** The Annex IV dossier is a structured document set. The release-assurance programme's assurance bundle (`mod-104` chapter `06`) is the primary source — the Annex IV items are *views* onto the bundle, filtered and re-narrated for the notified-body audience. Where the bundle carries a digest, the Annex IV dossier cites the digest so the notified body can walk the evidence pipeline directly.

**Release-assurance implication.** The Annex IV dossier is the largest single documentary deliverable the programme produces. The clarity, cross-referencing, and evidentiary depth of the bundle (`mod-104`) determines how much rework the Annex IV dossier requires. A well-instrumented bundle produces a dossier by transformation, not by re-authoring.

### Article 17 QMS documentation

**Who they are.** The notified body's QMS-assessor role.

**What they ask for.** The provider's quality-management-system documentation covering the elements Article 17 enumerates — strategy for regulatory compliance, techniques and procedures for design and design-control, techniques for development and quality control, examination and testing procedures used before, during, and after development, data-management procedures, risk-management system, post-market monitoring system, procedures for reporting serious incidents (Article 73), procedures for handling communications with authorities, record-keeping, and resource-management procedures.

**Handoff envelope.** The QMS documentation is typically produced by the analyst peer (`ai-governance-analyst` at level 15, per `mod-101` deferral contract) and elevated by the release-assurance programme. Where the provider maintains an ISO/IEC 42001 AI Management System, the AIMS clauses 4–10 documentation is the natural source and Article 17 is a re-narration.

**Release-assurance implication.** Article 17 is the reason why an AI Management System (`mod-104` chapter `06`) is worth building even for providers whose primary regulatory exposure is the EU AI Act. The QMS documentation Article 17 requires and the AIMS clauses 4–10 documentation the ISO/IEC 42001 auditor requires converge on the same content.

### Results of internal testing

**Who they are.** The notified body's technical assessor.

**What they ask for.** Evidence that the provider ran the internal testing regime the QMS requires before requesting third-party assessment — the reproducibility bundles, evaluation reports, red-team reports, guardrail-eval reports, and the pre-release release-gate output artefact.

**Handoff envelope.** The `mod-104` chapter `06` signed assurance bundle, plus an index that maps the bundle's contents onto the Annex IV / Article 17 fields.

**Release-assurance implication.** The internal-testing evidence is where the notified body confirms that the QMS is operating, not merely documented. A gap between what the QMS says the provider does and what the assurance bundle shows the provider did will surface here.

## Selecting the right notified body

Selection is not perfunctory. Three attributes matter and are worth checking before contract signature:

- **Designated scope.** The NANDO entry lists the specific Annex III categories and harmonised standards the notified body is designated to assess against. A notified body whose scope does not cover the release's Annex III category cannot issue the certificate. Scope is checkable from the NANDO record directly.
- **Competence roster.** The notified body's competence roster must include AI-domain assessors *and* QMS assessors. For AIMS-scope work under ISO/IEC 42006:2025, the body's accreditation-body attestation should be current.
- **Geographic reach and language.** Notified bodies operate primarily in the language(s) of their designating Member State and may charge additional fees for engagements conducted outside that language or across time zones.

The programme's typical practice is to shortlist three notified bodies whose designated scope covers the release, request proposals covering fees / timelines / surveillance regime, and select on scope-fit and competence rather than on price. The engagement is multi-year (initial certificate plus surveillance across the validity window) and price differences between competent notified bodies are small relative to the cost of switching bodies mid-window.

## The audit-visit workflow

Once the dossier lands, the notified body typically proceeds through a stage-1 review (documentary), a stage-2 audit (on-site or remote review of the QMS in operation), a technical-documentation assessment, and — on success — issue of the certificate. The release-assurance programme's role at each stage:

- **Stage 1 (documentary).** Respond to clarification requests, provide additional evidence citations from the bundle, correct any factual errors in the dossier. Turnaround is measured in days.
- **Stage 2 (QMS audit).** Escort the QMS assessor through the programme's operating procedures — release-gate walker (`mod-103` chapter `01`), evidence pipeline (`mod-104` chapter `01`), assurance-case store (`mod-102` chapter `04`), incident-response procedure. The assessor typically samples release-gate output artefacts across a period and walks the evidence pipeline to confirm the artefacts are integrity-protected.
- **Technical-documentation assessment.** Respond to the technical assessor's specific questions on the AI-system methodology, harm modelling, and testing regime. The risk engineer, model-evaluation engineer, and AI-eval engineer peers (`mod-101` deferral contract) support the responses; the programme owns the response-package assembly.
- **Certificate issue.** The notified body issues the EU technical-documentation-assessment certificate (Annex VII). The certificate is a controlled document under ISO/IEC 42001 clause 7.5 and lands in the AIMS controlled-documents register alongside the release-gate output artefacts (`mod-104` chapter `06`).
- **Surveillance.** Notified bodies conduct surveillance audits during the certificate's validity window. The programme has to produce the same class of evidence at surveillance as at initial certification, plus evidence of any material changes since the certificate was issued.
- **Substantial modification.** Where a release constitutes a *substantial modification* under Article 43(4), the provider has to notify the notified body and, depending on the modification's scope, may require a fresh conformity assessment. The release-gate has a criterion here (`mod-103`): every release candidate is evaluated against the substantial-modification test before promotion.

## Worked example — a biometric-categorisation product's Annex VII dossier

A provider is releasing a biometric-categorisation product that infers demographic attributes from facial images. Annex III point 1 classifies the product as high-risk and the biometric-category-specific mandate triggers the Annex VII notified-body route.

The release-assurance programme prepares the dossier:

1. **Notified-body selection.** Programme queries NANDO for notified bodies whose designated scope covers biometric categorisation under the EU AI Act; shortlists three; selects one whose competence roster includes both biometric-AI assessors and QMS assessors familiar with ISO/IEC 42001. Engagement contract signed, covering fees, timelines, confidentiality, and the surveillance regime.
2. **Annex IV technical documentation.** Assembled from the assurance bundle for release candidate `rc-2026-05-07`. Sections include the general description of the product, the training-data provenance (ML-BOM references from `mod-104` chapter `04`), the model-architecture description, the risk-management system per Article 9 (harm inventory v3 from `ai-risk-engineer`), the harmonised-standards conformance list (ISO/IEC 24029-2, ISO/IEC 25059, ISO/IEC 23894, ISO/IEC 42001), the post-market monitoring plan (`mod-110`), and the demographic-differentials measurement report (`ai-risk-engineer` fairness evidence).
3. **Article 17 QMS documentation.** The provider's ISO/IEC 42001 AIMS documentation, re-narrated as the Article 17 fields. Where a QMS clause matches an AIMS clause verbatim, the dossier cites the AIMS section by clause and paragraph.
4. **Internal-testing evidence.** The `mod-104` chapter `06` assurance bundle for the release candidate, with an index mapping bundle contents onto Annex IV / Article 17 fields.
5. **Stage-1 review.** The notified body's documentary assessor issues twelve clarification requests over four weeks; the programme responds with pointers into the bundle and, in three cases, produces supplementary evidence.
6. **Stage-2 audit.** Two-day remote audit; QMS assessor walks the release-gate walker (`mod-103`), samples six release-gate output artefacts from the last six months, verifies each artefact's signatures and Rekor entries, interviews the release-assurance on-call.
7. **Technical-documentation assessment.** Technical assessor spends three weeks on the demographic-differentials report and the model-architecture description; issues seven follow-up questions; the programme responds with methodology detail from the model-evaluation engineer.
8. **Certificate issue.** The notified body issues the EU technical-documentation-assessment certificate, valid for five years <!-- needs-research: verify current maximum certificate validity under the Act -->, scoped to the product family and the release candidate. The certificate lands in the AIMS controlled-documents register and is cited by the release-gate case as an external-evaluator leaf.
9. **Ongoing.** The programme sets up a surveillance-audit calendar entry, a substantial-modification test in the release-gate, and a certificate-renewal reminder eighteen months before expiry.

The programme's evidence pipeline (`mod-104`) is the substrate that keeps the audit-visit workflow tractable. Where the pipeline can produce digest-pinned samples on demand, the stage-2 audit runs in days rather than weeks; where it cannot, the notified body's cost estimate and timeline both slip.

## Interaction with ISO/IEC 42001 certification

A related but distinct interface worth naming is *ISO/IEC 42001 certification* by an accredited certification body under ISO/IEC 42006:2025. This is not the same engagement as an EU AI Act notified-body engagement, but the two interfaces overlap substantially:

- **Certification body vs notified body.** An ISO/IEC 42001 certification body is accredited to certify AIMS conformance under ISO/IEC 42006:2025; an EU AI Act notified body is designated to perform conformity assessment against the Act. The same organisation may hold both accreditations, but the two engagements are separate contracts with separate deliverables.
- **AIMS scope vs product scope.** ISO/IEC 42001 certification is *organisation-scoped* to the AI Management System; EU AI Act notified-body assessment is *product-scoped* (or product-family-scoped) to the AI system being placed on the market.
- **Complementary evidence.** An organisation with a certified AIMS produces evidence that can be reused (with re-narration) in the Article 17 QMS section of an Annex VII dossier; a notified body may accept AIMS certification as evidence of QMS competence but is not obliged to.

The release-assurance programme's typical practice is to pursue both: ISO/IEC 42001 certification for the AIMS and notified-body assessment per Article 43 for each in-scope product. The two audit calendars are coordinated so evidence produced for one is available to the other.

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the notified-body row in the external-parties section is the ancestor of this chapter's dossier.
- `mod-102` (assurance case) — notified-body certificates appear as external-evaluator leaves with validity windows.
- `mod-103` (release-gate) — the substantial-modification test is a release-gate criterion for products under an Annex VII certificate.
- `mod-104` (evidence pipeline) — the assurance bundle is the primary source for Annex IV dossier assembly.
- `mod-105` (cards) — the EU declaration of conformity is one of the artefacts elevated for the deployer audience.
- `mod-106` (cross-jurisdictional mapping) — the EU AI Act column of the crosswalk cites Article 43 for the conformity-assessment route selection.
- `mod-110` (post-market surveillance) — the Article 72 post-market monitoring plan is a required part of the Annex IV dossier.
- `mod-111` (GPAI systemic-risk) — for GPAI systemic-risk providers, the AI Office supervises directly rather than through notified bodies; the interface shape shifts accordingly.
- `mod-112` (programme ownership) — the notified-body certificate is a standing artefact the programme charter tracks across cycles.

## Summary

- A notified body under the EU AI Act is a conformity-assessment body designated by an EU Member State under Article 30, accredited against ISO/IEC 17065 and (for AIMS-scope certification bodies) ISO/IEC 42006:2025, and listed in the NANDO register.
- Article 43 offers two conformity-assessment routes: Annex VI (internal control) and Annex VII (notified-body involvement). Annex VII is mandatory for biometric-categorisation and remote-biometric-identification categories in Annex III.
- The notified body reviews the Article 11 / Annex IV technical documentation, the Article 17 QMS documentation, and the results of the provider's internal testing.
- The audit-visit workflow proceeds through stage 1 (documentary), stage 2 (QMS audit), technical-documentation assessment, certificate issue, surveillance, and substantial-modification handling.
- The release-assurance programme's assurance bundle (`mod-104` chapter `06`) is the primary source; the Annex IV dossier is a view onto the bundle, and the certificate is a validity-windowed leaf in the case.
- Exercise `02` has you assemble a notified-body Annex VII dossier for a worked biometric-categorisation product and design the surveillance-audit calendar.
