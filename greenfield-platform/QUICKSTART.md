# Quick Start Guide

> Get from zero to a full greenfield architecture plan in 6 steps.

---

## Prerequisites

- Clear understanding of the **business problem** being solved
- An AI assistant (Azure OpenAI, GitHub Copilot, AWS Bedrock, etc.)
- Stakeholder access for requirements validation

---

## Step 1 — Classify the Project

Open [phase0-classification.md](08-ai/prompts/phase0-classification.md) and run **Prompt P0.1** against your project brief.

This generates [project-profile.yaml](00-project-profile/project-profile.yaml) — the single source of truth that controls design depth, architecture recommendations, and which prompts to run.

> **Human checkpoint**: Review the generated classification. Correct any misidentified values before proceeding.

---

## Step 2 — Capture Requirements

Run **Prompts P1.1–P1.2** from [phase1-requirements.md](08-ai/prompts/phase1-requirements.md) to populate:

| Prompt | Output |
|--------|--------|
| P1.1 — Requirements Catalog | [requirements-catalog.md](01-requirements/requirements-catalog.md) |
| P1.2 — Non-Functional Requirements | [nfr-catalog.md](01-requirements/nfr-catalog.md) |

---

## Step 3 — Domain Discovery

Run **Prompts P1.3–P1.6** from [phase1-requirements.md](08-ai/prompts/phase1-requirements.md) to populate:

| Prompt | Output |
|--------|--------|
| P1.3 — Domain Model Extraction | [domain-model.md](04-domain/domain-model.md) |
| P1.4 — Bounded Context Identification | [bounded-contexts.md](04-domain/bounded-contexts.md) |
| P1.5 — Use Case Catalog | [use-case-catalog.md](04-domain/use-case-catalog.md) |
| P1.6 — Event Storming | [event-storming.md](04-domain/event-storming.md) |

**If your project is a Simple API**, you can skip P1.4–P1.6 and proceed to architecture.

> **Human checkpoint**: Validate domain boundaries and business rules with domain experts.

---

## Step 4 — Architecture Design

Run **Prompts P2.1–P2.6** from [phase2-architecture.md](08-ai/prompts/phase2-architecture.md) to populate:

| Prompt | Output |
|--------|--------|
| P2.1 — Architecture Decisions | [architecture-decisions.md](02-architecture/architecture-decisions.md) |
| P2.2 — Technology Selection | [technology-selection.md](02-architecture/technology-selection.md) |
| P2.3 — API Design | [api-contracts.md](03-design/api-contracts.md) |
| P2.4 — Data Model Design | [data-model.md](03-design/data-model.md) |
| P2.5 — Security Design | [security-model.md](03-design/security-model.md) |
| P2.6 — Resilience & Integration Design | [integration-design.md](03-design/integration-design.md) |

> **Human checkpoint**: Review architecture decisions and technology selections with the team.

---

## Step 5 — Implementation Planning

Run **Prompts P3.1–P3.6** from [phase3-implementation.md](08-ai/prompts/phase3-implementation.md) to populate:

| Prompt | Output |
|--------|--------|
| P3.1 — Project Structure | [project-structure.md](05-implementation/project-structure.md) |
| P3.2 — Coding Standards | [coding-standards.md](05-implementation/coding-standards.md) |
| P3.3 — Testing Strategy | [testing-strategy.md](06-quality/testing-strategy.md) |
| P3.4 — Quality Gates | [quality-gates.md](06-quality/quality-gates.md) |
| P3.5 — Deployment Strategy | [deployment-strategy.md](07-delivery/deployment-strategy.md) |
| P3.6 — CI/CD Pipeline | [cicd-pipeline.md](07-delivery/cicd-pipeline.md) |

> **Human checkpoint**: Approve implementation standards and delivery pipeline.

---

## Step 6 — Scaffold & Build

Use the generated architecture and design documents to:

1. Scaffold the solution structure per [project-structure.md](05-implementation/project-structure.md)
2. Configure CI/CD per [cicd-pipeline.md](07-delivery/cicd-pipeline.md)
3. Implement domain model per [domain-model.md](04-domain/domain-model.md)
4. Build APIs per [api-contracts.md](03-design/api-contracts.md)

---

## Execution Paths by Project Type

Not every project needs every prompt. Use the path that matches your classification:

| Classification | Path |
|---------------|------|
| **SIMPLE-API** | P0 → P1.1–P1.2 → P2.1–P2.3 → P3.1 → P3.3 → P3.5 |
| **SPA-API** | P0 → P1.1–P1.3 → P2.1–P2.5 → P3 (full) |
| **MOD-MONO** (Modular Monolith) | P0 → P1 (full) → P2 (full) → P3 (full) |
| **MICRO** (Microservices) | P0 → P1 (full) → P2 (full) → P3 (full) |
| **EVENT-DRV** (Event-Driven) | P0 → P1 (full, incl. P1.6 Event Storming) → P2 (full) → P3 (full) |

See [PROMPT-INDEX.md](08-ai/prompts/PROMPT-INDEX.md) for detailed execution paths.

---

## Key Files

| File | Purpose |
|------|---------|
| [ORCHESTRATION-PROMPT.md](08-ai/prompts/ORCHESTRATION-PROMPT.md) | Master guardrails — read this first |
| [PROMPT-INDEX.md](08-ai/prompts/PROMPT-INDEX.md) | Full catalog of all prompts |
| [project-profile.yaml](00-project-profile/project-profile.yaml) | Generated project classification (source of truth) |
| [architecture-decisions.md](02-architecture/architecture-decisions.md) | Architecture Decision Records |
| [domain-model.md](04-domain/domain-model.md) | Domain model & bounded contexts |

---

## Tips

- **Always start with P0** — the project profile drives everything else
- **Run prompts in order** — later prompts reference earlier outputs
- **Right-size the architecture** — don't build microservices for a CRUD app
- **One project at a time** — copy this folder per project for multi-project portfolios
- **Validate with domain experts** — AI extracts patterns, humans validate business intent
