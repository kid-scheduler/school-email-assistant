# Open Questions

Grouped on 2026-10-12; subsequent owner approvals are linked below. The [accepted MVP definition](product/mvp-definition.md) summarizes scope. An answer is needed by the activity identified below; not every question blocks every specification slice.

<a id="product"></a>

## Unresolved Product Behavior

| Question | Activity needing the answer |
| --- | --- |
| How should cancellation without a usable date, uncertain event matches, reinstatement, and cancellation of a separate action behave? | Scope review of a cancellation-inclusive slice must identify which cases need further owner decisions. Clearly canceled dated-event display is accepted in [Decision 0006](decisions/0006-display-clearly-canceled-dated-events.md); storage retention is separate below. |
| What happens to retained messages, excerpts, and household data after inbox disconnection or household deletion? | Privacy/data-lifecycle definition and real-data operation of those flows. A bounded display proposal can identify this dependency without choosing retention policy. |
| How long should source evidence be retained, and what evidence must remain available beyond the accepted excerpts/metadata? | Privacy policy and evidence-lifecycle definition before real-data storage. Storage representation is an implementation choice below. |
| What session lifetime and sign-in code expiry/resend behavior should be used? | Access-flow definition and authentication implementation. Persistent sessions and one-time email codes are already accepted; their lifecycle details are open. |
| How should expired, resent, or wrong-address household invitations be handled? | Invitation-flow definition and implementation. Separate viewer identities and effective revocation are already accepted. |

## Implementation Choices

| Question | Activity needing the answer |
| --- | --- |
| Which authentication provider supports the accepted email-code flow? Auth0 is considered, not selected. | Authentication design and implementation; not consolidation of MVP scope. |
| Which exact OAuth scopes implement the initial connection? | Connector design and provider verification before connecting real inboxes. [Decision 0003](decisions/0003-use-outlook-hotmail-for-the-first-inbox.md) already requires delegated read-only access. |
| How will tokens be encrypted and rotated? | Credential-storage and connector implementation before real-data access. |
| Which model should classify/extract, and should topic matching use embeddings or structured classification alone? | AI workflow design and separately authorized evaluation. Accepted relevance/review behavior remains authoritative. |
| Which operational criteria distinguish confident relevance, confident irrelevance, and `Needs review`? | Classification contract and evaluation before reliable processing. Accepted routing/precedence rules constrain the criteria; calendar thresholds are later-stage. |
| How much evidence should each model decision store, and in what representation? | Audit/storage design, constrained by the product retention decision above and accepted user-visible evidence requirements. |
| Should `Inbox` evolve into `ProviderConnection`, or should both exist? | Provider-neutral domain/schema design. |
| Should LangGraph state use first-class tables, serialized JSON, or both? Should the graph run in the API or a separate worker? | Persistence and execution design before workflow implementation. |
| Which backend framework, web tooling, hosting provider, and deployment topology implement the [selected components](decisions/0005-preserve-selected-component-direction.md)? | Technical design and implementation planning; component direction is already accepted. |
| How do the [conceptual relationships](data-model.md#relationships) and [digest workflow](langgraph-workflows.md#email-processing-graph) map to physical schemas and processing contracts? | Schema/API/workflow design after the relevant behavior is defined. |
| What package and public repository names should be used? | Packaging and public project setup before implementation expands. |

## Validation Needs

| Question | Activity needing the answer |
| --- | --- |
| Which additional synthetic acceptance cases and UI workflow checks are needed before formal specification? | Readiness review of the owner-selected slice. Existing [reconciliation scenarios](product/reconciliation-scenarios.md) are documentation evidence, not executed UI validation. Identify gaps first; new experiments and mocks need separate authorization. |
| How will same-event matching and contextual correction learning be validated against synthetic cases? | Processing-contract review and later authorized fixture/model evaluation, especially changed obligations versus unchanged reminders. |
| How will regression fixtures be curated from real school emails without leaking private content? | Fixture-governance definition before any real-message-derived test material is introduced. Synthetic examples remain the default. |

## Later-Stage Questions

| Question | Activity needing the answer |
| --- | --- |
| When should Gmail ingestion be added? | A later provider expansion decision after the one-inbox pilot; not first-release coverage. |
| Are school-managed student inboxes connectable, and should a parent or student authorize them? | Provider feasibility and consent/product definition for expanded coverage. |
| Should calendar events be proposed for review or created under user-defined policies, and how much review precedes the first write? | Second-stage calendar product definition after digest usefulness is established. |
| Should existing calendar content inform the digest or only prevent duplicates? | Calendar integration scope and access design. |
| Which history periods should be offered, who may change them, and should the setting affect `Past due date` history? | A future history-setting definition. The first release stays fixed at seven days; see [B3a](product/reconciliation-scenarios.md#date-range-boundaries-r5). |
| Should notifications use browser/PWA, native mobile, or both; which changes warrant them? | Later notification product/platform definition. |
| How should discovered categories be generalized and reviewed for sharing without exposing private details? | Future cross-household category-sharing definition. |

## Next Decision And Readiness

On 2026-10-12, the owner selected cancellation display as the next definition activity, then approved keeping clearly canceled dated events at their scheduled dates with `Canceled`, ordinary display windows, and preserved evidence. Both replies were `1` to their respective choices; [Decision 0006](decisions/0006-display-clearly-canceled-dated-events.md) records the approved scope and provenance.

The owner then replied `1` to select cached digest display and source verification for readiness planning; [Decision 0007](decisions/0007-select-cached-digest-readiness-slice.md) records provenance and scope. The [slice readiness review](product/cached-digest-readiness.md) maps accepted rules and existing evidence, with targeted behavior and coverage gaps. The owner subsequently replied `1` to approve contextual empty-digest presentation; [Decision 0008](decisions/0008-distinguish-empty-digest-check-history.md) records that behavior. The owner then replied `1` to approve the [full coverage inventory](product/cached-digest-readiness.md#accepted-coverage-inventory); [Decision 0009](decisions/0009-approve-cached-digest-acceptance-coverage.md) records that approval. [Supplemental examples](product/cached-digest-acceptance-examples.md) document supported outcomes and adjacent boundaries. The owner then replied `1` to approve K4 label treatment: `Canceled` without `Ongoing`, recorded in [Decision 0010](decisions/0010-suppress-ongoing-label-for-canceled-ranges.md). The owner then selected `1` and explicitly accepted documentation readiness only, recorded in [Decision 0011](decisions/0011-accept-cached-digest-documentation-readiness.md); excluded product behaviors and real-data dependencies remain open above. Writing the formal specification remains unauthorized. The [readiness checklist](product/mvp-definition.md#preparation-for-a-first-formal-specification) separates slice selection, its needed behavior decisions, acceptance evidence, and later authorization to write the specification. On each owner approval, record the decision and provenance and update supported documents before proceeding to the next question.
