# Cached Digest Display And Source Verification: Readiness

Recorded 2026-10-12. [Decision 0007](../decisions/0007-select-cached-digest-readiness-slice.md) records the owner's slice selection. This is a product-definition readiness review, not a formal specification, design, mock, test execution, or authorization to create one. [Requirements](../product-requirements.md) remain authoritative; experiment outputs are not authority.

## Selected Journey And Boundaries

An already authorized owner or household viewer opens the cached digest, reads household or child views, understands dates/actions/uncertainty and changes, and verifies supporting evidence. The review covers current-date placement on opening, household midnight, and resume, together with displayed inbox-check status. Clearly canceled dated events follow [Decision 0006](../decisions/0006-display-clearly-canceled-dated-events.md).

Inputs are already extracted items and their existing relevance/review state, child associations, source evidence, confirmed household timezone, and check history. Their creation and processing are dependencies, not new contracts selected here.

Ingestion, setup, authentication mechanics, correction learning, and unresolved cancellation cases are outside the selected slice. The accepted owner-triggered check remains a boundary with the refresh workflow; this slice reviews displayed status and results, not provider orchestration. Owner corrections, category decisions, filtered-item inspection, and the owner review queue remain accepted adjacent workflows. Reading their resulting states does not select their interactive workflows for specification.

## Authority And Existing Evidence

All scenario IDs below refer to the existing [reconciliation scenarios](reconciliation-scenarios.md). They document accepted outcomes; none demonstrates a working UI or model.

| Display concern | Authoritative rule | Existing evidence and gap |
| --- | --- | --- |
| Relevant actions, absent dates, external-detail gaps | [Action categories](../product-requirements.md#confirmed-action-categories), [body coverage](../product-requirements.md#content-coverage-for-the-first-release) | D1–D3 establish preservation of actions, missing details, and ranges. T1–T6 in the [supplemental examples](cached-digest-acceptance-examples.md#action-category-breadth) now cover every accepted action category; UI/model validation remains unperformed. |
| Shared household/child views and participant-specific details | [Date-aware digest](../product-requirements.md#date-aware-digest) | M1/M2 cover shared items, distinct times, and consistent updates. M3 is setup, outside this slice. |
| Upcoming/history placement, ranges, prominence, past-due-date labeling | [Date-aware digest](../product-requirements.md#date-aware-digest) | B1/B1a, B2/B3, B5/B6/B6a/B6b cover windows, aging, ranges, and boundaries. B3a's future setting and B7's ingestion windows are outside this slice. |
| Specificity, uncertainty, estimated dates | [Action categories](../product-requirements.md#confirmed-action-categories) | D3, B4/B4a and C1a–C1c cover labels and interpretation. Extraction itself remains outside this slice. |
| Date rollover without new mail or shifting interpreted dates | [Date-aware digest](../product-requirements.md#date-aware-digest) | C2a–C2d cover opening, midnight, resume, stable dates, and unchanged check history. |
| Review aging and retained pending items | [Topics](../product-requirements.md#configure-children-and-topics), [date-aware digest](../product-requirements.md#date-aware-digest) | A1/A4/A5 cover display expiry versus retained queue/category state. Queue access is a required adjacent dependency; its interaction is not specified here. |
| Source approval warnings on retained items | [Source lifecycle](../product-requirements.md#choose-school-sources) | S2–S4 establish warning state. Approval/reapproval processing is outside this slice. |
| Material updates and conflicts | [Date-aware digest](../product-requirements.md#date-aware-digest) | M2 covers a clear replacement; A4 covers aging of undated conflicts. V1 in the [supplemental examples](cached-digest-acceptance-examples.md#conflicts-and-source-verification) covers conflicting evidence presentation. Matching/classification evaluation is separate. |
| Clearly canceled dated events | [Date-aware digest](../product-requirements.md#date-aware-digest), [Decision 0006](../decisions/0006-display-clearly-canceled-dated-events.md) | K1–K3 in the [supplemental examples](cached-digest-acceptance-examples.md#clear-cancellations) document accepted outcomes. K4 documents approved suppression of `Ongoing` for a canceled range spanning today under [Decision 0010](../decisions/0010-suppress-ongoing-label-for-canceled-ranges.md). UI validation remains unperformed. |
| Excerpts, identifying metadata, owner original-email links, viewer access | [Verify source evidence](../product-requirements.md#verify-source-evidence), [household access](../product-requirements.md#sign-in-and-share-household-access) | D1/D2 and M2 mention evidence. V2–V5 in the [supplemental examples](cached-digest-acceptance-examples.md#conflicts-and-source-verification) cover owner/viewer evidence access, absent provider links, and revocation. |
| Check status and no implicit fetch on opening | [Date-aware digest](../product-requirements.md#date-aware-digest) | C2a/C2c cover preserved last success/failure. E1–E7 in the [supplemental examples](cached-digest-acceptance-examples.md#check-and-empty-states) cover check/empty states and success with a material update. |

## Questions Needed By This Slice

- **Product behavior:** contextual empty-digest presentation is accepted in [Decision 0008](../decisions/0008-distinguish-empty-digest-check-history.md). An empty view distinguishes no successful check yet from no currently eligible items after a successful check, while retaining check history and any later failure. Examples E1–E7 are now documented; UI validation remains pending; the decision does not change fetching behavior.
- **Validation coverage:** the full inventory is approved under [Decision 0009](../decisions/0009-approve-cached-digest-acceptance-coverage.md). [Supplemental examples](cached-digest-acceptance-examples.md) fill the documented gaps under accepted rules; K4 now follows the owner-approved label exception in Decision 0010. Documentation coverage is not executed UI/model validation.
- **Boundary review:** the [adjacent workflow review](cached-digest-acceptance-examples.md#adjacent-workflow-boundary-review) records accepted display constraints and deferred interaction dependencies. No new navigation or interaction behavior is selected. Unresolved cancellation cases remain outside the slice; existing uncertainty rules do not constitute a chosen reinstatement or cancellation-matching policy.

## Dependencies That Can Remain Open

Authentication vendor and code/session details, connector scopes and token storage, database schema, model/threshold choices, framework/hosting, and graph execution design do not need selection to review already authorized views of already extracted items. The specification must preserve accepted access, relevance, evidence, and date constraints without choosing these mechanisms.

Retention, disconnect/deletion, and invitation lifecycle decisions remain required before real-data operation of the affected flows. Model matching and correction learning need later evaluation. Their deferral here does not waive the MVP requirements. Timer/rendering/storage choices can remain implementation decisions. The slice does not introduce a schema or API contract.

## Readiness Checklist

- [x] Owner selects slice and boundaries; approval and provenance saved in Decision 0007.
- [x] Accepted rules mapped to existing scenario documentation.
- [x] Product questions, validation gaps, and adjacent workflow dependencies identified.
- [x] Implementation choices separated from behavior needed for this display-focused review.
- [x] Owner approves necessary empty/check-history behavior; provenance saved in Decision 0008.
- [x] Owner agrees acceptance coverage; supported missing examples are documented, including the separately approved K4 label exception.
- [x] Adjacent workflow boundaries and unresolved cancellation exclusions reviewed; deferred interactions are recorded without choosing new behavior.
- [x] Resolve K4 canceled-range label treatment with the owner and update its supported outcome under Decision 0010.
- [x] Owner accepts the documented readiness of this bounded slice; provenance saved in [Decision 0011](../decisions/0011-accept-cached-digest-documentation-readiness.md).
- [ ] Obtain separate authorization to write the formal specification.

Current assessment: the owner accepted documentation readiness for the selected display slice on 2026-10-12 under Decision 0011. Scope, accepted behavior, scenario coverage, adjacent boundaries, and deferred dependencies are documented; no unresolved product behavior was found to require another decision within these boundaries after K4 was resolved. This is a documentation readiness assessment, not a claim of UI/model quality or full-MVP readiness. No UI validation or broad testing has run. Formal specification writing remains separately unauthorized.

## Approval Provenance

On 2026-10-12, the owner replied `1` to select contextual empty-digest presentation. [Decision 0008](../decisions/0008-distinguish-empty-digest-check-history.md) records the approved scope, and [Date-Aware Digest](../product-requirements.md#date-aware-digest) contains the authoritative rule.

## Accepted Coverage Inventory

On 2026-10-12, the owner replied `1` to approve this full bounded inventory for documentation work; [Decision 0009](../decisions/0009-approve-cached-digest-acceptance-coverage.md) records provenance. [Supplemental examples](cached-digest-acceptance-examples.md) reuse existing cases and fill gaps under accepted behavior; it does not authorize a mock, experiment, implementation, or formal specification. New ambiguities discovered while preparing examples return to owner review before an outcome is chosen.

| Coverage group | Approved documentation work | What it enables |
| --- | --- | --- |
| Established display boundaries | Reuse D1–D3, M1/M2, applicable B1–B6b, C1a–C1c, C2a–C2d, A1/A4/A5, and S2–S4, limited to their display outcomes. | Traceable coverage of dates, child views, uncertainty, aging, and retained-source warnings without repeating accepted rules. |
| Clear cancellations | Add dated single-day and range cancellation cases, ordinary window exit, and consistent household/child evidence. Keep unresolved cancellation cases outside. | Review Decision 0006 against representative display situations. |
| Conflicting source evidence | Add a dated event with conflicting details and no clear replacement, retaining both sources and `Needs review`. | Check evidence presentation without defining matching thresholds. |
| Source verification and access | Add owner versus viewer excerpt/metadata access, original-email links where supported, and a provider with no supported original link. | Verify accepted access boundaries without selecting authentication or link implementation. |
| Check and empty states | Add never-successful and successful-but-empty views, running/failed checks with retained last success, cached items after failure, and material updates after a successful check. | Review Decision 0008 and accepted check-state presentation without changing check triggers. |
| Action-category breadth | Ensure forms, payments, schedule changes, supplies, academic concerns, and parent-response requests each have representative display evidence, reusing existing coverage where possible. | Avoid treating one form example as coverage for all accepted action types. |
| Adjacent workflow boundaries | Review display references to the owner review queue, pending categories, filtered-item inspection, correction workflows, and owner check requests. Record unresolved interaction details as dependencies rather than inventing navigation. | Confirm the slice preserves accepted capabilities while leaving adjacent workflows outside its scope. |

The approved inventory does not change the selected slice or claim validation has passed. Preparing the examples exposed K4, a canceled range crossing today; the subsequent owner-approved label exception is recorded below.

## Canceled Range Decision And Readiness Review

On 2026-10-12, the owner replied `1` to approve showing `Canceled` without `Ongoing` for a clearly canceled dated range spanning today. [Decision 0010](../decisions/0010-suppress-ongoing-label-for-canceled-ranges.md) records provenance; requirements and K4 are updated. Ordinary placement, range preservation, evidence, emphasis, history, and deletion rules are unchanged.

On 2026-10-12, the owner selected option `1` and explicitly accepted this documented readiness checklist for cached digest display and source verification, limited to documentation readiness. [Decision 0011](../decisions/0011-accept-cached-digest-documentation-readiness.md) records the acceptance and the owner's explicit instruction that formal specification writing remains deferred and requires separate authorization. Deferred interaction/technical choices remain tracked above and do not imply permission for real-data operation.
