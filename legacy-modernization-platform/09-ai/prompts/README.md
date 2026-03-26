# AI Prompt Library — Consolidated Reference

> This folder **contains** the complete AI prompt library that drives all
> assessment outputs in the `legacy-modernization-platform`. Everything needed
> to run the assessment is self-contained here.

---

## Folder Contents

```
09-ai/prompts/                              ← You are here
├── ORCHESTRATION-PROMPT.md                  ← Start here: AI guardrails, workflow, output standards
├── PROMPT-INDEX.md                          ← Master catalog of all 39 prompts
├── README.md                                ← This file: mapping & navigation
├── phase0-classification.md                 ← P0: Project Classification
├── phase1-inventory.md                      ← P1.1–P1.6 Inventory & Baseline
├── phase2-code-health.md                    ← P2.1–P2.4 Code Health Analysis
├── phase3-architecture-scoring.md           ← P3.1–P3.6 Scoring & Readiness
├── phase4-discovery-core.md                 ← P4.1–P4.7 Core Domain Extraction
├── phase5-discovery-tech.md                 ← P5.1–P5.10 Technology-Specific
└── phase6-discovery-legacy.md               ← P6.1–P6.12 Legacy Deep Extraction
```

---

## Quick Start

1. Open [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md) — understand guardrails & workflow
2. Run **Prompt P0.1** from [phase0-classification.md](phase0-classification.md) — classify the project
3. Check the **Depth Calibration Matrix** in ORCHESTRATION-PROMPT.md to determine which prompts to run
4. Follow the execution order in [PROMPT-INDEX.md](PROMPT-INDEX.md) for your project type
5. Outputs populate the numbered folders (`00-project-profile/` through `10-visuals/`)

---

## Prompt → Output Mapping

| Prompt | Source File | Output Template |
|--------|------------|-----------------|
| P0.1–P0.5 Classification | [phase0-classification.md](phase0-classification.md) | [00-project-profile/project-profile.yaml](../../00-project-profile/project-profile.yaml) |
| P1.1–P1.5 Inventory | [phase1-inventory.md](phase1-inventory.md) | [01-inventory/application-inventory.md](../../01-inventory/application-inventory.md) |
| P1.6 Performance Baseline | [phase1-inventory.md](phase1-inventory.md) | [01-inventory/performance-baseline.md](../../01-inventory/performance-baseline.md) |
| P2 Code Health | [phase2-code-health.md](phase2-code-health.md) | [02-assessment/code-layer.md](../../02-assessment/code-layer.md) |
| P2 + Manual Testability | [phase2-code-health.md](phase2-code-health.md) | [02-assessment/testability.md](../../02-assessment/testability.md) |
| P3.1 Multi-Layer | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [02-assessment/service-layer.md](../../02-assessment/service-layer.md) |
| P3.2 Event Maturity | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [02-assessment/event-layer.md](../../02-assessment/event-layer.md) |
| P3.3 Triangulation | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [02-assessment/domain-layer.md](../../02-assessment/domain-layer.md) |
| P3.4 Scoring | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [07-scoring/scoring-model.md](../../07-scoring/scoring-model.md) |
| P3.5 Migration Readiness | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [08-migration/readiness.md](../../08-migration/readiness.md) |
| P3.6 Portfolio View | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [10-visuals/portfolio-dashboard.md](../../10-visuals/portfolio-dashboard.md) |
| P1.3 + P2 Dependencies | [phase1-inventory.md](phase1-inventory.md) | [03-dependencies/dependency-model.md](../../03-dependencies/dependency-model.md) |
| P4.1–P5.10 Core & Tech Discovery | [phase4-discovery-core.md](phase4-discovery-core.md) / [phase5-discovery-tech.md](phase5-discovery-tech.md) | [04-domain/domain-mapping.md](../../04-domain/domain-mapping.md) (hub) |
| P4.6–P4.7 SP Extraction | [phase4-discovery-core.md](phase4-discovery-core.md) | [04-domain/sp-business-logic.md](../../04-domain/sp-business-logic.md) |
| P6.1 Use Cases | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [04-domain/use-case-catalog.md](../../04-domain/use-case-catalog.md) |
| P6.2 DB Schema | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [04-domain/domain-mapping.md](../../04-domain/domain-mapping.md) |
| P6.3 Event Flows | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [05-events/event-architecture.md](../../05-events/event-architecture.md) |
| P6.4 External Integrations | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [03-dependencies/integration-catalog.md](../../03-dependencies/integration-catalog.md) |
| P6.5 Config & Secrets | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [02-assessment/configuration-catalog.md](../../02-assessment/configuration-catalog.md) |
| P6.6 UI Behavior | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [04-domain/ui-behavior-catalog.md](../../04-domain/ui-behavior-catalog.md) |
| P6.7 Shared Libraries | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [02-assessment/shared-library-analysis.md](../../02-assessment/shared-library-analysis.md) |
| P6.8 Middleware | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [02-assessment/middleware-analysis.md](../../02-assessment/middleware-analysis.md) |
| P6.9 Error Handling | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [02-assessment/error-handling-catalog.md](../../02-assessment/error-handling-catalog.md) |
| P6.10 State Machines | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [04-domain/state-machine-catalog.md](../../04-domain/state-machine-catalog.md) |
| P6.11 Vendor Customizations | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [02-assessment/vendor-customization-catalog.md](../../02-assessment/vendor-customization-catalog.md) |
| P6.12 Anti-Corruption Layers | [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | [03-dependencies/anti-corruption-layers.md](../../03-dependencies/anti-corruption-layers.md) |
| P3.1–P3.6 Risk | [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | [06-risk/risk-assessment.md](../../06-risk/risk-assessment.md) |
| Decision Matrix | [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md) | [08-migration/strategy.md](../../08-migration/strategy.md) |

---

## Execution Order by Project Type

### Brownfield Enhancement (BF-ENH)
```
P0 → P1.1 → P2 → P1.3 → Done (lightweight)
```

### Brownfield Modernization (BF-MOD)
```
P0 → P1.1 → P2 → P1.3 → P1.4 → P1.5 → P3.1–P3.6 → P4.1–P4.7 → P6.1–P6.11
```

### Migration – Rehost (MIG-RH)
```
P0 → P1.1 → P2 → P1.3 → P1.6 → Done (lift-and-shift focus)
```

### Migration – Replatform (MIG-RP)
```
P0 → P1.1–P1.6 → P2 → P3.1–P3.3 → P3.4–P3.5 → P4.1–P4.7 (selective)
```

### Migration – Re-architect (MIG-RA) — Full
```
P0 → P1.1–P1.6 → P2 → P3.1–P3.6 → P4.1–P5.10 → P6.1–P6.12
```

See [PROMPT-INDEX.md](PROMPT-INDEX.md) for detailed execution paths and the full prompt catalog.
