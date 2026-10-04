# Product Overview

## Purpose

School Email Assistant helps parents turn school inbox noise into a trusted date-aware digest. It should identify what matters, ignore school items that do not apply to the user's children, and explain those choices. Formal calendar candidates are planned for a later stage.

Requirements discovery is paused at the [Version 0 trial snapshot](requirements-workshop-v0.md). This is a workshop record, not a formal specification or implementation approval.

## Core Promise

The product should help a parent know what matters, what requires action, and what can be safely ignored because it does not apply to their family, without giving automation more authority than it has earned.

Provider account access should stay inside the application. The product should fetch and scope email content through its own services, then hand normalized content to AI for analysis rather than letting an AI agent directly access a user's mailbox or credentials.

## Public-Safe Pilot Persona

The generalized pilot persona is a parent or guardian with children at different schools and educational stages. It preserves the requirements discovered with the product owner without documenting a real household's exact composition or account assignments.

Representative communication setup:

- School communication is spread across multiple household inboxes.
- Some messages arrive through a school platform; others come directly from teachers.
- Other household members may use personal or school-managed inboxes.
- The household manually maintains a shared calendar.

The selected pilot processes one owner-controlled personal Outlook/Hotmail inbox. Other inboxes, including Gmail and school-managed accounts, are deferred. The pilot cannot claim coverage for messages available only in those inboxes.

Invited household members, such as another guardian or a student, should each have a separate, read-only account that can view the digest without connecting an inbox. All authorized viewers may see the complete household digest. Viewers do not mark items as handled or change shared digest state in the first release.

### Current Workflow

In this persona's workflow, household members manually review school email and decide whether each message contains something important. Messages arrive through school communication platforms and directly from teachers. Noticed dates and commitments are manually added to a shared calendar.

The confirmed failure in this workflow is that important items are sometimes missed because the volume of school email makes consistent review difficult.

Generalized problem examples include:

- A school event is noticed too late to plan around.
- A required student activity fails to reach shared household awareness in time.
- An announcement does not clearly distinguish student arrival from audience start time.

These examples show two related needs: bringing relevant obligations to the family's attention early enough to act, and preserving role-specific details instead of collapsing several times into one generic event time.

### Worthwhile First-Release Outcome

Evaluate the first release after two weeks of normal use: the parent uses the digest as the main review surface, finds it less burdensome than checking individual emails, and experiences no surprises caused by the digest missing relevant events stated in approved-source email bodies in the connected inbox. No numeric time-saving baseline is required. Extend the pilot if too few events occur to judge coverage.

## Initial Product Shape

- Connect one owner-controlled inbox.
- Suggest likely school senders from the previous 90 days of message metadata.
- Let the user approve trusted sources.
- Let the owner add a missing trusted source at any time.
- Let the owner correct item relevance and child/category assignments, with corrections reflected in the digest and retained to improve future classification.
- Learn from corrections within the household, preserving their context; propose broader category-preference changes for owner approval.
- Configure children and topics.
- Process approved-source messages.
- Ignore irrelevant school items, such as events for another grade, class, club, sport, or child.
- Generate a single date-aware digest that reduces the need to read through individual school emails.
- Show supporting excerpts and source subject, sender, and received date; offer original-email links to the inbox owner where supported while letting household viewers read excerpts and metadata in the app.
- Retain relevant items that refer to external instructions and state the specific missing detail, such as `Arrival time not provided in email`, so users know what to check in the original.
- Apply clearly stated updates while retaining evidence; show unresolved conflicting details in `Needs review` with both source excerpts.
- Offer household and child-specific digest views to every authorized viewer. Shared events appear once in the household view and in each applicable child's view, preserving child-specific details.
- Let authorized household members view the digest.
- Give each household member a separate account rather than sharing one household login.
- Use passwordless one-time email-code sign-in with persistent sessions; let the owner invite viewers by email and revoke household access. Mailbox connection uses separate provider authorization. The auth provider is undecided; SMS codes are outside v1.
- Surface relevant upcoming events for the next four weeks, emphasizing the next two weeks and giving weeks three and four lower prominence.
- Show events from the past seven days in a clearly separate history section.
- Show actions whose due date passed within the previous seven days in a separate `Past due date` section without implying they remain unfinished.
- Provide a `Check for updates` action so the user can retrieve same-day changes before relying on an event's details.
- Keep the cached digest reasonably current through background checks every four hours.
- Show the cached digest on app open without making app opening itself trigger an inbox check.
- Surface required forms, payments, schedule changes, supplies to bring, academic concerns, and requests for a parent response as action items with source dates, stated due dates or timeframes, and plain-language `Exact date`, `Date range`, or `Needs review` labels.
- Show undated items for seven days after receipt, organized by received date and age, clearly distinguishing that fallback from a deadline; resolve relative timeframe language against the source email date.
- Include important dates/events in the digest while deferring formal calendar event candidates to a second product stage.

## Working Hypotheses

- The Outlook/Hotmail pilot can prove digest value using a subset of household communication despite incomplete inbox coverage.
- Child and school attribution will help distinguish communication across schools.
- Reliably surfacing important items from high-volume school email is the primary problem.
- Preserving confirmed role-specific timing requirements will make event details more useful and trustworthy.
- The date-aware digest will reduce the need to open individual school emails enough to become the family's primary school-information review surface.

These are working hypotheses, not confirmed release boundaries.

## Category Discovery

During setup, the product scans 90 days of inbox metadata to suggest sources. After the owner approves source rules, it analyzes the complete set of matching message bodies from that same 90-day period to suggest announcement categories. The owner chooses what matters. The product should also suggest new categories as approved-source messages arrive. Historical discovery does not expand the agreed digest display windows.

Sharing a generic category catalog across households is a future idea. Shared categories must not expose personal details or overly specific household information; the sanitization process remains unresolved.

Newly discovered categories appear in `New possible categories`, where the owner chooses which ones matter. Potentially relevant items in a proposed category remain in `Needs review` while the decision is pending. Household viewers do not change category preferences.

For each selected category, the owner explicitly selects individual children or `All children`. Categories may apply to one or multiple children; there is no implicit household-wide default.

Adding a child includes a review of relevant categories, with existing `All children` categories preselected for the new child. The owner can adjust the selections; saving the child confirms the category assignments.

An approved-source message directly naming a configured child and requesting action appears in `Needs review` even if its category is unselected or declined. The digest explains why this personalized obligation was retained.

## General Source Model

Different schools and communication systems organize sender identities differently. The product must not hardcode the first household's school domains or assume one matching strategy works everywhere.

The owner should be able to approve an exact sender address or an entire sender domain, based on how a school communicates. These two rule types are sufficient for v1; address-pattern and stable-sender-identifier rules are deferred until examples demonstrate a need. The product may recommend a rule from observed metadata, but the owner remains authoritative. Trusted-source approval permits processing; relevance classification determines digest inclusion. Confidently irrelevant messages are omitted, while low-confidence relevance decisions appear in a compact `Needs review` section.

## Pilot Source Configuration

Synthetic examples use changing staff display names and opaque plus-address identifiers on `school-platform.example`. The owner approves that platform domain once so new staff senders are not missed. A direct-teacher example uses `teacher@school.example`. These preserve configurable source-trust requirements; they are not real account details or universal defaults.

## Non-Goals For The First Version

- Analyzing attachment contents or external linked pages; v1 content analysis is limited to email bodies.
- Calendar connections, calendar writes, and automated reminders.
- Proactive email, browser, or mobile notifications.
- Full provider coverage.
- A general-purpose inbox assistant.
- A daily digest email as the default experience.
- Production billing or organization management.

## Planned Second Stage

- Add Google Calendar integration soon after the digest-focused first release proves useful.
- Consider proposed or automatic events, reminders, and policy-based automation within that stage; the exact behavior remains unresolved.
- Consider browser or mobile notifications after the first-release digest workflow is validated.
- Consider automatically checking for new mail when the owner opens the app or increasing background frequency.
