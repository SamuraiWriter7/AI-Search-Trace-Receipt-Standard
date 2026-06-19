# Source Interaction Trace

## Purpose

**Source Interaction Trace** defines how AI-mediated search systems may record minimized information about how sources were interacted with during a search event.

Version 0.1 of the AI Search Trace Receipt Standard records that sources were touched.

Version 0.2 adds a more precise layer:

> Record how a source was touched, not the source itself.

The goal is to support auditability, attribution, future contribution analysis, and governance review without storing raw source content, full URLs, complete browsing history, or personal identifiers.

---

## Version

```text
v0.2.0-candidate
```

---

## Core Concept

AI search does not merely retrieve sources.

It may interact with sources in different ways:

* Cite a source directly
* Use a source as background context
* Compare one source against another
* Summarize a source
* Use a source for verification
* Use a source as a counterpoint
* Retrieve a source and then ignore it
* Use a source as inspiration without direct citation

The Source Interaction Trace records these interactions as minimized structured signals.

It does not store the source content itself.

---

## Relationship to v0.1

Version 0.1 records broad source trace fields:

```yaml
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
```

This tells us:

```text
Sources were touched.
Some were cited.
Their broad categories are known.
Their raw identities are not stored.
```

Version 0.2 adds interaction-level signals:

```yaml
source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false
```

This tells us:

```text
A specific source fingerprint was cited.
It had high influence.
It was used as evidence.
The raw source content was not stored.
```

---

## New Optional Field

Version 0.2 introduces the optional top-level field:

```yaml
source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false
```

This field is optional.

When present, it records minimized source interaction signals.

---

## Conceptual Flow

```text
AI Search Event
  → Source Touched
    → Interaction Classified
      → Influence Bucketed
        → Usage Mode Encoded
          → Raw Content Excluded
            → Trace Receipt Updated
```

Simplified:

```text
Source touched
  → Interaction type
    → Influence level
      → Usage mode
        → No raw content
          → Receipt
```

---

## Field Definitions

### `source_fingerprint`

A non-reversible identifier for the source involved in the interaction.

Examples:

```text
domain_hash:38fa91
repo_hash:aa72ef
doc_hash:91cd02
paper_hash:7ab31f
```

The fingerprint should not expose:

* Full URLs
* Raw document titles when sensitive
* User-specific access paths
* Private document identifiers
* Tracking parameters

The goal is to make the source interaction verifiable without turning the receipt into a browsing log.

---

### `interaction_type`

Describes how the AI search process interacted with the source.

Initial values:

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

#### `retrieved`

The source was retrieved or considered by the search process.

This does not necessarily mean it influenced the final answer.

#### `cited`

The source was explicitly cited or referenced in the final answer.

#### `summarized`

The source was summarized by the AI system.

#### `compared`

The source was compared against one or more other sources.

#### `background_reference`

The source contributed general context but was not directly cited.

#### `validation_reference`

The source was used to verify, confirm, or check a claim.

#### `counterpoint`

The source was used as a contrasting or opposing view.

#### `ignored_after_retrieval`

The source was retrieved but not used in the final answer.

#### `unknown`

The interaction type could not be determined.

---

### `influence_level`

Describes the broad estimated influence of the source on the generated answer.

Initial values:

```text
none
low
medium
high
unknown
```

#### Important Boundary

`influence_level` is not a royalty weight.

It is not a payment score.

It is not a legal attribution claim.

It is only a minimized trace signal.

Future versions may define contribution graphs or royalty hooks, but v0.2 only records broad interaction influence.

---

### `usage_mode`

Describes the role of the source in the AI search result.

Initial values:

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

#### `evidence`

The source supported a claim in the answer.

#### `context`

The source provided background context.

#### `definition`

The source helped define a term, concept, or standard.

#### `comparison`

The source was used in comparison with another source or idea.

#### `example`

The source provided an example or case.

#### `verification`

The source was used to check the accuracy of a claim.

#### `disagreement`

The source provided a conflicting view or counterclaim.

#### `inspiration`

The source influenced direction or framing without being directly cited.

#### `unknown`

The usage mode could not be determined.

---

### `content_stored`

Declares whether raw source content was stored inside the receipt.

In v0.2, this value must be:

```yaml
content_stored: false
```

This field protects the boundary between trace evidence and content capture.

A valid Source Interaction Trace must not store the raw source text inside the receipt.

---

## Example

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

  - source_fingerprint: "paper_hash:7ab31f"
    interaction_type: "validation_reference"
    influence_level: "medium"
    usage_mode: "verification"
    content_stored: false
```

---

## Privacy Boundary

Source Interaction Trace must not become a browsing surveillance log.

It must not record:

* Full URLs
* Raw source content
* Full browsing history
* User-identifying access trails
* Exact behavioral timelines
* Private session identifiers
* Tracking parameters
* Account-specific source access paths

It records only minimized interaction signals.

---

## Trace Receipt vs. Source Capture

A source capture asks:

```text
What exact source content did the AI read?
What exact URL was opened?
What exact path did the user follow?
```

A Source Interaction Trace asks:

```text
What type of source interaction occurred?
Was the source cited, summarized, compared, or used as background?
What broad influence bucket describes the source?
Was raw source content excluded?
```

The first captures content and behavior.

The second preserves structural evidence.

---

## Interaction Trace vs. Contribution Claim

Source Interaction Trace is not the same as a contribution claim.

It does not decide:

* Who should be paid
* How much influence should count
* Whether a source legally contributed to the final answer
* Whether a source should receive attribution
* Whether copyright-relevant use occurred

It only records a minimized signal that may support future review.

In other words:

```text
Source Interaction Trace
  → may inform future Contribution Graph

Source Interaction Trace
  ≠ Contribution Graph
  ≠ Royalty Weight
  ≠ Legal Attribution
```

This separation is important.

v0.2 records the contact pattern.

Later versions may decide how that contact pattern should be interpreted.

---

## Relationship to Encoding Model

Source Interaction Trace relies on the Encoding Model introduced in v0.1.

The following fields are encoded signals:

```text
interaction_type
influence_level
usage_mode
content_stored
```

These fields convert source behavior into structured codes.

They do not preserve raw source text.

---

## Relationship to Privacy Boundary

Source Interaction Trace extends the privacy boundary from user queries and AI answers to source handling.

In v0.1, the required privacy constraints are:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false
```

In v0.2, source interactions add:

```yaml
content_stored: false
```

Together, these fields declare:

```text
The query is not stored.
The answer is not stored.
The personal identity is not linked.
The source content is not stored.
```

---

## Recommended Placement in Receipt

The `source_interactions` field should be placed after `source_trace` and before `answer_trace`.

Example:

```yaml
source_trace:
  source_count: 5
  source_fingerprints:
    - "domain_hash:38fa91"
    - "repo_hash:aa72ef"
  citation_count: 2
  source_class_codes:
    - "official"
    - "repository"

source_interactions:
  - source_fingerprint: "domain_hash:38fa91"
    interaction_type: "cited"
    influence_level: "high"
    usage_mode: "evidence"
    content_stored: false

answer_trace:
  answer_digest: "sha256:7c9e4f91a2b3c"
  confidence_bucket: "medium"
  transformation_code: "synthesis"
```

This placement keeps the receipt readable:

```text
Source summary
  → Source interaction detail
    → Answer trace
```

---

## Non-Goals

Version 0.2 does not define:

* Royalty distribution
* Contribution graph scoring
* Payment logic
* Full URL logging
* Raw content storage
* User-level browsing reconstruction
* Model-internal attention tracing
* Legal attribution decisions
* Copyright compliance decisions
* Training data provenance

These are outside the scope of Source Interaction Trace.

---

## v0.2 Boundary

Version 0.2 adds source interaction detail, but remains intentionally limited.

It answers:

```text
How was a source touched?
```

It does not answer:

```text
What exact source content was consumed?
Who owns the contribution?
How much should be paid?
What legal status does the interaction have?
```

That separation keeps v0.2 small, safe, and extensible.

---

## Summary

Source Interaction Trace adds one key capability:

```text
Not only that a source was touched,
but how it was touched.
```

It records:

```text
source fingerprint
interaction type
influence level
usage mode
content storage boundary
```

It does not record:

```text
raw source content
full URL
full browsing history
personal identity
exact behavioral timeline
```

This makes Source Interaction Trace the bridge between simple search trace receipts and future attribution or contribution systems.

The principle is:

> Record how the source was touched.
> Do not record the source itself.
