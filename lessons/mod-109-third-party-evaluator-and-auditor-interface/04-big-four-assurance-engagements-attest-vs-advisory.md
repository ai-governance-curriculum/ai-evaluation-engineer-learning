# Big-Four-Shape Assurance Engagements — Attest vs Advisory

## Motivation

The Big-Four accountancy firms — and the wider Big-Four-shape market that includes Accenture, BDO, Grant Thornton, RSM, and the specialised AI-assurance boutiques — have been quietly building AI-assurance practices since 2019 and are now, in many enterprises, the third-party party of first resort when the board asks "who is checking our AI controls?" For a release-assurance programme this creates a distinctive interface: the firms operate under codified assurance-engagement standards that differ from AISI-shape technical evaluation (chapter `01`), from notified-body conformity assessment (chapter `02`), and from NYC-AEDT-shape compliance audit (chapter `03`), and their engagements split into two very different modes — *attest* and *advisory* — that are often confused at intake and that produce very different artefacts.

The confusion has consequences. An assurance programme that engages a Big-Four firm expecting an attest opinion, and receives an advisory deliverable, has bought competent help with process improvement but has *not* produced an independent, opinion-carrying artefact that a regulator, board risk committee, or downstream contractual counterparty will accept as an assurance leaf in the case (`mod-102`). Conversely, a programme that engages for an attest opinion when an advisory engagement would have sufficed is spending several multiples of the advisory fee and constraining the firm's ability to help with remediation — attest independence rules prevent the same firm from designing the controls it later opines on.

This chapter walks the assurance-engagement standards the Big Four operate under, the concrete difference between attest and advisory engagements, the firm-specific AI-assurance offerings, what an attest opinion on an AI system typically covers, and why the release-assurance programme's evidence pipeline (`mod-104`) determines the cost and feasibility of the attest engagement.

## Assurance-engagement standards

Two standards frame Big-Four AI-assurance work: ISAE 3000 (Revised) for international engagements and SSAE 21 for US engagements. Both are the *generic* assurance-engagement standards — the shape they impose is domain-agnostic and applies equally to sustainability reporting, cybersecurity controls (SOC 2), and AI-management-system controls.

### ISAE 3000 (Revised)

**Who they are.** ISAE 3000 (Revised) — *Assurance Engagements Other than Audits or Reviews of Historical Financial Information* — is the International Auditing and Assurance Standards Board's standard for non-financial assurance. Published by the IAASB at [iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or](https://www.iaasb.org/publications/international-standard-assurance-engagements-isae-3000-revised-assurance-engagements-other-audits-or), it is what Big-Four firms operate under for AI-assurance engagements that produce an opinion outside the US.

**What they ask for.** ISAE 3000 (Revised) requires (a) a *responsible party* (the entity responsible for the subject matter — here, the release-assurance programme and the AI-system owner); (b) a *subject matter* (the AI-system controls or the AIMS as-designed / as-operating); (c) *suitable criteria* against which the subject matter is evaluated (NIST AI RMF, ISO/IEC 42001, an internal responsible-AI standard); (d) *sufficient appropriate evidence*; and (e) a *written assurance report* carrying an opinion at the engagement's assurance level (reasonable or limited).

**Handoff envelope.** The firm's engagement letter defining the assurance level, subject matter, criteria, and reporting audience; the responsible party's control library and evidence; the firm's testing plan; site visits and interviews; the written report.

**Release-assurance implication.** ISAE 3000 (Revised) engagements are what generate the *independent opinion* rows in the assurance case (`mod-102`). The engagement's assurance level (reasonable vs limited) affects the wording of the opinion and the depth of testing — reasonable assurance is a positive expression ("the controls are effective"); limited assurance is a negative expression ("nothing has come to our attention to suggest they are not").

### SSAE 21

**Who they are.** SSAE 21 — the AICPA's Statement on Standards for Attestation Engagements No. 21, *Direct Examination Engagements* — is the current US analogue for attestation engagements at the level of AICPA members. The AICPA's attestation-standards home is [aicpa-cima.com](https://www.aicpa-cima.com/) <!-- needs-research: verify SSAE 21 remains the current AICPA attestation standard for direct examination engagements and confirm exact URL under the merged AICPA-CIMA site -->. In the US the older SOC-1 / SOC-2 examination frameworks continue to dominate control-effectiveness engagements; AI-control examinations are increasingly framed as SOC 2-adjacent examinations against a criteria set the firm and the client agree on.

**What they ask for.** Similar to ISAE 3000 — responsible party, subject matter, suitable criteria, evidence, opinion.

**Handoff envelope.** Same shape as ISAE 3000 (Revised).

**Release-assurance implication.** For US-headquartered enterprises the SSAE 21 (or SOC-adjacent) engagement is often the primary attest interface; multinational enterprises typically anchor on ISAE 3000 (Revised) and cite SSAE conformance where the report will be relied on by US counterparties.

## Attest vs advisory — the concrete difference

The distinction is fundamental to how the engagement is procured, priced, staffed, and consumed.

### Attest engagement

**What it is.** An *independent examination or review* of a subject matter against suitable criteria, resulting in a *written opinion* the firm signs. Under ISAE 3000 (Revised) / SSAE 21 attest independence rules the firm cannot have designed the subject-matter controls, cannot have material financial interest in the controls' effectiveness, and must apply the standard's engagement quality-control procedures.

**Deliverable.** A written assurance report addressed to a specified reporting audience, with an opinion at the engagement's assurance level. Reports are typically *restricted-use* (only the reporting audience may rely on the opinion) or *general-use* (any user may rely) depending on the criteria used and the audience specified.

**Cost profile.** High. Attest work is heavily staffed by qualified engagement partners and quality-control reviewers, evidence-testing is depth-based rather than breadth-based, and the firm's exposure to opinion-liability drives an internal risk-management overhead the client pays for. A first-cycle attest on an AI system is often multiples of a first-cycle advisory engagement covering the same territory.

**Cadence.** Annual is the typical steady-state cadence, matched to the AIMS management-review cycle (`mod-104` chapter `06`, ISO/IEC 42001 clause 9.3) and to the reporting audience's calendar (audit committee, board risk committee, external counterparty).

**Who they are.** Attest engagements are led by the firm's assurance practice — audit-partner-track staff, with AI-domain SMEs seconded from the advisory practice under Chinese-wall arrangements. In the Big Four the assurance practice is the audit practice; in the wider market, boutique attest firms with AICPA-member partners fill the role.

**What they ask for.** A stable control library, evidence for each control's operation, walkthrough interviews, sampling of operational events across the engagement period, and access to the AIMS records (`mod-104` chapter `06`).

**Handoff envelope.** Engagement letter, control library and evidence set, walkthrough calendar, sampling plan, management representation letter, written opinion.

**Release-assurance implication.** The attest opinion is the highest-authority external-evaluator leaf in the release-gate case for enterprise-scale AI programmes not otherwise regulated under EU AI Act or a sector-specific regime. It anchors the board narrative and satisfies contractual counterparty requirements (e.g., an enterprise customer's AI-vendor assurance clause). The opinion's *usefulness* depends on the criteria being suitable — NIST AI RMF, ISO/IEC 42001, or an internal standard the counterparty accepts — and on the assurance level being high enough to matter.

### Advisory engagement

**What it is.** *Assistance* in designing, improving, or operating a control set. The firm brings expertise, tools, benchmarks, and templates; the client retains responsibility for the controls and the outcomes. Advisory engagements do *not* produce an opinion; deliverables are working documents, playbooks, gap-analyses, remediation roadmaps, and — often — transferred tooling.

**Deliverable.** Working documents, tools, templates. No opinion, no assurance report, no external-facing artefact suitable for board or regulator consumption as an independent assessment.

**Cost profile.** Lower per unit of scope than attest — but often larger scope, since advisory work fills capability gaps the client cannot fill internally. Cost is time-and-materials or fixed-fee against a defined deliverable set.

**Cadence.** Project-based (define, deliver, close) with optional retainer arrangements for ongoing capability support.

**Who they are.** The firm's advisory or consulting practice — different staff, different partner track, and (critically) different independence-rule regime from the attest practice. In the Big Four, advisory and audit sit in the same firm but are structurally separated under attest-independence rules to preserve the firm's ability to offer both to the same client, on different scopes, in the same year.

**What they ask for.** Access to teams, systems, and documentation to diagnose the current state; buy-in from decision-makers for the target state; time and attention from client staff to co-produce the deliverables.

**Handoff envelope.** Statement of work, project plan, deliverable list, working sessions, transferred artefacts.

**Release-assurance implication.** Advisory engagements are how the programme *builds capability* — the controls, the playbooks, the tooling — that a subsequent attest engagement then opines on. They are not themselves opinion-carrying evidence; they cannot substitute for an attest leaf.

### The Chinese-wall constraint

The most common intake mistake is asking one firm to *both* design a control and *then* attest to it. Attest independence rules forbid this: a firm that designed a control cannot then issue an independent opinion on that control's effectiveness. The mitigation is Chinese-wall structuring — advisory and attest work performed by separate practice groups within the firm, on non-overlapping subject matter, with documented independence procedures. In practice, the programme should treat *advisory and attest as engagements with different firms*, even when both are with the same Big-Four brand, and should not use advisory findings as evidence in an attest engagement.

## Firm-specific AI-assurance offerings

The Big Four and the adjacent market have all published branded AI-assurance offerings. Product naming shifts frequently; the offerings' contents are more stable than their names.

- **Deloitte** — Deloitte AI Assurance <!-- needs-research: verify current product naming and whether "Trustworthy AI framework" branding has been superseded -->. Anchored on Deloitte's Trustworthy AI framework; typical scope includes AIMS control-effectiveness examinations against ISO/IEC 42001 and NIST AI RMF-aligned control libraries.
- **PwC** — Responsible AI <!-- needs-research: verify current product naming and confirm the "Responsible AI Toolkit" is still the branded advisory deliverable -->. Anchored on the PwC Responsible AI framework; typical scope includes model risk management uplift and NIST AI RMF crosswalks on the advisory side, and attestation engagements against internal responsible-AI standards on the attest side.
- **EY** — Trusted AI <!-- needs-research: verify current product naming, whether "EY.ai" branding is the current umbrella, and product-family stability -->. Anchored on EY's Trusted AI framework; typical scope includes ISO/IEC 42001 readiness assessments (advisory) and attestation engagements on control-effectiveness (attest).
- **KPMG** — Trusted AI <!-- needs-research: verify current product naming and confirm the "KPMG AI in Control" framework naming -->. Anchored on KPMG's Trusted AI framework; typical scope includes AI-risk-and-controls assessments (advisory) and ISAE 3000 (Revised) engagements on control-effectiveness (attest).
- **Accenture** — Responsible AI <!-- needs-research: verify current product naming and Accenture's positioning in the attest vs advisory split — Accenture is primarily an advisory firm and does not offer attest engagements under ISAE 3000 (Revised) / SSAE 21 as a Big-Four-track engagement -->. Anchored on Accenture's Responsible AI framework; scope is advisory-only.

The programme's interface with each of these is the same at the assurance-standards level: ISAE 3000 (Revised) / SSAE 21 shape for attest, statement-of-work shape for advisory. The framework a firm markets its offering under (Trusted AI, Responsible AI, Trustworthy AI) is essentially a re-narration of NIST AI RMF, ISO/IEC 42001, and adjacent standards. When the programme is comparing firms on an attest engagement, the substance to compare is (a) which control library they will assess against, (b) which assurance level they will opine at, (c) the depth of their AI-domain SME bench under the Chinese-wall arrangement, and (d) their engagement partner's track record.

## What an attest opinion on an AI system typically covers

Attest opinions are always *criteria-referenced*. The opinion's subject matter is not "the AI system" — it is *"the control set the responsible party has designed and operated for the AI system against the [named criteria]"*. The criteria set determines what the opinion means. Three criteria patterns dominate:

- **Control-effectiveness against NIST AI RMF.** The programme's control library is mapped to NIST AI RMF sub-categories, and the attest tests control-effectiveness sub-category by sub-category. The opinion states whether the controls, as designed and operated, provide reasonable (or limited) assurance that the sub-category outcomes are achieved. This is the closest analogue to a SOC 2 examination in shape.
- **Control-effectiveness against ISO/IEC 42001.** The programme's AIMS control library is mapped to ISO/IEC 42001 clauses 4–10 and Annex A controls, and the attest tests conformance and effectiveness. In parallel, an ISO/IEC 42001 certification body may run an accredited certification audit under ISO/IEC 42006:2025 — the two are complementary, not substitutable.
- **Control-effectiveness against an internal responsible-AI standard.** The programme's control library is mapped to the enterprise's own responsible-AI standard (typically a translation of NIST AI RMF plus enterprise-specific controls), and the attest tests effectiveness. This pattern is common where the enterprise's board or a major counterparty has specified the internal standard as the reference criteria.

An attest opinion typically covers *design effectiveness* (the controls are designed adequately to achieve the criteria outcomes) and, at the higher assurance level, *operating effectiveness* (the controls operated as designed across the engagement period). The opinion's temporal scope — point-in-time (as of a date) vs period-of-time (over an engagement period) — is negotiated in the engagement letter.

## Why the evidence pipeline determines attest cost and feasibility

The single largest driver of attest engagement cost is *evidence-retrieval effort*. When the firm's engagement team asks "show me evidence that release-gate criterion X operated on every release candidate over the last twelve months, sampled to Y", the programme's answer is one of three shapes:

- **The evidence pipeline (`mod-104`) can produce the sample by query.** Every release-gate output artefact carries digest-pinned evidence, indexed by criterion and by release candidate. The engagement team receives a signed sample within days. Cost stays contained.
- **The evidence exists but is not indexed for retrieval.** The programme's staff spend weeks locating, curating, and re-attesting evidence for the sample. Cost multiplies; engagement partners raise scope-and-timeline flags.
- **The evidence is incomplete or not integrity-protected.** The engagement team cannot rely on the evidence at the assurance level requested; the opinion is downgraded, qualified, or delayed.

This is why the `mod-104` chapter `06` signed assurance bundle is not just an internal artefact — it is the substrate for cost-effective attest engagements. A mature evidence pipeline makes an ISAE 3000 (Revised) reasonable-assurance engagement feasible at a cost the programme's budget can absorb; an immature pipeline pushes the engagement into limited assurance or into deferral until the pipeline matures.

## Worked example — engaging a Big-Four firm for an ISAE 3000 (Revised) reasonable-assurance engagement on the AIMS

An enterprise is running an ISO/IEC 42001 AI Management System covering seven high-risk AI products. The board's risk committee has asked for independent assurance on the AIMS's control-effectiveness. The programme decides on an attest engagement.

1. **Firm selection.** Programme runs a request for proposals to three Big-Four firms; evaluates on control-library alignment, AI-domain SME bench, engagement partner track record, and price. Selects Firm A.
2. **Chinese-wall verification.** Programme confirms Firm A has *not* provided advisory services on the AIMS's design in the prior 24 months; documents the independence attestation.
3. **Engagement letter.** Signed under ISAE 3000 (Revised); subject matter is the AIMS's control-effectiveness against ISO/IEC 42001 clauses 4–10 and the applicable Annex A controls; assurance level is *reasonable*; period-of-time is 12 months; reporting audience is the board risk committee (restricted use); deliverable is the written assurance report.
4. **Control library and evidence delivery.** Programme hands Firm A the control library, the AIMS clause-mapping (`mod-104` chapter `06`), and query-access to the evidence pipeline for sampling.
5. **Walkthrough interviews.** Firm A conducts walkthroughs with the release-assurance on-call, risk engineer, AI-eval engineer, model-evaluation engineer, MLSec peer, and the head of AI governance.
6. **Sampling and testing.** Firm A samples across all seven products and across the 12-month period; requests evidence via the pipeline; the pipeline returns digest-pinned, DSSE-signed samples within engagement SLAs.
7. **Management representation letter.** Head of AI governance signs the management representation letter attesting to the completeness and accuracy of the evidence provided.
8. **Written opinion.** Firm A issues a reasonable-assurance opinion that the AIMS's controls, as designed and operated across the period, provide reasonable assurance that the ISO/IEC 42001 clause outcomes are achieved. Opinion is qualified in one area (post-market monitoring for one of the seven products, which is under remediation).
9. **Release-gate incorporation.** Programme ingests the opinion into the assurance case as an external-evaluator leaf with a 12-month validity window; the qualified area triggers a corrective-action record under ISO/IEC 42001 clause 10.2.

## Common intake mistakes

Three intake patterns come up often enough to name explicitly:

- **Collapsing attest and advisory into a single engagement.** The client asks the firm to "assess and improve" the AI controls, and the firm quotes an advisory engagement. The client later expects an opinion-carrying artefact suitable for board reporting; the advisory deliverable does not qualify. Fix at intake: name the required output artefact (opinion / working document) before scoping.
- **Selecting a firm on brand rather than on control-library alignment.** The client chooses the firm they use for financial audit rather than the firm whose AI-assurance control library best fits their AIMS. Fix at intake: score firms on control-library alignment as a distinct axis from brand and relationship.
- **Underestimating the evidence-pipeline dependency.** The client signs an ISAE 3000 (Revised) reasonable-assurance engagement without confirming the evidence pipeline can support the sampling volume. Costs escalate mid-engagement and the opinion is delayed or downgraded. Fix at intake: run a scoped pipeline-readiness assessment before the engagement letter is signed.

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the third-party evaluator row in the external-parties section covers Big-Four attest and advisory engagements.
- `mod-102` (assurance case) — an attest opinion is an external-evaluator leaf with a validity window; advisory deliverables are *not* case-leaf evidence.
- `mod-104` (evidence pipeline) — the pipeline's maturity determines attest engagement cost and feasibility; the assurance bundle is the primary source for the firm's sampling.
- `mod-105` (cards) — an attest opinion is a card-referenced external assurance artefact for the board and counterparty audiences.
- `mod-106` (cross-jurisdictional mapping) — the criteria set for attest engagements is drawn from the NIST AI RMF and ISO/IEC 42001 columns of the crosswalk.
- `mod-110` (post-market surveillance) — the ongoing surveillance regime feeds the annual re-attest cycle.
- `mod-112` (programme ownership) — the attest opinion is one of the standing assurance artefacts the head of AI governance briefs the board on.

## Summary

- Big-Four AI-assurance engagements operate under ISAE 3000 (Revised) internationally and SSAE 21 in the US; both are generic assurance-engagement standards applied to AI-control subject matter against suitable criteria.
- Attest engagements produce a *written opinion* at reasonable or limited assurance; advisory engagements produce *working documents and tools* with no opinion. The two cannot substitute for each other, and Chinese-wall constraints prevent the same firm from doing both on the same subject matter.
- Firm-specific offerings (Deloitte AI Assurance, PwC Responsible AI, EY Trusted AI, KPMG Trusted AI, Accenture Responsible AI) are re-narrations of NIST AI RMF, ISO/IEC 42001, and adjacent standards; the substance to compare is control library, assurance level, SME bench, and engagement partner.
- Attest opinions are always criteria-referenced — control-effectiveness against NIST AI RMF, ISO/IEC 42001, or an internal responsible-AI standard — and cover design and operating effectiveness across a specified temporal scope.
- The evidence pipeline (`mod-104`) is what determines attest engagement cost and feasibility; a mature pipeline enables reasonable-assurance engagements at contained cost.
- Exercise `04` has you scope an ISAE 3000 (Revised) reasonable-assurance engagement on a worked AIMS and defend the attest-vs-advisory split against an intake proposal that tried to collapse them.
