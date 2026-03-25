# Codex AI Engineering Template Set

This folder contains a practical template pack for teams using Codex with a large microservice estate.

Use these files as the starting point for a repo-native knowledge system:

- `AGENTS-Template.md`
  - Team-level operating instructions for Codex.
- `Service-Knowledge-Template.md`
  - Per-service knowledge pack template.
- `Dependency-Graph-Template.md`
  - Standard for capturing service dependencies from runtime, static, and contract sources.
- `Change-Playbook-Template.md`
  - Common enhancement and change patterns for a microservice.
- `Codex-Prompt-Templates.md`
  - Reusable prompts for safe, scoped development work.

Recommended usage:

1. Place a tailored `AGENTS.md` at repo root.
2. Create one service knowledge file per microservice.
3. Maintain one dependency graph artifact for the platform and one focused view per service.
4. Use the prompt templates to keep Codex tasks narrow, explicit, and code-correlated.

Design principle:

- Code is the source of truth.
- Structured metadata is the retrieval layer.
- Markdown summaries are the human guidance layer.
