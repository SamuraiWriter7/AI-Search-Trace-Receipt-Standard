# AI Search Trace Receipt Standard

**AI Search Trace Receipt Standard** defines a privacy-preserving minimum evidence structure for AI-mediated search events.

It is designed to record the trace of an AI search without storing the raw query, raw answer, full browsing history, raw source content, or personal identifiers.

The goal is to make AI search auditable, accountable, and compatible with future attribution, memory, rumination, and royalty systems without turning search history into surveillance infrastructure.

---

## Core Concept

AI search should leave a trace.

But that trace should not become surveillance.

This standard records minimized, encoded, non-reversible signals such as:

* Query fingerprints
* Source fingerprints
* Source interaction signals
* Sampling flags
* Intent codes
* Transformation codes
* Confidence buckets
* Answer digests
* User action signals
* Privacy boundaries
* Integrity hashes

It does not record:

* Raw user queries
* Raw AI answers
* Raw source content
* Full URLs
* Complete browsing history
* Personally linked identifiers
* Exact behavioral timelines
* Sensitive private conversations

The principle is simple:

> Record the trace, not the thought.
> Record the receipt, not the private conversation.
> Record how the source was touched, not the source itself.

---

## Background

AI-mediated search is becoming a primary interface for knowledge access.

Unlike traditional search engines, AI search does not merely return links. It may summarize, transform, compare, synthesize, classify, translate, or verify information before presenting an answer.

This creates a new problem:

> If AI search transforms information and interacts with sources, how can we later verify what happened without recording everything?

This standard answers that question by defining a minimal trace receipt.

Instead of preserving the entire search session, it preserves only the structural evidence needed for later audit, attribution, reflection, or value circulation.

---

## Relationship to Kazene Trace Receipt Protocol

This repository focuses only on AI search trace receipts.

The broader `kazene-trace-receipt-protocol` repository may define general trace receipt concepts across search, generation, memory, agent action, contribution graphs, and royalty hooks.

This standard is intentionally narrower.

```text
Kazene Trace Receipt Protocol
  └─ AI Search Trace Receipt Standard
```

In other words:

* `kazene-trace-receipt-protocol` = general trace receipt framework
* `AI Search Trace Receipt Standard` = search-specific trace receipt standard

This separation keeps the search layer simple, testable, and independently extensible.

---

## Version

Current candidate version:

```text
v0.2.0-candidate
```

Schema version:

```text
0.2.0
```

---

## Version History

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
```

### v0.1: AI Search Trace Receipt

Version 0.1 defines the minimum structure for recording AI-mediated search events.

It focuses on:

* Search trace identity
* Rounded timestamp bucket
* Sampling decision
* Encoding layer
* Query fingerprint
* Search intent code
* Source fingerprints
* Citation count
* Answer digest
* Privacy boundary
* Integrity hash

### v0.2: Source Interaction Trace

Version 0.2 adds **Source Interaction Trace**.

Version 0.1 records that sources were touched.

Version 0.2 records how sources were touched.

It adds minimized source interaction signals such as:

* Source fingerprint
* Interaction type
* Influence level
* Usage mode
* Raw content storage boundary

The goal is to support future audit, attribution, and contribution analysis without storing raw source content, full URLs, full browsing history, or user-identifying access trails.

---

## v0.2 Scope

Version 0.2 defines the minimum structure for recording AI-mediated search events and source interactions.

It covers:

* Search trace identity
* Rounded timestamp bucket
* Sampling decision
* Signal extraction
* Encoding layer
* Query fingerprint
* Search intent code
* Source fingerprints
* Source class codes
* Source interaction trace
* Interaction type codes
* Influence level buckets
* Usage mode codes
* Citation count
* Answer digest
* Confidence bucket
* Transformation code
* User action signal
* Privacy boundary
* Source content storage boundary
* Integrity hash
* Optional future hooks

It does not yet define:

* Generation trace receipts
* Contribution graphs
* Royalty weighting
* Payment hooks
* Full memory integration
* Cross-agent trace propagation
* Unified trace receipts
* Legal attribution decisions
* Copyright compliance decisions

These are reserved for later versions.

---

## Core Flow

```text
AI Search Event
  → Sampling Decision
    → Signal Extraction
      → Encoding Layer
        → Query Fingerprint
          → Source Trace
            → Source Interaction Trace
              → Answer Digest
                → Privacy Boundary
                  → Integrity Hash
                    → Trace Receipt
```

Or, more simply:

```text
Search
  → Sample
    → Extract
      → Encode
        → Fingerprint
          → Record source interaction
            → Digest
              → Minimize
                → Hash
                  → Receipt
```

---

## Encoding Layer

The encoding layer is one of the core ideas of this standard.

In this standard, encoding does not merely mean that data is stored as binary digits inside a computer.

The important step is to convert AI search behavior into a defined code system.

For example:

| Search Behavior    | Encoded Field         |
| ------------------ | --------------------- |
| Search intent      | `intent_code`         |
| Source category    | `source_class_codes`  |
| Source interaction | `interaction_type`    |
| Source influence   | `influence_level`     |
| Source usage role  | `usage_mode`          |
| AI transformation  | `transformation_code` |
| Confidence range   | `confidence_bucket`   |
| User reaction      | `action_code`         |
| Sampling decision  | `sampled`             |
| Privacy status     | `privacy_level`       |
| Retention rule     | `retention_policy`    |

In other words, AI search is not fully recorded.

It is:

```text
sampled
  → classified
    → encoded
      → minimized
        → preserved as a trace receipt
```

This makes the receipt machine-readable without turning it into a private thought archive.

---

## Source Interaction Trace

Source Interaction Trace is the main addition in v0.2.

It records minimized information about how sources were interacted with during an AI search event.

Example:

```yaml
source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false
```

This does not store the source itself.

It only records:

```text
A source fingerprint was touched.
The interaction type was classified.
The influence level was bucketed.
The usage mode was encoded.
Raw source content was not stored.
```

### Interaction Types

Initial `interaction_type` values:

```text
retrieved
cited
summarized
compared
background_reference
validation_reference
counterpoint
ignored_after_retrieval
unknown
```

### Influence Levels

Initial `influence_level` values:

```text
none
low
medium
high
unknown
```

Important boundary:

```text
influence_level is not a royalty weight.
influence_level is not a legal attribution score.
influence_level is only a minimized trace signal.
```

### Usage Modes

Initial `usage_mode` values:

```text
evidence
context
definition
comparison
example
verification
disagreement
inspiration
unknown
```

### Content Storage Boundary

In v0.2, each source interaction must declare:

```yaml
content_stored: false
```

This confirms that raw source content is not stored inside the trace receipt.

---

## Design Principles

### 1. No Raw Query Storage

The raw user query must not be stored inside the receipt.

Only a non-reversible fingerprint, intent code, or minimized signal may be recorded.

### 2. No Raw Answer Storage

The raw AI answer must not be stored inside the receipt.

Only a digest, hash, confidence bucket, or transformation code may be recorded.

### 3. No Raw Source Content Storage

Raw source content must not be stored inside the receipt.

Source Interaction Trace records how a source was touched, not the source itself.

### 4. No Personal ID Linkage

Trace receipts must not be directly linked to personal identifiers.

The standard is designed for structural evidence, not behavioral surveillance.

### 5. Sampling-First Design

Not every search event needs to be recorded.

The receipt includes a sampling section so systems can distinguish between:

* No sampling
* Random sampling
* Risk-based sampling
* Source-based sampling
* User opt-in sampling
* Audit-required sampling

### 6. Structured Encoding

Search events should be converted into defined code fields rather than stored as raw behavioral records.

Examples include:

* `intent_code`
* `source_class_codes`
* `interaction_type`
* `influence_level`
* `usage_mode`
* `transformation_code`
* `confidence_bucket`
* `action_code`
* `privacy_level`
* `retention_policy`

These fields are the practical expression of the encoding layer.

### 7. Privacy Boundary by Default

Every valid receipt must declare its privacy boundary.

The following values are required to be false:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

In v0.2, source interactions also require:

```yaml
content_stored: false
```

These fields define the boundary between a trace receipt and a surveillance log.

### 8. Hash-Based Integrity

Each receipt may include integrity hashes such as:

* `receipt_hash`
* `previous_receipt_hash`
* `signature`

This allows later verification without preserving raw content.

### 9. Optional Future Hooks

Version 0.2 keeps optional hooks for future systems:

* Royalty hook
* Memory hook
* Rumination hook
* Human review requirement

These hooks remain intentionally minimal.

---

## Repository Structure

```text
ai-search-trace-receipt-standard/
├─ README.md
├─ CHANGELOG.md
├─ docs/
│  ├─ ai-search-trace-receipt.md
│  ├─ encoding-model.md
│  ├─ privacy-boundary.md
│  └─ source-interaction-trace.md
├─ schemas/
│  └─ ai-search-trace-receipt.schema.json
├─ examples/
│  └─ ai-search-trace-receipt.example.yaml
├─ scripts/
│  └─ validate_examples.py
└─ .github/
   └─ workflows/
      └─ validate-examples.yml
```

---

## Main Schema

```text
schemas/ai-search-trace-receipt.schema.json
```

The schema defines the minimum valid structure for an AI Search Trace Receipt.

Required top-level fields:

```text
schema_version
trace_id
event_type
timestamp_bucket
sampling
query_trace
source_trace
answer_trace
privacy
integrity
```

Optional top-level fields:

```text
encoding
source_interactions
user_action_trace
hooks
```

---

## Encoded Fields in v0.2

The following fields represent the encoding layer in v0.2:

```text
query_trace.intent_code
source_trace.source_class_codes
source_interactions.interaction_type
source_interactions.influence_level
source_interactions.usage_mode
answer_trace.transformation_code
answer_trace.confidence_bucket
user_action_trace.action_code
sampling.sampled
privacy.privacy_level
privacy.retention_policy
```

These fields convert search and source interaction behavior into a structured, machine-readable format.

They are not intended to reconstruct the private query, full answer, or raw source content.

---

## Example Receipt

```yaml
schema_version: "0.2.0"
trace_id: "trace_20260619_9f3a82"
event_type: "ai_search_trace_receipt"
timestamp_bucket: "2026-06-19T15:00+09:00"

sampling:
  sampled: true
  sampling_method: "risk_based"
  sampling_rate_hint: 0.1

encoding:
  encoding_model: "codebook_based"
  codebook_version: "0.2.0"
  binary_representation: "implicit"
  raw_signal_policy: "not_stored"

query_trace:
  query_fingerprint: "simhash:ab82f91c"
  intent_code: "technical_research"
  sensitivity_bucket: "low"

source_trace:
  source_count: 5
  source_fingerprints:
    - "domain_hash:38fa91"
    - "domain_hash:91cd02"
    - "repo_hash:aa72ef"
  citation_count: 3
  source_class_codes:
    - "documentation"
    - "official"
    - "repository"

source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false

  - source_fingerprint: "repo_hash:aa72ef"
    interaction_type: "background_reference"
    influence_level: "medium"
    usage_mode: "context"
    content_stored: false

  - source_fingerprint: "domain_hash:91cd02"
    interaction_type: "compared"
    influence_level: "low"
    usage_mode: "comparison"
    content_stored: false

answer_trace:
  answer_digest: "sha256:7c9e4f91a2b3c"
  confidence_bucket: "medium"
  transformation_code: "synthesis"

user_action_trace:
  action_code: "refined_query"

privacy:
  raw_query_stored: false
  raw_answer_stored: false
  personal_id_linked: false
  privacy_level: "minimized"
  retention_policy: "short_term"

integrity:
  receipt_hash: "sha256:91bc3a7d9e"
  previous_receipt_hash: "sha256:44af09c81b"

hooks:
  royalty_hook: false
  memory_hook: true
  rumination_hook: false
  human_review_required: false
```

---

## Privacy Boundary

The privacy boundary is one of the most important parts of this standard.

A valid receipt must not become a behavioral surveillance record.

The following fields are required:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

Source interactions require:

```yaml
content_stored: false
```

This means the receipt records only minimized structural evidence.

It does not preserve the user’s private search text, generated answer text, raw source content, or personal identity.

---

## Trace Receipt vs. Surveillance Log

A surveillance log asks:

```text
Who searched what, exactly, when, where, and through which sources?
```

A trace receipt asks:

```text
Did an AI search event occur?
What minimized signals were produced?
Which source classes were touched?
How were sources interacted with?
Which transformation occurred?
Can the receipt be verified later?
```

The first captures behavior.

The second preserves structural evidence.

---

## Source Interaction Trace vs. Contribution Claim

Source Interaction Trace is not the same as a contribution claim.

It does not decide:

* Who should be paid
* How much influence should count
* Whether a source legally contributed to the final answer
* Whether a source should receive attribution
* Whether copyright-relevant use occurred

It only records a minimized signal that may support future review.

```text
Source Interaction Trace
  → may inform future Contribution Graph

Source Interaction Trace
  ≠ Contribution Graph
  ≠ Royalty Weight
  ≠ Legal Attribution
```

---

## Intended Use Cases

This standard may be useful for:

* AI search audit trails
* Attribution systems
* Search quality review
* Privacy-preserving observability
* Source interaction evidence
* Memory and reflection systems
* Royalty or contribution graph foundations
* Human review workflows
* AI governance and accountability layers

---

## Non-Goals

This standard is not intended to be:

* A full search history archive
* A user surveillance system
* A replacement for consent management
* A payment distribution engine
* A full attribution graph
* A model training dataset
* A personal profiling mechanism
* A complete AI governance framework
* A copyright compliance engine
* A legal attribution decision system

---

## Validation

Install dependencies:

```bash
pip install jsonschema pyyaml
```

Run validation:

```bash
python scripts/validate_examples.py
```

Expected result:

```text
[validate] AI Search Trace Receipt
  schema : schemas/ai-search-trace-receipt.schema.json
  example: examples/ai-search-trace-receipt.example.yaml
[ok] AI Search Trace Receipt example is valid
```

---

## GitHub Actions

This repository includes a validation workflow:

```text
.github/workflows/validate-examples.yml
```

The workflow validates example files against their corresponding JSON Schemas on push and pull request.

---

## Future Roadmap

Possible future versions:

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
v0.3: Source / Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

The roadmap may evolve as the standard matures.

---

## Status

This repository is currently a candidate specification.

The v0.2 focus is intentionally narrow:

> AI search should leave a verifiable trace, including how sources were touched, without becoming a record of private thought or raw source capture.

---

## License

License to be determined.

Recommended options may include:

* MIT License
* Apache License 2.0
* Creative Commons Attribution 4.0 for documentation
* A dual structure for schema and documentation

---

## Summary

AI search needs receipts.

Not surveillance logs.

Not full recordings.

Not private thought archives.

Not raw source captures.

This standard defines a minimal way to leave a trace:

```text
Search happened.
Signals were sampled.
Behavior was encoded.
Sources were touched.
Source interactions were classified.
An answer was generated.
The event was minimized.
The receipt can be verified.
The private conversation was not stored.
The raw source content was not stored.
```

That is the purpose of the AI Search Trace Receipt Standard.
