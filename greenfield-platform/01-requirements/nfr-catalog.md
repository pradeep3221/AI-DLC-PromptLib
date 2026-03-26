# Non-Functional Requirements (NFRs)

> Populated by: **Prompt P1.2** from [phase1-requirements.md](../08-ai/prompts/phase1-requirements.md)

---

## Performance

| Metric | Target | Measurement Method | Priority |
|--------|--------|-------------------|----------|
| Response time (P95) | | | Must / Should |
| Throughput (RPS) | | | Must / Should |
| Concurrent users | | | Must / Should |
| Startup time | | | Should / Could |

---

## Scalability

| Dimension | Requirement | Strategy |
|-----------|-------------|----------|
| Horizontal scaling | | Auto-scale / Manual |
| Data growth | | Partitioning / Archival |
| Geographic | | Single-region / Multi-region |

---

## Availability & Reliability

| Metric | Target |
|--------|--------|
| Availability SLA | e.g., 99.9% |
| RTO (Recovery Time Objective) | |
| RPO (Recovery Point Objective) | |
| MTTR (Mean Time to Recover) | |

---

## Security

| Requirement | Detail | Compliance |
|-------------|--------|------------|
| Authentication | | e.g., OAuth 2.0 / OIDC |
| Authorization | | e.g., RBAC / ABAC |
| Data encryption at rest | | |
| Data encryption in transit | | |
| Audit logging | | |
| Secrets management | | |

---

## Observability

| Requirement | Tool / Approach |
|-------------|----------------|
| Structured logging | |
| Distributed tracing | |
| Metrics & dashboards | |
| Alerting | |
| Health checks | |

---

## Compliance

| Standard | Applicable? | Requirements |
|----------|------------|--------------|
| GDPR | Yes / No | |
| HIPAA | Yes / No | |
| PCI-DSS | Yes / No | |
| SOX | Yes / No | |
| SOC 2 | Yes / No | |

---

## Operational

| Requirement | Detail |
|-------------|--------|
| Deployment frequency | e.g., Daily, Weekly |
| Rollback capability | |
| Blue-green / Canary | |
| Infrastructure as Code | |
| Disaster recovery | |

---

## Related

- Observability: [observability-design.md](../06-quality/observability-design.md) — performance and availability NFRs drive monitoring and alerting
- Resilience: [resilience-design.md](../03-design/resilience-design.md) — availability and latency NFRs shape resilience patterns
- Deployment: [deployment-strategy.md](../07-delivery/deployment-strategy.md) — scalability and availability NFRs drive scaling rules and deployment patterns

---

## Observations

- [ ] _AI-generated observations go here — review and validate with stakeholders_
