# AI Search Trace Receipt Standard

**AI Search Trace Receipt Standard** defines a privacy-preserving minimum evidence structure for AI-mediated search events.

It is designed to record the trace of an AI search without storing the raw query, raw answer, full browsing history, or personal identifiers.

The goal is to make AI search auditable, accountable, and compatible with future attribution, memory, rumination, and royalty systems without turning search history into surveillance infrastructure.

---

## Core Concept

AI search should leave a trace.

But that trace should not become surveillance.

This standard records minimized, encoded, non-reversible signals such as:

* Query fingerprints
* Source fingerprints
* Sampling flags
* Answer digests
* User action signals
* Privacy boundaries
* Integrity hashes

It does not record:

* Raw user queries
* Raw AI answers
* Complete browsing history
* Personally linked identifiers
* Exact behavioral timelines

The principle is simple:

> Record the trace, not the thought.
> Record the receipt, not the private conversation.

---

## Background

AI-mediated search is becoming a primary interface for knowledge access.

Unlike traditional search engines, AI search does not merely return links. It may summarize, transform, compare, synthesize, classify, or translate information before presenting an answer.

This creates a new problem:

> If AI search transforms information, how can we later verify what happened without recording everything?

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
v0.1.0-candidate
```

Schema version:

```text
0.1.0
```

---

## v0.1 Scope

Version 0.1 defines the minimum structure for recording AI-mediated search events.

It covers:

* Search trace identity
* Rounded timestamp bucket
* Sampling decision
* Query fingerprint
* Search intent code
* Source fingerprints
* Citation count
* Answer digest
* Confidence bucket
* Transformation code
* User action signal
* Privacy boundary
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

These are reserved for later versions.

---

## Core Flow

```text
AI Search Event
  → Sampling Decision
    → Query Fingerprint
      → Source Fingerprints
        → Answer Digest
          → Privacy Boundary
            → Integrity Hash
              → Trace Receipt
```

Or, more simply:

```text
Search
  → Sample
    → Fingerprint
      → Digest
        → Minimize
          → Hash
            → Receipt
```

---

## Design Principles

### 1. No Raw Query Storage

The raw user query must not be stored inside the receipt.

Only a non-reversible fingerprint, intent code, or minimized signal may be recorded.

### 2. No Raw Answer Storage

The raw AI answer must not be stored inside the receipt.

Only a digest, hash, confidence bucket, or transformation code may be recorded.

### 3. No Personal ID Linkage

Trace receipts must not be directly linked to personal identifiers.

The standard is designed for structural evidence, not behavioral surveillance.

### 4. Sampling-First Design

Not every search event needs to be recorded.

The receipt includes a sampling section so systems can distinguish between:

* No sampling
* Random sampling
* Risk-based sampling
* Source-based sampling
* User opt-in sampling
* Audit-required sampling

### 5. Privacy Boundary by Default

Every valid receipt must declare its privacy boundary.

The following values are required to be false:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

These fields define the boundary between a trace receipt and a surveillance log.

### 6. Hash-Based Integrity

Each receipt may include integrity hashes such as:

* `receipt_hash`
* `previous_receipt_hash`
* `signature`

This allows later verification without preserving raw content.

### 7. Optional Future Hooks

Version 0.1 includes optional hooks for future systems:

* Royalty hook
* Memory hook
* Rumination hook
* Human review requirement

These hooks are intentionally minimal in v0.1.

---

## Repository Structure

```text
ai-search-trace-receipt-standard/
├─ README.md
├─ CHANGELOG.md
├─ docs/
│  ├─ ai-search-trace-receipt.md
│  └─ privacy-boundary.md
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
user_action_trace
hooks
```

---

## Example Receipt

```yaml
schema_version: "0.1.0"
trace_id: "trace_20260619_9f3a82"
event_type: "ai_search_trace_receipt"
timestamp_bucket: "2026-06-19T15:00+09:00"

sampling:
  sampled: true
  sampling_method: "risk_based"
  sampling_rate_hint: 0.1

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

The privacy boundary is the most important part of this standard.

A valid receipt must not become a behavioral surveillance record.

The following fields are required:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

This means the receipt records only minimized structural evidence.

It does not preserve the user’s private search text, generated answer text, or personal identity.

---

## Trace Receipt vs. Surveillance Log

A surveillance log asks:

```text
Who searched what, exactly, when, and where?
```

A trace receipt asks:

```text
Did an AI search event occur,
what minimized signals were produced,
which source classes were touched,
and can the receipt be verified later?
```

The first captures behavior.

The second preserves structural evidence.

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
v0.2: Generation Trace Receipt
v0.3: Source / Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

The roadmap may evolve as the standard matures.

---

## Status

This repository is currently a candidate specification.

The v0.1 focus is intentionally narrow:

> AI search should leave a verifiable trace without becoming a record of private thought.

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

This standard defines a minimal way to leave a trace:

```text
Search happened.
Sources were touched.
An answer was generated.
The event was minimized.
The receipt can be verified.
The private conversation was not stored.
```

That is the purpose of the AI Search Trace Receipt Standard.
