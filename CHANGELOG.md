# Changelog

All notable changes to this project will be documented in this file.

This project follows a candidate-version style during early specification development.

---

## v0.1.0-candidate

### Summary

Initial candidate release of the **AI Search Trace Receipt Standard**.

This version defines a privacy-preserving minimum evidence structure for AI-mediated search events.

The purpose of this release is to establish a search-specific trace receipt format that can support future audit, attribution, memory, rumination, and royalty systems without storing raw search history or personal identifiers.

This release also introduces the initial **Encoding Layer**, which converts AI search behavior into structured code fields instead of preserving raw behavioral records.

---

### Added

* Added initial project README.
* Added AI Search Trace Receipt JSON Schema.
* Added example YAML receipt.
* Added privacy boundary documentation.
* Added search-specific trace receipt overview.
* Added encoding layer concept.
* Added encoding model documentation entry.
* Added structured encoding fields for search behavior.
* Added validation script for schema-example consistency.
* Added GitHub Actions workflow for example validation.
* Added candidate release status.
* Added relationship note to the broader `kazene-trace-receipt-protocol` repository.

---

### Encoding Layer

Added the initial Encoding Layer for AI search trace receipts.

The Encoding Layer defines how AI search behavior is converted into structured, machine-readable fields without storing the raw query, raw answer, or full search session.

In this standard, encoding does not merely mean storing data as binary digits.

It means mapping search behavior into defined code fields such as:

```text
query_trace.intent_code
source_trace.source_class_codes
answer_trace.transformation_code
answer_trace.confidence_bucket
user_action_trace.action_code
sampling.sampled
privacy.privacy_level
privacy.retention_policy
```

This allows the receipt to preserve structural evidence while avoiding private thought capture.

Conceptual flow:

```text
Search behavior
  → Sampled signal
    → Classified event
      → Encoded field
        → Minimized receipt
```

---

### Encoding Model

Added an initial encoding model for v0.1.

The v0.1 encoding model may be represented by an optional `encoding` object in example receipts:

```yaml
encoding:
  encoding_model: "codebook_based"
  codebook_version: "0.1.0"
  binary_representation: "implicit"
  raw_signal_policy: "not_stored"
```

This field clarifies that the trace receipt uses a defined codebook-style model rather than raw recording.

The initial encoding model supports:

* Codebook-based classification
* Implicit binary representation
* Raw signal non-storage
* Machine-readable trace fields
* Privacy-preserving event minimization

---

### Schema

Added:

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
encoding
hooks
```

---

### Example

Added:

```text
examples/ai-search-trace-receipt.example.yaml
```

The example demonstrates a valid AI search trace receipt using:

* Risk-based sampling
* Encoding model declaration
* Query fingerprint
* Technical research intent code
* Source fingerprints
* Source class codes
* Citation count
* Answer digest
* Confidence bucket
* Transformation code
* User action signal
* Privacy boundary
* Integrity hash
* Optional future hooks

---

### Documentation

Added:

```text
docs/ai-search-trace-receipt.md
docs/encoding-model.md
docs/privacy-boundary.md
```

The documentation explains:

* The purpose of AI Search Trace Receipts
* What the standard records
* What the standard must not record
* The distinction between trace receipts and surveillance logs
* The encoding layer
* The encoding model
* The privacy boundary
* Timestamp bucket guidance
* Query fingerprint guidance
* Source fingerprint guidance
* Retention policy guidance

---

### Validation

Added:

```text
scripts/validate_examples.py
```

The validation script checks the example YAML file against the JSON Schema.

Expected validation output:

```text
[validate] AI Search Trace Receipt
  schema : schemas/ai-search-trace-receipt.schema.json
  example: examples/ai-search-trace-receipt.example.yaml
[ok] AI Search Trace Receipt example is valid
```

---

### GitHub Actions

Added:

```text
.github/workflows/validate-examples.yml
```

The workflow runs validation on:

* Push
* Pull request

It installs:

```text
jsonschema
pyyaml
```

Then runs:

```bash
python scripts/validate_examples.py
```

---

### Scope

This version focuses only on AI-mediated search events.

It defines:

* Search trace identity
* Rounded timestamp bucket
* Sampling decision
* Signal extraction
* Encoding layer
* Query fingerprint
* Search intent code
* Source fingerprints
* Source class codes
* Citation count
* Answer digest
* Confidence bucket
* Transformation code
* User action signal
* Privacy boundary
* Integrity hash
* Optional future hooks

---

### Privacy Constraints

This version requires valid receipts to declare:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

These fields define the boundary between a trace receipt and a surveillance log.

---

### Excluded from v0.1

This version intentionally excludes:

* Raw query storage
* Raw answer storage
* Personal ID linkage
* Complete browsing history
* Exact behavioral timeline reconstruction
* Raw behavioral recording
* Generation trace receipts
* Contribution graph logic
* Royalty weighting
* Payment hooks
* Full memory integration
* Cross-agent trace propagation
* Unified trace receipts

---

### Relationship

This repository is a search-specific standard.

The broader `kazene-trace-receipt-protocol` repository may serve as the parent protocol layer for general trace receipt concepts.

```text
Kazene Trace Receipt Protocol
  └─ AI Search Trace Receipt Standard
```

---

### Core Principle

```text
Record the trace, not the thought.
Record the receipt, not the private conversation.
Encode the behavior, not the private mind.
```

---

### Candidate Status

This release is a candidate specification.

It is suitable for:

* Early review
* Schema validation
* Example testing
* Documentation refinement
* Encoding model refinement
* Future extension planning

It should not yet be treated as a finalized standard.

---

### Future Roadmap

Possible future versions:

```text
v0.1: AI Search Trace Receipt
v0.2: Generation Trace Receipt
v0.3: Source / Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

Roadmap items may change as the specification evolves.
