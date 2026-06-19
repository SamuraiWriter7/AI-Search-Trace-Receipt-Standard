# Source Contribution Graph

## Purpose

**Source Contribution Graph** defines a minimized graph structure for representing how sources contribute to an AI-mediated search answer.

Version 0.1 records that an AI search event occurred.

Version 0.2 records how individual sources were interacted with.

Version 0.3 records how sources relate to answer components through a graph structure.

The goal is to support auditability, attribution analysis, review workflows, and future value-circulation systems without defining royalty payments, legal attribution, or copyright compliance decisions.

---

## Version

```text
v0.3.0-candidate
```

---

## Core Principle

> Record contribution structure.
> Do not decide ownership, payment, or legal attribution.

Source Contribution Graph is a structural trace layer.

It does not determine:

* who should be paid
* how much should be paid
* whether a source legally contributed
* whether copyright-relevant use occurred
* whether attribution is legally required

It only records minimized graph signals that may support later review.

---

## Relationship to Earlier Versions

### v0.1: AI Search Trace Receipt

Records the search event itself.

```text
A search happened.
It was sampled.
It was encoded.
A receipt was created.
```

### v0.2: Source Interaction Trace

Records how each source was touched.

```text
A source was cited.
A source was summarized.
A source was used as background context.
Raw source content was not stored.
```

### v0.3: Source Contribution Graph

Records how sources relate to answer components.

```text
Source A supported answer component X.
Source B contextualized answer component X.
Source C contradicted answer component Y.
```

---

## Conceptual Flow

```text
AI Search Event
  → Source Interaction Trace
    → Answer Component Extraction
      → Contribution Node Creation
        → Contribution Edge Creation
          → Graph Boundary Declaration
            → Trace Receipt Updated
```

Simplified:

```text
Sources touched
  → Answer components identified
    → Relationships mapped
      → Contribution graph recorded
```

---

## New Optional Field

Version 0.3 introduces the optional top-level field:

```yaml
contribution_graph:
  graph_id: "graph_20260620_a13f"
  graph_type: "source_to_answer"
  nodes: []
  edges: []
  graph_policy:
    raw_content_stored: false
    royalty_decision_included: false
    legal_attribution_included: false
```

This field is optional.

When present, it records minimized contribution structure.

---

## Graph Model

The graph has three main parts:

```text
nodes
edges
graph_policy
```

### Nodes

Nodes represent sources, answer components, or intermediate trace elements.

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

Graph policy declares what the graph does not contain.

In v0.3, the graph must not contain:

```yaml
raw_content_stored: false
royalty_decision_included: false
legal_attribution_included: false
```

These fields preserve the boundary between contribution structure and payment or legal decisions.

---

## Example

```yaml
contribution_graph:
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

    - node_id: "ans_1"
      node_type: "answer_component"
      component_type: "synthesis"

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

  graph_policy:
    raw_content_stored: false
    royalty_decision_included: false
    legal_attribution_included: false
```

---

## Field Definitions

### `graph_id`

A non-reversible identifier for this contribution graph.

Example:

```text
graph_20260620_a13f
```

---

### `graph_type`

Defines the broad type of contribution graph.

Initial values:

```text
source_to_answer
source_to_claim
source_to_summary
mixed
unknown
```

---

### `nodes`

A list of graph nodes.

Each node must include:

```text
node_id
node_type
```

A source node may include:

```text
source_fingerprint
source_class_code
```

An answer component node may include:

```text
component_type
```

---

### `edges`

A list of graph relationships.

Each edge must include:

```text
from_node
to_node
relation_type
contribution_signal
evidence_mode
```

---

### `relation_type`

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

---

### `contribution_signal`

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

`contribution_signal` is not a royalty weight.

It is not a legal attribution score.

It is not a payment calculation.

It is only a minimized structural signal.

---

### `evidence_mode`

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

---

## Graph Policy

The graph policy declares the boundary of the contribution graph.

In v0.3, these values should be false:

```yaml
graph_policy:
  raw_content_stored: false
  royalty_decision_included: false
  legal_attribution_included: false
```

This means:

```text
The graph does not store raw source content.
The graph does not decide payment.
The graph does not decide legal attribution.
```

---

## Contribution Graph vs. Royalty Hook

Source Contribution Graph may inform a future royalty system.

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

## Contribution Graph vs. Source Interaction Trace

Source Interaction Trace records individual source contacts.

Contribution Graph records relationships among sources and answer components.

```text
Source Interaction Trace:
  Source A was cited.

Source Contribution Graph:
  Source A supported Answer Component X.
```

The second is more structured, but still not a payment rule.

---

## Privacy Boundary

Source Contribution Graph must not become a hidden content capture system.

It must not store:

* raw source content
* full URLs
* raw user queries
* raw AI answers
* complete browsing history
* personal identifiers
* exact behavioral timelines
* legal conclusions
* payment decisions

It records only minimized graph structure.

---

## Non-Goals

Version 0.3 does not define:

* royalty distribution
* payment allocation
* legal attribution
* copyright compliance
* ownership claims
* full provenance reconstruction
* model-internal attention graphs
* training data lineage

These are outside the scope of this version.

---

## Summary

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
```

It does not record:

```text
raw source content
full URLs
private queries
raw answers
payment decisions
legal attribution
```

The principle is:

> Record contribution structure.
> Do not decide ownership or payment.
