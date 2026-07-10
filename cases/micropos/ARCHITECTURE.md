# MicroPOS — Architecture

## Purpose

Define the public-safe edge/offline-first architecture baseline for MicroPOS and the Raspberry Pi pilot.

## Architecture style

MicroPOS separates the transaction path from external ERP availability.

```text
POS UI
  ↓
Local Application Service
  ↓
Local Operational Database
  ↓
Transactional Outbox
  ↓
Sync Worker
  ↓
Cloud Sync API
  ↓
Integration Layer
  ├── Odoo Adapter
  └── Dolibarr Adapter
```

## Edge responsibilities

The Raspberry Pi pilot node is responsible for:

- local application availability;
- local transaction persistence;
- receipt printing;
- local queue/outbox persistence;
- synchronization retries;
- local backups;
- startup recovery;
- diagnostics and health checks.

## Cloud responsibilities

Cloud services are responsible for:

- receiving synchronized events;
- idempotent event processing;
- central monitoring;
- remote backup targets;
- reporting aggregation;
- ERP integration;
- non-critical n8n orchestration.

## Synchronization model

A sale is complete locally before cloud acknowledgment.

```text
BEGIN LOCAL TRANSACTION
  ├── save sale
  ├── save payment
  ├── update local stock movement
  └── append outbox event
COMMIT

Sync worker
  ↓
POST event with idempotency key
  ↓
Cloud validates and processes
  ↓
ACK
  ↓
Outbox marks synchronized
```

## Failure assumptions

The architecture assumes:

- Internet may disappear for hours;
- power may fail unexpectedly;
- sync requests may be duplicated;
- ERP APIs may be unavailable;
- printers may disconnect;
- local storage may need restore;
- field technicians need simple diagnostics.

## Data ownership

For the pilot, MicroPOS owns the local transaction record required for sales continuity. ERP synchronization is downstream and must not block local sale completion.

## Operational principle

> Sell locally, persist safely, synchronize idempotently, reconcile explicitly.
