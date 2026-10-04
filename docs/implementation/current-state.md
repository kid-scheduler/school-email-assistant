# Current State

## Summary

School Email Assistant is in the requirements and harness setup phase. Requirements discovery is paused at the [Version 0 trial snapshot](../product/requirements-workshop-v0.md). No application functionality has been implemented, and this snapshot does not authorize formal specification or implementation.

## Completed

- Confirmed that undated items remain visible for seven days after receipt, organized by received date and age, distinct from deadlines; relative dates use the source email date.
- Confirmed that owner relevance and child/category corrections update the digest and provide feedback for future classification improvement; household viewers remain read-only.
- Confirmed that correction learning is scoped to the household and preserves context; broader explicit preference changes require owner approval, with cross-household learning deferred.
- Confirmed that v1 analyzes email bodies only; attachment contents and external linked pages are deferred.
- Created public project documentation skeleton.
- Defined initial product requirements.
- Defined initial architecture and LangGraph workflow direction.
- Added product repository `AGENTS.md`.
- Added project-local harness guidance.
- Added living documentation folders for product, architecture, decisions, and implementation state.
- Confirmed that the first release is a read-only, date-aware digest; calendar integration is the planned near-term second stage.
- Confirmed that worthwhile first-release outcomes are less time spent checking individual school emails and no surprises from relevant school events in processed messages.
- Confirmed a qualitative pilot evaluation after two weeks of normal use: primary use of the digest, less review burden, and no surprises caused by missed in-scope events; extend if too few events occur to judge coverage.
- Confirmed that invited household members, including guardians or students, can view the digest without connecting their inboxes.
- Confirmed that every authorized viewer may see the complete household digest and child-specific views; these views do not impose per-child access restrictions.
- Confirmed that the household owner and each viewer use separate accounts from the first release.
- Confirmed passwordless one-time email-code sign-in, replacing the earlier email-link decision, with persistent sessions, email invitations from the owner, and revocable viewer access; Outlook mailbox authorization remains separate. Auth0 is under consideration, not selected; SMS codes are outside v1.
- Confirmed that household viewers are read-only; v1 has no handled status or shared item-state updates.
- Confirmed that the first release processes one owner-controlled email account; all other household inboxes are deferred.
- Selected one owner-controlled personal Outlook/Hotmail inbox and Microsoft Graph for the pilot; messages available only in other inboxes remain outside coverage.
- Confirmed that the digest uses a fixed four-week upcoming horizon, emphasizes the next two weeks, and has a clearly separate seven-day past-events section.
- Aligned actions whose due date has passed with the existing seven-day history window, in `Past due date` without implying they are unfinished.
- Confirmed that forms, payments, schedule changes, required supplies, academic concerns, and parent-response requests are in scope and should show the source email date plus any stated due date or timeframe.
- Confirmed that the digest must distinguish date specificity from certainty in the system's interpretation.
- Confirmed that temporal items use `Exact date`, `Date range`, and `Needs review` labels instead of numeric confidence scores.
- Confirmed that v1 provides an on-demand `Check for updates` action, shows the last successful check and check status, and identifies material event changes.
- Confirmed that v1 performs background checks every four hours; app opening shows the cached digest but does not itself trigger an inbox check.
- Confirmed that the background cadence is operationally configurable rather than a user-facing v1 setting.
- Confirmed that initial source setup uses owner-approved suggestions from recent metadata and that the owner can add missing sources at any time.
- Confirmed that initial source discovery scans the previous 90 days of message metadata only.
- Confirmed that category discovery then analyzes all approved-source message bodies from the same 90-day period, before owner category selection.
- Confirmed that ongoing category suggestions appear in `New possible categories` for owner selection; potentially relevant items remain in `Needs review` while a decision is pending.
- Confirmed that each selected category requires explicit assignment to one or multiple children, with no implicit household-wide default.
- Confirmed that category selection includes an explicit `All children` option.
- Confirmed that adding a child shows relevant categories with existing `All children` categories preselected; the owner can adjust selections, and saving confirms the assignments.
- Confirmed that approved-source messages directly naming a configured child and requesting action appear in `Needs review` even when their category is unselected or declined.
- Confirmed that digest and review items show supporting excerpts, source subject, sender, and received date; original-email links are for the inbox owner where supported, while viewers read excerpts and metadata without mailbox access.
- Confirmed that relevant items referring to attachments or linked instructions remain visible with specific missing-detail wording and source metadata, without analyzing external contents.
- Confirmed that clear replacements update event or action details with retained evidence; unresolved conflicts appear in `Needs review` with both excerpts and source metadata.
- Confirmed that a shared event appears once in the household digest and in each applicable child's view, preserving child-specific details and consistent updates.
- Preserved a synthetic platform sender pattern with multiple staff display names and opaque plus-address identifiers on one example domain.
- Confirmed that source matching is configurable per school or communication system and must not hardcode the first user's schools.
- Confirmed that exact sender-address and sender-domain approval rules are sufficient for v1; pattern and stable-identifier rules are deferred until examples demonstrate a need.
- Confirmed that trusted messages are still relevance-filtered and that confidently irrelevant messages do not appear in the primary digest.
- Confirmed that low-confidence relevance decisions appear in a compact `Needs review` section with sender, subject, received date, and the reason for uncertainty.
- Retained platform-domain approval and a direct-teacher pattern as synthetic pilot configurations and acceptance examples, not universal defaults.
- Preserved a synthetic direct-teacher pattern with an individual address on an example school domain and a personalized academic-check-in subject type.
- Generalized household composition, account assignments, and incidents into a public-safe pilot persona while preserving the confirmed requirements they informed.
- Explicitly labeled provisional trial defaults, inherited architecture proposals, and unresolved decisions in the Version 0 snapshot.

## In Progress

- Requirements discovery paused at the product owner's request; no further discovery or implementation is underway.
- Building the generic agent development harness.
- Drafting blog posts before anything is published.

## Known Risks

- Essential details available only in attachments or linked pages are outside v1 coverage.
- MVP scope may still be too broad.
- The one-account pilot cannot cover school communication available only in other household inboxes.
- Event messages can contain different times for a child and parent; flattening these into one event time could mislead users.
- UI workflow expectations need mock validation before implementation.

## Open Questions

- Cancellation display remains unresolved; retaining a canceled item at its original date was proposed but not accepted.
- The auth provider, session/code behavior, privacy retention, and remaining synthetic acceptance examples remain unresolved; see [Open Questions](../open-questions.md).
- What is the first UI stack?
- What is the first persistence layer?
- What exact OpenSpec workflow will the project adopt?

## Last Verified

Documentation-only Version 0 snapshot. No application checks exist yet. `git diff --check` passed; 35 local Markdown links across 16 documents were validated. Public-safety review found only synthetic example addresses and public provider documentation links; exact household details and original school-email identifiers were removed.
