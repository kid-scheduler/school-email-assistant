# Project Harness: School Email Assistant

## Product Goal

Build a read-only, date-aware web digest from approved-source bodies in the pilot inbox. Calendar integration follows later.

## Current Phase

Documentation reconciliation and harness setup. Current scope stops before OpenSpec, application implementation, or skill creation; see [review status](../docs/product/requirements-workshop-v0-review.md#reconciliation-status).

## Primary User

A parent or guardian who receives school-related emails and wants help identifying relevant messages, required actions, deadlines, and events.

## Product Constraints

- The system must be trustworthy before it is automated.
- Users must approve trusted sources.
- Calendar writes must be review-gated until the product explicitly supports safer automation.
- Every AI-derived decision should be explainable with source evidence.
- Fixtures and examples must be synthetic or safely sanitized.

## Harness Constraints

- Public project docs should not depend on private project history.
- Keep durable state in Markdown.
- Use OpenSpec for behavior/change proposals when the project reaches the MVP definition stage.
- Use static HTML mocks as executable UI specs before implementation.
- Use deterministic scripts for checks that scripts can perform reliably.
