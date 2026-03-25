# Developer Request Template

Use this template when a developer wants Codex to implement or assess a change in an existing microservice.

The goal is to give Codex enough structured input to:

- find the right code flow quickly
- avoid scanning unrelated packages
- perform impact analysis before editing
- make changes consistently across layers

Suggested usage:

- copy this template into a ticket, markdown note, or prompt
- fill the required sections
- attach or reference the API spec and any contract diff

---

## 1. Request Type

- Change type:
  - existing API enhancement
  - request schema change
  - response schema change
  - new API
  - persistence change
  - dependency change
  - bug fix
- Target service:
- Target endpoint or operation:
- Story / ticket ID:

## 2. Business Context

- User story:
- Business goal:
- Actor / consumer:
- Why this change is needed:

## 3. Functional Rules

List all functional validations and business rules.

Example:

- field must be mandatory for partner users
- value must be one of supported codes
- if omitted during update, preserve the existing value
- do not publish event if status remains unchanged

## 4. Acceptance Criteria

List measurable acceptance criteria.

Example:

- API accepts the new field in request
- invalid values return `400`
- field is persisted in `[table/entity]`
- field is returned in response
- downstream event includes the new field
- existing clients remain backward compatible

## 5. Contract Inputs

- API spec path:
- Contract diff summary:
- Request schema change:
- Response schema change:
- Error contract change:
- Event schema change:
- Protobuf / AsyncAPI / OpenAPI references:

## 6. Impact Hints From Developer

Provide any known impact areas if already identified.

- impacted controller/handler:
- impacted service classes:
- impacted domain classes:
- impacted repositories/entities:
- impacted DB objects:
- impacted downstream clients:
- impacted topics/events:
- impacted tests:

## 7. Persistence Expectations

- Should data be stored in DB:
- table/entity affected:
- migration required:
- backward compatibility constraints:
- rollout concerns:

## 8. Dependency Expectations

- downstream systems likely impacted:
- upstream consumers likely impacted:
- event consumers likely impacted:
- contract owners to notify:

## 9. Validation And Testing Expectations

- unit tests expected:
- integration tests expected:
- contract tests expected:
- regression areas to verify:

## 10. Repo Context For Codex

Codex should read these first:

- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `knowledge/services/[service-name]/dependency-view.md`
- relevant contract file(s)

## 11. Required Codex Workflow

Ask Codex to follow this sequence:

1. Read the repo guidance and service knowledge files first.
2. Trace the actual code flow from entry point to persistence.
3. Produce an impact list by layer:
   - contract
   - validation
   - controller/handler
   - service
   - domain
   - mapping
   - persistence
   - downstream dependencies
   - tests
4. Flag any mismatch between docs and code.
5. Implement the change only after impact analysis.
6. Update tests and relevant docs.
7. Summarize residual risks and unverified areas.

## 12. Prompt Block For Developer

Copy and fill this section when prompting Codex.

```md
Work only in `[service-name]`.

Read first:
- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `knowledge/services/[service-name]/dependency-view.md`
- `[contract-file-path]`

Request type:
`[change type]`

Target endpoint / operation:
`[endpoint or operation]`

User story:
`[user story]`

Business rules:
- `[rule 1]`
- `[rule 2]`
- `[rule 3]`

Acceptance criteria:
- `[criteria 1]`
- `[criteria 2]`
- `[criteria 3]`

Contract change:
`[brief description of request/response/event changes]`

Persistence expectation:
`[what must be stored or changed in DB]`

First:
1. trace the current flow from entry point to persistence
2. list impacted classes and files by layer
3. list downstream dependency impact before editing

Then implement the change, update tests, and summarize residual risks.
```

## 13. Minimum Required Fields

At minimum, the developer should provide:

- target service
- target endpoint
- user story
- business validations
- acceptance criteria
- contract diff or API spec
- whether persistence must change

If these are missing, Codex may still work, but the chance of shallow analysis or missed impact goes up.
