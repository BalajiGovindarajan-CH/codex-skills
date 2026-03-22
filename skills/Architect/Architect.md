# Architect Skill

## Purpose

Produce architecture recommendations and create architecture diagrams using Draw.io or Mermaid.js.

## Input Requirements

- Always take requirements from the `Requirements` folder when it exists.
- If the `Requirements` folder is not available or the correct file is unclear, explicitly ask for the path to `requirements.md`.
- Treat the requirements as the source of truth for the problem statement and the business need to be solved.

## Workflow

### 1. Understand the Problem

- Read the problem statement first.
- Analyze the type of system being requested.
- Identify relevant system characteristics, such as:
  - API-driven
  - Composable
  - Domain-driven
  - Cloud-native
  - AI/ML-driven
  - Agentic
  - Batch-driven
  - Data pipeline
  - Configuration-driven
  - Interoperable

### 2. Identify Architecture Characteristics

- Derive and list the functional characteristics.
- Derive and list the non-functional characteristics.
- Specifically assess architecture needs such as:
  - Scalability
  - Availability
  - Observability
  - Containerization
  - Security architecture

### 3. Confirm Cloud Context

- Ask the user whether the architecture should leverage AWS or Azure for infrastructure.
- If the user does not specify a cloud preference, ask before finalizing the recommendation.

### 4. Produce the Architecture Recommendation

- Create a target system architecture based on the derived characteristics.
- Follow AWS Well-Architected Framework principles when preparing AWS-based recommendations.
- If a local AWS Well-Architected reference document exists in the same folder, use it.
- use other refernces in the same folder. Example Application Architecture.md files provides guidelines
- Summarize the recommendation clearly and pragmatically.

### 5. Record Architecture Decisions

- Include Architecture Decision Records for critical decisions.
- Use the following ADR format:
  - `ADR-01: <decision title>`
  - Problem
  - Options considered
  - Recommended option
  - Reason for recommendation

### 6. Create the Diagram

- Produce an architecture diagram using AWS services when the chosen cloud is AWS.
- Prefer Draw.io when a standards-aligned visual diagram is expected.
- Mermaid.js can be used when a lightweight diagram is sufficient or when Draw.io is not practical.
- The diagram should align with AWS architecture diagram standards when AWS is used.

## Output

- Produce the recommendation as a `.md` file in the `output` folder.
- The output should generally include:
  - Problem summary
  - Business need
  - Functional characteristics
  - Non-functional characteristics
  - Recommended architecture
  - Critical architecture decisions
  - Diagram reference or embedded Mermaid diagram

## Guardrails

- Do not produce architecture recommendations before understanding the requirements.
- Do not assume the cloud provider when that choice materially affects the design.
- Keep recommendations aligned to the stated business need and system constraints.
- Prefer explicit tradeoffs over vague best-practice statements.
