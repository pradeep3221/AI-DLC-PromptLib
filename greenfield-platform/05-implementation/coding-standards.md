# Coding Standards

> Populated by: **Prompt P3.2** from [phase3-implementation.md](../08-ai/prompts/phase3-implementation.md)

---

## General Principles

| Principle | Guideline |
|-----------|-----------|
| SOLID | Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion |
| DRY | Don't Repeat Yourself — but prefer duplication over wrong abstraction |
| YAGNI | You Ain't Gonna Need It — don't build for hypothetical requirements |
| KISS | Keep It Simple — simplest solution that works |

---

## C# Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Classes | PascalCase | `OrderService` |
| Interfaces | I-prefix PascalCase | `IOrderRepository` |
| Methods | PascalCase, verb | `CreateOrder()` |
| Properties | PascalCase | `OrderDate` |
| Private fields | _camelCase | `_orderRepository` |
| Local variables | camelCase | `orderTotal` |
| Constants | PascalCase | `MaxRetryCount` |
| Async methods | Suffix with Async | `GetOrderAsync()` |
| Boolean properties | Is/Has/Can prefix | `IsActive`, `HasPermission` |

---

## File Organization

| Rule | Detail |
|------|--------|
| One class per file | Exceptions: nested private classes, record types |
| File name = class name | `OrderService.cs` contains `OrderService` |
| Folder = namespace | Folder structure matches namespace hierarchy |
| Using directives | Global usings in `GlobalUsings.cs`, file-scoped namespaces |

---

## Error Handling

| Rule | Detail |
|------|--------|
| Use Result types | Prefer `Result<T>` over exceptions for expected failures |
| Domain exceptions | Use for invariant violations in domain layer |
| Never swallow exceptions | Always log or rethrow |
| Problem Details | API returns RFC 7807 for all errors |
| Validation | FluentValidation at application layer boundary |

---

## Dependency Injection

| Rule | Detail |
|------|--------|
| Register in composition root | Program.cs or extension methods |
| Use interfaces | Depend on abstractions, not concrete types |
| Lifetime awareness | Scoped for DB, Singleton for config, Transient for stateless |
| No service locator | Never inject IServiceProvider into business code |

---

## Code Quality

| Tool | Purpose | Configuration |
|------|---------|---------------|
| .editorconfig | Code style enforcement | Solution-level |
| Analyzers | Static analysis | Microsoft.CodeAnalysis, SonarAnalyzer |
| Architecture tests | Layer dependency rules | NetArchTest / ArchUnitNET |

---

## Git Standards

| Element | Convention |
|---------|-----------|
| Branch naming | feature/[ticket]-[description], bugfix/[ticket]-[description] |
| Commit messages | Conventional Commits: feat:, fix:, refactor:, docs:, test: |
| PR requirements | At least 1 review, all checks green, no merge conflicts |

---

## Observations

- [ ] _Adjust standards based on team experience and project complexity_
