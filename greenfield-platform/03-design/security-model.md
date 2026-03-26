# Security Model

> Populated by: **Prompt P2.5** from [phase2-architecture.md](../08-ai/prompts/phase2-architecture.md)

---

## Authentication

| Aspect | Decision |
|--------|----------|
| Protocol | OAuth 2.0 + OIDC / API Key / mTLS |
| Identity Provider | Entra ID / Auth0 / Duende IdentityServer |
| Token format | JWT / Opaque |
| Token lifetime | Access: __ min / Refresh: __ hours |
| Service-to-service auth | Client Credentials / Managed Identity |

---

## Authorization

| Strategy | Scope |
|----------|-------|
| Model | RBAC / ABAC / Policy-based |
| Enforcement layer | API Gateway / Application / Both |
| Role hierarchy | Admin > Manager > User > Guest |

### Role Definitions

| Role | Permissions | Scope |
|------|------------|-------|
| | | |

### Policy Definitions

| Policy | Rule | Applies To |
|--------|------|------------|
| | | |

---

## Data Protection

| Data Category | Classification | Protection |
|---------------|---------------|------------|
| PII | Sensitive | Encrypted at rest + in transit |
| Credentials | Secret | Key Vault / Secrets Manager |
| Business data | Internal | Encrypted in transit |
| Public data | Public | No encryption required |

---

## Secrets Management

| Secret Type | Storage | Rotation |
|-------------|---------|----------|
| Database connection strings | Key Vault | Automatic |
| API keys | Key Vault | Manual |
| Certificates | Key Vault | Auto-renewal |
| Service credentials | Managed Identity | N/A |

---

## Security Headers

| Header | Value | Purpose |
|--------|-------|---------|
| Strict-Transport-Security | max-age=31536000; includeSubDomains | Force HTTPS |
| Content-Security-Policy | default-src 'self' | Prevent XSS |
| X-Content-Type-Options | nosniff | Prevent MIME sniffing |
| X-Frame-Options | DENY | Prevent clickjacking |

---

## Audit & Compliance

| Requirement | Implementation |
|-------------|---------------|
| Audit logging | |
| Data retention | |
| Right to deletion (GDPR) | |
| Access reviews | |

---

## Threat Model

| Threat | Risk | Mitigation |
|--------|------|------------|
| SQL Injection | | Parameterized queries / ORM |
| XSS | | CSP headers, output encoding |
| CSRF | | Anti-forgery tokens |
| Broken Auth | | Token validation, rate limiting |
| Data Exposure | | Encryption, minimal response payloads |

---

## Related

- Coding standards: [coding-standards.md](../05-implementation/coding-standards.md) — security practices (input validation, parameterized queries, output encoding) should be enforced in code standards
- NFRs: [nfr-catalog.md](../01-requirements/nfr-catalog.md) — security NFRs and compliance requirements
- Infrastructure: [infrastructure-as-code.md](../07-delivery/infrastructure-as-code.md) — Key Vault, managed identities, and network security configured via IaC

---

## Observations

- [ ] _AI-generated observations go here — review with security team_
