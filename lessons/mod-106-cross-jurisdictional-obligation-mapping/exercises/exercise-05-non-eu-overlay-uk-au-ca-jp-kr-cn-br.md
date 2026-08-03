# exercise-05: Non-EU Jurisdictional Overlay — UK, Australia, Canada, Japan, South Korea, PRC, Brazil

**Estimated effort:** 3 hours

## Objective

Extend the map from exercises `01`–`04` with the **non-EU jurisdictional overlay** — UK (ICO AI guidance under UK GDPR), Australia (Voluntary AI Safety Standard + Privacy Act APPs), Canada (AIDA proposed + Quebec Law 25 + PIPEDA), Japan (METI AI Guidelines for Business + APPI + AI Promotion Act 2025), South Korea (AI Framework Act + PIPA), PRC (CAC Interim Measures for GenAI + PIPL + DSL + TC260-003), and Brazil (PL 2338/2023 + LGPD). Cross-reference shared deliverables with the EU AI Act anchor; add genuinely new rows for individual-rights obligations, substantive content requirements, jurisdiction-specific filings, and pending-instrument placeholders.

The exercise emphasises the mechanical discipline: not every jurisdiction applies, and each `applies_when` must be a *determined* classification with an evidence pointer and a legal-counsel signoff — not a default assumption.

## Prerequisites

- Chapter [`06-non-eu-jurisdictional-overlay.md`](../06-non-eu-jurisdictional-overlay.md).
- Exercises [`exercise-01`](exercise-01-eu-ai-act-obligation-to-deliverable-map.md), [`exercise-02`](exercise-02-nist-rmf-genai-profile-crosswalk.md), [`exercise-03`](exercise-03-iso-clauses-crosswalk.md), [`exercise-04`](exercise-04-us-state-overlay-colorado-nyc-cfpb-eeoc.md).
- Primary sources for the seven overlays (all listed in `resources.md`, but you should skim the ICO's AI guidance page, the Australian VAISS PDF, the ISED AIDA companion document, the METI AI Guidelines page, the Korean AI Framework Act summary, the CAC Interim Measures notice, and the PL 2338 Senate text).

## Problem statement

You will pick a **subset** of the seven overlays that your system's actual deployment surface triggers. The choice is a scoping call; it is not "all seven, always." Then, for each in-scope overlay:

1. Produce a per-jurisdiction scoping determination (legal-counsel signoff, evidence pointer, effective date).
2. Add the overlay rows to the map — cross-referencing shared deliverables to anchor rows, adding genuinely new rows where the obligation is jurisdiction-specific.
3. Handle *pending-instrument* rows honestly — AIDA and Brazil PL 2338 are not enacted; the rows must be `status: pending-instrument` and pre-populated.
4. Handle *gate-preceding* rows honestly — PRC algorithm filing, Korean in-country representative appointment, EU Article 49 registration (already on the anchor map). These block release; the map row records the artefact and the release gate depends on it.
5. Record cross-border data-storage implications for evidence pointers where the evidence store's location matters for a jurisdiction (particularly PRC / Korea / EU).

## Requirements

Produce five artefacts.

### 1. `non-eu-scoping-decisions.md`

For each of the seven jurisdictions, a short determination:

- **UK.** Is the system available to UK data subjects? Which regulator remits are triggered (ICO / FCA / MHRA / Ofcom / CMA)? Article 22 UK GDPR determination (solely automated? human-in-loop enough to take out of Article 22?).
- **Australia.** Is the system available to Australian users? APP applicability? VAISS voluntary adherence stance (adopting, partial, not adopting, and why).
- **Canada.** Is the system available to Canadian users? AIDA pending-in-force posture. Quebec Law 25 Article 22 applicability. PIPEDA / provincial-privacy-law posture.
- **Japan.** Is the system offered in Japan? METI-guideline actor typing (developer / provider / business user / multiple)? APPI cross-border transfer scenario. AI Promotion Act 2025 registration / cooperation applicability.
- **South Korea.** High-impact-AI classification determination. Foreign-provider representative applicability. PIPA automated-decision applicability.
- **PRC.** Territorial scope determination (is the service provided to the public in the PRC?). Algorithm-filing and security-assessment applicability. Substantive-content-policy applicability.
- **Brazil.** LGPD applicability. PL 2338 pending-in-force posture; if enacted, prohibited-risk and high-risk classification.

For each: the classification, the reasoning, the legal-counsel signoff (name + date), the evidence pointer.

Where a jurisdiction is out of scope, the file explicitly records `not-in-scope` with a determination trail. Silence is not an option.

### 2. `non-eu-extended-map.yaml`

The exercise-`04` map, extended with the in-scope non-EU overlay rows. Every anchor row that a non-EU overlay row shares a deliverable with gains a `sibling_jurisdictions` entry:

```yaml
sibling_jurisdictions:
  - instrument: au-vaiss
    row: au-vaiss.g2.risk-management
    relation: shares-deliverable
  - instrument: kr-ai-framework
    row: kr-ai-framework.high-impact.risk-management
    relation: contributes-to
  - instrument: ca-aida
    row: ca-aida.risk-mitigation.plan
    relation: shares-deliverable
```

Genuinely new non-EU rows follow the full row shape from chapter `08`. Required fields per new row: as in exercise `04`, plus `pending_instrument_notes` for AIDA / PL 2338 rows and `data_residency_note` where evidence storage location matters (PRC / Korea in particular).

The map header gains `frameworks_pinned.uk-ico-ai-guidance`, `.au-vaiss`, `.ca-aida`, `.ca-quebec-law-25`, `.jp-meti-guidelines`, `.jp-ai-promotion-act`, `.kr-ai-framework-act`, `.kr-pipa`, `.cn-cac-genai-interim-measures`, `.cn-pipl`, `.cn-tc260-003`, `.br-pl-2338`, `.br-lgpd` — each with the version-of-record for those in scope. Not-in-scope jurisdictions do not need a pin.

### 3. `pending-instrument-plan.md`

For AIDA and Brazil PL 2338 (and any other overlay you flag as pending), a short plan for pre-population:

- Which rows the map carries as `pending-instrument`.
- What text-of-record you are drafting against (which bill version, which committee stage).
- The triggering event that will flip the row from `pending-instrument` to `open` (bill enacted, Presidential Decree published, effective-date reached).
- The owner responsible for monitoring the trigger and updating the map.
- Where the draft deliverables will land in the evidence pipeline so they are ready when the trigger fires.

### 4. `gate-preceding-actions.md`

For each in-scope gate-preceding action, a short procedure:

- **EU Article 49 registration** (from anchor map). The pre-release action, the responsible authorised representative, the record.
- **PRC algorithm filing** (if in scope). The filing procedure, the responsible legal partner in PRC, the record.
- **PRC security assessment** (if in scope). The pre-launch security-assessment procedure, the artefact.
- **Korean in-country representative appointment** (if applicable). The appointment procedure, the appointee, the record.

Each action is a row on the map with `gate_dependency: blocking` and `status: covered | pending-external`. The procedure document is the artefact.

### 5. `cross-border-evidence-plan.md`

For each in-scope jurisdiction where the evidence pipeline's storage location matters (particularly PRC, potentially Korea and EU), a short plan:

- Where evidence for the jurisdiction's rows lives (primary store, and any jurisdictional mirror).
- The cross-border transfer mechanism (SCCs for EU, PIPL SCC / security assessment / certification for PRC, cross-border transfer safeguards for Korea).
- The retention alignment across jurisdictions (some regimes have minimum retention floors; some have maximum retention ceilings — the map row's retention must satisfy both).

## Starter guidance

- **Pick your subset honestly.** A system with EU + UK + US-only exposure does not need Korean or Chinese rows. Adding rows you don't actually need clutters the map. But *silence* on a jurisdiction that *does* apply is a defect.
- **Pending-instrument is a real status.** Do not over-claim by marking AIDA rows `covered` before the bill is law. The status keeps the map honest.
- **Shared deliverables are the norm.** Most non-EU risk-management, human-oversight, transparency, record-keeping, and post-market rows share deliverables with the anchor. Author the cross-references; do not duplicate the deliverable.
- **Individual-rights rows are almost always net-new.** UK Article 22 explanation, Quebec Law 25 automated-decision-notice, Korean PIPA automated-decision-refusal, LGPD Article 20 review — these have no EU AI Act analogue. Each gets its own deliverable and legal countersign.
- **Substantive content requirements are jurisdiction-specific.** The PRC content-policy row is not something a shared deliverable satisfies. Note the requirement, name the artefact, name the owner (typically product + legal, sometimes with a jurisdictional partner).
- **Language-of-record for disclosure.** Quebec disclosures must be in French; Korean disclosures in Korean; Chinese disclosures in simplified Chinese. Record a `language` sub-field on the deliverable for the rows where language matters.
- **Cross-border evidence storage is not decorative.** If evidence for PRC rows lives in a US-region S3 bucket, the transfer is a PIPL / DSL / CSL issue. Note the residency plan.
- **Sector-specific non-EU rules are not here.** JFSA for Japanese financial services, FCA / MHRA for UK sectors — those are `mod-107`. This exercise is horizontal non-EU only.
- **Do not fabricate jurisdictional facts.** If you cannot verify an effective date, a sub-clause number, or a regulator's current guidance, mark `<!-- needs-research: … -->`.

## Acceptance criteria

You have succeeded if:

- `non-eu-scoping-decisions.md` addresses all seven jurisdictions — each is either in scope with reasoning or explicitly not-in-scope with reasoning. Every determination has a legal-counsel signoff line and a determination date.
- `non-eu-extended-map.yaml` retains every prior row unchanged in its anchor / NIST / ISO / US fields and adds the non-EU overlay rows. Shared-deliverable overlays are cross-referenced; new rows follow the full schema.
- Every non-EU row is either `covered | partial | open | waived-with-residual | not-applicable | pending-instrument` — no other status. `pending-instrument` rows have `pending_instrument_notes`.
- The map header pins every in-scope non-EU instrument.
- `pending-instrument-plan.md` names, for each pending overlay, the text-of-record, the trigger, the owner, and the pre-populated draft location.
- `gate-preceding-actions.md` names, for each in-scope gate-preceding action, the procedure, the responsible role / representative, and the record artefact. Rows on the map have `gate_dependency: blocking` matched to these actions.
- `cross-border-evidence-plan.md` names, for each in-scope jurisdiction where residency matters, the storage location, the transfer mechanism, and the retention alignment.
- Every language-sensitive deliverable carries a `language` sub-field on its row.
- Every place a jurisdictional fact could not be verified is marked `<!-- needs-research: … -->` rather than guessed.
- A reviewer walking the extended map can see, for any obligation, the full set of jurisdictions that trigger it, which are cross-references, which require new deliverables, and where the programme's residual exposures live per jurisdiction.

## Stretch goals

- **Draft the ICO regulatory-sandbox engagement brief.** If the UK is in scope and your system is novel (particularly on the automated-decision-making side), the ICO's regulatory sandbox is a supervisory-engagement route. In `uk-ico-sandbox-brief.md`, sketch what a sandbox application would say. Cite what the ICO's sandbox call for participation typically asks for.
- **Author the PRC content-policy layer specification.** For an in-scope PRC deployment, the substantive-content-policy layer is not a paper artefact; it is an engineering deliverable. In `cn-content-policy-layer-spec.md`, specify (at a design level) the policy layer's inputs, decision surface, and evaluation.
- **Cross-reference the Hiroshima AI Process Code of Conduct.** If your system is a general-purpose model or a frontier system, the [Hiroshima AI Process Code of Conduct](https://www.mofa.go.jp/ecm/ec/page5e_000076.html) commitments are a Japanese and G7-endorsed voluntary code that regulators and enterprises reference. In `hiroshima-code-adherence.md`, note where your programme's practices align to the eleven principles.
- **Draft the Quebec Law 25 French-language disclosure.** In `qc-law-25-avis-decision-automatisee.fr.md`, produce the disclosure the deployer would present to a Quebec-resident data subject subject to a decision produced exclusively by automated processing. Note the legal-review chain.
- **Add ANPD guidance references.** For Brazil in scope, cross-reference the current ANPD AI-related regulatory documents (regulatory sandbox regulations, generative-AI impact-assessment guidance) on the LGPD and PL 2338 rows. `<!-- needs-research: enumerate current ANPD guidance at authoring time -->`.
- **Author the multi-jurisdictional-notice matrix.** In `multi-jurisdiction-notice-matrix.md`, produce a matrix: for each jurisdiction with a consumer / individual notice obligation (Colorado, LL 144, UK Article 22, Quebec Law 25, Korean PIPA, LGPD Article 20), what is disclosed, in what medium, in what language, and where the shared elements are (versus jurisdiction-specific elements). This is what `mod-105`'s public-audience card variants read from.
