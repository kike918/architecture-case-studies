# MicroPOS — Catàleg de Scripts Operatius

## Propòsit

Definir els scripts com a actius mantinguts per a provisió, suport, backup, sincronització i integració ERP.

## Estructura proposada

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

## Regles

- scripts versionats;
- accions destructives amb confirmació explícita o flags segurs;
- restore provat, no assumit;
- credencials mai incrustades;
- output llegible per màquina quan sigui útil;
- exit codes significatius;
- diagnòstic amb redacció de secrets;
- `dry-run` per a integracions quan sigui pràctic.
