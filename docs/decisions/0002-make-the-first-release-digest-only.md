# 0002: Make The First Release Digest-Only

## Status

Accepted

## Context

The generalized pilot persona manually reviews a high volume of school email and adds noticed dates to a shared calendar. Important events can be noticed too late. Calendar automation could reduce manual work, but it would add calendar authorization, review policy, deduplication, correction, and reminder behavior before the core email-filtering value has been proven.

## Decision

The first release will provide a read-only, date-aware digest of relevant school information. It should reduce the need to read individual school emails and surface upcoming obligations with role-specific details when available.

The first release will not connect to calendars, create or update calendar events, send calendar-based reminders, or deliver proactive notifications. Calendar integration is the planned near-term second stage after the digest proves useful; notifications may follow without delaying the first release.

## Consequences

- The first release can focus on inbox connection, trusted sources, child-aware relevance, extraction, and digest quality.
- Upcoming information must remain useful relative to the current date within the digest itself.
- The product still depends on the user to transfer information to a calendar when desired.
- Event extraction should preserve the evidence and role-specific details that a near-term calendar integration will need, without turning those details into formal calendar candidates in the first release.
- The first digest surface is a date-aware web app view with background checks every four hours and an on-demand inbox check. Opening the app shows cached data without itself triggering a check; daily email and near-real-time background fetching are not defaults. The four-hour cadence is operationally configurable rather than a user-facing v1 setting.
- Qualitative pilot usefulness criteria are confirmed. Remaining workflow decisions and representative synthetic acceptance examples must be completed before formal specification or implementation; see the Version 0 trial snapshot.
