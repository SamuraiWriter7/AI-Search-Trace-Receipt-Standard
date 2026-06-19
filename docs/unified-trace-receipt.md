# Unified Trace Receipt

## Purpose

**Unified Trace Receipt** defines a unified receipt envelope that binds together independently validated trace modules.

It does not merge raw records.

It does not collapse module boundaries.

It does not store raw queries, raw answers, or raw source content.

It does not calculate royalties, execute payment, decide legal attribution, or assign ownership.

Instead, it records how the following modules are linked:

* AI Search Trace Receipt
* Source Contribution Graph
* Royalty Hook

The purpose of this module is to provide a verifiable envelope for connecting search trace evidence, contribution structure, and value-circulation hooks while preserving privacy, modularity, and safety boundaries.

---

## Version

```text
v0.5.0-candidate
```

Schema version:

```text
0.5.0
```

---

## Core Principle

> Bind the trace modules.
> Do not collapse the boundaries.

Unified Trace Receipt is a binding layer.

It connects independently validated modules.

It does not absorb them into a single surveillance log, payment engine, legal attribution system, or ownership ledger.

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

Version 0.4 records how a Source Contribution Graph may be safely passed to downstream value-circulation or review systems.

```text
Contribution Graph A may be reviewed.
Contribution Graph A may be passed to royalty analysis.
Contribution Graph A must not trigger automatic payment.
Contribution Graph A must not decide ownership or legal attribution.
```

### v0.5: Unified Trace Receipt

Version 0.5 records how the modules are bound together.

```text
AI Search Trace Receipt A
  is linked to Source Contribution Graph B
  which is linked to Royalty Hook C.

The modules remain separate.
Raw content is not merged.
Payment is not executed.
Legal attribution is not decided.
Ownership is not assigned.
```

---

## Why This Module Exists

Starting with v0.3, larger extension layers are defined as separate schemas.

This is intentional.

```text
schemas/
├─ ai-search-trace-receipt.schema.json
├─ source-contribution-graph.schema.json
├─ royalty-hook.schema.json
└─ unified-trace-receipt.schema.json
```

This modular design prevents the main receipt schema from becoming too large.

However, once the modules are separated, a new question appears:

```text
Which AI Search Trace Receipt belongs to which Source Contribution Graph?

Which Source Contribution Graph is connected to which Royalty Hook?

Do these modules belong to the same event chain?

Were their boundaries preserved?
```

Unified Trace Receipt answers these questions.

It is the envelope that binds the modules.

It is not a new raw log.

---

## Conceptual Flow

```text
AI Search Event
  → AI Search Trace Receipt
    → Source Interaction Trace
      → Source Contribution Graph
        → Royalty Hook
          → Unified Trace Receipt
```

More precisely:

```text
Search trace evidence
  → source interaction evidence
    → contribution structure
      → value-circulation hook
        → unified module binding
```

The Unified Trace Receipt binds the chain.

It does not replace the chain.

---

## What Unified Trace Receipt Records

Unified Trace Receipt records:

```text
unified receipt identity
receipt type
module references
module relationships
event binding metadata
boundary preservation declarations
unified policy boundary
verification status
integrity chain
```

It answers questions such as:

```text
Which modules are included?
Which hashes identify those modules?
How are the modules related?
Do they belong to the same trace chain?
Were module boundaries preserved?
Has the integrity chain been verified?
Does the unified receipt include any prohibited decision?
```

---

## What Unified Trace Receipt Does Not Record

Unified Trace Receipt must not record:

```text
raw user query
raw AI answer
raw source content
full URL history
personal identity
payout identity
contract identity
payment amount
royalty percentage
legal attribution
ownership assignment
automatic execution authorization
```

The unified receipt is not a content archive.

It is not a surveillance log.

It is not a payment engine.

It is not a legal attribution system.

---

## Schema

Unified Trace Receipt is defined by:

```text
schemas/unified-trace-receipt.schema.json
```

Required top-level fields:

```text
schema_version
unified_receipt_id
receipt_type
module_refs
module_relationships
unified_policy_boundary
verification_status
integrity_chain
```

---

## Example File

Unified Trace Receipt example:

```text
examples/unified-trace-receipt.example.yaml
```

---

## Example

```yaml
schema_version: "0.5.0"
unified_receipt_id: "utr_20260620_a13f"
receipt_type: "ai_search_unified_trace"

module_refs:
  ai_search_trace_receipt:
    trace_id: "trace_20260620_a13f"
    receipt_hash: "sha256:abc123def456"
    schema_version: "0.2.0"

  source_contribution_graph:
    graph_id: "graph_20260620_a13f"
    graph_hash: "sha256:91bc3a7d9e"
    schema_version: "0.3.0"

  royalty_hook:
    hook_id: "royalty_hook_20260620_a13f"
    hook_hash: "sha256:7bd91ac44f"
    schema_version: "0.4.0"

module_relationships:
  relationship_type: "search_to_contribution_to_royalty_hook"
  linkage_status: "linked"

  event_binding:
    shared_event_fingerprint: "event_hash:20260620_a13f"
    binding_method: "hash_chain"
    binding_confidence: "high"

  boundary_preservation:
    modules_remain_separate: true
    raw_content_not_merged: true
    payment_not_executed: true
    legal_attribution_not_decided: true
    ownership_not_assigned: true

unified_policy_boundary:
  raw_query_stored: false
  raw_answer_stored: false
  raw_source_content_stored: false
  personal_id_linked: false
  payment_decision_included: false
  legal_attribution_included: false
  ownership_decision_included: false
  automatic_execution_allowed: false

verification_status:
  receipt_verified: true
  module_refs_verified: true
  integrity_chain_verified: true
  verification_level: "module_hashes_checked"
  verification_notes: "Module identifiers and hashes were checked without storing raw query, answer, or source content."

integrity_chain:
  unified_receipt_hash: "sha256:utr91bc3a7d9e"
  previous_unified_receipt_hash: "sha256:utr44af09c81b"
  module_hashes:
    ai_search_trace_receipt_hash: "sha256:abc123def456"
    source_contribution_graph_hash: "sha256:91bc3a7d9e"
    royalty_hook_hash: "sha256:7bd91ac44f"
  chain_method: "explicit_hash_bundle"
```

---

## Field Definitions

## `schema_version`

The schema version of the Unified Trace Receipt.

For v0.5:

```yaml
schema_version: "0.5.0"
```

---

## `unified_receipt_id`

A non-reversible identifier for the unified receipt.

Example:

```yaml
unified_receipt_id: "utr_20260620_a13f"
```

The unified receipt ID should not expose personal identifiers, private session IDs, payout identities, raw source paths, or raw query text.

---

## `receipt_type`

Defines the type of unified trace receipt.

Initial values:

```text
ai_search_unified_trace
search_contribution_royalty_bundle
audit_bundle
review_bundle
mixed
unknown
```

### `ai_search_unified_trace`

A unified receipt for an AI-mediated search trace chain.

### `search_contribution_royalty_bundle`

A unified receipt binding search evidence, contribution graph evidence, and a royalty hook.

### `audit_bundle`

A unified receipt intended for audit workflows.

### `review_bundle`

A unified receipt intended for human, governance, or policy review.

### `mixed`

The receipt contains multiple binding patterns.

### `unknown`

The receipt type cannot be determined.

---

# Module References

## `module_refs`

The `module_refs` object identifies the independently validated modules bound by the unified receipt.

Required module references:

```text
ai_search_trace_receipt
source_contribution_graph
royalty_hook
```

The modules remain independent.

The unified receipt references them through identifiers and hashes.

It does not copy their raw contents.

---

## `module_refs.ai_search_trace_receipt`

Reference to the AI Search Trace Receipt module.

Required fields:

```text
trace_id
receipt_hash
schema_version
```

Example:

```yaml
ai_search_trace_receipt:
  trace_id: "trace_20260620_a13f"
  receipt_hash: "sha256:abc123def456"
  schema_version: "0.2.0"
```

---

## `trace_id`

Identifier of the referenced AI Search Trace Receipt.

---

## `receipt_hash`

Integrity hash of the referenced AI Search Trace Receipt.

This allows verification without storing the full receipt content inside the unified receipt.

---

## `module_refs.source_contribution_graph`

Reference to the Source Contribution Graph module.

Required fields:

```text
graph_id
graph_hash
schema_version
```

Example:

```yaml
source_contribution_graph:
  graph_id: "graph_20260620_a13f"
  graph_hash: "sha256:91bc3a7d9e"
  schema_version: "0.3.0"
```

---

## `graph_id`

Identifier of the referenced Source Contribution Graph.

---

## `graph_hash`

Integrity hash of the referenced Source Contribution Graph.

---

## `module_refs.royalty_hook`

Reference to the Royalty Hook module.

Required fields:

```text
hook_id
hook_hash
schema_version
```

Example:

```yaml
royalty_hook:
  hook_id: "royalty_hook_20260620_a13f"
  hook_hash: "sha256:7bd91ac44f"
  schema_version: "0.4.0"
```

---

## `hook_id`

Identifier of the referenced Royalty Hook.

---

## `hook_hash`

Integrity hash of the referenced Royalty Hook.

---

# Module Relationships

## `module_relationships`

The `module_relationships` object describes how the referenced modules are linked.

Required fields:

```text
relationship_type
linkage_status
event_binding
boundary_preservation
```

---

## `relationship_type`

The broad relationship pattern between referenced modules.

Initial values:

```text
search_to_contribution_to_royalty_hook
search_to_contribution
contribution_to_royalty_hook
audit_bundle
review_bundle
mixed
unknown
```

### `search_to_contribution_to_royalty_hook`

The AI Search Trace Receipt is connected to a Source Contribution Graph, which is connected to a Royalty Hook.

### `search_to_contribution`

The receipt is connected to a contribution graph, but not necessarily to a royalty hook.

### `contribution_to_royalty_hook`

The contribution graph is connected to a royalty hook.

### `audit_bundle`

The modules are bound for audit review.

### `review_bundle`

The modules are bound for human, governance, or policy review.

### `mixed`

Multiple relationship patterns are present.

### `unknown`

The relationship type cannot be determined.

---

## `linkage_status`

The current linkage status of the referenced modules.

Initial values:

```text
linked
partially_linked
pending_review
broken
unknown
```

### `linked`

The modules are linked and the linkage is declared.

### `partially_linked`

Some modules are linked, but the chain is incomplete.

### `pending_review`

The linkage requires additional review.

### `broken`

The linkage is invalid or incomplete.

### `unknown`

The linkage status cannot be determined.

---

# Event Binding

## `event_binding`

The `event_binding` object records how the modules are bound to the same event or review chain.

Required fields:

```text
shared_event_fingerprint
binding_method
binding_confidence
```

---

## `shared_event_fingerprint`

A non-reversible fingerprint indicating shared event lineage across modules.

Example:

```yaml
shared_event_fingerprint: "event_hash:20260620_a13f"
```

This must not expose raw query text, raw source content, exact browsing timelines, or personal identifiers.

---

## `binding_method`

The method used to bind the modules together.

Initial values:

```text
hash_chain
explicit_reference
timestamp_bucket
shared_trace_id
mixed
unknown
```

### `hash_chain`

Modules are linked through a hash chain.

### `explicit_reference`

Modules explicitly reference each other.

### `timestamp_bucket`

Modules are linked through a shared rounded timestamp bucket.

### `shared_trace_id`

Modules are linked through a shared trace identifier.

### `mixed`

Multiple binding methods are used.

### `unknown`

The binding method cannot be determined.

---

## `binding_confidence`

Broad confidence level that the referenced modules belong to the same trace chain.

Initial values:

```text
low
medium
high
unknown
```

This is not a legal confidence score.

It is not payment confidence.

It is only a structural verification signal.

---

# Boundary Preservation

## `boundary_preservation`

The `boundary_preservation` object declares that module boundaries remain preserved.

Required fields:

```text
modules_remain_separate
raw_content_not_merged
payment_not_executed
legal_attribution_not_decided
ownership_not_assigned
```

---

## `modules_remain_separate`

Must be true.

```yaml
modules_remain_separate: true
```

This means the unified receipt binds module references but does not merge the modules into one raw record.

---

## `raw_content_not_merged`

Must be true.

```yaml
raw_content_not_merged: true
```

This means raw query, answer, and source content must not be merged into the unified receipt.

---

## `payment_not_executed`

Must be true.

```yaml
payment_not_executed: true
```

This means the unified receipt must not execute payment.

---

## `legal_attribution_not_decided`

Must be true.

```yaml
legal_attribution_not_decided: true
```

This means the unified receipt must not decide legal attribution.

---

## `ownership_not_assigned`

Must be true.

```yaml
ownership_not_assigned: true
```

This means the unified receipt must not assign ownership.

---

# Unified Policy Boundary

## `unified_policy_boundary`

The `unified_policy_boundary` object declares the safety and privacy boundary for the unified receipt.

Required fields:

```text
raw_query_stored
raw_answer_stored
raw_source_content_stored
personal_id_linked
payment_decision_included
legal_attribution_included
ownership_decision_included
automatic_execution_allowed
```

---

## `raw_query_stored`

Must be false.

```yaml
raw_query_stored: false
```

This means raw user query text is not stored inside the unified receipt.

---

## `raw_answer_stored`

Must be false.

```yaml
raw_answer_stored: false
```

This means raw AI answer text is not stored inside the unified receipt.

---

## `raw_source_content_stored`

Must be false.

```yaml
raw_source_content_stored: false
```

This means raw source content is not stored inside the unified receipt.

---

## `personal_id_linked`

Must be false.

```yaml
personal_id_linked: false
```

This means the unified receipt must not directly link to personal identifiers.

---

## `payment_decision_included`

Must be false.

```yaml
payment_decision_included: false
```

This means the unified receipt must not include a payment decision.

---

## `legal_attribution_included`

Must be false.

```yaml
legal_attribution_included: false
```

This means the unified receipt must not include a legal attribution decision.

---

## `ownership_decision_included`

Must be false.

```yaml
ownership_decision_included: false
```

This means the unified receipt must not include an ownership decision.

---

## `automatic_execution_allowed`

Must be false.

```yaml
automatic_execution_allowed: false
```

This means the unified receipt must not authorize automatic payment, contract execution, ownership assignment, or legal attribution.

---

# Verification Status

## `verification_status`

The `verification_status` object records verification status for the unified receipt and referenced modules.

Required fields:

```text
receipt_verified
module_refs_verified
integrity_chain_verified
verification_level
```

Optional field:

```text
verification_notes
```

---

## `receipt_verified`

Whether the unified receipt itself has been verified.

Example:

```yaml
receipt_verified: true
```

---

## `module_refs_verified`

Whether referenced module identifiers and hashes have been verified.

Example:

```yaml
module_refs_verified: true
```

---

## `integrity_chain_verified`

Whether the integrity chain has been verified.

Example:

```yaml
integrity_chain_verified: true
```

---

## `verification_level`

Broad verification level for this unified receipt.

Initial values:

```text
none
basic
module_hashes_checked
full_chain_checked
human_reviewed
unknown
```

### `none`

No verification has been performed.

### `basic`

Basic structural verification has been performed.

### `module_hashes_checked`

Referenced module hashes have been checked.

### `full_chain_checked`

The full integrity chain has been checked.

### `human_reviewed`

The unified receipt has been reviewed by a human or governance process.

### `unknown`

The verification level cannot be determined.

---

## `verification_notes`

Optional minimized notes about verification status.

Important boundary:

```text
verification_notes must not contain raw query, raw answer, or source content.
```

---

# Integrity Chain

## `integrity_chain`

The `integrity_chain` object records verification metadata for the unified receipt and referenced modules.

Required fields:

```text
unified_receipt_hash
module_hashes
chain_method
```

Optional fields:

```text
previous_unified_receipt_hash
signature
```

---

## `unified_receipt_hash`

Hash of this Unified Trace Receipt.

Example:

```yaml
unified_receipt_hash: "sha256:utr91bc3a7d9e"
```

---

## `previous_unified_receipt_hash`

Optional hash of a previous Unified Trace Receipt.

This may support chained integrity.

---

## `module_hashes`

The `module_hashes` object records hashes of the referenced modules.

Required fields:

```text
ai_search_trace_receipt_hash
source_contribution_graph_hash
royalty_hook_hash
```

Example:

```yaml
module_hashes:
  ai_search_trace_receipt_hash: "sha256:abc123def456"
  source_contribution_graph_hash: "sha256:91bc3a7d9e"
  royalty_hook_hash: "sha256:7bd91ac44f"
```

---

## `chain_method`

The method used to establish the integrity chain.

Initial values:

```text
hash_chain
merkle_like_summary
explicit_hash_bundle
signature_bundle
mixed
unknown
```

### `hash_chain`

The unified receipt and modules are linked through a hash chain.

### `merkle_like_summary`

The module hashes are summarized in a Merkle-like structure.

### `explicit_hash_bundle`

The module hashes are explicitly listed as a bundle.

### `signature_bundle`

The module references are bound through a signature bundle.

### `mixed`

Multiple chain methods are used.

### `unknown`

The chain method cannot be determined.

---

## `signature`

Optional signature for unified receipt verification.

---

# Unified Trace Receipt vs. Module Merge

Unified Trace Receipt is not a module merge.

```text
Module merge:
  Copy all module content into one large record.

Unified Trace Receipt:
  Reference modules through identifiers and hashes.
```

The unified receipt does not absorb raw contents.

It binds references.

---

# Unified Trace Receipt vs. Surveillance Log

A surveillance log asks:

```text
Who searched what, exactly, when, where, and through which sources?
```

A Unified Trace Receipt asks:

```text
Which trace modules belong together?
Were the modules verified?
Were module boundaries preserved?
Was raw content excluded?
Was automatic payment prohibited?
Was legal attribution not decided?
```

The first captures behavior.

The second preserves structural evidence and boundaries.

---

# Unified Trace Receipt vs. Royalty Engine

Unified Trace Receipt is not a royalty engine.

```text
Unified Trace Receipt
  → may bind a Royalty Hook reference

Unified Trace Receipt
  ≠ royalty calculator
  ≠ payment allocator
  ≠ distribution engine
  ≠ legal entitlement system
```

It can show that a Royalty Hook exists.

It cannot execute payment.

---

# Unified Trace Receipt vs. Legal Attribution

Unified Trace Receipt does not make legal claims.

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

It only records module bindings and verification signals.

---

# Privacy Boundary

Unified Trace Receipt must not become a hidden content capture, payout identity map, or behavioral profile.

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

It records only minimized module references, relationship metadata, boundary declarations, verification status, and integrity chain data.

---

# Safety Boundary

The unified receipt must preserve the following boundary:

```text
No raw query storage.
No raw answer storage.
No raw source content storage.
No personal ID linkage.
No automatic payment.
No legal attribution decision.
No ownership assignment.
No automated contract execution.
```

The unified receipt may bind modules.

It must not execute judgment.

---

# Validation

This module is validated separately from the AI Search Trace Receipt schema, Source Contribution Graph schema, and Royalty Hook schema.

Schema:

```text
schemas/unified-trace-receipt.schema.json
```

Example:

```text
examples/unified-trace-receipt.example.yaml
```

Validation command:

```bash
python scripts/validate_examples.py
```

Expected output:

```text
[validate] Unified Trace Receipt
  schema : schemas/unified-trace-receipt.schema.json
  example: examples/unified-trace-receipt.example.yaml
[ok] Unified Trace Receipt example is valid
```

---

# Non-Goals

Version 0.5 does not define:

* Raw search history archive
* Raw content capture
* Full browsing reconstruction
* Payment allocation
* Automatic payment
* Royalty calculation
* Legal attribution
* Copyright compliance
* Ownership claims
* Contract execution
* Creator identity resolution
* Payout identity mapping
* Model-internal attention graphs
* Training data lineage
* Complete AI governance framework

These are outside the scope of this version.

---

# Summary

Unified Trace Receipt adds one key capability:

```text
It binds independently validated trace modules into one verifiable envelope.
```

It records:

```text
unified receipt identity
module references
module relationships
event binding metadata
boundary preservation declarations
unified policy boundary
verification status
integrity chain
```

It does not record or decide:

```text
raw user query
raw AI answer
raw source content
personal identity
payment amount
royalty percentage
legal attribution
ownership assignment
automatic execution
```

The principle is:

> Bind the trace modules.
> Do not collapse the boundaries.
