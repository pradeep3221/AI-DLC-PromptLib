# Phase 1 — Requirements & Domain Discovery

> Capture functional and non-functional requirements, extract domain model, identify bounded contexts, catalog use cases, and perform event storming.

---

## P1.1 — Requirements Catalog

**Input:** Project brief, stakeholder interviews, existing documentation.

**Instruction:**
Extract and organize all functional requirements into a structured catalog.

**Steps:**
1. Identify all business capabilities the system must provide.
2. Group requirements by feature area or bounded context.
3. Assign priority (Must / Should / Could) using MoSCoW.
4. Write user stories in standard format: As a [role], I want [capability], so that [benefit].
5. Draft acceptance criteria in Given-When-Then format for each story.
6. Identify dependencies between features.

**Anti-Hallucination Rules:**
- Only extract requirements explicitly stated or clearly implied in the input.
- Tag any inferred requirements as **Confidence: MEDIUM** with rationale.
- Flag ambiguous requirements for stakeholder clarification.

**Output:** → `01-requirements/requirements-catalog.md`

---

## P1.2 — Non-Functional Requirements

**Input:** Project profile, stakeholder interviews, compliance requirements.

**Instruction:**
Identify and quantify all non-functional requirements (NFRs) across these categories:

| Category | Key Questions |
|----------|--------------|
| Performance | What response times are acceptable? What throughput is expected? |
| Scalability | How will load grow? Peak vs average? Geographic distribution? |
| Availability | What SLA is required? What's the cost of downtime? |
| Security | What data is sensitive? What compliance standards apply? |
| Observability | What must be monitored? What alerting is needed? |
| Operational | Deployment frequency? Rollback requirements? DR strategy? |

**Anti-Hallucination Rules:**
- Use industry benchmarks as defaults only when no specific requirement is stated.
- Tag default values as **Confidence: LOW** — they need stakeholder validation.
- Never assume compliance requirements — ask explicitly.

**Output:** → `01-requirements/nfr-catalog.md` + `01-requirements/acceptance-criteria.md`

---

## P1.3 — Domain Model Extraction

**Input:** Requirements catalog, project brief, domain expert interviews.

**Instruction:**
Extract the domain model by identifying:

1. **Entities** — Objects with identity that persist over time.
2. **Value Objects** — Immutable objects defined by their attributes.
3. **Aggregates** — Consistency boundaries grouping entities and value objects.
4. **Domain Events** — Significant things that happen in the domain.
5. **Domain Services** — Operations that don't belong to a single entity.

**For each aggregate, capture:**
- Root entity and child entities
- Invariants (rules that must always be true)
- Business rules with confidence levels
- Domain events it produces and consumes

**Anti-Hallucination Rules:**
- Only model concepts explicitly mentioned in requirements or domain descriptions.
- Tag inferred relationships as **Confidence: MEDIUM**.
- Mark complex business rules for domain expert validation.

**Output:** → `04-domain/domain-model.md`

---

## P1.4 — Bounded Context Identification

**Input:** Domain model from P1.3, requirements catalog.

**Instruction:**
Identify bounded contexts by applying these heuristics:

1. **Language boundaries** — Where the same word means different things (e.g., "Account" in billing vs identity).
2. **Change cadence** — Features that change together belong together.
3. **Team ownership** — Contexts should be ownable by a single team.
4. **Data ownership** — Each context owns its data, no shared databases.
5. **Strategic classification** — Core (competitive advantage), Supporting (necessary), Generic (commodity).

**For each bounded context, define:**
- Name and responsibility
- Aggregates it contains
- Ubiquitous language (key terms and definitions)
- Relationships with other contexts (pattern type: ACL, OHS, Conformist, Partnership, Shared Kernel)
- Integration events published and consumed

**When to skip:** Simple-API and Console-Batch projects typically don't need bounded context analysis.

**Output:** → `04-domain/bounded-contexts.md`

---

## P1.5 — Use Case Catalog

**Input:** Requirements catalog, domain model, bounded contexts.

**Instruction:**
Reverse-engineer use cases from the requirements:

1. Identify all actors (users, external systems, scheduled triggers).
2. For each actor, identify all interactions with the system.
3. For each interaction, document:
   - Use case name and ID
   - Actor(s)
   - Preconditions
   - Main flow (numbered steps)
   - Alternative flows
   - Error flows
   - Postconditions
   - Business rules applied
   - Domain events triggered
4. Map use cases to bounded contexts.
5. Classify complexity: S (Simple), M (Medium), L (Large), XL (Extra Large).
6. Prioritize for implementation order.

**Output:** → `04-domain/use-case-catalog.md`

---

## P1.6 — Event Storming

**Input:** Domain model, bounded contexts, use cases.

**Instruction:**
Perform a virtual event storming session:

1. **Domain Events** — List all significant events (past tense: OrderCreated, PaymentProcessed).
2. **Commands** — What triggers each event (imperative: CreateOrder, ProcessPayment).
3. **Aggregates** — Which aggregate handles each command.
4. **Policies** — Reactions: when [event] happens, then [command] is issued.
5. **Read Models** — Views needed to support queries.
6. **Hotspots** — Ambiguities, conflicts, or areas needing clarification.

**When to skip:** Simple-API and Console-Batch projects typically don't need event storming.

**Output:** → `04-domain/event-storming.md` + `04-domain/business-rules.md`
