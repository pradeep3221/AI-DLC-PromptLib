# AI Prompt Library — Greenfield Platform

> Navigation hub for the greenfield project design prompt library.

---

## Folder Contents

```
08-ai/prompts/
├── ORCHESTRATION-PROMPT.md      ← Master guardrails & workflow (read first)
├── phase0-classification.md     ← P0.1–P0.5: Project classification & profiling
├── phase1-requirements.md       ← P1.1–P1.6: Requirements & domain discovery
├── phase2-architecture.md       ← P2.1–P2.6: Architecture & design decisions
├── phase3-implementation.md     ← P3.1–P3.6: Implementation & delivery planning
├── PROMPT-INDEX.md              ← Full prompt catalog & execution paths
└── README.md                    ← This file
```

---

## Quick Start

1. **Read** [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md) — understand the guardrails and workflow.
2. **Run** P0.1 from [phase0-classification.md](phase0-classification.md) — classify your project.
3. **Follow** the execution path for your project type in [PROMPT-INDEX.md](PROMPT-INDEX.md).

---

## Prompt → Output Mapping

| Phase | Prompts | Key Outputs |
|-------|---------|-------------|
| Phase 0 | P0.1–P0.5 | `project-profile.yaml`, complexity score, technology direction |
| Phase 1 | P1.1–P1.6 | Requirements catalog, NFRs, domain model, bounded contexts, use cases |
| Phase 2 | P2.1–P2.6 | ADRs, technology selection, API contracts, data model, security, integrations |
| Phase 3 | P3.1–P3.6 | Project structure, coding standards, testing, quality gates, CI/CD, deployment |

---

## Execution Order by Project Type

| Type | Depth | Path |
|------|-------|------|
| **Simple-API** | Light | P0 → P1.1–P1.3 → P2.1–P2.5 → P3.1, P3.3, P3.5–P3.6 |
| **SPA-API** | Standard | P0 → P1.1–P1.3, P1.5 → P2 (full) → P3 (full) |
| **Modular-Monolith** | Deep | P0 → P1 (full) → P2 (full) → P3 (full) |
| **Microservices** | Deep | P0 → P1 (full) → P2 (full) → P3 (full) |
| **Event-Driven** | Deep | P0 → P1 (full, deep P1.6) → P2 (full) → P3 (full) |

---

## Total Prompt Count: 23

| Phase | Count | Focus |
|-------|-------|-------|
| Phase 0: Classification | 5 | Project type, architecture, complexity, technology |
| Phase 1: Requirements | 6 | Requirements, NFRs, domain, contexts, use cases, events |
| Phase 2: Architecture | 6 | ADRs, tech, API, data, security, resilience |
| Phase 3: Implementation | 6 | Structure, standards, testing, quality, deployment, CI/CD |
