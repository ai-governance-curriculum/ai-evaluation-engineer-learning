# exercise-05: Values-Baseline Overlay Audit

**Estimated effort:** 2 hours

## Objective

Take the release-gate map you produced in exercise `04` (or one from a peer or from a public example) and run the **values-baseline overlay audit** described in chapter `05` — walking OECD AI Principles, the Council of Europe Framework Convention, and the UNESCO Recommendation on the Ethics of AI against the assembled evidence, and flagging release-gate obligations the technical frameworks alone would let you miss.

The exercise's output is a **residual finding** — a claim that the assurance case is missing something a values-baseline reader would notice. That finding is the shape of a real assurance-program improvement ticket.

## Prerequisites

- Chapter `05-international-values-baseline.md`.
- Exercise `04` (your own or a peer's) as the base release-gate map.
- OECD AI Principles (`oecd.ai/en/ai-principles`), CoE Framework Convention text, UNESCO Recommendation on the Ethics of AI (open for direct citation).

## Problem statement

Assume the release-gate map from exercise `04` is complete — every EU AI Act article that applies is discharged, every ISO/IEC 42001 clause is mapped, every NIST AI RMF sub-category is plugged. In other words, the *technical* frameworks are satisfied.

Now run the values baseline as a cross-check:

- For each principle in the three instruments, ask: does the assembled evidence support this principle, or does the system's release visibly undercut it?
- Flag every principle where the answer is not clearly "yes." For each flagged principle, propose (a) an additional claim for the assurance case, (b) evidence to attach, or (c) a residual to escalate if the principle cannot be discharged inside the release-gate.

## Requirements

Produce `values-baseline-audit.md` containing:

1. **Base map header.** One paragraph naming the release-gate map you are auditing and the system it covers.
2. **OECD AI Principles pass.** Walk the five values-based principles (inclusive growth / well-being; human rights and democratic values; transparency and explainability; robustness / security / safety; accountability). For each:

   | Principle | Supported by base map? | Where (cite article / clause / sub-category) | If gap: proposed additional claim + evidence | Residual to escalate? |
   | --------- | ---------------------- | -------------------------------------------- | -------------------------------------------- | --------------------- |

3. **Council of Europe Framework Convention pass.** Walk the substantive principles (human dignity, equality, privacy, transparency, accountability, reliability, safe innovation) *and* the procedural principles (documentation, effective remedies, procedural safeguards, risk and impact management). Same table shape.
4. **UNESCO Recommendation pass.** Walk the ten principles (proportionality and do no harm, safety and security, fairness and non-discrimination, sustainability, privacy, human oversight, transparency and explainability, responsibility and accountability, awareness and literacy, multi-stakeholder governance). Same table shape.
5. **Residual-findings memo.** Consolidate the flagged gaps into a one-page memo addressed to the head of AI governance. For each residual finding:
   - State the finding (one sentence).
   - State the values-baseline principle it is grounded in.
   - Propose either a release-gate obligation addition (with cost / effort estimate) or a residual acceptance with rationale.
   - Name who signs the disposition.
6. **Bias check on the audit itself.** In one short section (half a page), reflect on which values-baseline principles you found *hardest* to judge on the assembled evidence. Common candidates: sustainability (environmental impact evidence rarely gathered), effective remedies (the assurance program has no natural authority over legal remedies), awareness and literacy (transparency to auditors ≠ awareness in end-users). Note the pattern — future release-gates should treat these principles as first-class.

## Starter guidance

- **This is a cross-check, not a duplicate release-gate.** If a principle is already discharged by the technical evidence you assembled in exercise `04`, mark "supported" and move on — don't re-litigate.
- **Common finds you should look for**, in order of typical frequency:
  1. *Sustainability* — no environmental-impact evidence for a large-model system.
  2. *Effective remedies* — no channel for affected end-users to appeal an AI-based decision.
  3. *Awareness and literacy* — a system card exists for auditors but not for end-users.
  4. *Proportionality* — a release-gate over-collects personal data for a low-risk deployment, or under-collects red-team coverage for a higher-risk one.
  5. *Multi-stakeholder governance* — no evidence of engagement with affected communities during MAP.
- **Residuals are legitimate.** A release-gate cannot single-handedly deliver every UNESCO or CoE principle; some (e.g. effective remedies through the courts of a specific jurisdiction) are outside the program's authority. Escalate honestly.
- **The disposition-signer matters.** Additions inside the program's scope are signed by this role or the architect; residuals outside its scope are signed by the head of AI governance or higher.

## Acceptance criteria

You have succeeded if:

- All three instruments are walked and every principle in each has a Y / N / partially cell.
- Every "not supported" cell has a proposed additional claim or an explicit residual with a signer.
- The residual-findings memo is one page, addressed to a specific role, and each finding cites the instrument and principle.
- The bias-check section names at least two principles that were hard to judge on the assembled evidence and offers a pattern-level observation.
- The audit does not double-count evidence already accepted by the technical release-gate.

## Stretch goals

- Extend the pass to include the OECD AI Classification Framework categories as a scoping check — is the system's classification consistent with the risk-management measures applied?
- Add a fourth pass over a jurisdiction-specific values instrument (e.g. Australia's Voluntary AI Safety Standard, Japan's METI AI Guidelines, PRC CAC guidance).
- Draft the change to the *program charter* (`mod-112`) that would institutionalise the values-baseline overlay as a standing step, not a one-off audit.
- Present the residual-findings memo to a partner and defend two findings against pushback.
