# Changelog

All notable changes to this project will be documented in this file.

This project follows a candidate-version style during early specification development.

---

## v0.1.0-candidate

### Summary

Initial candidate release of the **AI Search Trace Receipt Standard**.

This version defines a privacy-preserving minimum evidence structure for AI-mediated search events.

The purpose of this release is to establish a search-specific trace receipt format that can support future audit, attribution, memory, rumination, and royalty systems without storing raw search history or personal identifiers.

---

### Added

* Added initial project README.
* Added AI Search Trace Receipt JSON Schema.
* Added example YAML receipt.
* Added privacy boundary documentation.
* Added search-specific trace receipt overview.
* Added validation script for schema-example consistency.
* Added GitHub Actions workflow for example validation.
* Added candidate release status.
* Added relationship note to the broader `kazene-trace-receipt-protocol` repository.

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
* Query fingerprint
* Technical research intent code
* Source fingerprints
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
docs/privacy-boundary.md
```

The documentation explains:

* The purpose of AI Search Trace Receipts
* What the standard records
* What the standard must not record
* The distinction between trace receipts and surveillance logs
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
```

---

### Candidate Status

This release is a candidate specification.

It is suitable for:

* Early review
* Schema validation
* Example testing
* Documentation refinement
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
