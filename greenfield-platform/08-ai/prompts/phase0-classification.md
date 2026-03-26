# Phase 0 — Project Classification

> Classify your project, determine architecture style, generate project profile, and calibrate design depth.

---

## P0.1 — Determine Project Type

**Input:** Project brief, business requirements summary, or stakeholder description.

**Instruction:**
Analyze the provided project description and classify it into one of the following types:

| Type | Key Indicators |
|------|---------------|
| **Simple-API** | CRUD operations, single database, minimal business logic, 1–3 entities |
| **SPA-API** | Rich frontend + REST/GraphQL backend, moderate business logic, user-facing workflows |
| **Modular-Monolith** | Complex business domain, multiple bounded contexts, single deployable unit, team < 5 |
| **Microservices** | Multiple independent services, separate data stores, independent deployment, team > 5 |
| **Event-Driven** | Asynchronous workflows, event sourcing, CQRS, complex state transitions |
| **Worker-Service** | Background processing, queue consumers, scheduled jobs, no HTTP interface |
| **Console-Batch** | ETL, data migration, one-off processing, command-line tools |

**Output Format:**
```
Project Type: [TYPE]
Confidence: HIGH / MEDIUM / LOW
Rationale: [Why this classification]
Alternative: [Second-best classification and why it was not chosen]
```

---

## P0.2 — Determine Architecture Style

**Input:** Project type from P0.1, requirements summary.

**Instruction:**
Based on the project type, recommend an architecture style:

| Project Type | Default Style | Consider If... |
|-------------|--------------|----------------|
| Simple-API | CRUD / Layered | Clean Architecture if domain grows |
| SPA-API | Clean Architecture | CQRS if read/write patterns diverge |
| Modular-Monolith | Clean Architecture + Modules | Hexagonal if many integrations |
| Microservices | Clean Architecture per service | Hexagonal for integration-heavy services |
| Event-Driven | CQRS + Event Sourcing | Saga if distributed transactions needed |
| Worker-Service | Pipeline / Chain of Responsibility | — |
| Console-Batch | Procedural / Pipeline | — |

**Output Format:**
```
Architecture Style: [STYLE]
Confidence: HIGH / MEDIUM / LOW
Rationale: [Why this style fits]
Trade-offs: [What you give up]
Evolution Path: [How to evolve if complexity grows]
```

---

## P0.3 — Generate Project Profile

**Input:** Outputs from P0.1 and P0.2, plus any known constraints.

**Instruction:**
Generate a complete `project-profile.yaml` following the template in `00-project-profile/project-profile.yaml`. Fill in all known values and mark unknowns with `TBD`.

**Output:** Complete YAML file → `00-project-profile/project-profile.yaml`

---

## P0.4 — Complexity Assessment

**Input:** Project profile from P0.3.

**Instruction:**
Score the project across four dimensions:

| Dimension | Weight | Score (1–5) | Criteria |
|-----------|--------|-------------|----------|
| Domain Complexity | 35% | | 1=CRUD, 2=Rules, 3=Workflows, 4=State machines, 5=Event sourcing |
| Integration Complexity | 25% | | 1=None, 2=1–2 APIs, 3=3–5 systems, 4=Event-driven, 5=Legacy + real-time |
| Scale Requirements | 20% | | 1=Internal tool, 2=Department, 3=Company, 4=Public, 5=Global high-traffic |
| Team Factor | 20% | | 1=Expert team, 2=Senior, 3=Mixed, 4=Junior-heavy, 5=New team + new domain |

```
Complexity Score = Σ (Dimension Score × Weight)
```

| Score | Architecture Depth |
|-------|--------------------|
| 4.0–5.0 | Full: All prompts, deep design |
| 3.0–3.9 | Standard: Core prompts, moderate design |
| 2.0–2.9 | Light: Essential prompts, minimal design |
| < 2.0 | Minimal: Project structure + basic standards only |

---

## P0.5 — Technology Decision Guide

**Input:** Project profile, complexity score, team capabilities.

**Instruction:**
For each technology category, evaluate options and provide a recommendation:

| Category | Options to Evaluate | Decision Factors |
|----------|--------------------|--------------------|
| Runtime | .NET 8 / .NET 9 | LTS vs Current, feature needs |
| Frontend | Angular / React / Blazor / None | Team skills, requirements |
| Database | SQL Server / PostgreSQL / CosmosDB | Data model, scale, cost |
| ORM | EF Core / Dapper / Marten | Complexity, performance needs |
| Messaging | Azure Service Bus / RabbitMQ / Kafka | Volume, ordering, ecosystem |
| Cache | Redis / MemoryCache | Distribution needs |
| Identity | Entra ID / Auth0 / Duende | Enterprise vs B2C vs custom |
| Hosting | App Services / AKS / Container Apps | Scale, cost, ops capacity |
| Cloud Provider | Azure / AWS / GCP | Enterprise agreements, team expertise, service ecosystem |

**Cloud Provider Evaluation Matrix:**

| Factor | Azure | AWS | GCP |
|--------|-------|-----|-----|
| .NET ecosystem support | Excellent (first-class) | Good | Fair |
| Enterprise integration (AD, M365) | Native (Entra ID) | Via federation | Via federation |
| Managed Kubernetes | AKS (included) | EKS ($0.10/hr per cluster) | GKE (Autopilot) |
| Serverless (Functions) | Azure Functions | Lambda | Cloud Functions |
| Database (managed SQL) | Azure SQL, CosmosDB | RDS, DynamoDB | Cloud SQL, Firestore |
| Messaging | Service Bus, Event Grid | SQS, SNS, EventBridge | Pub/Sub |
| CI/CD integration | Azure DevOps, GitHub Actions | CodePipeline, GitHub Actions | Cloud Build, GitHub Actions |
| Cost model | Pay-as-you-go, Reserved, Enterprise | Pay-as-you-go, Reserved, Savings Plans | Pay-as-you-go, Committed Use |
| Team expertise | Evaluate | Evaluate | Evaluate |

> **Decision rule**: If the organization has an Enterprise Agreement with a cloud provider, default to that provider unless a specific service gap exists. Team expertise is the strongest factor after enterprise agreements.

**Output Format per category:**
```
Category: [CATEGORY]
Recommendation: [TECHNOLOGY]
Confidence: HIGH / MEDIUM / LOW
Rationale: [Why]
Trade-offs: [What you give up]
Alternative: [Second choice and when to prefer it]
```
