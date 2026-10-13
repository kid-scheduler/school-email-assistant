# Accepted MVP Definition

Consolidated 2026-10-12 from [product requirements](../product-requirements.md) and accepted decisions [0002](../decisions/0002-make-the-first-release-digest-only.md), [0003](../decisions/0003-use-outlook-hotmail-for-the-first-inbox.md), [0004](../decisions/0004-use-configurable-source-rules.md), and [0005](../decisions/0005-preserve-selected-component-direction.md). This is a navigation summary of accepted requirements, not a formal specification. Subsequent owner approvals are recorded under Next Activity And Provenance. Requirements remain authoritative; historical experiments are not authority.

## First User And Problem

A parent or guardian managing school communication for children at different schools and educational stages needs a less burdensome way to notice relevant obligations in time and understand child-specific details. Manual inbox scanning can miss important events or confuse student arrival with audience start time. See [Problem](../product-requirements.md#problem) and [Public-Safe Pilot Persona](../product-requirements.md#public-safe-pilot-persona).

The first user is the household owner. Invited household members have separate read-only identities and can view the whole household digest or any child view without connecting an inbox. Child views filter presentation, not access permissions. See [Users](../product-requirements.md#users).

## Core End-To-End Journey

1. The owner signs in with a one-time email code, separately authorizes read-only access to one personal Outlook/Hotmail inbox, and confirms the household timezone.
2. Metadata-based source discovery suggests senders; the owner approves exact-address or domain rules before any body analysis.
3. Category discovery analyzes approved-source bodies. The owner configures children, chooses categories and explicitly assigns them to children, including ignore preferences.
4. The owner and invited viewers review the cached household or child digest: relevant events, actions, uncertainty, updates, and source evidence.
5. Background checks and owner-triggered checks retrieve new information. Date-dependent display also updates from stored items without requiring an inbox check.
6. The owner reviews new category suggestions, inspects filtered items, and corrects relevance or assignments. Corrections update the digest and inform future household classification without silently changing explicit preferences. The owner can add or change sources and revoke viewer access.

Authoritative contracts: [Sign In And Share Household Access](../product-requirements.md#sign-in-and-share-household-access), [Choose School Sources](../product-requirements.md#choose-school-sources), [Configure Children And Topics](../product-requirements.md#configure-children-and-topics), [Date-Aware Digest](../product-requirements.md#date-aware-digest), and [Owner Corrections And Feedback](../product-requirements.md#owner-corrections-and-feedback).

## Included Capabilities And Coverage

- A React web digest, backend API, and Postgres; LangGraph coordinates AI workflows while application services control provider access. Detailed implementation choices remain open under [Decision 0005](../decisions/0005-preserve-selected-component-direction.md).
- Configurable owner-approved sources, child-aware relevance, discovered categories, and owner corrections. Source trust permits processing; it does not require inclusion. Approval lifecycle and processing lookbacks remain governed by [Choose School Sources](../product-requirements.md#choose-school-sources).
- Summaries, upcoming events, and relevant actions including forms, payments, schedule changes, supplies, academic concerns, and parent responses. Preserve role-specific details, original timeframe language, date specificity, interpretation uncertainty, and missing details. See [Confirmed Action Categories](../product-requirements.md#confirmed-action-categories).
- Household and child views of shared items, review sections and an owner review queue, separate past/history and past-due-date presentation, material updates and unresolved conflicts. Display windows, aging, timezone boundaries, refresh cadence, and cached date rollover live in [Date-Aware Digest](../product-requirements.md#date-aware-digest).
- Supporting excerpts and source metadata for authorized viewers; original-email links for the owner where supported. See [Verify Source Evidence](../product-requirements.md#verify-source-evidence).

Pilot coverage is limited to approved-source email bodies in the connected inbox. Other inboxes, attachments, and external linked pages are outside analysis and coverage. Relevant body information remains visible when external details are missing, with the gap explained rather than invented. See [Content Coverage](../product-requirements.md#content-coverage-for-the-first-release) and [Decision 0003](../decisions/0003-use-outlook-hotmail-for-the-first-inbox.md).

## Exclusions And Later Stages

The first release excludes calendar connections, formal calendar candidates/writes, automated reminders, proactive notifications, action-completion tracking, viewer edits, and a general-purpose autonomous inbox agent. App opening does not trigger an inbox check; daily digest email and near-real-time fetching are not defaults. Transactional sign-in and invitation emails remain included. See [Decision 0002](../decisions/0002-make-the-first-release-digest-only.md), [Non-Goals](../product-requirements.md#non-goals-for-the-first-implementation), and the linked journeys above.

Calendar integration is the planned second stage after digest usefulness is demonstrated. React Native, Gmail/other inbox coverage, additional source-rule types, configurable history, notifications, shared category catalogs, and cross-household correction learning remain later-stage work. Their unresolved details are tracked in [Open Questions](../open-questions.md#later-stage-questions). Full frontend polish, billing, organizations, and admin analytics are outside the first implementation.

## Accepted Pilot Success Criteria

After two weeks of normal use, the digest becomes the first user's main school-communication review surface and feels less burdensome than checking individual emails. Relevant events stated in approved-source bodies in the connected inbox do not surprise the user because the digest missed them. Extend evaluation if too few events occur to assess coverage; no numeric time-saving target has been established. See [Confirmed Worthwhile Outcomes](../product-requirements.md#confirmed-worthwhile-outcomes).

The detailed [Success Criteria](../product-requirements.md#success-criteria) also require the accepted setup, access, filtering, extraction, evidence, temporal, correction, and refresh behaviors. Qualitative usefulness does not replace those requirements or expand coverage.

## Preparation For A First Formal Specification

The owner selected cached digest display and source verification for readiness planning on 2026-10-12; see [Decision 0007](../decisions/0007-select-cached-digest-readiness-slice.md) and the [slice readiness review](cached-digest-readiness.md). This checklist neither writes nor authorizes a formal specification.

- [x] Consolidate accepted user, problem, journey, coverage, exclusions, and pilot outcomes with authoritative links.
- [x] Separate remaining questions by the activity needing an answer in [Open Questions](../open-questions.md).
- [x] Obtain owner approval for one bounded first specification slice, identifying its included journey and explicit boundaries.
- [x] Map that selected slice to accepted rules and existing [synthetic reconciliation scenarios](reconciliation-scenarios.md); identify validation gaps without generating new experiments or mocks.
- [x] Resolve product behavior needed within that slice, recording each owner approval and provenance before asking the next decision. Track unrelated questions as deferred rather than universal blockers.
- [x] Agree acceptance coverage for documentation review and prepare supported examples under Decision 0009; distinguish documentation evidence from unperformed UI/model validation.
- [x] Identify implementation choices needed to write that slice and those that can remain open until implementation. Resolve privacy/access lifecycle questions before real-data work that depends on them.
- [x] Owner accepts the documented readiness checklist for the bounded slice under [Decision 0011](../decisions/0011-accept-cached-digest-documentation-readiness.md).
- [ ] Obtain separate authorization to write the formal specification.

## Next Activity And Provenance

On 2026-10-12, the owner first replied `1` to select cancellation display as the next definition activity, then replied `1` to approve keeping clearly canceled dated events at their scheduled dates with a prominent `Canceled` label, ordinary upcoming/history windows, and preserved evidence. [Decision 0006](../decisions/0006-display-clearly-canceled-dated-events.md) records provenance and scope; [Date-Aware Digest](../product-requirements.md#date-aware-digest) contains the authoritative rule. This approval comes from the owner.

Cancellation without a usable date, uncertain matches, reinstatement, and cancellation of a separate action still need scope review. Display eligibility does not decide storage retention or deletion.

The owner subsequently replied `1` to select **cached digest display and source verification** as the first slice for readiness planning. [Decision 0007](../decisions/0007-select-cached-digest-readiness-slice.md) records that approval and boundaries. The [readiness review](cached-digest-readiness.md) maps accepted rules to existing scenarios and identifies targeted gaps. The owner then replied `1` to approve contextual empty/check-history presentation; [Decision 0008](../decisions/0008-distinguish-empty-digest-check-history.md) records provenance. The owner subsequently replied `1` to approve the [full coverage inventory](cached-digest-readiness.md#accepted-coverage-inventory), recorded in [Decision 0009](../decisions/0009-approve-cached-digest-acceptance-coverage.md). [Supplemental examples](cached-digest-acceptance-examples.md) cover supported outcomes and adjacent boundaries. The owner then replied `1` to approve K4 label treatment, recorded in [Decision 0010](../decisions/0010-suppress-ongoing-label-for-canceled-ranges.md): show `Canceled` without `Ongoing`. The owner subsequently selected `1` and explicitly accepted the bounded slice's documented readiness checklist, recorded in [Decision 0011](../decisions/0011-accept-cached-digest-documentation-readiness.md); UI/model validation remains unperformed and formal specification writing remains unauthorized.

Formal specs, mocks, implementation, experiments, skill creation, and Git mutations require separate authorization.
