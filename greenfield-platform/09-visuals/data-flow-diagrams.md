# Data Flow Diagrams

> Visual templates for data movement, transformation, and state transitions in greenfield projects.

---

## 1. API Request/Response Flow

```mermaid
sequenceDiagram
    actor Client
    participant GW as API Gateway
    participant Auth as Auth Service
    participant API as Application API
    participant Cache as Cache Layer
    participant DB as Database

    Client->>GW: HTTP Request + JWT
    GW->>Auth: Validate Token
    Auth-->>GW: Token Valid
    GW->>API: Forward Request
    API->>Cache: Check Cache
    alt Cache Hit
        Cache-->>API: Cached Data
    else Cache Miss
        API->>DB: Query
        DB-->>API: Result Set
        API->>Cache: Populate Cache
    end
    API-->>GW: Response DTO
    GW-->>Client: HTTP Response
```

---

## 2. CQRS Data Flow

```mermaid
graph LR
    subgraph Write Side
        Client1[Client] -->|Command| CmdAPI[Command API]
        CmdAPI --> CmdHandler[Command Handler]
        CmdHandler --> Aggregate[Domain Aggregate]
        Aggregate --> WriteDB[(Write Store)]
        Aggregate -->|Domain Event| Bus[Event Bus]
    end

    subgraph Read Side
        Bus -->|Project| Projector[Projection Handler]
        Projector --> ReadDB[(Read Store)]
        ReadDB --> QueryAPI[Query API]
        QueryAPI --> Client2[Client]
    end

    style WriteDB fill:#4CAF50,color:white
    style ReadDB fill:#2196F3,color:white
```

---

## 3. Event Sourcing Data Flow

```mermaid
sequenceDiagram
    participant Cmd as Command Handler
    participant Agg as Aggregate
    participant ES as Event Store
    participant Proj as Projector
    participant Read as Read Model

    Cmd->>Agg: Load from Events
    ES-->>Agg: Historical Events
    Agg->>Agg: Apply Command & Business Rules
    Agg->>ES: Append New Events
    ES->>Proj: Stream Events
    Proj->>Read: Update Projection
```

---

## 4. Data Pipeline (ETL / Ingestion)

```mermaid
graph LR
    subgraph Sources
        S1[REST API]
        S2[File Upload]
        S3[Message Queue]
    end

    subgraph Processing
        Ingest[Ingestion Service]
        Validate[Validation]
        Transform[Transformation]
        Enrich[Enrichment]
    end

    subgraph Storage
        Raw[(Raw / Staging)]
        Clean[(Processed Store)]
        Archive[(Archive / Cold)]
    end

    S1 --> Ingest
    S2 --> Ingest
    S3 --> Ingest
    Ingest --> Validate
    Validate -->|Invalid| DLQ[Dead Letter Queue]
    Validate -->|Valid| Transform
    Transform --> Enrich
    Ingest --> Raw
    Enrich --> Clean
    Raw -->|TTL| Archive
```

---

## 5. State Machine — Order Lifecycle

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> Submitted : Submit()
    Submitted --> Validated : Validate()
    Validated --> Approved : Approve()
    Validated --> Rejected : Reject()
    Approved --> Processing : StartProcessing()
    Processing --> Completed : Complete()
    Processing --> Failed : Error()
    Failed --> Processing : Retry()
    Rejected --> [*]
    Completed --> [*]

    note right of Validated
        Business rules applied
        at this transition
    end note
```

---

## 6. Multi-Service Data Synchronization

```mermaid
graph TD
    subgraph Service A
        A_API[API] --> A_DB[(DB A)]
        A_DB -->|CDC / Outbox| A_Event[Domain Events]
    end

    subgraph Event Infrastructure
        A_Event --> Broker[Message Broker]
    end

    subgraph Service B
        Broker --> B_Consumer[Event Consumer]
        B_Consumer --> B_DB[(DB B)]
    end

    subgraph Service C
        Broker --> C_Consumer[Event Consumer]
        C_Consumer --> C_DB[(DB C)]
    end

    style Broker fill:#FF9800,color:white
```

---

## 7. Authentication & Token Flow

```mermaid
sequenceDiagram
    actor User
    participant SPA as Frontend SPA
    participant IDP as Identity Provider
    participant API as Resource API
    participant DB as User Store

    User->>SPA: Login
    SPA->>IDP: Authorization Request (PKCE)
    IDP->>User: Login Prompt
    User->>IDP: Credentials
    IDP->>DB: Validate
    DB-->>IDP: User Record
    IDP-->>SPA: Auth Code
    SPA->>IDP: Exchange Code for Tokens
    IDP-->>SPA: Access Token + Refresh Token
    SPA->>API: API Call + Bearer Token
    API->>API: Validate JWT
    API-->>SPA: Protected Resource
```

---

## Usage Notes

- Replace placeholder entity names (Order, Service A) with actual domain entities
- State machines should reflect your domain's actual lifecycle rules
- For event sourcing, document the event schema alongside these diagrams
- Export complex diagrams to PNG for stakeholder presentations
