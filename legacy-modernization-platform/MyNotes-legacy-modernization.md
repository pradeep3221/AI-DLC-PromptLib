For legacy .NET projects (Brownfield project (Enhancements or Brownfield (.NET legacy) modernization) and Migration project)
	Application Discovery, Inventory (Baseline Mapping) & Assessment Framework
		Technology matrix: Back-end, Front-end, Database and integration - 
		How do we do that for Distributed or Event Driven architecture
		Output: System catalog (Md, spreadsheet or JSON), Service classification (Monolith / Modular Monolith / Microservices)
	Code Health Assessment 
		Dependency graph - visual dependency graph  - Project/Assembly Dependency Graph
		Dead code, 
		Complexity, 
		Refactoring priority
	Domain Discovery
Output: ?

# 🔍 Legacy .NET Inventory & Assessment Framework

## 1. 📦 Application Inventory (Baseline Mapping)

**Goal:** Understand *what exists before touching anything*

**Capture:**

* Applications / Services list
* Solution & project structure (.sln, csproj)
* Technology stack:

  * .NET Framework / .NET Core / .NET 6+
  * ASP.NET MVC / WebForms / Web API / Worker Services
* Hosting:

  * IIS / Windows Services / Azure / Containers
* External dependencies:

  * Databases (SQL Server, Oracle, etc.)
  * Third-party APIs
* Deployment pipelines (if any)

**Output:**

* System catalog (spreadsheet or JSON)
* Service classification:

  * Monolith / Modular Monolith / Microservices

---

## 2. 🧠 Code Health Assessment

### A. 🔗 Dependency Graph (Critical for Migration Strategy)

**What to analyze:**

* Project → Project dependencies
* Assembly references
* NuGet dependencies
* Cyclic dependencies

**Tools:**

* Visual Studio Dependency Graph
* NDepend
* `dotnet list package`
* Architecture tools (Structurizr, Archi)

**What to identify:**

* Tight coupling
* Cycles (big red flag 🚨)
* Shared libraries overuse

**Output:**

* Visual graph:

  * Layer violations
  * Core domain vs infrastructure leakage

---

### B. 🧟 Dead Code Detection

**What to look for:**

* Unused classes / methods
* Deprecated APIs still present
* Feature flags no longer used

**Tools:**

* NDepend
* ReSharper / Rider
* SonarQube

**Action:**

* Remove before migration → reduces cost & complexity

---

### C. 📊 Complexity Analysis

**Metrics:**

* Cyclomatic Complexity
* Method length
* Class size
* Nested dependencies

**Hotspots:**

* God classes
* Large controllers/services
* Business logic inside UI

**Tools:**

* SonarQube
* NDepend
* Code Metrics in Visual Studio

---

### D. 🔧 Refactoring Priority Model

Create a **scoring model**:

| Factor               | Weight                |
| -------------------- | --------------------- |
| Business Criticality | High                  |
| Change Frequency     | High                  |
| Complexity           | High                  |
| Dependency Level     | High                  |
| Test Coverage        | Low → Higher priority |

**Output:**

* Refactoring heatmap:

  * 🔴 High priority (fix first)
  * 🟡 Medium
  * 🟢 Low

---

## 3. 🧭 Domain Discovery (Most Important for Modernization)

This is where most migrations fail if skipped.

### A. Identify Domain Boundaries

**Approach:**

* Map features → modules
* Identify bounded contexts (DDD)

**Look for:**

* Business capabilities:

  * Billing
  * Claims
  * User Management
* Data ownership

---

### B. Reverse Engineer Domain Model

**Extract:**

* Core entities
* Aggregates
* Relationships
* Business rules hidden in code

**Sources:**

* Code (services, repositories)
* Database schema
* Stored procedures (!!)

---

### C. Event & Workflow Discovery

**Identify:**

* Key workflows
* Hidden business processes
* Async vs sync flows

**Example:**

* “Inspection report uploaded → validation → underwriting decision”

---

### D. Anti-Corruption Layer Identification

**Mark:**

* Legacy boundaries that should NOT leak into new system

---

## 4. 🧪 Testability Assessment

**Check:**

* Unit test coverage
* Integration tests
* Testability of code (tight coupling?)

**Output:**

* Risk score:

  * Low test coverage = High migration risk

---

## 5. ☁️ Migration Readiness Assessment

**Evaluate:**

* .NET upgrade path:

  * .NET Framework → .NET 8
* Compatibility issues:

  * System.Web
  * Windows-only dependencies
* Cloud readiness:

  * Stateless?
  * Config externalization?

---

## 6. 📊 Final Outputs (What You Should Produce)

### A. Architecture Artifacts

* Dependency Graph
* Context Map (DDD)
* System Landscape Diagram

### B. Reports

* Code Health Report
* Complexity Report
* Dead Code Report
* Migration Readiness Score

### C. Action Plan

* Refactoring backlog
* Migration strategy:

  * Rehost (Lift & Shift)
  * Refactor
  * Re-architect

---

# 🧩 How This Fits Your AI-Driven Approach

Given your GenAI work, you can **automate 60–70% of this**:

### 🔹 AI Opportunities

* Code summarization → Domain discovery
* Dependency extraction → Graph generation
* Dead code detection → Static analysis + LLM reasoning
* Refactoring suggestions → AI agents
* Knowledge graph → RAG over codebase

---

# 🚀 Suggested Repo Structure (Aligned with Your Prompt Library)

```
legacy-modernization/
│
├── inventory/
│   ├── app-catalog.json
│   ├── tech-stack.md
│
├── assessment/
│   ├── dependency-graph/
│   ├── code-health/
│   │   ├── complexity-report.md
│   │   ├── dead-code-report.md
│   │   └── refactoring-priority.md
│
├── domain-discovery/
│   ├── bounded-contexts.md
│   ├── domain-model.md
│   ├── workflows.md
│
├── migration/
│   ├── readiness-assessment.md
│   ├── strategy.md
│
├── ai-prompts/
│   ├── code-analysis/
│   ├── domain-extraction/
│   ├── refactoring/
│
└── tools/
    ├── scripts/
    └── automation/
```

---

# 💡 Key Insight (Architect-Level)

* **Inventory tells you WHAT you have**
* **Code Health tells you HOW BAD it is**
* **Domain Discovery tells you WHAT MATTERS**
* **Dependency Graph tells you HOW HARD it is to change**

👉 Migration success = **Domain clarity + Dependency control**

---

If you want next step, I can:

* Turn this into **50+ AI prompts for each step**
* Or design a **GenAI-powered assessment pipeline (Bedrock / Azure OpenAI)**
* Or create a **visual workflow (like Saga pattern style)**








Got it—you want a **clean, unified framework** that works for:

* **Brownfield (Enhancements)**
* **Brownfield Modernization (.NET legacy → modern .NET)**
* **Migration projects (rehost / replatform / re-architect)**

…and supports:

* App type classification (monolith, API, worker, distributed, EDA)
* Markdown outputs
* Enterprise-level assessment

Let’s structure this as a **single reusable model + workflow** you can plug into your repo / AI pipeline.

---

# 🧩 1. Project Classification Layer (First Step)

Every legacy .NET project should start with **2 dimensions**:

## A. Project Intent

```markdown
- Brownfield – Enhancements
- Brownfield – Modernization
- Migration – Rehost (Lift & Shift)
- Migration – Replatform
- Migration – Re-architect
```

---

## B. Application Architecture Type

```markdown
- Monolith
- API + SPA
- Worker / Background Processing
- Console / Batch
- Distributed (Microservices)
- Event-Driven Architecture (EDA)
- Hybrid (API + Events + Workers)
```

---

## C. Combined Classification (Example)

```markdown
## Project Classification

- Project Type: Brownfield – Modernization
- Architecture: Distributed (Event-Driven)
- Tech Stack: .NET Framework 4.7 → .NET 8
```

---

# 🔍 2. Unified Assessment Framework

This stays the same across all project types, but **depth varies**.

---

## 2.1 📦 Inventory & System Mapping

### What to Capture

* Applications / Services
* App Type (Monolith, API, Worker, etc.)
* Deployment model
* Dependencies (DB, APIs, Queues)

---

### Markdown Output

```markdown
# Application Inventory

## Applications

| Name            | Type              | Architecture | Tech |
|-----------------|------------------|--------------|------|
| Claims Portal   | Web (Monolith)   | Monolith     | .NET Framework |
| Claims API      | API              | Distributed  | .NET 6 |
| Processor       | Worker Service   | EDA          | .NET Worker |

## Observations
- Mix of monolith + distributed services
- Partial modernization already started
```

---

## 2.2 🧠 Code Health Assessment

Applies to ALL project types.

### Key Areas

* Dependency graph (project + service level)
* Dead code
* Complexity
* Test coverage
* Refactoring priority

---

### Markdown Output

```markdown
# Code Health Report

## Summary
- High complexity in ClaimsService
- Dead code ~18%

## Dependency Issues
- Tight coupling between UI and business logic

## Refactoring Priority
- 🔴 ClaimsService (High)
- 🟡 Notification Module (Medium)
```

---

## 2.3 🔗 Dependency Analysis (2 Levels)

### A. Monolith / Single App

* Project → Project dependencies

### B. Distributed / EDA

* Service → Service dependencies
* Event → Consumer mapping

---

### Markdown Output

```markdown
# Dependency Graph

## Service Dependencies

- Claims API → Validation API (REST)
- Claims API → Service Bus (Publishes ClaimCreated)

## Risks
- Synchronous dependency chain (latency risk)
```

---

## 2.4 📡 Event-Driven Analysis (If Applicable)

ONLY for:

* Distributed systems
* Event-driven architecture

---

### Markdown Output

```markdown
# Event Catalog

## ClaimCreated
- Producer: Claims API
- Consumers:
  - Validation Service
  - Audit Service

## Issues
- No retry/DLQ strategy
- No event versioning
```

---

## 2.5 🧭 Domain Discovery (CRITICAL)

Applies to:

* Modernization
* Re-architecture

Less critical for:

* Lift & Shift

---

### Output

```markdown
# Domain Discovery

## Bounded Contexts
- Claims
- Validation
- Payments

## Key Entities
- Claim
- Policy
```

---

## 2.6 🧪 Testability & Risk

```markdown
# Test Assessment

## Coverage
- Unit Tests: 20%
- Integration: Minimal

## Risks
- High regression risk during migration
```

---

## 2.7 ☁️ Migration Readiness

### Evaluate

* .NET compatibility
* Windows dependencies
* Cloud readiness
* Statelessness

---

### Output

```markdown
# Migration Readiness

## Findings
- Heavy System.Web usage
- Not container-ready

## Recommendation
- Refactor before migrating to .NET 8
```

---

# 🚀 3. How It Differs by Project Type

This is the **most important part**.

---

## 🟢 A. Brownfield – Enhancements

**Focus:**

* Quick understanding
* Minimal disruption

**Do:**

* Inventory (light)
* Code hotspots
* Dependency awareness

**Skip/Reduce:**

* Deep domain modeling
* Full event mapping

---

## 🟡 B. Brownfield – Modernization

**Focus:**

* Code quality + architecture improvement

**Do FULL:**

* Code health
* Dependency graph
* Domain discovery
* Refactoring plan

**Add:**

* Strangler pattern planning

---

## 🔵 C. Migration – Rehost (Lift & Shift)

**Focus:**

* Infrastructure, not code

**Do:**

* Inventory
* Compatibility check
* Infra dependencies

**Skip:**

* Heavy refactoring
* Domain modeling

---

## 🟠 D. Migration – Replatform

**Focus:**

* Platform + minor code changes

**Do:**

* Code health (moderate)
* Dependency cleanup
* Config externalization

---

## 🔴 E. Migration – Re-architect

**Focus:**

* Full transformation

**Do EVERYTHING:**

* Domain discovery
* Event flow mapping
* Service decomposition
* Dependency redesign

---

# 🧩 4. Final Repo Structure (Markdown-Centric)

```plaintext
legacy-dotnet-assessment/
│
├── 01-classification/
│   └── project-classification.md
│
├── 02-inventory/
│   └── application-inventory.md
│
├── 03-code-health/
│   ├── code-health.md
│   ├── complexity.md
│   └── dead-code.md
│
├── 04-dependencies/
│   └── dependency-graph.md
│
├── 05-event-analysis/
│   └── event-catalog.md
│
├── 06-domain/
│   └── domain-discovery.md
│
├── 07-testing/
│   └── test-assessment.md
│
├── 08-migration/
│   ├── readiness.md
│   └── strategy.md
│
└── 09-ai-prompts/
    └── *.md
```

---

# 🤖 5. AI-Driven Extension (Aligned with Your Work)

You can turn this into a **GenAI pipeline**:

### Input:

* GitHub repo
* Solution files
* Logs / DB schema

### Output:

* All `.md` files above
* Dependency graphs
* Domain map

---

# 💡 Architect Insight (This is the key takeaway)

* **Enhancement → Focus on hotspots**
* **Modernization → Focus on structure**
* **Migration → Focus on compatibility**
* **Re-architecture → Focus on domain + boundaries**

👉 Same framework, different depth

---

If you want, next I can:

* Generate **50+ ready-to-use AI prompts mapped to each section**
* Or design a **.NET tool + Bedrock/Azure OpenAI pipeline** to auto-generate these `.md` reports
* Or create a **visual orchestration (like Saga + workflow diagrams)**





-----------------------------

Perfect—let’s elevate this into a **production-grade, enterprise-ready framework** that you can:

* Plug into your **GitHub repo**
* Drive with **GenAI (Bedrock / Azure OpenAI)**
* Use for **Brownfield + Modernization + Migration + Distributed systems**
* Standardize outputs as **Markdown-first + machine-readable**

---

# 🚀 0. What’s Enhanced (vs previous version)

This version adds:

* ✅ **Unified meta-model (YAML + MD hybrid)**
* ✅ **Architecture-aware assessment (Monolith → EDA)**
* ✅ **Scoring system (quantifiable decisions)**
* ✅ **Service + Event + Domain triangulation**
* ✅ **Modernization decision engine**
* ✅ **AI-ready prompt hooks**
* ✅ **Cross-project portfolio view**

---

# 🧩 1. Unified Project Meta-Model (STANDARDIZE THIS FIRST)

Instead of scattered docs → define a **single source of truth**

## 📄 `project-profile.yaml`

```yaml
project:
  name: Claims Modernization
  intent: Brownfield-Modernization   # Enhancement | Modernization | Migration-Rehost | Replatform | Rearchitect
  
architecture:
  type: Distributed                  # Monolith | API+SPA | Worker | Distributed | Event-Driven | Hybrid
  style: Event-Driven
  deployment: Azure App Services

technology:
  current:
    dotnet: .NET Framework 4.7
    frontend: AngularJS
  target:
    dotnet: .NET 8
    frontend: Angular 17

components:
  - name: Claims API
    type: API Service
  - name: Claims Processor
    type: Worker Service
  - name: Notification Handler
    type: Event Consumer

communication:
  sync: [REST]
  async: [Azure Service Bus]

data:
  databases:
    - SQL Server
  shared_db: true
```

👉 This becomes:

* Input to AI
* Input to dashboards
* Input to decision engine

---

# 🔍 2. Multi-Layer Assessment Model (NEW – 4 Layers)

Instead of flat assessment → think in layers:

---

## 🧱 Layer 1: Code Layer (Inside Application)

* Complexity
* Dead code
* Testability
* Dependency graph (projects)

---

## 🔗 Layer 2: Service Layer (Distributed View)

* Service coupling
* API contracts
* Sync dependencies

---

## 📡 Layer 3: Event Layer (EDA Systems)

* Event producers/consumers
* Event flow
* Schema/versioning
* DLQ/retry

---

## 🧭 Layer 4: Domain Layer (Business View)

* Bounded contexts
* Aggregates
* Workflows

---

## 🔺 Key Insight

👉 Most teams only do **Layer 1**
👉 Real modernization requires **ALL 4 layers aligned**

---

# 📊 3. Quantitative Scoring Model (Decision Engine)

Turn assessment into **numbers → decisions**

---

## A. Code Health Score

```markdown
Score = (Complexity + Coupling + Dead Code + Test Coverage) / 4
```

| Metric        | Score (1–5) |
| ------------- | ----------- |
| Complexity    | 4           |
| Coupling      | 5           |
| Dead Code     | 3           |
| Test Coverage | 2           |

👉 **Code Health Score = 3.5 (Poor)**

---

## B. Architecture Fitness Score

| Factor        | Score |
| ------------- | ----- |
| Modularity    | 2     |
| Scalability   | 3     |
| Resilience    | 2     |
| Observability | 1     |

---

## C. Migration Readiness Score

| Factor             | Score |
| ------------------ | ----- |
| .NET Compatibility | 2     |
| Cloud Readiness    | 2     |
| Statelessness      | 1     |

---

## D. Final Decision Matrix

```markdown
| Score Range | Recommendation              |
|------------|----------------------------|
| 4–5        | Rehost / Minor changes     |
| 3–4        | Replatform                |
| 2–3        | Refactor + Modernize      |
| <2         | Re-architect              |
```

---

# 🔗 4. Advanced Dependency Modeling (NEW)

---

## A. 3 Types of Dependencies

### 1. Code Dependencies

* Project → Project

### 2. Runtime Dependencies

* API calls
* DB access

### 3. Event Dependencies

* Producer → Consumer

---

## B. Markdown Output (Enhanced)

```markdown
# Dependency Model

## Code Dependencies
- UI → Business Layer
- Business → Data Layer

## Runtime Dependencies
- Claims API → Validation API (REST)

## Event Dependencies
- Claims API → Service Bus → Validation Service

## Critical Issues
- Shared DB across services ❌
- Cyclic dependency in core modules ❌
```

---

# 📡 5. Event-Driven Deep Analysis (Enhanced)

---

## A. Event Maturity Model

| Level | Description      |
| ----- | ---------------- |
| L1    | Basic pub/sub    |
| L2    | Retry + DLQ      |
| L3    | Versioned events |
| L4    | Event sourcing   |

---

## B. Output

```markdown
# Event Architecture Assessment

## Maturity Level: L1

## Gaps
- No DLQ handling
- No schema versioning
- Tight coupling via event payload

## Recommendation
- Introduce versioned contracts
- Add retry + DLQ strategy
```

---

# 🧭 6. Domain Discovery (Enhanced with Mapping)

---

## A. Triangulation Model (🔥 Important)

You now map:

```text
Domain ↔ Service ↔ Event
```

---

## Output

```markdown
# Domain Mapping

| Domain       | Service              | Events              |
|-------------|---------------------|---------------------|
| Claims      | Claims API          | ClaimCreated        |
| Validation  | Validation Service  | ClaimValidated      |
| Payments    | Payment Service     | PaymentProcessed    |
```

---

👉 This is your **modern architecture blueprint**

---

# 🧪 7. Risk Model (NEW)

---

## A. Risk Categories

* Technical Risk
* Migration Risk
* Business Risk
* Data Risk

---

## Output

```markdown
# Risk Assessment

## High Risk
- Low test coverage
- Shared database

## Medium Risk
- Tight service coupling

## Low Risk
- Stateless APIs
```

---

# 🚀 8. Migration Strategy Generator (SMART OUTPUT)

Instead of static doc → generate strategy dynamically:

---

## Output

```markdown
# Migration Strategy

## Recommended Approach
- Strangler Pattern for Claims Module
- Incremental service extraction

## Phases

### Phase 1: Stabilization
- Add logging & monitoring
- Increase test coverage

### Phase 2: Decoupling
- Remove shared DB
- Introduce API boundaries

### Phase 3: Modernization
- Migrate to .NET 8
- Introduce event-driven workflows
```

---

# 📁 9. FINAL Repo Structure (ENTERPRISE GRADE)

```plaintext
legacy-modernization-platform/
│
├── 00-project-profile/
│   └── project-profile.yaml
│
├── 01-inventory/
│   └── application-inventory.md
│
├── 02-assessment/
│   ├── code-layer.md
│   ├── service-layer.md
│   ├── event-layer.md
│   └── domain-layer.md
│
├── 03-dependencies/
│   └── dependency-model.md
│
├── 04-domain/
│   └── domain-mapping.md
│
├── 05-events/
│   └── event-architecture.md
│
├── 06-risk/
│   └── risk-assessment.md
│
├── 07-scoring/
│   └── scoring-model.md
│
├── 08-migration/
│   ├── readiness.md
│   └── strategy.md
│
├── 09-ai/
│   ├── prompts/
│   └── workflows/
│
└── 10-visuals/
    ├── dependency-graph.png
    └── workflow-diagrams.md
```

---

# 🤖 10. AI Integration Hooks (FOR YOUR GENAI PLATFORM)

Each section can map to an AI prompt:

| Section     | AI Task                 |
| ----------- | ----------------------- |
| Inventory   | Extract system metadata |
| Code Health | Analyze complexity      |
| Dependency  | Build graph             |
| Domain      | Extract entities        |
| Events      | Identify event flows    |
| Strategy    | Recommend modernization |

---

# 💡 Final Architect Insight (This is the real upgrade)

👉 Legacy modernization is NOT:

* Just upgrading .NET version ❌
* Just moving to cloud ❌

👉 It is:

**Aligning Code + Services + Events + Domain into clean boundaries**

---

# 🔥 If You Want Next Level

I can now:

### 1. Generate **50+ production AI prompts**

Mapped exactly to each section

### 2. Build a **.NET tool / CLI**

```bash
dotnet legacy-analyzer scan repo
```

### 3. Design **visual architecture (Saga-style)**

* Service flows
* Event flows
* Migration roadmap

Just tell me what direction 👍


ComprehensivePromptLibrary    →    AI Engine    →    legacy-modernization-platform
(What to analyze)              (Executes)           (Where results land)
       PROMPTS                                            TEMPLATES



Dimension	ComprehensivePromptLibrary (9 files)			legacy-modernization-platform (28 files)
Role		The brain — AI instructions (what to extract)	The body — output templates (where to store it)
Audience	AI agent / prompt engineer						Assessment team / reviewers / stakeholders
File type	Executable prompts with instructions			Fillable templates with placeholder tables
Execution	Run sequentially, prompt-by-prompt				Populated by prompt outputs