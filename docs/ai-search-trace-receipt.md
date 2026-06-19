# AI Search Trace Receipt

## Purpose

AI Search Trace Receipt defines a minimal structure for recording AI-mediated search events.

It is not a search history archive.

It is a privacy-preserving receipt that records only the minimum trace signals needed for later audit, attribution, reflection, or value-circulation systems.

## What This Standard Records

This standard may record:

- trace ID
- rounded timestamp bucket
- sampling status
- query fingerprint
- intent code
- source fingerprints
- citation count
- answer digest
- confidence bucket
- transformation code
- user action signal
- privacy boundary
- integrity hash
- optional future hooks

## What This Standard Must Not Record

This standard must not record:

- raw user query
- raw AI answer
- full browsing history
- personally linked identifier
- exact behavioral timeline
- sensitive personal content

## Conceptual Model

```text
Search Event
  → Sample
    → Fingerprint
      → Digest
        → Minimize
          → Hash
            → Receipt
Trace, Not Surveillance

The key distinction is:

Surveillance log:
  Who searched what, exactly, when, and where?

Trace receipt:
  A search event occurred, a minimized fingerprint was produced,
  sources were touched in hashed form, and the resulting answer
  has a digest.

The first is behavioral capture.

The second is structural evidence.

v0.1 Scope

Version 0.1 covers only AI search events.

It does not yet define:

generation trace receipts
contribution graphs
royalty weighting
payment hooks
full memory integration
cross-agent trace propagation

These are reserved for later versions.


---

# docs/privacy-boundary.md

```md
# Privacy Boundary

## Core Rule

Kazene Trace Receipt Protocol v0.1 is built on the principle of privacy minimization.

The protocol should preserve structural evidence while avoiding behavioral surveillance.

## Required Privacy Constraints

Every valid AI Search Trace Receipt must declare:

```yaml
raw_query_stored: false
raw_answer_stored: false
personal_id_linked: false

These values are not optional.

They define the boundary between a trace receipt and a surveillance log.

Timestamp Buckets

Precise timestamps should be avoided.

Recommended examples:

2026-06-19T15:00+09:00
2026-06-19
2026-W25

The goal is to support auditability without reconstructing a precise behavioral timeline.

Query Fingerprints

A query fingerprint should be non-reversible.

Acceptable approaches may include:

cryptographic hash
semantic hash
locality-sensitive hash
categorized intent code
aggregated statistical signature

The raw query text should not be stored inside the receipt.

Source Fingerprints

Source fingerprints should avoid exposing a complete browsing trail.

They may represent:

hashed domain
hashed repository
hashed document ID
source class code
aggregated source category
Retention

Retention should be short, purpose-bound, or aggregated.

Recommended policies:

short_term
aggregated_only
delete_after_audit
unspecified

Long-term storage of trace receipts should require additional governance review.
