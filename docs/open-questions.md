# Open Questions

## Product

- Cancellation display is unresolved. Keeping the event at its original date with a `Canceled` label was proposed but not accepted; no retention/display rule is confirmed.
- Which representative synthetic acceptance cases and UI workflow checks are required before formal specification? Discovery is paused at the [Version 0 trial snapshot](product/requirements-workshop-v0.md).
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
- What frontend will manage connected accounts, source approval, topic preferences, and review queues?
- How should the inherited schema and workflow proposals be reconciled with multiple-child assignments, owner/viewer roles, and the digest-only body-analysis boundary?
- What package name and public repository name should the project use before implementation expands?
