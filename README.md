# School Email Assistant

School Email Assistant helps parents turn school inbox noise into a daily, child-aware summary and a reliable calendar of events they actually care about.

This is a fresh implementation intended to stand on its own as a public project.

## Project Direction

The product will use LangGraph to coordinate email processing workflows with explicit state, deterministic validation, human review points, and auditable calendar decisions. Provider access, OAuth, persistence, and calendar writes should remain ordinary application services around the graph.

## Documentation

Planning documents live in [docs](./docs/README.md):

- [Agent Guidance](./AGENTS.md)
- [Product Requirements](./docs/product-requirements.md)
- [Product Overview](./docs/product/overview.md)
- [Architecture](./docs/architecture.md)
- [Architecture Overview](./docs/architecture/overview.md)
- [LangGraph Workflows](./docs/langgraph-workflows.md)
- [Data Model](./docs/data-model.md)
- [Development Harness](./docs/development-harness.md)
- [Current State](./docs/implementation/current-state.md)
- [Open Questions](./docs/open-questions.md)

## Initial Priorities

1. Finalize the documentation and project boundaries.
2. Refine the generic agent development harness in a separate repository.
3. Keep app-specific fixtures and tests in this repository.
4. Build the first read-only LangGraph email-processing workflow.
5. Include important dates/events in the digest, while deferring formal calendar candidates and writes to a second product stage.
