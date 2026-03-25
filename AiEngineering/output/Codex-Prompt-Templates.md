# Codex Prompt Templates

Use these prompts to keep Codex focused on real code paths instead of broad repo-wide summarization.

Replace bracketed placeholders before use.

---

## 1. Safe Enhancement In One Existing API

```md
Work only in `[service-name]`.

Before editing, read:
- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `[contract-file]`

Task:
Add `[business change]` to `[API/operation name]`.

First, trace the exact request flow from entry point to persistence and list:
- controller/handler
- service classes
- domain objects
- repositories
- outbound clients
- tests covering this flow

Then implement the change across the affected layers only.

If the request or response schema changes, list downstream impact before editing.

After changes:
- update tests
- update contract files if needed
- summarize residual risks
```

## 2. Request Schema Change With Impact Analysis

```md
Work only in `[service-name]`.

I need to change request schema `[request-name]` by adding/changing `[field-name]`.

Read:
- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `[openapi or schema file]`

Do this in order:
1. Identify all classes and methods affected by this request model.
2. Classify impact into validation, service, domain, persistence, outbound contract, and tests.
3. Show the impact list.
4. Implement the code changes.
5. Update tests and docs.

Do not scan unrelated packages.
```

## 3. New API For A User Story

```md
Work only in `[service-name]`.

Read:
- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- existing APIs related to `[business capability]`

User story:
`[story text]`

First:
- identify similar existing flows and reusable domain patterns
- propose the endpoint contract
- list impacted modules

Then implement:
- controller/handler
- request/response models
- service logic
- domain logic
- persistence changes if needed
- tests
- contract documentation

Keep the implementation aligned with existing patterns in this service.
```

## 4. Service Reverse Engineering Without Shallow Summary

```md
Analyze only `[service-name]`.

Do not produce a broad architecture summary first.

Instead, generate a service knowledge pack with:
- main entry points
- top 3 to 5 business flows
- domain entities and invariants
- persistence model
- downstream dependencies
- change impact rules
- key code paths and tests

For every section, include concrete file paths.

Keep descriptions short and factual. Prefer traceability over prose.
```

## 5. Dependency Mapping For One Service

```md
Focus on `[service-name]`.

Build a local dependency map using:
- outbound client classes
- event producers/consumers
- config-based endpoints
- contract files
- tracing or runtime metadata if available

Classify each dependency as:
- runtime-confirmed
- static-only
- contract-only

Output:
- inbound callers
- outbound dependencies
- events published
- events consumed
- datastores used
- unknown or suspicious edges for manual review
```

## 6. Cross-Service Change Planning

```md
I am planning a change that starts in `[source-service]` and may affect `[target-services]`.

Do not edit code yet.

Read:
- `AGENTS.md`
- service knowledge files for impacted services
- dependency graph artifacts
- relevant contracts

Produce:
- impacted services
- impacted contracts
- likely code paths per service
- rollout risks
- test strategy
- recommended order of implementation
```

## 7. Review Prompt For Safe Code Review

```md
Review the current changes in `[service-name]`.

Focus on:
- behavioral regressions
- contract compatibility issues
- missed validation updates
- domain invariant violations
- persistence mismatches
- missing tests

List findings first with file paths and severity.
Keep summary brief.
```
