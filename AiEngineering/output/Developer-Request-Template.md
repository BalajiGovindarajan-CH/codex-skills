# User Story Codex Request Template

Use this as the single story-specific file for a Jira user story or developer task.

This file combines:

- developer intake
- impact-analysis notes
- Codex execution prompt

Everything here should be specific to one user story.

Shared inputs should stay outside this file and be reused across stories:

- `AGENTS.md`
- service knowledge files
- dependency views or graph artifacts
- service-level change playbooks
- contract repositories

This file is intended to live outside the service Git repo. It is a working request artifact, not a durable code artifact.

Suggested usage:

1. Create one copy per Jira story.
2. Fill only the story-specific business and technical sections.
3. Let the developer add initial impact hints.
4. Use the embedded prompt block to run Codex.
5. Update the file with final implementation notes if needed.

If you later connect Codex to Jira, the business context, rules, and acceptance criteria can be pulled directly instead of copied manually.

---

## 1. Story Identity

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
- Jira link:
- Developer:
- local story file path:

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
- impacted endpoint path(s):

## 6. Developer Impact Analysis

The developer should add the initial impact hypothesis here before running Codex.

This is not the final truth. It is a starting point to narrow the search.

- impacted controller/handler:
- impacted service classes:
- impacted domain classes:
- impacted repositories/entities:
- impacted DB objects:
- impacted downstream clients:
- impacted topics/events:
- impacted tests:
- risks or unknowns:

Do not restate the full layer-by-layer impact workflow here. Codex should derive that from the service-level `change-playbook.md` based on the change type.

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

## 9. Story-Specific Validation Expectations

- unit tests expected:
- integration tests expected:
- contract tests expected:
- regression areas to verify:

## 10. Shared Repo Context For Codex

Codex should read these first:

- `AGENTS.md`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `knowledge/services/[service-name]/dependency-view.md`
- relevant contract file(s)

These files are common across user stories and should not be duplicated into this request file.

General instructions such as coding standards, architecture guardrails, branching, commit workflow, and validation policy should stay in `AGENTS.md`, not in this story file.

## 11. Target Repo Resolution

- service repo path:
- expected branch naming pattern:
- branch to create for this story:

Codex should use this section to find the correct local service repo under the workspace root.

## 12. Story Execution Notes

Use this section only for story-specific execution notes.

Examples:

- developer has already reviewed initial impact
- persistence migration must be deferred to a later story
- downstream contract owner must approve before merge
- only additive changes are allowed in this story

## 13. Story-Specific Codex Prompt

Copy and fill this section when prompting Codex for this story.

```md
Work only in `[service-name]`.

Read first:
- `AGENTS.md`
- `[this story request file]`
- `knowledge/services/[service-name]/service.md`
- `knowledge/services/[service-name]/change-playbook.md`
- `knowledge/services/[service-name]/dependency-view.md`
- `[contract-file-path]`

Story:
`[story ID / Jira link]`

Story file path:
`[local story request file path]`

Request type:
`[change type]`

Service repo path:
`[local service repo path]`

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

Developer impact hints:
- `[known controller or handler]`
- `[known service classes]`
- `[known persistence classes]`
- `[known downstream dependencies]`

Use the service `change-playbook.md` section that matches `[change type]`.

First, produce impact analysis from live code and the shared service artifacts.
Create or use the story branch before implementation if required by `AGENTS.md`.
Then implement the approved change, update tests, and summarize residual risks.
```

## 14. Final Implementation Notes

Fill this section after Codex work is reviewed or completed.

- actual files changed:
- actual layers impacted:
- tests updated:
- contracts updated:
- migration required:
- downstream changes required:
- open issues:

## 15. Minimum Required Fields

At minimum, the developer should provide:

- target service
- target endpoint
- user story
- business validations
- acceptance criteria
- contract diff or API spec
- whether persistence must change

Recommended additional inputs:

- initial impact hints
- downstream dependency expectations
- specific endpoint path
- known DB/table/entity impact
- local service repo path
- expected branch name

Avoid duplicating generic impact-checklist content here if that already exists in the service `change-playbook.md`.
Avoid duplicating general instructions that already exist in `AGENTS.md`.

If these are missing, Codex may still work, but the chance of shallow analysis or missed impact goes up.
