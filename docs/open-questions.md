# Open Questions

## Product

- What is the first target user flow: Outlook-only read-only summaries, or full Outlook-to-calendar automation?
- Should the daily digest be delivered by email first, or simply exposed through an API/frontend?
- How much user review is required before the first calendar event can be created?
- Should topics be per child by default, or can some topics apply to all children?
- What should happen when an email seems relevant to multiple children?

## Providers

- Which provider comes first after Outlook email: Outlook Calendar, Gmail, or Google Calendar?
- Should email polling be enough for the first version, or should provider webhooks be included early?
- What OAuth scopes are acceptable for the initial product?
- How will tokens be encrypted and rotated?

## AI And Workflow

- Which model should be used for classification and extraction?
- Should embeddings be used for topic matching, or should topic rules start with structured model classification only?
- What confidence thresholds should route to auto-add versus approval?
- How much source evidence should be stored for each model decision?
- How will regression fixtures be curated from real school emails without leaking private content?

## Data And Architecture

- Should `Inbox` evolve into a generalized `ProviderConnection`, or should a new entity be introduced alongside it?
- Should LangGraph state be persisted in first-class tables, serialized JSON, or both?
- Should the graph run in the API process initially, or in a separate worker from day one?
- What frontend will manage connected accounts, source approval, topic preferences, and review queues?

- What package name and public repository name should the project use before implementation expands?
