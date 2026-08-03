# exercise-04: Big-Four Assurance — Attest vs Advisory

**Estimated effort:** 2 hours

## Objective

Scope an **ISAE 3000 (Revised) reasonable-assurance attest engagement** on one worked AIMS and defend the **attest-vs-advisory split** against an intake proposal that tried to collapse them. Produce the engagement-scoping memo, the criteria-and-control-library mapping, the evidence-pipeline readiness assessment, the Chinese-wall independence attestation, and the intake-mistake defence memo the programme uses on the next engagement proposal that arrives conflating the two modes.

The exercise is design and authoring, not solving. The focus is on the intake decision — whether attest or advisory is the right mode for the outcome the enterprise wants — and on the evidence-pipeline preparation that determines whether an attest engagement is even feasible at the requested assurance level.

## Prerequisites

- Chapter [`04-big-four-assurance-engagements-attest-vs-advisory.md`](../04-big-four-assurance-engagements-attest-vs-advisory.md) — the assurance-standards frame, the attest-vs-advisory difference, the branded firm offerings, the criteria patterns, and the evidence-pipeline dependency for attest cost and feasibility.
- Chapter [`06-delivery-timing-envelope-and-evidence-hardening-playbook.md`](../06-delivery-timing-envelope-and-evidence-hardening-playbook.md) — the engagement-charter template applied to attest engagements, with the four hardening practices (digest-pin, sample-by-query, redact-per-audience, sign-the-envelope) that make sample retrieval on demand feasible.
- Familiarity with `mod-104` chapter `06` (assurance bundle and AIMS controlled-documents register) and `mod-102` (assurance case — the attest opinion as an external-evaluator leaf).
- Familiarity with the enterprise's AIMS structure per ISO/IEC 42001 clauses 4–10 and Annex A.
- Skim access to the IAASB's ISAE 3000 (Revised) landing page at [iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or](https://www.iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or) and one of the Big-Four firms' current AI-assurance product pages.

## Problem statement

Pick one enterprise AIMS and one intake situation. Two dimensions to pin:

- **The AIMS.** An ISO/IEC 42001-conforming AI Management System covering three-to-seven AI products in a single enterprise. The AIMS is real (in the exercise's sense — you invent it, but you author it with the structure a real AIMS would have) and has been operating for at least twelve months, so a period-of-time attest engagement is meaningful.
- **The intake situation.** One of the following intake shapes (pick one, or invent your own — the point is the intake decision):
  - **Board-driven attest.** The board's risk committee has asked for independent assurance on the AIMS's control-effectiveness. The intake question is which firm and which criteria set.
  - **Counterparty-driven attest.** A major enterprise customer has a contractual clause requiring an independent assurance opinion on the AI-vendor's AIMS. The intake question is which assurance level satisfies the clause without over-scoping.
  - **Collapsed intake.** A business owner has asked one firm to "assess and improve" the AI controls. The firm has quoted an advisory engagement. The business owner expected an opinion-carrying artefact and does not yet know the two do not substitute. The intake question is how to separate the two engagements and which to run first.
  - **Regulator-adjacent attest.** A sector regulator has published a non-binding expectation that firms carry independent third-party assurance on their AIMS. The intake question is which criteria set and which firm best positions the enterprise for the anticipated future binding rule.

Pin the AIMS scope, the seven AI products it covers, and the intake situation before you begin the artefact set.

## Requirements

Produce five artefacts in a single directory.

### 1. `intake-decision-memo.md`

A three-page memo that fixes:

- **AIMS identity.** Named enterprise, AIMS scope, ISO/IEC 42001 certification status (certified against ISO/IEC 42006:2025 by an accredited certification body, in progress, not pursued), the seven AI products the AIMS covers with one-line descriptions, and the AIMS's management-review cycle (ISO/IEC 42001 clause 9.3) date.
- **Reporting audience.** Board risk committee, enterprise customer's audit committee, regulator, or a combination. The audience determines the report's restricted-use vs general-use profile and the criteria set the audience will accept.
- **Outcome required.** What the enterprise needs the engagement to produce — an independent opinion the audience will consume as an assurance leaf, or capability-building working documents. This is the *attest vs advisory* decision, made explicitly.
- **Attest-vs-advisory decision and reasoning.** Where the outcome requires an opinion, the engagement is attest and this section defends the assurance level (reasonable vs limited) against the audience's needs and the evidence-pipeline maturity. Where the outcome is capability-building, the engagement is advisory and this section defends the scope, the deliverable set, and the transferred-tooling expectation.
- **Where an intake proposal collapsed the two, disentangle them.** For the collapsed-intake shape (if chosen), name the two separate engagements the collapsed proposal actually implies — an advisory engagement to close identified capability gaps, followed by an attest engagement to opine on the resulting control set — and the sequencing (advisory first, attest at least one AIMS management-review cycle later so operating-effectiveness testing has adequate period-of-time evidence).
- **Firm selection considerations.** The four axes from chapter `04` — control-library alignment, assurance level offered, AI-domain SME bench under Chinese-wall arrangement, engagement-partner track record. Whether the enterprise's existing financial-audit firm is or is not an eligible attest firm for the AIMS engagement (independence-rule cross-checks with the financial audit).

### 2. `criteria-and-control-library-mapping.md`

The criteria set the attest engagement will opine against, and the mapping from the programme's own control library onto the criteria. Sections:

- **Criteria set selection.** Which of the three criteria patterns from chapter `04` applies:
  - **NIST AI RMF sub-categories.** The AI RMF's MAP / MEASURE / MANAGE / GOVERN functions, with the specific sub-categories the engagement will test against.
  - **ISO/IEC 42001 clauses.** Clauses 4–10 and the Annex A controls applicable to the AIMS's scope.
  - **Internal responsible-AI standard.** The enterprise's own standard as reference criteria, with its provenance and its adoption pathway named.
- **Control-library mapping.** A table mapping each of the enterprise's controls onto the criteria element(s) it satisfies. Columns: control identifier, control description, criteria element(s), evidence source (which `mod-104` chapter `06` assurance-bundle leaf or AIMS controlled-document), peer-role owner (from the `mod-101` deferral contract), and the sampling channel the pipeline exposes.
- **Coverage gaps.** Where a criteria element has no control mapped to it, the gap is named — either the criteria element is not applicable (with reasoning) or the control-library uplift is needed before the engagement can proceed. Gaps of the second kind are what an advisory engagement would close before the attest engagement begins.
- **Suitability defence.** A short paragraph defending the criteria set's *suitability* under ISAE 3000 (Revised) — the criteria are relevant, complete, reliable, neutral, and understandable to the intended users of the opinion.

### 3. `evidence-pipeline-readiness-assessment.md`

The evidence-pipeline readiness assessment. Chapter `04` is emphatic — the pipeline's ability to produce sample sets on demand is what determines whether the engagement can run at the requested assurance level at a cost the budget can absorb. Sections:

- **Pipeline capability snapshot.** For each of the four hardening practices from chapter `06`:
  - **Digest-pin every leaf.** Which artefact classes in the pipeline are digest-pinned; which are not; the remediation plan for any gap.
  - **Sample by query, not by curation.** Which query surfaces the pipeline exposes; the expected latency per query class; the peer-role owner of each query surface.
  - **Redact per audience.** Which redaction passes are automated per audience class (attest firm, notified body, AISI-shape evaluator); which are manual; the review latency per manual redaction.
  - **Sign the envelope.** Which envelope formats the pipeline supports (DSSE, in-toto); the key management for envelope signing; the verification path the attest firm will walk.
- **Sample-volume projection.** Estimated sample volumes per criteria element for the engagement's period (twelve months, seven products) at each assurance level (reasonable vs limited). Whether the pipeline can absorb the sample-retrieval workload within engagement SLAs.
- **Readiness verdict.** *Ready for reasonable assurance*, *ready for limited assurance only*, or *ready after remediation*, with the specific remediation set and its lead time named.
- **Pre-engagement remediation plan.** Where remediation is needed, the peer-role owner of each remediation item, the target completion date, and the evidence the remediation itself produces (metadata attestations, key-management runbooks, redaction-audit logs).

### 4. `chinese-wall-independence-attestation.md`

The independence attestation the programme requires from the selected attest firm. Sections:

- **Attest-firm identity.** The selected firm (Big Four or Big-Four-shape); the engagement partner and the engagement quality-control reviewer; the assurance practice group the engagement sits in; the AI-domain SMEs seconded from the advisory practice under the Chinese-wall arrangement.
- **Prior-engagement history with the firm.** Every prior engagement the firm has performed for the enterprise in the past twenty-four months, across both attest and advisory practice groups, and across all subject matters. For each prior engagement, whether it touched the subject matter of the current attest engagement (the AIMS's control set) — if so, the independence disposition (Chinese-wall separation is inadequate; a different firm must be selected).
- **Concurrent engagement inventory.** Every engagement the firm is currently performing for the enterprise, across both attest and advisory practice groups. For each, the concurrent-engagement disposition — Chinese-wall separation is adequate (different subject matter, different partner leadership, documented independence procedures) or inadequate.
- **Independence attestation content.** What the firm must attest to in writing before engagement start — the specific independence rules under ISAE 3000 (Revised) they are attesting compliance with, the Chinese-wall procedures they are operating, the individuals involved in the engagement and their independence individually attested.
- **Ongoing-independence process.** How independence is maintained through the engagement — the firm's internal monitoring, the programme's own monitoring (any new advisory engagement with the same firm during the attest engagement period must be reviewed for independence impact), and the reporting cadence if any independence event occurs.
- **Financial-audit cross-check.** If the same firm performs the enterprise's financial audit, the specific independence rules governing the combined engagement (typically permissible under existing financial-audit-and-AI-attest guidelines, but requiring documented consideration).

### 5. `intake-mistake-defence-memo.md`

The defence memo the programme uses when the *next* intake proposal arrives conflating attest and advisory (per chapter `04`'s common intake mistakes). Written as an internal-facing artefact — the programme's release-assurance methodology owner responding to a business owner's proposal. Sections:

- **The three common intake mistakes.** Chapter `04` names three: collapsing attest and advisory into a single engagement; selecting a firm on brand rather than on control-library alignment; underestimating the evidence-pipeline dependency. For each mistake, the memo names the misintake pattern, the concrete failure mode, and the intake-time fix.
- **The disentangling script.** The script the methodology owner uses when a business owner arrives asking for an outcome that would require both an advisory and an attest engagement. The script names the two engagements, sequences them, names the firm-independence implications (same firm on both, only under Chinese-wall separation between practice groups on non-overlapping subject matter; different firm on the attest often being simpler), and names the timing implication (advisory first, at least one AIMS management-review cycle before attest).
- **The scope-vs-brand script.** The script for the case where the business owner is asking for the enterprise's existing financial-audit firm to perform the AI attest engagement. The script names the four scoring axes from chapter `04`, walks the scoring, and defends the selection on scope-fit even where brand comfort would prefer a different firm.
- **The pipeline-dependency script.** The script for the case where the business owner is asking for a reasonable-assurance engagement without confirming pipeline readiness. The script names the readiness verdict from `evidence-pipeline-readiness-assessment.md`, walks the remediation lead time, and defends either a deferred engagement decision or a downgraded assurance level.
- **The escalation path.** What happens if the intake conversation cannot be resolved at the methodology-owner level — escalation to `head-of-ai-governance` (level 60, per the `mod-101` deferral contract) with the decision-support memo the escalation carries.

## Starter guidance

- **Attest and advisory are different engagements, always.** They can never substitute for each other. If the outcome requires an opinion, the engagement is attest and the constraints (assurance level, criteria suitability, independence, evidence-pipeline maturity) all attach. If the outcome is capability-building, the engagement is advisory and the constraints are looser but the deliverable is not opinion-carrying.
- **Criteria suitability is where the attest opinion earns its authority.** An opinion against an unsuitable criteria set is an opinion the audience cannot use. Spend proportional effort defending suitability — relevance, completeness, reliability, neutrality, understandability to the intended users.
- **The evidence pipeline is the load-bearing dependency.** Chapter `04` is emphatic — the pipeline's readiness is what determines cost and feasibility. `evidence-pipeline-readiness-assessment.md` is the load-bearing artefact.
- **Chinese-wall separation is procedural, not decorative.** The programme's role is to require the attestation, verify it against the concurrent-engagement inventory, and monitor independence through the engagement. A firm that cannot attest to Chinese-wall separation on a specific engagement is not eligible for that engagement, even if their AI-assurance practice is otherwise strongest.
- **The intake decision is the load-bearing decision.** Getting attest-vs-advisory right at intake is far more consequential than getting the firm selection right afterward. Author `intake-decision-memo.md` with the same care an assurance partner would apply to an engagement-acceptance decision.
- **The three common intake mistakes recur.** Chapter `04`'s list is not a one-time observation — it is the pattern first-time programmes exhibit. The `intake-mistake-defence-memo.md` is designed to be reusable across future intake conversations, not just the one at hand.
- **`<!-- needs-research: … -->` markers are legitimate.** The Big-Four firms' current product naming, the ISAE / SSAE current version numbers, and the specific criteria libraries the firms use are all subject to revision. Where you would need to verify a specific citation, mark it rather than guessing.

## Acceptance criteria

You have succeeded if:

- `intake-decision-memo.md` fixes the AIMS identity, reporting audience, outcome required, and attest-vs-advisory decision with reasoning. Where the intake situation collapsed the two, the memo disentangles them and sequences the resulting engagements.
- `criteria-and-control-library-mapping.md` selects a criteria set from the three patterns, maps every control onto its criteria element, names coverage gaps, and defends suitability under ISAE 3000 (Revised). No coverage gap is hidden; either an element is not applicable with reasoning, or a remediation is named.
- `evidence-pipeline-readiness-assessment.md` covers each of the four hardening practices with a capability snapshot, projects sample volumes at each assurance level, delivers a readiness verdict, and names the pre-engagement remediation plan where remediation is needed.
- `chinese-wall-independence-attestation.md` inventories prior and concurrent engagements with the selected firm, names the independence-attestation content, describes ongoing-independence monitoring, and addresses the financial-audit cross-check.
- `intake-mistake-defence-memo.md` walks the three intake mistakes with concrete disentangling / scope-vs-brand / pipeline-dependency scripts and names the escalation path to `head-of-ai-governance`.
- The attest-vs-advisory decision is made explicitly and defended — nowhere is the assumption made that the two can substitute for each other.
- The evidence-pipeline readiness verdict is honest — where the pipeline is not ready for reasonable assurance, the memo says so and either defers the engagement or downgrades the assurance level rather than pretending readiness.
- The engagement charter template from chapter `06` is either present as an appended section or explicitly referenced so a reviewer can see the calendar and hardening declarations in operation.
- Every place a fact would need to be verified against a specific firm's current product naming, ISAE / SSAE version numbers, or the enterprise's own AIMS structure is marked `<!-- needs-research: … -->`.

## Stretch goals

- **Draft the engagement letter.** In `engagement-letter-draft.md`, author the ISAE 3000 (Revised) engagement letter's key clauses — responsible party, subject matter, criteria, assurance level, reporting audience, temporal scope, deliverable, engagement partner, quality-control reviewer, management representation letter requirement.
- **Compose the management representation letter.** In `management-representation-letter.md`, draft the letter the head of AI governance signs attesting to the completeness and accuracy of the evidence provided. Cite the specific evidence classes (`mod-104` chapter `06` assurance bundle, `mod-102` chapter `04` assurance case, `mod-108` tier-decision artefacts).
- **Author the qualified-opinion contingency.** In `qualified-opinion-response.md`, walk the case where the firm's draft opinion is qualified on one control area — the programme's response (remediation-plan drafting, ISO/IEC 42001 clause 10.2 corrective-action entry, board-committee communication).
- **Design the multi-year attest cycle.** In `multi-year-cycle-plan.md`, sketch the second and third year of the attest engagement — how the samples across cycles are structured, how the criteria set evolves as the AIMS matures, how the assurance level might trend upward from limited to reasonable across cycles as the pipeline matures.
- **Author the second-firm advisory engagement.** In `second-firm-advisory-scope.md`, for the collapsed-intake shape (if chosen), draft the statement-of-work for the *advisory* engagement performed by a *different* firm (or a different practice group with attested Chinese-wall separation) that closes the capability gaps identified in `criteria-and-control-library-mapping.md`. The advisory engagement precedes the attest engagement by at least one AIMS management-review cycle.
- **Cross-reference the notified-body engagement.** In `attest-and-notified-body-coordination.md`, sketch how the attest engagement's evidence set overlaps with the notified-body engagement from exercise `02`. Where the two audiences can consume the same underlying evidence with different redaction passes, the programme's discipline is to prepare the evidence once and redact per audience (chapter `06`).
