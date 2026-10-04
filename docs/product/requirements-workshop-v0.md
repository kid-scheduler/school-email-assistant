# Requirements Workshop: Version 0 Trial

## Status

Requirements discovery is paused at the product owner's request. This preserves the Version 0 workshop trial, not an implemented release, formal specification, or approval to implement. No merge into main is part of this checkpoint.

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

## Working Hypotheses And Future Ideas

The digest can reduce review burden enough to become the primary school-information surface, and one inbox can establish usefulness despite incomplete household coverage. Neither hypothesis has been tested.

Google Calendar is the planned near-term second stage, but review/automation behavior is unresolved. Gmail, school-managed inboxes, mobile clients, notifications, shared generic category catalogs, and cross-household learning are future capabilities, not Version 0 requirements.

React, React Native, Postgres, detailed schemas, and full calendar workflow diagrams are inherited architecture proposals, not selected stack or formal contracts. LangGraph coordination and application-controlled provider access remain project guidance. No application stack or authentication provider is selected; Auth0 was discussed as a candidate only. SMS sign-in is outside Version 0.

## Unresolved At Pause

- Cancellation display: retaining an item at its original date with `Canceled` was proposed, but has not been accepted. No cancellation history rule is confirmed.
- Representative synthetic acceptance cases and UI workflow validation remain incomplete.
- Auth provider, persistent-session lifetime, code expiry/resend behavior, and invitation edge cases remain undefined.
- Data retention, deletion/disconnection behavior, evidence storage limits, and credential protection need decisions before implementation.
- Detailed relevance/uncertainty criteria, event matching, and correction-learning mechanics need validation; no model or thresholds are selected.
- Inherited data/workflow proposals need reconciliation with child assignments, body-only digest analysis, and read-only household roles before formal specification.

## Preservation Checks

This checkpoint contains documentation only. Public-safety review uses the generalized persona and synthetic examples. Whitespace and local documentation-link checks accompany the commit; there are no application tests to run.
