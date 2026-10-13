# 0005: Preserve Selected Component Direction

## Status

Accepted direction; restored during documentation reconciliation on 2026-10-04.

## Context

The product owner selected major components before the Version 0 workshop. The workshop preservation pass incorrectly weakened them to unselected proposals. [R6](../product/requirements-workshop-v0-review.md#r6-entry-point-status-and-authoritative-stack-direction-need-reconciliation) records that mismatch; the owner explicitly requested restoration during reconciliation.

## Decision

Use React for the first web surface, a backend API, and Postgres. Add React Native later, once the web workflow and API contracts are stable. LangGraph coordinates AI workflows; application services control provider access and side effects.

## Consequences

Component selection does not select a backend framework, detailed database schema, authentication vendor, session policy, deployment topology, or hosting provider. Those remain open. Mobile delivery and calendar integration remain outside the first digest release. This record restores existing direction; it does not authorize OpenSpec or application implementation.
