# 0010: Suppress Ongoing Label For Canceled Ranges

## Status

Accepted by the product owner on 2026-10-12.

## Context And Provenance

Example K4 in the [cached-digest acceptance examples](../product/cached-digest-acceptance-examples.md#clear-cancellations) exposed ambiguity: a clearly canceled range spanning today meets ordinary current/upcoming placement, but `Ongoing` could suggest that the event is happening.

The owner replied `1` to approve **show `Canceled` without `Ongoing`**. The alternative was `Canceled` plus a secondary explanation such as `Scheduled range includes today`. This approval comes directly from the owner.

## Decision

For a clearly canceled dated event range spanning today, show prominent `Canceled` without `Ongoing`. Keep one item in current/upcoming under ordinary eligibility, preserve the complete scheduled date range and supporting evidence, and apply ordinary emphasis and history rules.

The authoritative rule lives in [Date-Aware Digest](../product-requirements.md#date-aware-digest).

## Limits

This changes label treatment only. It does not alter date-window overlap, deletion or retention policy, or the selected slice's excluded cancellation cases. It does not authorize a formal specification, mock, implementation, experiment, skill creation, or Git mutation.
