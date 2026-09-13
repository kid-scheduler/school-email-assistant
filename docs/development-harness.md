# Development Harness

The generic development harness should live outside this repository. This repository should contain only School Email Assistant code, docs, domain fixtures, and domain-specific tests.

## Proposed Harness Repository

The generic harness should live in its own repository, for example `agent-dev-harness`.

## Relationship To This Project

The harness provides reusable working practices and tooling. School Email Assistant provides domain material.

Harness-owned examples:

- Task contract templates.
- Architecture decision templates.
- Sprint planning and handoff templates.
- Generic evaluator rubrics.
- Generic quality gate scripts.
- Repo adapters for common stacks.
- Agent operating guides.

School Email Assistant-owned examples:

- Sanitized school email fixtures.
- Provider-specific mock payloads.
- LangGraph workflow tests for school email classification.
- Calendar candidate fixtures.
- Product-specific acceptance criteria.
- Privacy and safety rules for family/school data.

## Principles

The harness should encode repeatable development behavior rather than product assumptions.

It should help agents and humans:

- Define the work before changing code.
- Preserve context across long-running efforts.
- Turn recurring mistakes into checks or guidance.
- Separate feedforward guidance from feedback sensors.
- Run deterministic checks before inferential review.
- Capture decisions as artifacts.
- Make project state inspectable and recoverable.

## First Integration Point

Once the harness repository exists, this project can add a lightweight local configuration layer, for example:

```text
.harness/
  project.md
  quality-gates.md
  workflows.md
```

Those files should describe how the generic harness applies to School Email Assistant without copying the harness itself into this repo.
