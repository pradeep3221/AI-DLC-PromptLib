# Workflow Diagrams

> Visual diagrams for the legacy modernization assessment and migration process.

---

## 1. Assessment Flow (4-Layer Model)

```mermaid
graph TD
    subgraph "Phase 0: Assessment"
        P0[0.0 Project Classification] --> INV[0.1-0.6 Inventory]
        INV --> L1[Layer 1: Code Health]
        L1 --> L2[Layer 2: Service Assessment]
        L2 --> L3[Layer 3: Event Assessment]
        L3 --> L4[Layer 4: Domain Assessment]
        L4 --> SCORE[0.11 Scoring Engine]
    end
    
    subgraph "Phase 1: Discovery"
        SCORE --> D1[1.1-1.7 Core Extraction]
        D1 --> D2[1.8-1.17 Tech-Specific]
        D2 --> D3[1.18-1.29 Legacy Deep]
    end
    
    D3 --> DECIDE{Decision Matrix}
    DECIDE -->|≥4.0| REHOST[Rehost]
    DECIDE -->|3.0-3.9| REPLAT[Replatform]
    DECIDE -->|2.0-2.9| REFACT[Refactor + Modernize]
    DECIDE -->|<2.0| REARCH[Re-architect]
```

---

## 2. Migration Pattern: Strangler Fig

```mermaid
graph LR
    Client([Client]) --> Router{API Gateway}
    Router -->|New routes| NewAPI[New .NET 8 API]
    Router -->|Legacy routes| ACL[Anti-Corruption Layer]
    ACL --> Legacy[Legacy Application]
    NewAPI --> NewDB[(New Database)]
    ACL --> LegacyDB[(Legacy Database)]
    NewAPI -.->|Data Sync| LegacyDB
    
    style NewAPI fill:#4CAF50,color:white
    style Legacy fill:#f44336,color:white
    style ACL fill:#FF9800,color:white
```

---

## 3. Domain-Service-Event Triangulation

```mermaid
graph TD
    subgraph "Code Layer"
        C1[Entity: Order]
        C2[Entity: Customer]
        C3[Entity: Payment]
    end
    
    subgraph "Service Layer"
        S1[OrderService]
        S2[CustomerService]
        S3[PaymentService]
    end
    
    subgraph "Event Layer"
        E1[OrderCreated]
        E2[PaymentReceived]
        E3[???]
    end
    
    C1 ---|✅ Aligned| S1
    S1 ---|✅ Aligned| E1
    C2 ---|✅ Aligned| S2
    S2 ---|❌ No Event| E3
    C3 ---|✅ Aligned| S3
    S3 ---|✅ Aligned| E2
```

---

## 4. Scoring Radar Template

```mermaid
%%{init: {'theme': 'base'}}%%
pie title Assessment Score Distribution
    "Code Health" : 35
    "Architecture Fitness" : 35
    "Migration Readiness" : 30
```

---

## 5. Migration Wave Timeline

```mermaid
gantt
    title Migration Wave Plan
    dateFormat  YYYY-MM-DD
    
    section Phase 1 - Stabilize
    Add monitoring         :a1, 2026-04-01, 14d
    Increase test coverage :a2, 2026-04-01, 30d
    Document rules         :a3, 2026-04-08, 21d
    
    section Phase 2 - Decouple
    Remove shared DB       :b1, after a2, 30d
    Add API boundaries     :b2, after a2, 21d
    Add ACLs               :b3, after b2, 14d
    
    section Phase 3 - Migrate
    Migrate .NET version   :c1, after b1, 30d
    Replace libraries      :c2, after c1, 14d
    Performance testing    :c3, after c2, 14d
    
    section Phase 4 - Optimize
    Containerize           :d1, after c3, 21d
    Add observability      :d2, after c3, 14d
```

---

## 6. Dependency Graph Template

> Replace with actual dependency graph generated from code analysis.
> Export as PNG to `dependency-graph.png` in this folder.

```mermaid
graph TD
    subgraph "UI Layer"
        WebApp[Web Application]
        Admin[Admin Portal]
    end
    
    subgraph "Service Layer"
        API[API Service]
        Worker[Worker Service]
    end
    
    subgraph "Data Layer"
        DAL[Data Access]
        Cache[Cache Service]
    end
    
    subgraph "External"
        DB[(SQL Server)]
        Queue[Message Queue]
        ExtAPI[External API]
    end
    
    WebApp --> API
    Admin --> API
    API --> DAL
    API --> Cache
    API --> Queue
    Worker --> Queue
    Worker --> DAL
    DAL --> DB
    API --> ExtAPI
```
