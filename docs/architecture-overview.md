# Architecture Overview

## Series Migration Bridge

Series Migration Bridge is a reference architecture for making internal technical frameworks more accessible through natural language.

It combines a conversational interface, structured backend execution, confidence-based routing, and auditability to help domain experts interact with internal capabilities that are traditionally exposed through developer-oriented libraries and documentation.

## Goal

The goal of this architecture is to reduce the gap between:

- **domain intent**, expressed in natural language by economists, researchers, analysts, or other subject-matter experts
- **technical implementation**, typically exposed through internal libraries, APIs, and developer documentation

In the example implementation, this pattern is applied to a migration-oriented use case. However, the same design can be extended to other internal frameworks such as:

- projection modeling
- international data submission
- simulation workflows
- case-processing systems
- analytical and research support tools

## High-level flow

1. A user interacts with a Copilot Studio agent in natural language.
2. The agent interprets the request and chooses one of two main paths:
   - answer from attached knowledge sources
   - invoke a backend action through a custom connector
3. The custom connector calls an Azure-hosted FastAPI service.
4. The FastAPI service processes the request through a deterministic Tier-1 path.
5. The backend returns a structured response with:
   - `status`
   - `run_id`
   - `result`
   - `next_action`
   - `reason_codes`
6. The agent presents the result to the user.
7. Audit metadata can be persisted to Microsoft Fabric.
8. If confidence is low, the request can be routed to a deeper Tier-2 path or human support workflow.

## Core components

### 1. Copilot Studio

Copilot Studio provides the conversational entry point for users.

Its role is to:

- accept natural-language requests
- answer explanatory questions from attached documentation
- invoke backend actions through custom connectors
- present structured results to the user
- communicate low-confidence or escalation outcomes clearly

This is the main user-facing layer of the architecture.

### 2. Knowledge layer

The knowledge layer supports explanation-oriented interactions.

Examples include:

- library handbooks
- framework documentation
- usage guidance
- internal terminology references

This layer allows the agent to answer questions such as:

- What is this framework responsible for?
- How do I perform a specific workflow?
- Where does this submission come from?
- What is this process linked to?

Not every valuable interaction requires code generation or backend execution.

### 3. Custom connector

The custom connector bridges Copilot Studio to backend APIs.

Its role is to:

- define the action contract
- pass structured request parameters to the backend
- return structured responses to the agent

This provides a governed and reusable integration point between conversational UX and technical services.

### 4. Azure-hosted FastAPI backend

The FastAPI service provides structured execution.

Its role is to:

- receive requests from the custom connector
- validate and process structured inputs
- execute deterministic Tier-1 logic
- return machine-readable result objects
- support audit logging and traceability

In the example implementation, the backend is hosted on Azure App Service.

### 5. Tier-1 deterministic processing

Tier 1 is the deterministic processing layer.

Its purpose is to handle requests that are:

- in scope
- well understood
- safe to process consistently

For those requests, the system returns a usable result.

The exact result depends on the capability being exposed.  
Examples may include:

- code generation
- transformation results
- structured evaluations
- metadata extraction
- framework-specific outputs

### 6. Tier-2 fallback or escalation

Tier 2 represents the path for requests that should not be answered deterministically.

This path may include:

- deeper reasoning workflows
- additional context retrieval
- more advanced processing services
- human review or technical support

The purpose of Tier 2 is not to replace Tier 1, but to complement it when confidence is low.

### 7. Microsoft Fabric audit layer

Microsoft Fabric supports auditability and traceability.

Example audit metadata may include:

- `run_id`
- `status`
- `tier`
- `reason_codes`
- `created_by`
- timestamps

This helps support:

- monitoring
- operational review
- troubleshooting
- governance and trust

### 8. DevOps and observability

The architecture also includes a supporting operational layer.

Typical elements include:

- GitHub for source control
- GitHub Actions for CI/CD
- Azure deployment targets
- application logging
- health and runtime monitoring

This ensures the solution pattern can be maintained as an operational system, not just demonstrated as a prototype.

## Interaction modes

This architecture supports three main interaction modes.

### Explanation

The user asks a question about a framework, workflow, or concept.

Examples:

- What does this framework do?
- What is this submission linked to?
- How do I perform this type of projection?

The response is grounded in documentation or handbook knowledge.

### Execution

The user requests a structured operation.

Examples:

- convert an expression
- run a transformation
- generate a deterministic output

The agent invokes the backend and returns the result.

### Fallback

The user requests something outside deterministic scope.

In this case, the system should:

- communicate low confidence clearly
- preserve traceability
- recommend escalation or a deeper workflow
- avoid inventing unsupported outputs

## Why this architecture matters

This architecture matters because many internal technical assets are highly valuable but difficult for non-developer users to access directly.

A conversational layer can help make those assets:

- more discoverable
- more explainable
- easier to use
- safer to scale across non-developer audiences

The broader value is not just a single implementation.  
It is the reusable pattern for exposing internal frameworks through natural language while preserving control and auditability.

## Final takeaway

Series Migration Bridge should be understood as a reference architecture for:

- natural-language access to internal technical capabilities
- deterministic execution where appropriate
- clear fallback where confidence is low
- traceability across the interaction lifecycle

It is a pattern for making internal developer-facing frameworks more accessible to domain experts without losing governance.
