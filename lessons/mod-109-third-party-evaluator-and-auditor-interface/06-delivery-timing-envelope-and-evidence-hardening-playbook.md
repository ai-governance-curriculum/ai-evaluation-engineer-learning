# Delivery Timing, Envelope, and Evidence-Hardening Playbook

## Motivation

Chapters `01` through `05` walk four distinct third-party interfaces (AISI-shape technical evaluators, EU AI Act notified bodies, NYC AEDT independent bias auditors, Big-Four attest firms) and one worked-example public-sector precedent (NIST FRVT/FRTE). Each interface has a different disclosure profile, a different reviewer, a different regulatory mandate, and a different notion of what "good" evidence looks like. Read chapter-by-chapter they can feel like four unrelated engagements the programme happens to run in parallel.

They are not. Underneath the surface differences sits a shared operating discipline the release-assurance programme has to run *for every third-party engagement it accepts*, without which any of the four engagements can degrade in the same predictable ways — deadlines missed because the calendar was set inside the engagement rather than outside it, dossiers rejected because the evidence was assembled in a hurry rather than continuously, engagements re-scoped mid-flight because the envelope had a component nobody owned. This chapter names that discipline and gives the programme a playbook that survives across evaluator types.

Three failure modes recur often enough at first-time engagements that the playbook is worth spelling out explicitly:

- **Timing collapse.** The engagement's calendar is set from the evaluator's needs alone, without accounting for the release-gate's own promotion windows or the programme's own evidence-assembly lead times. The programme is scrambling in weeks four through seven of an eight-week engagement, and the evaluator's report lands after the release-gate has already had to decide.
- **Envelope drift.** The delivery envelope's components are enumerated at intake but no single named owner accepts every component. When the engagement ships, one component is missing (the DSSE-signed manifest, the redacted safety-case draft, the credential-scoping attestation), and the evaluator's stage-1 review returns a request for it a week later.
- **Evidence softness.** The programme's evidence pipeline (`mod-104`) is used for internal release-gate consumption and never stress-tested against an external reviewer's provenance and sampling expectations. Under external scrutiny the evidence turns out to be present but not integrity-protected, or integrity-protected but not indexed, or indexed but not reproducible; the engagement's assurance level is downgraded or the engagement is delayed.

The chapter's playbook is designed against those three failure modes. Its content is not new — every component below has already been touched in `mod-104` (evidence pipeline), `mod-102` (assurance case), `mod-103` (release-gate), and the four interface-specific chapters — but this is where the components are pulled into a *single reusable third-party-engagement operating procedure* the programme can apply on intake without re-authoring for each new engagement type.

## The three shared disciplines

The playbook rests on three disciplines the programme applies to every third-party engagement regardless of the evaluator's shape:

- **Delivery timing** — the calendar the engagement runs on, back-planned from the evaluator's report-delivery date to the programme's own preparation lead times, and cross-referenced with the release-gate cadence so the report actually informs the release-gate decision it was scheduled to inform.
- **Delivery envelope** — the enumerated set of artefacts, credentials, access channels, and controlled documents the programme hands the evaluator, with a named owner for each component and an intake checklist a reviewer can run against.
- **Evidence hardening** — the discipline that turns internally-adequate evidence into externally-defensible evidence: provenance chains that survive external sampling, redaction that preserves the shape of the harm inventory while protecting commercially-sensitive detail, and integrity attestations that a third-party reviewer will accept without re-attesting them themselves.

The three braid: timing determines when evidence has to be hard enough to hand over; the envelope enumerates what has to be handed over; hardening is what makes the envelope's contents survive the evaluator's review. A programme that has one discipline strong and two weak will fail the engagement predictably in the two weak dimensions.

## Delivery timing

### Back-planning from the report-delivery date

The engagement's fixed point is the evaluator's report-delivery date, not the engagement's start date. Report-delivery is fixed by the evaluator's own resourcing (an AISI-shape institute's evaluation cycle, a notified body's stage-1/stage-2 sequencing, an AEDT auditor's methodology cadence, a Big-Four firm's engagement partner's calendar) and is difficult to move once contracted. The programme's calendar back-plans from that date.

Four milestones sit between engagement start and report delivery, and the programme's calendar names each one with an owner and a slack budget:

- **Envelope-ready.** All components of the delivery envelope (see below) are assembled, cross-checked, and owner-signed. This is the earliest date at which the evaluator can meaningfully begin review. Programme owns the milestone.
- **Kick-off.** Envelope handed to the evaluator; evaluator's team briefed on the deployment context, the assurance case's shape, and the reproducibility bundle's structure. Programme owns the kick-off; evaluator owns the acknowledgement.
- **Mid-engagement checkpoint.** Structured evaluator-programme review — typically at 40–60% of the engagement window — where the evaluator flags any missing evidence, requests supplementary material, or clarifies scope. Evaluator owns the agenda; programme owns the response.
- **Draft-review window.** The evaluator's draft findings or report land; the programme reviews for factual accuracy (not for methodology negotiation — see the AEDT independence discussion in chapter `03` and the notified-body confidentiality discipline in chapter `02`); corrections are exchanged. Evaluator owns the draft; programme owns the factual-corrections response with a fixed turnaround.

The report-delivery date sits after the draft-review window closes and after the evaluator's own final-issue procedures complete. The programme's own release-gate window sits *after* report-delivery — never before, never coincident. A release-gate that has to decide before the report is in is a release-gate that cannot cite the engagement's evidence, and the engagement was scheduled against the wrong gate.

### The programme's lead time — envelope-ready is not free

The envelope-ready milestone is where first-time programmes underestimate their own lead time. Assembling a delivery envelope for an AISI-shape engagement, a notified-body Annex VII engagement, or a Big-Four ISAE 3000 (Revised) reasonable-assurance engagement is not a two-day exercise. Realistic lead times, calibrated against the four interface types:

- **AISI-shape engagement (chapter `01`).** Six to twelve weeks between engagement decision and envelope-ready, assuming the reproducibility bundles from `mod-104` chapter `03` already exist for the release candidate being handed over. First-time engagements (a new AISI institute, a new deployment surface, no prior reproducibility-bundle discipline) sit at the top of the range.
- **Notified-body Annex VII engagement (chapter `02`).** Eight to sixteen weeks between engagement decision and envelope-ready, driven primarily by the Annex IV technical-documentation assembly and the Article 17 QMS documentation set. Where an ISO/IEC 42001 AIMS is in place, the range compresses toward the lower end because Article 17 is a re-narration of AIMS clauses 4–10.
- **AEDT independent bias audit (chapter `03`).** Four to eight weeks between engagement decision and envelope-ready, driven by dataset assembly, category-tagging completeness, and the historical-data option's documentation.
- **Big-Four attest engagement (chapter `04`).** Six to twelve weeks between engagement decision and envelope-ready, driven by control-library mapping and the evidence-pipeline readiness for sample retrieval on demand.

Envelope-ready is *not* the same as engagement-ready-in-principle. Engagement-ready-in-principle is when the programme has decided to run the engagement; envelope-ready is when the evaluator can begin review. The gap between the two is the programme's own preparation work and it is under-forecast on first-time engagements roughly always.

### Cross-referencing the release-gate cadence

The programme's release-gate cadence (`mod-103`) sets the outer envelope of when the engagement's report can be usefully consumed. Four cross-references matter:

- **Report before promotion.** For engagements whose report is a hard-gate leaf (AISI-shape at tier 3, notified-body certificate for a mandated Annex III category, AEDT audit for a hiring product covering NYC-resident candidates), the report-delivery date must precede the release-gate's promotion window for the corresponding release candidate. Missing this cross-reference produces a released product that cannot cite the engagement's evidence.
- **Report before disclosure.** For engagements whose report content flows into an external card (`mod-105`) or an external filing, the report-delivery date must precede the card's or filing's cut-off. Chapter `04`'s worked example of the ISAE 3000 (Revised) opinion, chapter `03`'s worked example of the AEDT summary posting, and chapter `02`'s worked example of the EU declaration of conformity all sit on this cross-reference.
- **Certificate validity window.** For engagements whose output has a validity window (notified-body certificates, attest opinions with period-of-time scope, AEDT audits with a one-year re-audit obligation), the release-assurance calendar carries a *re-engagement reminder* keyed to the window's expiry minus the corresponding envelope-ready lead time. Missing this cross-reference produces a certificate lapse where the release-gate cannot pass.
- **Substantial-modification test.** For engagements where a material change to the system between engagement and release invalidates the report (notified-body Annex VII per Article 43(4), some attest engagements' subsequent-events considerations), the release-gate carries a substantial-modification test on every release candidate between report-delivery and the next scheduled engagement.

The four cross-references live in the programme's engagement calendar as first-class entries, not as reminders in the release-assurance owner's personal notes.

### Failure mode — timing collapse

Timing collapse presents as an on-call scramble in the last third of the engagement window. Typical anatomy: the engagement's start date was set on the evaluator's calendar; the programme's own envelope-ready milestone was implicit rather than named; the reproducibility bundles for the release candidate turn out to require re-generation; the redacted safety-case draft has not been reviewed by legal; the credentialed-access scoping requires coordination with `ai-infra-security` (level 35, per `mod-101` deferral contract) whose on-call did not know the engagement existed; and the evaluator is asking follow-up questions the programme cannot answer because their staff were pulled into other releases.

The playbook's discipline against timing collapse is the back-planned calendar with named owners and named slack budgets on each milestone. The slack budget matters: a milestone whose planned duration matches its expected duration has zero slack and will slip on any unplanned event. A five-day milestone with a two-day slack budget absorbs a one-week evaluator clarification without cascading; a milestone with no slack cascades on the first delay.

## Delivery envelope

### The seven components

The delivery envelope is the enumerated set of artefacts, credentials, access channels, and controlled documents the programme hands the evaluator. Every third-party engagement the programme runs has seven components. The components' contents differ by engagement type; the *structure* does not.

- **Deployment-context statement.** A short, structured document that names the AI system under evaluation, its deployment surface, its user population, its tool-use surface, its data-access surface, and its position in the enterprise's deployment-tier scheme (`mod-108`). Chapter `01`'s AISI worked example, chapter `02`'s Annex IV general-description section, chapter `03`'s AEDT scope memo, and chapter `04`'s subject-matter statement are all specialisations of this component. The evaluator uses it to orient their review.
- **Deployment-tier framework document.** The enterprise's own tier scheme (`mod-108` chapter `05`) or the tier-decision artefact for the specific release candidate under evaluation. Chapter `01`'s AISI worked example calls this out explicitly; chapter `02`'s Annex IV risk-management-system section incorporates it; chapter `04`'s NIST AI RMF crosswalk uses it as the criteria context. Shared under the mutual NDA where the tier scheme is confidential.
- **Assurance case draft or excerpt.** The relevant portion of the SACM `ArgumentPackage` from `mod-102` chapter `04`, redacted of any commercially-sensitive harm-inventory detail the evaluator does not need. Chapter `01`'s "draft safety case" and chapter `02`'s Annex IV risk-management-system section are the two most-common shapes. The redaction discipline is discussed in the evidence-hardening section below.
- **Reproducibility bundles for provider-side evaluations.** The `mod-104` chapter `03` bundles for whichever provider-side evaluations the evaluator needs to triangulate against — functional-adequacy, robustness, safety, fairness, capability-elicitation — depending on the engagement's scope. Chapters `01`, `02`, and `04` all consume these; chapter `03` (AEDT) substitutes the audit input dataset for reproducibility bundles because the DCWP methodology is prescribed.
- **Credentialed access channel.** Where the engagement includes evaluator-run testing (AISI-shape, some Big-Four attest examinations), a dedicated credentials set scoped to a pinned model version, with a bounded evaluation window, rate limits, and log-store segregation. Owned jointly with `ai-infra-security` (level 35). Where the engagement is documentary-only (notified-body Annex VII stage 1, some Big-Four advisory scopes), this component is present but empty — noted as "not applicable to this engagement type" rather than omitted, so the checklist remains uniform across engagement types.
- **QMS or AIMS documentation excerpt.** For engagements against ISO/IEC 42001 clauses 4–10 or EU AI Act Article 17 QMS documentation, the relevant AIMS-clause excerpts. Chapter `02` and chapter `04` both consume this component; chapters `01` and `03` typically do not, and mark the component "not applicable" rather than omitting it.
- **Return channel and provenance manifest.** The manifest describing how the evaluator returns their report to the programme — the signed-artefact expectation, the digest-pinning requirement against the model version tested, the transparency-log entry (Rekor, or equivalent) where applicable, the ingestion path into the `mod-104` chapter `06` assurance bundle, and the release-gate leaf-identifier the report will populate. Every engagement has this component; its content differs by engagement type but the *shape* is invariant.

The seven-component structure is deliberately uniform across engagement types. Uniformity is what makes the intake checklist reusable, the owner assignments transferrable, and the completeness review mechanical rather than judgement-heavy.

### One owner per component, always

Every component has a single named owner. Named — not a role, not a team, not a substitute-if-unavailable. The seven ownership rows sit in the engagement's charter and are re-confirmed at kick-off. Typical owner assignments, calibrated against the peer-role registry from `mod-101` deferral contract:

- **Deployment-context statement.** Release-assurance methodology owner (this programme).
- **Deployment-tier framework document.** Release-assurance methodology owner (this programme), co-signed by head of AI governance (level 60) where the tier scheme is being handed to a new evaluator for the first time.
- **Assurance case draft or excerpt.** Release-assurance methodology owner (this programme), with the specific claims and evidence-contract rows referenced by peer-role owner (ai-risk-engineer for harm-inventory-derived claims, ai-eval-engineer for evaluation-derived claims, model-evaluation-engineer for measurement-derived claims).
- **Reproducibility bundles.** Owned by the peer role that produced each bundle (`mod-101` deferral contract), with the release-assurance programme owning the *aggregation* into the delivery envelope.
- **Credentialed access channel.** Owned jointly by the release-assurance programme (scope, window, log-store segregation) and `ai-infra-security` (level 35 — credential issuance, IAM enforcement, revocation).
- **QMS or AIMS documentation excerpt.** Owned by the AI-governance analyst peer (level 15, per `mod-101` deferral contract) with re-narration for the specific engagement handled by the release-assurance programme.
- **Return channel and provenance manifest.** Release-assurance methodology owner (this programme), with the transparency-log entry owned jointly with `ai-infra-security`.

The rows go into the engagement charter with a *primary* and a *backup* owner named for each component. Backup owners are named for continuity — a component whose owner is unavailable at the kick-off date but has no named backup will slip the envelope-ready milestone.

### The intake checklist

Every component has three checklist items applied at envelope-ready:

- **Present.** The component's artefact(s) exist in the pre-agreed location, in the pre-agreed format.
- **Current.** The component's artefact(s) are pinned to the release candidate under evaluation — not to a prior candidate, not to a template, not to an outdated snapshot.
- **Signed.** The component's artefact(s) carry the integrity attestation the engagement's provenance manifest requires — DSSE signature, in-toto attestation, or the engagement-specific equivalent.

Twenty-one checklist items per envelope, applied by the release-assurance on-call at envelope-ready and independently reviewed by the primary owner of the return-channel-and-provenance-manifest component (which is the release-assurance methodology owner themselves — so the discipline is that the release-assurance on-call *and* the methodology owner both sign the checklist before the envelope is released to the evaluator).

Where an item fails the checklist, the failing component is *fixed* before the envelope ships. The checklist is not a self-report; it is a gate. An envelope-ready milestone that ships with any of the twenty-one items unsigned is a milestone that has not been met, and the calendar's slack budget starts to erode.

### Failure mode — envelope drift

Envelope drift presents as a stage-1 clarification request from the evaluator asking for a component the programme thought had shipped. Typical anatomy: the envelope was ready in principle at kick-off but one component (usually the credentialed-access channel, the QMS documentation excerpt, or the return-channel provenance manifest) was owned by a team not in the kick-off; the component was not on the intake checklist; the evaluator's stage-1 review surfaces the gap a week in; the programme's on-call spends the following week chasing the missing component while the evaluator's clock keeps ticking.

The playbook's discipline against envelope drift is the seven-component structure with named owners and the twenty-one-item intake checklist. The checklist's role is to make missing components mechanically detectable at envelope-ready rather than politically detectable a week into stage 1.

## Evidence hardening

### What "hard enough" means

Evidence that is adequate for internal release-gate consumption is not always adequate for external third-party review. Three axes distinguish internally-adequate from externally-defensible:

- **Provenance chain.** Internal consumers trust the pipeline that produced the evidence because they operate it; external reviewers do not. Externally-defensible evidence carries a provenance chain the reviewer can walk from the source system to the artefact, without the programme's staff having to re-narrate it.
- **Redaction discipline.** Internal consumers see the full harm inventory and the full commercial context; external reviewers see a redaction shaped by the disclosure profile. Externally-defensible redaction preserves the *shape* of what is being described (the harm inventory's structure, the evaluation set's coverage, the tier scheme's axes) while withholding *specific commercially-sensitive detail* the reviewer does not need. Over-redaction is a common failure mode discussed in chapter `01`'s AISI worked example.
- **Integrity attestation.** Internal consumers rely on the pipeline's operational integrity; external reviewers require cryptographic attestation. Externally-defensible evidence carries the `mod-104` chapter `05` MLSec attestation set — eval-set-integrity, exfiltration control, ML-BOM SPDX/SLSA/Sigstore packaging (per `mod-104` chapter `04`) — with signatures that verify against public keys the reviewer can obtain independently.

The three axes braid: a provenance chain the reviewer cannot walk is a chain that does not exist; a redaction the reviewer sees through is a redaction that did not preserve the shape; an integrity attestation the reviewer cannot verify is not an attestation at all. Evidence is hard when the reviewer can accept it without re-attesting.

### The hardening discipline

Four practices produce externally-defensible evidence from the `mod-104` evidence pipeline:

- **Digest-pin every leaf.** Every artefact in the delivery envelope references the release candidate's model digest, the harness's commit hash, the eval-set descriptor's identifier, and the pipeline-run identifier. Chapter `01`'s AISI return-channel provenance and chapter `02`'s Annex IV cross-referencing both depend on this. Un-digested leaves force the reviewer to accept "trust me" evidence.
- **Sample by query, not by curation.** The evidence pipeline (`mod-104`) supports on-demand sampling by evaluation criterion, release candidate, and time window. When the reviewer requests a sample ("show me evidence that release-gate criterion X operated on release candidates over the last twelve months, sampled to Y"), the sample is retrieved by pipeline query — not curated by hand. Chapter `04`'s discussion of attest engagement cost turns on this discipline. Hand-curated samples are indistinguishable from cherry-picked samples in a reviewer's eyes.
- **Redact the detail, preserve the shape.** Redaction removes commercially-sensitive specifics (customer names, competitive positioning, specific attack payloads per chapter `01`) but preserves the *structure* of what is being described. A redacted harm-inventory row shows the harm class, the deployment surface, the mitigation family, and the peer role that owns the evidence, even if the specific customer or specific commercial context is redacted. A redacted assurance-case leaf shows the claim, the evidence-contract row's shape, and the reviewer's peer analogue, even where the specific quantitative result is redacted for a not-yet-published release. Chapter `01`'s AISI worked example's safety-case redaction and chapter `02`'s Annex IV harmonised-standards divergence sections both apply this practice.
- **Sign the entire envelope, not just leaves.** The delivery envelope carries a signed manifest (DSSE envelope or equivalent) listing every artefact by digest and every credentialed-access endpoint by identifier. The signed manifest is what the reviewer verifies once at intake; the individual artefact signatures are what the reviewer verifies on sampling. Both layers are present; both layers are the release-assurance methodology owner's signature (or their delegate's, named in the envelope) and, where the engagement's provenance requirements are heavier, co-signed by `ai-infra-security` (level 35).

The four practices are not evaluator-specific — they apply uniformly across AISI-shape, notified-body, AEDT, and Big-Four engagements. The specific attestation formats and the specific redaction targets differ by engagement type; the discipline does not.

### Redaction as a discipline the assurance case has to survive

Redaction is easy to over-apply and hard to un-apply. Programmes learning this discipline often start over-redacted (removing too much detail, leaving the reviewer unable to triangulate) and slowly calibrate toward a redaction that preserves the shape without leaking the specifics. Two heuristics help:

- **Redact to the *audience of the leaf*, not to the audience of the whole envelope.** A specific eval-set descriptor might need redaction for a Big-Four firm (where a competitor's engagement partner might rotate into the account) but not for an AISI-shape institute (where the descriptor is going into a bilateral NDA and the institute's evaluators are cleared). A single redaction pass across the whole envelope loses this discrimination. The programme's redaction procedure is applied per leaf, not per envelope.
- **A redacted leaf still cites its underlying digest.** The reviewer can see that the underlying artefact exists, is integrity-protected, and is available under a different disclosure regime if the engagement's scope changes. This is what allows chapter `01`'s AISI safety-case redaction to be defensible: the redaction is opaque about the specific customer, but transparent about the harm-model shape and the underlying assurance-case node's digest.

Redaction is also the discipline the programme applies against the AEDT interface's independence line (chapter `03`). The redaction preserves the input data's *lineage* while withholding candidate PII; the auditor sees enough to run the DCWP methodology without contamination and without seeing candidate-identifying information they do not need.

### Failure mode — evidence softness

Evidence softness presents in one of three shapes: the reviewer requests a sample the pipeline cannot produce on demand, and the programme's staff spend a week curating; the reviewer walks a provenance chain and the chain breaks at a step the internal consumers never had to walk; the reviewer verifies a signature against a public key and the key rotation was not carried in the manifest.

The playbook's discipline against evidence softness is the four hardening practices above, applied continuously rather than in a pre-engagement scramble. Continuous hardening is what makes the `mod-104` evidence pipeline production-ready for external consumption; scrambled hardening produces evidence that is fresh enough for the current engagement but not durable across the engagement's validity window.

## Worked example — assembling the playbook for one engagement

Consider the same customer-support-agent frontier deployment from chapter `01`'s worked example, now being handed to a Big-Four firm for an ISAE 3000 (Revised) reasonable-assurance engagement on the AIMS covering the deployment (chapter `04`'s worked example specialised to this product).

The programme applies the playbook:

1. **Fix the report-delivery date.** Firm A's engagement partner commits to a report-delivery date of week fourteen from engagement kick-off. Programme back-plans four milestones: envelope-ready at week zero (the kick-off itself); mid-engagement checkpoint at week seven; draft-review window opening at week twelve; report-delivery at week fourteen. Slack budgets: three business days on envelope-ready (front-loaded), one week on mid-engagement checkpoint (mid-loaded), five business days on draft-review window (tail-loaded).
2. **Cross-reference the release-gate cadence.** The corresponding release candidate's release-gate promotion window opens at week sixteen — two weeks after report-delivery. The two-week gap absorbs the draft-review window's slack budget and gives the programme time to ingest the report into the assurance case as an external-evaluator leaf. Where the gap is smaller than the sum of the draft-review-window slack and the ingestion time, the release-gate window is deferred to preserve the ordering.
3. **Set envelope-ready lead time.** Assuming the reproducibility bundles from `mod-104` chapter `03` exist for the release candidate and the AIMS documentation is current, envelope-ready lead time is eight weeks: control-library mapping (three weeks), evidence-pipeline query provisioning (two weeks), redaction pass on the harm-inventory-derived leaves (two weeks), envelope-signing and intake checklist (one week). The engagement-decision date is pinned eight weeks before kick-off.
4. **Assemble the seven components.** Deployment-context statement (drafted by release-assurance methodology owner, one page). Deployment-tier framework document (the `mod-108` tier-decision artefact for the release candidate, co-signed by head of AI governance). Assurance-case excerpt (SACM `ArgumentPackage` for the release candidate, redacted per the discipline below). Reproducibility bundles for provider-side evaluations (aggregated from the peer-role owners). Credentialed access channel (empty for this engagement — attest examination is documentary and pipeline-query-based, noted "not applicable" rather than omitted). AIMS documentation excerpt (clauses 4–10 and the Annex A control set relevant to the engagement scope, drafted by the AI-governance analyst peer, re-narrated for the engagement). Return channel and provenance manifest (signed DSSE envelope listing every artefact and every pipeline-query endpoint).
5. **Apply the four hardening practices.** Every leaf carries its digest; the pipeline supports on-demand sampling by control library and by release candidate over the twelve-month engagement period; the harm-inventory-derived leaves are redacted per the redact-to-audience heuristic (Firm A's engagement partner is cleared for the AIMS scope but not for the specific competitive positioning of the customer-support product); the envelope carries a signed manifest and every leaf carries a DSSE signature.
6. **Apply the twenty-one-item intake checklist.** Release-assurance on-call and methodology owner both sign the checklist at envelope-ready minus three business days (front-loaded slack budget applied). Two items fail on the first pass — the AIMS documentation excerpt's clause 8.4 (operational planning and control) is pinned to the AIMS version prior to the release candidate; the return-channel provenance manifest's Rekor entry is not present. Both are fixed; the checklist is re-signed; the envelope ships to Firm A at kick-off.
7. **Mid-engagement checkpoint at week seven.** Firm A's engagement partner requests supplementary evidence on two Annex A controls (A.6.2.5 on impact analysis, A.9.2 on data-quality management). Programme retrieves the samples by pipeline query within two business days; Firm A confirms the samples satisfy the request.
8. **Draft-review window at week twelve.** Firm A issues the draft opinion with one qualification (post-market monitoring for one of the seven products under the AIMS). Programme reviews for factual accuracy; no factual corrections; the qualified area is confirmed for corrective-action tracking under ISO/IEC 42001 clause 10.2.
9. **Report-delivery at week fourteen.** Signed opinion delivered; ingested into the assurance case as an external-evaluator leaf with a twelve-month validity window; release-gate cites the leaf at the week-sixteen promotion window.

The programme's engagement calendar carries the certificate-validity re-engagement reminder at week fifty-two minus the envelope-ready lead time (week forty-four), so the following year's engagement decision is made in time to preserve continuity.

The playbook is not the whole engagement — the interface-specific disciplines from chapters `01`–`04` still apply — but the playbook is what makes the engagement operable at all.

## The engagement-charter template

The playbook's operational artefact is the *engagement charter* — a short, structured document the programme drafts at engagement decision and updates through the engagement's lifecycle. The charter carries:

- **Engagement identity.** Engagement identifier, evaluator organisation, evaluator engagement-team lead, contract reference, engagement type (AISI-shape / notified-body / AEDT / Big-Four attest / Big-Four advisory), and the release candidate(s) or AIMS scope the engagement covers.
- **Calendar.** Report-delivery date, envelope-ready date, kick-off date, mid-engagement checkpoint date, draft-review window opening date, and the slack budget on each milestone. Cross-references to the release-gate cadence and any external disclosure deadlines.
- **Seven-component owner assignments.** Primary and backup owner for each of the seven envelope components, with the AIMS clause the component is being asserted under where applicable.
- **Hardening declarations.** The specific attestation formats the envelope will carry (DSSE, in-toto, Rekor); the specific redaction targets the envelope will apply (per-leaf, calibrated to evaluator audience); the specific sampling channels the pipeline will expose.
- **Intake checklist.** The twenty-one-item checklist state at each milestone (envelope-ready, mid-engagement checkpoint, draft-review window).
- **Return-artefact disposition.** How the evaluator's return artefact will be ingested (assurance-case leaf, external card citation, release-gate criterion); the validity window; the re-engagement reminder date.
- **Peer-role acknowledgements.** Signed acknowledgements from each peer role whose evidence is being handed over (`ai-risk-engineer` for harm-inventory-derived evidence, `ai-eval-engineer` for evaluation-derived evidence, `model-evaluation-engineer` for measurement-derived evidence, `ai-infra-security` for credential-scoping evidence, `ai-governance-analyst` for AIMS-documentation-derived evidence).

The charter lives alongside the engagement's contract and the delivery envelope in the AIMS controlled-documents register (`mod-104` chapter `06`). Its structure is uniform across engagement types; its content differs by engagement.

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the seven-component owner assignments cite the peer-role registry directly; the playbook is where the deferral contract's external-parties row becomes operationally executable.
- `mod-102` (assurance case) — the return-artefact disposition ingests the evaluator's report as an external-evaluator leaf with a validity window; the case-integration is where the engagement's evidence becomes case evidence.
- `mod-103` (release-gate) — the four cross-references (report-before-promotion, report-before-disclosure, certificate-validity-window, substantial-modification-test) are release-gate criteria the playbook makes explicit.
- `mod-104` (evidence pipeline) — the four hardening practices (digest-pin, sample-by-query, redact-per-audience, sign-the-envelope) are the pipeline's external-facing operating mode; the assurance bundle from chapter `06` is the primary source for envelope assembly.
- `mod-105` (cards) — the report-before-disclosure cross-reference is what makes the external card's evaluator-cited paragraphs defensible on the card's publication date.
- `mod-108` (deployment-tier gating) — the deployment-tier framework document is one of the seven envelope components; the tier-decision artefact from chapter `05` is what the evaluator reads to understand the release candidate's tier landing.
- `mod-110` (post-market surveillance) — the certificate-validity re-engagement reminder is one of the surveillance plan's calendar entries.
- `mod-112` (programme ownership) — the engagement charter is one of the standing artefacts the programme charter tracks across cycles.

## Summary

- Every third-party engagement the programme runs — AISI-shape, notified-body, AEDT, Big-Four — sits on three shared disciplines: delivery timing (back-planned from report-delivery), delivery envelope (seven components with named owners and a twenty-one-item intake checklist), and evidence hardening (four practices that turn internally-adequate evidence into externally-defensible evidence).
- Delivery timing back-plans from the evaluator's report-delivery date through four milestones (envelope-ready, kick-off, mid-engagement checkpoint, draft-review window), with slack budgets on each milestone and cross-references into the release-gate cadence.
- The delivery envelope has seven components (deployment-context statement, deployment-tier framework document, assurance-case excerpt, reproducibility bundles, credentialed access channel, QMS/AIMS documentation excerpt, return channel and provenance manifest); every component has a single named owner with a named backup; the twenty-one-item intake checklist (present / current / signed for each component) is a gate at envelope-ready.
- Evidence hardening rests on four practices: digest-pin every leaf, sample by pipeline query rather than by curation, redact commercially-sensitive detail while preserving the shape of what is being described, sign the envelope's manifest as well as its leaves. The four practices apply uniformly across engagement types.
- The engagement charter is the playbook's operational artefact — a structured document at engagement decision that carries the calendar, the owner assignments, the hardening declarations, the intake-checklist state, and the return-artefact disposition. It lives alongside the engagement contract in the AIMS controlled-documents register.
- Three failure modes recur without the playbook — timing collapse, envelope drift, evidence softness — and the playbook's three disciplines are designed against them.
- The playbook is the synthesis of chapters `01`–`05`: what the four interface-specific chapters have in common when read as a set, expressed as a reusable operating procedure the programme can apply on intake without re-authoring for each new engagement type.
