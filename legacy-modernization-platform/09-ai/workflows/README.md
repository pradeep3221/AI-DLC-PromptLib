# AI Workflows

> Workflow definitions for automating the assessment pipeline using GenAI.

---

## 1. Assessment Pipeline Workflow

```mermaid
graph TD
    Start([Start]) --> Classify[P0 Classify Project]
    Classify --> Profile[Generate project-profile.yaml]
    Profile --> Inventory[P1.1-P1.6 Inventory & Baseline]
    Inventory --> CodeHealth[P2 Code Health]
    CodeHealth --> Decision{Project Intent?}
    
    Decision -->|Enhancement| Done([Lightweight Done])
    Decision -->|Modernization| FullAssess[P3.1-P3.6 Architecture Scoring]
    Decision -->|Migration| FullAssess
    
    FullAssess --> Discovery[Phase 4: Domain Discovery]
    Discovery --> Core[P4.1-P4.7 Core Extraction]
    Core --> Tech{Multi-tech?}
    
    Tech -->|Yes| TechPrompts[P5.1-P5.10 Tech-Specific]
    Tech -->|No| Legacy[P6.1-P6.12 Legacy Deep]
    TechPrompts --> Legacy
    
    Legacy --> Scoring[Generate Scores]
    Scoring --> Strategy[Generate Strategy]
    Strategy --> Done2([Full Assessment Done])
```

---

## 2. Workflow Steps

| Step | Input | AI Prompt | Output | Human Review? |
|:----:|-------|-----------|--------|:------------:|
| 1 | Repo URL | P0.1–P0.5 | project-profile.yaml | ✅ Validate classification |
| 2 | Source code | P1.1–P1.6 | application-inventory.md | Optional |
| 3 | Source code | P2 | code-layer.md | Optional |
| 4 | Assessment data | P3.1–P3.6 | Scoring files | ✅ Validate scores |
| 5 | Source code | P4.1–P6.12 | domain-mapping.md | ✅ Validate UNCERTAIN rules |
| 6 | All outputs | Decision matrix | strategy.md | ✅ Approve strategy |

---

## 3. Integration Points

| Platform | Integration Method | Notes |
|---------|-------------------|-------|
| Azure OpenAI | REST API / SDK | For prompt execution |
| AWS Bedrock | Bedrock API | Alternative AI backend |
| GitHub Actions | CI workflow | Automated on PR |
| CLI Tool | `dotnet legacy-analyzer` | Local development |

---

## 4. Automation Levels

| Level | Description | Human Involvement |
|:-----:|------------|-------------------|
| **L1** | Manual prompt execution | Copy-paste prompts, review all outputs |
| **L2** | Semi-automated pipeline | AI generates, human reviews |
| **L3** | Fully automated with checkpoints | AI generates + validates, human approves strategy |
| **L4** | Continuous assessment | Runs on every commit, alerts on regression |
