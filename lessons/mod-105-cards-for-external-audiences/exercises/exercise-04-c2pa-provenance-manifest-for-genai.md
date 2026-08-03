# exercise-04: C2PA Provenance Manifest for a GenAI System

**Estimated effort:** 2 hours

## Objective

Author the **`provenance.c2pa` block** of your system card (from exercise `02`) and the underlying C2PA manifest it points at. The exercise fixes the shape of a walkable, signed content-provenance manifest for a specific GenAI-output type, binds it to your system card's head, and forces you to declare a defensible disclosure position against EU AI Act Article 50 sub-obligations and the four disclosure-vs-secrecy tensions chapter `06` enumerates.

## Prerequisites

- Chapter [`06-c2pa-provenance-and-disclosure-tradeoffs.md`](../06-c2pa-provenance-and-disclosure-tradeoffs.md).
- Exercises [`exercise-01`](exercise-01-model-card-for-a-regulated-product.md) and [`exercise-02`](exercise-02-system-card-composition-from-evidence-tree.md) — this exercise attaches to the same system card.
- Skim access to the [C2PA technical specification](https://spec.c2pa.org/) (v2.1 or later; the specification landing page is the required reading, and you should be able to name the manifest / assertion / claim / signature structure on demand).
- Skim access to [EU AI Act Article 50](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) sub-paragraphs 1–4.
- Optional but recommended: install the [C2PA `c2patool`](https://github.com/contentauth/c2patool) locally and try signing a small sample asset before starting the exercise. Not required — you can hand-author the manifest JSON if `c2patool` is unavailable, but the tool makes the hash-binding step concrete.

## Problem statement

Your system card from exercise `02` describes a GenAI-output-producing system. Extend it with the C2PA provenance block chapter `06` fixes, produce a matching underlying C2PA manifest as a signed artefact, and write the reasoning paragraph that the card body carries about the disclosure-vs-secrecy trade-offs the system faces.

You must pick a **primary output type** for the manifest. The choice constrains which C2PA assertions are meaningful and which fallback declarations you write.

### Output-type options

Pick exactly one. If your exercise `02` system produces multiple output types, pick the highest-liability one and note the others as `out-of-scope-for-this-manifest` in the card body.

- **Option A — Image / video.** The system produces still images or short videos (e.g., a marketing-asset generator, a training-material illustration tool, a synthetic-media assistant). C2PA image / video manifests are the most mature and the [Content Credentials](https://contentcredentials.org/) tooling is available.
- **Option B — Audio.** The system produces synthetic speech or music (e.g., a text-to-speech accessibility system, a voice-clone assistant, a music-generation tool). C2PA audio assertions are supported; the [SynthID for audio](https://deepmind.google/technologies/synthid/) work is a complementary watermarking layer worth naming.
- **Option C — Text (documents, articles, code).** The system produces long-form text. C2PA text-assertion adoption is more recent and rougher; you will have to pin the specification version explicitly and cite either the current C2PA text-content-credentials clauses or a `<!-- needs-research: … -->` marker if the clause name changes between spec revisions. Watermarking (e.g., [SynthID for text](https://deepmind.google/discover/blog/watermarking-ai-generated-text-and-video-with-synthid/)) is complementary and should be carried in a separate provenance field.
- **Option D — Structured document (PDF / DOCX / SVG).** The system produces documents that carry both text and embedded imagery. The manifest is chained to the document's byte stream; the assertion set typically combines `c2pa.actions`, `c2pa.training-mining-and-generative-ai-use`, and a document-format-specific assertion.

## Requirements

Produce five artefacts.

### 1. `sample-output.<ext>`

A small sample output of the type you chose (a 512×512 PNG, a 5-second WAV, a 200-word `.txt`, or a two-page PDF — the point is that it is byte-stable and can be hashed). The sample is what the manifest binds to. It is fine for the sample to be a stub — you are not evaluating the sample's *quality*; you are exercising the *manifest binding*.

### 2. `manifest.json`

A C2PA manifest that binds to `sample-output.<ext>`. It must carry:

- `claim_generator` — a producer-tool identifier (e.g., `"example.corp/genai-signer/v1.4"`).
- `claim_generator_info[]` — at least one entry naming the software.
- `assertions[]` — at least four assertions, including:
  - `c2pa.hash.data` (or the format-appropriate hash binding) — the byte-hash binding to `sample-output.<ext>`.
  - `c2pa.actions` — the actions applied to produce the asset (`created`, `edited`, `translated`, etc.).
  - `c2pa.training-mining-and-generative-ai-use` — the training-data-use disclosure category the C2PA vocabulary defines (e.g., `notAllowed`, `allowed`, `constrained`).
  - `c2pa.ai-generated` (or, for non-generative components, `not-ai-generated`) — the AI-generated status assertion.
- `signature` — the manifest is signed. For the exercise you may use a self-signed certificate; declare this explicitly in the card body. The signing key does **not** need to chain to a real root of trust for the exercise, but the manifest must be *verifiable* against the certificate you produce.
- `claim.dc:title`, `claim.dc:format`, and any other Dublin Core fields the tool you use requires.

If you use `c2patool` you can drive it with a small JSON config and reproduce the manifest. If you hand-author the JSON, include a short `verify.sh` (or equivalent) that a reviewer can run to re-verify the signature against the certificate. A `<!-- needs-research: … -->` marker is acceptable where a specific spec clause name has changed between C2PA revisions — do not guess.

### 3. `producer-credential/`

The signing material as a small directory: the certificate (`producer.crt`), any intermediate (`intermediate.crt` if you produce a chain), a `README.md` that documents the credential type, and a `credential-content-address.txt` that records the SHA-256 of the credential material as it would live in the store. Note explicitly whether the certificate chains to a public root, a self-signed root, or a hypothetical Enterprise CA. Do not use a real production key.

### 4. `head-provenance-block.yaml`

The `provenance.c2pa` block for the system card's head. Follow chapter `06`'s shape:

```yaml
provenance:
  c2pa:
    manifest_content_address: "sha256:..."       # the manifest itself, in the store
    manifest_generator: "example.corp/genai-signer/v1.4"
    producer_credential:
      issuer: "..."
      subject: "..."
      credential_content_address: "sha256:..."
    assertions:
      - kind: "c2pa.actions"
        content_address: "sha256:..."
      - kind: "c2pa.training-mining-and-generative-ai-use"
        content_address: "sha256:..."
      - kind: "c2pa.ai-generated"
        content_address: "sha256:..."
    disclosure_position:
      article_50_1: "..."           # narrative rationale
      article_50_2_ai_generated_watermarking: true|false
      article_50_3_deepfake_disclosure: "..."
      article_50_4_public_interest_text: "..."
    verification_endpoint: "https://provenance.example.corp/verify"
    fallback_declaration:
      content_address: "sha256:..."
  watermarking:                                 # OPTIONAL — include if you claim any
    scheme_id: "..."
    scheme_documentation_content_address: "sha256:..."
    detection_endpoint: "..."
  iptc_fallback:                                # OPTIONAL — include for image / video
    digital_source_type: "..."
```

Every content-address must be populated. Placeholders are acceptable but must be marked as placeholders (e.g., `sha256:0000...placeholder`).

### 5. `disclosure-position.md`

A 1–2 page section for the system card body that reasons about each of the four disclosure-vs-secrecy tensions chapter `06` names, applied to your chosen output type and scenario:

- **Article 50 sub-obligations.** For each of Article 50(1) (interaction with natural persons), 50(2) (AI-generated content watermarking), 50(3) (deepfake disclosure), and 50(4) (public-interest text disclosure), name whether your system is in scope and how the C2PA manifest + any fallback discharges the obligation.
- **Content-provenance stripping.** How does your system handle the case where the manifest is removed in transit? Cite the `fallback_declaration` you shipped.
- **Watermarking / IPTC complements.** If you shipped a watermarking scheme or an IPTC-fallback field, argue why. If you did not, name explicitly why they are out of scope (cost / no vendor / not applicable to the output type).
- **Attack-payload disclosure.** If any of your C2PA assertions or the disclosure section reveals information an adversary could weaponise (e.g., naming the watermark scheme too specifically), name what you withheld and why. This is the tension chapter `06`'s decision-rule table §1 covers.

The section must **name what the *public* variant discloses** and note what the regulator, third-party evaluator, and board variants would additionally receive. Exercise `05` operationalises the derivation; here you are only naming the delta position.

## Starter guidance

- **Bind to bytes, not to prose.** A C2PA manifest is nothing if it does not hash-bind to a specific asset byte stream. If your `verify.sh` cannot re-derive the hash and check it against the manifest, the manifest is not walkable.
- **Sign with something reproducible.** The exercise does not test the strength of your PKI setup; it tests that the manifest carries a signature a reviewer can check. A self-signed OpenSSL certificate is fine — declare it as such.
- **Content-address everything.** The manifest, the credential, and each individual assertion all get a SHA-256. Chapter `06`'s block shape has explicit slots for each; do not collapse them into one digest.
- **Say what you *do not* claim.** If your system does not do watermarking, the head block still has room to say so (`watermarking: not-shipped`). Silence looks like an omission.
- **A `<!-- needs-research: … -->` marker is a legitimate answer.** C2PA text-assertion clause names have moved between revisions and the spec continues to evolve. If a clause name changes between the spec version you pin and a later revision, mark it rather than guessing.
- **`c2patool` shortens the loop.** If it is available in your environment, use it to generate the manifest and to verify it. Hand-authoring the JSON is instructive but easy to get subtly wrong; verifying with the tool is what proves the manifest is walkable.
- **Do not use a real production signing key.** For any credential material, generate a fresh keypair for the exercise and destroy it after. If you commit signing material to a repo, keep it under an `exercise-only/` path and mark it clearly.

## Acceptance criteria

You have succeeded if:

- `sample-output.<ext>` is a small, byte-stable asset that the manifest binds to.
- `manifest.json` carries at least the four required assertions, a valid signature (self-signed acceptable, declared as such), and the correct byte-hash binding to `sample-output.<ext>`.
- Running `c2patool verify` (or the equivalent `verify.sh` you shipped) against `sample-output.<ext>` and `manifest.json` succeeds and reports the assertions the manifest claims.
- `producer-credential/` documents the signing chain and cites the `credential_content_address`.
- `head-provenance-block.yaml` conforms to chapter `06`'s shape; every field is populated (placeholders marked); the `disclosure_position` reads to specific Article 50 sub-paragraphs.
- `disclosure-position.md` names the system's position on each of Article 50(1) / (2) / (3) / (4), the fallback for manifest stripping, and the reasoning for whether watermarking / IPTC complements are in scope.
- A peer reviewer can pick the C2PA manifest cited on the card, walk to the credential, verify the signature, walk to each assertion, and cross-check the disclosure position against Article 50 — chapter `06`'s manifest-in-the-store audit walk succeeds end-to-end.
- Every place you were unable to pin a specific spec clause is marked with `<!-- needs-research: … -->` rather than a guessed clause number.

## Stretch goals

- **Chained edit manifests.** Produce a second manifest for a lightly edited version of `sample-output.<ext>` (e.g., a crop of the image, a trimmed WAV, an appended paragraph). The edit manifest chains to the original. Show that a reviewer walking the chain sees both the generative step and the edit step. This is the "manifests are chained" property chapter `06` fixes.
- **Compare against a published Content Credentials asset.** Find a real published image with Content Credentials in the wild (many stock-photo providers now attach them). Read its manifest via the [Content Credentials verify page](https://contentcredentials.org/verify) or with `c2patool`. Diff its shape against yours — what assertions did the vendor ship that you did not? Which of theirs would be inappropriate for your regulatory context?
- **Add a watermarking scheme.** For an image or audio output, adopt a documented watermarking scheme (SynthID descriptions, an open-source scheme like [invisible-watermark](https://github.com/ShieldMnt/invisible-watermark), or a research prototype) and carry both the C2PA block and the `watermarking` block in the head. Argue why the two together defend the disclosure position better than either alone.
- **Draft the deployer-facing UI disclosure.** Chapter `06`'s Article 50 discussion notes that a fallback-textual disclosure often surfaces in the tool UI. Write a two-paragraph disclosure that the deployer would surface to end users when the C2PA manifest is stripped or unavailable, and cite it as `disclosure.ui_copy_content_address` on the head.
- **Cross-reference the C2PA credential chain to the SLSA / Sigstore layer from mod-104.** The C2PA producer credential and the mod-104 chapter `04` Sigstore attestation live under different trust roots and serve different obligations, but a mature program often integrates them. Draft a short `credential-integration.md` that explains how your program would connect the two (e.g., an internal CA that anchors both, an OIDC-bound short-lived Fulcio certificate as the C2PA producer credential, or a decoupled model with named boundaries). Cite the specific sub-obligation each layer discharges.
