# MicroPOS — Operational Scripts Catalog

## Purpose

Define scripts as maintained operational assets for provisioning, support, backup, synchronization and ERP integration.

## Proposed structure

```text
scripts/
├── install/
│   ├── bootstrap.sh
│   ├── install-runtime.sh
│   ├── configure-network.sh
│   ├── install-micropos.sh
│   └── first-run.sh
├── ops/
│   ├── start.sh
│   ├── stop.sh
│   ├── restart.sh
│   ├── status.sh
│   ├── healthcheck.sh
│   └── diagnostics.sh
├── backup/
│   ├── backup-db.sh
│   ├── backup-config.sh
│   ├── restore-db.sh
│   ├── verify-backup.sh
│   └── rotate-backups.sh
├── sync/
│   ├── sync-now.sh
│   ├── retry-failed.sh
│   ├── inspect-queue.sh
│   ├── export-pending.sh
│   └── reconciliation-report.sh
└── integrations/
    ├── odoo/
    │   ├── export-customers.py
    │   ├── export-products.py
    │   ├── push-sales.py
    │   └── reconcile.py
    └── dolibarr/
        ├── export-customers.py
        ├── export-products.py
        ├── push-sales.py
        └── reconcile.py
```

## Rules

- scripts are versioned;
- destructive actions require explicit confirmation or safe flags;
- restore procedures are tested, not assumed;
- credentials are never embedded;
- output is machine-readable where useful;
- scripts return meaningful exit codes;
- diagnostics redact secrets;
- every integration script supports dry-run where practical.
