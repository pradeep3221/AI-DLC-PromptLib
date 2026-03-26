# 📚 Comprehensive Legacy Modernization Prompt Library — Index

> Unified prompt library for legacy .NET assessment, modernization, and migration.
> Merges strategic decision frameworks with executable AI-driven prompts.

---

## Document Information

| Property | Value |
|----------|-------|
| **Library Version** | 4.0.0 |
| **Last Updated** | March 2026 |
| **Status** | Active |
| **Scope** | Brownfield Enhancement · Brownfield Modernization · Migration (Rehost / Replatform / Re-architect) |

---

## Quick Reference — All Prompts

### Phase 0: Project Classification

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P0** | Project Classification & Meta-Model | [phase0-classification.md](phase0-classification.md) | Classify intent, architecture, tech stack; generate `project-profile.yaml` |

### Phase 1: Inventory & Baseline

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P1.1** | Component Inventory | [phase1-inventory.md](phase1-inventory.md#p11-component-inventory) | Catalog all apps, projects, services |
| **P1.2** | Technology Matrix | [phase1-inventory.md](phase1-inventory.md#p12-technology-matrix) | Map technologies + modernization paths |
| **P1.3** | Dependency Mapping | [phase1-inventory.md](phase1-inventory.md#p13-dependency-mapping) | Inter-component dependencies & data flows |
| **P1.4** | Create Domain Model | [phase1-inventory.md](phase1-inventory.md#p14-create-domain-model) | Entities, aggregates, relationships |
| **P1.5** | Define Bounded Contexts | [phase1-inventory.md](phase1-inventory.md#p15-define-bounded-contexts) | DDD context map & integration strategy |
| **P1.6** | Performance Baselining | [phase1-inventory.md](phase1-inventory.md#p16-performance-baselining) | Baseline metrics for post-migration comparison |

### Phase 2: Code Health Assessment

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P2.1** | Dependency Graph Generation | [phase2-code-health.md](phase2-code-health.md#part-1-dependency-graph-generation-p21) | Multi-level dependency graphs with Mermaid |
| **P2.2** | Dead Code Identification | [phase2-code-health.md](phase2-code-health.md#part-2-dead-code-identification-p22) | Unused code across .NET, JS/TS, SQL |
| **P2.3** | Code Complexity Metrics | [phase2-code-health.md](phase2-code-health.md#part-3-code-complexity-metrics-p23) | Cyclomatic, cognitive, maintainability |
| **P2.4** | Refactoring Prioritization | [phase2-code-health.md](phase2-code-health.md#part-4-refactoring-prioritization-matrix-p24) | Business impact × complexity scoring |

### Phase 3: Architecture Assessment & Scoring

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P3.1** | Multi-Layer Assessment | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p31-multi-layer-assessment-model) | 4-layer analysis: Code → Service → Event → Domain |
| **P3.2** | Event Maturity Assessment | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p32-event-maturity-assessment) | L1–L4 event architecture maturity |
| **P3.3** | Domain-Service-Event Triangulation | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p33-domain-service-event-triangulation) | Cross-reference domain ↔ service ↔ event |
| **P3.4** | Quantitative Scoring Engine | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p34-quantitative-scoring-engine) | Code health, architecture fitness, migration readiness scores |
| **P3.5** | Migration Readiness Assessment | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p35-migration-readiness-assessment) | .NET compat, cloud readiness, decision matrix |
| **P3.6** | Portfolio View | [phase3-architecture-scoring.md](phase3-architecture-scoring.md#p36-portfolio-view) | Cross-project portfolio dashboard |

### Phase 4: Domain Discovery — Core

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P4.1** | Multi-Technology Domain Scan | [phase4-discovery-core.md](phase4-discovery-core.md#p41-multi-technology-domain-scan) | Discover domain concepts across all tech types |
| **P4.2** | Service Contract Analysis | [phase4-discovery-core.md](phase4-discovery-core.md#p42-service-contract-analysis-wcfasmx) | WCF/ASMX → Commands/Queries |
| **P4.3** | VB.NET Business Rules Extraction | [phase4-discovery-core.md](phase4-discovery-core.md#p43-vbnet-business-rules-extraction) | Extract domain logic from VB.NET |
| **P4.4** | WPF ViewModel Analysis | [phase4-discovery-core.md](phase4-discovery-core.md#p44-wpf-viewmodel-analysis) | Commands, validation, computed properties |
| **P4.5** | Console/Worker Service Analysis | [phase4-discovery-core.md](phase4-discovery-core.md#p45-consoleworker-service-analysis) | Background process domain logic |
| **P4.6** | SP Deep Business Rules Extraction | [phase4-discovery-core.md](phase4-discovery-core.md#p46-stored-procedure-deep-business-rules-extraction) | Stored procedure rule extraction with confidence levels |
| **P4.7** | SP Caller Technology Mapping | [phase4-discovery-core.md](phase4-discovery-core.md#p47-identify-sp-caller-technologies) | Map all callers of each SP |

### Phase 5: Domain Discovery — Technology-Specific

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P5.1** | JavaScript/TypeScript Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p51-javascripttypescript-business-rules) | JS/TS business rules |
| **P5.2** | Java Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p52-java-business-rules-extraction) | Spring/JavaEE rules |
| **P5.3** | Python Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p53-python-business-rules-extraction) | Django/Flask/FastAPI rules |
| **P5.4** | PHP Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p54-php-business-rules-extraction) | Laravel/Symfony/legacy rules |
| **P5.5** | iOS (Swift/Obj-C) Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p55-iosswift-business-rules-extraction) | Mobile business logic |
| **P5.6** | Salesforce Apex Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p56-salesforce-apex-extraction) | Apex + declarative rules |
| **P5.7** | Ruby Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p57-ruby-business-rules-extraction) | Rails/Sinatra rules |
| **P5.8** | ASP.NET WebForms Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p58-webforms-business-rules-extraction) | Code-behind business logic |
| **P5.9** | Angular/Frontend Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p59-angular-business-rules-extraction) | Frontend rules (keep vs move) |
| **P5.10** | PowerShell/Shell Extraction | [phase5-discovery-tech.md](phase5-discovery-tech.md#p510-powershell-business-rules-extraction) | Script automation rules |

### Phase 6: Domain Discovery — Legacy Deep Extraction

| ID | Prompt | File | Purpose |
|----|--------|------|---------|
| **P6.1** | Use Cases / Application Logic | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p61-build-use-case-catalog-from-code) | Orchestration logic extraction |
| **P6.2** | Database Schema Semantics | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p62-database-schema--domain-semantics) | Schema with business meaning |
| **P6.3** | Event Flows & Side Effects | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p63-event--message-flow-extraction) | Triggers, notifications, jobs |
| **P6.4** | Integration Points | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p64-integration-point-extraction) | External system contracts |
| **P6.5** | Configuration & Environment | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p65-configuration--secret-extraction) | Config, secrets, feature flags |
| **P6.6** | Legacy UI Behavior | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p66-ui-behavior-extraction) | Screens, forms, navigation |
| **P6.7** | Shared Libraries/Common | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p67-shared-library-analysis) | Shared business logic |
| **P6.8** | Middleware/Pipeline Logic | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p68-middleware--interceptor-chain-analysis) | HTTP modules, interceptors |
| **P6.9** | Error Handling & Exceptions | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p69-error-handling--recovery-patterns) | Exception patterns, error codes |
| **P6.10** | Workflow/State Machines | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p610-state-machine-extraction) | State transitions, approval rules |
| **P6.11** | Third-Party Customizations | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p611-3rd-party--vendor-customization-extraction) | Framework extensions |
| **P6.12** | Anti-Corruption Layer Identification | [phase6-discovery-legacy.md](phase6-discovery-legacy.md#p612-anti-corruption-layer-identification) | Legacy boundary mapping |

---

## Execution Order by Project Type

### 🟢 Brownfield — Enhancements (Minimal Depth)

```
P0 → P1.1 → P1.2 → P1.3 → P2 (light) → Done
```

### 🟡 Brownfield — Modernization (Full Depth)

```
P0 → P1.1 → P1.2 → P1.3 → P1.4 → P1.5 → P1.6
  → P2 (full) → P3.1 → P3.2 → P3.3 → P3.4
  → P4.1–P4.7 → P5.1–P5.10 (matching tech) → P6.1–P6.12
```

### 🔵 Migration — Rehost (Lift & Shift)

```
P0 → P1.1 → P1.2 → P1.3 → P1.6 → P3.5 → Done
```

### 🟠 Migration — Replatform

```
P0 → P1.1 → P1.2 → P1.3 → P1.6 → P2 (moderate) → P3.5
  → P6.5 (config) → P6.4 (integrations) → Done
```

### 🔴 Migration — Re-architect (Everything)

```
P0 → P1.1 → P1.2 → P1.3 → P1.4 → P1.5 → P1.6
  → P2 (full) → P3.1 → P3.2 → P3.3 → P3.4 → P3.5 → P3.6
  → P4.1–P6.12 (all applicable)
```

---

## File Map

```
legacy-modernization-platform/09-ai/prompts/
├── PROMPT-INDEX.md                    ← You are here
├── ORCHESTRATION-PROMPT.md            ← AI guardrails, workflow, output standards
├── README.md                          ← Prompt → Output mapping & navigation
├── phase0-classification.md           ← P0: Project classification + YAML meta-model
├── phase1-inventory.md                ← P1: Inventory, tech matrix, domain model, perf baseline
├── phase2-code-health.md              ← P2: Dependency graphs, dead code, complexity, refactoring
├── phase3-architecture-scoring.md     ← P3: 4-layer model, event maturity, scoring, migration readiness
├── phase4-discovery-core.md           ← P4: Core domain: multi-tech scan, SPs, WCF, VB.NET, WPF
├── phase5-discovery-tech.md           ← P5: 10 technology-specific extractions
└── phase6-discovery-legacy.md         ← P6: 12 legacy deep extraction prompts
```
