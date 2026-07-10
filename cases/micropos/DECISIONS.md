# MicroPOS — Key Architecture Decisions

## ADR-001 — Offline-first transaction path

**Decision:** a sale is committed locally before cloud synchronization.

**Why:** business continuity must not depend on Internet availability.

**Trade-offs:** reconciliation and conflict handling become explicit responsibilities.

---

## ADR-002 — Raspberry Pi as optional edge node

**Decision:** validate Raspberry Pi as a local service node for the pilot.

**Why:** low-cost local hosting, printing, queue persistence and recoverability can be evaluated independently from cloud availability.

**Trade-offs:** hardware maintenance, storage wear, power quality and thermal behavior must be tested.

---

## ADR-003 — MicroPOS remains independent from ERP

**Decision:** Odoo and Dolibarr are integration targets, not the edge transaction engine.

**Why:** customers have different maturity levels and the POS must remain operational without ERP availability.

**Trade-offs:** adapter contracts and reconciliation logic are required.

---

## ADR-004 — Transactional outbox for synchronization

**Decision:** create an outbox record in the same local transaction as the sale state.

**Why:** avoids losing synchronization intent after local commit.

**Trade-offs:** queue retention, retries, dead-letter handling and monitoring are required.

---

## ADR-005 — Idempotent cloud processing

**Decision:** every synchronization event has an idempotency identity and duplicate-safe handling.

**Why:** intermittent networks naturally produce retries and duplicate delivery.

---

## ADR-006 — n8n orchestrates non-critical workflows

**Decision:** n8n may schedule, notify and coordinate integrations but does not own the local sales transaction.

**Why:** automation failure must not block point-of-sale operation.

---

## ADR-007 — Scripts are maintained product assets

**Decision:** provisioning, diagnostics, backup, restore, sync and ERP scripts are versioned and tested.

**Why:** field operations must be reproducible and supportable.

---

## ADR-008 — Pilot simplicity before platform expansion

**Decision:** validate sales, cash, minimum inventory, printing, offline continuity, restore and sync before adding broad ERP or vertical modules.

**Why:** the edge hypothesis must be proven before horizontal feature growth.
