# Harness Code Style Guidance

Major components are selected in [Decision 0005](../docs/decisions/0005-preserve-selected-component-direction.md); detailed implementation choices remain open. These rules apply once code is introduced.

## General

- Prefer clear, boring code over clever abstractions.
- Keep provider-specific code isolated behind interfaces.
- Keep model prompts and schemas close to the graph node that uses them.
- Treat fixture data as part of the test surface.
- Avoid adding dependencies until they solve a concrete problem.

## TypeScript Preference

TypeScript is the likely default unless a decision record chooses another stack.

If TypeScript is used:

- Prefer explicit domain types for workflow state and provider boundaries.
- Use schema validation for model outputs and external provider payloads.
- Keep tests close to the behavior they verify.

## Comments

Use comments sparingly. Explain why something is non-obvious, not what the syntax already says.
