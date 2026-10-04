# Harness Architecture Guidance

## Current Architecture Status

No application code exists. React web, React Native later, a backend API, and Postgres are selected; see [Decision 0005](../docs/decisions/0005-preserve-selected-component-direction.md). Detailed architecture remains provisional.

## Intended Boundaries

- API/service layer: account setup, provider connections, user preferences, review queues, digest access.
- Provider connectors: email and calendar provider APIs behind stable interfaces.
- Graph workflow: LangGraph state machine for classification, extraction, validation, review routing, and digest inclusion.
- Persistence: durable records for accounts, children, trusted sources, messages, graph runs, extracted items, event candidates, review items, and digests.
- UI: user-facing workflows validated first through static HTML mocks.

## Architecture Principles

- Keep AI decisions auditable.
- Keep side effects outside model calls.
- Validate extracted calendar candidates deterministically.
- Use human review for ambiguous, high-impact, or policy-gated actions.
- Separate email read connections from calendar write connections.
- Prefer provider-neutral domain shapes inside graph state.

## Decision Records

Record architecture decisions in `docs/decisions/`.
