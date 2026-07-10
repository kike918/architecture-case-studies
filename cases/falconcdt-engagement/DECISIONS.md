# FalconCDT Engagement Platform — Key Architecture Decisions

## ADR-001 — Multi-instance before multi-tenancy

### Context

The product needed to support multiple B2B deployments with different branding, participants, rewards, rules and operating timelines.

### Decision

Use independent white-label instances rather than a shared multi-tenant database architecture.

### Why

- stronger client isolation;
- lower initial complexity;
- easier client-specific changes during product validation;
- simpler failure and rollback boundaries;
- lower risk of premature shared-domain assumptions.

### Trade-offs

Costs include:

- duplicated deployments;
- repeated patch application;
- more upgrade coordination;
- potential configuration drift.

### Reversal condition

Reconsider when deployment count and maintenance cost materially exceed the complexity cost of a shared control plane and tenant isolation model.

---

## ADR-002 — MySQL as the runtime source of truth

### Context

External providers supply result data, but the application needs deterministic scoring, ranking and audit behavior.

### Decision

Normalize external data into MySQL before using it for runtime scoring and ranking.

### Why

- deterministic business behavior;
- auditability;
- reduced external API coupling;
- consistent frontend reads;
- controlled synchronization.

### Trade-offs

- synchronization jobs become operational dependencies;
- stale data is possible when sync fails;
- reconciliation logic is required.

### Reversal condition

No expected reversal for core domain state. External APIs may change, but the application-owned normalized state remains necessary.

---

## ADR-003 — One official result provider, optional enrichment providers

### Context

Different sports-data providers expose different strengths and coverage.

### Decision

Assign one provider responsibility for official score/status and allow secondary providers only for optional presentation enrichment.

### Why

Two providers must not independently decide the same business fact when that fact changes scoring and rankings.

### Trade-offs

- official provider becomes an important dependency;
- enrichment mapping can fail or remain partial;
- some UI fields may use fallback behavior.

### Reversal condition

An official-provider migration requires explicit reconciliation and cutover, not implicit provider competition.

---

## ADR-004 — Lightweight layered architecture without a heavy framework

### Context

The initial product required rapid delivery, practical hosting and maintainability with a small team.

### Decision

Use PHP 8.2+, PDO, MySQL and explicit application boundaries:

```text
Controllers
Services
Repositories
Providers
Views
```

### Why

- low infrastructure overhead;
- direct hosting compatibility;
- explicit business boundaries;
- easier incremental extraction of responsibilities.

### Trade-offs

- more internal conventions must be maintained deliberately;
- framework-provided capabilities must be implemented selectively;
- architecture discipline depends on review and documentation.

### Reversal condition

Reconsider only when product complexity, team size or operational requirements make framework migration economically justified.

---

## ADR-005 — Application owns domain state; n8n owns orchestration

### Context

The product needs scheduled notifications, result synchronization and operational summaries.

### Decision

Use n8n to trigger protected HTTP endpoints. Do not let n8n own scoring, ranking or phase transitions and do not use direct database access for core workflows.

### Why

- keeps domain invariants inside the application;
- prevents automation workflows becoming a second business-logic implementation;
- preserves testability and auditability;
- supports orchestration changes without rewriting domain rules.

### Trade-offs

- application endpoints must be designed and secured;
- external workflow health still requires monitoring;
- retries and idempotency must be considered.

### Reversal condition

None for core domain ownership. Orchestration technology may change without moving business rules outside the application.

---

## ADR-006 — Queue notification work by channel

### Context

Email, Telegram and future channels have different failure modes and credentials.

### Decision

Generate channel-specific notification work through templates and queues, with manual processing available for operational fallback.

### Why

- separates generation from delivery;
- improves operational control;
- enables channel-specific behavior;
- supports retry and deduplication patterns.

### Trade-offs

- queue monitoring is required;
- delivery may be eventual rather than immediate;
- operational tooling becomes necessary as volume grows.

### Reversal condition

Move to dedicated workers or message infrastructure when volume or latency requirements justify the added complexity.

---

## ADR-007 — Public ranking without public prediction history

### Context

Engagement requires visible rankings, but participants should not automatically expose their full prediction history.

### Decision

Expose ranking outcomes publicly while keeping detailed prediction history private to the participant and authorized administration.

### Why

- supports engagement;
- protects participant privacy;
- reduces strategic copying during active competition;
- separates aggregate outcome from detailed user behavior.

### Trade-offs

- some social comparison features are intentionally limited;
- authorization rules must remain explicit.

### Reversal condition

Only if future campaign rules explicitly require public prediction histories with informed participant expectations and appropriate authorization.
