# Architecture Overview

## Current State

No application code has been implemented yet. Architecture is currently documented as intended boundaries and workflow expectations.

## Expected System Shape

```mermaid
flowchart LR
  User["Parent / Guardian"] --> UI["Web UI"]
  UI --> API["API Service"]
  API --> DB["Database"]
  API --> Graph["LangGraph Workflow"]
  Graph --> Model["LLM / Structured Output"]
  Graph --> Email["Email Connectors"]
  Graph --> Calendar["Calendar Connectors"]
```

## Key Boundaries

- UI handles configuration, digest review, and approval flows.
- API handles account state, preferences, review queues, and persisted records.
- Graph handles workflow state and AI-assisted classification/extraction.
- Provider connectors hide external provider differences.
- Calendar writes require deterministic validation and policy checks.

## Links

- Product requirements: `docs/product-requirements.md`
- LangGraph workflows: `docs/langgraph-workflows.md`
- Data model: `docs/data-model.md`
