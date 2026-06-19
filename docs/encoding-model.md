# Encoding Model

## Purpose

The Encoding Model defines how AI search behavior is converted into structured, machine-readable trace signals.

In the **AI Search Trace Receipt Standard**, encoding does not merely mean storing data as binary digits.

The important step is to convert AI search behavior into a defined code system.

This allows an AI search event to leave a verifiable trace without preserving the raw query, raw answer, full browsing history, or personal identifiers.

---

## Core Idea

AI search should not be fully recorded.

Instead, it should be:

```text
sampled
  → classified
    → encoded
      → minimized
        → preserved as a trace receipt
```

The Encoding Model turns search behavior into fields such as:

* `intent_code`
* `source_class_codes`
* `transformation_code`
* `confidence_bucket`
* `action_code`
* `privacy_level`
* `retention_policy`

These fields are machine-readable signals.

They are not intended to reconstruct the private query or the full generated answer.

---

## Conceptual Flow

```text
AI Search Event
  → Sampling Decision
    → Signal Extraction
      → Structured Encoding
        → Fingerprinting / Digesting
          → Privacy Boundary
            → Integrity Hash
              → Trace Receipt
```

A simpler version:

```text
Search behavior
  → Sampled signal
    → Classified event
      → Encoded field
        → Minimized receipt
```

---

## Encoding vs. Raw Recording

A raw recording attempts to preserve the original event.

For AI search, that would mean storing:

* The full user query
* The full AI answer
* The full list of visited or retrieved sources
* Exact timestamps
* User identity or session identity
* Detailed behavioral history

This standard rejects that approach.

Instead, it uses structured encoding.

Structured encoding records only the minimum signals needed to describe the event at a high level.

```text
Raw recording:
  What exactly did the user ask?

Structured encoding:
  What kind of search event occurred?
```

```text
Raw recording:
  What exact answer did the AI generate?

Structured encoding:
  What kind of transformation was performed, and what is the digest of the result?
```

```text
Raw recording:
  Which exact private behavior happened over time?

Structured encoding:
  What minimized trace fields can support later audit without reconstructing private thought?
```

---

## Encoded Fields in v0.1

The following fields represent the initial Encoding Layer in v0.1.

| Search Behavior   | Encoded Field                      | Purpose                                      |
| ----------------- | ---------------------------------- | -------------------------------------------- |
| Search intent     | `query_trace.intent_code`          | Describes the category of the search         |
| Source category   | `source_trace.source_class_codes`  | Describes the type of sources touched        |
| AI transformation | `answer_trace.transformation_code` | Describes how information was transformed    |
| Confidence range  | `answer_trace.confidence_bucket`   | Describes the broad confidence level         |
| User reaction     | `user_action_trace.action_code`    | Describes a minimized user action signal     |
| Sampling decision | `sampling.sampled`                 | Describes whether this event was sampled     |
| Privacy status    | `privacy.privacy_level`            | Describes the privacy treatment              |
| Retention rule    | `privacy.retention_policy`         | Describes how long the trace may be retained |

---

## Example Encoding Object

The optional `encoding` object may be used to declare the encoding model used by a receipt.

```yaml
encoding:
  encoding_model: "codebook_based"
  codebook_version: "0.1.0"
  binary_representation: "implicit"
  raw_signal_policy: "not_stored"
```

### Field Meanings

#### `encoding_model`

Defines the type of encoding model used.

Initial values may include:

```text
codebook_based
hash_based
hybrid
```

* `codebook_based` means behavior is mapped into predefined codes.
* `hash_based` means signals are primarily represented through non-reversible hashes or digests.
* `hybrid` means both codebook fields and hashes are used.

#### `codebook_version`

Identifies the version of the codebook used for classification.

Example:

```text
0.1.0
```

This allows code meanings to evolve over time without breaking older receipts.

#### `binary_representation`

Defines whether binary representation is explicit or implicit.

Initial values:

```text
implicit
explicit
```

* `implicit` means fields are encoded as structured values, and binary representation is handled by storage or transport systems.
* `explicit` means the standard directly defines binary codes or bit-level representations.

In v0.1, `implicit` is recommended.

#### `raw_signal_policy`

Defines how raw signals are treated.

Initial values:

```text
not_stored
minimized
review_required
```

* `not_stored` means raw query and raw answer data are not stored.
* `minimized` means only reduced signals are retained.
* `review_required` means additional governance review is needed before storage or processing.

---

## Codebook-Based Encoding

A codebook-based model maps search behavior into controlled values.

Example:

```yaml
query_trace:
  intent_code: "technical_research"
```

This does not reveal the raw query.

It only indicates that the search event belongs to a technical research category.

Another example:

```yaml
answer_trace:
  transformation_code: "synthesis"
```

This does not preserve the generated answer.

It only indicates that the AI performed a synthesis operation.

---

## Initial Code Fields

### `intent_code`

Represents the broad intent of the search.

Initial values:

```text
general_question
news_check
technical_research
academic_research
product_comparison
legal_policy_check
medical_health_info
creative_support
code_research
unknown
```

### `source_class_codes`

Represents the broad type of sources touched.

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

### `transformation_code`

Represents the type of transformation performed by the AI.

Initial values:

```text
direct_answer
summary
comparison
synthesis
translation
extraction
classification
unknown
```

### `confidence_bucket`

Represents a broad confidence range.

Initial values:

```text
low
medium
high
unresolved
```

### `action_code`

Represents a minimized user action signal.

Initial values:

```text
none
clicked_source
refined_query
saved_answer
shared_answer
rejected_answer
requested_correction
```

### `privacy_level`

Represents the privacy treatment of the receipt.

Initial values:

```text
minimized
aggregated
anonymized
review_required
```

### `retention_policy`

Represents the expected retention behavior.

Initial values:

```text
short_term
aggregated_only
delete_after_audit
unspecified
```

---

## Binary Representation

This standard recognizes that all digital data is ultimately represented in binary form by computing systems.

However, that is not the main meaning of encoding in this specification.

The important distinction is:

```text
Binary storage:
  Data is represented as 0 and 1 internally.

Structured encoding:
  Search behavior is mapped into defined fields and controlled codes.
```

In v0.1, binary representation is considered **implicit**.

This means the standard defines the structured code fields, while storage systems handle the underlying binary representation.

Future versions may define explicit bit-level representations if needed.

---

## Fingerprints and Digests

Encoding may be combined with non-reversible fingerprints and digests.

Examples:

```yaml
query_trace:
  query_fingerprint: "simhash:ab82f91c"
```

```yaml
answer_trace:
  answer_digest: "sha256:7c9e4f91a2b3c"
```

```yaml
source_trace:
  source_fingerprints:
    - "domain_hash:38fa91"
    - "repo_hash:aa72ef"
```

These values help preserve verifiability without storing raw content.

---

## Encoding and Privacy

The Encoding Model supports the privacy boundary of the standard.

A valid receipt must not use encoded fields as a disguised way to store private content.

For example, an encoded field should not contain:

* Raw query text
* Raw answer text
* Full URLs with personal parameters
* Email addresses
* Account identifiers
* Exact private behavioral timelines
* Sensitive personal content

The encoding layer exists to reduce private exposure, not to hide surveillance inside technical fields.

---

## Trace Receipt vs. Thought Capture

The Encoding Model helps enforce the distinction between trace receipts and thought capture.

A trace receipt should answer:

```text
What kind of AI search event occurred?
Was it sampled?
What type of sources were touched?
What kind of transformation occurred?
Can the receipt be verified later?
```

A trace receipt should not answer:

```text
What exactly did the user think?
What private wording did the user use?
What full answer did the user receive?
What exact behavioral sequence can identify the user?
```

This is the boundary.

---

## Example Receipt Fragment

```yaml
sampling:
  sampled: true
  sampling_method: "risk_based"
  sampling_rate_hint: 0.1

encoding:
  encoding_model: "codebook_based"
  codebook_version: "0.1.0"
  binary_representation: "implicit"
  raw_signal_policy: "not_stored"

query_trace:
  query_fingerprint: "simhash:ab82f91c"
  intent_code: "technical_research"
  sensitivity_bucket: "low"

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

answer_trace:
  answer_digest: "sha256:7c9e4f91a2b3c"
  confidence_bucket: "medium"
  transformation_code: "synthesis"

user_action_trace:
  action_code: "refined_query"
```

This fragment shows the basic role of the Encoding Model:

```text
A search event happened.
The raw query was not stored.
The raw answer was not stored.
The event was classified.
The event was minimized.
The receipt remains machine-readable.
```

---

## Version 0.1 Boundary

In v0.1, the Encoding Model is intentionally simple.

It defines:

* Controlled code fields
* Broad buckets
* Optional encoding object
* Implicit binary representation
* Raw signal non-storage
* Privacy-preserving machine readability

It does not yet define:

* Full binary serialization
* Cross-agent encoding propagation
* Royalty weighting codes
* Contribution graph encoding
* Model-specific internal trace codes
* Fine-grained behavioral telemetry

These may be considered in later versions.

---

## Summary

The Encoding Model is the layer that turns AI search behavior into a receipt.

It does not record private thought.

It does not preserve the full conversation.

It does not reconstruct the user’s search history.

It converts search behavior into minimized, structured, verifiable signals.

```text
Search happened.
Signals were sampled.
Behavior was classified.
Fields were encoded.
Raw content was not stored.
The receipt can be verified.
```

That is the role of the Encoding Model.
