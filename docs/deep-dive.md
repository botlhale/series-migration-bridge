# Deep Dive: Series Migration Bridge

## A conversational access layer for internal technical frameworks

Series Migration Bridge is a reference implementation that demonstrates how to expose internal technical capabilities through a conversational interface.

The pattern is designed for organizations with valuable internal libraries and frameworks that are primarily accessible to developers today, but could be made more usable for domain experts through natural language.

This implementation combines:

- Copilot Studio
- custom connectors
- Azure App Service
- FastAPI
- Microsoft Fabric
- GitHub Actions

The result is a solution pattern that supports:

- explanation of internal frameworks
- guided interaction with domain workflows
- structured backend execution
- confidence-based fallback
- auditability and traceability

## Problem statement

Many internal frameworks are technically strong but operationally inaccessible to non-developer users.

Developers can:

- read documentation
- inspect APIs
- write Python code
- compose technical workflows

Economists, researchers, analysts, and other domain users often begin with business or research questions instead:

- What does this framework do?
- How do I perform this kind of projection?
- What is this submission linked to?
- Where does this data come from?
- What transformation should be run?

The architecture is intended to bridge this gap.

## Architecture summary

At a high level, the solution works as follows:

1. A user interacts with a Copilot Studio agent in natural language.
2. The agent either:
   - answers from attached knowledge sources, or
   - invokes a custom connector action.
3. The connector calls an Azure-hosted FastAPI backend.
4. The backend performs deterministic Tier-1 processing.
5. The backend returns a structured response:
   - `status`
   - `run_id`
   - `result`
   - `next_action`
   - `reason_codes`
6. The agent formats the response appropriately.
7. Audit metadata can be written to Microsoft Fabric.

## Why a tiered model?

The tiered model allows the system to remain useful without overstating capability.

- **Tier 1**: deterministic, safe, in-scope handling
- **Tier 2**: deeper or more flexible handling for cases outside deterministic scope

This approach supports:

- predictable behavior
- responsible fallback
- clearer trust boundaries
- easier operational monitoring

## What this implementation demonstrates

This repository demonstrates several ideas.

### 1. Knowledge + action together

The agent can both:

- answer internal framework questions from documentation
- invoke backend actions for structured execution

### 2. Confidence-aware orchestration

The system distinguishes between:

- successful deterministic handling
- low-confidence cases that should escalate
- error conditions

### 3. Auditability

Each request can produce a `run_id`, allowing traceability across:

- agent response
- backend processing
- audit persistence

### 4. Extensibility

Although this implementation uses a migration-oriented example, the architecture is reusable for:

- projection modeling frameworks
- submission workflows
- simulation tools
- case-processing systems
- other internal domain libraries

## Example interaction modes

This pattern supports multiple user intents.

### Explanatory

- “What is this framework responsible for?”
- “Where is this submission sourced from?”
- “How do I perform this projection?”

### Execution-oriented

- “Convert this expression”
- “Generate the transformation”
- “Run the structured evaluation”

### Fallback-oriented

- “This request is outside deterministic scope”
- “Route to Tier 2”
- “Provide guidance for escalation”

## Technology stack

- **Copilot Studio** for conversational orchestration
- **Power Platform custom connector** for backend integration
- **Azure App Service** for hosting
- **FastAPI** for service implementation
- **Microsoft Fabric** for audit and data persistence
- **GitHub Actions** for CI/CD
- **Python** for backend logic

## Responsible AI notes

This project is designed with several control principles in mind:

- Distinguish clearly between knowledge-grounded answers and backend-generated execution
- Avoid fabricating outputs when confidence is low
- Preserve request traceability using run IDs
- Use escalation paths for ambiguous or high-complexity cases
- Treat generated outputs as assistive artifacts that should be reviewed appropriately

## Lessons learned

Some practical lessons from building and demonstrating the solution:

- users respond well when the explanation starts with their problem, not the technology
- showing both explanation and execution paths makes the pattern more compelling
- confidence gating is a feature, not a limitation
- auditability increases trust in AI-assisted workflows
- the architecture becomes more valuable when presented as a reusable pattern, not a one-off demo

## Next steps

Potential future enhancements include:

- fuller Tier-2 implementation
- richer evaluation datasets
- stronger production hardening for identity and secret management
- expanded support for additional internal frameworks
- improved observability dashboards and operational analytics

## Final takeaway

The most important idea in this repository is not the specific migration example.

It is the architectural pattern:

**making internal technical assets explainable and usable through natural language, while preserving control, traceability, and extensibility.**
