# User Journey Maps

> Visual templates mapping user interactions to system components and technical flows.

---

## 1. Primary User Journey — Happy Path

```mermaid
journey
    title User Registration & First Action
    section Sign Up
        Visit landing page: 5: User
        Click Register: 4: User
        Fill registration form: 3: User
        Receive verification email: 4: User, System
        Verify email: 5: User
    section First Login
        Login with credentials: 4: User
        Complete onboarding wizard: 3: User, System
        View dashboard: 5: User, System
    section First Action
        Create first resource: 4: User
        Receive confirmation: 5: User, System
```

---

## 2. User Flow → System Interaction Map

```mermaid
graph TD
    subgraph User Actions
        U1[Browse Products]
        U2[Add to Cart]
        U3[Checkout]
        U4[Complete Payment]
        U5[View Order Status]
    end

    subgraph API Endpoints
        E1[GET /products]
        E2[POST /cart/items]
        E3[POST /orders]
        E4[POST /payments]
        E5[GET /orders/:id]
    end

    subgraph Services
        S1[Product Service]
        S2[Cart Service]
        S3[Order Service]
        S4[Payment Service]
    end

    subgraph Data
        D1[(Product DB)]
        D2[(Cart Cache)]
        D3[(Order DB)]
        D4[Payment Gateway]
    end

    U1 --> E1 --> S1 --> D1
    U2 --> E2 --> S2 --> D2
    U3 --> E3 --> S3 --> D3
    U4 --> E4 --> S4 --> D4
    U5 --> E5 --> S3
```

---

## 3. Role-Based Access Flow

```mermaid
graph TD
    subgraph Roles
        Admin[Admin User]
        Manager[Manager]
        Standard[Standard User]
        Guest[Guest / Anonymous]
    end

    subgraph Features
        Dash[Dashboard]
        CRUD[CRUD Operations]
        Reports[Reports & Analytics]
        Settings[System Settings]
        UserMgmt[User Management]
        AuditLog[Audit Log]
    end

    Admin --> Dash & CRUD & Reports & Settings & UserMgmt & AuditLog
    Manager --> Dash & CRUD & Reports
    Standard --> Dash & CRUD
    Guest --> Dash

    style Admin fill:#f44336,color:white
    style Manager fill:#FF9800,color:white
    style Standard fill:#4CAF50,color:white
    style Guest fill:#9E9E9E,color:white
```

---

## 4. Error & Recovery Journey

```mermaid
journey
    title Error Handling — Payment Failure
    section Attempt
        User submits payment: 4: User
        System processes payment: 3: System
        Payment gateway rejects: 1: System, Gateway
    section Recovery
        Show error message: 3: System
        User updates payment method: 3: User
        Retry payment: 4: User
        Payment succeeds: 5: System, Gateway
    section Confirmation
        Show success page: 5: System
        Send receipt email: 5: System
```

---

## 5. Multi-Persona Interaction

```mermaid
sequenceDiagram
    actor Customer
    actor Support
    actor Admin
    participant App as Application
    participant DB as Database
    participant Notif as Notification Service

    Customer->>App: Submit Support Ticket
    App->>DB: Create Ticket
    App->>Notif: Notify Support Team
    Notif->>Support: Email / Dashboard Alert

    Support->>App: View Ticket
    App->>DB: Fetch Ticket Details
    Support->>App: Add Response
    App->>DB: Update Ticket
    App->>Notif: Notify Customer
    Notif->>Customer: Email Update

    Admin->>App: View SLA Dashboard
    App->>DB: Aggregate Metrics
```

---

## 6. Onboarding Funnel

```mermaid
graph TD
    Visit[Landing Page Visit] -->|80%| Signup[Sign Up Started]
    Signup -->|60%| Verify[Email Verified]
    Verify -->|75%| Onboard[Onboarding Complete]
    Onboard -->|50%| FirstAction[First Meaningful Action]
    FirstAction -->|70%| Retained[Active User - Day 7]

    Visit -.->|20% drop| X1[Bounced]
    Signup -.->|40% drop| X2[Abandoned]
    Verify -.->|25% drop| X3[Not Verified]
    Onboard -.->|50% drop| X4[Stalled]
    FirstAction -.->|30% drop| X5[Churned]

    style X1 fill:#f44336,color:white
    style X2 fill:#f44336,color:white
    style X3 fill:#f44336,color:white
    style X4 fill:#f44336,color:white
    style X5 fill:#f44336,color:white
    style Retained fill:#4CAF50,color:white
```

---

## Usage Notes

- Replace placeholder entities with your actual domain personas and features
- Journey maps are best reviewed with product / UX stakeholders
- Use the User Flow → System Interaction Map to validate API coverage
- Role-Based Access Flow should align with your security model in [03-design/security-model.md](../03-design/security-model.md)
