# Change Playbook Template

Use this file per service for repeatable change patterns. The goal is to help Codex and developers apply the same impact-analysis routine every time.

Suggested location:

- `knowledge/services/[service-name]/change-playbook.md`

---

## 1. Add Field To Existing Request

Example:

- add `customerType` to `CreateOrderRequest`

Checklist:

1. Update request DTO/schema.
2. Update validation annotations or validators.
3. Update controller or handler mapping.
4. Update service method signatures if needed.
5. Update domain objects and invariants.
6. Update persistence mapping and schema if stored.
7. Update outbound contracts if field propagates downstream.
8. Update unit, integration, and contract tests.
9. Review backward compatibility and defaulting behavior.

## 2. Add Field To Existing Response

Checklist:

1. Update response DTO and mapper.
2. Verify data source availability.
3. Review consumer compatibility.
4. Update OpenAPI or other contract specs.
5. Add or update serialization and API tests.

## 3. Change Validation Rules

Checklist:

1. Identify all validators and annotations.
2. Check business rule duplication in service/domain layers.
3. Update error contract if message or code changes.
4. Update negative-path tests.

## 4. Add New Business Logic To Existing API

Checklist:

1. Trace the current end-to-end flow.
2. Identify the correct layer for the new rule.
3. Check whether the rule affects persistence or downstream calls.
4. Update domain invariants and tests.
5. Review observability and audit needs.

## 5. Add New API For A User Story

Checklist:

1. Confirm business goal and actor.
2. Reuse existing domain concepts where possible.
3. Define request, response, and error contract.
4. Define auth and validation behavior.
5. Implement controller, service, domain, persistence, mapping, and tests.
6. Register metrics, tracing, and logging.
7. Update OpenAPI and service knowledge docs.

## 6. Change Persistence Model

Checklist:

1. Identify owned tables/entities affected.
2. Decide whether migration is backward compatible.
3. Add migration or DDL change.
4. Update repositories and mapping layers.
5. Review read/write path compatibility during rollout.
6. Add persistence and migration tests if available.

## 7. Add New Downstream Dependency

Checklist:

1. Justify why an existing dependency cannot be reused.
2. Add approved client/adapter.
3. Define timeout, retry, circuit-breaker, and fallback policy.
4. Update dependency graph metadata.
5. Add integration or contract coverage.

## 8. Publish Or Consume New Event

Checklist:

1. Define event contract and ownership.
2. Confirm idempotency and ordering assumptions.
3. Implement producer or consumer path.
4. Add schema validation and tests.
5. Update AsyncAPI and dependency graph.

## 9. Mandatory Change Summary

For every completed change, record:

- business capability impacted
- files changed
- contracts changed
- downstream impact
- test coverage updated
- rollout or migration considerations
