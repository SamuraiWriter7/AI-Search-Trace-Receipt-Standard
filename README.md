# AI Search Trace Receipt Standard

**AI Search Trace Receipt Standard** defines a privacy-preserving minimum evidence structure for AI-mediated search events.

It is designed to record the trace of an AI search without storing the raw query, raw answer, full browsing history, raw source content, or personal identifiers.

The goal is to make AI search auditable, accountable, and compatible with future attribution, memory, rumination, contribution analysis, and royalty systems without turning search history into surveillance infrastructure.

---

## Core Concept

AI search should leave a trace.

But that trace should not become surveillance.

This standard records minimized, encoded, non-reversible signals such as:

* Query fingerprints
* Source fingerprints
* Source interaction signals
* Contribution graph signals
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
* Royalty decisions
* Legal attribution decisions

The principle is simple:

> Record the trace, not the thought.
> Record the receipt, not the private conversation.
> Record how the source was touched, not the source itself.
> Record contribution structure, not ownership or payment.

---

## Background

AI-mediated search is becoming a primary interface for knowledge access.

Unlike traditional search engines, AI search does not merely return links. It may summarize, transform, compare, synthesize, classify, translate, verify, or contextualize information before presenting an answer.

This creates a new problem:

> If AI search transforms information and interacts with sources, how can we later verify what happened without recording everything?

This standard answers that question by defining minimized trace receipts and modular trace structures.

Instead of preserving the entire search session, it preserves only the structural evidence needed for later audit, attribution analysis, reflection, or value circulation.

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
v0.3.0-candidate
```

Current module versions:

```text
AI Search Trace Receipt: 0.2.0
Source Contribution Graph: 0.3.0
```

---

## Version History

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
v0.3: Source Contribution Graph
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

### v0.3: Source Contribution Graph

Version 0.3 adds **Source Contribution Graph** as an independent module.

Version 0.2 records how individual sources were interacted with.

Version 0.3 records how sources relate to answer components, claims, and intermediate summaries through a minimized graph structure.

It adds:

* Graph identity
* Contribution nodes
* Contribution edges
* Relation types
* Contribution signal buckets
* Evidence modes
* Graph policy boundaries
* Graph integrity metadata

The goal is to support contribution analysis without defining royalty payments, legal attribution, ownership claims, or copyright compliance decisions.

---

## Modular Schema Design

Starting with v0.3, larger extension layers are defined as separate schemas.

The main AI Search Trace Receipt schema acts as a receipt envelope.

Specialized structures such as Source Contribution Graph are validated as independent modules.

This keeps the core receipt small, stable, and extensible.

```text
AI Search Trace Receipt Standard
├─ Core receipt schema
│  └─ schemas/ai-search-trace-receipt.schema.json
│
├─ Independent modules
│  └─ schemas/source-contribution-graph.schema.json
│
├─ Examples
│  ├─ examples/ai-search-trace-receipt.example.yaml
│  └─ examples/source-contribution-graph.example.yaml
│
└─ Documentation
   ├─ docs/ai-search-trace-receipt.md
   ├─ docs/encoding-model.md
   ├─ docs/privacy-boundary.md
   ├─ docs/source-interaction-trace.md
   └─ docs/source-contribution-graph.md
```

The design shift is:

```text
v0.1 / v0.2:
  Extend the core receipt with optional fields.

v0.3 and later:
  Define larger structures as independent modules.
```

This prevents the main receipt schema from becoming too large.

The receipt remains the envelope.

The modules become attached structural evidence.

---

## v0.3 Scope

Version 0.3 defines a modular contribution graph for AI-mediated search.

It covers:

* Source contribution graph identity
* Graph type
* Source nodes
* Answer component nodes
* Claim nodes
* Intermediate summary nodes
* Contribution edges
* Relation type codes
* Contribution signal buckets
* Evidence modes
* Graph policy boundaries
* Optional graph integrity metadata

It does not define:

* Royalty distribution
* Payment allocation
* Legal attribution
* Copyright compliance
* Ownership claims
* Full provenance reconstruction
* Model-internal attention graphs
* Training data lineage
* Unified trace receipts

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
              → Source Contribution Graph
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
            → Map contribution structure
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

| Search Behavior       | Encoded Field         |
| --------------------- | --------------------- |
| Search intent         | `intent_code`         |
| Source category       | `source_class_codes`  |
| Source interaction    | `interaction_type`    |
| Source influence      | `influence_level`     |
| Source usage role     | `usage_mode`          |
| Contribution relation | `relation_type`       |
| Contribution signal   | `contribution_signal` |
| Evidence basis        | `evidence_mode`       |
| AI transformation     | `transformation_code` |
| Confidence range      | `confidence_bucket`   |
| User reaction         | `action_code`         |
| Sampling decision     | `sampled`             |
| Privacy status        | `privacy_level`       |
| Retention rule        | `retention_policy`    |

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

## Source Contribution Graph

Source Contribution Graph is the main addition in v0.3.

It records minimized relationships between source fingerprints, claims, summaries, and answer components.

It is defined as an independent module:

```text
schemas/source-contribution-graph.schema.json
```

Example:

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

This records:

```text
Source fingerprint src_1 supported answer component ans_1.
The contribution signal was high.
The evidence basis was citation.
No raw source content, raw query, or raw answer was stored.
No royalty or legal attribution decision was included.
```

### Node Types

Initial `node_type` values:

```text
source
answer_component
intermediate_summary
claim
unknown
```

### Relation Types

Initial `relation_type` values:

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

### Contribution Signals

Initial `contribution_signal` values:

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

### Evidence Modes

Initial `evidence_mode` values:

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

### Graph Policy Boundary

Every valid Source Contribution Graph must declare:

```yaml
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

This keeps the graph as structural evidence rather than content capture, payment logic, or legal judgment.

---

## Design Principles

### 1. No Raw Query Storage

The raw user query must not be stored inside the receipt.

Only a non-reversible fingerprint, intent code, or minimized signal may be recorded.

### 2. No Raw Answer Storage

The raw AI answer must not be stored inside the receipt or contribution graph.

Only a digest, hash, confidence bucket, transformation code, or component digest may be recorded.

### 3. No Raw Source Content Storage

Raw source content must not be stored inside the receipt or graph.

Source Interaction Trace records how a source was touched.

Source Contribution Graph records how a source structurally related to answer components.

Neither records the source itself.

### 4. No Personal ID Linkage

Trace receipts and contribution graphs must not be directly linked to personal identifiers.

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
* `relation_type`
* `contribution_signal`
* `evidence_mode`
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

Source interactions require:

```yaml
content_stored: false
```

Contribution graphs require:

```yaml
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

These fields define the boundary between a trace receipt and a surveillance log.

### 8. Hash-Based Integrity

Each receipt or graph may include integrity hashes such as:

* `receipt_hash`
* `previous_receipt_hash`
* `graph_hash`
* `previous_graph_hash`
* `signature`

This allows later verification without preserving raw content.

### 9. Optional Future Hooks

The standard keeps optional hooks for future systems:

* Royalty hook
* Memory hook
* Rumination hook
* Human review requirement

These hooks remain intentionally minimal until later versions define their semantics.

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
│  ├─ source-interaction-trace.md
│  └─ source-contribution-graph.md
├─ schemas/
│  ├─ ai-search-trace-receipt.schema.json
│  └─ source-contribution-graph.schema.json
├─ examples/
│  ├─ ai-search-trace-receipt.example.yaml
│  └─ source-contribution-graph.example.yaml
├─ scripts/
│  └─ validate_examples.py
└─ .github/
   └─ workflows/
      └─ validate-examples.yml
```

---

## Schemas

### AI Search Trace Receipt Schema

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

### Source Contribution Graph Schema

```text
schemas/source-contribution-graph.schema.json
```

The schema defines a modular graph structure for source contribution analysis.

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

---

## Examples

### AI Search Trace Receipt Example

```text
examples/ai-search-trace-receipt.example.yaml
```

### Source Contribution Graph Example

```text
examples/source-contribution-graph.example.yaml
```

---

## Encoded Fields in v0.3

The following fields represent the encoding layer in v0.3:

```text
query_trace.intent_code
source_trace.source_class_codes
source_interactions.interaction_type
source_interactions.influence_level
source_interactions.usage_mode
contribution_graph.nodes.node_type
contribution_graph.edges.relation_type
contribution_graph.edges.contribution_signal
contribution_graph.edges.evidence_mode
answer_trace.transformation_code
answer_trace.confidence_bucket
user_action_trace.action_code
sampling.sampled
privacy.privacy_level
privacy.retention_policy
```

These fields convert search, source interaction, and contribution behavior into a structured, machine-readable format.

They are not intended to reconstruct the private query, full answer, raw source content, or legal ownership status.

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

Contribution graphs require:

```yaml
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

This means the standard records only minimized structural evidence.

It does not preserve the user’s private search text, generated answer text, raw source content, personal identity, payment decision, or legal attribution decision.

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
Which contribution relationships were mapped?
Which transformation occurred?
Can the receipt or graph be verified later?
```

The first captures behavior.

The second preserves structural evidence.

---

## Source Contribution Graph vs. Royalty Hook

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

This distinction is central to v0.3.

---

## Source Contribution Graph vs. Legal Attribution

Source Contribution Graph does not make legal claims.

It does not decide:

* Authorship
* Copyright status
* Ownership
* Derivative-work status
* Fair use
* Citation sufficiency
* Licensing compliance
* Liability

It only records minimized structural relationships that may support later review.

---

## Intended Use Cases

This standard may be useful for:

* AI search audit trails
* Attribution systems
* Search quality review
* Privacy-preserving observability
* Source interaction evidence
* Contribution structure analysis
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
* A royalty allocation engine

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
[validate] Source Contribution Graph
  schema : schemas/source-contribution-graph.schema.json
  example: examples/source-contribution-graph.example.yaml
[ok] Source Contribution Graph example is valid
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
v0.3: Source Contribution Graph
v0.4: Royalty Hook
v0.5: Unified Trace Receipt
```

The roadmap may evolve as the standard matures.

---

## Status

This repository is currently a candidate specification.

The v0.3 focus is intentionally narrow:

> AI search should leave a verifiable trace, including how sources were touched and how they structurally contributed to answer components, without becoming a record of private thought, raw source capture, payment decision, or legal attribution.

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

Not premature royalty engines.

Not legal attribution machines.

This standard defines a minimal way to leave a trace:

```text
Search happened.
Signals were sampled.
Behavior was encoded.
Sources were touched.
Source interactions were classified.
Contribution relationships were mapped.
An answer was generated.
The event was minimized.
The receipt and graph can be verified.
The private conversation was not stored.
The raw source content was not stored.
Ownership and payment were not decided.
```

That is the purpose of the AI Search Trace Receipt Standard.
