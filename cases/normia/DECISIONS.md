# Normia — Key Architecture Decisions

## ADR-001 — Modular monolith for the MVP

**Decision:** use a modular Laravel monolith before considering microservices.

**Why:** the product is still validating domain boundaries through a real pilot. Distributed architecture would add deployment, observability and consistency costs before the domain is stable.

**Trade-offs:** module discipline must be enforced inside one codebase.

**Reversal condition:** only when independent scaling, ownership or deployment needs are proven.

---

## ADR-002 — Single-tenant installation per client

**Decision:** isolated installation per client for the MVP.

**Why:** simpler privacy boundaries, lower complexity and clearer operational ownership.

**Trade-offs:** duplicated deployment and upgrade work.

**Reversal condition:** repeated client patterns and operational scale justify shared tenancy.

---

## ADR-003 — MySQL is the operational source of truth

**Decision:** operational state, tasks, controls, deviations, corrective actions and audit semantics live in the application database.

**Why:** daily operations must continue independently of Telegram, n8n or blockchain availability.

**Trade-offs:** synchronization and anchoring layers must reconcile with the application state.

---

## ADR-004 — Laravel owns domain rules; channels share services

**Decision:** web, QR, Telegram Bot and Mini App call shared application services rather than implementing separate business logic.

**Why:** one set of rules for permissions, conformity, state transitions and audit events.

**Trade-offs:** channel adapters must be thin and may need tailored UX without duplicating domain behavior.

---

## ADR-005 — n8n orchestrates but does not govern domain state

**Decision:** n8n triggers schedules, retries invocations and delivers notifications, while Laravel remains responsible for business decisions.

**Why:** domain invariants must remain testable and centralized.

**Trade-offs:** protected idempotent endpoints and workflow monitoring are required.

---

## ADR-006 — Audit locally before anchoring externally

**Decision:** create semantic audit events and a local append-oriented ledger before Merkle batching and Polygon anchoring.

**Why:** blockchain should strengthen integrity evidence, not replace domain context or operational storage.

**Trade-offs:** more layers and explicit reconciliation between event, ledger, batch and anchor states.

---

## ADR-007 — Polygon stays outside the critical path

**Decision:** sanitary and operational workflows continue even if anchoring is delayed or unavailable.

**Why:** physical operation cannot depend on RPC availability, gas, nonce handling or blockchain finality.

**Trade-offs:** verification may temporarily show pending anchor status.

---

## ADR-008 — No personal or sensitive data on-chain

**Decision:** anchor only aggregated cryptographic commitments and minimal metadata.

**Why:** privacy, minimization and reversibility constraints.

**Trade-offs:** verification requires access to the off-chain manifest and authorized operational records.

---

## ADR-009 — Critical history is corrected by supersession

**Decision:** closed critical records are not silently overwritten or deleted. Corrections preserve the original and create a superseding record or event.

**Why:** auditability and historical reconstruction.

**Trade-offs:** queries and UI must represent current and superseded state clearly.

---

## ADR-010 — Validate the Golden Flow before horizontal expansion

**Decision:** prioritize one complete vertical slice from task execution through deviation, containment, corrective action, verification and audit.

**Why:** isolated CRUD modules do not prove the product model.

**Trade-offs:** some broad feature areas remain intentionally delayed.
