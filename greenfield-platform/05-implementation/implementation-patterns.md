# Implementation Patterns

> Populated by: **Prompt P3.2** from [phase3-implementation.md](../08-ai/prompts/phase3-implementation.md)
>
> **Scope**: This file captures **coding-time patterns** — how to implement patterns in C# code, organized by architectural layer. For **design-time pattern decisions** (why each pattern was selected, trade-offs, anti-patterns), see [architecture-patterns.md](../02-architecture/architecture-patterns.md).

---

## Patterns by Layer

### Domain Layer

| Pattern | Usage | Example |
|---------|-------|---------|
| Aggregate | Consistency boundary | Order (root) → OrderLine (child) |
| Value Object | Immutable domain concept | Money, Address, Email |
| Domain Event | Side-effect notification | OrderCreatedEvent |
| Specification | Query encapsulation | ActiveOrdersSpec |
| Factory | Complex creation logic | Order.Create(…) |

### Application Layer

| Pattern | Usage | Example |
|---------|-------|---------|
| CQRS | Read/Write separation | CreateOrderCommand / OrderDetailsQuery |
| Mediator | Request routing | MediatR IRequestHandler |
| Pipeline Behavior | Cross-cutting concerns | ValidationBehavior, LoggingBehavior |
| Result Type | Error handling without exceptions | Result<OrderDto, Error> |

### Infrastructure Layer

| Pattern | Usage | Example |
|---------|-------|---------|
| Repository | Data access abstraction | IOrderRepository → EfOrderRepository |
| Unit of Work | Transaction management | DbContext.SaveChangesAsync() |
| Outbox | Reliable event publishing | Outbox table + background publisher |
| Specification (query) | Query building | EF Core IQueryable extensions |

### API Layer

| Pattern | Usage | Example |
|---------|-------|---------|
| Minimal API / Controllers | Endpoint definition | app.MapPost / [ApiController] |
| Middleware | Request pipeline | ExceptionMiddleware, CorrelationId |
| Filter | Action-level concerns | ValidationFilter |

---

## Cross-Cutting Patterns

| Concern | Pattern | Implementation |
|---------|---------|---------------|
| Logging | Structured logging | Serilog + ILogger<T> |
| Correlation | Request correlation | CorrelationId middleware |
| Caching | Cache-aside | IDistributedCache |
| Validation | Pipeline validation | FluentValidation + MediatR behavior |
| Authorization | Policy-based | [Authorize(Policy = "…")] |

---

## Observations

- [ ] _Select patterns appropriate for project complexity — not every project needs all patterns_
