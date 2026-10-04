# Product Requirements

## Version 0 Status

The Version 0 workshop checkpoint has been merged into main. Documentation reconciliation is complete; formal specification and implementation remain deferred. See [Trial Snapshot](product/requirements-workshop-v0.md) for decision labels and [Review](product/requirements-workshop-v0-review.md#reconciliation-status) for finding status.

## Problem

Parents receive a steady stream of school-related emails across multiple children, schools, activities, and systems. Important dates and required actions are mixed with fundraising, newsletters, announcements, and real school events that may not apply to their child. The first release should help users choose the schools, senders, children, and topics they care about, ignore irrelevant items, and replace repeated inbox scanning with one date-aware digest.

The public-safe pilot persona receives messages from school communication platforms and directly from teachers. The household manually reads these messages, decides what matters, and adds important items to a shared calendar. Important items can be missed because there are too many messages to review consistently.

Generalized problem examples are a school event noticed too late to plan around and a required student activity whose student arrival time is difficult to distinguish from the audience start time. These examples preserve the needs identified during discovery without recounting a real household's incidents. The first-release problem includes both timely discovery of relevant obligations and accurate interpretation of role-specific event details.

## First Release Goals

- Let the household owner connect one email account for read-only processing.
- Discover likely school-related senders from recent email.
- Let the user approve trusted sources instead of silently trusting AI decisions.
- Let the household owner add missing trusted sources at any time.
- Support child-specific profiles for school, grade, interests, and ignore rules.
- Classify incoming school email by child, source, topic, urgency, and actionability.
- Filter out irrelevant school items, such as events for another grade, class, club, sport, or child.
- Extract summaries, required actions, deadlines, upcoming event details, and role-specific times.
- Treat required forms, payments, schedule changes, supplies to bring, academic concerns, and requests for a parent response as in-scope action items.
- Show when each action item was mentioned in email and associate it with any stated due date or timeframe.
- Distinguish source date specificity from confidence in the system's interpretation.
- Present relevant information in one digest so the user does not need to read through every school email.
- Let authorized household members use separate accounts to view the digest without requiring them to connect an inbox.
- Show relevant upcoming events within a fixed four-week horizon, emphasizing the next two weeks over weeks three and four.
- Show past events in a clearly separate history section, defaulting to seven days.
- Let the user check for new messages on demand so same-day event changes can be retrieved before relying on the digest.
- Check the connected inbox in the background every four hours so the cached digest remains reasonably current between manual checks.
- Collect user feedback so source and topic matching improves over time.

## Product Surfaces

The product owner selected these major components; this direction is restored in [Decision 0005](decisions/0005-preserve-selected-component-direction.md):

- A React web application as the first user-facing surface.
- A React Native phone application after the web workflow and API contracts are stable.
- A backend API service for accounts, provider connections, preferences, digests, and review flows.
- A Postgres database for persisted product state, provider metadata, graph state, extracted items, and audit records.

The backend framework, detailed schema, authentication vendor, deployment topology, and hosting remain undecided. Component selection does not authorize implementation.

The first implementation should prioritize the web app, API service, and database. The phone app should be planned as part of the product architecture, but it does not need to be built before the web version proves the core workflows.

## Users

- Parents or guardians with one or more children in school.
- Families with a mix of elementary, middle, and high school communications.
- Users who receive school email through Gmail or Outlook and use Google Calendar or Outlook Calendar.

### Public-Safe Pilot Persona

The pilot persona is a parent or guardian managing communication for children at different schools and educational stages. School messages are spread across multiple household inboxes, potentially including parent-controlled and school-managed accounts. This is a generalized scenario, not a record of the product owner's household.

The first release processes one owner-controlled personal Outlook/Hotmail inbox. Messages available only in other inboxes are outside pilot coverage. The persona uses a shared calendar, but calendar connection is not required for the digest; Google Calendar is the planned follow-on integration.

Invited household members, including another guardian or a student, should each have a separate account that can view the digest. Viewing access does not require connecting or processing their inboxes. All authorized household viewers may see the complete digest and may switch to a child-specific view. These views filter presentation; they do not restrict which children's information a viewer is allowed to access.

The first release therefore has at least two account roles:

- A household owner who connects inboxes and manages the household setup.
- Read-only household viewers who authenticate separately and can view the shared digest.

Household viewers do not change configuration, provide shared item status, or mark items as handled in the first release.

### Generalized Current Workflow

- Family members manually scan school email for relevant information.
- They manually judge whether an item is important.
- They manually add noticed dates and commitments to a shared calendar.
- The process sometimes misses important items because of email volume.

### Confirmed Problem Cases

- A relevant school event may be seen or remembered too late for the family to plan around it.
- A required child activity may not reach the family's shared awareness in time.
- One communication may contain multiple meaningful times for different people, such as a student's required arrival time and a parent's audience start time.
- Treating every time in a message as the same event time would produce an incomplete or misleading result.

### Confirmed Action Categories

The first-release digest should surface each of these when relevant:

- Forms requiring completion or signature
- Payment deadlines
- Schedule changes
- Supplies or materials to bring
- Academic concerns
- Requests for a parent response

Each action item should show the source email date and one of:

- An explicit due-by date from the source
- A resolved relative date, such as converting "next Monday" relative to the source email date
- A resolved date range for a broad timeframe such as "next week"
- A clear indication that the source provided no due date or timeframe

A source date range such as `Oct 2–6` includes both endpoint calendar days unless the source explicitly says otherwise (for example, `before Oct 6`). Preserve any explicit time limits or uncertainty rather than overriding them with the inclusive-day convention.

The digest should preserve the source's original timeframe language as evidence. It must not turn a broad timeframe into a fabricated exact deadline.

When the body provides no event date, due date, or timeframe, use the email's received date to organize the item and show its age, clearly labeled as the received date rather than an event date or deadline. Keep these undated items visible for seven household-local calendar dates, counting the received date as day one. They leave the digest at midnight starting day eight: an item received Sept 27 at 18:00 remains eligible through Oct 3 and leaves at 00:00 Oct 4. This is calendar-day aging, not 168 elapsed hours. Pending review items remain accessible in the owner review queue after leaving the digest. Relative phrases normally resolve against the source email date, using the estimated received-date fallback below when the source timestamp is missing or unreliable; retain the original phrase. Items with explicit or resolved dates use those dates for placement instead of this undated fallback.

When the source sent timestamp is missing or unreliable, use the received timestamp in the household timezone to estimate relative dates. Show the estimate with `Estimated from received date`, explain that the source timestamp was unavailable or unreliable, and preserve the original phrase and received timestamp. For an email received Oct 4 saying “tomorrow,” estimate Oct 5. Do not present this fallback as a confidently resolved source date or let it imply future calendar-write eligibility.

Each temporal item should communicate two separate qualities:

- **Source specificity:** whether the source gave an exact date, an exact relative date, a broad range, or no timeframe.
- **Interpretation certainty:** whether the system's resolved date or range is clear or needs review.

For example, "next Monday" in a clearly dated email can resolve to an exact date with high interpretation certainty, while "sometime early next week" should remain a range and may carry lower interpretation certainty.

The first release should communicate these qualities with plain-language labels rather than numeric confidence scores:

- `Exact date` for a specific source date or a clearly resolved exact relative date
- `Date range` for a broad but resolvable timeframe
- `Needs review` when the timeframe cannot be interpreted confidently

### Confirmed Worthwhile Outcomes

- The first user spends less time checking individual school emails.
- The first user is not surprised by relevant school events that were present in processed messages but somehow missed.

Evaluate usefulness qualitatively after two weeks of normal use. No numeric time-saving baseline has been established, so no numeric target is required. The pilot is worthwhile if the digest becomes the user's main review surface, feels less burdensome than checking individual school emails, and avoids surprises caused by missing relevant in-scope events. Extend the evaluation if there are too few school events to judge coverage. In-scope coverage is limited to email bodies from approved sources in the connected inbox; this is not a guarantee about information outside that boundary.

## Core User Journeys

### Sign In And Share Household Access

Use passwordless one-time email codes for owner and viewer sign-in in v1. Users enter the code sent to their email address; this replaces the earlier email-link decision. Keep sessions persistent so users do not need a new sign-in email on every visit. The authentication vendor and session lifetime remain implementation decisions. Auth0 is under consideration, not selected. SMS codes are not part of v1.

The household owner invites viewers by email. Each viewer authenticates with their own email identity and receives read-only access to the household digest. The owner can revoke a viewer's household access at any time; revocation must prevent further access through existing sessions as well as future sign-ins.

Sign-in and invitation emails are transactional access messages, separate from the deferred digest emails and proactive notifications. App sign-in does not authorize mailbox access: the owner separately connects the selected Outlook/Hotmail inbox through Microsoft OAuth. Viewers do not need mailbox authorization.

### Connect Accounts

The first release connects one owner-controlled email account for read-only processing. It does not require a calendar connection.

Providers considered for the generalized pilot:

- Outlook email
- Gmail

One owner-controlled personal Outlook/Hotmail inbox is selected for the pilot. Coverage follows the messages in that inbox, not the household's full set of children or schools. Outlook/Hotmail was selected because Microsoft Graph supports delegated read access for personal Microsoft accounts without administrator consent, while Gmail full-message read access uses a restricted OAuth scope with additional verification and testing-token constraints. Google Calendar integration is deferred until after the digest-focused release proves useful.

### Choose School Sources

During first-time setup, the system scans message metadata from the previous 90 days and suggests likely school-related sources. The household owner accepts, rejects, or edits the suggestions. The owner can also add a missing source at any time, including after initial setup.

Examples:

- A school domain
- A principal or teacher address
- ParentSquare or district announcement sender
- Activity-specific senders such as orchestra, athletics, counseling, or PTA

AI can rank and explain suggestions, but only user-approved sources should create downstream summaries.

Suggestion is not approval. Message content from an unapproved source must not enter content-analysis workflows. During first-time setup, source discovery scans metadata from the previous 90 days; after owner approval, category discovery analyzes matching message bodies from that same period.

When a new source is approved after setup, analyze matching messages from a 14-calendar-date window including approval day. Reapproving a disabled source uses the same 14-date window including reapproval day, including matching messages received while it was disabled. Reconcile with existing items rather than creating duplicates or resetting their received dates. The 90-day lookback is only for first-time setup. These processing windows do not expand the digest display windows. Count the triggering household-local date as the final included date, start at midnight on the first included date, and stop at the triggering check time. For approval Oct 4 at noon, the 14-date backfill begins Sept 21 at 00:00 and includes messages through Oct 4 noon. The first-time 90-date discovery window uses the same convention: a scan triggered Oct 4 at noon begins July 7 at 00:00. Category discovery during setup uses that same initial discovery window. Do not scan the future remainder of the triggering day.

Source approval granularity varies by school and communication system. The product must not hardcode the first user's school domains, ParentSquare behavior, or a single universal matching strategy.

The confirmed first-release source-rule types are:

- Exact sender-address approval for an individual teacher or staff member
- Sender-domain approval for a school, district, or communication platform

Address-pattern and stable-sender-identifier rules are deferred until examples demonstrate a need for them.

The system may recommend a rule based on observed metadata and should explain its breadth, but the household owner chooses and approves the rule. A broad domain rule permits processing from that domain; it does not force every message into the digest.

When the owner narrows or disables an approval, stop analyzing new messages no longer covered by an active approved rule. Retain and continue displaying previously approved items under the ordinary digest display rules, with a warning when their source is no longer approved. Narrowing or disabling is not deletion. Another active covering rule still permits analysis; do not label that source unapproved merely because one rule changed. See [source lifecycle scenarios](product/reconciliation-scenarios.md#source-rule-lifecycle-r3) for confirmed outcomes.

### Synthetic Pilot Source Configuration

Synthetic communication-platform examples preserve this sender pattern:

- Display name: `<staff member> via <school platform>`
- Transport address: `donotreply+<synthetic-id>@school-platform.example`
- Subject types: school-wide newsletter, class newsletter, volunteer request, and event announcement

The examples use a different opaque address identifier for each synthetic staff sender. Exact-address approval would create multiple approvals and may miss newly encountered platform senders.

In this synthetic pilot configuration, the owner approves `school-platform.example` once as a trusted delivery-platform domain. That approval covers current and future sender addresses on that domain in the connected inbox; individual staff senders do not require separate approval. This preserves the confirmed requirement to support owner-approved broad platform trust without embedding a real household's platform configuration or making it a universal default.

Platform trust determines which messages may be processed, while relevance determines which processed messages appear in the digest. The digest should omit trusted-source messages that are confidently irrelevant to the household; displaying every processed message would reproduce the inbox-review burden. Low-confidence relevance decisions should appear in a compact `Needs review` section rather than being silently hidden.

A synthetic direct-teacher example has this structure:

- Display name: `<teacher>`
- Address: `teacher@school.example`
- Subject type: personalized academic check-in

This represents the confirmed requirement that direct teacher email can contain an in-scope academic concern. It is a synthetic acceptance pattern for exact-address or school-domain rules, not evidence that all schools use the same convention.

### Configure Children And Topics

The confirmed desired setup experience is category discovery: scan an initial set of messages for categories of announcements, present the discovered categories, and let the household owner choose which ones matter. The system should also suggest newly encountered categories during ongoing use. This reduces the need for the owner to invent a complete topic list before seeing examples.

Initial category discovery uses the complete set of messages from the previous 90 days that match owner-approved source rules. Setup therefore proceeds from metadata-based source suggestions to owner approval, then body analysis of the approved historical messages, then owner category selection. The system must not analyze unapproved message bodies to discover categories.

The historical category-discovery window is separate from digest display: only relevant extracted items within the agreed upcoming and past windows enter the dated digest sections.

During ongoing use, newly discovered categories appear in a separate `New possible categories` section that asks the household owner which ones they care about. The owner selects or declines each category. Undecided category suggestions remain available in `New possible categories` until the owner decides, even after their supporting items leave the digest; the suggestions do not expire after seven days. Until that decision, potentially relevant items in the proposed category appear in the digest’s `Needs review` section rather than automatically entering the primary digest or being silently hidden. Undated items awaiting a category decision leave the digest after the ordinary seven-day received-date window, but remain accessible in an owner review queue until decided; aging out of the digest does not discard the pending item. The same queue transition for undated conflicts and uncertain child assignments is described in [Date-Aware Digest](#date-aware-digest). Household viewers remain read-only and do not make category decisions.

For every selected category, the owner explicitly chooses which children it applies to. The selection offers individual children and an `All children` option. A category can apply to one or multiple children; selecting `All children` applies it to every configured child. Category preferences have no implicit household-wide scope. The same child-selection behavior applies during setup and when deciding newly suggested categories.

When adding a child, show all relevant categories for owner review and preselect categories already marked `All children` for that child. The owner can adjust these selections and choose other relevant categories during this step. Saving the child confirms the selected category assignments; suggestions do not take effect before saving.

For approved-source messages, category preferences must not silently hide a personalized obligation: when a message directly names a configured child and requests action, show the relevant item in `Needs review` even if its category is unselected or declined. Explain that the child's direct mention and action request triggered this exception. The message still requires approved-source status; this exception does not grant trust to a new sender. A direct teacher message naming a configured child and requesting action also overrides an explicit topic ignore rule by going to `Needs review`, with that reason explained. A general school-wide newsletter does not trigger this exception merely because it contains many dates, news items, or a generic request; it follows ordinary child-aware relevance and ignore rules. Personalization is about the message's child-specific request, not just the sender being a teacher. A later item-specific owner correction takes precedence on reprocessing the same message; see [Owner Corrections And Feedback](#owner-corrections-and-feedback).

Each child should have a profile:

- Name
- School
- Grade
- Relevant aliases or classroom labels
- Topics of interest
- Topics to ignore

Topics should be natural-language rules with examples, not only static keywords. For example, "Orchestra" can include concerts, rehearsals, call times, required attire, schedule changes, auditions, and parent meetings.

Ignore rules should also be child-aware. A message can come from a trusted school source and still be irrelevant if it concerns a grade, class, activity, team, or event that does not apply to any configured child.

### Future Idea: Shared Category Catalog

Generic categories learned across households could eventually help new users configure their digest. Any shared catalog must exclude personal names, school identifiers, source addresses, message excerpts, and categories so specific that they reveal a household's private information. The sanitization and approval process is unresolved; cross-household category sharing is not a confirmed v1 requirement.

### Date-Aware Digest

During household setup, prefill a detected timezone for the owner to confirm or change. Save the confirmed household timezone and use it for date interpretation, day boundaries, and all household/child views; viewers’ device timezones do not independently change those rules. If detection is unavailable, the owner must select a timezone before confirming it. No timezone-detection implementation is selected.

The digest offers a household view and individual child views. A shared event appears once in the household view, labeled with all applicable children and any child-specific times or instructions. It also appears once in each applicable child's view. These are views of the same event, so updates remain consistent across views. Every authorized viewer can access all of these views.

The digest should provide one place to review:

- New relevant school messages
- Upcoming events found or updated within the next four weeks, with the next two weeks visually emphasized
- Required actions and deadlines
- Forms, payments, schedule changes, required supplies, academic concerns, and parent-response requests, each with the source email date and any stated due date or timeframe
- Relevant dates or events mentioned in email, without promoting irrelevant items into the user's attention stream
- Distinct times for different participants when a message provides them, such as student arrival time and parent start time
- Items whose dates, times, audience, or required actions are unclear
- An `Exact date`, `Date range`, or `Needs review` label for each temporal item
- Confidently ignored items only when the user asks to inspect them
- Low-confidence relevance decisions in a compact `Needs review` section showing sender, subject, received date, and why relevance is uncertain
- Events from the history window in a separate, clearly labeled past section, defaulting to the previous seven complete calendar days

Undated review items with conflicting instructions or uncertain child assignments also leave the digest after the seven-day received-date window and remain accessible in the owner review queue until decided. Preserve their uncertainty and source evidence; moving an item out of the digest does not resolve or discard it. The calendar-day expiry rule is defined in [Confirmed Action Categories](#confirmed-action-categories).

An event whose date range spans today appears once in the current/upcoming section, labeled `Ongoing`, with its complete original range preserved. Do not also duplicate it in the past section. A relevant event range is eligible for current/upcoming display when any part overlaps the upcoming window. Preserve the full source range even when it extends beyond the four-week horizon; do not clip it or require the entire range to fit. The upcoming window covers 28 household-local calendar dates including today: from the start of today through the end of day 27 after today. With today Oct 4, include Oct 4–31; a single-date Nov 1 event is outside the window. The first two weeks cover the first 14 dates (Oct 4–17), followed by weeks three and four (Oct 18–31). An event range receives the first-two-week emphasis when any part overlaps those first 14 dates. Show the event once with its complete range rather than duplicating or clipping it across prominence groups; an Oct 16–20 event is emphasized, while an Oct 18–20 event has lower prominence.

By default, history covers the seven complete household-local calendar days before today, from the start of day seven days ago through the end of yesterday; today belongs to current/upcoming. With today Oct 4, include Sept 27–Oct 3, including both dates. A past event range is eligible for history when any part overlaps this window. Preserve its complete source range even if it began before the window. An event still spanning today follows the ongoing rule above and is not duplicated in history.

Past events must not be visually mixed with upcoming events. The first release uses a fixed seven-day history period with no user-facing setting. Keep the history period as a separate configuration value consumed by window calculation rather than embedding seven-day assumptions throughout the product, so it can readily become a user setting later. Do not build that setting in the first release. Supported values and who may change it are future-setting decisions. The upcoming horizon remains fixed at four weeks; this history preference does not change source-processing lookbacks or undated-item aging.

When an action's due date passes, move it into a separate `Past due date` section within the same seven-day history window used for past events. For an action with a date range, enter `Past due date` only after the final day of that range ends in the household timezone. Preserve the entire range and original phrase; this placement does not convert the range into an exact source deadline. This label describes the date only: v1 has no completion tracking and must not claim that the action is unfinished. This is the initial display rule and may be revisited after pilot feedback.

The first release will use a date-aware web app view with low-frequency background checks and an explicit `Check for updates` action. A daily digest email is not the default because it would add to the inbox volume the product is intended to reduce. Proactive notifications and near-real-time background fetching are deferred so the first release can be delivered more quickly.

Opening the app should display the cached digest without app opening itself triggering an inbox check. The cached digest may include messages retrieved by four-hour background checks. The household owner can select `Check for updates` to start an immediate inbox check. The digest should display when it last checked the inbox successfully and whether a check is currently running or failed. When a newer message changes the time, location, requirements, or other material details of an existing event, the digest should identify that event as updated and show the current information with source evidence.

The four-hour cadence should be an operational configuration value, not a user-facing preference in the first release, so it can be tuned later without changing digest behavior.

When newer source information clearly replaces earlier details for the same event or action, present the replacement as the current information and retain evidence of the change. Recency alone does not resolve a contradiction. If the messages conflict without a clear replacement, show the item in `Needs review` with both supporting excerpts and their source metadata; identify the conflicting detail instead of choosing a value without adequate evidence.

### Owner Corrections And Feedback

The household owner can mark a review item relevant or irrelevant and correct its child and category assignments. Corrections should update the current digest and be retained as feedback to improve future classification. The owner must also be able to correct an ordinary digest item or an item inspected in the filtered-items view, so confidently wrong decisions can be recovered.

When the owner marks a specific item irrelevant, keep that item hidden on reprocessing the same email, even if it otherwise qualifies for the personalized child-action exception. The explicit item correction wins; replay must not reopen `Needs review` or silently change broader category preferences. A later approved-source follow-up that materially changes the obligation returns to `Needs review`, with the changed requirement explained and the earlier correction retained as context. An unchanged reminder stays hidden under the specific-item correction. A new message or more recent timestamp alone is not a material change.

This feedback concerns relevance and classification, not action completion. Household viewers remain read-only. Use individual corrections to improve classification of similar future messages within the same household, preserving the context of the correction. For example, rejecting a trip for another grade should improve grade matching without disabling relevant field trips. Broader changes to explicit category preferences or child assignments must be proposed for owner approval rather than applied silently. Cross-household learning from corrections is a future decision and is outside v1.

### Verify Source Evidence

Digest and `Needs review` items should show a short supporting excerpt and the source email subject, sender, and received date so users can locate the original in their inbox. Preserve the source timestamp used to interpret relative date phrases separately when it differs from the received date. The inbox owner can follow an original-email link where supported by the provider. Authorized household viewers can read the supporting excerpt and identifying metadata within the app without mailbox access; digest access does not grant access to the original mailbox.

### Content Coverage For The First Release

Source discovery uses message metadata; category discovery and digest extraction analyze the email body. Attachment contents and external linked pages are outside the first-release analysis boundary. Information available only in an attachment or linked page is outside the pilot's event and action coverage.

When the body identifies a relevant event or action but refers to an attachment or linked page for essential details, retain the item with the information available in the body. State specifically what is missing, such as `Arrival time not provided in email`, and explain the body's reference to external instructions using a supporting excerpt. Do not infer the contents of the attachment or linked page. Show the source subject, sender, and received date, plus an original-email link for the owner where supported, so the user can check the missing details.

Digest completeness is independent of future calendar-write eligibility: missing or ambiguous dates/times and missing external details must remain visible under the digest relevance and display rules. A missing time does not imply an all-day event. See [reconciliation scenarios](product/reconciliation-scenarios.md#digest-completeness-r1).

### Planned Second Stage: Calendar Integration

Calendar integration is not part of the first release, but it is the planned near-term follow-on once the digest proves useful. Calendar automation must be policy-driven:

- Summary only
- Ask before adding
- Auto-add high-confidence events
- Never add calendar events for this topic/source

Calendar writes should be reversible and auditable. Every created event should link back to the source email when the provider allows it.

### Reconciliation Evidence And Remaining Questions

[Review findings](product/requirements-workshop-v0-review.md#reconciliation-status) are resolved with [synthetic scenarios](product/reconciliation-scenarios.md) covering lifecycle, precedence, and date boundaries. Cancellation display, privacy retention, authentication details, and classification/matching validation remain separate [open questions](open-questions.md). These documentation decisions do not authorize implementation.

## Functional Requirements

- Connect and refresh OAuth credentials per provider.
- Retrieve recent and new email from approved providers.
- Normalize HTML email into model-ready text while retaining source metadata.
- Limit content analysis to the email body; do not fetch attachment contents or external linked pages for analysis in v1.
- Store provider message IDs for deduplication.
- Keep user account access inside application-controlled provider connectors; AI should analyze scoped content handed to it by the application, not directly access a user's mailbox or credentials.
- Support exact sender-address and sender-domain approval rules without hardcoding a particular school or communication vendor.
- Explain the breadth of a suggested source rule before the owner approves it.
- Apply the selected source-rule granularity independently for different schools and communication systems.
- Generate source suggestions from recent message metadata and explain why each source was suggested.
- Limit initial source discovery to message metadata from the previous 90 days.
- During first-time setup, discover announcement categories from approved-source message bodies in the same 90-date discovery window. After setup, newly approved or reapproved sources use the 14-date backfill defined above.
- Present newly discovered categories in `New possible categories` for owner selection, retaining potentially relevant items in `Needs review` while the category decision is pending, with undated items moving out of the digest into an accessible owner review queue after the seven-day window.
- Require explicit child selection for each chosen category, offer an `All children` option, and use those assignments when evaluating relevance.
- Route approved-source messages that directly name a configured child and request action to `Needs review` when their category is unselected or declined, explaining the exception.
- When adding a child, present relevant categories for review, preselect existing `All children` categories, and confirm the owner's adjusted selections when saving the child.
- Allow the household owner to approve, reject, edit, or manually add trusted sources at any time.
- Classify messages against children, topics, and user preferences.
- Exclude confidently irrelevant trusted-source messages from the primary digest.
- Route low-confidence relevance decisions to a compact `Needs review` section with enough metadata to support a decision.
- Extract digest-ready event details including date, participant-specific times, title, location, description, confidence, and source evidence.
- Extract in-scope action items with the source email date, any stated due date or timeframe, and source evidence.
- Resolve relative date phrases against the source message timestamp in the household timezone; when it is missing or unreliable, estimate from the received timestamp with a clear fallback label.
- Preserve the original date or timeframe phrase alongside any resolved date or range.
- Show a short supporting excerpt and source subject, sender, and received date for digest and review items, with an original-email link for the inbox owner where supported.
- Retain relevant items whose body refers to external instructions, identify the specific missing details, and provide source metadata to help users locate the email.
- Preserve source specificity separately from interpretation certainty for every resolved temporal value.
- Label action items with no stated date or timeframe instead of inventing a deadline.
- Organize items without a stated date or timeframe by email received date, preserving the distinction between message age and an event or due date.
- Preserve and expose ambiguity instead of inventing a single time when the source describes multiple roles or is unclear.
- Detect duplicate messages and updates to previously extracted information.
- Merge newer source information into an existing event while preserving evidence of what changed.
- Apply clear replacements to event or action details; route unresolved conflicts to `Needs review` with both excerpts and source metadata rather than resolving them by recency alone.
- Persist graph runs, decisions, extracted items, and user feedback.
- Let the owner correct relevance, child assignments, and category assignments for review, digest, and inspected filtered items; update the digest and retain corrections for future classification improvement.
- Use correction feedback within its household; require owner approval before applying broader changes to explicit category preferences or child assignments.
- Generate or refresh a date-aware digest for the user.
- Separate actions whose due date has passed into `Past due date` without implying that they are incomplete.
- Provide an on-demand inbox check, display its status and last-successful-check time, and distinguish materially updated events from unchanged events.
- Run inbox checks every four hours, with the cadence stored as operational configuration rather than hardcoded.
- Do not make app opening itself trigger an inbox check.
- Give each authorized household viewer a separate identity and access to the digest independently of inbox connection ownership.
- Give every authorized viewer access to the complete household digest and child-specific views, without per-child access restrictions.
- Display shared events once in the household view and once in each applicable child's view, preserving child-specific times and instructions.
- Restrict household viewers to read-only access; only the household owner manages inbox connections and configuration.
- Support passwordless one-time email-code sign-in with persistent sessions, owner-issued email invitations, and revocable household viewer access.

## Non-Goals For The First Implementation

- Analyzing attachment contents or external linked pages.
- A free-roaming autonomous inbox agent.
- AI agents with direct access to user email accounts, OAuth credentials, mailbox search, or calendar APIs.
- Calendar connections, calendar writes, or automated reminders.
- Reading every email in a user's mailbox indefinitely.
- Full frontend polish.
- Multi-tenant billing, organizations, or admin analytics.
- Email, browser, mobile push, or SMS notifications.

## Success Criteria

- The household owner can connect the selected Hotmail/Outlook account and approve school-related senders.
- Initial source discovery considers 90 days of message metadata without processing unapproved message content.
- Initial category suggestions come from the complete 90-day set of approved-source messages, with source approval preceding body analysis.
- A newly encountered category appears in `New possible categories`, and its potentially relevant items remain reviewable until the owner chooses whether the category matters; undated items leave the digest after seven days but remain accessible in the owner review queue.
- The owner can assign a category to one or multiple children; category relevance is evaluated for the selected children without an implicit household-wide default.
- Adding a child presents relevant categories with existing `All children` categories preselected; saving applies the owner's final selections to that child.
- An approved-source message directly naming a configured child and requesting action remains visible in `Needs review` even when its category is unselected or declined.
- An event relevant to multiple children appears once in the household view and in each applicable child's view; all views show consistent updates and preserve child-specific details.
- The product can apply an exact-address rule for one source and a domain rule for another without code changes.
- In the synthetic pilot scenario, one platform-domain approval covers newly observed sender addresses on that domain.
- The primary digest does not display every trusted-source message and excludes messages confidently classified as irrelevant.
- Low-confidence messages remain visible in `Needs review` with sender, subject, received date, and an explanation of the uncertainty.
- The owner can add a missing trusted source after initial setup without reconnecting the inbox.
- The system can process recent approved-source email through a LangGraph workflow.
- The system can produce structured summaries, topic matches, required actions, deadlines, and upcoming event details.
- The digest identifies each in-scope action category and shows when its source email was sent.
- The digest preserves and resolves stated due dates or timeframes without converting vague ranges into fabricated exact deadlines.
- The digest distinguishes exact dates from ranges and clearly marks interpretations that need review.
- Temporal certainty is communicated with plain-language labels rather than numeric confidence scores.
- The digest clearly identifies action items whose source provides no due date or timeframe.
- Items with no stated date or timeframe remain visible for seven household-local calendar dates including receipt day and leave at midnight starting day eight, without presenting received date as an event date or deadline. Pending review items remain accessible in the owner review queue.
- The digest distinguishes role-specific times when the source does, including student arrival time and parent start time.
- The digest presents relevant upcoming information relative to the current date without requiring a calendar connection.
- The digest shows the next four weeks, emphasizes the next two weeks, and keeps the default previous seven complete calendar days in a clearly separate past section.
- An action moves to `Past due date` after its due date passes, without an unsupported completion-status claim.
- After a successful user-initiated check, a material same-day event update is visible and clearly marked as an update.
- A clear replacement updates the displayed event or action details with retained evidence; an unresolved conflict shows both supporting sources in `Needs review` without presenting an unsupported resolution.
- The user can see when the inbox was last checked successfully and whether the current check succeeded or failed.
- Scheduled checks run every four hours, and changing that operational cadence does not require changing the digest contract.
- The digest can explain why each item was included.
- Relevant items with essential details outside the body state what is missing without inventing those details; their source subject, sender, and received date help users locate the email.
- The owner can verify an item against its supporting excerpt and original-email link where supported; authorized viewers can read the excerpt and source metadata without mailbox access.
- User feedback can update future source/topic behavior.
- Owner relevance and assignment corrections update the current digest and are retained for improving future classification; household viewers cannot make these corrections.
- A contextual correction can inform similar future messages without silently changing explicit category preferences; broader preference changes require owner approval.
- After two weeks of normal use, the first user reports using the digest as the main school-communication review surface and finding it less burdensome than checking individual emails; no numeric time-saving baseline is required.
- During that period, relevant school events stated in approved-source email bodies in the connected account do not surprise the user because the digest missed them. Extend the pilot if too few events occur to assess coverage.
- Invited household members can view the digest under the agreed household access model.
- Owners and invited viewers can sign in by entering a one-time code sent to their email address, without a password. Viewers do not need to connect an inbox; revoked viewers lose household access even if they have an existing app session.

The pilot usefulness criteria above are confirmed. Remaining workflow decisions and representative synthetic acceptance examples must be completed before formal specification or implementation. Refresh behavior is defined as four-hour background checks plus owner-triggered checks.
