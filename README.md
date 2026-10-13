# School Email Assistant

School Email Assistant helps parents turn school inbox noise into a date-aware, child-aware digest by identifying what matters and ignoring what does not apply to their children. Calendar integration is planned soon after the digest proves useful.

This is a fresh implementation intended to stand on its own as a public project.

The Version 0 checkpoint is merged; documentation reconciliation is complete. See [review status](docs/product/requirements-workshop-v0-review.md#reconciliation-status). No application functionality has been implemented; the workshop snapshot is not a formal specification or implementation approval.

## Project Direction

The product will use LangGraph to coordinate email processing workflows with explicit state, deterministic validation, human review points, and auditable calendar decisions. Provider access, OAuth, persistence, and calendar writes should remain ordinary application services around the graph.

## Documentation

Planning documents live in [docs](./docs/README.md):

- [Agent Guidance](./AGENTS.md)
- [Product Requirements](./docs/product-requirements.md)
- [Product Overview](./docs/product/overview.md)
- [Accepted MVP Definition](./docs/product/mvp-definition.md)
- [Accepted Slice Readiness](./docs/product/cached-digest-readiness.md)
- [Architecture](./docs/architecture.md)
- [Architecture Overview](./docs/architecture/overview.md)
- [LangGraph Workflows](./docs/langgraph-workflows.md)
- [Data Model](./docs/data-model.md)
- [Development Harness](./docs/development-harness.md)
- [Current State](./docs/implementation/current-state.md)
- [Open Questions](./docs/open-questions.md)

## Current Scope

Requirements reconciliation is complete, and the owner accepted documentation readiness for [cached digest display and source verification](docs/product/cached-digest-readiness.md). Formal specification writing, mocks, implementation, and new experiments remain deferred and require separate authorization.
