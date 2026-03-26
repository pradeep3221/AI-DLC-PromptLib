# Legacy Modernization Platform

An AI-driven assessment framework for legacy .NET projects — covering brownfield enhancements, modernization, and full migration (rehost, replatform, re-architect).

**Library Version:** 4.0.0 | **Last Updated:** March 2026

---

## What This Is

A structured, repeatable process for evaluating legacy .NET codebases and producing data-driven migration decisions. It combines:

- **39 AI prompts** that analyze a codebase across code, architecture, domain, and event layers
- **30 assessment templates** that capture findings in standardized Markdown
- **A quantitative scoring engine** that converts findings into migration strategy recommendations
- **Anti-hallucination guardrails** ensuring AI outputs are evidence-based with confidence levels

## Who It's For

- Solution architects assessing legacy .NET applications
- Engineering leads planning modernization or migration projects
- Teams using GenAI (Azure OpenAI, AWS Bedrock) for automated codebase analysis

---

## Repository Structure

```
legacy-modernization-platform/
│
├── 00-project-profile/          ← Project identity & classification (YAML)
├── 01-inventory/                ← Application catalog & performance baseline
├── 02-assessment/               ← 10 assessment files (code, service, event, domain layers + cross-cutting)
├── 03-dependencies/             ← Dependency model, integrations, anti-corruption layers
├── 04-domain/                   ← Domain mapping, use cases, SPs, state machines, UI behavior
├── 05-events/                   ← Event architecture & maturity
├── 06-risk/                     ← Risk assessment matrix
├── 07-scoring/                  ← Quantitative scoring engine & decision matrix
├── 08-migration/                ← Readiness assessment & migration strategy
├── 09-ai/
│   ├── prompts/                 ← 39 AI prompts (THE ENGINE — start here)
│   └── workflows/               ← Automation pipeline architecture
├── 10-visuals/                  ← Portfolio dashboard & Mermaid diagram templates
├── QUICKSTART.md                ← Step-by-step getting started guide
└── README.md                    ← This file
```

---

## How It Works

### Two-Phase Execution

```
Phase 0: Classify → Inventory → Code Health → Architecture Scoring → Migration Readiness
Phase 1: Domain Discovery → Business Rules → State Machines → Integrations → Deep Extraction
```

**Phase 0** (Prompts P0–P3) classifies the project and assesses its technical health.
**Phase 4–6** (Prompts P4.1–P6.12) performs deep domain discovery, extracting business rules from code, stored procedures, UI, middleware, config, and vendor customizations.

### 4-Layer Assessment Model

| Layer | Scope | Output |
|-------|-------|--------|
| **Layer 1: Code** | Complexity, dead code, testability, coupling | [02-assessment/code-layer.md](02-assessment/code-layer.md) |
| **Layer 2: Service** | Service catalog, API contracts, coupling analysis | [02-assessment/service-layer.md](02-assessment/service-layer.md) |
| **Layer 3: Event** | Event maturity (L1–L4), producers/consumers, DLQ | [02-assessment/event-layer.md](02-assessment/event-layer.md) |
| **Layer 4: Domain** | Bounded contexts, aggregates, business rules | [02-assessment/domain-layer.md](02-assessment/domain-layer.md) |

### Scoring → Strategy Decision

The scoring engine combines three dimensions into a single decision score:

```
Decision Score = Code Health (35%) + Architecture Fitness (35%) + Migration Readiness (30%)
```

| Score | Recommended Strategy |
|-------|---------------------|
| 4.0–5.0 | Rehost (Lift & Shift) |
| 3.0–3.9 | Replatform |
| 2.0–2.9 | Refactor + Modernize |
| < 2.0 | Re-architect |

---

## Depth by Project Type

Not every project needs every prompt. The framework adapts to project intent:

| Project Type | Prompts to Run | Depth |
|--------------|---------------|-------|
| **Brownfield Enhancement** | `0.0 → 0.1 → 0.2 → 0.3 → 0.7 (light)` | Quick hotspot analysis |
| **Brownfield Modernization** | `0.0 → 0.1–0.6 → 0.7–0.13 → 1.1–1.29` | Full assessment + domain discovery |
| **Migration — Rehost** | `0.0 → 0.1 → 0.2 → 0.3 → 0.6 → 0.12` | Infrastructure focus |
| **Migration — Replatform** | `0.0 → 0.1–0.6 → 0.7 → 0.12 → 1.21–1.22` | Platform + config changes |
| **Migration — Re-architect** | `0.0 → 0.1–0.13 → 1.1–1.29 (all)` | Full transformation |

---

## Key Design Principles

- **Confidence tagging** — Every extracted rule is labeled HIGH / MEDIUM / LOW / UNCERTAIN. UNCERTAIN rules require human validation.
- **Anti-hallucination guardrails** — AI must verify files exist, cite file paths and line numbers, never fabricate metrics.
- **Triangulation** — Domain, service, and event layers are cross-referenced to detect misalignment.
- **Evidence-based** — No business rule is accepted without a source file, line number, and code snippet.

---

## AI Prompt Library

The prompt library in [09-ai/prompts/](09-ai/prompts/) is the engine that drives the entire framework.

| File | Prompts | Scope |
|------|---------|-------|
| [ORCHESTRATION-PROMPT.md](09-ai/prompts/ORCHESTRATION-PROMPT.md) | — | Master control: guardrails, workflow, output standards |
| [phase0-classification.md](09-ai/prompts/phase0-classification.md) | P0.1–P0.5 | Project classification & profile generation |
| [phase1-inventory.md](09-ai/prompts/phase1-inventory.md) | P1.1–P1.6 | Inventory, tech matrix, dependencies, domain model, performance |
| [phase2-code-health.md](09-ai/prompts/phase2-code-health.md) | P2.1–P2.4 | Dependency graphs, dead code, complexity, refactoring |
| [phase3-architecture-scoring.md](09-ai/prompts/phase3-architecture-scoring.md) | P3.1–P3.6 | 4-layer model, event maturity, scoring, readiness, portfolio |
| [phase4-discovery-core.md](09-ai/prompts/phase4-discovery-core.md) | P4.1–P4.7 | Core domain: multi-tech scan, WCF, VB.NET, WPF, SPs |
| [phase5-discovery-tech.md](09-ai/prompts/phase5-discovery-tech.md) | P5.1–P5.10 | JS/TS, Java, Python, PHP, iOS, Salesforce, Ruby, WebForms, Angular, PowerShell |
| [phase6-discovery-legacy.md](09-ai/prompts/phase6-discovery-legacy.md) | P6.1–P6.12 | Use cases, DB schema, events, integrations, config, UI, shared libs, middleware, errors, state machines, vendor customizations, ACLs |

See [PROMPT-INDEX.md](09-ai/prompts/PROMPT-INDEX.md) for the full catalog and [09-ai/prompts/README.md](09-ai/prompts/README.md) for prompt-to-output file mapping.

---

## Output Templates

All assessment files (folders `00`–`08`, `10`) are blank templates populated by running the prompts against a real codebase. Key outputs:

| Output | Template | Generated By |
|--------|----------|-------------|
| Project profile | [project-profile.yaml](00-project-profile/project-profile.yaml) | Prompt P0.3 |
| Application inventory | [application-inventory.md](01-inventory/application-inventory.md) | Prompts P1.1–P1.5 |
| Code health assessment | [code-layer.md](02-assessment/code-layer.md) | Prompt P2 |
| Scoring & decision | [scoring-model.md](07-scoring/scoring-model.md) | Prompt P3.4 |
| Migration strategy | [strategy.md](08-migration/strategy.md) | Prompt P3.5 + decision matrix |
| Portfolio dashboard | [portfolio-dashboard.md](10-visuals/portfolio-dashboard.md) | Prompt P3.6 |

---

## Getting Started

See [QUICKSTART.md](QUICKSTART.md) for a step-by-step guide, or jump straight to:

1. Read [ORCHESTRATION-PROMPT.md](09-ai/prompts/ORCHESTRATION-PROMPT.md) to understand the guardrails
2. Run Prompt P0.1 from [phase0-classification.md](09-ai/prompts/phase0-classification.md) to classify your project
3. Follow the execution order for your project type (see table above)

---

## License

This framework is provided as-is for internal use in legacy modernization assessments.
