# Resources for mod-110-post-market-surveillance (Post-Market Surveillance and Continuous Assurance)

Primary sources first. Every URL below points at the organisation that issues, hosts, or operates the instrument — the Regulation's consolidated text on EUR-Lex, the FDA guidance page, the standards body, the incident registry's canonical URL — so your reading pins to text that survives editorial rewrites. Secondary reading, thematic commentary, and vendor documentation sit at the bottom.

The load-bearing reads for this module differ per chapter. Chapter `01`'s load-bearing reads are the consolidated text of Regulation (EU) 2024/1689 (Articles 9-15, 20, 26, 43, 47, 49, 72, plus Annex III and Annex IV) and the ISO/IEC 42001 clauses (7.5, 9.3, 10.2) that shape controlled-document discipline. Chapter `02`'s are the same Regulation's Articles 3(49), 20, 26(5), 73, and 79, plus GDPR Article 33 for the parallel 72-hour data-breach clock. Chapter `03`'s is the NIST AI RMF 1.0 Playbook (`MANAGE-4.1` and `MANAGE-4.3`). Chapter `04`'s is the FDA guidance on Predetermined Change Control Plans (2024) plus 21 CFR Part 803 (Medical Device Reporting) and Article 72(3)'s equivalence clause. Chapter `05`'s are the three external registries (AIID, OECD.AI AIM, MIT AI Risk Repository) and the sign-and-log stack (Sigstore, Rekor, DSSE). If you read nothing else across the module, read the consolidated EU AI Act text end-to-end for Articles 72 and 73 plus the FDA PCCP guidance — those three primary sources carry the module's statutory backbone.

## Chapter `01` — Article 72 post-market monitoring plan

### EU AI Act primary sources

- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the consolidated Regulation text. Articles 9 (risk management), 10 (data governance), 11 (technical documentation), 12 (record-keeping), 13 (transparency and provision of information to deployers), 14 (human oversight), 15 (accuracy, robustness, and cybersecurity), 17 (quality management system), 20 (corrective actions and duty of information), 26 (obligations of deployers), 43 (conformity assessment), 47 (EU declaration of conformity), 49 (registration), 71 (EU database), 72 (post-market monitoring), 74 (market surveillance), 79 (procedure for AI systems presenting a risk), and Annex III (high-risk AI systems), Annex IV (technical documentation) are the specific citations this chapter uses.
- [European Commission — European AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office landing page.
- [European Commission — AI Act implementing acts and guidance](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — the AI Act policy hub for implementing acts and Commission guidance. <!-- needs-research: verify whether the Commission has published the implementing act laying down the post-market monitoring plan template under Article 72(3) as of 2026-07 -->
- [European Commission — EU database for high-risk AI systems (Article 71)](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the Article 71 register landing page. <!-- needs-research: verify the canonical URL for the Article 71 EU database of registered high-risk AI systems and its API / query interface as of 2026-07 -->

### ISO/IEC standards the plan builds on

- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard whose clauses 7.5 (documented information), 9.3 (management review), and 10.2 (nonconformity and corrective action) discipline the plan as a controlled document.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance the Article 9 risk-management system frequently applies alongside.
- [ISO/IEC 24029-2:2023 — *AI — Assessment of the robustness of neural networks*](https://www.iso.org/standard/79804.html) — the neural-network robustness assessment standard, relevant to the Article 15 robustness declaration. <!-- needs-research: verify current publication status of Part 2 -->
- [ISO/IEC 25059:2023 — *SQuaRE — Quality model for AI systems*](https://www.iso.org/standard/80655.html) — the AI-system quality model.

### Deployer-channel and observability substrate

- [OpenTelemetry — Semantic Conventions for Generative AI](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the observability schema the deployed-system telemetry emits under, consumed by the peer `ai-eval-engineer`. <!-- needs-research: verify the current OpenTelemetry gen-ai semantic convention URL and stability level as of 2026-07 -->
- [OpenInference](https://github.com/Arize-ai/openinference) — the tracing specification for LLM applications, an adjacent substrate.

## Chapter `02` — Article 73 serious-incident workflow

### EU AI Act primary sources

- [Regulation (EU) 2024/1689 — the EU AI Act (consolidated text)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Article 3(49) (serious-incident definition), Article 20 (corrective actions), Article 22 (authorised representatives), Article 26(5) (deployer's duty to inform the provider of a serious incident), Article 43 (conformity assessment — the notified-body interface that is live during a Article 73 event), Article 55 (obligations for providers of GPAI models with systemic risk — the parallel channel to the AI Office), Article 73 (reporting of serious incidents), Article 74 (market surveillance and control of AI systems in the Union market), and Article 79 (procedure at national level for dealing with AI systems presenting a risk) are the specific citations this chapter uses.

### Adjacent EU regimes running in parallel

- [Regulation (EU) 2016/679 — the General Data Protection Regulation (consolidated text)](https://eur-lex.europa.eu/eli/reg/2016/679/oj) — Article 33 (notification of a personal data breach to the supervisory authority) is the 72-hour parallel obligation to Article 73 where personal data is involved. Article 34 (communication of a personal data breach to the data subject) is the downstream notification path.
- [European Data Protection Board (EDPB) — Guidelines on personal data breach notification](https://www.edpb.europa.eu/) — the EDPB landing page. <!-- needs-research: verify current guidelines URL for personal data breach notification and check for AI-Act-specific guidance from EDPB as of 2026-07 -->

### National competent authorities

- [European Commission — designated national competent authorities under the AI Act](https://digital-strategy.ec.europa.eu/en/policies/ai-office) — the AI Office coordinates the network of Member State market-surveillance authorities. <!-- needs-research: verify the canonical list of Member State market-surveillance authorities and their notification channels as of 2026-07; the list of designated Article 70 authorities is being populated on a rolling basis -->

## Chapter `03` — Peer-eval and risk signal into the re-review cycle

### NIST AI RMF and Playbook

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST AI RMF landing.
- [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) — the operational elaboration of the framework. `MANAGE-4.1` (AI risks and benefits from third-party resources are regularly monitored) and `MANAGE-4.3` (incidents and errors are communicated to relevant AI actors) are the specific citations this chapter uses.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific profile that extends the RMF's `MEASURE` and `MANAGE` functions.
- [NIST — Trustworthy and Responsible AI Resource Center (AIRC)](https://airc.nist.gov/) — the AIRC hub.

### Standards clauses the re-review discipline builds on

- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — clauses 9.3 (management review — the trigger register and fire register are standing inputs) and 10.2 (nonconformity and corrective action — the outcome of a re-review that produces a superseding disposition).

### Online-eval and observability substrates the peer `ai-eval-engineer` uses

- [Arize Phoenix](https://phoenix.arize.com/) — the open-source LLM observability and evaluation platform.
- [Langfuse](https://langfuse.com/) — the open-source LLM engineering platform (tracing, evals, prompt management).
- [Weights & Biases — Weave](https://wandb.ai/site/weave) — the LLM tracing and evaluation product.
- [OpenTelemetry — Semantic Conventions for Generative AI](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — the observability schema the substrates converge on.

## Chapter `04` — FDA PCCP and continuous change control

### FDA primary sources

- [FDA guidance — *Predetermined Change Control Plans for Artificial Intelligence-Enabled Device Software Functions* (2024)](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/predetermined-change-control-plans-artificial-intelligence-enabled-device-software-functions) — the finalised guidance defining PCCP's three components.
- [FDA — Software as a Medical Device (SaMD)](https://www.fda.gov/medical-devices/digital-health-center-excellence/software-medical-device-samd) — the SaMD framework the PCCP applies within.
- [FDA — Artificial Intelligence and Machine Learning in Software as a Medical Device](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-software-medical-device) — the AI/ML SaMD action plan hub.
- [FDA / Health Canada / MHRA — Good Machine Learning Practice for Medical Device Development: Guiding Principles (GMLP)](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — the joint GMLP guiding principles the modification protocol frequently cites.
- [21 CFR Part 820 — Quality System Regulation (and QMSR final rule effective 2026-02-02)](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-820) — the QSR clauses PCCP verification activities discharge under. <!-- needs-research: verify the QMSR final-rule effective-date implementation status as of 2026-07 and any transition-period considerations -->
- [21 CFR Part 803 — Medical Device Reporting](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-803) — the MDR reporting obligations that run in parallel with Article 73. <!-- needs-research: verify the current wall-clocks in 21 CFR 803.50 (30-day reports) and 803.53 (5-day reports) as of 2026-07 -->
- [21 CFR Part 801 — Labeling](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-801) — the device-labelling framework PCCP anticipates updates to.

### EU sector-regulatory parallels

- [Regulation (EU) 2017/745 — Medical Device Regulation (MDR)](https://eur-lex.europa.eu/eli/reg/2017/745/oj) — the EU MDR whose post-market-surveillance regime under Chapter VII is the sector-parallel to Article 72 that the Article 72(3) equivalence clause references.
- [Regulation (EU) 2017/746 — In Vitro Diagnostic Regulation (IVDR)](https://eur-lex.europa.eu/eli/reg/2017/746/oj) — the IVDR counterpart for in-vitro diagnostics.
- [Regulation (EU) 2024/1689 — Article 72(3)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the equivalence clause that permits integration of AI-Act monitoring into an existing sector-regulated plan.

### ISO standards the medical-device QMS carries

- [ISO 13485:2016 — *Medical devices — Quality management systems*](https://www.iso.org/standard/59752.html) — the medical-device QMS the tagged evidence store discharges against under the FDA-scope audit view.
- [ISO 14971:2019 — *Medical devices — Application of risk management to medical devices*](https://www.iso.org/standard/72704.html) — the medical-device risk-management standard the PCCP impact assessment converges on.
- [IEC 62304 — *Medical device software — Software life cycle processes*](https://www.iso.org/standard/38421.html) — the software-lifecycle standard for medical-device software.

## Chapter `05` — Incident-DB back-feed and non-compliance escalation

### External incident registries

- [AI Incident Database (AIID)](https://incidentdatabase.ai/) — the Responsible AI Collaborative's registry of AI incidents; the longest-running open registry and the most cited.
- [AIID — API documentation](https://incidentdatabase.ai/apps/discover/) — the discover / query surface. <!-- needs-research: verify the current API endpoint and query interface for AIID as of 2026-07 -->
- [OECD.AI Incidents Monitor (AIM)](https://oecd.ai/en/incidents/) — the OECD's monitor of AI incidents and hazards drawn from global news sources.
- [OECD AI Policy Observatory](https://oecd.ai/) — the wider AI-policy hub that publishes periodic incident reports.
- [MIT AI Risk Repository](https://airisk.mit.edu/) — a categorised database of AI risks drawn from a systematic review of the literature.

### Corrective-action, escalation, and evidence signing

- [Regulation (EU) 2024/1689 — Article 20 (corrective actions and duty of information)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the corrective-action route every forced-downgrade and withdrawal drives.
- [Sigstore project](https://www.sigstore.dev/) — the signing-infrastructure the escalation record is DSSE-signed with.
- [Sigstore — Rekor transparency log](https://docs.sigstore.dev/logging/overview/) — the transparency-log the escalation record and every disposition artefact is logged in.
- [Sigstore — DSSE (Dead Simple Signing Envelope) specification](https://github.com/secure-systems-lab/dsse) — the signing-envelope format the escalation record uses.
- [Sigstore — Fulcio](https://docs.sigstore.dev/certificate_authority/overview/) — the certificate authority whose Fulcio-issued certs the audit verifies signatures against.
- [`in-toto` attestation framework](https://in-toto.io/) — the attestation framework the assurance-store discipline uses.
- [ISO/IEC 42001:2023 — clauses 9.3 and 10.2](https://www.iso.org/standard/81230.html) — management review and corrective action clauses the trigger register, fire register, and escalation record are standing inputs to.

### Adjacent registries and initiatives

- [UK AI Security Institute (formerly UK AI Safety Institute)](https://www.aisi.gov.uk/) — the UK AISI landing page; publishes findings that map into the trigger register. <!-- needs-research: verify whether the UK AISI has launched a national incident registry by 2026-07 or continues to publish via research reports -->
- [US AI Safety Institute (NIST)](https://www.nist.gov/aisi) — the US AISI landing page.
- [Partnership on AI — AI Incident Database contributions](https://partnershiponai.org/) — Partnership on AI's coordination role in incident-registry standardisation.

## Horizontal frameworks all chapters braid with

- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal NIST framework.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the horizontal EU AI regulation.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.

## Adjacent module cross-references

- [`mod-101-release-assurance-position`](../mod-101-release-assurance-position/) — the second-line-of-defence pattern the escalation contract extends; the deferral-contract entries the trigger contract rewrites for the `ai-eval-engineer` and `ai-risk-engineer` peer rows.
- [`mod-102-assurance-case-engineering`](../mod-102-assurance-case-engineering/) — the assurance case whose claims are the anchors re-reviews reopen; the harm inventory the external-registry back-feed cross-checks; the defeaters vocabulary the trigger contract references.
- [`mod-103-release-gate-architecture`](../mod-103-release-gate-architecture/) — the runbook whose incident-cutover and rollback triggers consume the plan's signals; the second-line effective-challenge signer whose co-sign the escalation contract binds; the dashboard where the trigger register is rendered.
- [`mod-104-evaluation-evidence-pipeline`](../mod-104-evaluation-evidence-pipeline/) — the content-addressed store where every scan, every trigger, every disposition, and every escalation record lands as a signed artefact; the assurance bundle whose supersession is the record of a re-review; the `regulatory_scope` and `retention_class` fields that carry the dual-regime tagging.
- [`mod-105-cards-for-external-audiences`](../mod-105-cards-for-external-audiences/) — the external-facing card whose derived paragraphs cite the current post-market-monitoring state.
- [`mod-106-cross-jurisdictional-obligation-mapping`](../mod-106-cross-jurisdictional-obligation-mapping/) — the per-jurisdiction obligation map that pins which post-market monitoring regime applies where.
- [`mod-107-sector-regulated-assurance`](../mod-107-sector-regulated-assurance/) — the wider sector-overlay pattern chapter `04` specialises for PCCP; SR 11-7 ongoing-monitoring, DORA, and MiFID sector rules run in parallel with Article 72 in the same runbook.
- [`mod-108-deployment-tier-gating`](../mod-108-deployment-tier-gating/) — forced-downgrade is a re-review disposition landing on the tier architecture; T3-and-above deployments carry the head-of-AI-governance co-sign requirement.
- [`mod-109-third-party-evaluator-and-auditor-interface`](../mod-109-third-party-evaluator-and-auditor-interface/) — notified-body findings and evaluator reports are one signal class the plan ingests; the certificate-validity re-engagement calendar lands as surveillance-plan entries.
- [`mod-111-gpai-systemic-risk-assurance`](../mod-111-gpai-systemic-risk-assurance/) — the AI Office notification channel that extends the escalation contract for Article 55 GPAI systemic-risk providers.
- [`mod-112-owning-an-assurance-program`](../mod-112-owning-an-assurance-program/) — running the plan, the trigger register, and the escalation contract across a portfolio is the operational core of the programme.

## Suggested reading order for this module

1. Chapter `01`, then read Regulation (EU) 2024/1689 Articles 9-15, 20, 26, and 72 in the consolidated text, plus Annex III and Annex IV. Exercise `01` authors the Article 72 plan.
2. Chapter `02`, then read Articles 3(49), 20, 26(5), 73, and 79 of the same text plus GDPR Article 33. Exercise `02` authors the Article 73 serious-incident workflow.
3. Chapter `03`, then read the NIST AI RMF Playbook `MANAGE-4.1` and `MANAGE-4.3` elaborations and ISO/IEC 42001 clauses 9.3 and 10.2. Exercise `03` authors the trigger contract.
4. Chapter `04`, then read the FDA PCCP guidance and 21 CFR Part 803. Exercise `04` authors the unified monitoring runbook.
5. Chapter `05`, then spend an hour on each of the three registries (AIID, OECD.AI AIM, MIT AI Risk Repository). Exercise `05` authors the ingest procedure and the walked escalation.

You are not expected to memorise every Article's paragraph text, every ISO clause number, every FDA CFR section, or every registry's schema. You are expected to know which primary source owns each obligation, which peer-role registry entries feed each trigger's signal, and to look up the specific citations confidently when the plan, the runbook, or the escalation record needs to reference them.
