# Reconciliation Checkpoint Review

Reviewed: 2026-10-04

Baseline: reconciliation following `requirements-workshop-v0`, preserved at commit `10d49aa` on `stage/requirements-reconciliation-v1` and annotated tag `requirements-reconciliation-v1`. This is an independent documentation review, not an application test or approval to implement.

## Reconciliation Status

Updated: 2026-10-04. Findings below describe the checkpoint; this table records subsequent owner decisions.

| Finding | Status | Evidence and remaining work |
| --- | --- | --- |
| C1 | Resolved | Owner selected review for every received-date fallback estimate. [Temporal labels](../product-requirements.md#confirmed-action-categories), [workflow routing](../langgraph-workflows.md#validate-digest-fidelity), success criteria, and [C1 scenarios](reconciliation-scenarios.md#estimated-date-routing-c1) show paired review/estimate labels, preserve range breadth, and prohibit `Exact date` on a fallback-derived single date. |
| C2 | Resolved | Owner selected calculation from stored items on display, at household-local midnight for active views, and on resume. [Digest requirements](../product-requirements.md#date-aware-digest), [display workflow](../langgraph-workflows.md#date-aware-display), and [C2 scenarios](reconciliation-scenarios.md#cached-date-rollover-c2) update placement independently of inbox checks while preserving check status and interpreted dates. |

## Verified Corrections

- Digest fidelity preserves undated and incomplete items independently of calendar-write eligibility.
- Conceptual category and item assignments support multiple children and participant-specific details.
- React web, backend API, Postgres, and later React Native are restored as selected direction.
- Source-rule changes distinguish continued display of historical evidence from permission for future analysis.
- Explicit item corrections survive replay; materially changed obligations can return to review.
- Date-range and calendar-day scenarios provide concrete expected outcomes.
- Overview and current state link to authoritative detail instead of repeating the full requirements.

The original R1–R7 findings are reconciled at the documentation level. The following interactions emerged from reviewing the resulting contracts. Their current status is recorded above.

## C1: Estimated Date Labels And Review Routing

Evidence: `docs/product-requirements.md`, Confirmed Action Categories and Date-Aware Digest; `docs/langgraph-workflows.md`, Validate Digest Fidelity; scenario B4a.

The received-timestamp fallback requires `Estimated from received date` and prohibits treating the result as confidently resolved. Other rules route uncertain temporal interpretations to `Needs review`, while the digest's enumerated temporal labels omit the new estimate label. The documents do not explicitly say whether every estimate enters review or how the estimate label combines with specificity labels.

Decision needed: always route fallback estimates to review, or allow primary-digest placement with an estimate label under explicitly defined conditions. Then align the label list, workflow routing, success criteria, and B4a. Do not resolve this by assuming that a computed date is reliable evidence of the intended date.

## C2: Calendar-Day Transitions Versus Cached Rendering

Evidence: `docs/product-requirements.md`, Date-Aware Digest and undated expiry; `docs/langgraph-workflows.md`, Digest Refresh Graph; scenarios B5 and B6.

Items must change placement or age out at household-local midnight, but app opening displays cached data and does not check the inbox. The graph renders and persists a digest during inbox refresh, scheduled every four hours. Reusing yesterday's rendered output could violate today's windows even with no new messages.

Decision needed: calculate placement from stored items at display time, or define a local date-rollover refresh independent of inbox checks. Define what happens for a view left open across midnight. This is an observable freshness contract; it does not require selecting a frontend timer or database representation now.

## Process Observations

- Numbered alternatives and an explicit next step reduced the effort needed to answer.
- The task stopped when its assigned findings were reconciled and distinguished remaining questions from that completion claim.
- The history-setting discussion briefly recommended expanding v1; the owner chose deferred delivery. Recommendations should account for the existing MVP boundary.
- Documentation checks establish formatting and link validity, not semantic agreement or runtime behavior.

## Checkpoint Scope

At the checkpoint, C1 and C2 were explicitly open. This follow-up resolves only those interactions with the owner and stops afterward, without reopening settled source, child-assignment, or window-counting decisions. The original V0 tag remains unchanged.
