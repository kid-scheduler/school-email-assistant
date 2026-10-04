# Open Questions

## Product

- How should received-date estimates combine temporal labels and `Needs review` routing? See [C1](product/requirements-reconciliation-review.md#c1-estimated-date-labels-and-review-routing).
- How should cached digest placement reflect household-local date changes without an inbox check, including a view left open across midnight? See [C2](product/requirements-reconciliation-review.md#c2-calendar-day-transitions-versus-cached-rendering).
- Cancellation display is unresolved. Keeping the event at its original date with a `Canceled` label was proposed but not accepted; no retention/display rule is confirmed.
- Which additional synthetic acceptance cases and UI workflow checks are needed before formal specification? Reconciliation is documentation-only.
- What should happen to retained messages, excerpts, and household data when an inbox is disconnected or a household is deleted?

## Providers

- Which authentication provider should support one-time email-code sign-in? Auth0 is under consideration but has not been selected.
- What session lifetime and sign-in code expiry/resend behavior should be used?
- How should expired, resent, or wrong-address household invitations be handled?
- When should Gmail ingestion be added after the Outlook/Hotmail pilot?
- Are school-managed student inboxes technically and administratively connectable, and should the product ask a parent or student to authorize them?
- What OAuth scopes are acceptable for the initial product?
- How will tokens be encrypted and rotated?

## Planned Calendar Stage

- Should a later release propose calendar events for review or create them automatically under user-defined policies?
- How much user review should be required before the first calendar event can be created?
- Should existing calendar content eventually inform the digest or only help prevent duplicate event creation?

## Future History Setting

- Which history periods should users be offered, who may change them, and should the setting also change `Past due date` history? The first release stays fixed at seven days; see [B3a](product/reconciliation-scenarios.md#date-range-boundaries-r5).

## Future Notifications

- Should notifications eventually come from a browser/PWA, a native mobile app, or both?
- Which changes are important enough to notify about rather than waiting for the user to open the digest?

## Future Shared Categories

- How should discovered categories be generalized and reviewed before sharing them across households without exposing private details?

## AI And Workflow

- Which model should be used for classification and extraction?
- Should embeddings be used for topic matching, or should topic rules start with structured model classification only?
- What criteria distinguish confident relevance, confident irrelevance, and `Needs review` in the digest? Calendar auto-add thresholds are a separate future-stage decision.
- How much source evidence should be stored for each model decision, and for how long?
- How will same-event matching and contextual correction learning be validated against synthetic cases?
- How will regression fixtures be curated from real school emails without leaking private content?

## Data And Architecture

- Should `Inbox` evolve into a generalized `ProviderConnection`, or should a new entity be introduced alongside it?
- Should LangGraph state be persisted in first-class tables, serialized JSON, or both?
- Should the graph run in the API process initially, or in a separate worker from day one?
- Which backend framework, web tooling, hosting provider, and deployment topology should implement the [selected components](decisions/0005-preserve-selected-component-direction.md)?
- How should the reconciled [conceptual relationships](data-model.md#relationships) and [digest workflow](langgraph-workflows.md#email-processing-graph) map to physical schemas and validated processing contracts?
- What package name and public repository name should the project use before implementation expands?
