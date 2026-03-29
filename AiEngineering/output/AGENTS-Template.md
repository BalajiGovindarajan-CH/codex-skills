# `AGENTS.md` Template

Use this file at the root of the Codex workspace as the common instruction set for all services.

This file should be platform-wide, stable, and reused across user stories. Do not make it story-specific.

It should define:

- general guardrails
- architecture boundaries
- coding standards
- validation rules
- branching and commit workflow
- when Codex should stop and ask for confirmation

---

## Purpose

This workspace contains services that are part of the `[platform-name]` microservice landscape.

Codex should read this file first for every implementation, review, or analysis task.

Service-specific knowledge should live outside this file in:

- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `knowledge/services/[service-name]/dependency-view.md`
- service-level contract files

Story-specific request files should live outside Git, for example:

- a local story folder under the Codex workspace
- Jira attachments
- Confluence pages
- another approved task-tracking location

## Working Model

- `AGENTS.md` is the common instruction layer for all services.
- each service repo should be cloned under the workspace root when needed for the story
- service knowledge files provide service-specific context
- dependency views provide dependency and impact hints
- change playbooks provide change-type-specific impact flows
- story request files provide user-story-specific inputs
- live code, contracts, configs, and tests are the final source of truth

Codex should use shared knowledge to narrow the search, then verify all important behavior in code before editing.

## Scope Rules

- Default to the smallest safe change set.
- Do not refactor unrelated modules unless explicitly requested.
- Prefer service-scoped work over repo-wide scans.
- Do not change public contracts, schemas, topics, tables, or shared libraries without first listing impact.
- If a request may affect multiple services, complete impact analysis before editing.

## Required Read Order

For implementation tasks:

1. Read `AGENTS.md`
2. Read the story-specific request file if one is provided
3. Read the target service knowledge file
4. Read the target service change playbook
5. Read the target service dependency view
6. Read the relevant contract file(s)
7. Inspect live code and tests for the affected flow

## Workspace Layout

Recommended layout:

- workspace root
  - `AGENTS.md`
  - local story request folder, for example `.codex/story-requests/`
  - service repo folders cloned as needed

Example:

- `workspace-root/AGENTS.md`
- `workspace-root/.codex/story-requests/ABC-123.md`
- `workspace-root/customer-service/`
- `workspace-root/order-service/`

Codex should be launched from the workspace root so `AGENTS.md` is loaded consistently.

## Architecture Guardrails

- Controllers or handlers orchestrate request handling only.
- Validation should stay in the existing validation layer or established pattern.
- Business rules belong in service/domain layers.
- Persistence concerns stay in repository/DAO/entity layers.
- Mapping logic stays in dedicated mapper/translator classes when that pattern exists.
- Cross-service communication must use approved clients/adapters.
- Do not bypass existing architecture boundaries unless explicitly required and documented.

## Coding Standards

- Preserve existing package structure and naming conventions.
- Prefer explicit, readable changes over clever abstractions.
- Follow established patterns already used in the target service.
- Keep methods focused and avoid mixing orchestration with business rules.
- Add comments only where code would otherwise be difficult to follow.
- Update related tests and docs in the same change when behavior changes.

## Validation Rules

Run the smallest reliable validation set for the touched area:

- unit tests for changed logic
- integration tests for API and persistence flow
- contract tests for schema or event changes
- linting/static analysis if configured

If full validation is not possible, state exactly what was and was not verified.

## Branching And Commit Workflow

- Create or use a dedicated feature branch for each user story.
- Do not commit directly to the main branch for story work unless the team explicitly allows it.
- Before implementation, complete impact analysis and get developer review if that is part of the team workflow.
- After the developer reviews and approves the impact, implement the change on the feature branch.
- Commit only the files relevant to the approved story change.
- Use clear commit messages tied to the story or task when possible.

## First-Step Triage

At the start of a new task, Codex should determine whether the request is tied to a specific user story.

If it is a user-story-driven change:

1. ask for the path to the story-specific request file if the path was not already provided
2. read that story file first
3. identify the target service repo from the story file
4. load the service-specific knowledge files from that repo
5. perform impact analysis before making code changes

If it is not a user-story-driven change:

- proceed with normal repo analysis using `AGENTS.md` and the service-specific files

## Impact Analysis Rules

Before editing, Codex should:

- identify the inbound entry point
- trace the flow to service/domain/persistence layers
- inspect downstream dependencies and contracts
- inspect tests that cover current behavior
- use the service `change-playbook.md` for the change-type-specific checklist

Dependency classifications should use these tags where applicable:

- `runtime-confirmed`
- `static-only`
- `contract-only`

## Output Expectations For Codex

For implementation tasks, Codex should:

1. state the files and flows it inspected
2. describe impact before changing contracts
3. implement only the approved scoped change
4. update tests and relevant docs
5. summarize residual risks or unverified areas

## Escalation Triggers

Stop and ask for confirmation if:

- a contract-breaking change is required
- multiple services need coordinated edits
- data migration is needed
- there is ambiguity in business rules
- code and documentation disagree on expected behavior
- the requested change conflicts with existing architecture guardrails
