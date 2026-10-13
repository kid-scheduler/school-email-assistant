# 0008: Distinguish Empty Digest Check History

## Status

Accepted by the product owner on 2026-10-12.

## Context And Provenance

During readiness review of the [selected cached-display slice](0007-select-cached-digest-readiness-slice.md), the owner replied `1` to approve distinguishing the reason for an empty digest. The alternative was a single `No items to show` message with separate check history. This decision comes from the owner in the requirements conversation.

## Decision

For a digest with no currently displayable items, use a contextual empty message that distinguishes:

- `No successful inbox check yet` when no check has succeeded.
- `No relevant items in the current display windows` after a successful check.

Keep existing check-status and last-success information visible, including any later failure. Exact copy and layout can be validated later while preserving this distinction. The authoritative rule lives in [Date-Aware Digest](../product-requirements.md#date-aware-digest).

## Consequences And Limits

- An empty view communicates its relationship to check history without implying there are no school obligations or claiming information is current after a failed check.
- This does not expand coverage, change check triggers, discard cached items, or resolve pending review/category items.
- Acceptance examples remain to be documented and reviewed; this is not UI validation.
- Formal specification writing, mocks, implementation, new experiments, skill creation, and Git mutations remain unauthorized.
