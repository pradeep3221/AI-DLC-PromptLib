For new .NET projects (Greenfield - building from scratch)
	Project Classification & Architecture Decision
		Project type: API, SPA+API, Event-Driven, Worker, Console-Batch
		Architecture style: Simple CRUD, Layered, Modular Monolith, Microservices, Event-Driven, CQRS
		Output: Project profile (YAML), complexity score, architecture recommendation
	Requirements & Domain Discovery
		Functional requirements catalog
		Non-functional requirements (performance, scalability, security, availability)
		Domain modeling: Entities, Aggregates, Value Objects, Domain Events
		Bounded contexts identification
		Use case reverse-engineering from requirements
	Architecture Design
		Architecture Decision Records (ADRs)
		Technology stack selection with rationale
		API design (REST, gRPC, GraphQL)
		Data model design (relational, document, event store)
		Security model (AuthN, AuthZ, data protection)
		Resilience patterns (retry, circuit breaker, bulkhead)
	Implementation Planning
		Solution & project structure
		Coding standards & conventions
		Testing strategy (unit, integration, contract, E2E)
		CI/CD pipeline design
		Infrastructure as Code
		Deployment strategy (blue-green, canary, rolling)
Output: Complete architecture & implementation blueprint

# 🏗️ Greenfield .NET Design & Implementation Framework

## 1. 📋 Project Classification

**Goal:** Understand *what we're building before writing any code*

**Capture:**

* Business domain & problem statement
* Project type classification
* Architecture style recommendation
* Complexity assessment

**Output:**

* Project profile (YAML)
* Architecture recommendation with rationale

---

## 2. 📝 Requirements & Domain Discovery

**Goal:** Capture *what the system must do* and *what domain concepts exist*

**Capture:**

* Functional requirements with acceptance criteria
* Non-functional requirements (NFRs)
* Domain concepts, entities, relationships
* Bounded contexts and context map
* Use cases with actors and flows

**Output:**

* Requirements catalog
* Domain model
* Use case catalog

---

## 3. 🏛️ Architecture Design

**Goal:** Make *deliberate, documented architecture decisions*

**Capture:**

* Architecture Decision Records (ADRs)
* Technology stack with selection rationale
* API contracts and versioning strategy
* Data model and persistence strategy
* Security architecture
* Integration points and protocols

**Output:**

* ADR catalog
* API specifications
* Data model diagrams
* Security model

---

## 4. 🔧 Implementation Planning

**Goal:** Define *how we build, test, and deliver*

**Capture:**

* Solution structure and project layout
* Coding standards and naming conventions
* Testing pyramid and strategy
* CI/CD pipeline stages
* Deployment strategy
* Observability (logging, metrics, tracing)

**Output:**

* Project scaffold specification
* CI/CD pipeline definition
* Deployment runbook


## Structure
```
greenfield-platform/
├── README.md                        ← Main documentation hub
├── QUICKSTART.md                    ← 6-step getting started guide
├── MyNotes-greenfield.md            ← Notes & design rationale
│
├── 00-project-profile/
│   └── project-profile.yaml        ← Single source of truth (YAML)
├── 01-requirements/
│   ├── requirements-catalog.md      ← Functional requirements
│   ├── nfr-catalog.md               ← Non-functional requirements
│   └── acceptance-criteria.md       ← Given-When-Then criteria
├── 02-architecture/
│   ├── architecture-decisions.md    ← ADRs with complexity scoring
│   ├── architecture-patterns.md     ← Pattern catalog & anti-patterns
│   └── technology-selection.md      ← Technology stack with rationale
├── 03-design/
│   ├── api-contracts.md             ← REST/gRPC contracts, RFC 7807
│   ├── data-model.md                ← Entity schemas, ER diagrams
│   ├── security-model.md            ← AuthN/AuthZ, threat model
│   ├── integration-design.md        ← External system integrations, ACLs
│   └── resilience-design.md         ← Retry, circuit breaker, health checks
├── 04-domain/
│   ├── domain-model.md              ← Aggregates, entities, value objects
│   ├── bounded-contexts.md          ← Context map, relationships
│   ├── use-case-catalog.md          ← Use cases with flows
│   ├── event-storming.md            ← Commands, events, policies
│   └── business-rules.md            ← Rules catalog with confidence
├── 05-implementation/
│   ├── project-structure.md         ← Solution layout, layer rules
│   ├── coding-standards.md          ← C# conventions, git standards
│   └── implementation-patterns.md   ← Patterns by layer (DDD, CQRS, etc.)
├── 06-quality/
│   ├── testing-strategy.md          ← Testing pyramid, coverage targets
│   ├── quality-gates.md             ← CI quality gates, PR checklist
│   └── observability-design.md      ← Logging, metrics, tracing, alerting
├── 07-delivery/
│   ├── deployment-strategy.md       ← Blue-green/canary, scaling rules
│   ├── cicd-pipeline.md             ← Pipeline stages, branch strategy
│   ├── release-planning.md          ← MVP scope, sprint phases
│   └── infrastructure-as-code.md    ← IaC resources, environment diffs
├── 08-ai/
│   ├── prompts/
│   │   ├── ORCHESTRATION-PROMPT.md  ← Master guardrails & workflow
│   │   ├── phase0-classification.md ← P0.1–P0.5: Project classification
│   │   ├── phase1-requirements.md   ← P1.1–P1.6: Requirements & domain
│   │   ├── phase2-architecture.md   ← P2.1–P2.6: Architecture & design
│   │   ├── phase3-implementation.md ← P3.1–P3.6: Implementation & delivery
│   │   ├── PROMPT-INDEX.md          ← Full 23-prompt catalog
│   │   └── README.md               ← Prompt library navigation hub
│   └── workflows/
│       └── README.md               ← Pipeline workflow diagrams
└── 09-visuals/
    ├── architecture-diagrams.md     ← 8 Mermaid diagram templates
    └── project-dashboard.md         ← Executive view + Gantt milestones


 ```

### Key differences from the legacy platform:



 

Created 13 todos

Let me read the key files from the legacy platform to understand the structure and content patterns.    

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/README.md#1-1), lines 1 to 150

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/QUICKSTART.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/00-project-profile/project-profile.yaml)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/MyNotes-legacy-modernization.md#1-1), lines 1 to 100

Read all legacy platform files

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/README.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/QUICKSTART.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/MyNotes-legacy-modernization.md#1-1), lines 1 to 500

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/00-project-profile/project-profile.yaml)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/01-inventory/application-inventory.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/01-inventory/performance-baseline.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/code-layer.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/configuration-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/domain-layer.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/error-handling-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/event-layer.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/middleware-analysis.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/service-layer.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/shared-library-analysis.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/testability.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/02-assessment/vendor-customization-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/03-dependencies/dependency-model.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/03-dependencies/anti-corruption-layers.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/03-dependencies/integration-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/04-domain/domain-mapping.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/04-domain/state-machine-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/04-domain/ui-behavior-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/04-domain/sp-business-logic.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/05-events/event-architecture.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/06-risk/risk-assessment.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/04-domain/use-case-catalog.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/07-scoring/scoring-model.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/08-migration/readiness.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/08-migration/strategy.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/ORCHESTRATION-PROMPT.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase2-code-health.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase1-inventory.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase3-architecture-scoring.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase0-classification.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase4-discovery-core.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase6-discovery-legacy.md#1-1), lines 1 to 600

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/PROMPT-INDEX.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/README.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/workflows/README.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/09-ai/prompts/phase5-discovery-tech.md#1-1), lines 1 to 600

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/10-visuals/workflow-diagrams.md)

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/legacy-modernization-platform/10-visuals/portfolio-dashboard.md)

Read [](file:///c%3A/Users/prade/AppData/Roaming/Code/User/workspaceStorage/f5cd9143ac5656cda86a4e8fd3e3b37d/GitHub.copilot-chat/chat-session-resources/48bf46a5-f24c-4668-a439-6dac690cdf99/toolu_vrtx_01E7MU2zd2cBYq6LiqMQCwku__vscode-1774491622932/content.txt)

Starting: *Create greenfield folder structure* (2/13)

Now I have a thorough understanding of the legacy platform. Let me create the greenfield platform with an analogous structure adapted for new project development. I'll create all files organized in batches. 

Updated todo list

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/README.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/QUICKSTART.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/MyNotes-greenfield.md)

Starting: *Create 00-project-profile* (3/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/00-project-profile/project-profile.yaml)

Starting: *Create 01-requirements* (4/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/01-requirements/requirements-catalog.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/01-requirements/nfr-catalog.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/01-requirements/acceptance-criteria.md)

Starting: *Create 02-architecture* (5/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/02-architecture/architecture-decisions.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/02-architecture/technology-selection.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/02-architecture/architecture-patterns.md)

Starting: *Create 03-design* (6/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/03-design/api-contracts.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/03-design/data-model.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/03-design/security-model.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/03-design/integration-design.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/03-design/resilience-design.md)

Starting: *Create 04-domain* (7/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/04-domain/domain-model.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/04-domain/bounded-contexts.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/04-domain/use-case-catalog.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/04-domain/event-storming.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/04-domain/business-rules.md)

Starting: *Create 05-implementation* (8/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/05-implementation/project-structure.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/05-implementation/coding-standards.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/05-implementation/implementation-patterns.md)

Starting: *Create 06-quality* (9/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/06-quality/testing-strategy.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/06-quality/quality-gates.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/06-quality/observability-design.md)

Starting: *Create 07-delivery* (10/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/07-delivery/deployment-strategy.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/07-delivery/cicd-pipeline.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/07-delivery/release-planning.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/07-delivery/infrastructure-as-code.md)

Starting: *Create 08-ai prompts & workflows* (11/12)

Now creating the AI prompts — the engine of the framework: 

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/ORCHESTRATION-PROMPT.md)

 

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/phase0-classification.md)

 

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/phase1-requirements.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/phase2-architecture.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/phase3-implementation.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/PROMPT-INDEX.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/prompts/README.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/08-ai/workflows/README.md)

Starting: *Create 09-visuals* (12/12)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/09-visuals/architecture-diagrams.md)

Created [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform/09-visuals/project-dashboard.md)

Completed: *Create 09-visuals* (12/12)

Let me verify the complete structure: 

Read [](file:///e%3A/GenerativeAIDev/AI-DLC-PromptLib/greenfield-platform)

Ran terminal command: Get-ChildItem -Recurse "e:\GenerativeAIDev\AI-DLC-PromptLib\greenfield-platform" | Where-Object { -not $_.PSIsContainer } | Select-Object -ExpandProperty FullName | ForEach-Object { $_.Replace("e:\GenerativeAIDev\AI-DLC-PromptLib\greenfield-platform\", "") }

The greenfield-platform folder is complete with **36 files** across **10 numbered directories**. Here's the structure:

```
greenfield-platform/
├── README.md                        ← Main documentation hub
├── QUICKSTART.md                    ← 6-step getting started guide
├── MyNotes-greenfield.md            ← Notes & design rationale
│
├── 00-project-profile/
│   └── project-profile.yaml        ← Single source of truth (YAML)
├── 01-requirements/
│   ├── requirements-catalog.md      ← Functional requirements
│   ├── nfr-catalog.md               ← Non-functional requirements
│   └── acceptance-criteria.md       ← Given-When-Then criteria
├── 02-architecture/
│   ├── architecture-decisions.md    ← ADRs with complexity scoring
│   ├── architecture-patterns.md     ← Pattern catalog & anti-patterns
│   └── technology-selection.md      ← Technology stack with rationale
├── 03-design/
│   ├── api-contracts.md             ← REST/gRPC contracts, RFC 7807
│   ├── data-model.md                ← Entity schemas, ER diagrams
│   ├── security-model.md            ← AuthN/AuthZ, threat model
│   ├── integration-design.md        ← External system integrations, ACLs
│   └── resilience-design.md         ← Retry, circuit breaker, health checks
├── 04-domain/
│   ├── domain-model.md              ← Aggregates, entities, value objects
│   ├── bounded-contexts.md          ← Context map, relationships
│   ├── use-case-catalog.md          ← Use cases with flows
│   ├── event-storming.md            ← Commands, events, policies
│   └── business-rules.md            ← Rules catalog with confidence
├── 05-implementation/
│   ├── project-structure.md         ← Solution layout, layer rules
│   ├── coding-standards.md          ← C# conventions, git standards
│   └── implementation-patterns.md   ← Patterns by layer (DDD, CQRS, etc.)
├── 06-quality/
│   ├── testing-strategy.md          ← Testing pyramid, coverage targets
│   ├── quality-gates.md             ← CI quality gates, PR checklist
│   └── observability-design.md      ← Logging, metrics, tracing, alerting
├── 07-delivery/
│   ├── deployment-strategy.md       ← Blue-green/canary, scaling rules
│   ├── cicd-pipeline.md             ← Pipeline stages, branch strategy
│   ├── release-planning.md          ← MVP scope, sprint phases
│   └── infrastructure-as-code.md    ← IaC resources, environment diffs
├── 08-ai/
│   ├── prompts/
│   │   ├── ORCHESTRATION-PROMPT.md  ← Master guardrails & workflow
│   │   ├── phase0-classification.md ← P0.1–P0.5: Project classification
│   │   ├── phase1-requirements.md   ← P1.1–P1.6: Requirements & domain
│   │   ├── phase2-architecture.md   ← P2.1–P2.6: Architecture & design
│   │   ├── phase3-implementation.md ← P3.1–P3.6: Implementation & delivery
│   │   ├── PROMPT-INDEX.md          ← Full 23-prompt catalog
│   │   └── README.md               ← Prompt library navigation hub
│   └── workflows/
│       └── README.md               ← Pipeline workflow diagrams
└── 09-visuals/
    ├── architecture-diagrams.md     ← 8 Mermaid diagram templates
    └── project-dashboard.md         ← Executive view + Gantt milestones
```

**Key differences from the legacy platform:**

| Legacy Modernization | Greenfield Platform |
|---------------------|---------------------|
| 01-inventory (app catalog) | 01-requirements (requirements catalog, NFRs) |
| 02-assessment (code health, 10 files) | 02-architecture (ADRs, patterns, tech selection) |
| 03-dependencies (ACLs, integrations) | 03-design (API, data model, security, resilience) |
| 05-events, 06-risk, 07-scoring | 05-implementation, 06-quality, 07-delivery |
| 08-migration (readiness, strategy) | No migration — delivery-focused instead |
| 39 prompts (P0–P6, discovery-heavy) | 23 prompts (P0–P3, design-forward) |
| Assessment → Score → Migration decision | Requirements → Architecture → Implementation plan |
