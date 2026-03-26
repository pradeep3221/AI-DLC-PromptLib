# Workflow Automation — Greenfield Platform

> Workflow definitions for AI-assisted greenfield project design pipeline.

---

## Design Pipeline

```mermaid
graph TD
    Start([Start]) --> P0{Phase 0: Classify}
    P0 --> Profile[project-profile.yaml]
    Profile --> Type{Project Type?}

    Type -->|Simple-API| Light[Light Path]
    Type -->|SPA-API| Standard[Standard Path]
    Type -->|Modular-Monolith| Deep[Deep Path]
    Type -->|Microservices| Deep
    Type -->|Event-Driven| Deep

    Light --> P1L[P1: Requirements Light]
    Standard --> P1S[P1: Requirements Standard]
    Deep --> P1D[P1: Requirements Full]

    P1L --> Review1{Human Review}
    P1S --> Review1
    P1D --> Review1

    Review1 --> P2[Phase 2: Architecture]
    P2 --> Review2{Human Review}
    Review2 --> P3[Phase 3: Implementation]
    P3 --> Review3{Human Review}
    Review3 --> Scaffold([Scaffold & Build])
```

---

## Workflow Steps

| Step | Phase | Input | Output | Human Review? |
|------|-------|-------|--------|---------------|
| 1 | P0: Classify | Project brief | project-profile.yaml | Yes — validate classification |
| 2 | P1: Requirements | Profile + stakeholder input | Requirements, domain model, use cases | Yes — validate domain boundaries |
| 3 | P2: Architecture | Requirements + domain model | ADRs, API, data model, security | Yes — validate decisions |
| 4 | P3: Implementation | Architecture outputs | Structure, standards, CI/CD, deployment | Yes — validate pipeline |
| 5 | Scaffold | All outputs | Runnable project scaffold | Yes — final review |

---

## Integration Points

| Platform | Integration |
|----------|------------|
| GitHub Copilot | Run prompts directly in IDE |
| Azure OpenAI | API-based prompt execution |
| GitHub Actions | Automated scaffold generation |
| Azure DevOps | Pipeline template generation |

---

## Automation Levels

| Level | Description | What's Automated |
|-------|-------------|-----------------|
| L1 — Manual | Run prompts manually in AI chat | Nothing — copy/paste |
| L2 — Semi-Auto | Use scripts to run prompts sequentially | Prompt execution pipeline |
| L3 — Auto + Review | Automated pipeline with human checkpoints | Prompt execution + output population |
| L4 — Full Auto | Fully automated design-to-scaffold | Include project scaffold generation |
