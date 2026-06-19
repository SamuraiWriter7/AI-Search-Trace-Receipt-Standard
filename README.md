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
* Royalty hook signals
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
* Payment decisions
* Legal attribution decisions
* Ownership assignments

The principle is simple:

> Record the trace, not the thought.
> Record the receipt, not the private conversation.
> Record how the source was touched, not the source itself.
> Record contribution structure, not ownership or payment.
> Connect to value circulation, but do not calculate royalties.

---

## Background

AI-mediated search is becoming a primary interface for knowledge access.

Unlike traditional search engines, AI search does not merely return links. It may summarize, transform, compare, synthesize, classify, translate, verify, or contextualize information before presenting an answer.

This creates a new problem:

> If AI search transforms information and interacts with sources, how can we later verify what happened without recording everything?

This standard answers that question by defining minimized trace receipts and modular trace structures.

Instead of preserving the entire search session, it preserves only the structural evidence needed for later audit, attribution analysis, reflection, contribution review, or value circulation.

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
v0.4.0-candidate
```

Current module versions:

```text
AI Search Trace Receipt: 0.2.0
Source Contribution Graph: 0.3.0
Royalty Hook: 0.4.0
```

---

## Version History

```text
v0.1: AI Search Trace Receipt
v0.2: Source Interaction Trace
v0.3: Source Contribution Graph
v0.4: Royalty Hook
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

### v0.4: Royalty Hook

Version 0.4 adds **Royalty Hook** as an independent module.

Version 0.3 records contribution structure.

Version 0.4 records how a Source Contribution Graph may be safely passed to downstream value-circulation, attribution review, royalty analysis, or governance audit systems.

It adds:

* Hook identity
* Source graph reference
* Eligibility signals
* Review requirement
* Allowed downstream use
* Prohibited downstream use
* Policy boundary
* Hook integrity metadata

The goal is to support controlled value-circulation review without calculating royalties, deciding payment, assigning ownership, or determining legal attribution.

---

## Modular Schema Design

Starting with v0.3, larger extension layers are defined as separate schemas.

The main AI Search Trace Receipt schema acts as a receipt envelope.

Specialized structures such as Source Contribution Graph and Royalty Hook are validated as independent modules.

This keeps the core receipt small, stable, and extensible.

```text
AI Search Trace Receipt Standard
├─ Core receipt schema
│  └─ schemas/ai-search-trace-receipt.schema.json
│
├─ Independent modules
│  ├─ schemas/source-contribution-graph.schema.json
│  └─ schemas/royalty-hook.schema.json
│
├─ Examples
│  ├─ examples/ai-search-trace-receipt.example.yaml
│  ├─ examples/source-contribution-graph.example.yaml
│  └─ examples/royalty-hook.example.yaml
│
└─ Documentation
   ├─ docs/ai-search-trace-receipt.md
   ├─ docs/encoding-model.md
   ├─ docs/privacy-boundary.md
   ├─ docs/source-interaction-trace.md
   ├─ docs/source-contribution-graph.md
   └─ docs/royalty-hook.md
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

The modules become attached structural evidence and controlled connection layers.

---

## v0.4 Scope

Version 0.4 defines a Royalty Hook for AI-mediated search contribution structures.

It covers:

* Royalty hook identity
* Hook type
* Source Contribution Graph reference
* Eligibility for review
* Eligibility for royalty analysis
* Eligibility for public attribution review
* Confidence level
* Human review requirement
* Review reason
* Review status
* Allowed downstream use
* Prohibited downstream use
* Policy boundary
* Optional hook integrity metadata

It does not define:

* Royalty distribution
* Payment allocation
* Automatic payment
* Legal attribution
* Copyright compliance
* Ownership claims
* Contract execution
* Creator identity resolution
* Payout identity mapping
* Full provenance reconstruction
* Model-internal attention graphs
* Training data lineage
* Unified trace receipts

These are reserved for later versions or downstream systems.

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
                → Royalty Hook
                  → Human Review / Policy Engine / Royalty Analysis
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
              → Connect to value-circulation review
                → Preserve boundaries
                  → Verify
```

---

## Encoding Layer

The encoding layer is one of the core ideas of this standard.

In this standard, encoding does not merely mean that data is stored as binary digits inside a computer.

The important step is to convert AI search behavior into a defined code system.

For example:

| Search Behavior           | Encoded Field               |
| ------------------------- | --------------------------- |
| Search intent             | `intent_code`               |
| Source category           | `source_class_codes`        |
| Source interaction        | `interaction_type`          |
| Source influence          | `influence_level`           |
| Source usage role         | `usage_mode`                |
| Contribution relation     | `relation_type`             |
| Contribution signal       | `contribution_signal`       |
| Evidence basis            | `evidence_mode`             |
| Downstream use category   | `allowed_downstream_use`    |
| Prohibited downstream use | `prohibited_downstream_use` |
| Review status             | `review_status`             |
| AI transformation         | `transformation_code`       |
| Confidence range          | `confidence_bucket`         |
| User reaction             | `action_code`               |
| Sampling decision         | `sampled`                   |
| Privacy status            | `privacy_level`             |
| Retention rule            | `retention_policy`          |

In other words, AI search is not fully recorded.

It is:

```text
sampled
  → classified
    → encoded
      → minimized
        → preserved as trace evidence
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

## Royalty Hook

Royalty Hook is the main addition in v0.4.

It records how a Source Contribution Graph may be safely passed to downstream value-circulation or review systems.

It is defined as an independent module:

```text
schemas/royalty-hook.schema.json
```

Royalty Hook is not a royalty engine.

It does not calculate royalties.

It does not decide payment.

It does not assign ownership.

It does not determine legal attribution.

It only records safe connection conditions.

Example:

```yaml
schema_version: "0.4.0"
hook_id: "royalty_hook_20260620_a13f"
hook_type: "contribution_graph_bridge"

source_graph_ref:
  graph_id: "graph_20260620_a13f"
  graph_hash: "sha256:91bc3a7d9e"
  graph_schema_version: "0.3.0"

eligibility:
  eligible_for_review: true
  eligible_for_royalty_system: true
  eligible_for_public_attribution: false
  confidence_level: "medium"

review:
  human_review_required: true
  review_reason: "contribution_signal_present"
  review_status: "pending"

allowed_downstream_use:
  - "attribution_review"
  - "royalty_analysis"
  - "governance_audit"

prohibited_downstream_use:
  - "automatic_payment"
  - "legal_attribution_decision"
  - "ownership_assignment"
  - "automated_contract_execution"
  - "identity_resolution"
  - "raw_content_reconstruction"
  - "user_profiling"

policy_boundary:
  payment_decision_included: false
  legal_attribution_included: false
  ownership_decision_included: false
  automatic_execution_allowed: false
  human_review_required_before_payment: true
  raw_content_stored: false
  raw_query_stored: false
  raw_answer_stored: false

integrity:
  hook_hash: "sha256:7bd91ac44f"
  source_graph_hash: "sha256:91bc3a7d9e"
  previous_hook_hash: "sha256:3fa12bc980"
```

This records:

```text
A Source Contribution Graph is referenced.
The graph may be passed to royalty analysis.
Human review is required.
Automatic payment is prohibited.
Legal attribution decisions are prohibited.
Ownership assignment is prohibited.
Raw content reconstruction is prohibited.
```

### Hook Types

Initial `hook_type` values:

```text
contribution_graph_bridge
attribution_review_bridge
royalty_analysis_bridge
governance_audit_bridge
mixed
unknown
```

### Eligibility Signals

Royalty Hook records eligibility for:

```text
review
royalty analysis
public attribution review
```

Important boundaries:

```text
eligible_for_royalty_system does not authorize payment.
eligible_for_public_attribution does not decide public attribution.
confidence_level is not a payment confidence score.
```

### Review Status

Initial `review_status` values:

```text
pending
in_review
approved_for_analysis
rejected
archived
unknown
```

Important boundary:

```text
approved_for_analysis is not approval for payment.
approved_for_analysis is not legal attribution.
approved_for_analysis is not ownership assignment.
```

### Allowed Downstream Use

Initial `allowed_downstream_use` values:

```text
attribution_review
royalty_analysis
governance_audit
provenance_review
public_attribution_review
memory_review
unknown
```

These categories allow review or analysis.

They do not allow automatic execution.

### Prohibited Downstream Use

Initial `prohibited_downstream_use` values:

```text
automatic_payment
legal_attribution_decision
ownership_assignment
automated_contract_execution
identity_resolution
raw_content_reconstruction
user_profiling
unknown
```

This field is central to the safety boundary of v0.4.

### Policy Boundary

Every valid Royalty Hook must declare:

```yaml
payment_decision_included: false
legal_attribution_included: false
ownership_decision_included: false
automatic_execution_allowed: false
human_review_required_before_payment: true
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
```

This keeps the hook as a safe connection layer rather than a payment engine, legal attribution system, or ownership assignment mechanism.

---

## Design Principles

### 1. No Raw Query Storage

The raw user query must not be stored inside the receipt, contribution graph, or royalty hook.

Only a non-reversible fingerprint, intent code, or minimized signal may be recorded.

### 2. No Raw Answer Storage

The raw AI answer must not be stored inside the receipt, contribution graph, or royalty hook.

Only a digest, hash, confidence bucket, transformation code, or component digest may be recorded.

### 3. No Raw Source Content Storage

Raw source content must not be stored inside the receipt, graph, or hook.

Source Interaction Trace records how a source was touched.

Source Contribution Graph records how a source structurally related to answer components.

Royalty Hook records how that graph may be passed downstream.

None of them records the source itself.

### 4. No Personal ID Linkage

Trace receipts, contribution graphs, and royalty hooks must not be directly linked to personal identifiers.

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
* `allowed_downstream_use`
* `prohibited_downstream_use`
* `review_status`
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

Royalty hooks require:

```yaml
payment_decision_included: false
legal_attribution_included: false
ownership_decision_included: false
automatic_execution_allowed: false
human_review_required_before_payment: true
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
```

These fields define the boundary between a trace system and surveillance, payment automation, or legal judgment.

### 8. Hash-Based Integrity

Each receipt, graph, or hook may include integrity hashes such as:

* `receipt_hash`
* `previous_receipt_hash`
* `graph_hash`
* `previous_graph_hash`
* `hook_hash`
* `previous_hook_hash`
* `signature`

This allows later verification without preserving raw content.

### 9. Human Review Before Payment

Royalty Hook requires that payment-related action must not be automatic.

The following boundary must hold:

```yaml
automatic_execution_allowed: false
human_review_required_before_payment: true
```

This means downstream systems may analyze contribution evidence, but payment requires a separate review process.

### 10. Optional Future Hooks

The standard keeps optional hooks for future systems:

* Royalty hook
* Memory hook
* Rumination hook
* Human review requirement

These hooks remain intentionally bounded until later versions define their full semantics.

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
│  ├─ source-contribution-graph.md
│  └─ royalty-hook.md
├─ schemas/
│  ├─ ai-search-trace-receipt.schema.json
│  ├─ source-contribution-graph.schema.json
│  └─ royalty-hook.schema.json
├─ examples/
│  ├─ ai-search-trace-receipt.example.yaml
│  ├─ source-contribution-graph.example.yaml
│  └─ royalty-hook.example.yaml
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

### Royalty Hook Schema

```text
schemas/royalty-hook.schema.json
```

The schema defines a safety-bounded hook for passing contribution graph references to downstream value-circulation, attribution review, royalty analysis, or governance audit systems.

Required top-level fields:

```text
schema_version
hook_id
hook_type
source_graph_ref
eligibility
review
allowed_downstream_use
prohibited_downstream_use
policy_boundary
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

### Royalty Hook Example

```text
examples/royalty-hook.example.yaml
```

---

## Encoded Fields in v0.4

The following fields represent the encoding layer in v0.4:

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
royalty_hook.hook_type
royalty_hook.eligibility.confidence_level
royalty_hook.review.review_reason
royalty_hook.review.review_status
royalty_hook.allowed_downstream_use
royalty_hook.prohibited_downstream_use
answer_trace.transformation_code
answer_trace.confidence_bucket
user_action_trace.action_code
sampling.sampled
privacy.privacy_level
privacy.retention_policy
```

These fields convert search, source interaction, contribution behavior, and downstream connection conditions into a structured, machine-readable format.

They are not intended to reconstruct the private query, full answer, raw source content, payment decision, legal attribution, or ownership status.

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

Royalty hooks require:

```yaml
payment_decision_included: false
legal_attribution_included: false
ownership_decision_included: false
automatic_execution_allowed: false
human_review_required_before_payment: true
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
```

This means the standard records only minimized structural evidence and controlled connection conditions.

It does not preserve the user’s private search text, generated answer text, raw source content, personal identity, payment decision, legal attribution decision, or ownership decision.

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
Which downstream review hooks were allowed or prohibited?
Which transformation occurred?
Can the receipt, graph, or hook be verified later?
```

The first captures behavior.

The second preserves structural evidence.

---

## Source Contribution Graph vs. Royalty Hook

Source Contribution Graph records contribution structure.

Royalty Hook records how that structure may be passed downstream.

```text
Source Contribution Graph:
  Source A supported Answer Component X.

Royalty Hook:
  This contribution graph may be reviewed for royalty analysis,
  but it must not trigger automatic payment.
```

The graph maps structure.

The hook controls downstream use.

---

## Royalty Hook vs. Royalty Engine

Royalty Hook is not a royalty engine.

```text
Royalty Hook
  → may pass evidence to royalty analysis

Royalty Hook
  ≠ royalty calculator
  ≠ payment allocator
  ≠ distribution engine
  ≠ legal entitlement system
```

This distinction is central to v0.4.

---

## Royalty Hook vs. Legal Attribution

Royalty Hook does not make legal claims.

It does not decide:

* Authorship
* Copyright status
* Ownership
* Derivative-work status
* Fair use
* Citation sufficiency
* Licensing compliance
* Liability
* Public attribution requirement

It only records safe connection conditions for downstream review.

---

## Intended Use Cases

This standard may be useful for:

* AI search audit trails
* Attribution systems
* Search quality review
* Privacy-preserving observability
* Source interaction evidence
* Contribution structure analysis
* Royalty analysis preparation
* Value-circulation review
* Memory and reflection systems
* Human review workflows
* AI governance and accountability layers

---

## Non-Goals

This standard is not intended to be:

* A full search history archive
* A user surveillance system
* A replacement for consent management
* A payment distribution engine
* A royalty calculator
* A legal attribution engine
* A copyright compliance engine
* A model training dataset
* A personal profiling mechanism
* A full attribution graph
* A complete AI governance framework
* A payout identity mapping system
* An automated contract execution system

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
[validate] Royalty Hook
  schema : schemas/royalty-hook.schema.json
  example: examples/royalty-hook.example.yaml
[ok] Royalty Hook example is valid
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

The v0.4 focus is intentionally narrow:

> AI search should leave a verifiable trace, including how sources were touched, how they structurally contributed to answer components, and how contribution graphs may be safely passed to value-circulation review, without becoming a record of private thought, raw source capture, automatic payment, ownership assignment, or legal attribution.

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

Not automatic payment triggers.

This standard defines a minimal way to leave a trace:

```text
Search happened.
Signals were sampled.
Behavior was encoded.
Sources were touched.
Source interactions were classified.
Contribution relationships were mapped.
A value-circulation hook was exposed.
Automatic payment was prohibited.
Legal attribution was not decided.
Ownership was not assigned.
An answer was generated.
The event was minimized.
The receipt, graph, and hook can be verified.
The private conversation was not stored.
The raw source content was not stored.
```

That is the purpose of the AI Search Trace Receipt Standard.
