# Changelog

All notable changes to this project will be documented in this file.

This project follows a candidate-version style during early specification development.

---

## v0.3.0-candidate

### Summary

Third candidate release of the **AI Search Trace Receipt Standard**.

This version introduces **Source Contribution Graph** as an independent module.

Version 0.1 recorded that an AI search event occurred.

Version 0.2 recorded how individual sources were interacted with.

Version 0.3 records how sources, claims, summaries, and answer components are structurally related through a minimized contribution graph.

The goal is to support auditability, attribution analysis, review workflows, and future value-circulation systems without defining royalty payments, ownership claims, legal attribution, or copyright compliance decisions.

---

### Added

* Added Source Contribution Graph.
* Added `schemas/source-contribution-graph.schema.json`.
* Added `examples/source-contribution-graph.example.yaml`.
* Added `docs/source-contribution-graph.md`.
* Added modular schema design guidance.
* Added independent validation target for Source Contribution Graph.
* Added graph identity fields.
* Added graph node definitions.
* Added graph edge definitions.
* Added contribution relation types.
* Added contribution signal buckets.
* Added evidence mode codes.
* Added graph policy boundaries.
* Added optional graph integrity metadata.
* Added distinction between Source Contribution Graph and Royalty Hook.
* Added distinction between Source Contribution Graph and legal attribution.
* Added distinction between contribution structure and ownership or payment decisions.

---

### Modular Schema Design

Starting with v0.3, larger extension layers are defined as separate schemas.

The main AI Search Trace Receipt schema acts as a receipt envelope.

Specialized structures such as Source Contribution Graph are validated as independent modules.

This keeps the core receipt small, stable, and extensible.

```text
AI Search Trace Receipt Standard
├─ Core receipt schema
│  └─ schemas/ai-search-trace-receipt.schema.json
│
└─ Independent modules
   └─ schemas/source-contribution-graph.schema.json
```

The design shift is:

```text
v0.1 / v0.2:
  Extend the core receipt with optional fields.

v0.3 and later:
  Define larger structures as independent modules.
```

---

### Schema

Added:

```text
schemas/source-contribution-graph.schema.json
```

This schema defines a minimized graph structure for source contribution analysis.

Required top-level fields:

```text
schema_version
graph_id
graph_type
nodes
edges
graph_policy
```

Optional top-level field:

```text
integrity
```

The schema version is:

```text
0.3.0
```

---

### Example

Added:

```text
examples/source-contribution-graph.example.yaml
```

The example demonstrates a valid Source Contribution Graph using:

* Source nodes
* Answer component nodes
* Claim nodes
* Contribution edges
* Relation types
* Contribution signal buckets
* Evidence modes
* Graph policy boundaries
* Optional integrity metadata

Example fragment:

```yaml
schema_version: "0.3.0"
graph_id: "graph_20260620_a13f"
graph_type: "source_to_answer"

nodes:
  - node_id: "src_1"
    node_type: "source"
    source_fingerprint: "domain_hash:38fa91"
    source_class_code: "official"

  - node_id: "ans_1"
    node_type: "answer_component"
    component_type: "synthesis"
    component_digest: "sha256:7c9e4f91a2b3c"

edges:
  - from_node: "src_1"
    to_node: "ans_1"
    relation_type: "supports"
    contribution_signal: "high"
    evidence_mode: "cited"

graph_policy:
  raw_content_stored: false
  raw_query_stored: false
  raw_answer_stored: false
  royalty_decision_included: false
  legal_attribution_included: false
```

---

### Documentation

Added:

```text
docs/source-contribution-graph.md
```

Updated README with:

* v0.3 version status
* Modular Schema Design section
* Source Contribution Graph section
* Updated repository structure
* Updated schema list
* Updated example list
* Updated encoded fields list
* Updated privacy boundary
* Source Contribution Graph vs. Royalty Hook section
* Source Contribution Graph vs. Legal Attribution section
* Updated roadmap

---

### Validation

Updated:

```text
scripts/validate_examples.py
```

Added validation target:

```text
Source Contribution Graph
```

The validation script now checks:

```text
schemas/ai-search-trace-receipt.schema.json
examples/ai-search-trace-receipt.example.yaml

schemas/source-contribution-graph.schema.json
examples/source-contribution-graph.example.yaml
```

Expected output:

```text
[validate] AI Search Trace Receipt
  schema : schemas/ai-search-trace-receipt.schema.json
  example: examples/ai-search-trace-receipt.example.yaml
[ok] AI Search Trace Receipt example is valid
[validate] Source Contribution Graph
  schema : schemas/source-contribution-graph.schema.json
  example: examples/source-contribution-graph.example.yaml
[ok] Source Contribution Graph example is valid
```

---

### Node Types

Added initial `node_type` values:

```text
source
answer_component
intermediate_summary
claim
unknown
```

These values describe the entities represented inside the contribution graph.

---

### Relation Types

Added initial `relation_type` values:

```text
supports
contextualizes
contradicts
defines
compares
summarizes
inspires
verifies
unknown
```

These values describe structural relationships between graph nodes.

---

### Contribution Signals

Added initial `contribution_signal` values:

```text
none
low
medium
high
unknown
```

Important boundary:

```text
contribution_signal is not a royalty weight.
contribution_signal is not a payment score.
contribution_signal is not a legal attribution score.
```

It is only a minimized structural signal.

---

### Evidence Modes

Added initial `evidence_mode` values:

```text
cited
summarized
compared
background_reference
validation_reference
counterpoint
derived_from_interaction
unknown
```

These values describe the evidence basis for a contribution edge.

---

### Graph Policy

Added required graph policy boundaries:

```yaml
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

These fields declare:

```text
The graph does not store raw source content.
The graph does not store raw user queries.
The graph does not store raw AI answers.
The graph does not decide payment.
The graph does not decide legal attribution.
```

---

### Integrity

Added optional graph integrity metadata:

```yaml
integrity:
  graph_hash: "sha256:91bc3a7d9e"
  previous_graph_hash: "sha256:44af09c81b"
```

This may support later graph verification without storing raw content.

---

### Scope

This version focuses on minimized contribution structure for AI-mediated search events.

It records:

* Source nodes
* Answer component nodes
* Claim nodes
* Intermediate summary nodes
* Contribution edges
* Relation types
* Contribution signal buckets
* Evidence modes
* Graph policy boundaries
* Optional graph integrity metadata

It does not record:

* Raw source content
* Full URLs
* Raw user queries
* Raw AI answers
* Complete browsing history
* Personal identifiers
* Exact behavioral timelines
* Payment decisions
* Legal attribution decisions
* Ownership claims

---

### Excluded from v0.3

This version intentionally excludes:

* Royalty distribution
* Payment allocation
* Legal attribution
* Copyright compliance
* Ownership claims
* Full provenance reconstruction
* Model-internal attention graphs
* Training data lineage
* Full URL logging
* Raw content storage
* User-level browsing reconstruction
* Unified trace receipts

---

### Relationship to Earlier Versions

v0.1:

```text
Did an AI search event occur?
```

v0.2:

```text
How was each source touched?
```

v0.3:

```text
How did sources structurally contribute to answer components?
```

---

### Relationship to Future Versions

Source Contribution Graph may inform a future Royalty Hook.

But it is not itself a royalty system.

```text
Source Contribution Graph
  → may inform Royalty Hook

Source Contribution Graph
  ≠ Royalty Hook
  ≠ Payment Rule
  ≠ Legal Attribution
```

Possible future versions:

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
v0.3: Source Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

---

### Core Principle

```text
Record contribution structure.
Do not decide ownership or payment.
```


## v0.2.0-candidate

### Summary

Second candidate release of the **AI Search Trace Receipt Standard**.

This version introduces **Source Interaction Trace**, a minimized layer for recording how sources were interacted with during AI-mediated search.

Version 0.1 recorded that sources were touched.

Version 0.2 records how sources were touched.

The goal is to support auditability, attribution, future contribution analysis, and governance review without storing raw source content, full URLs, full browsing history, or user-identifying access trails.

---

### Added

* Added Source Interaction Trace.
* Added optional `source_interactions` field to the AI Search Trace Receipt schema.
* Added source interaction type codes.
* Added source influence level buckets.
* Added source usage mode codes.
* Added `content_stored: false` boundary for source interactions.
* Added `docs/source-interaction-trace.md`.
* Added v0.2 source interaction example fragments.
* Added source interaction guidance to README.
* Added distinction between Source Interaction Trace and Contribution Graph.
* Added distinction between Source Interaction Trace and royalty weighting.
* Added distinction between source interaction evidence and raw source capture.

---

### Schema

Updated:

```text
schemas/ai-search-trace-receipt.schema.json
```

Changed schema version:

```text
0.1.0 → 0.2.0
```

Added optional top-level field:

```text
source_interactions
```

The field is optional and is not included in the top-level `required` array.

This keeps Source Interaction Trace extensible while preserving compatibility for receipts that do not include interaction-level source details.

---

### New Optional Field

Added:

```yaml
source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false
```

Each source interaction record requires:

```text
source_fingerprint
interaction_type
influence_level
usage_mode
content_stored
```

---

### Source Interaction Types

Added initial `interaction_type` values:

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

These values describe how the AI search process interacted with a source.

---

### Influence Levels

Added initial `influence_level` values:

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
influence_level is not a payment score.
influence_level is not a legal attribution score.
```

It is only a minimized trace signal.

---

### Usage Modes

Added initial `usage_mode` values:

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

These values describe the role a source played in the search result or answer construction process.

---

### Source Content Boundary

Added required source interaction boundary:

```yaml
content_stored: false
```

This confirms that raw source content is not stored inside the trace receipt.

This extends the v0.1 privacy boundary:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

Together, these declare:

```text
The query is not stored.
The answer is not stored.
The personal identity is not linked.
The source content is not stored.
```

---

### Documentation

Added:

```text
docs/source-interaction-trace.md
```

Updated README with:

* v0.2 version status
* Source Interaction Trace overview
* Updated core flow
* Updated repository structure
* Updated example receipt
* Updated encoded fields list
* Updated privacy boundary
* Source Interaction Trace vs. Contribution Claim section
* Future roadmap adjustment

---

### Example

The v0.2 example should include `source_interactions` after `source_trace` and before `answer_trace`.

Example fragment:

```yaml
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
```

---

### Scope

This version focuses on source interaction evidence for AI-mediated search events.

It records:

* That sources were touched
* How sources were interacted with
* Whether they were cited, summarized, compared, or used as background
* Broad source influence level
* Broad usage mode
* Raw source content exclusion

It does not record:

* Raw source content
* Full URLs
* Complete browsing history
* User-identifying access trails
* Exact behavioral timelines
* Private session identifiers

---

### Excluded from v0.2

This version intentionally excludes:

* Raw query storage
* Raw answer storage
* Raw source content storage
* Full URL logging
* Personal ID linkage
* Complete browsing history
* Exact behavioral timeline reconstruction
* Generation trace receipts
* Contribution graph scoring
* Royalty weighting
* Payment hooks
* Legal attribution decisions
* Copyright compliance decisions
* Full memory integration
* Cross-agent trace propagation
* Unified trace receipts

---

### Relationship to v0.1

v0.1:

```text
Which sources were touched?
How many sources were involved?
Were citations present?
```

v0.2:

```text
How was each source used?
How strongly did it influence the answer?
Was it cited, summarized, compared, or only used as background?
Was raw source content excluded?
```

---

### Relationship to Future Versions

Source Interaction Trace may inform future contribution or attribution systems, but it does not define them.

```text
Source Interaction Trace
  → may inform future Contribution Graph

Source Interaction Trace
  ≠ Contribution Graph
  ≠ Royalty Weight
  ≠ Legal Attribution
```

Possible future versions:

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
v0.3: Source / Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

---

### Core Principle

```text
Record how the source was touched.
Do not record the source itself.
```

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
v0.2: Source Interaction Trace
v0.3: Source / Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

Roadmap items may change as the specification evolves.
