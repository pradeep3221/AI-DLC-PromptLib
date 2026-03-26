# Greenfield Platform

An AI-driven design and implementation framework for new .NET projects — covering architecture decisions, domain modeling, implementation standards, and delivery planning.

**Library Version:** 1.0.0 | **Last Updated:** March 2026

---

## What This Is

A structured, repeatable process for designing and building new .NET applications with data-driven architecture decisions. It combines:

- **30+ AI prompts** that guide a project through requirements, architecture, design, and implementation phases
- **25+ design templates** that capture decisions in standardized Markdown
- **A quantitative complexity engine** that calibrates architecture depth to project needs
- **Anti-hallucination guardrails** ensuring AI outputs are evidence-based with confidence levels

## Who It's For

- Solution architects designing new .NET applications
- Engineering leads planning greenfield projects
- Teams using GenAI (Azure OpenAI, AWS Bedrock) for AI-assisted design and scaffolding

---

## Repository Structure

```
greenfield-platform/
│
├── 00-project-profile/          ← Project identity & classification (YAML)
├── 01-requirements/             ← Requirements catalog, NFRs, acceptance criteria
├── 02-architecture/             ← Architecture decisions, technology selection, patterns
├── 03-design/                   ← API contracts, data model, integration design
├── 04-domain/                   ← Domain modeling, bounded contexts, event storming, use cases
├── 05-implementation/           ← Project structure, coding standards, conventions
├── 06-quality/                  ← Testing strategy, quality gates, observability, security
├── 07-delivery/                 ← CI/CD, deployment strategy, release planning, IaC
├── 08-ai/
│   ├── prompts/                 ← 30+ AI prompts (THE ENGINE — start here)
│   └── workflows/               ← Automation pipeline architecture
├── 09-visuals/                  ← Architecture diagrams & dashboard templates
├── QUICKSTART.md                ← Step-by-step getting started guide
└── README.md                    ← This file
```

---

## How It Works

### Four-Phase Execution

```
Phase 0: Classify → Profile → Complexity Calibration → Technology Decision
Phase 1: Requirements → Domain Discovery → Bounded Contexts → Use Cases
Phase 2: Architecture Decisions → API Design → Data Model → Security → Resilience
Phase 3: Implementation Standards → Testing Strategy → CI/CD → Deployment
```

**Phase 0** (Prompts P0.1–P0.5) classifies the project type and calibrates design depth.
**Phase 1** (Prompts P1.1–P1.6) captures requirements and performs domain discovery.
**Phase 2** (Prompts P2.1–P2.6) produces architecture decisions and detailed design.
**Phase 3** (Prompts P3.1–P3.6) defines implementation standards, quality gates, and delivery pipeline.

### 4-Layer Design Model

| Layer | Scope | Output |
|-------|-------|--------|
| **Layer 1: Domain** | Bounded contexts, aggregates, business rules, events | [04-domain/domain-model.md](04-domain/domain-model.md) |
| **Layer 2: Architecture** | Patterns, technology selection, ADRs | [02-architecture/architecture-decisions.md](02-architecture/architecture-decisions.md) |
| **Layer 3: API & Integration** | API contracts, integration points, protocols | [03-design/api-contracts.md](03-design/api-contracts.md) |
| **Layer 4: Quality & Delivery** | Testing, CI/CD, observability, deployment | [06-quality/testing-strategy.md](06-quality/testing-strategy.md) |

### Complexity → Architecture Depth

The complexity engine calibrates how much architecture a project actually needs:

```
Complexity Score = Domain Complexity (35%) + Integration Complexity (25%) + Scale Requirements (20%) + Team Factor (20%)
```

| Score | Recommended Architecture |
|-------|------------------------|
| 4.0–5.0 | Microservices / Event-Driven |
| 3.0–3.9 | Modular Monolith |
| 2.0–2.9 | Layered Monolith |
| < 2.0 | Simple CRUD / Minimal Architecture |

---

## Depth by Project Type

Not every project needs every prompt. The framework adapts to project complexity:

| Project Type | Prompts to Run | Depth |
|--------------|---------------|-------|
| **Simple API** | `P0 → P1.1 → P2.1–P2.3 → P3.1 → P3.3` | Minimal — CRUD focus |
| **SPA + API** | `P0 → P1 → P2 → P3.1–P3.4` | Standard — full stack |
| **Modular Monolith** | `P0 → P1 (full) → P2 (full) → P3 (full)` | Domain-driven design focus |
| **Microservices** | `P0 → P1 (full) → P2 (full) → P3 (full)` | Full architecture treatment |
| **Event-Driven** | `P0 → P1 (full, incl. P1.6) → P2 (full) → P3 (full)` | Event-first, deep domain modeling |

---

## Key Design Principles

- **Right-sized architecture** — Complexity scoring prevents over-engineering simple projects and under-engineering complex ones.
- **Domain-first** — Business domain drives architecture decisions, not technology preferences.
- **Decision records** — Every architecture choice is documented with context, rationale, and alternatives considered.
- **Evidence-based** — AI recommendations cite industry patterns, framework documentation, and project constraints.
- **Anti-hallucination guardrails** — AI must reference real framework capabilities and verified patterns.

---

## AI Prompt Library

The prompt library in [08-ai/prompts/](08-ai/prompts/) is the engine that drives the entire framework.

| File | Prompts | Scope |
|------|---------|-------|
| [ORCHESTRATION-PROMPT.md](08-ai/prompts/ORCHESTRATION-PROMPT.md) | — | Master control: guardrails, workflow, output standards |
| [phase0-classification.md](08-ai/prompts/phase0-classification.md) | P0.1–P0.5 | Project classification & profile generation |
| [phase1-requirements.md](08-ai/prompts/phase1-requirements.md) | P1.1–P1.6 | Requirements, domain discovery, bounded contexts, use cases |
| [phase2-architecture.md](08-ai/prompts/phase2-architecture.md) | P2.1–P2.6 | Architecture decisions, API design, data model, security, resilience |
| [phase3-implementation.md](08-ai/prompts/phase3-implementation.md) | P3.1–P3.6 | Project structure, testing, CI/CD, deployment, observability |

See [PROMPT-INDEX.md](08-ai/prompts/PROMPT-INDEX.md) for the full catalog and [08-ai/prompts/README.md](08-ai/prompts/README.md) for prompt-to-output file mapping.

---

## Output Templates

All design files (folders `00`–`07`, `09`) are blank templates populated by running the prompts against project requirements. Key outputs:

| Output | Template | Generated By |
|--------|----------|-------------|
| Project profile | [project-profile.yaml](00-project-profile/project-profile.yaml) | Prompt P0.3 |
| Requirements catalog | [requirements-catalog.md](01-requirements/requirements-catalog.md) | Prompts P1.1–P1.2 |
| Architecture decisions | [architecture-decisions.md](02-architecture/architecture-decisions.md) | Prompt P2.1 |
| Domain model | [domain-model.md](04-domain/domain-model.md) | Prompts P1.3–P1.5 |
| Testing strategy | [testing-strategy.md](06-quality/testing-strategy.md) | Prompt P3.3 |
| Deployment strategy | [deployment-strategy.md](07-delivery/deployment-strategy.md) | Prompt P3.5 |

---

## Getting Started

See [QUICKSTART.md](QUICKSTART.md) for a step-by-step guide, or jump straight to:

1. Read [ORCHESTRATION-PROMPT.md](08-ai/prompts/ORCHESTRATION-PROMPT.md) to understand the guardrails
2. Run Prompt P0.1 from [phase0-classification.md](08-ai/prompts/phase0-classification.md) to classify your project
