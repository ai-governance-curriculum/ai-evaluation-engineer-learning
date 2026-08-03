# mod-107-sector-regulated-assurance: SR 11-7 / OCC 2011-12 / SR 23-4 / FDA GMLP / PCCP / DORA

Walks the release-assurance methodology owner out of the horizontal frameworks (NIST AI RMF, ISO/IEC 42001, EU AI Act) and into the **sector-regulated** ground where an AI system actually deploys — U.S. banking (SR 11-7, OCC 2011-12, SR 23-4), U.S. medical devices (FDA GMLP + PCCP), EU financial-sector operational resilience (DORA), and the supervisory-overlay layer (ECB Banking Supervision, EIOPA, ESMA, U.S. interagency communications, CFPB circulars, EEOC guidance). Each chapter paraphrases the instrument at the level a release-assurance owner needs, threads the adaptation the AI/ML wave requires on top of a shape drafted before it existed, and points at the release-package artefacts the release-gate consumes or emits.

**Estimated effort:** 15 hours

## Learning objectives

- Adapt SR 11-7, OCC 2011-12, and SR 23-4 shape to AI / ML models: three-lines-of-defence structure, effective challenge, model inventory, on-going monitoring, model-risk tiering, third-party-model risk.
- Author an SR-11-7-shaped model-risk-management document set for one AI model, including model description, development test, on-going monitoring, and model performance report.
- Apply FDA Good Machine Learning Practice (GMLP) principles and Predetermined Change Control Plans (PCCP) to an AI/ML-enabled medical-device scenario.
- Read EU DORA (Regulation 2022/2554) obligations that apply when an AI system participates in a critical financial-service function, and integrate ICT-third-party-provider expectations.
- Interpret ECB / EIOPA / ESMA supervisory expectations on AI, FDIC / OCC interagency third-party-risk guidance, CFPB adverse-action-notice circulars, and EEOC / ADA AI guidance for consumer-facing use cases.
- Reason about vendor-platform coverage of the sector-regulated shape: ModelOp Center, Monitaur Governance OS, Fiddler AI.

## Lecture chapters

1. [`01-sr-11-7-and-model-risk-management-adapted-to-ai.md`](01-sr-11-7-and-model-risk-management-adapted-to-ai.md) — SR 11-7 / OCC 2011-12 element by element (model definition and scope, inventory, tiering, effective challenge, development and use, independent validation and on-going monitoring, governance). Three lines of defence, the Model Performance Report standing artefact, and the four joints where AI stresses the 2011 shape (foundation-model reuse, prompt-based and agentic surfaces, evaluation-set contamination, moving upstream).
2. [`02-sr-23-4-third-party-relationships-and-foundation-models.md`](02-sr-23-4-third-party-relationships-and-foundation-models.md) — Interagency Guidance on Third-Party Relationships (2023-06-06) / SR 23-4 lifecycle (planning, due diligence, contract negotiation, on-going monitoring, termination). The seven contract items to fight for with a foundation-model provider; concentration and sub-outsourcing hazards; how SR 23-4 braids with SR 11-7 in the release-package.
3. [`03-fda-gmlp-and-pccp-for-ai-ml-medical-devices.md`](03-fda-gmlp-and-pccp-for-ai-ml-medical-devices.md) — the 10 GMLP guiding principles by lifecycle phase; PCCP's three components (Description of Modifications, Modification Protocol, Impact Assessment); why PCCP is not a mechanism for continuously-learning models; the release-gate criteria that fire on every pre-authorised modification.
4. [`04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md`](04-dora-and-ict-third-party-risk-when-ai-carries-a-critical-function.md) — DORA's five pillars, focused on ICT risk management (Articles 5–16), incident classification (17–23), resilience testing (24–27), and ICT third-party risk (28–44). Article 30(3) mandatory contractual provisions for critical-function arrangements; the ESAs' oversight of designated critical ICT third-party service providers; RTS/ITS pointers.
5. [`05-ecb-eiopa-esma-and-adjacent-supervisory-overlays.md`](05-ecb-eiopa-esma-and-adjacent-supervisory-overlays.md) — the *soft* supervisory-overlay layer above the anchor instruments: ECB Banking Supervision expectations on model risk and AI, EIOPA opinions on AI in insurance, ESMA statements on AI in investment services, U.S. interagency communications. The watch-list process (monthly / quarterly / annual / ad-hoc) that keeps overlay currency in the release-package.
6. [`06-consumer-facing-overlays-cfpb-eeoc-ada-and-vendor-platforms.md`](06-consumer-facing-overlays-cfpb-eeoc-ada-and-vendor-platforms.md) — CFPB Circulars 2022-03 and 2023-03 (adverse-action reasons under ECOA / Regulation B), EEOC 2022 (ADA) and 2023 (Title VII) technical assistance, and the build-versus-buy terrain (ModelOp Center, Monitaur Governance OS, Fiddler AI). The distinction between the *operational layer* a vendor can carry and the *authorship layer* the release-assurance owner cannot outsource.

## Structure

- `01-…md` … `06-…md`: lecture chapters (above).
- [`exercises/`](exercises/): per-exercise prompts. Solutions live in the paired [`ai-evaluation-engineer-solutions`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-solutions) repo.
- [`labs/`](labs/): long-form hands-on labs.
- [`quizzes/`](quizzes/): knowledge checks.
- [`resources.md`](resources.md): external references (primary sources first).

## Suggested pace

- **Chapter `01`** — read once, then skim SR 11-7 and OCC 2011-12 end-to-end (they are short by regulatory standards). Draft your worked-shape system's SR-11-7 element mapping on paper before opening exercise `01`.
- **Chapter `02`** — read after `01`. Read the 2023 Interagency Guidance on Third-Party Relationships alongside; the SR 23-4 announcement letter itself is only a page. Chapter `02` is prerequisite background for exercises `01` and `03` — no dedicated exercise.
- **Chapter `03`** — read alongside the FDA GMLP page and the PCCP final guidance (December 2024). Exercise `02` produces a GMLP-plus-PCCP submission shape for a SaMD scenario.
- **Chapter `04`** — read after `03`. DORA's Level-1 text is long (roughly 100 articles); read the pillar-preambles and the specific articles chapter `04` cites, and let the RTS/ITS remain a reference. Exercise `03` develops Article 30(3) clauses.
- **Chapter `05`** — read the sectoral supervisors' landing pages alongside the chapter — the primary sources shift, and the chapter is written to be robust to that shift. Exercise `04` produces overlay applicability memos and a watch-list-currency statement.
- **Chapter `06`** — read the CFPB circulars and EEOC technical assistance directly; each is short and the release-package language draws directly from them. Exercise `05` produces the consumer-facing-overlay row and a vendor-coverage map.

## Dependencies

- Requires mod-101 (release-assurance position — the four bodies of literature the programme maps to), mod-102 (assurance-case engineering — sector obligations sit as branches of the case), mod-103 (release-gate architecture — the sector-rule-citation field, tier mapping to MRM tier), mod-104 (evaluation evidence pipeline — SR-11-7 and DORA artefacts flow through the pipeline), mod-105 (cards for external audiences — the SaMD labelling artefact is the FDA sibling of a system card), and mod-106 (cross-jurisdictional obligation mapping — the sector overlay is a per-jurisdiction column).
- Consumed by mod-108 (deployment-tier gating — MRM tier is one feeder), mod-109 (third-party evaluator and auditor interface — MRM validators, notified bodies, and DORA-designated auditors compose here), mod-110 (post-market surveillance — SR-11-7 on-going monitoring, GMLP principle 10, DORA Articles 17–23), mod-111 (GPAI systemic-risk assurance — the provider side of the SR-23-4 / DORA arrangement), and mod-112 (owning an assurance program — the release-assurance methodology's subordination to the entity's MRM policy).
- All three capstone projects consume this module where the invented system deploys into a regulated sector.
