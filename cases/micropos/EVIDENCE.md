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

## Commercial web vs. edge POS — evidence reconciliation (2026-11-09)

The earlier matrix refers specifically to the **edge POS target**. The commercial `MicroPos-web` implementation must be classified separately:

| Commercial web capability | Read-only source | Evidence boundary |
|---|---|---|
| Multilingual static site | `MicroPos-web@dev/README.md` and `ROADMAP.md` | Astro ES/EN/CA documented; published commercial URL; not proof of every live page |
| Lead/CRM workflow | Same README and roadmap | PHP/SQLite mini CRM, API v1, persisted lead activities; documented implementation |
| Payments | Same README and roadmap | Manual/partial payments and Bold test/production code paths documented; test approval is **not** proof of arbitrary live production payments |
| Integration outbox and n8n | Same README and roadmap | Recorded live API/webhook-to-n8n checks in commercial system; **not** evidence for edge POS synchronization |
| Packaging | `MicroPos-web@dev/HOSTINGER-DEPLOYMENT.md` | INSTALL/UPDATE artifacts and preservation policy documented; package generation does not imply deploy |
| Raspberry Pi POS | Existing architecture case / `PILOT_PLAN.md` | Planned, no execution results inspected |

**Promotion gates:** verify a dated live commercial release and its smoke tests before broader deployment claims. Complete an independent hardware pilot (sale offline, print, restart, duplicate-safe sync, real restore, ERP reconciliation) before promoting the edge track to Pilot or Deployed.

**Source review is documentary, not a current production health check.**

