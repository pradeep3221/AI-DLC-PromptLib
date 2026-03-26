# Observability Design

> Populated by: **Prompt P3.4** from [phase3-implementation.md](../08-ai/prompts/phase3-implementation.md)

---

## Three Pillars

| Pillar | Tool | Standard |
|--------|------|----------|
| Logging | Serilog / NLog / Microsoft.Extensions.Logging | Structured JSON |
| Metrics | Prometheus / Application Insights / OpenTelemetry | OpenTelemetry SDK |
| Tracing | Jaeger / Zipkin / Application Insights | W3C Trace Context |

---

## Logging Standards

| Field | Required | Example |
|-------|----------|---------|
| Timestamp | Yes | ISO 8601 UTC |
| Level | Yes | Information / Warning / Error |
| Message | Yes | Structured template |
| CorrelationId | Yes | Request-scoped GUID |
| UserId | If authenticated | |
| ServiceName | Yes | Orders.API |
| Exception | If error | Full stack trace |

**Log Levels:**
| Level | When to Use |
|-------|------------|
| Debug | Development-only detailed info |
| Information | Business events, request/response logs |
| Warning | Unexpected but recoverable situations |
| Error | Failures requiring attention |
| Critical | System-level failures |

---

## Metrics

| Metric | Type | Labels |
|--------|------|--------|
| http_requests_total | Counter | method, endpoint, status |
| http_request_duration_seconds | Histogram | method, endpoint |
| active_connections | Gauge | service |
| business_events_total | Counter | event_type |
| error_count | Counter | service, error_type |

---

## Health Checks

| Endpoint | Check | Interval |
|----------|-------|----------|
| /health/live | Self (liveness) | 10s |
| /health/ready | Dependencies (readiness) | 30s |
| /health/startup | Initialization (startup) | 5s |

---

## Alerting Rules

| Alert | Condition | Severity | Action |
|-------|-----------|----------|--------|
| High error rate | Error rate > 5% for 5 min | Critical | Page on-call |
| High latency | P95 > 2s for 10 min | Warning | Notify team |
| Health check failure | Any critical check fails | Critical | Page on-call |
| Disk usage | > 80% | Warning | Notify team |

---

## Dashboards

| Dashboard | Audience | Key Panels |
|-----------|----------|------------|
| Service Health | Engineering | Request rate, error rate, latency, saturation |
| Business Metrics | Product | Key business events, user activity |
| Infrastructure | SRE | CPU, memory, disk, network |

---

## Observability for Async & Event-Driven Workflows

> Synchronous HTTP tracing is straightforward. Async workflows (background jobs, message consumers, event handlers) require explicit correlation propagation.

### CorrelationId Propagation

| Context | How to Propagate |
|---------|------------------|
| HTTP → HTTP | Forward `X-Correlation-Id` header |
| HTTP → Message Queue | Set `CorrelationId` as message property/header |
| Message Consumer → DB | Attach `CorrelationId` to logging scope via `ILogger.BeginScope` |
| Message Consumer → HTTP | Forward `CorrelationId` as request header |
| Background Job (scheduled) | Generate new `CorrelationId` at job start, log with `JobName` |
| Event Handler → Event Handler | Carry `CorrelationId` from source event metadata |

### Message Consumer Logging

| Field | Required | Example |
|-------|----------|--------|
| CorrelationId | Yes | From message metadata |
| MessageId | Yes | Unique message identifier |
| MessageType | Yes | `OrderCreatedEvent` |
| QueueName | Yes | `orders-queue` |
| DeliveryCount | Yes | Retry attempt number |
| ConsumerGroup | If applicable | `order-processor` |
| ProcessingDuration | Yes | Time to handle message |

### Background Job Logging

| Field | Required | Example |
|-------|----------|--------|
| JobId | Yes | Unique execution ID |
| JobName | Yes | `SyncInventoryJob` |
| ScheduleExpression | Yes | `0 */5 * * *` |
| ExecutionDuration | Yes | Total run time |
| ItemsProcessed | If batch | Count of records |
| Outcome | Yes | Success / Partial / Failed |

### Async-Specific Metrics

| Metric | Type | Labels |
|--------|------|--------|
| messages_received_total | Counter | queue, message_type |
| messages_processed_total | Counter | queue, message_type, outcome |
| message_processing_duration_seconds | Histogram | queue, message_type |
| dead_letter_messages_total | Counter | queue, message_type |
| background_job_duration_seconds | Histogram | job_name, outcome |
| background_job_items_processed_total | Counter | job_name |

### Async-Specific Alerts

| Alert | Condition | Severity | Action |
|-------|-----------|----------|--------|
| Dead letter queue growing | DLQ count > 10 for 5 min | Warning | Investigate poison messages |
| Consumer lag | Lag > 1000 messages for 10 min | Warning | Scale consumers |
| Job failure | Job fails 3 consecutive runs | Critical | Page on-call |
| Processing timeout | Message processing > 5 min | Warning | Check for deadlocks |

---

## Related

- Resilience patterns: [resilience-design.md](../03-design/resilience-design.md) — retry/circuit breaker affects observability
- Quality gates: [quality-gates.md](quality-gates.md) — observability checks in CI/CD

---

## Observations

- [ ] _Adjust observability depth based on project scale and operational requirements_
