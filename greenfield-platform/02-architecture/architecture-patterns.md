# Architecture Patterns

> Populated by: **Prompt P2.1** from [phase2-architecture.md](../08-ai/prompts/phase2-architecture.md)
>
> **Scope**: This file captures **design-time pattern decisions** — why a pattern was selected and its trade-offs. For **coding-time implementation** of these patterns (C# code structure, NuGet packages, layer assignments), see [implementation-patterns.md](../05-implementation/implementation-patterns.md).

---

## Selected Patterns

| Pattern | Purpose | Where Applied | Rationale |
|---------|---------|---------------|-----------|
| | | | |

---

## Pattern Details

### [Pattern Name]

**Category:** Structural / Behavioral / Integration / Data / Resilience

**Description:**
_What this pattern does and why we're using it._

**Implementation Approach:**

```
[High-level structure or pseudocode]
```

**Dependencies:**
- _Libraries or frameworks required_

**Trade-offs:**
- Pro: _benefit_
- Con: _cost_

---

## Anti-Patterns to Avoid

| Anti-Pattern | Risk | Prevention Strategy |
|-------------|------|-------------------|
| Distributed Monolith | High coupling between services defeats microservices benefits | Service autonomy checks, database-per-service |
| Anemic Domain Model | Business logic scattered across services instead of domain | Rich domain model, aggregate-based design |
| Chatty APIs | Excessive round trips between services | BFF pattern, aggregate endpoints |
| Shared Database | Tight coupling through shared data store | Database-per-service, eventual consistency |
| Big Ball of Mud | No clear boundaries or structure | Bounded contexts, modular architecture |

---

## Observations

- [ ] _AI-generated observations go here — review and validate with the team_
