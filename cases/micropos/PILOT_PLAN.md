# MicroPOS — Raspberry Pi Pilot Plan

## Objective

Validate whether a Raspberry Pi can operate as a stable edge node for MicroPOS in a low-connectivity business environment.

## Phase A — Baseline node

Install and validate:

- Raspberry Pi OS Lite;
- reproducible application packaging;
- MicroPOS application;
- local database;
- automatic startup;
- print service;
- health check;
- local backup;
- diagnostics.

Measure:

- boot recovery;
- RAM and CPU usage;
- storage use;
- temperature;
- service restart behavior;
- local response time;
- unattended recovery.

## Phase B — Business operation scenarios

Execute and record evidence for:

1. normal sale;
2. sale with no Internet;
3. cash opening;
4. cash closing;
5. receipt printing;
6. network loss during operation;
7. several hours offline;
8. reconnection and backlog sync;
9. duplicate delivery attempts;
10. stock conflict scenario;
11. unexpected reboot;
12. backup creation;
13. full restore to a clean environment.

## Phase C — Synchronization

Validate:

- local commit before sync;
- persistent outbox;
- retry policy;
- idempotency;
- acknowledgment;
- dead-letter handling;
- reconciliation report;
- observability of pending and failed events.

## Pilot sequence

```text
Raspberry Lab
     ↓
Controlled simple-business pilot
     ↓
Operational evidence review
     ↓
More complex food-service pilot
     ↓
Product packaging decision
```

## Exit criteria

The pilot is successful only if:

- sales continue offline;
- restart does not lose committed sales;
- duplicate sync does not duplicate business transactions;
- backup can be restored successfully;
- print workflow is stable enough for field use;
- diagnostics identify common failure states;
- synchronization backlog is visible and reconcilable.

## Non-goals

The pilot does not need to validate:

- full Odoo deployment on Raspberry Pi;
- full Dolibarr deployment on Raspberry Pi;
- advanced accounting;
- complex multi-store synchronization;
- production-scale cloud orchestration.
