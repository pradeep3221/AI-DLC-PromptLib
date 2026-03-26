# Phase 2 — Architecture & Design

> Produce architecture decisions, API contracts, data model, security design, and integration/resilience design.

---

## P2.1 — Architecture Decision Records

**Input:** Project profile, complexity score, requirements catalog, domain model.

**Instruction:**
Generate Architecture Decision Records (ADRs) for the key decisions this project requires.

**Mandatory ADRs:**
1. **Architecture Style** — Why this style over alternatives.
2. **Project Structure** — Monorepo vs polyrepo, solution layout.
3. **Communication Pattern** — Sync (REST/gRPC) vs Async (messaging), or both.
4. **Data Persistence** — Database choice, ORM, migration strategy.
5. **Error Handling** — Result types vs exceptions, global error handling.

**Conditional ADRs (based on project type):**
6. **Event Strategy** — Event sourcing, outbox pattern, idempotency (Event-Driven / Microservices).
7. **Service Boundaries** — How services are partitioned (Microservices).
8. **Module Boundaries** — How modules are isolated (Modular Monolith).
9. **Frontend Architecture** — SPA framework, state management, API communication (SPA-API).

**ADR Format:**
```
## ADR-[NNN]: [Title]
**Status:** Proposed / Accepted / Deprecated / Superseded
**Context:** [What's the problem?]
**Decision:** [What did we choose?]
**Alternatives Considered:**
| Option | Pros | Cons |
**Consequences:** [What follows from this decision?]
**Confidence:** HIGH / MEDIUM / LOW
```

**Output:** → `02-architecture/architecture-decisions.md`

---

## P2.2 — Technology Selection

**Input:** Project profile (P0.3), technology decision guide (P0.5), team capabilities.

**Instruction:**
Finalize technology selections with detailed rationale for each category.

**For each technology choice, provide:**
1. Selected technology and version
2. Selection rationale (why this over alternatives)
3. Team readiness assessment
4. Risk factors and mitigations
5. NuGet/package baseline (key libraries to include)

**Evaluation criteria per category:**
- Maturity & community support
- Team experience
- Performance characteristics
- Licensing & cost
- Ecosystem integrations
- Long-term viability

**Anti-Hallucination Rules:**
- Only recommend packages that exist and are actively maintained.
- State the latest stable version number only if confident.
- Flag any experimental or pre-release recommendations.

**Output:** → `02-architecture/technology-selection.md` + `02-architecture/architecture-patterns.md`

---

## P2.3 — API Design

**Input:** Use case catalog, bounded contexts, NFRs.

**Instruction:**
Design the API contracts for the system.

**Steps:**
1. Define API design standards (naming, versioning, pagination, error format).
2. Catalog all endpoints grouped by resource/aggregate.
3. Define request/response contracts (DTOs) for each endpoint.
4. Design authentication and authorization per endpoint.
5. Define rate limiting and throttling policies.
6. Create API dependency diagram.

**Design Principles:**
- RESTful: Resources as nouns, HTTP verbs for actions, proper status codes.
- Consistency: Same patterns across all endpoints.
- Minimality: Only expose what consumers need. Avoid leaking domain model.
- Versioning: Strategy for backward compatibility.

**When to skip:** Worker-Service and Console-Batch projects without HTTP interfaces.

**Output:** → `03-design/api-contracts.md`

---

## P2.4 — Data Model Design

**Input:** Domain model, bounded contexts, NFRs (performance, scale).

**Instruction:**
Design the data persistence layer.

**Steps:**
1. Map aggregates to database tables/collections.
2. Define entity schemas (columns, types, constraints, indexes).
3. Design relationships (foreign keys, navigation properties).
4. Identify access patterns and design indexes accordingly.
5. Plan data migration strategy (tooling, naming, versioning).
6. Design caching strategy for hot data paths.

**Considerations:**
- Database-per-service vs shared database (based on architecture style).
- Read model separation if CQRS.
- Event store design if event sourcing.
- Data archival and retention policies.

**Output:** → `03-design/data-model.md`

---

## P2.5 — Security Design

**Input:** NFRs (security, compliance), project profile, integration catalog.

**Instruction:**
Design the security architecture.

**Steps:**
1. Authentication strategy (identity provider, token format, flows).
2. Authorization model (RBAC, ABAC, policy-based) with role/permission matrix.
3. Data protection (encryption at rest, in transit, field-level).
4. Secrets management (Key Vault, environment variables, rotation).
5. Security headers and CORS policy.
6. Audit logging requirements.
7. Threat model (top 5 threats + mitigations).

**Anti-Hallucination Rules:**
- Never assume compliance requirements — only include those explicitly stated.
- Use OWASP Top 10 as a baseline threat model.
- Recommend proven patterns — no experimental security approaches.

**Output:** → `03-design/security-model.md`

---

## P2.6 — Resilience & Integration Design

**Input:** Integration points from requirements, NFRs (availability, reliability), bounded contexts.

**Instruction:**
Design resilience patterns and external system integrations.

**Resilience Design:**
1. Retry policies (per integration type: HTTP, database, messaging).
2. Circuit breaker configuration.
3. Timeout policies.
4. Bulkhead isolation.
5. Fallback strategies.
6. Health check endpoints.
7. Error handling strategy by layer.

**Integration Design:**
1. Catalog all external system integrations.
2. For each integration: protocol, auth, SLA, error handling, data mapping.
3. Anti-corruption layer design for each external system.
4. Event-based integration design (if applicable).
5. Data flow diagrams.

**Output:** → `03-design/integration-design.md` + `03-design/resilience-design.md`
