# Resilience Design

> Populated by: **Prompt P2.6** from [phase2-architecture.md](../08-ai/prompts/phase2-architecture.md)

---

## Resilience Strategy Summary

| Component | Pattern | Configuration | Fallback |
|-----------|---------|---------------|----------|
| | | | |

---

## Retry Policy

| Scope | Max Retries | Backoff | Jitter | Retryable Errors |
|-------|-------------|---------|--------|-------------------|
| HTTP calls | 3 | Exponential (2s base) | Yes | 408, 429, 500, 502, 503 |
| Database | 3 | Linear (1s) | No | Transient / Deadlock |
| Messaging | 5 | Exponential (5s base) | Yes | Timeout |

---

## Circuit Breaker

| Scope | Failure Threshold | Break Duration | Half-Open Allowed |
|-------|-------------------|----------------|-------------------|
| | 5 failures / 30s | 60s | 1 request |

---

## Timeout Policy

| Scope | Timeout | Action on Timeout |
|-------|---------|-------------------|
| HTTP calls | 30s | Cancel + fallback |
| Database queries | 15s | Cancel + log |
| Background jobs | Configurable | Log + retry |

---

## Health Checks

| Check | Endpoint | Interval | Critical? |
|-------|----------|----------|-----------|
| Self | /health | 30s | Yes |
| Database | /health/db | 60s | Yes |
| External API | /health/ext | 120s | No |
| Messaging | /health/mq | 60s | Yes |

---

## Error Handling Strategy

| Layer | Strategy |
|-------|----------|
| API Controller | Return Problem Details (RFC 7807), log error |
| Application Service | Catch domain exceptions, translate to result types |
| Domain | Throw domain-specific exceptions |
| Infrastructure | Wrap external exceptions, apply retry/circuit breaker |

---

## Bulkhead Isolation

> Bulkhead pattern prevents a failure in one component from cascading to others by isolating resources (thread pools, connections, semaphores).

| Scope | Isolation Type | Configuration | Purpose |
|-------|---------------|---------------|--------|
| External API calls | Semaphore | Max 10 concurrent | Prevent slow API from exhausting thread pool |
| Database connections | Connection pool | Max 20 per service | Prevent query storms from starving other services |
| Message processing | Separate consumer groups | 5 concurrent per queue | Prevent one queue backup from blocking others |
| Background jobs | Dedicated thread pool | 2–5 threads per job type | Prevent long-running job from blocking others |
| HTTP client instances | Named HttpClient | Separate `HttpClient` per dependency | Prevent DNS/connection issues from spreading |

### Implementation Guidance

```
// Polly Bulkhead example
services.AddHttpClient("PaymentGateway")
    .AddPolicyHandler(Policy.BulkheadAsync<HttpResponseMessage>(
        maxParallelization: 10,
        maxQueuingActions: 5,
        onBulkheadRejectedAsync: (ctx) => { /* log + metric */ }
    ));
```

---

## Related

- Integration design: [integration-design.md](integration-design.md) — resilience patterns applied at integration boundaries
- Observability: [observability-design.md](../06-quality/observability-design.md) — circuit breaker state and bulkhead rejections should be monitored
- NFRs: [nfr-catalog.md](../01-requirements/nfr-catalog.md) — availability and latency NFRs drive resilience configuration

---

## Observations

- [ ] _AI-generated observations go here — review and validate_
