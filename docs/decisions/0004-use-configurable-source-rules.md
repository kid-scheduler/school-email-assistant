# 0004: Use Configurable Source Rules

## Status

Accepted

## Context

The generalized pilot examples include a communication platform with many sender addresses on one synthetic domain and a direct teacher using an example school domain. Other schools may use different platforms, domains, sender conventions, or individual addresses. Encoding the pilot's domains or vendor behavior as universal product logic would make the product specific to one household.

## Decision

Trusted-source matching is household configuration, not hardcoded school or vendor behavior. The first release supports owner-approved exact sender-address and sender-domain rules. Different schools and communication systems may use different rule granularities in the same household.

The product may suggest a rule based on observed metadata and explain its breadth, but the owner remains authoritative. Platform-domain approval and the direct-teacher example are synthetic pilot configurations and acceptance cases, not universal defaults.

## Consequences

- New schools can be configured without code changes when exact-address or domain rules are sufficient.
- Broad source trust remains separate from relevance filtering and digest inclusion.
- The data model and workflow use provider-neutral source rules.
- Exact-address and domain rules are sufficient for v1. Additional rule types, such as address patterns or stable sender identifiers, are deferred until examples demonstrate a need.

## Lifecycle Follow-Up

Owner decisions on 2026-10-04 confirm setup-only historical discovery, bounded backfill for later approval/reapproval, and retained display with a warning after narrowing/disabling. The authoritative windows and behavior live in [Choose School Sources](../product-requirements.md#choose-school-sources), with [synthetic lifecycle outcomes](../product/reconciliation-scenarios.md#source-rule-lifecycle-r3). Stopping future analysis is distinct from deleting stored content.
