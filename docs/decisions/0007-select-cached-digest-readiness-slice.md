# 0007: Select Cached Digest Display And Source Verification

## Status

Accepted for readiness planning by the product owner on 2026-10-12. Formal specification writing remains unauthorized.

## Context And Provenance

After approving [clearly canceled dated-event display](0006-display-clearly-canceled-dated-events.md), the owner replied `1` to the next-step choices, selecting **cached digest display and source verification** as the first specification slice for readiness review. This selection uses accepted product requirements, independently of historical experiments.

## Decision

Prepare readiness for household/child views of already extracted items, date placement and rollover, uncertainty, source evidence, and clearly canceled dated events. Preserve existing access and relevance rules as constraints on displayed data.

Inbox ingestion, setup, authentication mechanics, correction learning, and unresolved cancellation cases remain outside this slice. Readiness review must identify dependencies that cannot safely remain outside rather than silently extending scope or inventing fallback behavior.

## Consequences

- The [slice readiness review](../product/cached-digest-readiness.md) maps accepted rules to existing scenario evidence and identifies missing decisions or validation coverage.
- Selection is not a claim of readiness or a new product behavior decision.
- Owner review actions, category decisions, and correction processing remain separate workflow dependencies; their accepted MVP capabilities are not removed.
- Formal specs, mocks, implementation, new experiments, skill creation, and Git mutations still require separate authorization.
