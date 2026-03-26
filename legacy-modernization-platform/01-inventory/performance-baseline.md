# Performance Baseline

> **AI Prompt**: [P1.6 — Performance Baselining](../09-ai/prompts/phase1-inventory.md)
> **Purpose**: Capture current performance characteristics before migration to enable before/after comparison.

---

## Current Environment

| Metric | Value | Measurement Method | Date Captured |
|--------|-------|--------------------|---------------|
| Peak concurrent users | — | *APM / logs* | — |
| Avg response time (p50) | — ms | *APM* | — |
| 95th percentile response time | — ms | *APM* | — |
| 99th percentile response time | — ms | *APM* | — |
| Throughput (requests/sec) | — | *Load balancer metrics* | — |
| Error rate (%) | — | *Application logs* | — |
| CPU utilization (avg/peak) | —% / —% | *Infrastructure monitoring* | — |
| Memory utilization (avg/peak) | —% / —% | *Infrastructure monitoring* | — |
| Database query time (avg) | — ms | *DB profiler / APM* | — |
| Disk I/O (avg) | — IOPS | *OS metrics* | — |

---

## Critical Transaction Baselines

| Transaction / Endpoint | Avg Latency | P95 Latency | Volume/Day | SLA Target | Status |
|-----------------------|-------------|-------------|-----------|-----------|--------|
| *Login / Auth* | — ms | — ms | — | — ms | 🟢/🟡/🔴 |
| *Primary query / search* | — ms | — ms | — | — ms | 🟢/🟡/🔴 |
| *Create / update record* | — ms | — ms | — | — ms | 🟢/🟡/🔴 |
| *Report generation* | — ms | — ms | — | — ms | 🟢/🟡/🔴 |
| *Batch processing* | — min | — min | — | — min | 🟢/🟡/🔴 |

---

## Database Performance

| Metric | Value | Notes |
|--------|-------|-------|
| Total database size | — GB | — |
| Largest tables (top 5) | — | *Table name, row count, size* |
| Slowest queries (top 10) | — | *Query, avg time, frequency* |
| Index hit ratio | —% | — |
| Connection pool size | — | — |
| Max concurrent connections | — | — |
| Deadlock frequency | — /week | — |

---

## Resource Utilization Patterns

### Peak Usage Windows

| Time Period | CPU | Memory | DB Connections | Notes |
|------------|-----|--------|---------------|-------|
| Business hours (9-5) | —% | —% | — | — |
| Batch window | —% | —% | — | — |
| Off-peak | —% | —% | — | — |
| Month-end processing | —% | —% | — | — |

### Seasonal / Cyclical Patterns

> *Document any known spikes: month-end, quarter-end, annual events, marketing campaigns, etc.*

---

## Infrastructure Footprint

| Component | Current Spec | Utilization | Notes |
|-----------|-------------|-------------|-------|
| Web/App Server(s) | — CPU, — RAM | —% | — |
| Database Server(s) | — CPU, — RAM | —% | — |
| Cache Layer | — | —% | — |
| Message Queue | — | —% | — |
| File Storage | — GB | —% | — |
| Network bandwidth | — Mbps | —% | — |

---

## Known Performance Issues

| Issue | Impact | Frequency | Workaround | Root Cause |
|-------|--------|-----------|-----------|-----------|
| *Slow report generation* | — | — | — | — |
| *Memory leak under load* | — | — | — | — |
| *Connection pool exhaustion* | — | — | — | — |

---

## Migration Performance Targets

> Define acceptable performance thresholds post-migration.

| Metric | Current Baseline | Target (Post-Migration) | Tolerance |
|--------|-----------------|------------------------|-----------|
| Response time (p95) | — ms | — ms | ±—% |
| Throughput | — req/s | — req/s | ±—% |
| Error rate | —% | —% | ≤—% |
| Cold start time | N/A | — ms | — |
| Batch processing time | — min | — min | ±—% |

---

## Data Sources & Confidence

| Section | Data Source | Confidence | Notes |
|---------|-----------|-----------|-------|
| Response times | — | HIGH/MEDIUM/LOW | — |
| Resource utilization | — | HIGH/MEDIUM/LOW | — |
| Database metrics | — | HIGH/MEDIUM/LOW | — |
| Transaction volumes | — | HIGH/MEDIUM/LOW | — |

> See [ORCHESTRATION-PROMPT.md](../09-ai/prompts/ORCHESTRATION-PROMPT.md) for confidence level definitions.
