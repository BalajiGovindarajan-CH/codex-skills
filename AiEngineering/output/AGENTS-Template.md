# `AGENTS.md` Template

Use this file at the root of a repository so Codex has stable instructions before reading large amounts of code.

---

## Purpose

This repository contains `[system-name]`, which is part of the `[platform-name]` microservice landscape.

Codex should use this file as the first source of project-specific instructions before making changes.

## Scope Rules

- Default to the smallest possible change set.
- Do not refactor unrelated modules unless explicitly requested.
- Do not change public contracts, schemas, topics, table definitions, or shared libraries without listing the impact first.
- If the request affects multiple services, finish impact analysis before editing.
- Prefer service-scoped work over repo-wide scans.

## First Files To Read

For any task, read these before broader exploration:

1. `README.md`
2. `docs/architecture.md`
3. `knowledge/services/[service-name]/service.yaml`
4. `knowledge/services/[service-name]/change-playbook.md`
5. Contract files:
   - `openapi.yaml`
   - `asyncapi.yaml`
   - `proto/*.proto`

## Architecture Boundaries

- Controllers or handlers should only orchestrate request handling.
- Business rules belong in service/domain layers.
- Persistence concerns stay in repository/DAO layers.
- Mapping logic should stay in dedicated mapper/translator classes.
- Cross-service communication must go through approved clients/adapters.

## Change Policy

When changing an existing API:

1. Identify request/response contract changes.
2. Trace impacted validation, service, domain, persistence, mapping, and tests.
3. Check downstream consumers and published events.
4. Update documentation and tests in the same change.

When creating a new API:

1. Reuse existing domain concepts where possible.
2. Confirm auth, validation, idempotency, and error contract.
3. Add integration and contract coverage where applicable.

## Dependency Analysis Rules

Before editing, inspect:

- inbound entry point
- service layer path
- domain invariants
- persistence path
- outbound dependencies
- tests covering the current behavior

Classify dependencies as:

- `runtime-confirmed`
- `static-only`
- `contract-only`

## Coding Standards

- Preserve existing package structure and naming conventions.
- Prefer explicit, readable changes over clever abstractions.
- Keep methods focused and avoid mixing orchestration with business rules.
- Add comments only where the code would otherwise be hard to follow.

## Validation Expectations

Run the smallest reliable validation set for the touched area:

- unit tests for changed logic
- integration tests for API and persistence flow
- contract tests for schema or event changes
- linting/static analysis if configured

If full validation is not possible, state exactly what was and was not verified.

## Output Expectations For Codex

For implementation tasks, Codex should:

1. State the files and flows it inspected.
2. Describe impact before changing contracts.
3. Make the code changes.
4. Update tests and relevant docs.
5. Summarize residual risks or unverified areas.

## Escalation Triggers

Stop and ask for confirmation if:

- a contract-breaking change is required
- multiple services need coordinated edits
- data migration is needed
- there is ambiguity in business rules
- the code and docs disagree on expected behavior
