# Resources for mod-108-deployment-tier-gating

Primary sources first. Every URL below points at the organisation that issues or hosts the instrument — the lab's own publication page, the standards body, the summit's official site, the benchmark's canonical URL — so your reading pins to text that survives editorial rewrites. Secondary reading, thematic communications, and vendor documentation sit at the bottom.

The frontier-lab publications and the multilateral summit outcomes are the load-bearing reads for this module. If you read nothing else, read one of the three source frameworks end-to-end and the Seoul Frontier AI Safety Commitments.

## The three source frameworks (chapter `01`)

### Anthropic Responsible Scaling Policy (RSP)

- [Anthropic — Responsible Scaling Policy](https://www.anthropic.com/rsp) — the current Responsible Scaling Policy landing page.
- [Anthropic — Responsible Scaling Policy announcement (2023-09)](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — the original announcement of the RSP.
- [Anthropic — Core Views on AI Safety](https://www.anthropic.com/news/core-views-on-ai-safety) — the surrounding safety-view context in which the RSP sits.
- [Anthropic — Usage Policies](https://www.anthropic.com/legal/aup) — the acceptable-use policy the enterprise deployer contracts against. <!-- needs-research: confirm the current URL and version for the Anthropic usage/acceptable-use policy; the URL structure has changed. -->

### OpenAI Preparedness Framework

- [OpenAI — Safety and Preparedness](https://openai.com/safety/preparedness/) — the Preparedness Framework landing page.
- [OpenAI — Preparedness Framework announcement (2023-12)](https://openai.com/index/openai-preparedness-framework/) — the original announcement. <!-- needs-research: verify the current canonical URL for the Preparedness Framework document; subsequent revisions have appeared, and OpenAI has reorganised the page. -->
- [OpenAI — Usage Policies](https://openai.com/policies/usage-policies/) — the enterprise deployer contracts against these.
- [OpenAI — SWE-bench Verified announcement](https://openai.com/index/introducing-swe-bench-verified/) — reference for the SWE-bench Verified subset the tier gate cites.

### Google DeepMind Frontier Safety Framework (FSF)

- [Google DeepMind — Introducing the Frontier Safety Framework (2024-05)](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — the original FSF announcement blog.
- [Google DeepMind — Frontier Safety Framework (PDF)](https://deepmind.google/public-policy-and-ethics/) — the DeepMind public-policy-and-ethics landing page; the FSF document is linked here. <!-- needs-research: verify the current direct PDF URL for the Frontier Safety Framework document and any updated version. -->

### Adjacent frontier-lab publications (context reading)

- [Meta — Frontier AI Framework](https://ai.meta.com/static-resource/meta-frontier-ai-framework/) — Meta's frontier framework; complementary read.
- [Microsoft — Responsible AI Standard](https://www.microsoft.com/en-us/ai/responsible-ai) — Microsoft's responsible-AI landing page.

## Capability-evidence benchmarks (chapter `02`)

### Safety-side benchmarks

- [HarmBench](https://www.harmbench.org/) — the HarmBench reference site.
- [HarmBench paper — Mazeika et al., 2024 (arXiv:2402.04249)](https://arxiv.org/abs/2402.04249) — the associated arXiv paper.
- [AIR-Bench 2024 — repo](https://github.com/stanford-crfm/air-bench-2024) — the reference repository. <!-- needs-research: verify canonical URL and the current version of AIR-Bench 2024 and its associated paper (Zeng et al.). -->
- [SafetyBench paper — Zhang et al., 2023 (arXiv:2309.07045)](https://arxiv.org/abs/2309.07045) — the SafetyBench paper.
- [SafetyBench — repo](https://github.com/thu-coai/SafetyBench) — the reference implementation. <!-- needs-research: verify current URL for the SafetyBench dataset and any updated version. -->
- [AgentDojo](https://agentdojo.spylab.ai/) — the AgentDojo reference site. <!-- needs-research: confirm the current canonical URL; the SPY Lab hosting URL has been stable but may move. -->
- [AgentDojo paper — Debenedetti et al., 2024 (arXiv:2406.13352)](https://arxiv.org/abs/2406.13352) — the associated arXiv paper.
- [InjecAgent paper — Zhan et al., 2024 (arXiv:2403.02691)](https://arxiv.org/abs/2403.02691) — the InjecAgent paper.
- [InjecAgent — repo](https://github.com/uiuc-kang-lab/InjecAgent) — the reference implementation. <!-- needs-research: verify current canonical repository URL. -->

### Capability-side benchmarks

- [SWE-bench](https://www.swebench.com/) — the SWE-bench reference site.
- [SWE-bench paper — Jimenez et al., 2023 (arXiv:2310.06770)](https://arxiv.org/abs/2310.06770) — the original SWE-bench paper.
- [SWE-bench Verified — announcement](https://openai.com/index/introducing-swe-bench-verified/) — the Verified subset announcement.
- [τ-bench paper — Yao et al., 2024 (arXiv:2406.12045)](https://arxiv.org/abs/2406.12045) — the τ-bench paper.
- [τ-bench — repo](https://github.com/sierra-research/tau-bench) — the reference implementation. <!-- needs-research: verify the canonical repo URL; multiple mirrors exist. -->
- [GAIA paper — Mialon et al., 2023 (arXiv:2311.12983)](https://arxiv.org/abs/2311.12983) — the GAIA paper.
- [GAIA leaderboard on Hugging Face](https://huggingface.co/spaces/gaia-benchmark/leaderboard) — the reference leaderboard hosting.
- [CyBench paper — Zhang et al., 2024 (arXiv:2408.08926)](https://arxiv.org/abs/2408.08926) — the CyBench paper. <!-- needs-research: confirm the current canonical CyBench URL and any updated version. -->

### Adjacent evaluation methodology

- [MLCommons AI Safety benchmark](https://mlcommons.org/benchmarks/ai-safety/) — the MLCommons AI Safety working group's benchmark.
- [HELM (Holistic Evaluation of Language Models)](https://crfm.stanford.edu/helm/) — Stanford CRFM's holistic evaluation suite.
- [BIG-bench](https://github.com/google/BIG-bench) — the broader capability benchmark; historical anchor for the field.
- [MMLU paper — Hendrycks et al., 2020 (arXiv:2009.03300)](https://arxiv.org/abs/2009.03300) — the MMLU paper; historical baseline citation.

## Cybersecurity frameworks (chapter `03`)

### NCSC / CISA Guidelines for Secure AI System Development

- [NCSC — Guidelines for Secure AI System Development](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development) — the NCSC hosting.
- [CISA — Guidelines for Secure AI System Development](https://www.cisa.gov/resources-tools/resources/guidelines-secure-ai-system-development) — CISA's co-hosting.
- [NCSC — announcement of the joint guidelines (2023-11)](https://www.ncsc.gov.uk/news/uk-develops-new-global-guidelines-ai-security) — the original announcement.
- [CISA — announcement of the joint guidelines (2023-11)](https://www.cisa.gov/news-events/news/cisa-and-uk-national-cyber-security-centre-ncsc-publish-joint-guidelines-secure-ai-system) — CISA's announcement. <!-- needs-research: verify the current signatory list — the initial publication cited 21 international partners; additional signatories have been added since. -->

### Google Secure AI Framework (SAIF)

- [safety.google — Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) — the SAIF landing page.
- [Google — SAIF announcement (2023-06)](https://blog.google/technology/safety-security/introducing-googles-secure-ai-framework/) — the original SAIF announcement.
- [Google — SAIF risk-assessment tool](https://saif.google/) — the interactive SAIF map and risk-assessment tool.
- [Coalition for Secure AI (CoSAI)](https://www.coalitionforsecureai.org/) — the associated CoSAI programme.

### OWASP Top 10 for LLM Applications

- [OWASP — Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — the OWASP project landing page. <!-- needs-research: verify the current published version of the OWASP LLM Top 10 (the 2025 revision restructured several categories; confirm the current v1.x or v2 numbering and identifiers). -->
- [OWASP — Top 10 for LLM Applications repository](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications) — the source repository.
- [OWASP — Top 10 for LLM Applications 2025 release (PDF)](https://genai.owasp.org/) — the GenAI Security Project landing that hosts the 2025 release materials. <!-- needs-research: verify the direct URL for the current 2025 PDF release; the GenAI Security Project has reorganised its documents. -->

### MITRE ATLAS

- [MITRE ATLAS](https://atlas.mitre.org/) — the ATLAS reference site.
- [MITRE ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) — the tactics-and-techniques matrix.
- [MITRE ATLAS on GitHub](https://github.com/mitre-atlas) — the ATLAS GitHub organisation.
- [MITRE ATT&CK](https://attack.mitre.org/) — the reference framework ATLAS is modelled on.

## Reversal-side references (chapter `04`)

The reversal-side dispositions do not have a dedicated framework; they compose out of the frontier-lab frameworks (which each pre-commit to a not-deploy pathway) and out of general-purpose incident-response and change-management practice.

- [NIST SP 800-61 rev. 3 — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r3/final) — the reference cyber incident-response guide the AI incident-response bridges to. <!-- needs-research: confirm current revision number and publication year for SP 800-61; the guide has been through multiple revisions. -->
- [NIST SP 800-53 rev. 5 — Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) — the reference security-control catalogue; incident-response and change-management controls.
- [NIST AI RMF 1.0 — MANAGE function (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the MANAGE function including MANAGE-2 (risk-response actions) and MANAGE-4 (post-deployment monitoring and response).
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard; clauses on operations, monitoring, incident response, and continual improvement apply.

## Multilateral commitments (chapter `05`)

### Bletchley (2023-11)

- [UK Government — AI Safety Summit 2023: The Bletchley Declaration](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration) — the declaration text.
- [UK Government — AI Safety Summit 2023: chair's summary](https://www.gov.uk/government/publications/ai-safety-summit-2023-chairs-statement-day-1-1-november) — additional summit outputs. <!-- needs-research: confirm signatory count (initially 28 countries + EU) and any subsequent additions. -->

### Seoul (2024-05)

- [UK Government — Seoul Declaration for safe, innovative and inclusive AI](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — the Seoul Declaration text.
- [UK Government — Frontier AI Safety Commitments, AI Seoul Summit 2024](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — the 16-company Frontier AI Safety Commitments text. <!-- needs-research: verify the current list of signatory companies (initial 16) and any additions. -->
- [UK Government — Seoul Ministerial Statement (2024-05)](https://www.gov.uk/government/publications/seoul-ministerial-statement-for-advancing-ai-safety-innovation-and-inclusivity-ai-seoul-summit-2024) — the ministerial statement.

### Paris (2025-02)

- [Élysée — Sommet pour l'action sur l'IA](https://www.elysee.fr/en/sommet-pour-l-action-sur-l-ia) — the Paris AI Action Summit landing page. <!-- needs-research: confirm the exact current URL and specific outcome document titles for the Paris summit. -->
- [France Diplomacy — Paris AI Action Summit outcomes](https://www.diplomatie.gouv.fr/en/french-foreign-policy/digital-diplomacy/artificial-intelligence-summits/) — French MFA hosting of summit outcomes. <!-- needs-research: verify the current URL for the summit outcomes on France Diplomacy. -->

### Frontier Model Forum

- [Frontier Model Forum](https://www.frontiermodelforum.org/) — the FMF landing page.
- [Frontier Model Forum — About](https://www.frontiermodelforum.org/about/) — the founding-members and mission page. <!-- needs-research: verify current FMF membership beyond the founding members (Anthropic, Google, Microsoft, OpenAI); further members may have joined. -->
- [Frontier Model Forum — publications](https://www.frontiermodelforum.org/updates/) — the publications and updates feed the enterprise programme reads as a public library.

### AI Safety Institutes (safety-testing partners)

- [UK AI Safety Institute](https://www.aisi.gov.uk/) — the UK AISI landing page.
- [US AI Safety Institute (NIST)](https://www.nist.gov/aisi) — the US AISI landing page.
- [International Network of AI Safety Institutes](https://www.commerce.gov/news/press-releases/2024/11/first-ever-international-network-ai-safety-institutes-set-launch-san) — the multilateral network of AISIs.

## Horizontal frameworks the tier gate braids with

- [NIST AI RMF 1.0 (AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework) — the horizontal U.S. AI risk-management framework.
- [NIST AI 600-1 — Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) — the GenAI-specific profile.
- [ISO/IEC 42001:2023 — *AI management system*](https://www.iso.org/standard/81230.html) — the AIMS standard.
- [ISO/IEC 23894:2023 — *AI — Guidance on risk management*](https://www.iso.org/standard/77304.html) — the risk-management guidance.
- [Regulation (EU) 2024/1689 — the EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — the EU horizontal AI regulation. Article 15 (accuracy, robustness, cybersecurity) and Article 55 (GPAI systemic-risk obligations) are the specific articles the tier gate discharges.
- [OECD AI Principles](https://oecd.ai/en/ai-principles) — the internationally-aligned principle set.

## Adjacent module cross-references

The tier gate composes with several other modules; the reference points there are:

- [`mod-101-release-assurance-position`](../mod-101-release-assurance-position/) — the release-assurance methodology owner's position and the four bodies of literature.
- [`mod-102-assurance-case-engineering`](../mod-102-assurance-case-engineering/) — the assurance case the tier claim lands in.
- [`mod-103-release-gate-architecture`](../mod-103-release-gate-architecture/) — the release-gate walker and the surface-specific tier variants (chapter `05` runbook).
- [`mod-104-evaluation-evidence-pipeline`](../mod-104-evaluation-evidence-pipeline/) — the evidence pipeline the tier-decision artefact slots into and the digest-pinning discipline.
- [`mod-105-cards-for-external-audiences`](../mod-105-cards-for-external-audiences/) — the derived external-facing paragraphs.
- [`mod-106-cross-jurisdictional-obligation-mapping`](../mod-106-cross-jurisdictional-obligation-mapping/) — the per-jurisdiction obligation map the tier gate references.
- [`mod-107-sector-regulated-assurance`](../mod-107-sector-regulated-assurance/) — the sector-regulated overlays that add sub-sections to the tier-decision artefact.
- [`mod-109-third-party-evaluator-and-auditor-interface`](../mod-109-third-party-evaluator-and-auditor-interface/) — external auditors and notified bodies who read the tier-decision artefact.
- [`mod-110-post-market-surveillance`](../mod-110-post-market-surveillance/) — the periodic re-evaluation channel that triggers the reversal dispositions.
- [`mod-111-gpai-systemic-risk-assurance`](../mod-111-gpai-systemic-risk-assurance/) — the GPAI systemic-risk obligations (EU AI Act Article 55) the tier gate composes with.
- [`mod-112-owning-an-assurance-program`](../mod-112-owning-an-assurance-program/) — the operating model that owns the tier-scheme template and the escalation contract.

## Suggested reading order for this module

1. Chapter `01`, then read at least one of the three source frameworks end-to-end (the Anthropic RSP is shortest; the FSF and Preparedness are next). If you internalise the shape — capability evidence → tier → mitigation obligation, pre-committed and publishable — the rest of the module follows.
2. Chapter `02`, then read one benchmark paper per family (HarmBench for safety, SWE-bench Verified for capability, AgentDojo for tool-use robustness). The point is not to memorise the benchmarks; it is to distinguish what the peer track produces from what the methodology owner reads. Exercise `02` authors a threshold-spec set.
3. Chapter `03`, then read the NCSC / CISA Guidelines, the OWASP LLM Top 10 landing page, and the MITRE ATLAS matrix. SAIF is short and conceptual; the other three carry the concrete weight. Exercise `03` produces the four-framework attestation section.
4. Chapter `04`, then re-skim `mod-103` chapter `05` (runbook) if you have not recently. Exercise `04` designs the four dispositions and the escalation contract.
5. Chapter `05` alongside the Seoul Frontier AI Safety Commitments and one Frontier Model Forum publication. Exercise `05` composes the full tier-decision artefact end-to-end.

You are not expected to memorise every framework's numbering or every benchmark's version. You are expected to know which frontier-lab publication owns each shape, what the tier gate consumes from each peer track, and to look up the exact identifier confidently when a tier-decision artefact needs to cite it.
