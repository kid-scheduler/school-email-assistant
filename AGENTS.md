# AGENTS.md

This is the entry point for AI agents and human contributors working in School Email Assistant. Keep this file short; follow links into `.harness/` and `docs/` when a task needs more detail.

## Project Purpose

School Email Assistant helps parents turn school inbox noise into trusted daily summaries. The first surface may summarize important dates and events; formal calendar candidates are a second-stage capability.

The product should help users:

- Connect school-related inboxes and calendars.
- Approve trusted school senders.
- Configure child-specific topics and preferences.
- Receive daily summaries of relevant messages.
- Include important dates/events in the digest, but defer formal calendar candidates until the first digest-focused surface is useful.

## Current Operating Mode

Requirements and harness setup.

We are not implementing application functionality yet. Current work should improve requirements, specs, documentation, fixtures, mocks, and harness guidance.

## Essential Rules

- Keep the public repository self-contained and publishable.
- Do not reference private local paths, private prototype details, real school emails, real student names, credentials, or account identifiers.
- Keep project state in Markdown when decisions, risks, open questions, or current status change.
- Update product docs, architecture docs, and decision logs when implementation changes make them stale.
- Prefer deterministic scripts for formatting, linting, tests, fixture replay, and mechanical generation.
- Use progressive disclosure: read deeper docs only when the task needs them.
- Keep app-specific fixtures and acceptance tests in this repository, not in the generic harness repo.

## Code Style Essentials

No application stack has been selected yet.

When code is introduced:

- Prefer TypeScript unless a spec or decision record chooses otherwise.
- Keep provider-specific APIs behind provider-neutral interfaces.
- Keep model/AI calls typed, auditable, and testable.
- Add comments only where they explain non-obvious decisions.

For deeper guidance, see `.harness/code-style.md`.

## Architecture Essentials

- LangGraph should coordinate AI workflow state and routing.
- Provider APIs, OAuth, persistence, and calendar writes should remain ordinary application services around the graph.
- Calendar writes are out of scope for the first product surface and must be validation- and review-gated when introduced later.
- Static HTML mocks should define user-facing workflow expectations before backing functionality is built.

For deeper guidance, see `.harness/architecture.md`.

## Quality Gates

Before considering work complete, run the relevant checks listed in `.harness/quality-gates.md`.

If a check cannot run, record why in the final response or handoff.

## Workflows

Use `.harness/workflows.md` for common work patterns.

## Living Docs

Durable product and implementation knowledge should live in:

- `docs/product/`
- `docs/architecture/`
- `docs/decisions/`
- `docs/implementation/`

## Safety And Privacy

Use synthetic examples by default. Do not commit raw school emails, private inbox/calendar screenshots, credentials, tokens, provider account IDs, or personal student information.
