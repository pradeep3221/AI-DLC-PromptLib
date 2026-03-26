# Team Topology Diagrams

> Visual templates for team structure, ownership boundaries, and communication patterns aligned with system architecture.

---

## 1. Team-to-Bounded-Context Alignment (Conway's Law)

```mermaid
graph TB
    subgraph Team Alpha
        T1[Team Alpha<br/>3 devs + 1 QA]
    end

    subgraph Team Beta
        T2[Team Beta<br/>4 devs + 1 QA]
    end

    subgraph Team Platform
        T3[Platform Team<br/>2 devs + 1 SRE]
    end

    subgraph Bounded Contexts
        BC1[Orders Context]
        BC2[Inventory Context]
        BC3[Payments Context]
        BC4[Shared Infrastructure]
    end

    T1 -->|Owns| BC1
    T1 -->|Owns| BC2
    T2 -->|Owns| BC3
    T3 -->|Owns| BC4

    BC1 ---|Domain Events| BC2
    BC1 ---|ACL| BC3
    BC1 --> BC4
    BC2 --> BC4
    BC3 --> BC4

    style T3 fill:#2196F3,color:white
```

---

## 2. Team Topologies — Four Types

```mermaid
graph TD
    subgraph Stream-Aligned Teams
        SA1[Orders Team]
        SA2[Customer Team]
        SA3[Analytics Team]
    end

    subgraph Enabling Team
        EN1[Architecture Guild]
    end

    subgraph Platform Team
        PT1[DevOps / Platform]
    end

    subgraph Complicated Subsystem
        CS1[ML / Recommendation Engine]
    end

    EN1 -.->|Facilitates| SA1
    EN1 -.->|Facilitates| SA2
    PT1 -->|X-as-a-Service| SA1
    PT1 -->|X-as-a-Service| SA2
    PT1 -->|X-as-a-Service| SA3
    CS1 -->|API| SA1
    CS1 -->|API| SA3

    style SA1 fill:#4CAF50,color:white
    style SA2 fill:#4CAF50,color:white
    style SA3 fill:#4CAF50,color:white
    style EN1 fill:#9C27B0,color:white
    style PT1 fill:#2196F3,color:white
    style CS1 fill:#FF9800,color:white
```

---

## 3. Code Ownership Map

```mermaid
graph TB
    subgraph Repository Structure
        Repo[Monorepo / Multi-Repo]
    end

    subgraph Ownership
        O1[src/Orders/**<br/>Owner: Team Alpha]
        O2[src/Payments/**<br/>Owner: Team Beta]
        O3[src/Shared/**<br/>Owner: Platform Team]
        O4[infra/**<br/>Owner: Platform Team]
        O5[tests/**<br/>Owner: All Teams]
    end

    Repo --> O1 & O2 & O3 & O4 & O5

    subgraph Review Policy
        R1[O1→ Alpha approves]
        R2[O2 → Beta approves]
        R3[O3 → Platform + Consumer team approve]
    end

    O1 --> R1
    O2 --> R2
    O3 --> R3
```

---

## 4. Communication & Dependency Flow

```mermaid
graph LR
    subgraph Team Alpha
        A[Orders Team]
    end

    subgraph Team Beta
        B[Payments Team]
    end

    subgraph Team Gamma
        C[Notifications Team]
    end

    subgraph Platform
        P[Platform Team]
    end

    A -->|API Contract| B
    A -->|Domain Events| C
    B -->|Domain Events| C
    A -.->|Needs from| P
    B -.->|Needs from| P
    C -.->|Needs from| P

    style A fill:#4CAF50,color:white
    style B fill:#FF9800,color:white
    style C fill:#9C27B0,color:white
    style P fill:#2196F3,color:white
```

---

## 5. Interaction Modes

| Team A | Team B | Mode | Description |
|--------|--------|------|-------------|
| Orders | Payments | **Collaboration** | Joint design of checkout flow |
| Orders | Platform | **X-as-a-Service** | Consume CI/CD, logging platform |
| Architecture Guild | Orders | **Facilitating** | Coaching on DDD patterns |
| Orders | Notifications | **Events** | Async via domain events |

```mermaid
graph TD
    subgraph Collaboration
        C1[Team A] <-->|Joint Design| C2[Team B]
    end

    subgraph X-as-a-Service
        X1[Consumer Team] -->|Uses| X2[Platform Team]
    end

    subgraph Facilitating
        F1[Enabling Team] -.->|Coaches| F2[Stream Team]
    end

    style C1 fill:#4CAF50,color:white
    style C2 fill:#4CAF50,color:white
    style X2 fill:#2196F3,color:white
    style F1 fill:#9C27B0,color:white
```

---

## 6. Scaling — Team Split Decision

```mermaid
graph TD
    Start[Single Team<br/>Owns Everything] --> Q1{Cognitive Load<br/>Too High?}
    Q1 -->|No| Stay[Keep Single Team]
    Q1 -->|Yes| Q2{Clear Domain<br/>Boundaries?}
    Q2 -->|Yes| Split[Split by<br/>Bounded Context]
    Q2 -->|No| Extract[Extract<br/>Platform Concerns]
    Split --> Val1[Each team owns<br/>1-2 contexts max]
    Extract --> Val2[Platform team<br/>serves shared infra]

    style Start fill:#FF9800,color:white
    style Split fill:#4CAF50,color:white
    style Extract fill:#2196F3,color:white
```

---

## Usage Notes

- Team boundaries should align with bounded contexts to minimize cross-team coordination
- Review [04-domain/bounded-contexts.md](../04-domain/bounded-contexts.md) to ensure alignment
- Update ownership maps when team responsibilities shift
- Reference: _Team Topologies_ by Skelton & Pais for Stream-Aligned, Enabling, Complicated Subsystem, and Platform team patterns
