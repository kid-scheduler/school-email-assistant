# Data Model

## Proposal Status

This inherited conceptual model is preserved for the [Version 0 trial](product/requirements-workshop-v0.md), not accepted as a formal schema. Owner/viewer roles, multiple-child category and event assignments, and date-aware cached digests require reconciliation before specification. Calendar entities/policies are future-stage proposals; delivery fields do not imply proactive email in v1. Retention and credential storage remain unresolved.

## Proposed Core Entities

### Account

Owns users, children, sources, provider connections, topics, and digest policy.

### User

Represents a parent or guardian who can configure sources, review candidates, and receive digests.

### Child

Represents a child-specific context.

Suggested fields:

- `id`
- `accountId`
- `displayName`
- `schoolName`
- `grade`
- `aliases`
- `active`

### Provider Connection

Represents an external email or calendar integration. Email and calendar connections should be separate so users can read from one provider and write events to another.

Suggested fields:

- `id`
- `accountId`
- `provider`
- `capability`: `EMAIL_READ` or `CALENDAR_WRITE`
- `email`
- `credentials`
- `status`
- `createdAt`
- `updatedAt`

### Trusted Source Rule

User-approved rule describing which senders the system may process. Rules are configured per household and may differ across schools and communication systems.

Suggested fields:

- `id`
- `accountId`
- `providerConnectionId`
- `type`: `EMAIL_ADDRESS` or `DOMAIN` initially; future evidence may add `ADDRESS_PATTERN` or `STABLE_SENDER_ID`
- `value`
- `displayName`
- `scopeLabel`: user-facing school, district, or platform context
- `status`: `SUGGESTED`, `APPROVED`, `REJECTED`, `DISABLED`
- `approvedByUserId`
- `notes`

### Topic Rule

A natural-language preference or interest area explicitly assigned to one or multiple children. Category preferences have no implicit household-wide scope. The existing suggested fields below must be reconciled with this product decision before formal specification.

Suggested fields:

- `id`
- `accountId`
- `childId`
- `name`
- `description`
- `includeExamples`
- `excludeExamples`
- `calendarPolicy`
- `status`

### Email Message

Stores provider-stable metadata and normalized content.

Suggested fields:

- `id`
- `accountId`
- `providerConnectionId`
- `providerMessageId`
- `threadId`
- `sourceId`
- `subject`
- `from`
- `to`
- `sentAt`
- `receivedAt`
- `textBody`
- `htmlBody`
- `contentHash`

### Graph Run

Persists one workflow execution.

Suggested fields:

- `id`
- `accountId`
- `workflowName`
- `workflowVersion`
- `status`
- `input`
- `state`
- `startedAt`
- `completedAt`
- `error`

### Extracted School Item

Structured result from a processed email.

Suggested fields:

- `id`
- `accountId`
- `emailMessageId`
- `childId`
- `topicRuleId`
- `type`: `SUMMARY`, `ACTION`, `DEADLINE`, `EVENT`
- `title`
- `summary`
- `dueAt`
- `confidence`
- `evidence`
- `status`

### Calendar Event Candidate

Validated candidate before or after calendar write.

Suggested fields:

- `id`
- `accountId`
- `emailMessageId`
- `childId`
- `topicRuleId`
- `title`
- `description`
- `location`
- `startsAt`
- `endsAt`
- `timezone`
- `allDay`
- `confidence`
- `validationStatus`
- `dedupeKey`
- `approvalStatus`

### Calendar Event Link

Maps local candidates to provider calendar events.

Suggested fields:

- `id`
- `accountId`
- `calendarConnectionId`
- `calendarEventCandidateId`
- `providerEventId`
- `status`
- `lastSyncedAt`

### Review Item

Represents something the user must decide.

Suggested fields:

- `id`
- `accountId`
- `type`
- `subjectId`
- `status`
- `decision`
- `decisionByUserId`
- `decidedAt`

### Digest

Represents a daily digest window and rendered output.

Suggested fields:

- `id`
- `accountId`
- `windowStart`
- `windowEnd`
- `status`
- `renderedSummary`
- `sentAt`

## Relationships

```mermaid
erDiagram
  ACCOUNT ||--o{ USER : has
  ACCOUNT ||--o{ CHILD : has
  ACCOUNT ||--o{ PROVIDER_CONNECTION : connects
  ACCOUNT ||--o{ TRUSTED_SOURCE : approves
  CHILD ||--o{ TOPIC_RULE : has
  PROVIDER_CONNECTION ||--o{ EMAIL_MESSAGE : fetches
  TRUSTED_SOURCE ||--o{ EMAIL_MESSAGE : matches
  EMAIL_MESSAGE ||--o{ GRAPH_RUN : processed_by
  EMAIL_MESSAGE ||--o{ EXTRACTED_SCHOOL_ITEM : yields
  EXTRACTED_SCHOOL_ITEM ||--o{ CALENDAR_EVENT_CANDIDATE : may_create
  CALENDAR_EVENT_CANDIDATE ||--o| CALENDAR_EVENT_LINK : syncs_to
  ACCOUNT ||--o{ DIGEST : receives
  DIGEST ||--o{ EXTRACTED_SCHOOL_ITEM : includes
```
