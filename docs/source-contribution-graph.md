# Source Contribution Graph

## Purpose

**Source Contribution Graph** defines a minimized graph structure for representing how sources contribute to answer components in AI-mediated search.

Version 0.1 of the AI Search Trace Receipt Standard records that an AI search event occurred.

Version 0.2 records how individual sources were interacted with.

Version 0.3 introduces a graph layer that represents relationships between source fingerprints, claims, summaries, and answer components.

The purpose of this module is to support auditability, attribution analysis, review workflows, and future value-circulation systems without defining royalty payments, ownership claims, legal attribution, or copyright compliance decisions.

---

## Version

```text
v0.3.0-candidate
```

---

## Core Principle

> Record contribution structure.
> Do not decide ownership or payment.

Source Contribution Graph is a structural trace layer.

It records minimized relationships between sources and answer components.

It does not determine:

* Who should be paid
* How much should be paid
* Whether a source legally contributed
* Whether copyright-relevant use occurred
* Whether attribution is legally required
* Whether a source owns part of the generated answer

Those decisions are outside the scope of v0.3.

---

## Relationship to Earlier Versions

### v0.1: AI Search Trace Receipt

Version 0.1 records the search event itself.

```text
A search happened.
It was sampled.
It was encoded.
A receipt was created.
```

### v0.2: Source Interaction Trace

Version 0.2 records how each source was touched.

```text
A source was retrieved.
A source was cited.
A source was summarized.
A source was used as background context.
Raw source content was not stored.
```

### v0.3: Source Contribution Graph

Version 0.3 records how sources relate to answer components.

```text
Source A supported Answer Component X.
Source B contextualized Answer Component X.
Source C verified Claim Y.
Claim Y supported Answer Component X.
```

---

## Why This Module Is Separate

Starting with v0.3, larger extension layers are defined as separate schemas.

The main AI Search Trace Receipt schema acts as a receipt envelope.

Specialized structures such as Source Contribution Graph are validated as independent modules.

This keeps the core receipt small, stable, and extensible.

```text
AI Search Trace Receipt
  ├─ Core receipt fields
  ├─ Source Interaction Trace
  └─ Source Contribution Graph
```

The Contribution Graph is not just another receipt field.

It is an attached structural map.

---

## Conceptual Flow

```text
AI Search Event
  → Source Interaction Trace
    → Answer Component Identification
      → Contribution Node Creation
        → Contribution Edge Creation
          → Graph Boundary Declaration
            → Contribution Graph
```

Simplified:

```text
Sources touched
  → Answer components identified
    → Relationships mapped
      → Contribution graph recorded
```

---

## Graph Model

The Source Contribution Graph has four main parts:

```text
graph identity
nodes
edges
graph policy
```

### Graph Identity

The graph identity identifies the contribution graph itself.

Required fields:

```text
schema_version
graph_id
graph_type
```

### Nodes

Nodes represent entities inside the contribution graph.

Initial node types:

```text
source
answer_component
intermediate_summary
claim
unknown
```

### Edges

Edges represent relationships between nodes.

Initial relation types:

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

### Graph Policy

Graph policy declares what the graph does not contain or decide.

Required policy boundaries:

```yaml
raw_content_stored: false
raw_query_stored: false
raw_answer_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

---

## New Schema

Version 0.3 introduces a separate schema:

```text
schemas/source-contribution-graph.schema.json
```

This schema is validated independently from the main AI Search Trace Receipt schema.

---

## Example File

Version 0.3 introduces a separate example:

```text
examples/source-contribution-graph.example.yaml
```

---

## Example

```yaml
schema_version: "0.3.0"
graph_id: "graph_20260620_a13f"
graph_type: "source_to_answer"

nodes:
  - node_id: "src_1"
    node_type: "source"
    source_fingerprint: "domain_hash:38fa91"
    source_class_code: "official"

  - node_id: "src_2"
    node_type: "source"
    source_fingerprint: "repo_hash:aa72ef"
    source_class_code: "repository"

  - node_id: "src_3"
    node_type: "source"
    source_fingerprint: "paper_hash:7ab31f"
    source_class_code: "academic"

  - node_id: "ans_1"
    node_type: "answer_component"
    component_type: "synthesis"
    component_digest: "sha256:7c9e4f91a2b3c"

  - node_id: "claim_1"
    node_type: "claim"
    component_type: "claim"
    component_digest: "sha256:2f4a91bc83de"

edges:
  - from_node: "src_1"
    to_node: "ans_1"
    relation_type: "supports"
    contribution_signal: "high"
    evidence_mode: "cited"

  - from_node: "src_2"
    to_node: "ans_1"
    relation_type: "contextualizes"
    contribution_signal: "medium"
    evidence_mode: "background_reference"

  - from_node: "src_3"
    to_node: "claim_1"
    relation_type: "verifies"
    contribution_signal: "medium"
    evidence_mode: "validation_reference"

  - from_node: "claim_1"
    to_node: "ans_1"
    relation_type: "supports"
    contribution_signal: "medium"
    evidence_mode: "derived_from_interaction"

graph_policy:
  raw_content_stored: false
  raw_query_stored: false
  raw_answer_stored: false
  royalty_decision_included: false
  legal_attribution_included: false

integrity:
  graph_hash: "sha256:91bc3a7d9e"
  previous_graph_hash: "sha256:44af09c81b"
```

---

## Field Definitions

## `schema_version`

The schema version of the Source Contribution Graph.

For v0.3:

```yaml
schema_version: "0.3.0"
```

---

## `graph_id`

A non-reversible identifier for this contribution graph.

Example:

```yaml
graph_id: "graph_20260620_a13f"
```

The graph ID should not expose personal identifiers, raw query text, session IDs, or private source paths.

---

## `graph_type`

Defines the broad type of contribution graph.

Initial values:

```text
source_to_answer
source_to_claim
source_to_summary
mixed
unknown
```

### `source_to_answer`

Sources are mapped directly to answer components.

### `source_to_claim`

Sources are mapped to specific claims.

### `source_to_summary`

Sources are mapped to intermediate summaries.

### `mixed`

The graph contains multiple relationship patterns.

### `unknown`

The graph type cannot be determined.

---

# Nodes

## `nodes`

The `nodes` array defines the entities inside the contribution graph.

Each node must include:

```text
node_id
node_type
```

Example:

```yaml
nodes:
  - node_id: "src_1"
    node_type: "source"
    source_fingerprint: "domain_hash:38fa91"
    source_class_code: "official"
```

---

## `node_id`

A local identifier for a graph node.

Example:

```yaml
node_id: "src_1"
```

The `node_id` is local to the graph.

It does not need to be globally unique.

---

## `node_type`

Defines the type of node.

Initial values:

```text
source
answer_component
intermediate_summary
claim
unknown
```

### `source`

A source touched during the AI search event.

### `answer_component`

A component of the final answer.

### `intermediate_summary`

A summary created during the search or reasoning process.

### `claim`

A claim extracted, verified, supported, or contradicted during answer construction.

### `unknown`

The node type cannot be determined.

---

## `source_fingerprint`

A non-reversible source identifier for source nodes.

Example:

```yaml
source_fingerprint: "domain_hash:38fa91"
```

This should not store full URLs, raw titles, private file paths, tracking parameters, or personal identifiers.

---

## `source_class_code`

A broad category for the source node.

Initial values:

```text
official
documentation
academic
news
repository
blog
forum
database
unknown
```

---

## `component_type`

A broad category for an answer component, claim, or intermediate summary.

Initial values:

```text
direct_answer
summary
comparison
synthesis
translation
extraction
classification
claim
unknown
```

---

## `component_digest`

An optional digest of an answer component.

Example:

```yaml
component_digest: "sha256:7c9e4f91a2b3c"
```

This must not contain raw answer text.

It exists only to support later verification.

---

# Edges

## `edges`

The `edges` array defines contribution relationships between graph nodes.

Each edge must include:

```text
from_node
to_node
relation_type
contribution_signal
evidence_mode
```

Example:

```yaml
edges:
  - from_node: "src_1"
    to_node: "ans_1"
    relation_type: "supports"
    contribution_signal: "high"
    evidence_mode: "cited"
```

---

## `from_node`

The source node ID for this edge.

Example:

```yaml
from_node: "src_1"
```

---

## `to_node`

The target node ID for this edge.

Example:

```yaml
to_node: "ans_1"
```

---

## `relation_type`

Describes the relationship between two nodes.

Initial values:

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

### `supports`

The source or claim supports an answer component.

### `contextualizes`

The source provides background context for an answer component.

### `contradicts`

The source or claim conflicts with another node.

### `defines`

The source helps define a term, concept, or boundary.

### `compares`

The source contributes to a comparison.

### `summarizes`

The node summarizes another node.

### `inspires`

The source influenced framing or direction without serving as direct evidence.

### `verifies`

The source helps confirm or validate a claim.

### `unknown`

The relationship type cannot be determined.

---

## `contribution_signal`

A broad signal of contribution strength.

Initial values:

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

## `evidence_mode`

Describes the evidence basis for the edge.

Initial values:

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

### `cited`

The relationship is based on an explicit citation.

### `summarized`

The relationship is based on a summarized source.

### `compared`

The relationship is based on comparison.

### `background_reference`

The relationship is based on background context.

### `validation_reference`

The relationship is based on verification or checking.

### `counterpoint`

The relationship is based on contrast or disagreement.

### `derived_from_interaction`

The relationship is derived from a prior source interaction trace.

### `unknown`

The evidence basis cannot be determined.

---

# Graph Policy

## `graph_policy`

The `graph_policy` object declares the boundary of the contribution graph.

It prevents the graph from becoming a hidden content capture, royalty engine, or legal attribution system.

Required fields:

```text
raw_content_stored
raw_query_stored
raw_answer_stored
royalty_decision_included
legal_attribution_included
```

---

## `raw_content_stored`

Must be false.

```yaml
raw_content_stored: false
```

This means raw source content is not stored inside the graph.

---

## `raw_query_stored`

Must be false.

```yaml
raw_query_stored: false
```

This means raw user query text is not stored inside the graph.

---

## `raw_answer_stored`

Must be false.

```yaml
raw_answer_stored: false
```

This means raw AI answer text is not stored inside the graph.

---

## `royalty_decision_included`

Must be false.

```yaml
royalty_decision_included: false
```

This means v0.3 does not decide payment, revenue allocation, royalties, or compensation.

---

## `legal_attribution_included`

Must be false.

```yaml
legal_attribution_included: false
```

This means v0.3 does not decide legal attribution, copyright status, ownership, or liability.

---

# Integrity

## `integrity`

The optional `integrity` object may contain graph verification metadata.

Example:

```yaml
integrity:
  graph_hash: "sha256:91bc3a7d9e"
  previous_graph_hash: "sha256:44af09c81b"
```

---

## `graph_hash`

A hash of this contribution graph.

---

## `previous_graph_hash`

An optional hash of a previous contribution graph.

This may support chained integrity.

---

## `signature`

An optional signature for graph verification.

---

# Contribution Graph vs. Source Interaction Trace

Source Interaction Trace records individual source contacts.

Source Contribution Graph records relationships among sources, claims, summaries, and answer components.

```text
Source Interaction Trace:
  Source A was cited.

Source Contribution Graph:
  Source A supported Answer Component X.
```

The graph is more structured, but it is still not a payment rule.

---

# Contribution Graph vs. Royalty Hook

Source Contribution Graph may inform a future Royalty Hook.

But it is not itself a royalty system.

```text
Contribution Graph
  → may inform Royalty Hook

Contribution Graph
  ≠ Royalty Hook
  ≠ Payment Rule
  ≠ Legal Attribution
```

This distinction is central to v0.3.

---

# Contribution Graph vs. Legal Attribution

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

# Privacy Boundary

Source Contribution Graph must not become a hidden content capture system.

It must not store:

* Raw source content
* Full URLs
* Raw user queries
* Raw AI answers
* Complete browsing history
* Personal identifiers
* Exact behavioral timelines
* Legal conclusions
* Payment decisions

It records only minimized graph structure.

---

# Validation

This module is validated separately from the main AI Search Trace Receipt schema.

Schema:

```text
schemas/source-contribution-graph.schema.json
```

Example:

```text
examples/source-contribution-graph.example.yaml
```

Validation command:

```bash
python scripts/validate_examples.py
```

Expected output:

```text
[validate] Source Contribution Graph
  schema : schemas/source-contribution-graph.schema.json
  example: examples/source-contribution-graph.example.yaml
[ok] Source Contribution Graph example is valid
```

---

# Non-Goals

Version 0.3 does not define:

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

These are outside the scope of this version.

---

# Summary

Source Contribution Graph adds one key capability:

```text
Not only how sources were touched,
but how they structurally contributed to answer components.
```

It records:

```text
nodes
edges
relation types
contribution signals
evidence modes
graph policy
integrity metadata
```

It does not record:

```text
raw source content
full URLs
private queries
raw answers
payment decisions
legal attribution
ownership claims
```

The principle is:

> Record contribution structure.
> Do not decide ownership or payment.
