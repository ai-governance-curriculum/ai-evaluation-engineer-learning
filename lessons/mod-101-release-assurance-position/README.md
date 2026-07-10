# mod-101-release-assurance-position: Release-Assurance Position: The Assurance Methodology Owner on the Ladder

Opens the AI Evaluation Engineer track by pinning the role to one job — *own the release-assurance methodology* — and by walking the four bodies of literature (NIST AI RMF, ISO/IEC 42001, EU AI Act, values baseline) that every subsequent module maps into.

**Estimated effort:** 12 hours

## Learning objectives

- Distinguish this role's ownership (release-assurance methodology) from `ai-eval-engineer` (application-layer eval engineering), `model-evaluation-engineer` (model-eval methodology depth), `ai-risk-engineer` (risk-engineering craft), `ai-governance-analyst` (operational analyst legwork), and `senior-ai-governance-architect` / `head-of-ai-governance` (control-library and program leadership).
- Paraphrase NIST AI RMF 1.0 GOVERN / MAP / MEASURE / MANAGE and locate the sub-categories the assurance program plugs each release-gate obligation into, using the NIST AI RMF Playbook as the day-to-day reference.
- Walk the clause structure of ISO/IEC 42001:2023 and locate the clauses (4–10) that the assurance program maps its evidence into.
- Read the EU AI Act obligations that shape a release-gate: Articles 8–15 (risk-management system, data governance, technical documentation, records, transparency, human oversight, accuracy / robustness / cybersecurity), Article 17 (QMS), Article 26 (deployer obligations), Article 43 (conformity assessment), Article 47 (EU declaration of conformity), Article 49 (registration), Article 55 (systemic-risk GPAI), Article 61 (post-market obligations), Article 72 (post-market monitoring plan).
- Position OECD AI Principles, the Council of Europe AI Framework Convention, and the UNESCO Ethics Recommendation as the international values baseline the assurance program must not undercut.
- Draft the role's deferral contract: what evidence each peer / prerequisite / higher track owes this program, and what artefacts this program owes each of them.

## Lecture chapters

1. [`01-release-assurance-position-on-the-ladder.md`](01-release-assurance-position-on-the-ladder.md) — Where this role sits on the level ladder, what it owns, what it defers, and the differentiator against peers.
2. [`02-nist-ai-rmf-and-playbook.md`](02-nist-ai-rmf-and-playbook.md) — GOVERN / MAP / MEASURE / MANAGE, and how a release-gate obligation plugs into a sub-category. Introduces AI 600-1 (GenAI Profile) and AI 100-2 (adversarial-ML taxonomy).
3. [`03-iso-iec-42001-clause-structure.md`](03-iso-iec-42001-clause-structure.md) — Clauses 4–10 in Harmonised Structure and how release-assurance evidence maps into each. Introduces Annex A and the adjacent ISO standards (23894, 42005, 25059, 24029-2, 42006, 5259, 8183).
4. [`04-eu-ai-act-articles-shaping-the-release-gate.md`](04-eu-ai-act-articles-shaping-the-release-gate.md) — Articles 8–15, 17, 26, 43, 47, 49, 55, 61, 72, with the release-gate implication for each.
5. [`05-international-values-baseline.md`](05-international-values-baseline.md) — OECD AI Principles, Council of Europe Framework Convention, UNESCO Recommendation; the values cross-check against the assurance case.
6. [`06-deferral-contract.md`](06-deferral-contract.md) — Evidence-in and artefacts-out by party, framework citations, escalation paths when the contract breaks.

## Structure

- `01-…md` … `06-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapters 01 + 06 first** — they define the role and its contract; every other module refers back to them.
- **Chapters 02, 03, 04** — walk in that order (framework → management system → statute) so each layer contextualises the next.
- **Chapter 05** — read once and then keep as a checklist to run against later assurance cases.
- **Exercises** — do `01` after chapter `06`, then `02`, `03`, `04` after their matching chapters, then `05` as the capstone cross-check.
