# Quality Gates

> Populated by: **Prompt P3.4** from [phase3-implementation.md](../08-ai/prompts/phase3-implementation.md)

---

## Gate Definitions

| Gate | Stage | Criteria | Blocking? |
|------|-------|----------|-----------|
| G1 — Build | CI | Compiles, no warnings-as-errors | Yes |
| G2 — Unit Tests | CI | All pass, coverage > threshold | Yes |
| G3 — Static Analysis | CI | No critical/high findings | Yes |
| G4 — Integration Tests | CI | All pass | Yes |
| G5 — Security Scan | CI | No critical CVEs | Yes |
| G6 — Architecture Rules | CI | No layer violations | Yes |
| G7 — Code Review | PR | At least 1 approval | Yes |
| G8 — Performance | Pre-Deploy | Latency < threshold | No (warning) |

---

## Static Analysis

| Tool | Purpose | Configuration |
|------|---------|---------------|
| Roslyn Analyzers | C# code quality | .editorconfig |
| SonarQube / SonarCloud | Quality gate dashboard | sonar-project.properties |
| dotnet format | Style enforcement | .editorconfig |
| SecurityCodeScan | Security vulnerabilities | NuGet analyzer |

---

## PR Checklist

- [ ] Code compiles with zero warnings
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] No new static analysis warnings
- [ ] Architecture tests pass
- [ ] Security scan clean
- [ ] Documentation updated (if public API changed)
- [ ] At least 1 code review approval

---

## Metrics Dashboard

| Metric | Current | Target | Trend |
|--------|---------|--------|-------|
| Test coverage | | 80%+ | |
| Build success rate | | 95%+ | |
| Mean time to fix | | < 1 day | |
| Technical debt ratio | | < 5% | |
| Security vulnerabilities | | 0 critical | |

---

## Related

- Testing strategy: [testing-strategy.md](testing-strategy.md) — gates verify test categories defined in the testing pyramid
- Observability: [observability-design.md](observability-design.md) — observability checks (health endpoints, structured logging) are quality gates
- CI/CD pipeline: [cicd-pipeline.md](../07-delivery/cicd-pipeline.md) — gates are enforced as pipeline stages

---

## Observations

- [ ] _Adjust gates based on project maturity — start with essentials, add over time_
