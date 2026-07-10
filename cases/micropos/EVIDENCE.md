# MicroPOS — Evidence Register

## Purpose

Separate architecture decisions from pilot evidence and future product claims.

## Evidence scale

- **Documented baseline** — architecture or product direction approved for implementation.
- **Lab planned** — hardware/software validation defined but not yet executed.
- **Prototype** — experimental implementation.
- **Pilot pending** — field use still required.
- **Pilot validated** — controlled real-business use completed.
- **Production validated** — not currently claimed.

## Capability matrix

| Capability | Evidence level | Notes |
|---|---|---|
| Edge/offline-first architecture | Documented baseline | Architecture direction defined |
| Raspberry Pi edge node | Lab planned | Hardware pilot pending |
| Local sales operation | Pilot MVP scope | Implementation/validation pending |
| Local database persistence | Documented baseline | Technology choice to be finalized in implementation |
| Transactional outbox | Documented baseline | Implementation pending |
| Idempotent synchronization | Documented baseline | Implementation pending |
| Receipt printing | Lab/pilot pending | Printer integration must be validated |
| Cash operations | Pilot MVP scope | Implementation pending |
| Minimum inventory | Pilot MVP scope | Implementation pending |
| Backup scripts | Planned implementation | Restore validation required |
| Diagnostics scripts | Planned implementation | Field usefulness pending |
| Dolibarr adapter | Planned prototype | Pilot pending |
| Odoo adapter | Planned prototype | Pilot pending |
| n8n orchestration | Architecture role defined | Workflows not production validated for MicroPOS |
| Controlled simple-business pilot | Planned | Pending |
| Complex food-service pilot | Later pilot | Depends on first pilot results |
| Production validation | Not claimed | Evidence insufficient |

## Required pilot evidence

Before stronger claims, MicroPOS must demonstrate:

- sale completion without Internet;
- durable local commit;
- restart recovery;
- duplicate-safe synchronization;
- backlog visibility;
- successful backup and restore;
- stable printing;
- useful diagnostics;
- explicit ERP reconciliation.

## Claim discipline

This case documents a planned architecture and pilot. It must not claim production-grade offline reliability, ERP integration maturity or field-proven Raspberry Pi stability until those outcomes are demonstrated.
