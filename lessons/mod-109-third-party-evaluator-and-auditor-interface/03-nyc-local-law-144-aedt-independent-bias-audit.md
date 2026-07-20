# NYC Local Law 144 — AEDT Independent Bias Audit

## Motivation

New York City Local Law 144 of 2021 — the Automated Employment Decision Tool law — is the first US municipal statute to mandate an *independent bias audit* as a precondition for lawful deployment of an AI system in an in-scope use case. It took effect 2023-01-01, with enforcement beginning 2023-07-05 following the New York City Department of Consumer and Worker Protection (DCWP) final rules. The law's scope is narrow — employment decisions on candidates for employment or promotion who live in New York City — but its shape is broadly instructive because it prefigures a class of *compliance-driven, use-case-scoped, publicly-published* third-party audits that is very different from the AISI-shape safety evaluation (chapter `01`) or the notified-body conformity assessment (chapter `02`).

The interface differences matter. An AISI-shape evaluator's report is *generally confidential* — findings summarised publicly, payloads and methodological detail withheld. A notified body's certificate is *scoped to a product family* and its underlying dossier is not public. An AEDT independent bias audit produces a *public summary of results* that must be posted on the employer's or employment agency's website and distributed to notice recipients. The release-assurance programme therefore has to design the handoff with the *published output* as a first-class consideration: what the auditor will publish, what the employer will post, and how the assurance case (`mod-102`) has to be able to survive external scrutiny of the numbers.

The interface is also *narrower* than AISI or notified-body engagements. The DCWP prescribes the statistical methodology (selection rates, impact ratios by category), the auditor's independence criteria, and the disclosure format. This means less room for the programme to negotiate the shape of the handoff — but correspondingly more responsibility to prepare the input dataset that the auditor's methodology consumes without contamination or gaps.

This chapter walks what an AEDT is under the law, who the independent auditor is, what a bias audit produces, and how the release-assurance programme prepares the handoff.

## What an AEDT is under Local Law 144

Under the NYC DCWP's final rules ([nyc.gov/site/dca/about/automated-employment-decision-tools.page](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) and the rule text at [rules.cityofnewyork.us/rule/automated-employment-decision-tools-updated/](https://rules.cityofnewyork.us/rule/automated-employment-decision-tools-updated/) <!-- needs-research: verify the current published rule URL post-2024 amendments -->), an Automated Employment Decision Tool is a computational process derived from machine learning, statistical modelling, data analytics, or artificial intelligence that issues a simplified output — a score, classification, or recommendation — that is used to *substantially assist or replace* discretionary decision-making for employment decisions that affect natural persons.

Two aspects of the DCWP definition warrant emphasis. First, the *substantially assist or replace* clause is what pulls a tool into scope: a tool whose output is one input among many that a human decision-maker weighs freely may be out of scope, while a tool whose output is the primary determinant of the decision is in. Second, *employment decisions* under the rule cover hiring and promotion for candidates who live in New York City — the geographic scope pins to the candidate's residence, not the employer's location.

The release-assurance implication: an in-scope AEDT deployment requires a *bias audit completed within one year prior to use*, and re-audit at least annually. The audit is a hard-gate criterion in the release process — a release-gate case for a hiring product covering NYC-resident candidates cannot pass without a current audit.

## Who the independent auditor is

**Who they are.** The DCWP rules define an *independent auditor* as a person or group that is *not* employed by, and does *not* have a material relationship with, the employer, employment agency, or provider of the AEDT. Independence is a hard criterion: it excludes anyone who worked on the design, development, or implementation of the AEDT; anyone who has a direct financial interest in the outcome; and anyone whose independence could reasonably be questioned under the DCWP's tests.

Practically, independent auditors are a mix of specialist HR-analytics consulting firms, employment-law-adjacent quant shops, and Big-Four-shape firms (chapter `04`) that have built a Local Law 144 practice. The market is small and the credentials are practitioner-level rather than institutional — there is no NYC-issued "certified AEDT auditor" registry <!-- needs-research: verify no auditor-certification registry has been introduced since 2024 -->.

**What they ask for.** A dataset representative of the AEDT's operation over a defined historical window — the tool's inputs, the tool's outputs (score / classification / recommendation), the downstream hiring or promotion outcomes tied to each candidate, and the candidate's category tags (race / ethnicity / sex, and their intersections) required for the impact-ratio calculation.

**Handoff envelope.** A structured evidence package: the dataset, a data-dictionary, a methodology memo describing how the AEDT operates and where it sits in the hiring or promotion workflow, a written attestation of the auditor's independence, and a written engagement scope naming the AEDT versions covered and the historical window.

**Release-assurance implication.** The audit is scoped to a specific AEDT (identified by version and use-case) and produces a summary of results the employer or employment agency must post publicly and distribute to candidates. The release-assurance programme's role is to prepare the input dataset well enough that the auditor can execute the DCWP methodology without gaps, without contamination, and without ambiguity in the category tagging.

## What a bias audit produces

The DCWP-prescribed output has a specific shape. Every AEDT bias audit produces:

- **Selection rates by category.** For each intersectional category the rule requires (race/ethnicity crossed with sex), the selection rate — the proportion of candidates in that category who received a positive determination from the AEDT — is computed.
- **Impact ratios.** The impact ratio is the selection rate of a category divided by the selection rate of the most-selected category. The rule specifies the "four-fifths rule" heritage — an impact ratio below 0.8 is a conventional signal of adverse impact — though the law itself does not set a pass/fail threshold on the ratio.
- **Optionally, scoring rates.** For AEDTs that output a continuous score rather than a binary classification, the audit reports mean scores and impact ratios on those scores by category.
- **A summary of results.** A narrative summary suitable for public posting and for distribution to candidates, describing the audit's scope, the categories covered, the results, and — critically — the *source* and *number* of the data used. The summary must not be so aggregated that the underlying data quality is obscured.

The summary is *posted publicly* on the employer's or employment agency's website in a form accessible to candidates, and is distributed to candidates as part of the notice the law requires.

## How the release-assurance programme prepares the input dataset

Dataset preparation is where the programme earns its keep on this interface. Four preparation dimensions matter:

### Representative sample

The dataset must cover the AEDT's operation across the historical window in a way that is *representative* of the deployment context. Sampling artefacts — pulling only the last quarter when the AEDT's behaviour shifted mid-window, pulling only one hiring pipeline when the AEDT feeds several — will bias the audit numbers before the auditor even starts. The programme's evidence pipeline (`mod-104`) is the natural source: the online-eval slice's traces cover the AEDT's operational surface with the coverage attestation the AI-eval engineer produces (`mod-101` deferral contract).

Where the AEDT has been in use for less than the audit's target window, or where sample-size on any category is insufficient for the impact-ratio calculation, the DCWP rules allow a *historical-data* option: the employer may use test data or historical data from a similar AEDT. The programme has to make and document that choice explicitly — a switch to historical data is an evidentiary decision the auditor will inspect.

### Category tagging

Impact ratios require category tags on each candidate. The tags come from candidate self-identification (during the application flow) and from Equal Employment Opportunity data collection where the employer collects it. The programme's role is to ensure the tags are *available* on every row of the dataset and are *not derived by inference* from other features. Inferred category tags — from names, from ZIP codes, from photos — are not acceptable evidence and will invalidate the audit.

### Statistical sufficiency

The impact-ratio calculation requires enough candidates in each category for the ratio to be meaningful. The DCWP rules allow the auditor to exclude a category from the ratio calculation if the sample size falls below a threshold, but they require that fact to be disclosed in the summary. The programme should stress-test the dataset against expected minimum-sample-size thresholds before the auditor receives it, and — where a category is under-sampled — document why (small population in the applicant pool, tool used only for a specific role class, historical-data option invoked) so the auditor can decide how to disclose.

### Data lineage and integrity

Every row in the dataset must be traceable to a specific AEDT operation (input, output, decision context) and to a specific candidate record. Lineage is what allows the auditor to verify the dataset is not a curated sample, and integrity attestation is what allows the summary of results to be defensible against candidate challenge. The `mod-104` chapter `05` MLSec attestations (eval-set-integrity, exfiltration control) provide the shape here; the programme adapts them to the AEDT-audit dataset.

## The candidate-notice obligation

Local Law 144 is unusual among AI-audit regimes in that it imposes a *candidate-facing notice obligation* directly on the employer or employment agency, distinct from the audit itself. Two notice components:

- **Advance notice of AEDT use.** Candidates who reside in New York City and who are subject to an AEDT must be notified at least ten business days before the tool is used, of the tool's use, the job qualifications and characteristics the tool will assess, and (on request) the type of data collected, the source of the data, and the employer's data-retention policy.
- **Availability of the audit summary.** The audit's summary of results must be posted publicly on the employer's or employment agency's website in a form that is accessible to candidates. Some employers also include the summary URL in the advance notice.

The release-assurance programme's role in the notice obligation is *supporting*, not *owning* — the notice is typically owned by the employer's HR or talent function — but the programme has to produce the audit-summary URL and the underlying-data descriptions the notice cites, on the timing the notice requires. Where the audit is not current (older than one year, or scope has shifted), the notice cannot be issued and the AEDT cannot lawfully be used.

## Difference from AISI-shape evaluation

The AEDT audit is instructive precisely because its shape differs from the AISI-shape evaluations of chapter `01` on four axes:

| Axis                        | AISI-shape evaluation                                             | AEDT independent bias audit                                          |
| --------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------- |
| Purpose                     | Safety-driven — elicit and characterise dangerous capabilities    | Compliance-driven — demonstrate the tool does not cause disparate impact |
| Scope                       | Capability-scoped — the whole model or system class               | Use-case-scoped — one AEDT, one employment-decision workflow          |
| Methodology                 | Evaluator-owned, novel, evolving                                  | Prescribed by DCWP rule — selection rates, impact ratios              |
| Confidentiality             | Findings generally confidential; payloads always confidential     | Summary of results is *published publicly* and distributed to candidates |
| Cadence                     | Per-major-release or per-frontier-model                            | At least annual, within one year of first use                         |
| Auditor market              | Small (national safety institutes and a handful of research orgs) | Small (specialist HR-analytics firms plus Big-Four practices)          |

The programme learns two things from setting the two interfaces side by side. First, the *published output* changes how the assurance case has to be built — every number the auditor will publish must survive external scrutiny, including by candidates and by their employment lawyers. Second, the *methodology being prescribed* by the DCWP means the programme's leverage is on the *input side*, not on the evaluation-method side; the input dataset is what determines whether the audit is producible at all.

## Worked example — handing an internal hiring-recommendation product to an AEDT auditor

A provider has built an internal hiring-recommendation product used by their staffing agency subsidiary to rank applicants for entry-level roles. NYC-resident candidates are in scope; the product's output is used to shortlist candidates for a human recruiter to interview, and DCWP considers it to substantially assist the decision. Local Law 144 applies.

The release-assurance programme prepares the handoff:

1. **Auditor selection.** Programme runs a request for proposals; selects an auditor with a documented independence attestation, a Local Law 144 methodology brief, and references from three previous engagements. Contract signed, covering fees, timelines, confidentiality of provider-internal data, and the auditor's right to describe the audit methodology in the summary.
2. **Scope memo.** One-page document naming the AEDT version, the hiring workflow it sits in, the historical window covered (the prior twelve months), the sample-size expectations by category, and the reason for any category exclusions.
3. **Dataset assembly.** Programme queries the online-eval slice (`mod-104`) for all AEDT operations against NYC-resident candidates in the window. Each row carries the AEDT inputs, the AEDT output (recommended-shortlist / not-recommended), the downstream shortlist decision, the interview outcome, the offer outcome, and the candidate's self-identified category tags (from the application form's optional EEO section).
4. **Data-dictionary and lineage attestation.** Programme documents each column of the dataset, its source system, and the transformation applied. Attestation includes the MLSec integrity attestation confirming no rows were dropped or reweighted before delivery.
5. **Category-sufficiency check.** Programme stress-tests the dataset against the auditor's expected minimum-sample-size thresholds; two intersectional categories fall below threshold; programme documents the small applicant-pool reason and invokes the historical-data option per DCWP rule <!-- needs-research: verify the historical-data option is still available under the current DCWP rule -->.
6. **Auditor engagement.** Auditor receives the dataset, runs the DCWP methodology, computes selection rates and impact ratios, and produces a draft summary of results.
7. **Programme review of the summary.** Programme reviews the summary for factual accuracy and for consistency with the underlying dataset (not for methodology adjustment). Where the summary has a factual error, the programme requests a correction; where the summary is unfavourable, the programme does *not* attempt to negotiate the numbers — the auditor's independence is what makes the audit valid.
8. **Publication and distribution.** Employer posts the summary on the careers page, updates the candidate-notice template, and starts the annual re-audit calendar.
9. **Release-gate incorporation.** Programme adds the audit's date, the covered AEDT version, and the summary URL to the release-gate case as an external-evaluator leaf with a validity window of one year.

## What the auditor cannot do — respecting the independence line

The DCWP independence rules place hard limits on what the auditor can accept from the employer and on what the employer can attempt to influence:

- **The auditor cannot receive design input from the employer on the methodology.** The DCWP prescribes the methodology; deviations are the auditor's judgement, not the employer's request.
- **The auditor cannot accept employer-adjusted numbers.** If the auditor's calculation of an impact ratio disagrees with the employer's internal calculation, the auditor's number is authoritative for the summary. The employer's channel for disagreement is factual correction (a data-lineage error, a mis-tagged row) not methodology negotiation.
- **The auditor cannot suppress unfavourable results.** The summary must reflect the audit as run. The employer's response to an unfavourable audit is remediation of the tool, not renegotiation of the summary.

The release-assurance programme's role in respecting the line is to *not ask the auditor to compromise* the line — a request that reads as pressure on the numbers is a serious independence breach and can invalidate the audit. Where the programme wants to discuss the tool's behaviour or its remediation options, that discussion is with the risk engineer (`ai-risk-engineer`, level 25) and the model-evaluation engineer, not with the auditor.

## The AEDT shape as a precedent for other jurisdictions

Local Law 144 is early — first-in-nation for a municipal AEDT audit mandate — and its shape is being adapted in other jurisdictions. Colorado SB 24-205 (the Colorado AI Act) imposes obligations on developers and deployers of high-risk AI systems in the employment and other consequential-decision contexts, with different (and more demanding) documentation obligations <!-- needs-research: verify Colorado SB 24-205 status, effective date, and its interaction with independent-audit obligations -->. Illinois, California, and the EU AI Act (Annex III point 4 on employment) all touch adjacent territory with different mechanisms.

The release-assurance programme's takeaway is that the AEDT-shape audit — compliance-driven, use-case-scoped, publicly-summarised — is likely to appear in multiple jurisdictions the programme's release-gate covers. Designing the input-dataset preparation, category-tagging, and lineage-attestation once, as a reusable capability, is a better bet than treating each jurisdictional audit as bespoke. The `mod-106` cross-jurisdictional crosswalk is where these obligations are consolidated.

## Common failure modes on the AEDT interface

Four failure modes come up repeatedly and are worth designing against.

- **Category tags derived by inference.** The employer's data-collection process failed to capture voluntary self-identification, so the audit team infers demographics from names or ZIP codes. This invalidates the impact-ratio calculation and exposes the employer to a candidate challenge. Fix: instrument the application flow to solicit and store voluntary self-identification.
- **Sample from the wrong window.** The dataset covers a window in which the AEDT was operated in a very different configuration from the current one, so the audit numbers do not reflect current performance. Fix: pin the audit window to a configuration-stable period, and where a configuration change lands mid-window, split the audit into pre- and post-change segments.
- **Summary posted in an inaccessible form.** The summary is posted as a PDF behind a login, or as a graphic that fails screen-reader accessibility, or in a language the candidate does not read. The DCWP-required *accessibility* to candidates is not satisfied. Fix: use the plain-HTML summary template the auditor supplies, on a public URL, in the language of the candidate notice.
- **Annual re-audit calendar drifts.** The first audit lands on 15 March; the second audit lands on 20 April the following year; between 15 March and 20 April the AEDT is being used without a current audit. Fix: put the re-audit calendar entry sixty days before the current audit's one-year expiry so slippage does not create a gap.

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the AEDT auditor is a third-party evaluator row in the external-parties section.
- `mod-102` (assurance case) — the AEDT audit is an external-evaluator leaf with a one-year validity window.
- `mod-103` (release-gate) — the release-gate for hiring or promotion products covering NYC-resident candidates cannot pass without a current audit.
- `mod-104` (evidence pipeline) — the online-eval slice is the natural source for the input dataset; MLSec attestations cover dataset integrity.
- `mod-105` (cards) — the summary of results feeds the fairness section of the external card.
- `mod-106` (cross-jurisdictional mapping) — Local Law 144 sits alongside Colorado SB 24-205, EU AI Act Article 10 (data governance for high-risk systems), and other jurisdictional obligations in the crosswalk.
- `mod-110` (post-market surveillance) — the audit's category coverage is what the surveillance plan monitors between annual audits.

## Summary

- NYC Local Law 144 mandates an independent bias audit as a precondition for lawful deployment of an AEDT that affects NYC-resident candidates for employment or promotion; audits must be completed within one year of first use and at least annually thereafter.
- The independent auditor is a person or group without an employment or material relationship with the employer, employment agency, or AEDT provider; auditor independence is a hard criterion under DCWP rules.
- The audit produces selection rates and impact ratios by intersectional category, plus a summary of results that is posted publicly and distributed to candidates.
- The release-assurance programme's leverage is on the input side: representative sampling, self-identified (not inferred) category tags, statistical sufficiency, and lineage-and-integrity attestation.
- Unlike AISI-shape evaluations, the AEDT audit is compliance-driven, use-case-scoped, methodologically prescribed, and produces a *publicly-posted* summary — the assurance case must survive external scrutiny of the numbers.
- Exercise `03` has you prepare the input dataset and auditor engagement package for a worked hiring-recommendation product and design the annual re-audit calendar.
