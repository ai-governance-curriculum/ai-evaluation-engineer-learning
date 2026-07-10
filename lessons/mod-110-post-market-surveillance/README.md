# mod-110-post-market-surveillance: Post-Market Surveillance and Continuous Assurance

> Scaffolded by `aicg org execute-plan`. Lecture chapters and exercise content are authored on subsequent autonomous cycles.

**Estimated effort:** 12 hours

## Learning objectives

- Design the EU AI Act Article 72 post-market monitoring plan — the concrete telemetry, incident-log, drift-detection, and re-review triggers that satisfy the Article's expectations
- Design Article 73 incident-reporting workflow (serious-incident timelines, root-cause conservatism, notification to competent authorities)
- Wire application-layer online-eval and regression signal (consumed from `ai-eval-engineer` at level 30) into the assurance re-review cycle; wire risk-signal (consumed from `ai-risk-engineer` at level 25) into the same cycle
- Adopt the FDA PCCP shape for on-going ML change control where the sector applies, and reason about the interaction between PCCP and Article 72
- Back-feed incident evidence from the AI Incident Database, OECD.AI Incidents Monitor, and internal incident logs into re-review triggers so the assurance program updates against real-world evidence — depth in incident-response is owned by `ai-risk-engineer`
- Design the non-compliance escalation path — deferred-approval, forced-downgrade, and 'do-not-deploy' outcomes
- Coordinate deployer registrations across EU-member-state deployer registries where required

## Structure

- `01-…md` … `0N-…md`: lecture chapters.
- `exercises/`: per-exercise prompts.
- `labs/`: long-form hands-on labs.
- `quizzes/`: knowledge checks.
- `resources.md`: external references.
