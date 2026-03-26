# Quick Start Guide

> Get from zero to a full legacy modernization assessment in 6 steps.

---

## Prerequisites

- Access to the target application's **source code repository**
- An AI assistant (Azure OpenAI, GitHub Copilot, AWS Bedrock, etc.)
- Familiarity with the codebase being assessed (or a team member who has it)

---

## Step 1 — Classify the Project

Open [phase0-classification.md](09-ai/prompts/phase0-classification.md) and run **Prompt P0.1** against your repository.

This generates [project-profile.yaml](00-project-profile/project-profile.yaml) — the single source of truth that controls assessment depth, scoring thresholds, and which prompts to run.

> **Human checkpoint**: Review the generated classification. Correct any misidentified values before proceeding.

---

## Step 2 — Build the Inventory

Run **Prompts P1.1–P1.6** from [phase1-inventory.md](09-ai/prompts/phase1-inventory.md) to populate:

| Prompt | Output |
|--------|--------|
| P1.1 — Application Inventory | [application-inventory.md](01-inventory/application-inventory.md) |
| P1.2 — Technology Matrix | (section in inventory) |
| P1.3 — Dependency Scan | [dependency-model.md](03-dependencies/dependency-model.md) |
| P1.4 — Domain Model Extraction | [domain-layer.md](02-assessment/domain-layer.md) |
| P1.5 — Cross-Cutting Concerns | (section in inventory) |
| P1.6 — Performance Baseline | [performance-baseline.md](01-inventory/performance-baseline.md) |

---

## Step 3 — Assess Code Health

Run **Prompts P2.1–P2.4** from [phase2-code-health.md](09-ai/prompts/phase2-code-health.md) to populate:

- [code-layer.md](02-assessment/code-layer.md) — Dependency graphs, dead code, complexity hotspots, refactoring candidates
- [testability.md](02-assessment/testability.md) — Test coverage assessment

**If your project is a Brownfield Enhancement (BF-ENH)**, you can stop here.

---

## Step 4 — Architecture Scoring

Run **Prompts P3.1–P3.6** from [phase3-architecture-scoring.md](09-ai/prompts/phase3-architecture-scoring.md) to populate:

| Prompt | Output |
|--------|--------|
| P3.1 — Multi-Layer Architecture | [service-layer.md](02-assessment/service-layer.md) |
| P3.2 — Event Maturity | [event-layer.md](02-assessment/event-layer.md) |
| P3.3 — Triangulation Engine | [domain-layer.md](02-assessment/domain-layer.md) |
| P3.4 — Scoring Model | [scoring-model.md](07-scoring/scoring-model.md) |
| P3.5 — Migration Readiness | [readiness.md](08-migration/readiness.md) |
| P3.6 — Portfolio Dashboard | [portfolio-dashboard.md](10-visuals/portfolio-dashboard.md) |

> **Human checkpoint**: Validate the generated scores and readiness assessment.

---

## Step 5 — Domain Discovery

Run the discovery prompts based on your technology stack:

| Phase | File | When to Run |
|-------|------|------------|
| **P4** Core Discovery | [phase4-discovery-core.md](09-ai/prompts/phase4-discovery-core.md) | Always (P4.1–P4.7) |
| **P5** Tech-Specific | [phase5-discovery-tech.md](09-ai/prompts/phase5-discovery-tech.md) | Only for detected tech stacks (P5.1–P5.10) |
| **P6** Legacy Deep Dive | [phase6-discovery-legacy.md](09-ai/prompts/phase6-discovery-legacy.md) | Full migrations only (P6.1–P6.12) |

Key outputs: [domain-mapping.md](04-domain/domain-mapping.md), [use-case-catalog.md](04-domain/use-case-catalog.md), [event-architecture.md](05-events/event-architecture.md), [integration-catalog.md](03-dependencies/integration-catalog.md)

> **Human checkpoint**: Review UNCERTAIN business rules and validate domain boundaries.

---

## Step 6 — Generate Strategy

The [scoring-model.md](07-scoring/scoring-model.md) decision matrix automatically determines the recommended migration strategy, which is written to [strategy.md](08-migration/strategy.md).

> **Human checkpoint**: Approve the final migration strategy.

---

## Execution Paths by Project Type

Not every project needs every prompt. Use the path that matches your classification:

| Classification | Path |
|---------------|------|
| **BF-ENH** (Enhancement) | P0 → P1.1 → P2 → P1.3 → Done |
| **BF-MOD** (Modernization) | P0 → P1.1 → P2 → P1.3 → P1.4 → P1.5 → P3 → P4 → P6 |
| **MIG-RH** (Rehost) | P0 → P1.1 → P2 → P1.3 → P1.6 → Done |
| **MIG-RP** (Replatform) | P0 → P1 → P2 → P3.1–P3.3 → P3.4–P3.5 → P4 (selective) |
| **MIG-RA** (Re-architect) | P0 → P1 → P2 → P3 → P4 → P5 → P6 (full) |

See [PROMPT-INDEX.md](09-ai/prompts/PROMPT-INDEX.md) for detailed execution paths.

---

## Key Files

| File | Purpose |
|------|---------|
| [ORCHESTRATION-PROMPT.md](09-ai/prompts/ORCHESTRATION-PROMPT.md) | Master guardrails — read this first |
| [PROMPT-INDEX.md](09-ai/prompts/PROMPT-INDEX.md) | Full catalog of all 39 prompts |
| [project-profile.yaml](00-project-profile/project-profile.yaml) | Generated project classification (source of truth) |
| [scoring-model.md](07-scoring/scoring-model.md) | Quantitative scoring & decision matrix |
| [strategy.md](08-migration/strategy.md) | Final migration recommendation |

---

## Tips

- **Always start with P0** — the project profile drives everything else
- **Run prompts in order** — later prompts reference earlier outputs
- **Review AI outputs** — especially business rules marked UNCERTAIN
- **One project at a time** — copy this folder per project for multi-project portfolios
- **Use depth hints** — the orchestration prompt adjusts depth based on project complexity
