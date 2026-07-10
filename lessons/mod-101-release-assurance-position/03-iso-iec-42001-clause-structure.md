# ISO/IEC 42001:2023 — Clause Structure and Assurance-Evidence Mapping

## Motivation

Where NIST AI RMF is a voluntary risk-management framework, **ISO/IEC 42001:2023** is a *management-system standard* — the AI Management System (AIMS). It is written in the ISO Harmonised Structure (HS) shared with ISO 9001, ISO 27001, ISO 27701, and other management-system standards, so the shape will feel familiar to anyone who has worked with an ISMS or QMS.

ISO/IEC 42001 matters to a release-assurance program for two reasons.

First, it is *certifiable*. Organisations that pursue formal AIMS certification (through an accredited certification body — ISO/IEC 42006 governs how those bodies are accredited) are audited against clauses 4–10 of the standard. The release-assurance program produces most of the evidence the AIMS certification auditor needs.

Second, it is *the interoperability language* between the assurance program and the rest of the enterprise's management systems. Where the ISMS carries information-security controls (ISO 27001 Annex A), the AIMS carries AI-specific controls (ISO 42001 Annex A) that overlap on data governance and impact assessment. A release-gate evidence artefact that maps cleanly to a clause is one an auditor recognises without translation.

This chapter walks clauses 4–10, the shape of Annex A (the AI-specific controls list), and how the release-assurance program's evidence plugs into each.

## The Harmonised Structure — the shape you already know

ISO's Harmonised Structure (also called Annex SL structure) fixes clauses 1–10 for every ISO management-system standard. In ISO/IEC 42001:2023 those clauses are:

- **Clauses 1–3** — Scope, Normative references, Terms and definitions. (Not audited; reference material.)
- **Clause 4** — Context of the organisation.
- **Clause 5** — Leadership.
- **Clause 6** — Planning.
- **Clause 7** — Support.
- **Clause 8** — Operation.
- **Clause 9** — Performance evaluation.
- **Clause 10** — Improvement.

Clauses 4–10 are the *management-system requirements*. Annex A (informative) lists the AI-specific controls that Annex B (informative) then narrates. Annex C carries AI-related risk sources; Annex D carries integration hints across ISO management systems.

A conformance audit walks clauses 4–10 and asks, for each, "show me the documented information." What follows is what the release-assurance program has ready for each clause.

## Clause 4 — Context of the organisation

**What the standard requires.** Determine external and internal issues relevant to the AI management system; understand the needs and expectations of interested parties; determine the scope of the AIMS; establish and maintain the AIMS itself.

**What the release-assurance program contributes.**

- The catalogue of interested parties for the AI systems in scope: regulators (per jurisdiction), deployers, users, affected populations, third-party evaluators / auditors, insurers. This catalogue reappears in `mod-105` (cards for external audiences).
- The scope statement for the release-assurance program: which AI systems it decides releases for, which it does not, and the interface to peer / prerequisite / higher tracks (the deferral contract in chapter `06`).
- The maintained connection between the AIMS scope and the model / system inventory produced by the analyst.

Documented information typically includes: an AIMS scope document, an interested-parties register, and a program charter for the release-assurance function.

## Clause 5 — Leadership

**What the standard requires.** Top-management commitment; AI policy; roles, responsibilities, and authorities.

**What the release-assurance program contributes.**

- The RACI for the release-gate: who signs, who can veto, who is accountable for post-market surveillance. See `mod-103`.
- The release-assurance charter that top management has approved and communicated.
- The AI policy that the release-gate enforces at the artefact level — accepted uses, prohibited uses, escalation to counsel.

Documented information typically includes: the AI policy, the RACI matrix, and the top-management approval record.

## Clause 6 — Planning

**What the standard requires.** Actions to address risks and opportunities; AI risk assessment; AI risk treatment; AI system impact assessment; AI objectives and planning to achieve them.

**What the release-assurance program contributes.**

- **AI risk assessment** — the assurance case (`mod-102`) is the operationalisation of "the risks are identified, analysed, and evaluated." ISO/IEC 23894:2023 (AI risk-management guidance) is the reference for method.
- **AI risk treatment** — the release-gate architecture (`mod-103`) records treatment decisions per risk (accept, mitigate, transfer, avoid) and the evidence that discharges each.
- **AI system impact assessment** — ISO/IEC 42005:2025 is the guidance for the impact assessment itself; the release-assurance program either co-owns or reviews the impact assessment attached to each release-gate decision.
- **AI objectives** — the release-gate SLOs (accuracy, robustness, safety thresholds) and the assurance-program KPIs.

Documented information typically includes: the risk assessment record, the risk-treatment plan, the impact assessment, and the objectives register.

## Clause 7 — Support

**What the standard requires.** Resources; competence; awareness; communication; documented information.

**What the release-assurance program contributes.**

- **Competence and awareness** — the training curriculum for release-gate signers, third-party interface owners, and post-market surveillance operators.
- **Communication** — the standing communication cadence with peer teams (analyst, risk engineer, eval engineer, model-eval engineer, MLSec) and with external audiences (regulators, auditors).
- **Documented information** — the evidence pipeline (`mod-104`) is the operationalisation of "documented information is available and suitable for use, adequately protected." Immutable logs, lineage, ML-BOM / SPDX AI, signed release-gate outputs.

Documented information typically includes: training records, communication logs, and the evidence-repository index.

## Clause 8 — Operation

**What the standard requires.** Operational planning and control; AI risk assessment during operation; AI risk treatment during operation; AI system impact assessment during operation.

**What the release-assurance program contributes.**

- The standing release-gate procedure — its inputs, its evidence checklist, its decision criteria, its outputs.
- The change-control procedure for AI systems in scope — when a change requires a new gate, when a delta assessment suffices.
- The third-party evaluator / auditor interface (`mod-109`) as the operational shape for external assurance.

Documented information typically includes: the release-gate SOP, the change-control SOP, and the per-release-gate decision records with attached evidence.

## Clause 9 — Performance evaluation

**What the standard requires.** Monitoring, measurement, analysis, and evaluation; internal audit; management review.

**What the release-assurance program contributes.**

- **Monitoring and measurement** — the post-market surveillance (`mod-110`) loop and the online-eval interface with `ai-eval-engineer`.
- **Internal audit** — the periodic self-audit of the assurance program's own evidence, and the interface to internal-audit / three-lines-of-defence.
- **Management review** — the standing input to management review: release-gate throughput, decisions, incidents, corrective actions, changes to the risk landscape.

Documented information typically includes: post-market surveillance reports, internal-audit records, and management-review minutes.

## Clause 10 — Improvement

**What the standard requires.** Continual improvement; nonconformity and corrective action.

**What the release-assurance program contributes.**

- The corrective-action loop from incidents (both internal and external, e.g. items pulled from OECD.AI's Incidents Monitor or the AI Incident Database) into the release-gate.
- The continual-improvement plan for the assurance methodology itself: what gate criteria are being tightened, what evidence layer is being added, what deferral edge is being renegotiated.

Documented information typically includes: the nonconformity register and the improvement plan.

## Annex A — the AI-specific controls, in one paragraph

Annex A lists AI-specific controls that the AIMS commits to. The categories track familiar release-assurance concerns:

- Policies related to AI.
- Internal organisation for AI.
- Resources for AI systems.
- Assessing impacts of AI systems.
- AI system life cycle (planning, requirements, design, verification and validation, deployment, operation, retirement).
- Data for AI systems.
- Information for interested parties of AI systems.
- Use of AI systems.
- Third-party and customer relationships.

Annex B narrates each control with implementation guidance. The release-assurance program uses Annex A as the *control library* that the release-gate references, and cross-links each control into the corresponding NIST AI RMF sub-category and the corresponding EU AI Act article — the crosswalk lives in `mod-106`.

## Adjacent ISO documents that release-assurance leans on

- **ISO/IEC 23894:2023** — AI risk-management guidance. The method behind Clause 6 risk assessment.
- **ISO/IEC 42005:2025** — AI impact assessment guidance. The method behind Clause 6 impact assessment.
- **ISO/IEC 25059:2023** — Software quality model extended for AI systems (SQuaRE for AI). Useful for framing the "quality characteristics" the release-gate measures against.
- **ISO/IEC 24029-2:2023** — Robustness of neural networks. Useful for framing the robustness clause of MEASURE and the corresponding Annex A control.
- **ISO/IEC 42006** — Accreditation requirements for bodies certifying AIMS. Useful for the auditor-interface module (`mod-109`).
- **ISO/IEC 5259 series (data quality for analytics and ML) and ISO/IEC 8183 (data life cycle framework for AI)** — useful for the data-governance clauses.

Not every one of these will be pulled by every release-gate. What matters is that the release-assurance program *knows* the standards live and cites into them when the release-gate obligation touches the topic.

## Worked example — one clause, one evidence artefact

For clause 8 (Operation), a release-assurance program will typically maintain:

- A **release-gate SOP** — a documented procedure that says: intake, evidence checklist, decision criteria, signers, output artefacts. The SOP itself is *documented information* required by clause 7.5 and *operational control* required by clause 8.1.
- A **per-release decision record** — the assurance case, the evidence bundle, the decision, the signers, the release notes. This record satisfies clause 8.1 and feeds clause 9 (performance evaluation) and clause 10 (improvement).

Where the SOP and the decision record cite the NIST AI RMF sub-category and the EU AI Act article on the same line, the auditor's job is finished quickly.

## Where this shows up in the rest of the track

- `mod-102` (assurance-case engineering) — the assurance case is the operationalisation of clauses 6.1 (risks) and 8 (operation).
- `mod-103` (release-gate architecture) — the release-gate is the operationalisation of clause 8.1.
- `mod-104` (evidence pipeline) — the pipeline is the operationalisation of clause 7.5 (documented information).
- `mod-105` (cards for external audiences) — cards are the operationalisation of the "information for interested parties" Annex A control.
- `mod-106` (cross-jurisdictional mapping) — Annex A is the third column of the crosswalk (after NIST AI RMF and EU AI Act).
- `mod-109` (third-party interface) — the AIMS certification body relationship, governed by ISO/IEC 42006.
- `mod-110` (post-market surveillance) — the operationalisation of clauses 9 and 10.

## Summary

- ISO/IEC 42001:2023 is a certifiable AI management-system standard in the ISO Harmonised Structure. Clauses 4–10 are the auditable requirements.
- Clause 4 sets context; clause 5 is leadership and policy; clause 6 is planning (risk assessment, risk treatment, impact assessment, objectives); clause 7 is support (competence, communication, documented information); clause 8 is operation; clause 9 is performance evaluation (monitoring, internal audit, management review); clause 10 is improvement.
- Annex A is the AI-specific controls list the AIMS commits to.
- The release-assurance program produces most of the evidence the AIMS certification auditor needs, and cross-links each control into NIST AI RMF sub-categories and EU AI Act articles.
- Adjacent standards (ISO/IEC 23894, 42005, 25059, 24029-2, 42006, 5259 series, 8183) fill in the methods and topic-specific controls.
- Exercise 03 has you walk one release-gate artefact across clauses 4–10 and identify what documented information each clause requires.
