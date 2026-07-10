# MicroPOS — Catálogo de Scripts Operativos

## Propósito

Definir los scripts como activos mantenidos para provisión, soporte, backup, sincronización e integración ERP.

## Estructura propuesta

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
    └── dolibarr/
```

## Reglas

- scripts versionados;
- acciones destructivas con confirmación explícita o flags seguros;
- restore probado, no asumido;
- credenciales nunca embebidas;
- output legible por máquina cuando sea útil;
- exit codes significativos;
- diagnóstico con redacción de secretos;
- `dry-run` para integraciones cuando sea práctico.
