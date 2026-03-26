# Infrastructure Diagrams

> Visual templates for cloud infrastructure, networking, and container orchestration layouts.

---

## 1. Cloud Resource Topology (Azure)

```mermaid
graph TB
    subgraph Azure Subscription
        subgraph Resource Group
            subgraph Networking
                VNET[Virtual Network]
                NSG[Network Security Group]
                AGW[Application Gateway / WAF]
            end

            subgraph Compute
                AKS[AKS Cluster]
                FUNC[Azure Functions]
            end

            subgraph Data
                SQL[(Azure SQL)]
                Redis[(Azure Cache for Redis)]
                SB[Service Bus]
                Storage[Blob Storage]
            end

            subgraph Observability
                AI[Application Insights]
                LA[Log Analytics]
            end

            subgraph Security
                KV[Key Vault]
                AAD[Entra ID]
            end
        end
    end

    AGW --> AKS
    AKS --> SQL
    AKS --> Redis
    AKS --> SB
    AKS --> Storage
    AKS --> KV
    FUNC --> SB
    FUNC --> SQL
    AKS --> AI
    FUNC --> AI
    AI --> LA
    AAD --> AGW
```

---

## 2. Kubernetes Cluster Layout

```mermaid
graph TB
    subgraph AKS Cluster
        subgraph Ingress
            Nginx[Ingress Controller]
        end

        subgraph Namespace: app
            API1[api-service<br/>3 replicas]
            API2[worker-service<br/>2 replicas]
            API3[bff-service<br/>2 replicas]
        end

        subgraph Namespace: infrastructure
            Redis[Redis]
            RabbitMQ[RabbitMQ]
        end

        subgraph Namespace: monitoring
            Prom[Prometheus]
            Grafana[Grafana]
            Jaeger[Jaeger]
        end
    end

    Nginx --> API1
    Nginx --> API3
    API1 --> Redis
    API1 --> RabbitMQ
    API2 --> RabbitMQ
    API1 --> Prom
    API2 --> Prom
    Prom --> Grafana
    API1 --> Jaeger
```

---

## 3. Network Topology

```mermaid
graph TB
    Internet[Internet] --> WAF[WAF / CDN]
    WAF --> LB[Load Balancer]

    subgraph DMZ
        LB --> APIGW[API Gateway]
    end

    subgraph App Subnet 10.0.1.0/24
        APIGW --> App1[App Service 1]
        APIGW --> App2[App Service 2]
    end

    subgraph Data Subnet 10.0.2.0/24
        App1 --> DB[(Database)]
        App2 --> DB
        App1 --> Cache[(Redis)]
        App2 --> Cache
    end

    subgraph Private Subnet 10.0.3.0/24
        App1 --> Queue[Message Broker]
        Queue --> Worker[Worker Service]
        Worker --> DB
    end

    style DMZ fill:#FFEB3B,color:black
    style Internet fill:#9E9E9E,color:white
```

---

## 4. Container Architecture

```mermaid
graph TB
    subgraph Docker Compose / K8s Pod
        subgraph api-service
            API[ASP.NET API<br/>:8080]
        end
        subgraph worker-service
            Worker[Worker<br/>BackgroundService]
        end
        subgraph frontend
            SPA[React/Angular SPA<br/>:3000]
        end
    end

    subgraph Infrastructure Containers
        DB[(PostgreSQL<br/>:5432)]
        Redis[(Redis<br/>:6379)]
        RMQ[RabbitMQ<br/>:5672 / :15672]
        Seq[Seq Logging<br/>:5341]
    end

    SPA -->|HTTP| API
    API --> DB
    API --> Redis
    API --> RMQ
    Worker --> RMQ
    Worker --> DB
    API --> Seq
    Worker --> Seq
```

---

## 5. Multi-Environment Promotion

```mermaid
graph LR
    subgraph Development
        Dev[Dev Environment]
    end

    subgraph Staging
        Stage[Staging Environment]
    end

    subgraph Production
        ProdA[Prod - Region A]
        ProdB[Prod - Region B]
    end

    Dev -->|CI Pipeline| Stage
    Stage -->|Approval Gate| ProdA
    ProdA -->|Geo-Replication| ProdB

    subgraph Shared
        ACR[Container Registry]
        KV[Key Vault per Env]
        TF[Terraform State]
    end

    Dev --> ACR
    Stage --> ACR
    ProdA --> ACR

    style Dev fill:#4CAF50,color:white
    style Stage fill:#FF9800,color:white
    style ProdA fill:#f44336,color:white
    style ProdB fill:#f44336,color:white
```

---

## 6. Disaster Recovery Topology

```mermaid
graph TB
    subgraph Primary Region
        P_LB[Load Balancer]
        P_App[App Services]
        P_DB[(Primary DB)]
        P_Storage[Storage]
    end

    subgraph Secondary Region
        S_LB[Load Balancer]
        S_App[App Services - Standby]
        S_DB[(Replica DB)]
        S_Storage[Storage - GRS]
    end

    TM[Traffic Manager / Front Door] --> P_LB
    TM -.->|Failover| S_LB

    P_LB --> P_App
    P_App --> P_DB
    S_LB --> S_App
    S_App --> S_DB

    P_DB -->|Geo-Replication| S_DB
    P_Storage -->|Geo-Redundant| S_Storage

    style P_App fill:#4CAF50,color:white
    style S_App fill:#9E9E9E,color:white
```

---

## Usage Notes

- Adapt cloud resources to your chosen provider (Azure, AWS, GCP)
- Replace placeholder service names with actual project services
- Network diagrams should reflect your security model in [03-design/security-model.md](../03-design/security-model.md)
- IaC templates should match these diagrams — see [07-delivery/infrastructure-as-code.md](../07-delivery/infrastructure-as-code.md)
