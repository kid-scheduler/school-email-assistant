# Version 0 Requirements Review

Reviewed: 2026-10-04

Baseline: tag `requirements-workshop-v0`, commit `f35d4a62bfc472c2efc33f150f73d996cb6d781e`. The findings below describe that baseline. The reconciliation status records subsequent documentation corrections and owner decisions; the immutable tag is unchanged.

## Reconciliation Status

Updated: 2026-10-04. “Resolved” means the documentation conflict is corrected, not that an application or formal spec exists.

| Finding | Status | Evidence and remaining work |
| --- | --- | --- |
| R1 | Resolved | [Digest fidelity](../langgraph-workflows.md#validate-digest-fidelity) is independent of [future calendar eligibility](../langgraph-workflows.md#future-calendar-eligibility-and-writes); [D1–D3](reconciliation-scenarios.md#digest-completeness-r1) preserve undated actions and missing external details without fabricated times. |
| R2 | Resolved | [Relationship contract](../data-model.md#relationships) and assignment collections replace single-child digest/topic assumptions; [M1–M3](reconciliation-scenarios.md#multiple-child-relationships-r2) cover participant times and consistent shared updates. Physical schema remains undecided. |
| R6 | Resolved | [Decision 0005](../decisions/0005-preserve-selected-component-direction.md) restores selected components; [AGENTS.md](../../AGENTS.md), architecture guidance, entry points, and [checkpoint status](requirements-workshop-v0.md#status) distinguish selected direction, later mobile delivery, open details, and the subsequent merge. |
| R3 | Resolved | [Source requirements](../product-requirements.md#choose-school-sources) and [S1–S4](reconciliation-scenarios.md#source-rule-lifecycle-r3) record owner decisions: 90 days only for first-time setup, two weeks for later approval/reapproval, and retained display with a warning after narrowing/disabling when no active rule covers the source. B7 confirms calendar-date backfill boundaries; deletion/disconnection retention remains separate. |
| R4 | Resolved | [A1–A5](reconciliation-scenarios.md#review-aging-and-precedence-r4) record owner decisions on digest-to-queue aging, personalized-action versus topic-ignore precedence, specific-item correction replay, changed follow-ups, and category suggestions persisting until decided. R5 confirms temporal boundaries; classification mechanics still require validation. |
| R5 | Resolved | [B1–B7](reconciliation-scenarios.md#date-range-boundaries-r5) confirm overlap/ongoing placement, inclusive source ranges, emphasis, calendar-day display/processing windows, expiry, household-timezone setup, and labeled received-date estimates. First-release history stays fixed with configuration isolated for a later setting. Cancellation remains a separate open behavior. |
| R7 | Resolved | [Overview](overview.md) links to authoritative journey rules and tuning values; [current state](../implementation/current-state.md) is a compact operational summary. Requirements retain observable success criteria; the checkpoint retains historical accepted defaults. |

## Authority And Scope

The subsequent [checkpoint review](requirements-reconciliation-review.md) verifies the main corrections and records two new open interactions: estimated-date routing and cached date-rollover behavior. Resolving R1–R7 does not establish full specification readiness.

[Product Requirements](../product-requirements.md) own current behavioral rules and acceptance criteria; [decisions](../decisions/) record accepted direction. The checkpoint describes the workshop and its provisional defaults, while the immutable tag preserves the original. Overview/state docs summarize through links. [Scenarios](reconciliation-scenarios.md) own reconciliation examples and explicitly mark pending outcomes. Stop after documentation reconciliation; do not start OpenSpec, application implementation, or skill creation.

## Findings

### R1: Date validation conflicts with digest coverage

Evidence: `docs/product-requirements.md`, Confirmed Action Categories and Content Coverage; `docs/langgraph-workflows.md`, Validate Events.

The requirements preserve undated items and incomplete body details. The proposed validator rejects missing dates and requires a start time or an all-day interpretation. Applying it to digest extraction would discard required items or invent all-day semantics. The workflow's proposal-status note already acknowledges reconciliation is needed.

Next action: distinguish digest completeness from later calendar-write eligibility. Test a required action without a deadline and an event whose arrival instructions are in an attachment. Neither should disappear or gain an invented time.

### R2: Multi-child behavior is not represented by the proposed schema

Evidence: `docs/product-requirements.md`, Configure Children And Topics and Date-Aware Digest; `docs/data-model.md`, Topic Rule, Extracted School Item, and Relationships.

Categories and events may apply to several children, with one household event and different participant details. The proposed fields and relationships still describe a single `childId`. The schema explicitly labels this as unfinished reconciliation, so this is a known contract gap rather than an implemented defect.

Next action: define the relationship contract and examples before choosing tables. Test one event applying to two children with different arrival times and one later update shared across their views.

### R3: Source approval changes lack a lifecycle contract

Evidence: `docs/product-requirements.md`, Choose School Sources and Functional Requirements.

Sources can be added or edited after setup, but behavior for existing items is undefined. Does adding a source trigger the historical scan? Does removing or narrowing a rule hide prior items, retain them, or delete content? Disconnect/deletion retention is already open, but source-rule changes are a distinct lifecycle gap.

Next action: ask for expected behavior on approval, narrowing, disabling, and reapproval. Preserve the distinction between stopping future analysis and removing already stored content.

### R4: Review-item aging and precedence are incomplete

Evidence: `docs/product-requirements.md`, Configure Children And Topics, Confirmed Action Categories, and Date-Aware Digest.

Pending categories keep potentially relevant items in `Needs review`; undated items age out after seven days. It is unclear which rule wins when an undecided category item reaches day eight. Personalized child-action exceptions also need a defined interaction with explicit ignore rules and later owner corrections.

Next action: test those boundary cases and specify precedence. Do not assume all review items share the ordinary digest retention window.

### R5: Display windows do not define date-range boundaries

Evidence: `docs/product-requirements.md`, Confirmed Action Categories and Date-Aware Digest.

Date ranges are preserved, but rules do not specify placement when a range crosses today, the four-week horizon, or the past-history boundary. Household timezone is referenced without a setup/default rule. Cancellation display is already explicitly unresolved and should remain so.

Next action: use synthetic examples for ranges crossing each boundary and an email sent near midnight in a different timezone. Ask for observable display behavior before designing date storage.

### R6: Entry-point status and authoritative stack direction need reconciliation

Evidence: `AGENTS.md`, Project Purpose; `docs/product/requirements-workshop-v0.md`, Status and Working Hypotheses And Future Ideas; `docs/product-requirements.md`, Product Surfaces.

The entry-point purpose still describes calendar connection and daily summaries without the current web-digest boundary. The snapshot says no merge into main is part of the checkpoint, although the checkpoint has since been merged. That wording needs historical context.

More materially, the snapshot and requirements label React, React Native, and Postgres as unselected proposals. The product owner explicitly requested these major components before the workshop. A preservation pass should not weaken that direction without a new human decision. Distinguish selected component technologies from undecided backend framework, schema, authentication vendor, and deployment details.

Next action: reconcile these claims with the recorded product-owner direction and update current guidance while retaining the immutable tag as historical evidence.

### R7: Repeated behavioral detail creates several maintenance locations

Evidence: `docs/product-requirements.md`, Goals, Core User Journeys, Functional Requirements, and Success Criteria; `docs/product/overview.md`, Initial Product Shape; `docs/implementation/current-state.md`, Completed.

Four-hour checks, seven-day windows, source discovery, and feedback rules recur across several documents. Restating behavior as an acceptance criterion can be useful; copying the same tuning value into overview and state logs makes drift harder to detect. The long Completed list also duplicates requirements rather than providing a compact operational summary.

Next action: choose an authoritative home for each behavior, link summaries to it, and retain acceptance criteria that add observable verification. Do not remove repetition mechanically when it serves a different reader need.

## Review Limits And Follow-Up

This is a documentation review, not a complete security review, provider capability verification, or model evaluation. Retention, authentication edge cases, matching, and learning evaluation are already recorded in `docs/open-questions.md`; their presence is not evidence that the workshop forgot them.

The next pass should prioritize R1, R2, and R6, then resolve the lifecycle and precedence examples with the product owner. Original review scope made no requirement changes. The reconciliation table above records subsequent changes. Skill creation is outside the current authorized scope.
