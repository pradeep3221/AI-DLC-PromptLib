# Phase 3 — Implementation & Delivery

> Define project structure, coding standards, testing strategy, quality gates, deployment, and CI/CD pipeline.

---

## P3.1 — Project Structure

**Input:** Architecture style (P2.1), technology selection (P2.2), bounded contexts (P1.4).

**Instruction:**
Define the solution structure and project layout.

**Steps:**
1. Define solution file (.sln) organization.
2. Define project structure per architectural layer (Domain, Application, Infrastructure, API).
3. Define shared/cross-cutting projects (SharedKernel, BuildingBlocks).
4. Define test project structure mirroring source projects.
5. Define folder conventions within each project.
6. Define dependency rules between layers (what can reference what).
7. Generate architecture test definitions to enforce layer boundaries.

**Structure Templates by Architecture Style:**

### Clean Architecture
```
src/
├── [Name].Domain/           ← Zero dependencies
├── [Name].Application/      ← Depends on Domain
├── [Name].Infrastructure/   ← Implements Application interfaces
└── [Name].API/              ← Composition root
```

### Modular Monolith
```
src/
├── Modules/
│   ├── [Module1]/
│   │   ├── [Module1].Domain/
│   │   ├── [Module1].Application/
│   │   ├── [Module1].Infrastructure/
│   │   └── [Module1].Contracts/     ← Public API for other modules
│   └── [Module2]/
├── [Name].API/                       ← Composition root
└── [Name].SharedKernel/
```

### Microservices
```
services/
├── [Service1]/
│   ├── src/
│   │   ├── [Service1].Domain/
│   │   ├── [Service1].Application/
│   │   ├── [Service1].Infrastructure/
│   │   └── [Service1].API/
│   └── tests/
├── [Service2]/
└── shared/
    └── BuildingBlocks/
```

**Output:** → `05-implementation/project-structure.md`

---

## P3.2 — Coding Standards & Patterns

**Input:** Technology selection, team experience, architecture style.

**Instruction:**
Define coding standards, naming conventions, and implementation patterns.

**Steps:**
1. C# coding conventions (naming, file organization, using directives).
2. Error handling strategy (Result types vs exceptions, Problem Details).
3. Dependency injection guidelines (lifetimes, registration, no service locator).
4. Implementation patterns by layer (see template).
5. Git workflow (branch naming, commit messages, PR requirements).
6. Code quality tooling (.editorconfig, analyzers, architecture tests).

**Calibrate depth based on team experience:**
- **Senior team:** Focus on patterns and architecture rules. Light on naming conventions.
- **Mixed/Junior team:** Detailed naming conventions, examples for each pattern, code review guidelines.

**Output:** → `05-implementation/coding-standards.md` + `05-implementation/implementation-patterns.md`

---

## P3.3 — Testing Strategy

**Input:** Architecture style, use case catalog, NFRs, complexity score.

**Instruction:**
Define the testing strategy across the testing pyramid.

**Steps:**
1. Define test categories and their scope (unit, integration, contract, E2E, architecture).
2. Set coverage targets by layer.
3. Define testing patterns (Arrange-Act-Assert, Builders, Fakes, Fixtures).
4. Define test project structure.
5. Define test data strategy (builders, fixtures, seeding, factories).
6. Identify critical paths requiring E2E tests.
7. Define performance testing approach (if NFRs require it).

**Right-sizing:**
- **Simple-API:** Unit + Integration tests only. 70% coverage target.
- **SPA-API:** Full pyramid. 80% coverage target.
- **Microservices:** Full pyramid + Contract tests. 80% coverage target.
- **Event-Driven:** Full pyramid + Saga tests. 85% coverage target.

**Output:** → `06-quality/testing-strategy.md`

---

## P3.4 — Quality Gates & Observability

**Input:** Testing strategy, NFRs, deployment strategy.

**Instruction:**
Define quality gates for CI/CD pipeline and observability design.

**Quality Gates:**
1. Build gate (compilation, warnings-as-errors).
2. Test gates (unit, integration, architecture).
3. Static analysis gate (analyzers, code quality).
4. Security scan gate (dependency vulnerabilities, SAST).
5. Coverage gate (minimum threshold).
6. Code review gate (approval requirements).
7. Performance gate (optional, for performance-critical paths).

**Observability:**
1. Logging strategy (structured logging, correlation IDs, log levels).
2. Metrics definition (request rate, error rate, latency, business metrics).
3. Tracing configuration (distributed tracing, span naming).
4. Health check endpoints (liveness, readiness, startup).
5. Alerting rules (conditions, severity, actions).
6. Dashboard definitions (service health, business metrics, infrastructure).

**Output:** → `06-quality/quality-gates.md` + `06-quality/observability-design.md`

---

## P3.5 — Deployment Strategy

**Input:** Project profile, NFRs (availability, compliance), infrastructure constraints.

**Instruction:**
Design the deployment and release strategy.

**Steps:**
1. Environment strategy (local, dev, staging, production).
2. Deployment pattern (blue-green, canary, rolling, recreate).
3. Rollback strategy and triggers.
4. Scaling rules (auto-scale triggers, min/max instances).
5. Release planning (MVP scope, sprint phases, release checklist).
6. Success criteria (KPIs, baseline metrics).

**Right-sizing:**
- **Simple-API:** App Service with deployment slots. Rolling deploy.
- **Microservices:** Kubernetes / Container Apps. Canary deploy. Independent releases.
- **Event-Driven:** Same as Microservices with additional event infrastructure.

**Output:** → `07-delivery/deployment-strategy.md` + `07-delivery/release-planning.md`

---

## P3.6 — CI/CD Pipeline & Infrastructure

**Input:** Technology selection, deployment strategy, quality gates.

**Instruction:**
Design the CI/CD pipeline and infrastructure-as-code.

**CI/CD Pipeline:**
1. Pipeline platform selection (GitHub Actions / Azure DevOps / GitLab CI).
2. Pipeline stages (Build → Test → Analyze → Package → Deploy).
3. Stage details (commands, gates, timeouts).
4. Branch strategy (trunk-based, GitFlow, GitHub Flow).
5. Artifact strategy (Docker images, NuGet packages, tags).
6. Secrets management (pipeline secrets, Key Vault integration).
7. Notification strategy (build failures, deployments, security findings).

**Infrastructure as Code:**
1. IaC tool selection (Bicep / Terraform / Pulumi).
2. Resource inventory per environment.
3. Resource topology diagram.
4. Environment differences (SKUs, replicas, scaling).
5. Tagging strategy.

**Output:** → `07-delivery/cicd-pipeline.md` + `07-delivery/infrastructure-as-code.md`
