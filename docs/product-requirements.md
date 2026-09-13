# Product Requirements

## Problem

Parents receive a steady stream of school-related emails across multiple children, schools, activities, and systems. Important dates and required actions are mixed with fundraising, newsletters, announcements, and general noise. The product should help users choose the schools, senders, children, and topics they care about, then produce a daily summary and calendar updates for the relevant events.

## Goals

- Let a user connect one or more inboxes.
- Discover likely school-related senders from recent email.
- Let the user approve trusted sources instead of silently trusting AI decisions.
- Support child-specific profiles for school, grade, interests, ignore rules, and calendar policy.
- Classify incoming school email by child, source, topic, urgency, and actionability.
- Extract summaries, required actions, deadlines, and event candidates.
- Add or update calendar events when the user's policy allows it.
- Send a daily digest of relevant summaries, actions, and calendar activity.
- Collect user feedback so source and topic matching improves over time.

## Users

- Parents or guardians with one or more children in school.
- Families with a mix of elementary, middle, and high school communications.
- Users who receive school email through Gmail or Outlook and use Google Calendar or Outlook Calendar.

## Core User Journeys

### Connect Accounts

The user connects email providers separately from calendar providers. A user may read email from Outlook but write events to Google Calendar.

Required providers:

- Outlook email
- Outlook Calendar
- Gmail
- Google Calendar

### Choose School Sources

The system scans recent email and suggests likely school-related senders and domains. The user accepts, rejects, or edits the list.

Examples:

- A school domain
- A principal or teacher address
- ParentSquare or district announcement sender
- Activity-specific senders such as orchestra, athletics, counseling, or PTA

AI can rank and explain suggestions, but only user-approved sources should create downstream summaries or calendar events.

### Configure Children And Topics

Each child should have a profile:

- Name
- School
- Grade
- Relevant aliases or classroom labels
- Topics of interest
- Topics to ignore
- Calendar policy

Topics should be natural-language rules with examples, not only static keywords. For example, "Orchestra" can include concerts, rehearsals, call times, required attire, schedule changes, auditions, and parent meetings.

### Daily Digest

The daily digest should include:

- New relevant school messages
- Upcoming events found or updated
- Required actions and deadlines
- Items needing approval
- Ignored or low-confidence items only when the user asks to inspect them

### Calendar Automation

Calendar automation must be policy-driven:

- Summary only
- Ask before adding
- Auto-add high-confidence events
- Never add calendar events for this topic/source

Calendar writes should be reversible and auditable. Every created event should link back to the source email when the provider allows it.

## Functional Requirements

- Connect and refresh OAuth credentials per provider.
- Retrieve recent and new email from approved providers.
- Normalize HTML email into model-ready text while retaining source metadata.
- Store provider message IDs for deduplication.
- Support approved source lists by email address and domain.
- Classify messages against children, topics, and user preferences.
- Extract event candidates with start date, end date, title, location, description, confidence, and evidence.
- Validate date completeness and reject ambiguous calendar candidates.
- Detect duplicate events and event updates.
- Persist graph runs, decisions, extracted items, and user feedback.
- Generate a daily digest per account.

## Non-Goals For The First Implementation

- A free-roaming autonomous inbox agent.
- Silent calendar writes from unapproved sources.
- Reading every email in a user's mailbox indefinitely.
- Full frontend polish.
- Multi-tenant billing, organizations, or admin analytics.
- SMS or push notifications.

## Success Criteria

- A user can connect an Outlook inbox and approve school-related senders.
- The system can process recent approved-source email through a LangGraph workflow.
- The system can produce structured summaries, topic matches, and event candidates.
- Event candidates are validated and deduplicated before calendar writes.
- The daily digest can explain why each item was included.
- User feedback can update future source/topic behavior.
