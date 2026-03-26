# Workflow Diagrams

> Visual templates for the greenfield design process, development workflows, and decision flows.

---

## 1. Greenfield Design Process (4-Phase Model)

```mermaid
graph TD
    subgraph "Phase 0: Classification"
        P0[Project Profiling] --> P0A[Type Classification]
        P0A --> P0B[Complexity Scoring]
        P0B --> P0C[Depth Recommendation]
    end

    subgraph "Phase 1: Requirements & Domain"
        P0C --> P1A[Functional Requirements]
        P1A --> P1B[Non-Functional Requirements]
        P1B --> P1C[Domain Modeling]
        P1C --> P1D[Bounded Contexts]
        P1D --> P1E[Use Case Catalog]
    end

    subgraph "Phase 2: Architecture & Design"
        P1E --> P2A[Architecture Decisions - ADRs]
        P2A --> P2B[Technology Selection]
        P2B --> P2C[API & Data Design]
        P2C --> P2D[Security & Resilience]
    end

    subgraph "Phase 3: Implementation & Delivery"
        P2D --> P3A[Project Structure]
        P3A --> P3B[Coding Standards]
        P3B --> P3C[Testing Strategy]
        P3C --> P3D[CI/CD & Deployment]
        P3D --> P3E[Infrastructure as Code]
    end

    P3E --> Ready{Ready to Build}
    Ready -->|Yes| Scaffold[Scaffold Solution]
    Ready -->|No| Review[Review Gaps]
    Review --> P1A
```

---

## 2. Architecture Decision Flow

```mermaid
graph TD
    Need[Identify Architecture Need] --> Context[Gather Context & Constraints]
    Context --> Options[List Options with Trade-offs]
    Options --> Evaluate[Evaluate Against NFRs]
    Evaluate --> Decide{Decision}
    Decide -->|Option A| ADR[Record ADR]
    Decide -->|Option B| ADR
    Decide -->|Need More Info| Spike[Spike / Prototype]
    Spike --> Evaluate
    ADR --> Implement[Implement Decision]
    Implement --> Validate[Validate with Tests]
    Validate --> Monitor[Monitor in Production]
    Monitor --> Revisit{Revisit Needed?}
    Revisit -->|Yes| Need
    Revisit -->|No| Done[Decision Stable]

    style ADR fill:#4CAF50,color:white
    style Spike fill:#FF9800,color:white
```

---

## 3. Technology Selection Workflow

```mermaid
graph TD
    Req[Identify Requirement] --> Candidates[Research Candidates]
    Candidates --> Matrix[Build Evaluation Matrix]
    Matrix --> POC[Proof of Concept]

    POC --> Score{Score ≥ Threshold?}
    Score -->|Yes| Select[Select Technology]
    Score -->|No| Alt[Next Candidate]
    Alt --> POC

    Select --> ADR[Record in ADR]
    ADR --> Integrate[Integrate into Architecture]

    subgraph Evaluation Criteria
        E1[Maturity & Community]
        E2[Performance & Scalability]
        E3[Team Expertise]
        E4[Licensing & Cost]
        E5[Security & Compliance]
    end

    Matrix --> E1 & E2 & E3 & E4 & E5
```

---

## 4. Sprint / Development Workflow

```mermaid
graph LR
    Backlog[Product Backlog] --> Refine[Refinement]
    Refine --> Sprint[Sprint Planning]
    Sprint --> Dev[Development]

    Dev --> PR[Pull Request]
    PR --> Review[Code Review]
    Review -->|Approved| Merge[Merge to Main]
    Review -->|Changes| Dev
    Merge --> CI[CI Pipeline]
    CI -->|Pass| Deploy[Deploy to Dev/Staging]
    CI -->|Fail| Fix[Fix Build]
    Fix --> Dev
    Deploy --> QA[QA Validation]
    QA -->|Pass| Release[Release Candidate]
    QA -->|Fail| Bug[Bug Fix]
    Bug --> Dev
    Release --> Prod[Deploy to Production]
```

---

## 5. Code Review Checklist Flow

```mermaid
graph TD
    PR[Pull Request Created] --> A{Builds & Tests Pass?}
    A -->|No| Fix1[Fix CI Issues]
    A -->|Yes| B{Follows Coding Standards?}
    B -->|No| Fix2[Apply Standards]
    B -->|Yes| C{Security Review OK?}
    C -->|No| Fix3[Address Security]
    C -->|Yes| D{Domain Logic Correct?}
    D -->|No| Fix4[Fix Domain Logic]
    D -->|Yes| E{Test Coverage Adequate?}
    E -->|No| Fix5[Add Tests]
    E -->|Yes| F{Documentation Updated?}
    F -->|No| Fix6[Update Docs]
    F -->|Yes| Approve[Approve & Merge]

    Fix1 --> A
    Fix2 --> B
    Fix3 --> C
    Fix4 --> D
    Fix5 --> E
    Fix6 --> F

    style Approve fill:#4CAF50,color:white
```

---

## 6. Incident Response Workflow

```mermaid
graph TD
    Alert[Alert Triggered] --> Triage{Severity?}
    Triage -->|P1 Critical| Page[Page On-Call]
    Triage -->|P2 High| Notify[Notify Team Channel]
    Triage -->|P3 Medium| Queue[Add to Queue]

    Page --> Investigate[Investigate]
    Notify --> Investigate
    Queue --> Investigate

    Investigate --> Mitigate{Can Mitigate?}
    Mitigate -->|Yes| Fix[Apply Fix / Rollback]
    Mitigate -->|No| Escalate[Escalate]
    Escalate --> Investigate

    Fix --> Verify[Verify Resolution]
    Verify --> Postmortem[Blameless Post-Mortem]
    Postmortem --> Action[Action Items → Backlog]

    style Page fill:#f44336,color:white
    style Notify fill:#FF9800,color:white
    style Queue fill:#4CAF50,color:white
```

---

## 7. Project Execution Path by Type

```mermaid
graph TD
    Start[Project Profile] --> Type{Project Type?}

    Type -->|Simple API| Path1[Minimal Path]
    Type -->|SPA + API| Path2[Standard Path]
    Type -->|Modular Monolith| Path3[Full Path]
    Type -->|Microservices| Path4[Extended Path]
    Type -->|Event-Driven| Path5[Extended + Events Path]

    Path1 --> P1_Steps["Classification → Requirements →<br/>API Design → Implement"]
    Path2 --> P2_Steps["Classification → Requirements →<br/>Domain → Architecture →<br/>API + Frontend → Implement"]
    Path3 --> P3_Steps["Full Phase 0–3<br/>+ Module Boundaries<br/>+ Integration Tests"]
    Path4 --> P4_Steps["Full Phase 0–3<br/>+ Service Decomposition<br/>+ Contract Tests<br/>+ Infrastructure"]
    Path5 --> P5_Steps["Full Phase 0–3<br/>+ Event Storming<br/>+ Saga Design<br/>+ Event Store"]

    style Path1 fill:#4CAF50,color:white
    style Path2 fill:#8BC34A,color:white
    style Path3 fill:#FF9800,color:white
    style Path4 fill:#f44336,color:white
    style Path5 fill:#9C27B0,color:white
```

---

## Usage Notes

- The Phase 0–3 flow aligns with [QUICKSTART.md](../QUICKSTART.md) execution steps
- Decision flows should result in ADRs recorded in [02-architecture/architecture-decisions.md](../02-architecture/architecture-decisions.md)
- Sprint workflows should align with your CI/CD pipeline in [07-delivery/cicd-pipeline.md](../07-delivery/cicd-pipeline.md)
- Incident response should connect to observability setup in [06-quality/observability-design.md](../06-quality/observability-design.md)
