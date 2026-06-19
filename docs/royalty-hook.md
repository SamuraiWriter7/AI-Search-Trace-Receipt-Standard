# Royalty Hook

## Purpose

**Royalty Hook** defines a safety-bounded connection layer between a Source Contribution Graph and downstream value-circulation systems.

It does not calculate royalties.

It does not decide payment.

It does not assign ownership.

It does not determine legal attribution.

Instead, it records whether and how a contribution graph may be passed to downstream systems such as:

* Attribution review
* Royalty analysis
* Governance audit
* Provenance review
* Public attribution review
* Memory review

The purpose of this module is to create a controlled bridge from contribution structure to possible future value circulation without allowing automatic payment, legal attribution, ownership assignment, or raw content reconstruction.

---

## Version

```text
v0.4.0-candidate
```

Schema version:

```text
0.4.0
```

---

## Core Principle

> Connect to value circulation.
> Do not calculate royalties.

Royalty Hook is a connection boundary.

It exposes a safe hook for downstream review and analysis.

It does not execute economic, legal, or ownership decisions.

---

## Relationship to Earlier Versions

### v0.1: AI Search Trace Receipt

Version 0.1 records that an AI search event occurred.

```text
A search happened.
It was sampled.
It was encoded.
A receipt was created.
```

### v0.2: Source Interaction Trace

Version 0.2 records how individual sources were interacted with.

```text
A source was retrieved.
A source was cited.
A source was summarized.
A source was used as background context.
Raw source content was not stored.
```

### v0.3: Source Contribution Graph

Version 0.3 records how sources structurally relate to answer components, claims, and intermediate summaries.

```text
Source A supported Answer Component X.
Source B contextualized Answer Component X.
Source C verified Claim Y.
Claim Y supported Answer Component X.
```

### v0.4: Royalty Hook

Version 0.4 records how a contribution graph may be safely passed to downstream value-circulation or review systems.

```text
Contribution Graph A may be reviewed.
Contribution Graph A may be passed to royalty analysis.
Contribution Graph A must not trigger automatic payment.
Contribution Graph A must not decide ownership or legal attribution.
```

---

## Why This Module Is Separate

Royalty Hook is defined as a separate schema.

```text
schemas/royalty-hook.schema.json
```

It is not embedded directly inside the main AI Search Trace Receipt schema.

This follows the modular design introduced in v0.3:

```text
AI Search Trace Receipt Standard
├─ Core receipt schema
│  └─ schemas/ai-search-trace-receipt.schema.json
│
├─ Contribution graph module
│  └─ schemas/source-contribution-graph.schema.json
│
└─ Royalty hook module
   └─ schemas/royalty-hook.schema.json
```

The reason is simple:

Royalty Hook is not a receipt field.

It is an external connection boundary.

It sits between contribution evidence and downstream value-circulation systems.

---

## Conceptual Flow

```text
AI Search Event
  → AI Search Trace Receipt
    → Source Interaction Trace
      → Source Contribution Graph
        → Royalty Hook
          → Human Review / Policy Engine / Royalty Analysis
```

The Royalty Hook does not bypass review.

It routes contribution evidence toward controlled downstream use.

---

## What Royalty Hook Records

Royalty Hook records:

```text
hook identity
hook type
source contribution graph reference
eligibility signals
review requirement
allowed downstream use
prohibited downstream use
policy boundary
optional integrity metadata
```

It answers questions such as:

```text
Which contribution graph is being referenced?
May this graph be reviewed?
May this graph be passed to a royalty analysis system?
Is human review required?
Which downstream uses are allowed?
Which downstream uses are prohibited?
Does the hook include any payment, ownership, or legal attribution decision?
```

---

## What Royalty Hook Does Not Record

Royalty Hook must not record or decide:

```text
payment amount
royalty percentage
legal ownership
copyright status
final attribution claim
contractual entitlement
creator identity payout rule
automatic payment authorization
```

This boundary is essential.

Royalty Hook is not a royalty engine.

It is a safe connection point.

---

## Schema

Royalty Hook is defined by:

```text
schemas/royalty-hook.schema.json
```

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

## Example File

Royalty Hook example:

```text
examples/royalty-hook.example.yaml
```

---

## Example

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

---

## Field Definitions

## `schema_version`

The schema version of the Royalty Hook.

For v0.4:

```yaml
schema_version: "0.4.0"
```

---

## `hook_id`

A non-reversible identifier for the hook.

Example:

```yaml
hook_id: "royalty_hook_20260620_a13f"
```

The hook ID should not expose personal identifiers, private session IDs, raw source paths, or payout identities.

---

## `hook_type`

Defines the type of downstream bridge represented by this hook.

Initial values:

```text
contribution_graph_bridge
attribution_review_bridge
royalty_analysis_bridge
governance_audit_bridge
mixed
unknown
```

### `contribution_graph_bridge`

The hook connects a Source Contribution Graph to downstream review or analysis.

### `attribution_review_bridge`

The hook is intended for attribution review.

### `royalty_analysis_bridge`

The hook is intended for royalty analysis.

This does not authorize payment.

### `governance_audit_bridge`

The hook is intended for audit or governance review.

### `mixed`

The hook supports multiple bridge types.

### `unknown`

The hook type cannot be determined.

---

# Source Graph Reference

## `source_graph_ref`

The `source_graph_ref` object identifies the Source Contribution Graph referenced by the hook.

Required fields:

```text
graph_id
graph_hash
```

Optional field:

```text
graph_schema_version
```

Example:

```yaml
source_graph_ref:
  graph_id: "graph_20260620_a13f"
  graph_hash: "sha256:91bc3a7d9e"
  graph_schema_version: "0.3.0"
```

---

## `graph_id`

The identifier of the referenced Source Contribution Graph.

---

## `graph_hash`

The integrity hash of the referenced Source Contribution Graph.

This allows downstream systems to verify which contribution graph the hook points to without storing raw graph content inside the hook.

---

## `graph_schema_version`

The optional schema version of the referenced Source Contribution Graph.

For v0.3 graphs:

```yaml
graph_schema_version: "0.3.0"
```

---

# Eligibility

## `eligibility`

The `eligibility` object records whether the referenced contribution graph may be passed to downstream systems.

Required fields:

```text
eligible_for_review
eligible_for_royalty_system
eligible_for_public_attribution
confidence_level
```

---

## `eligible_for_review`

Whether this hook is eligible for human, governance, or policy review.

Example:

```yaml
eligible_for_review: true
```

---

## `eligible_for_royalty_system`

Whether this hook may be passed to a downstream royalty analysis system.

Example:

```yaml
eligible_for_royalty_system: true
```

Important boundary:

```text
eligible_for_royalty_system does not authorize payment.
```

It only means the hook may be reviewed or analyzed by a royalty-related system.

---

## `eligible_for_public_attribution`

Whether this hook may be considered for public attribution review.

Example:

```yaml
eligible_for_public_attribution: false
```

Important boundary:

```text
eligible_for_public_attribution does not decide public attribution.
```

It only indicates whether public attribution review is allowed.

---

## `confidence_level`

A broad confidence level for the hook eligibility signals.

Initial values:

```text
low
medium
high
unknown
```

This is not a payment confidence score.

It is only a broad signal for review and routing.

---

# Review

## `review`

The `review` object records review requirement and current review status.

Required fields:

```text
human_review_required
review_reason
review_status
```

---

## `human_review_required`

Whether human review is required before downstream action.

Example:

```yaml
human_review_required: true
```

For v0.4, human review should be required before any payment-related downstream decision.

---

## `review_reason`

The reason why review is required or recommended.

Initial values:

```text
contribution_signal_present
public_attribution_requested
royalty_analysis_requested
governance_audit_required
low_confidence
policy_boundary_check
unknown
```

---

## `review_status`

The current review status of the hook.

Initial values:

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

---

# Allowed Downstream Use

## `allowed_downstream_use`

The `allowed_downstream_use` array lists downstream use categories that are permitted for this hook.

Initial values:

```text
attribution_review
royalty_analysis
governance_audit
provenance_review
public_attribution_review
memory_review
unknown
```

Example:

```yaml
allowed_downstream_use:
  - "attribution_review"
  - "royalty_analysis"
  - "governance_audit"
```

These categories allow review or analysis.

They do not allow automatic execution.

---

# Prohibited Downstream Use

## `prohibited_downstream_use`

The `prohibited_downstream_use` array lists downstream use categories that are explicitly forbidden.

Initial values:

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

Example:

```yaml
prohibited_downstream_use:
  - "automatic_payment"
  - "legal_attribution_decision"
  - "ownership_assignment"
```

This field is central to the safety boundary of v0.4.

---

# Policy Boundary

## `policy_boundary`

The `policy_boundary` object declares what the hook does not contain or authorize.

Required fields:

```text
payment_decision_included
legal_attribution_included
ownership_decision_included
automatic_execution_allowed
human_review_required_before_payment
raw_content_stored
raw_query_stored
raw_answer_stored
```

---

## `payment_decision_included`

Must be false.

```yaml
payment_decision_included: false
```

This means the hook does not include a payment decision.

---

## `legal_attribution_included`

Must be false.

```yaml
legal_attribution_included: false
```

This means the hook does not include a legal attribution decision.

---

## `ownership_decision_included`

Must be false.

```yaml
ownership_decision_included: false
```

This means the hook does not include an ownership decision.

---

## `automatic_execution_allowed`

Must be false.

```yaml
automatic_execution_allowed: false
```

This means the hook does not authorize automatic payment, attribution, contract execution, or ownership assignment.

---

## `human_review_required_before_payment`

Must be true.

```yaml
human_review_required_before_payment: true
```

This means any payment decision requires a separate downstream process with human or policy review.

---

## `raw_content_stored`

Must be false.

```yaml
raw_content_stored: false
```

This means raw source content is not stored inside the hook.

---

## `raw_query_stored`

Must be false.

```yaml
raw_query_stored: false
```

This means raw user query text is not stored inside the hook.

---

## `raw_answer_stored`

Must be false.

```yaml
raw_answer_stored: false
```

This means raw AI answer text is not stored inside the hook.

---

# Integrity

## `integrity`

The optional `integrity` object may contain hook verification metadata.

Example:

```yaml
integrity:
  hook_hash: "sha256:7bd91ac44f"
  source_graph_hash: "sha256:91bc3a7d9e"
  previous_hook_hash: "sha256:3fa12bc980"
```

---

## `hook_hash`

A hash of this Royalty Hook.

---

## `source_graph_hash`

A hash of the referenced Source Contribution Graph.

This should match the hash declared in `source_graph_ref.graph_hash`.

---

## `previous_hook_hash`

An optional hash of a previous Royalty Hook.

This may support chained integrity.

---

## `signature`

An optional signature for hook verification.

---

# Royalty Hook vs. Source Contribution Graph

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

# Royalty Hook vs. Royalty Engine

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

# Royalty Hook vs. Legal Attribution

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

# Privacy Boundary

Royalty Hook must not become a hidden content capture, payout identity map, or behavioral profile.

It must not store:

* Raw source content
* Full URLs
* Raw user queries
* Raw AI answers
* Complete browsing history
* Personal identifiers
* Payout identities
* Contract identities
* Exact behavioral timelines
* Legal conclusions
* Payment decisions
* Ownership assignments

It records only minimized connection conditions.

---

# Safety Boundary

Royalty Hook must not allow automatic execution.

The following boundary must hold:

```text
No automatic payment.
No legal attribution decision.
No ownership assignment.
No automated contract execution.
No raw content reconstruction.
No identity resolution.
No user profiling.
```

The hook may support review.

It must not execute judgment.

---

# Validation

This module is validated separately from the main AI Search Trace Receipt schema and Source Contribution Graph schema.

Schema:

```text
schemas/royalty-hook.schema.json
```

Example:

```text
examples/royalty-hook.example.yaml
```

Validation command:

```bash
python scripts/validate_examples.py
```

Expected output:

```text
[validate] Royalty Hook
  schema : schemas/royalty-hook.schema.json
  example: examples/royalty-hook.example.yaml
[ok] Royalty Hook example is valid
```

---

# Non-Goals

Version 0.4 does not define:

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
* Full URL logging
* Raw content storage
* User-level browsing reconstruction
* Unified trace receipts

These are outside the scope of this version.

---

# Summary

Royalty Hook adds one key capability:

```text
It safely connects contribution evidence to downstream value-circulation review.
```

It records:

```text
hook identity
source graph reference
eligibility signals
review requirement
allowed downstream use
prohibited downstream use
policy boundary
integrity metadata
```

It does not record or decide:

```text
payment amount
royalty percentage
legal attribution
ownership
automatic execution
raw source content
raw user query
raw AI answer
payout identity
```

The principle is:

> Connect to value circulation.
> Do not calculate royalties.
