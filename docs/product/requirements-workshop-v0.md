# Requirements Workshop: Version 0 Trial

## Status

At the original checkpoint, requirements discovery was paused and merging was outside that checkpoint's scope. The checkpoint was subsequently merged into main (merge commit `95d76c2`). The immutable `requirements-workshop-v0` tag preserves the original record. This working copy now includes authorized documentation reconciliation, not formal specification or implementation approval; see [review status](requirements-workshop-v0-review.md#reconciliation-status).

[Product Requirements](../product-requirements.md) retain workshop detail; [Open Questions](../open-questions.md) retain unresolved decisions. The human product owner remains authoritative. Proposals do not become requirements without acceptance.

## Public-Safe Pilot Persona

A parent or guardian manages communication for children at different schools and educational stages. Messages are spread across household inboxes and arrive through school platforms and directly from teachers. Household members manually review messages and transfer noticed obligations to a shared calendar.

Generalized problem cases are late awareness of a school event, missed awareness of a required student activity, and confusion between student arrival and audience start times. No exact grades, household account assignments, real names, school identifiers, original subjects, sender identifiers, or verbatim school messages are retained. Example addresses/domains are synthetic.

The persona motivates child-aware filtering, role-specific times, and household viewing. It does not constrain the product to one family's schools or conventions.

## Confirmed Requirements

- A read-only, date-aware web digest is the first release; calendar connections/writes, proactive notifications, and completion tracking are outside it.
- One owner-controlled personal Outlook/Hotmail inbox contributes messages through Microsoft Graph. Messages available only in other inboxes are outside coverage.
- Owners approve exact-address or domain source rules before body analysis. Source trust is separate from relevance; confidently irrelevant messages are omitted, uncertain items remain in `Needs review`.
- Categories are discovered from approved-source messages and explicitly assigned to children or `All children`. Newly proposed categories and personalized child-action exceptions remain reviewable.
- Email bodies are the content boundary. Missing external details, source excerpts, and lookup metadata remain visible; attachment and linked-page analysis are deferred.
- Dates preserve source specificity and interpretation uncertainty. Relative dates use the source email date; student and audience times are not collapsed.
- Clear replacements update existing items with evidence; unresolved conflicts retain both sources in `Needs review`.
- Separate owner/viewer identities use one-time email codes. Viewers have read-only access to all household and child views. Invitations and revocation are required; mailbox authorization is separate.
- Owner corrections update the digest and inform household-scoped classification. Broader preference changes require approval; cross-household learning is deferred.
- Usefulness is judged qualitatively: less inbox-review burden, the digest becoming the primary review surface, and no surprises caused by missed in-scope events. This is an evaluation goal, not an accuracy claim about a system that has not been built.

## Provisional Trial Defaults

These defaults were accepted for the trial, but remain tunable after evaluation. Their provisional status does not undo the accepted Version 0 behavior.

| Area | Accepted Version 0 Default |
| --- | --- |
| Historical discovery | 90 days of metadata, followed by bodies matching owner-approved source rules |
| Upcoming window | Four weeks, with the first two emphasized |
| History | Previous seven days, clearly separated from upcoming items |
| Undated items | Seven days after receipt, labeled by received date and age, not a fabricated deadline |
| Passed deadlines | Separate `Past due date` section for seven days, without claiming incomplete status |
| Freshness | Four-hour configurable background checks plus owner-triggered checks; opening the app displays cached data |
| Pilot evaluation | Two weeks of normal use, extended if too few events occur to assess coverage |

Current reconciliation follow-up: the owner confirmed fixed seven-day history in the first release, with a separate configuration value so a user setting can be added later. Details of that future setting are deferred. The table above preserves workshop defaults. See [current digest requirements](../product-requirements.md#date-aware-digest).

## Working Hypotheses And Future Ideas

The digest can reduce review burden enough to become the primary school-information surface, and one inbox can establish usefulness despite incomplete household coverage. Neither hypothesis has been tested.

Google Calendar is the planned near-term second stage, but review/automation behavior is unresolved. Gmail, school-managed inboxes, mobile clients, notifications, shared generic category catalogs, and cross-household learning are future capabilities, not Version 0 requirements.

React web first, React Native later, a backend API, and Postgres are selected product-owner component direction, restored in [Decision 0005](../decisions/0005-preserve-selected-component-direction.md). Detailed schemas, backend framework, deployment topology, hosting, and authentication vendor remain undecided. Full calendar workflows are future-stage proposals. LangGraph coordination and application-controlled provider access remain project guidance. Auth0 is a candidate only; SMS sign-in is outside Version 0.

## Unresolved At Pause

- Cancellation display: retaining an item at its original date with `Canceled` was proposed, but has not been accepted. No cancellation history rule is confirmed.
- Representative synthetic reconciliation cases are now documented; UI workflow validation remains incomplete.
- Auth provider, persistent-session lifetime, code expiry/resend behavior, and invitation edge cases remain undefined.
- Data retention, deletion/disconnection behavior, evidence storage limits, and credential protection need decisions before implementation.
- Detailed relevance/uncertainty criteria, event matching, and correction-learning mechanics need validation; no model or thresholds are selected.
- Conceptual child assignments and digest/calendar validation separation are reconciled; storage design and detailed workflows remain proposals. Source lifecycle is now confirmed in [synthetic scenarios](reconciliation-scenarios.md); review aging/precedence and date boundaries are also confirmed.

## Preservation Checks

This checkpoint contains documentation only. Public-safety review uses the generalized persona and synthetic examples. Whitespace and local documentation-link checks accompany the commit; there are no application tests to run.
