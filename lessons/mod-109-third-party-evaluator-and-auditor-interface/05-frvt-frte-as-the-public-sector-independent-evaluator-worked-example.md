# FRVT / FRTE as the Public-Sector Independent-Evaluator Worked Example

## Motivation

The NIST Face Recognition Vendor Test (FRVT) — running since the year 2000, now continued as the Face Recognition Technology Evaluation (FRTE) — is the closest thing the AI ecosystem has to a *mature*, *decade-scale*, *public-sector*, *independent-evaluator* interface. It has run through multiple generations of algorithms (early feature-based methods, deep-learning-era convolutional networks, transformer-era face-recognition models), across multiple deployment contexts (one-to-one verification, one-to-many identification, morph-attack detection), and it has published demographic-differentials results that reshaped the vendor market. If a release-assurance programme wants a pre-existing worked example of what an AISI-shape evaluator interface will look like *once the AISI shape matures*, FRVT/FRTE is the reference.

The shape lessons are load-bearing. FRVT/FRTE's sealed-evidence submission, its longitudinal comparison across evaluation rounds, its published demographic-differentials, and its versioned vendor identifiers are exactly the pattern the release-assurance programme should expect AISI-shape institutes to converge on as they mature. Where chapter `01` treated the AISI-shape interface as new territory, this chapter reads FRVT/FRTE as *precedent* — the same shape, with two decades of operating experience baked in.

There is also a specific technical lesson. FRVT/FRTE's *sealed-envelope* evidence submission — vendors submit sealed algorithm binaries to NIST; NIST runs the binaries on sealed test data; NIST publishes performance reports — is the strongest published example of a workflow that solves the attack-payload-non-disclosure problem chapter `01` describes for AISI-shape evaluations. The evaluation set does not leak to vendors; the vendor's algorithm details do not leak to NIST beyond what the algorithm's runtime behaviour reveals; and the published report is aggregated at the level where individual test items are not recoverable.

## What FRVT / FRTE is

**Who they are.** FRVT / FRTE is a NIST programme run out of the Image Group in the Information Access Division. Its landing page is [nist.gov/itl/iad/image-group/face-recognition-vendor-test-frvt](https://www.nist.gov/itl/iad/image-group/face-recognition-vendor-test-frvt) <!-- needs-research: verify current NIST URL structure and confirm the FRVT-to-FRTE naming transition -->; ongoing results are published at [pages.nist.gov/frvt/](https://pages.nist.gov/frvt/) <!-- needs-research: verify current results-publishing URL and whether the ongoing-results tracks are still split by verification / identification / morph-attack / etc. -->.

The programme has been running for over two decades and is one of the longest-running independent AI-evaluation programmes in existence. Its methodology — algorithm submission, sealed test data, published demographic-differentials — has been adopted or referenced by biometric-industry procurement processes worldwide.

NIST also runs related programmes of the same shape in adjacent biometric modalities — the Speaker Recognition Evaluation (SRE), the Iris Exchange (IREX), the Fingerprint Vendor Technology Evaluation lineage, and more <!-- needs-research: verify current SRE / IREX / fingerprint programme naming and status -->. Together these programmes constitute a *portfolio* of public-sector biometric evaluations from which the shape lessons in this chapter generalise.

**What they ask for.** A sealed algorithm binary submitted per the NIST API specification for the evaluation track in question (one-to-one verification, one-to-many identification, morph-attack detection, each with its own concept of operations and API shape). Vendors also submit metadata — algorithm identifier, submission date, self-reported operating parameters — that becomes part of the published record.

**Handoff envelope.** A concept-of-operations document describing the evaluation track; the API specification the algorithm binary must implement; a submission portal accepting the sealed binary; a per-vendor identifier under which results are published; and — critically — no leakage of the test dataset to the vendor at any point.

**Release-assurance implication.** FRVT/FRTE is not a template a private enterprise's release-gate directly uses — the workflow is public-sector and biometric-specific. But its shape is a template for how an AISI-shape evaluator interface can be operated at scale, over decades, with strong methodology preservation. This chapter reads out the shape lessons.

## The sealed-envelope evidence submission

The FRVT/FRTE workflow's central methodological control is the *sealed envelope*: neither the vendor nor NIST is exposed to information that would compromise the evaluation's integrity.

- **Vendor to NIST.** The vendor submits a sealed algorithm binary conforming to NIST's API specification. The binary is delivered under an agreement that permits NIST to run it on NIST-controlled infrastructure against NIST-held test data, and to publish aggregate performance metrics tied to the vendor's identifier.
- **NIST to vendor.** NIST does not disclose the composition, provenance, or individual items of the test data. The vendor sees only the *aggregate results* NIST publishes, and (where the API permits) response-level indicators the vendor's algorithm's own runtime produced. The test data itself remains sequestered.
- **NIST-side operation.** NIST runs the vendor's binary against the sequestered test data on NIST-controlled hardware and produces the performance report. The vendor does not participate in the running of the evaluation and does not see raw model outputs on individual test items.

Two properties fall out of this workflow that matter for the release-assurance programme:

- **Contamination is structurally impossible.** Because vendors never see the test data, they cannot train against it — deliberately or otherwise. This solves, at the workflow level, the benchmark-contamination problem that plagues most AI benchmarks in the open web.
- **The vendor cannot dispute individual test items post hoc.** The vendor's disagreement channel is on aggregate metric interpretation, not on individual test-item labelling or curation. This significantly reduces adjudication overhead.

## The reproducibility bundle NIST requires

For a vendor's algorithm to be evaluable and re-evaluable across generations, the submission has to be a *reproducibility bundle* in the sense chapter `03` of `mod-104` uses the term. FRVT/FRTE's version of the bundle includes:

- **The algorithm binary.** The sealed binary conforming to the API specification for the evaluation track.
- **The algorithm identifier.** A vendor-scoped, unique identifier for the submitted algorithm. Vendors typically submit multiple algorithms across a programme's lifetime; each has a distinct identifier so longitudinal comparison is possible.
- **The submission-date metadata.** The date the algorithm was accepted for evaluation.
- **The self-reported operating parameters.** Vendor-declared parameters (feature dimensionality, expected operating latency, hardware requirements) that inform how NIST configures the evaluation run.
- **The vendor's declaration.** A signed declaration that the submitted binary is the same algorithm the vendor markets under the identifier — an integrity attestation that prevents vendors from submitting a "test-optimised" binary and then shipping a different one to customers.

The bundle is what NIST holds. NIST does *not* redistribute the binary; it runs the binary and publishes the results. The vendor retains the binary and controls its downstream release.

## The demographic-differentials report

Beginning with the 2019 FRVT Part 3 report on demographic effects, NIST has published demographic-differentials for face-recognition algorithms — false-match and false-non-match rates broken out by sex, age-group, and racial / regional demographic categories <!-- needs-research: verify current demographic-differentials publication cadence and category definitions -->. The report's shape is the template many AISI-shape institutes are now converging on for their own published outputs:

- **Aggregate performance across the whole test population.** Baseline false-match and false-non-match rates.
- **Per-demographic-slice performance.** The same metrics broken out by demographic slice, with sample-size disclosure per slice.
- **Cross-vendor comparison.** All submitted algorithms ranked on each metric, with each vendor's identifier visible.
- **Longitudinal comparison.** How each vendor's successive algorithm submissions compare over the programme's lifetime.
- **Methodology annex.** The full evaluation protocol, test-set characteristics (to the extent disclosable without compromising sequestration), and computed-statistics definitions.

The report's *published-ness* changes what the assurance case has to survive. A vendor whose FRVT/FRTE demographic-differentials report shows a false-non-match rate on one demographic slice that is 100× higher than on another cannot use the assurance case to hide the number — the number is public and citeable. This mirrors the NYC AEDT dynamic (chapter `03`), but at national-programme scale and with vendor-level cross-comparison.

## Shape lessons for enterprise handoffs to AISI-shape evaluators

Reading FRVT/FRTE as precedent, five shape lessons fall out for the release-assurance programme's AISI-shape interface (chapter `01`) as those interfaces mature:

### Sealed evaluation

**Lesson.** The evaluator holds the test data; the vendor holds the model; neither exchanges what would compromise the other's methodology. FRVT/FRTE has operated this way for two decades and the workflow's integrity is what makes its results defensible against vendor pressure and against academic critique.

**Application.** For AISI-shape engagements, the sealed-evaluation workflow is the target end state. Where the current AISI-shape engagement (chapter `01`) has the evaluator running attack payloads against the vendor's live system, the sealed variant has the vendor submitting a sealed model to the evaluator's infrastructure. This solves the payload-non-disclosure problem at the workflow level rather than at the NDA level.

### Published demographic breakdowns

**Lesson.** The evaluator publishes performance broken out by the axes that matter for the deployment context (demographics, use case, operating conditions). The programme's assurance case has to survive that publication.

**Application.** As AISI-shape institutes mature, expect published capability-elicitation results with vendor-visible cross-comparison on the dangerous-capability axes that matter (autonomous replication task-length, deceptive-alignment behavioural indicators, uplift on dual-use scientific tasks). The `mod-105` external card has to be able to cite the AISI publication as one of its authoritative external references.

### Versioned vendor identifiers

**Lesson.** Each algorithm submission carries a distinct identifier and is comparable to the vendor's other submissions across the programme's lifetime. This lets NIST publish *trajectory* — improvement, regression, plateau — for each vendor.

**Application.** The release-assurance programme's model-digest pinning (`mod-104` chapter `04`) is the analogue at the enterprise level. Extending this to the external AISI-shape interface, the AISI's report should cite the enterprise's model digest (or the enterprise's model-registry identifier) so future AISI reports can be compared to earlier ones. The `mod-104` provenance pipeline already carries the metadata; the AISI interface should be designed to receive it.

### Longitudinal comparison across evaluation rounds

**Lesson.** FRVT/FRTE publishes rolling results, so a vendor's Q1 submission can be compared to their Q2 submission and to their competitors' submissions on the same test set. This produces a *trajectory* view of the industry, not just point-in-time snapshots.

**Application.** For enterprise AISI-shape engagements, the release-assurance programme should design the interface such that successive engagements are comparable — same evaluation harness (or a documented delta), same or overlapping evaluation set (to the extent the AISI's threat model permits), and same reporting shape. Longitudinal comparison is what turns AISI engagements from *point-in-time assurance* into *trajectory assurance*.

### Portfolio across modalities

**Lesson.** NIST does not treat FRVT/FRTE in isolation; it runs a *portfolio* of biometric-recognition evaluations of the same shape across face, voice, iris, and fingerprint. The methodology cross-fertilises across modalities and the vendor community sees the same interface pattern regardless of which modality they submit against.

**Application.** As AISI-shape institutes mature, expect a similar *portfolio* of evaluation tracks — dangerous-capability evaluation, cyber-uplift evaluation, biological-uplift evaluation, deceptive-alignment evaluation, autonomy evaluation — each with its own concept-of-operations and API but with a common submission interface. The release-assurance programme should build its AISI-interface adapter (`mod-104` adapter shape from chapter `02`) as a *general adapter* to that pattern, not as a bespoke integration per institute.

## Worked example — reading a FRVT/FRTE round and adapting the shape for a customer-support-agent AISI handoff

A release-assurance programme wants to design its next AISI-shape engagement (chapter `01`) with FRVT/FRTE's shape lessons applied. The programme is preparing to hand a customer-support-agent frontier deployment to the UK AI Security Institute.

1. **Read the current FRVT/FRTE round.** Programme staff read the most recent FRVT/FRTE ongoing-results publication ([pages.nist.gov/frvt/](https://pages.nist.gov/frvt/)) with attention to the demographic-differentials report's structure — how NIST discloses aggregate performance, per-slice performance, cross-vendor comparison, and longitudinal trajectory. The reading is a *shape study*, not a technical study.
2. **Sealed-evaluation adaptation.** Where the current UK AI Security Institute engagement (chapter `01`) has the Institute running attack payloads against the vendor's live production surface, the programme proposes a *sealed variant*: the vendor submits a sealed model snapshot (digest-pinned, hardware-independent packaging) to the Institute's evaluation infrastructure; the Institute runs its evaluations there. The programme drafts the concept-of-operations document.
3. **Versioned identifier.** The submission carries the model's `mod-104` chapter `04` digest as its identifier. The engagement's return report is pinned to that digest so the report is comparable to any subsequent submission the vendor makes.
4. **Longitudinal design.** The engagement is scoped as *the first of a planned series* rather than as a one-off. The concept-of-operations document names the evaluation set (to the extent the Institute permits), the reporting shape, and the cadence for subsequent rounds. The `mod-104` chapter `06` assurance bundle is extended to carry the round's identifier so the release-gate case can walk the trajectory across rounds.
5. **Published-output preparation.** The programme assumes the Institute will publish at least aggregate findings and prepares the `mod-105` external card to cite the eventual publication URL. The card is drafted such that the Institute's numbers, whatever they turn out to be, will fit the card's structure without contradiction.
6. **Portfolio-adapter design.** The programme designs its AISI-interface adapter as a *general adapter* — the same interface accepts a UK AI Security Institute submission, a US AI Safety Institute submission, or an AI Verify Foundation submission, with per-institute metadata but a shared submission shape. The adapter lives alongside the `mod-104` chapter `02` evidence-pipeline adapters.

The result is an AISI-shape engagement designed at the shape maturity FRVT/FRTE has reached, rather than at the shape immaturity the AISI landscape currently exhibits.

## Where FRVT/FRTE differs from the emerging AISI shape

Two disanalogies are worth calling out so the shape lessons are not over-generalised.

- **Deployment surface.** FRVT/FRTE evaluates *narrow-task* biometric algorithms with a well-defined input-output specification (a pair of images or a probe against a gallery). AISI-shape evaluations target *general-purpose* models and *agentic* systems whose deployment surface is vastly larger and harder to specify. The sealed-envelope workflow adapts; the API specification does not — an AISI equivalent has to be model-family-general and elicitation-methodology-open in a way FRVT's per-track API is not.
- **Evaluation ownership.** FRVT/FRTE is a single-programme, single-institute operation. AISI-shape evaluation is inherently multi-institute — a frontier release may be evaluated by UK AI Security Institute, US AI Safety Institute, METR, and Apollo Research in parallel. The shape lessons apply per institute but the *portfolio adapter* (see below) has to accommodate cross-institute coordination in a way FRVT/FRTE has never needed.

Neither disanalogy invalidates the shape lessons; both refine how the programme applies them. Sealed evaluation, versioned identifiers, longitudinal comparison, and portfolio adapter design remain the right targets; the specific API specifications and cross-institute coordination protocols are open engineering problems the assurance-engineering community is currently working through.

The result is that the enterprise's AISI-shape interface is designed for the maturity level FRVT/FRTE has already reached: successive engagements produce comparable outputs; sealed evaluation removes the payload-leakage risk at the workflow level; a general adapter accommodates multiple institutes without bespoke integration; and the release-gate case reads trajectory across rounds rather than a stack of point-in-time snapshots. None of this requires the AISI-shape institutes to be fully mature — it requires the *provider side* to be ready when they are.

## Why the shape lessons matter now

Two forces make FRVT/FRTE-shape maturity more valuable to study now than at any prior point.

- **AISI-shape institutes are scaling.** UK AI Security Institute, US AI Safety Institute, and their consortium partners have moved from bespoke first-round engagements toward repeatable methodologies with published task suites (`Inspect`), shared benchmark development, and (in some cases) pre-deployment testing agreements with multiple providers. The programme's interface with these institutes will change from *first-time engagement design* to *cross-round engagement adaptation* over the next several years, and the FRVT/FRTE shape lessons are what make cross-round adaptation systematic.
- **GPAI systemic-risk supervision is being built.** The EU AI Office (see `mod-111`) is standing up supervision of Article 55 GPAI systemic-risk providers, and the shape it converges on is likely to draw on the same reference points — sealed evaluation, published aggregate results, versioned model identifiers, longitudinal comparison. The programme that already understands the FRVT/FRTE shape is well positioned to negotiate the Office's interface as it stabilises.

Both forces argue for treating FRVT/FRTE not as a biometric-industry curiosity but as *the* precedent case study for how mature independent-evaluator interfaces are constructed.

## Where this shows up in the rest of the track

- `mod-101` (deferral contract) — the external row for third-party evaluators is where the FRVT/FRTE shape lessons land.
- `mod-102` (assurance case) — longitudinal external-evaluator leaves (comparable across rounds) are a natural extension of the evidence-contract row shape from chapter `06`.
- `mod-103` (release-gate) — trajectory assurance across AISI rounds is a distinct release-gate criterion class from point-in-time assurance.
- `mod-104` (evidence pipeline) — the AISI-interface adapter is a general adapter for AISI-shape submissions; the sealed-evaluation workflow is a variant of the reproducibility-bundle exchange in chapter `03`.
- `mod-105` (cards) — published AISI outputs are card-cited external references.
- `mod-110` (post-market surveillance) — successive AISI rounds are one signal source for the surveillance plan.
- `mod-111` (GPAI systemic-risk) — for Article 55 systemic-risk providers, the FRVT/FRTE shape lessons apply directly to the AI Office's own evaluation regime as it develops.

## Summary

- NIST FRVT (now continued as FRTE) is a two-decade-long public-sector independent-evaluator programme whose sealed-envelope evidence submission, published demographic-differentials, and longitudinal cross-vendor comparison make it the closest available worked example of what AISI-shape evaluation will look like at maturity.
- The workflow's sealed envelope (vendor submits algorithm; NIST holds test data; neither exchanges what would compromise the other's methodology) structurally solves the contamination and payload-non-disclosure problems that AISI-shape evaluations currently address through NDA.
- The reproducibility bundle NIST requires is a sealed binary plus versioned identifier, submission-date metadata, self-reported operating parameters, and a vendor declaration of algorithm identity.
- The demographic-differentials report publishes aggregate performance, per-slice performance, cross-vendor comparison, longitudinal trajectory, and methodology annex — a shape enterprise assurance programmes should expect AISI-shape institutes to converge on.
- Five shape lessons for the enterprise AISI-shape interface: sealed evaluation, published demographic breakdowns, versioned vendor identifiers, longitudinal comparison, portfolio across modalities. Design the AISI-interface adapter as a general adapter to this pattern, not as a bespoke integration per institute.
- NIST also runs the same shape of evaluation across speaker, iris, and fingerprint modalities — the shape lessons generalise beyond face recognition to a portfolio pattern the AISI-shape ecosystem is likely to adopt.
- Exercise `05` has you read the current FRVT/FRTE round and design the next AISI-shape engagement with the five shape lessons applied.
