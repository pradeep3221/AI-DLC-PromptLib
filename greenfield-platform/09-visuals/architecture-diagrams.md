# Architecture Diagrams

> Visual diagram templates for greenfield project design and architecture documentation.

---

## 1. Architecture Overview

```mermaid
graph TB
    Client[Client / SPA] --> Gateway[API Gateway]
    Gateway --> API1[Service A API]
    Gateway --> API2[Service B API]
    API1 --> DB1[(Database A)]
    API2 --> DB2[(Database B)]
    API1 --> MQ[Message Broker]
    API2 --> MQ
    MQ --> Worker[Worker Service]
    Worker --> DB1
    API1 --> Cache[(Cache)]
    API2 --> Cache
```

---

## 2. Clean Architecture Layers

```mermaid
graph TB
    subgraph Outer [Infrastructure & Presentation]
        API[API / Controllers]
        Infra[Infrastructure]
        UI[Frontend SPA]
    end
    subgraph Middle [Application]
        App[Application Services<br/>Commands, Queries, DTOs]
    end
    subgraph Core [Domain]
        Domain[Entities, Value Objects<br/>Domain Events, Interfaces]
    end
    API --> App
    Infra --> App
    App --> Domain
    UI --> API
```

---

## 3. Domain Context Map

```mermaid
graph LR
    subgraph Core Domain
        Orders[Orders Context]
    end
    subgraph Supporting
        Inventory[Inventory Context]
        Notifications[Notification Context]
    end
    subgraph Generic
        Identity[Identity Context]
        Payments[Payment Context]
    end
    Orders -->|Domain Events| Inventory
    Orders -->|Domain Events| Notifications
    Orders -->|ACL| Payments
    Identity -->|OHS| Orders
```

---

## 4. Deployment Topology

```mermaid
graph TB
    subgraph Cloud Region
        LB[Load Balancer]
        subgraph App Tier
            App1[Instance 1]
            App2[Instance 2]
        end
        subgraph Data Tier
            DB[(Primary DB)]
            DBR[(Read Replica)]
            Cache[(Redis Cache)]
        end
        subgraph Messaging
            MQ[Message Broker]
            DLQ[Dead Letter Queue]
        end
    end
    LB --> App1
    LB --> App2
    App1 --> DB
    App2 --> DB
    DB --> DBR
    App1 --> Cache
    App2 --> Cache
    App1 --> MQ
    App2 --> MQ
    MQ --> DLQ
```

---

## 5. CI/CD Pipeline Flow

```mermaid
graph LR
    Commit[Git Push] --> Build[Build]
    Build --> Test[Unit + Integration Tests]
    Test --> Analyze[Static Analysis + Security]
    Analyze --> Package[Docker Build & Push]
    Package --> DevDeploy[Deploy Dev]
    DevDeploy --> StageDeploy[Deploy Staging]
    StageDeploy --> Approve{Manual Approval}
    Approve -->|Yes| ProdDeploy[Deploy Production]
    Approve -->|No| Stop[Stop]
```

---

## 6. Event Flow Diagram

```mermaid
sequenceDiagram
    actor User
    participant API
    participant CommandHandler
    participant Aggregate
    participant EventBus
    participant Consumer

    User->>API: POST /orders
    API->>CommandHandler: CreateOrderCommand
    CommandHandler->>Aggregate: Create(...)
    Aggregate->>Aggregate: Validate & Apply Rules
    Aggregate-->>CommandHandler: OrderCreatedEvent
    CommandHandler->>EventBus: Publish(OrderCreatedEvent)
    EventBus->>Consumer: Handle(OrderCreatedEvent)
```

---

## 7. Testing Pyramid

```mermaid
pie title Test Distribution
    "Unit Tests" : 70
    "Integration Tests" : 20
    "Contract Tests" : 5
    "E2E Tests" : 5
```

---

## 8. Complexity Radar

```mermaid
pie title Complexity Score Breakdown
    "Domain Complexity (35%)" : 35
    "Integration Complexity (25%)" : 25
    "Scale Requirements (20%)" : 20
    "Team Factor (20%)" : 20
```
