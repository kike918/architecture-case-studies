# MicroPOS

🌐 **Languages:** English · [Español](README.es.md) · [Català](README.ca.md)

**Status:** Architecture baseline published; Raspberry Pi edge pilot planned. ERP adapters and operational scripts are defined as implementation targets, not yet production validated.

## Executive summary

MicroPOS is a lightweight point-of-sale architecture for small businesses and low-connectivity environments. The central hypothesis is that a business should be able to sell, print, close cash, preserve local data and recover from connectivity loss without depending on a continuously available cloud connection.

The proposed architecture uses a Raspberry Pi as an optional edge node for the pilot, a local operational data store, an outbox-based synchronization path, operational scripts for provisioning and recovery, and adapters for Odoo and Dolibarr instead of coupling the POS core to one ERP.

**Evidence level:** architecture baseline + hardware pilot planned. Offline behavior, synchronization, printing, recovery and ERP adapters still require implementation and field validation.

## Problem

Many small businesses need more than a browser POS but less than a large always-online ERP deployment. The architecture must support:

- local sales during Internet loss;
- printing and cash operations;
- controlled recovery after restart or power loss;
- eventual synchronization;
- duplicate prevention;
- backups and restore;
- simple remote diagnostics;
- optional ERP integration according to business maturity.

## Architecture overview

```text
Business devices
        │
        ▼
┌─────────────────────────┐
│ Raspberry Pi Edge Node  │
│                         │
│ MicroPOS local app      │
│ Local operational DB    │
│ Transactional outbox    │
│ Sync worker             │
│ Print service           │
│ Backup agent            │
│ Health diagnostics      │
└────────────┬────────────┘
             │
      intermittent Internet
             │
             ▼
┌─────────────────────────┐
│ DCP Cloud Services      │
│ Sync API                │
│ n8n orchestration       │
│ Monitoring              │
│ Backups                 │
│ Integration services    │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
      Odoo      Dolibarr
```

## Core architectural position

MicroPOS should remain independent from Odoo and Dolibarr.

```text
MicroPOS Core
      │
      ├── Odoo Adapter
      ├── Dolibarr Adapter
      ├── CSV Import / Export
      └── API / Webhooks
```

This keeps daily sales available locally while allowing different back-office maturity levels.

## Raspberry Pi pilot

The pilot is designed to validate, not to demonstrate every possible feature.

### Phase A — Edge node baseline

- Raspberry Pi OS Lite;
- container runtime or reproducible service packaging;
- MicroPOS app;
- local database;
- print service;
- health checks;
- local backups;
- automatic startup.

### Phase B — Business operations

Test:

1. normal sale;
2. fully offline sale;
3. cash opening and closing;
4. receipt printing;
5. unexpected restart;
6. connectivity loss during operation;
7. reconnection after several hours;
8. duplicate event prevention;
9. stock conflict handling;
10. backup and real restore.

### Phase C — Synchronization

```text
Local transaction
       ↓
Local DB commit
       ↓
Outbox event
       ↓
Sync worker
       ↓
Cloud API
       ↓
Idempotent processing
       ↓
ACK
       ↓
Mark synchronized
```

## ERP strategy

### Odoo
Recommended for businesses that need broader ERP capabilities, richer accounting/operations scope or existing Odoo processes.

### Dolibarr
Recommended as a lighter back-office option where a simpler operational and administrative footprint is more appropriate.

### Architectural rule

Neither ERP is the transaction engine of the edge POS pilot. They are integration targets.

## Scripts catalog

MicroPOS includes an operational automation strategy:

```text
scripts/
├── install/
├── ops/
├── backup/
├── sync/
└── integrations/
    ├── odoo/
    └── dolibarr/
```

The scripts should become reproducible operational assets, not one-off shell history.

## Pilot MVP scope

### Sales
- product catalog;
- fast search;
- cart;
- simple discounts;
- payment methods;
- receipt printing;
- controlled cancellation.

### Cash
- opening;
- income;
- expense;
- closing;
- reconciliation;
- variance.

### Minimum inventory
- receipt;
- issue;
- adjustment;
- current stock;
- sale-generated movement.

### Customers
- optional customer;
- name;
- phone;
- optional identification;
- basic history.

### Technical operations
- offline operation;
- backup;
- restore;
- synchronization;
- diagnostics;
- minimum audit trail.

## Product packaging direction

MicroPOS is not intended to be sold as software alone.

```text
MicroPOS Start
software + configuration + initial catalog + training + support

MicroPOS Edge
Raspberry Pi + local operation + backup + printing + monitoring + remote support

MicroPOS Business
MicroPOS + ERP integration + automation + dashboards + CRM/integrations
```

## Evidence discipline

The case distinguishes architecture from validation. Raspberry Pi behavior, sync reliability, adapter quality and field suitability must be demonstrated through the pilot before stronger claims are made.

## Related documents

### English
- [`ARCHITECTURE.md`](ARCHITECTURE.md)
- [`DECISIONS.md`](DECISIONS.md)
- [`PILOT_PLAN.md`](PILOT_PLAN.md)
- [`ERP_STRATEGY.md`](ERP_STRATEGY.md)
- [`SCRIPTS_CATALOG.md`](SCRIPTS_CATALOG.md)
- [`EVIDENCE.md`](EVIDENCE.md)

### Español
- [`README.es.md`](README.es.md)
- [`ARCHITECTURE.es.md`](ARCHITECTURE.es.md)
- [`DECISIONS.es.md`](DECISIONS.es.md)

### Català
- [`README.ca.md`](README.ca.md)
- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)

---

MicroPOS is documented here as an edge/offline-first architecture and pilot program, not as a production-validated POS platform.
