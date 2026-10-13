# Cached Digest Acceptance Examples

Recorded 2026-10-12 under [Decision 0009](../decisions/0009-approve-cached-digest-acceptance-coverage.md). These synthetic product examples supplement the [existing reconciliation scenarios](reconciliation-scenarios.md) for the selected [readiness slice](cached-digest-readiness.md). They are documentation, not a formal specification, executable fixtures, UI validation, or model experiments. Expected outcomes below derive from accepted requirements; any unresolved outcome is explicitly pending.

## Context And Reused Coverage

Unless a row says otherwise, the household timezone is confirmed as `America/Los_Angeles`, today is **2026-10-12**, Morgan and Riley are configured synthetic children, and the reader is an authorized owner or viewer. Inputs are already stored, approved-source body-derived items, with relevance and child assignments established. Use `teacher@school.example` as a synthetic source where a sender is needed. Processing/matching mechanisms are not selected by these examples.

Reuse D1–D3, M1/M2, B1/B1a/B2/B3/B4/B4a/B5/B6/B6a/B6b, C1a–C1c, C2a–C2d, A1/A4/A5, and S2–S4 from [reconciliation scenarios](reconciliation-scenarios.md) for their documented display outcomes and original dates. Setup, ingestion, feedback learning, and future settings are outside the selected slice.

## Clear Cancellations

Authority: [Date-Aware Digest](../product-requirements.md#date-aware-digest) and [Decision 0006](../decisions/0006-display-clearly-canceled-dated-events.md).

| ID | Synthetic situation | Supported display outcome |
| --- | --- | --- |
| K1 | Stored Oct 15 concert applies to Morgan and Riley. A clearly matched approved-source body says “The Oct 15 concert is canceled.” | Keep the event on Oct 15 with prominent `Canceled`, its scheduled date and evidence. Show the same cancellation once in the household view and once in each applicable child view; do not present an active commitment or add a separate canceled section. |
| K2 | Stored relevant event range Oct 20–22 is clearly canceled in approved-source body information. | Preserve Oct 20–22 and evidence, use ordinary upcoming eligibility/emphasis, and prominently label it `Canceled`. Do not collapse the range or start a new cancellation-specific display window. |
| K3 | K1 is displayed Oct 22, then Oct 23, with no new check. | Its scheduled Oct 15 date remains eligible for ordinary seven-day history on Oct 22 and leaves on Oct 23. Retain cancellation labeling/evidence while displayed; leaving the display window is not a storage-deletion decision. |
| K4 | A clearly canceled Oct 10–14 range spans today, Oct 12. | Show one current/upcoming item with the complete scheduled range, evidence, and prominent `Canceled`, without `Ongoing`. Ordinary eligibility/emphasis/history remain unchanged. Owner-approved label treatment is recorded in [Decision 0010](../decisions/0010-suppress-ongoing-label-for-canceled-ranges.md). |

K4's display question is resolved by Decision 0010. Cancellation without usable dates, uncertain event matching, reinstatement, and canceling separate actions remain excluded rather than receiving invented outcomes.

## Conflicts And Source Verification

Authority: [Date-Aware Digest](../product-requirements.md#date-aware-digest), [Verify Source Evidence](../product-requirements.md#verify-source-evidence), and [Household Access](../product-requirements.md#sign-in-and-share-household-access).

| ID | Synthetic situation | Supported display outcome |
| --- | --- | --- |
| V1 | Already matched Oct 15 concert has one approved body saying “Audience starts at 18:00” and another saying “Audience starts at 18:30,” with no clear replacement. | Show `Needs review`, identify the start-time conflict, and show both supporting excerpts with their source metadata. Do not resolve by recency alone. |
| V2 | Owner opens evidence for K1; this provider supports an original-email link. | Show excerpt, subject, sender, and received date, and allow the owner to follow the supported original-email link. Preserve a distinct source timestamp used for relative-date interpretation when applicable. |
| V3 | Viewer reads the same item's evidence without mailbox authorization. | Show the excerpt and identifying metadata in the app. Household digest access grants no access to the original mailbox; no viewer mailbox authorization is required. |
| V4 | Owner reads an item whose provider offers no supported original-email link. | Supporting excerpt, subject, sender, and received date remain available to locate the email. Do not make a provider link a prerequisite for showing the item or invent a mailbox link. |
| V5 | Previously invited viewer's household access has been revoked, but their app session still exists. | The existing session does not permit further household digest/evidence access. This is an accepted access constraint, not a choice of session or revocation mechanism. |

## Check And Empty States

Authority: [Date-Aware Digest](../product-requirements.md#date-aware-digest) and [Decision 0008](../decisions/0008-distinguish-empty-digest-check-history.md). No row makes opening the app trigger an inbox check.

| ID | Synthetic stored state | Supported display outcome |
| --- | --- | --- |
| E1 | No displayable items and no successful check recorded. | Contextual message distinguishes `No successful inbox check yet`; do not invent a last-success timestamp or imply coverage is established. |
| E2 | Last successful check Oct 12 at 08:00; no items eligible for the current display windows. | Contextual message distinguishes `No relevant items in the current display windows`; retain last success. This does not claim no school obligations exist. |
| E3 | E2 remains empty; a later check at 12:00 fails. | Retain the successful-check empty-state distinction and 08:00 last success, while clearly showing the later failure. Do not suggest the failed check established current coverage. |
| E4 | No successful check ever; attempted check fails; no displayable items. | Retain the no-success distinction and failed-check status. A failure does not turn the view into successful-but-empty. |
| E5 | Cached relevant Oct 15 concert remains eligible; a later check fails. | Keep the eligible cached item, last successful check, and failure visible. Failure does not clear cached items or turn them into an empty state. Apply ordinary date rollover separately, as in C2. |
| E6 | A check is running with an existing 08:00 last success. | Show running status and retained last success; starting a check is not a new success. Check orchestration and trigger interaction remain adjacent dependencies. |
| E7 | Owner-triggered check succeeds; already matched Oct 12 event clearly replaces audience start 18:00 with 18:30. | Show current 18:30, a material-update indication, and retained change evidence consistently in applicable views; reflect the successful check in check history. Use existing M2/C2 expectations to distinguish a source update from date-only rollover. |

Exact copy and layout are reviewable later. These rows do not define retries, polling, failure taxonomies, or source-processing contracts.

## Action-Category Breadth

Authority: [Confirmed Action Categories](../product-requirements.md#confirmed-action-categories). Use synthetic messages sent and received Oct 12 at 09:00 household-local time with already established relevance. All cases retain source evidence and the source email date; placement follows the accepted date rules.

| ID | Category and synthetic body | Supported display outcome |
| --- | --- | --- |
| T1 | Form: “Please sign Morgan's permission form by Oct 16.” | Form action, Oct 16 due date, and source date; no completion-status claim. Existing D1 covers a form without a due date. |
| T2 | Payment: “Riley's activity payment is due Oct 19.” | Payment action with stated deadline and source evidence. |
| T3 | Schedule change: “Morgan's Oct 14 rehearsal now starts at 17:30 instead of 17:00.” | Relevant schedule-change information and distinct current/previous details with update evidence. No invented audience time. |
| T4 | Supplies: “Riley should bring materials sometime next week.” | Preserve original phrase and resolved broad timeframe, retaining range specificity rather than fabricating one due day. Reuse D3 for the range/uncertainty rule. |
| T5 | Academic concern: “We need to discuss Morgan's missing assignments.” No date/timeframe. | Relevant academic concern with no stated due date/timeframe. Show received date/age without inventing a meeting, deadline, or completion state. |
| T6 | Parent response: “Please reply by Oct 14 to confirm Riley's attendance.” | Parent-response action with stated due date and source evidence. |

## Adjacent Workflow Boundary Review

These checks preserve accepted capabilities without choosing routes, controls, or contracts for adjacent workflows. Where mechanics are unspecified, record a dependency rather than a made-up interaction.

| Boundary | Accepted constraint carried into this slice | Deferred work |
| --- | --- | --- |
| Owner review queue | Aged undated pending items leave the digest but remain accessible to the owner with uncertainty/evidence preserved; see A1/A4. | Queue navigation and decision interactions. Do not treat expiry as resolution or deletion. |
| Pending categories | Suggestions remain until owner decision, even when supporting items age out; potential relevance follows `Needs review`. Viewers make no category decisions; see A5 and topic requirements. | Selecting/declining categories and child assignments. |
| Filtered items and corrections | The primary digest omits confidently irrelevant items; owner can inspect and correct them. Existing correction state remains authoritative; viewers are read-only. | Inspection/correction interaction and learning. A display-only slice does not waive owner recovery capabilities. |
| Check request | Only the owner requests an immediate check; running/success/failure state and cached results remain distinguishable. | Request interaction, concurrency, and provider services. |
| Authentication/access | Authorized viewers can read all household/child views without mailbox access; revoked viewers lose access. | Sign-in/invitation mechanics, lifetime, and real-data privacy lifecycle. |

Boundary review found no need to choose a provider, framework, physical schema, or model for this document. K4 label treatment is now accepted in Decision 0010. The owner accepted the documented slice's documentation readiness under [Decision 0011](../decisions/0011-accept-cached-digest-documentation-readiness.md), with excluded behaviors and deferred interaction dependencies retained; specification writing still needs separate authorization. No mock, UI test, model evaluation, or broad test suite has been run.
