# mod-112-owning-an-assurance-program: Owning an Enterprise AI-Evaluation-Assurance Program

**Estimated effort:** 14 hours

This is the capstone module of the AI Evaluation Engineer track. The preceding eleven modules gave you the methodology — the release-gate architecture, the assurance case, the evidence pipeline, the audience-appropriate cards, the cross-jurisdictional mapping, the sector overlays, the deployment-tier gating, the third-party-evaluator interface, the post-market loop, and the GPAI systemic-risk assurance surface. This module turns the methodology into a *running function*: a team-scope assurance programme with an intake queue, a decision log, an exception log, a deferred-approval log, an effective-challenge convention, contracts with the six peer tracks, interfaces upward to the senior architect and head of AI governance and outward to external supervisors, a defensible build-vs-buy stance across the vendor landscape, and an incident-driven roadmap.

The module is written from the level-35 assurance owner's chair. It does not assume you have institution-scope authority; it assumes you are inheriting or authoring a team-scope programme that has to defend its posture against auditors, its capacity against peer-track absorption, its authority against over-reach, and its investment against fashion.

## Learning objectives

- Design the operating model for a team-scope AI-evaluation-assurance program: intake-to-decision cycle, evidence-package versioning, exception log, deferred-approval log, second-line effective-challenge convention, and reporting-line contract with `head-of-ai-governance` (level 60)
- Contract with peer / prerequisite tracks: `ai-governance-analyst` (intake, inventory, first-draft cards), `ai-risk-engineer` (harm models, adversarial-eval, guardrails), `ai-eval-engineer` (app-layer eval evidence), `model-evaluation-engineer` (methodology depth), `ai-infra-security` (eval-set-security, judge supply-chain), `agentic-safety-engineer` (frontier-agent evidence for GPAI use cases)
- Interface with `senior-ai-governance-architect` (level 50) for control-library coverage, cross-jurisdiction reconciliation, and policy taxonomy
- Interface with the European AI Office (and equivalent supervisory bodies) for regulator communications and the appropriate route of escalation from a team-scope program to institution-scope leadership
- Make the build-vs-buy decision across governance-platform surfaces: Credo AI, Holistic AI, ModelOp Center, ServiceNow AI Control Tower, IBM watsonx.governance, Fiddler AI, Monitaur — with an explicit fit-vs-gap analysis against the operating model
- Read enterprise responsible-AI standards (Microsoft Responsible AI Standard v2, Google Responsible AI Toolkit, AWS Responsible AI Overview) as reference worked examples for the internal standard the assurance program authors and enforces
- Prioritise incident-driven investment: how a specific incident from the AI Incident Database, OECD.AI Incidents Monitor, or an internal near-miss log rewrites the next quarter's release-gate roadmap

## Chapters

1. [`01-operating-model-and-the-effective-challenge-convention.md`](01-operating-model-and-the-effective-challenge-convention.md) — the six-stage intake-to-decision cycle; evidence-package versioning (MAJOR / MINOR / PATCH); the decision, exception, and deferred-approval logs; the effective-challenge convention borrowed from Federal Reserve SR 11-7; the reporting-line contract with the head of AI governance; the classes of decision the programme may not make alone.
2. [`02-peer-track-contract-matrix.md`](02-peer-track-contract-matrix.md) — the compact six-row matrix that carries the artefact schema, freshness contract, sign-off party, escalation path, and reciprocal owed-back list for `ai-governance-analyst`, `ai-risk-engineer`, `ai-eval-engineer`, `model-evaluation-engineer`, `ai-infra-security`, and `agentic-safety-engineer`; cross-peer routing rules for judge quality, fairness, adversarial eval, and trace-instrumentation coverage.
3. [`03-senior-architect-head-of-governance-and-external-supervisor-interfaces.md`](03-senior-architect-head-of-governance-and-external-supervisor-interfaces.md) — interfaces *upward* to the senior architect (control library, policy taxonomy, cross-jurisdiction reconciliation) and the head of AI governance (institution-scope decisions, risk-appetite, board reporting), and *outward* to the European AI Office, competent Member State authorities, sector supervisors, independent auditors, and notified bodies; the escalation-contract shape restated at each interface.
4. [`04-build-vs-buy-governance-platform-fit-vs-gap.md`](04-build-vs-buy-governance-platform-fit-vs-gap.md) — the ten capability surfaces the programme's tooling substrate has to cover; a pass / partial / fail fit-vs-gap analysis against Credo AI, Holistic AI, ModelOp Center, ServiceNow AI Control Tower, IBM watsonx.governance, Fiddler AI, and Monitaur; the migration-risk lens on evidence-schema lock-in; Microsoft, Google, and AWS's public responsible-AI standards read as shape references for the internal standard the programme authors.
5. [`05-incident-driven-roadmap-prioritisation.md`](05-incident-driven-roadmap-prioritisation.md) — the ritual that translates AIID, OECD.AI Incidents Monitor, MIT AI Risk Repository, and internal-near-miss-log signal into release-gate evidence-gap rows; the `(likelihood-in-your-inventory × severity-if-repeated) ÷ cost-to-close` ranking formula; the reactive-vs-preventive split; the escalation packet for gaps a release-gate change alone cannot close; the quarterly roadmap-review ritual with the head of AI governance.

## Exercises

Each exercise operationalises one chapter for a realistic, self-scoped organisation. All five exercises are design-and-authoring work; the solutions live in the paired `-solutions` repository.

1. [`exercises/exercise-01-operating-model-and-effective-challenge-convention.md`](exercises/exercise-01-operating-model-and-effective-challenge-convention.md) — author the operating-model handbook for a self-scoped organisation: intake-to-decision loop, versioning convention, three registers, effective-challenge rotation, and reporting-line contract.
2. [`exercises/exercise-02-peer-track-contract-matrix.md`](exercises/exercise-02-peer-track-contract-matrix.md) — author the six-row peer-track contract matrix, defend each row against the counterparty peer's proxy, and rehearse the escalation path for a broken contract.
3. [`exercises/exercise-03-senior-architect-and-head-of-governance-interface.md`](exercises/exercise-03-senior-architect-and-head-of-governance-interface.md) — draft the interface specifications with the senior architect and the head of AI governance and rehearse the escalation contract for a first-time market-surveillance request from a competent Member State authority.
4. [`exercises/exercise-04-build-vs-buy-platform-fit-gap-analysis.md`](exercises/exercise-04-build-vs-buy-platform-fit-gap-analysis.md) — run the fit-vs-gap analysis across the vendor landscape for your operating model; defend the build / buy split against a procurement counterparty; own the evidence schema.
5. [`exercises/exercise-05-incident-driven-roadmap-prioritisation.md`](exercises/exercise-05-incident-driven-roadmap-prioritisation.md) — run the ritual against a real incident from AIID or the OECD.AI Incidents Monitor; produce the evidence-gap rows and the escalation packet; defend the ranking against your peer leads and the head of AI governance.

## Structure

- `01-…md` … `05-…md`: lecture chapters.
- `exercises/`: per-exercise prompts.
- `labs/`: long-form hands-on labs (deferred).
- `quizzes/`: knowledge checks (deferred).
- `resources.md`: external references, primary sources first.

## Suggested reading order

Read chapter `01` end-to-end first — everything downstream sits on the operating model. Then read chapter `02` for the input side and chapter `03` for the output side; the two are mirror images. Read chapter `04` next to fix the tooling substrate the running loop uses. Finish with chapter `05` — the incident-driven ritual is what re-visits chapters `01`–`04` on a quarterly cadence and keeps the programme honest.

If you read nothing else across the module, read the [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) second-line-of-defence pattern that grounds chapter `01`'s effective-challenge convention, [ISO/IEC 42001](https://www.iso.org/standard/81230.html) clauses 5 (leadership) and 9.3 (management review) that discipline the reporting-line contract, and one of Microsoft's, Google's, or AWS's public responsible-AI standards straight through as a shape reference for what the programme authors internally.
