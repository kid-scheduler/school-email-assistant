# 0006: Display Clearly Canceled Dated Events

## Status

Accepted by the product owner on 2026-10-12.

## Context And Provenance

Cancellation display was unresolved after requirements reconciliation. In the requirements conversation, the owner first replied `1` to select cancellation display as the next definition activity. The owner then replied `1` to approve keeping a clearly canceled dated event at its scheduled date with a prominent `Canceled` label, rather than moving it to a separate canceled-events section.

## Decision

For a dated event that approved-source email body information clearly identifies as canceled, keep the event at its scheduled date with a prominent `Canceled` label. Preserve its scheduled date/range and supporting evidence, and apply ordinary upcoming/history display eligibility. Make cancellation clear rather than presenting the event as an active commitment.

The authoritative display rule lives in [Date-Aware Digest](../product-requirements.md#date-aware-digest).

## Scope And Consequences

- Users can find the cancellation where they expect to find the event; no separate canceled-events section or new display window is introduced.
- This decides digest display, not data deletion or storage retention.
- Cancellations without a usable date, uncertain event matches, reinstatement, and cancellation of a separate action remain questions for scope review. Existing uncertainty, conflict, and evidence requirements continue to apply; this decision does not supply missing answers.
- No first specification slice, formal specification, mock, implementation, experiment, skill creation, or Git mutation is authorized.
