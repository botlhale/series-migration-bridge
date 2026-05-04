<div align="center">
  <img src="assets/smb_icon.png" alt="Series Migration Bridge Logo" width="350"/>
</div>

# Series Migration Bridge

A reference architecture and solution pattern for exposing internal technical frameworks through natural language using Copilot Studio, Azure-hosted FastAPI, custom connectors, and Microsoft Fabric.

## Overview

Series Migration Bridge demonstrates how to make developer-facing internal libraries and frameworks more accessible to domain experts such as economists, researchers, analysts, and other subject-matter users.

Many organizations have strong internal technical assets, but they are often easiest to use if you can:

- read technical documentation
- understand APIs
- write code in Python or similar languages
- navigate engineering-oriented workflows

That works well for developers.  
It is often not how domain experts naturally work.

This project shows a reusable pattern for creating a **natural-language access layer** over internal technical capabilities so users can:

- ask explanatory questions about internal frameworks
- get guided usage support
- invoke structured backend actions
- receive technically grounded outputs when appropriate
- safely defer to deeper workflows when confidence is low

Although the example implementation started from a migration-oriented use case, the architecture is intentionally broader and can be extended to:

- projection modeling frameworks
- international data submission workflows
- simulation systems
- case-processing libraries
- analytical and research support tooling

## Architecture diagram

The following diagram shows the conversational entry point, backend execution path, confidence-based routing, and audit layer.

![Series Migration Bridge Architecture](./assets/series_migration_bridge.png)

## Why this matters

The value of this pattern is not just code generation.

It is about reducing the gap between:

- **domain intent**, expressed in natural language
- **technical implementation**, exposed through internal libraries and developer-facing interfaces

This makes internal technical assets more:

- explainable
- discoverable
- usable
- governable
- scalable across non-developer audiences

## Architecture at a glance

The solution pattern combines:

- **Copilot Studio** for conversational orchestration
- **Knowledge sources** for documentation-grounded explanations
- **Power Platform custom connectors** for backend integration
- **Azure App Service** hosting a **FastAPI** service
- **Deterministic Tier-1 processing** for safe, structured execution
- **Optional Tier-2 routing** for more complex or low-confidence requests
- **Microsoft Fabric** for auditability and traceability
- **GitHub Actions** for CI/CD and deployment workflows

## Core interaction modes

### 1. Explanation

The agent answers questions about internal frameworks, workflows, or documentation in natural language.

Examples:

- What is this framework responsible for?
- What is this submission linked to?
- How do I perform this type of projection?
- Where is this data coming from?

### 2. Execution

The agent invokes structured backend logic for requests that can be handled deterministically.

Examples:

- Convert an expression
- Run a transformation
- Generate a structured output
- Evaluate a framework-specific request

### 3. Fallback

The agent signals low confidence and avoids inventing unsupported outputs.

Examples:

- Route to Tier 2
- Recommend escalation
- Ask for clarification
- Preserve traceability with `run_id`

## Design principles

This pattern is built around a few key ideas:

- **Natural-language accessibility** for domain experts
- **Knowledge + action** in a single agent experience
- **Confidence-aware orchestration**
- **Traceability and auditability**
- **Responsible fallback behavior**
- **Extensibility across internal technical domains**

## Responsible AI posture

This solution is intended to be assistive and governed.

It is designed to:

- distinguish between documentation-grounded answers and backend-generated execution
- avoid fabricating outputs when confidence is low
- preserve request traceability through identifiers such as `run_id`
- support escalation to deeper workflows or human review when appropriate

See [Responsible AI Notes](./docs/responsible-ai.md) for more.

## Repository contents

```text
.
├── README.md
├── docs/
│   ├── architecture-overview.md
│   ├── deep-dive.md
│   └── responsible-ai.md
└── assets/
    ├── architecture-diagram.png
    └── demo-screen.png
```

## Learn more

For a deeper explanation of the architecture, design choices, and lessons learned, see:

- [Architecture Overview](./docs/architecture-overview.md)
- [Deep Dive](./docs/deep-dive.md)
- [Responsible AI Notes](./docs/responsible-ai.md)
- [Demo Script](./docs/demo-script.md)

## Suggested demo flow

A simple live demo can show all three interaction modes:

1. **Knowledge / explanation path**  
   `According to the library handbook, what is Tier 1 responsible for in the migration workflow?`

2. **Successful execution path**  
   `Convert this FAME code: IF SALES > 100 THEN GROWTH = LOG(SALES);`

3. **Low-confidence path**  
   `Convert this FAME code: DATEOF(X) + PRICE`

This sequence demonstrates:

- knowledge-grounded explanation
- deterministic backend execution
- responsible fallback when confidence is low

## Example use cases beyond migration

This architecture can support broader internal enablement scenarios such as:

- helping economists understand projection modeling frameworks
- helping researchers navigate internal analytical libraries
- explaining how international data submissions are sourced and linked
- guiding users through framework-specific workflows
- surfacing technical outputs only when useful and appropriate

## Intended positioning

This repository should be understood as a:

- reference architecture
- solution pattern
- documentation-first project showcase
- reusable enterprise AI design example

It is not limited to a single implementation detail or one library.  
The broader goal is to demonstrate how internal technical assets can be made accessible through conversation without losing control or traceability.

## Final takeaway

The most important idea in this project is not a single tool call or conversion result.

It is the architectural pattern:

**turning developer-facing internal frameworks into domain-accessible capabilities through natural language.**
