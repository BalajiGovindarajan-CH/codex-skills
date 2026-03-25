# Service Knowledge Template

Use one copy of this file per microservice. Keep it short, factual, and linked to real code paths.

Suggested location:

- `knowledge/services/[service-name]/service.md`

---

## 1. Service Identity

- Service name:
- Bounded context:
- Business capability:
- Repo path:
- Deployment unit:
- Owner team:
- Slack/Teams channel:
- On-call group:

## 2. Purpose

Describe in 3 to 5 lines:

- what problem this service solves
- who calls it
- what business outcomes it supports

## 3. Entry Points

List the main inbound paths:

- REST controllers:
- GraphQL resolvers:
- gRPC services:
- Event consumers:
- Scheduled jobs:
- Batch entry points:

For each entry point capture:

- code path
- request model
- auth model
- validation location

## 4. Core Request Flows

Document only the top 3 to 5 important flows.

### Flow: `[name]`

- Entry point:
- Main service class:
- Domain objects involved:
- Persistence classes:
- Outbound clients:
- Published events:
- Key validations:
- Business invariants:
- Main tests:

## 5. Domain Model

List the core business entities and invariants.

### Entity: `[entity-name]`

- Responsibility:
- Source class:
- Important fields:
- Lifecycle states:
- Invariants:
- Related entities:

## 6. Data Ownership

- Owned tables/collections:
- Read-only tables/collections:
- Cache usage:
- Migration mechanism:
- Data retention or audit constraints:

## 7. Contracts

- OpenAPI path:
- AsyncAPI path:
- Protobuf path:
- External schemas referenced:

For each public contract capture:

- operation/event name
- owning code path
- backward compatibility expectations
- known consumers

## 8. Dependencies

### Upstream Dependencies

- caller service or client
- interface used
- criticality

### Downstream Dependencies

- target service/system
- protocol
- purpose
- fallback/retry behavior
- dependency class
  - `runtime-confirmed`
  - `static-only`
  - `contract-only`

## 9. Change Impact Rules

When request schema changes:

- DTOs to update:
- validators to update:
- service methods to update:
- domain objects to update:
- repositories/queries to update:
- mappers to update:
- tests to update:
- downstream contracts to review:

When response schema changes:

- serializers/mappers to update:
- consumers to notify:
- contract tests to update:

When persistence changes:

- schema migration path:
- backfill required:
- compatibility concerns:

## 10. Non-Functional Constraints

- latency expectations:
- throughput profile:
- idempotency requirements:
- consistency model:
- security/privacy constraints:
- audit requirements:

## 11. Build and Validate

- local startup command:
- unit test command:
- integration test command:
- contract test command:
- lint/static analysis command:

## 12. Known Risks and Gaps

- stale documentation areas
- fragile modules
- missing tests
- unclear ownership

## 13. References

- architecture docs:
- ADRs:
- dashboards:
- tracing/service map:
- runbooks:
