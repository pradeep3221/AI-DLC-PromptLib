# Prompt Index — Greenfield Platform

> Master catalog of all prompts with quick reference, execution paths, and output file mapping.

---

## Quick Reference

| ID | Prompt Name | File | Purpose |
|----|------------|------|---------|
| P0.1 | Determine Project Type | [phase0-classification.md](phase0-classification.md) | Classify project (API, SPA, Microservices, etc.) |
| P0.2 | Determine Architecture Style | [phase0-classification.md](phase0-classification.md) | Select architecture (CRUD, Clean, CQRS, etc.) |
| P0.3 | Generate Project Profile | [phase0-classification.md](phase0-classification.md) | Create project-profile.yaml |
| P0.4 | Complexity Assessment | [phase0-classification.md](phase0-classification.md) | Score complexity, calibrate design depth |
| P0.5 | Technology Decision Guide | [phase0-classification.md](phase0-classification.md) | Evaluate and recommend technology stack |
| P1.1 | Requirements Catalog | [phase1-requirements.md](phase1-requirements.md) | Extract and organize functional requirements |
| P1.2 | Non-Functional Requirements | [phase1-requirements.md](phase1-requirements.md) | Identify and quantify NFRs |
| P1.3 | Domain Model Extraction | [phase1-requirements.md](phase1-requirements.md) | Extract entities, aggregates, value objects, events |
| P1.4 | Bounded Context Identification | [phase1-requirements.md](phase1-requirements.md) | Identify bounded contexts and relationships |
| P1.5 | Use Case Catalog | [phase1-requirements.md](phase1-requirements.md) | Reverse-engineer use cases from requirements |
| P1.6 | Event Storming | [phase1-requirements.md](phase1-requirements.md) | Virtual event storming session |
| P2.1 | Architecture Decision Records | [phase2-architecture.md](phase2-architecture.md) | Generate ADRs for key decisions |
| P2.2 | Technology Selection | [phase2-architecture.md](phase2-architecture.md) | Finalize technology stack with rationale |
| P2.3 | API Design | [phase2-architecture.md](phase2-architecture.md) | Design API contracts and standards |
| P2.4 | Data Model Design | [phase2-architecture.md](phase2-architecture.md) | Design database schema and access patterns |
| P2.5 | Security Design | [phase2-architecture.md](phase2-architecture.md) | Design security architecture |
| P2.6 | Resilience & Integration Design | [phase2-architecture.md](phase2-architecture.md) | Design resilience patterns and integrations |
| P3.1 | Project Structure | [phase3-implementation.md](phase3-implementation.md) | Define solution layout and layer rules |
| P3.2 | Coding Standards & Patterns | [phase3-implementation.md](phase3-implementation.md) | Define conventions and implementation patterns |
| P3.3 | Testing Strategy | [phase3-implementation.md](phase3-implementation.md) | Design testing pyramid and coverage targets |
| P3.4 | Quality Gates & Observability | [phase3-implementation.md](phase3-implementation.md) | Define CI quality gates and observability |
| P3.5 | Deployment & Release | [phase3-implementation.md](phase3-implementation.md) | Design deployment and release strategy |
| P3.6 | CI/CD & Infrastructure | [phase3-implementation.md](phase3-implementation.md) | Design pipeline and IaC |

**Total: 23 prompts across 4 phases**

---

## Execution Order by Project Type

### SIMPLE-API
```
P0.1 → P0.2 → P0.3 → P0.4 → P0.5
→ P1.1 → P1.2 → P1.3 (light)
→ P2.1 → P2.2 → P2.3 → P2.4 → P2.5 (light)
→ P3.1 → P3.2 → P3.3 (light) → P3.5 → P3.6
```

### SPA-API
```
P0 (full)
→ P1.1 → P1.2 → P1.3 → P1.5
→ P2 (full)
→ P3 (full)
```

### MOD-MONO (Modular Monolith)
```
P0 (full)
→ P1 (full: P1.1–P1.6)
→ P2 (full)
→ P3 (full)
```

### MICRO (Microservices)
```
P0 (full)
→ P1 (full: P1.1–P1.6)
→ P2 (full) — per-service ADRs
→ P3 (full) — per-service CI/CD
```

### EVENT-DRV (Event-Driven)
```
P0 (full)
→ P1 (full: P1.1–P1.6, deep P1.6)
→ P2 (full) — emphasis on P2.6
→ P3 (full) — emphasis on P3.5 event infrastructure
```

---

## Output File Map

| Prompt | Output File(s) |
|--------|---------------|
| P0.3 | `00-project-profile/project-profile.yaml` |
| P1.1 | `01-requirements/requirements-catalog.md` |
| P1.2 | `01-requirements/nfr-catalog.md`, `01-requirements/acceptance-criteria.md` |
| P1.3 | `04-domain/domain-model.md` |
| P1.4 | `04-domain/bounded-contexts.md` |
| P1.5 | `04-domain/use-case-catalog.md` |
| P1.6 | `04-domain/event-storming.md`, `04-domain/business-rules.md` |
| P2.1 | `02-architecture/architecture-decisions.md` |
| P2.2 | `02-architecture/technology-selection.md`, `02-architecture/architecture-patterns.md` |
| P2.3 | `03-design/api-contracts.md` |
| P2.4 | `03-design/data-model.md` |
| P2.5 | `03-design/security-model.md` |
| P2.6 | `03-design/integration-design.md`, `03-design/resilience-design.md` |
| P3.1 | `05-implementation/project-structure.md` |
| P3.2 | `05-implementation/coding-standards.md`, `05-implementation/implementation-patterns.md` |
| P3.3 | `06-quality/testing-strategy.md` |
| P3.4 | `06-quality/quality-gates.md`, `06-quality/observability-design.md` |
| P3.5 | `07-delivery/deployment-strategy.md`, `07-delivery/release-planning.md` |
| P3.6 | `07-delivery/cicd-pipeline.md`, `07-delivery/infrastructure-as-code.md` |
