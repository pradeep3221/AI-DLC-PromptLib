# Testing Strategy

> Populated by: **Prompt P3.3** from [phase3-implementation.md](../08-ai/prompts/phase3-implementation.md)

---

## Testing Pyramid

```
         /  E2E  \           ← Few: Critical user journeys
        / Contract \          ← Some: API contract verification
       / Integration \        ← More: Infrastructure + API tests
      /    Unit Tests  \      ← Many: Domain + Application layer
```

---

## Test Categories

| Category | Scope | Runner | Count Target |
|----------|-------|--------|-------------|
| Unit | Domain, Application | xUnit / NUnit | 70%+ of total |
| Integration | Infrastructure, API | xUnit + WebApplicationFactory | 20% |
| Contract | API contracts | Pact / WireMock | Per external integration |
| E2E | Full user flows | Playwright / Selenium | Critical paths only |
| Architecture | Layer dependency rules | NetArchTest / ArchUnitNET | Per project |

---

## Coverage Targets

| Layer | Target | Rationale |
|-------|--------|-----------|
| Domain | 90%+ | Business logic — highest risk |
| Application | 80%+ | Use case orchestration |
| Infrastructure | 60%+ | Integration verified by integration tests |
| API | 70%+ | Endpoint behavior |
| Overall | 80%+ | Balanced coverage |

---

## Testing Patterns

| Pattern | Purpose | Example |
|---------|---------|---------|
| Arrange-Act-Assert | Test structure | Standard unit test layout |
| Builder | Test data creation | OrderBuilder.WithItems(3).Build() |
| Fake / Stub | Dependency isolation | FakeOrderRepository |
| Integration fixture | Shared setup | WebApplicationFactory, Testcontainers |
| Snapshot testing | Contract verification | Verify JSON response shape |

---

## Test Organization

```
tests/
├── [Project].UnitTests/
│   ├── Domain/
│   │   ├── Orders/
│   │   │   └── OrderTests.cs
│   │   └── Shared/
│   └── Application/
│       └── Orders/
│           └── CreateOrderHandlerTests.cs
├── [Project].IntegrationTests/
│   ├── Api/
│   │   └── OrdersEndpointTests.cs
│   └── Infrastructure/
│       └── OrderRepositoryTests.cs
└── [Project].ArchTests/
    └── LayerDependencyTests.cs
```

---

## Test Data Strategy

| Approach | When to Use |
|----------|------------|
| Builders | Complex object creation in unit tests |
| Fixtures | Shared setup for integration tests |
| Seeding | Database state for integration tests |
| Factories | Randomized valid data (AutoFixture / Bogus) |

---

## Observations

- [ ] _Adjust coverage targets based on project risk and team capacity_
