# Product Overview

## Purpose

School Email Assistant helps parents turn school inbox noise into a trusted date-aware digest. It should identify what matters, ignore school items that do not apply to the user's children, and explain those choices. Formal calendar candidates are planned for a later stage.

The Version 0 checkpoint is merged. Documentation reconciliation is complete; [review status](requirements-workshop-v0-review.md#reconciliation-status) tracks outcomes. Formal specification and implementation remain deferred.

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

The digest should become the primary review surface, reduce inbox-review burden, and avoid surprises from missed in-scope items. Evaluation timing and coverage limits live in [Confirmed Worthwhile Outcomes](../product-requirements.md#confirmed-worthwhile-outcomes).

## Initial Product Shape

A React web digest backed by an API and Postgres comes first; React Native follows later. See [selected direction](../decisions/0005-preserve-selected-component-direction.md) for open implementation choices.

- Owner connects the pilot inbox and approves configurable sources before body analysis.
- Owner selects discovered categories and assigns children explicitly.
- The digest preserves actions, dates, uncertainty, external-detail gaps, participant details, and source evidence.
- Household and child views share logical items; invited viewers have separate read-only identities.
- Owner corrections improve household classification without silently changing explicit preferences.

The authoritative behavior and tuning values live in [Core User Journeys](../product-requirements.md#core-user-journeys), particularly [Date-Aware Digest](../product-requirements.md#date-aware-digest). [Synthetic scenarios](reconciliation-scenarios.md) record confirmed lifecycle, aging, and range expectations, with future-setting and implementation details explicitly deferred.

## Working Hypotheses

- The Outlook/Hotmail pilot can prove digest value using a subset of household communication despite incomplete inbox coverage.
- Child and school attribution will help distinguish communication across schools.
- Reliably surfacing important items from high-volume school email is the primary problem.
- Preserving confirmed role-specific timing requirements will make event details more useful and trustworthy.
- The date-aware digest will reduce the need to open individual school emails enough to become the family's primary school-information review surface.

These are working hypotheses, not confirmed release boundaries.

## Setup And Source Configuration

See [Choose School Sources](../product-requirements.md#choose-school-sources) for approval and discovery, [Configure Children And Topics](../product-requirements.md#configure-children-and-topics) for categories and personalized-action review, and [Synthetic Pilot Source Configuration](../product-requirements.md#synthetic-pilot-source-configuration) for example platform and direct-teacher rules. Source trust permits processing; relevance determines visibility. These are configurable household rules, not universal school defaults.

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
