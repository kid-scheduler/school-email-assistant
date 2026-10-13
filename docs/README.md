# School Email Assistant Documentation

School Email Assistant helps parents turn school inbox noise into a date-aware, child-aware digest of what matters. Calendar integration is the planned second stage after the digest proves useful.

This repository is the fresh implementation home. It is intended to stand on its own as a public project, with requirements, architecture, workflows, and product decisions recorded here.

## Document Map

- [Version 0 Trial Snapshot](./product/requirements-workshop-v0.md): paused workshop, public-safe persona, decision status, provisional defaults, and unresolved boundaries.
- [Agent Guidance](../AGENTS.md): the progressive-disclosure entry point for agents and contributors.
- [Product Requirements](./product-requirements.md): user goals, scope, policies, and non-goals.
- [Product Overview](./product/overview.md): durable product summary and current product boundary.
- [Accepted MVP Definition](./product/mvp-definition.md): accepted journey, boundaries, success criteria, and approval provenance.
- [Cached Digest Readiness](./product/cached-digest-readiness.md): owner-accepted documentation readiness, scope, and deferred dependencies.
- [Cached Digest Acceptance Examples](./product/cached-digest-acceptance-examples.md): synthetic display expectations under accepted rules.
- [Architecture](./architecture.md): proposed system boundaries, major services, and integration points.
- [Architecture Overview](./architecture/overview.md): current implementation architecture summary.
- [LangGraph Workflows](./langgraph-workflows.md): graph state, nodes, branching, and human-in-the-loop flow.
- [Data Model](./data-model.md): core entities and relationships.
- [Development Harness](./development-harness.md): how this project should relate to the future generic harness repo.
- [Decision Log](./decisions/): key product and architecture decisions, including the digest-first release boundary.
- [Current State](./implementation/current-state.md): implementation status, risks, and open questions.
- [Open Questions](./open-questions.md): decisions to resolve before implementation.

## Working Assumptions

- Users may receive school email in Gmail, Outlook, or both.
- Users may want events written to Google Calendar, Outlook Calendar, or both; calendar integration is the planned second stage and is not part of the first release.
- Email access and calendar write access should be separate OAuth connections.
- AI may suggest sources, topics, summaries, actions, deadlines, and important date/event mentions, but users remain the authority for what sources are trusted and what topics matter.
- Application code should access provider accounts and hand scoped, normalized content to AI for analysis; AI should not directly access user email accounts or credentials.
- Calendar writes require deterministic validation and deduplication before any event is created or updated.
- LangGraph should coordinate workflow execution; provider APIs, persistence, OAuth, and calendar writes should remain ordinary application services.

## Current Scope

Requirements reconciliation is complete, and the owner accepted documentation readiness for [cached digest display and source verification](product/cached-digest-readiness.md). Formal specification writing, mocks, implementation, and new experiments remain deferred and require separate authorization.
