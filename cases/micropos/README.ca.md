# MicroPOS

🌐 **Idiomes:** [English](README.md) · [Español](README.es.md) · Català

**Estat:** Baseline arquitectònic publicat; pilot edge amb Raspberry Pi planificat. Els adapters ERP i els scripts operatius estan definits com a objectius d’implementació, no com a capacitats productives validades.

## Resum executiu

MicroPOS és una arquitectura POS lleugera per a petits negocis i entorns de baixa connectivitat. La hipòtesi central és que un negoci ha de poder vendre, imprimir, tancar caixa, preservar dades locals i recuperar-se de la pèrdua de connectivitat sense dependre d’una connexió contínua al núvol.

L’arquitectura proposada utilitza una Raspberry Pi com a node edge opcional per al pilot, persistència operacional local, sincronització mitjançant outbox, scripts per a provisió i recuperació, i adapters per a Odoo i Dolibarr en lloc d’acoblar el core POS a un únic ERP.

**Nivell d’evidència:** baseline arquitectònic + pilot de hardware planificat. Offline, sincronització, impressió, recuperació i adapters ERP requereixen implementació i validació de camp.

## Problema

MicroPOS ha de suportar:

- vendes locals sense Internet;
- impressió i operació de caixa;
- recuperació després de reinici o tall elèctric;
- sincronització eventual;
- prevenció de duplicats;
- backup i restore;
- diagnòstic remot simple;
- integració ERP opcional segons la maduresa del negoci.

## Arquitectura resumida

```text
Dispositius del negoci
        │
        ▼
┌─────────────────────────┐
│ Raspberry Pi Edge Node  │
│ MicroPOS local          │
│ Base operacional local  │
│ Transactional outbox    │
│ Sync worker             │
│ Print service           │
│ Backup agent            │
│ Health diagnostics      │
└────────────┬────────────┘
             │
       Internet intermitent
             │
             ▼
┌─────────────────────────┐
│ Serveis Cloud DCP       │
│ Sync API                │
│ n8n                     │
│ Monitoring              │
│ Backups                 │
│ Integracions            │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
      Odoo      Dolibarr
```

## Decisió ERP

MicroPOS es manté independent:

```text
MicroPOS Core
      │
      ├── Adapter Odoo
      ├── Adapter Dolibarr
      ├── CSV Import / Export
      └── API / Webhooks
```

Odoo i Dolibarr són destins d’integració, no el motor transaccional del node edge.

## Pilot Raspberry Pi

### Fase A — baseline del node

- Raspberry Pi OS Lite;
- empaquetat reproduïble;
- MicroPOS;
- base local;
- impressió;
- health checks;
- backups;
- arrencada automàtica.

### Fase B — escenaris d’operació

- venda normal;
- venda offline;
- obertura i tancament de caixa;
- impressió;
- reinici inesperat;
- pèrdua i retorn d’Internet;
- backlog de sincronització;
- duplicats;
- conflicte d’estoc;
- backup i restore real.

### Fase C — sincronització

```text
Transacció local
       ↓
Commit local
       ↓
Outbox event
       ↓
Sync worker
       ↓
Cloud API
       ↓
Processament idempotent
       ↓
ACK
       ↓
Marcar sincronitzat
```

## Scripts operatius

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

## Abast MVP del pilot

- vendes;
- caixa;
- inventari mínim;
- clients bàsics;
- offline;
- backup/restore;
- sincronització;
- diagnòstic;
- auditoria mínima.

## Direcció de producte

```text
MicroPOS Start
software + configuració + catàleg inicial + formació + suport

MicroPOS Edge
Raspberry Pi + operació local + backup + impressió + monitoratge + suport remot

MicroPOS Business
MicroPOS + ERP + automatització + dashboards + CRM/integracions
```

## Documents relacionats

- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)
- [`PILOT_PLAN.ca.md`](PILOT_PLAN.ca.md)
- [`ERP_STRATEGY.ca.md`](ERP_STRATEGY.ca.md)
- [`SCRIPTS_CATALOG.ca.md`](SCRIPTS_CATALOG.ca.md)
- [`EVIDENCE.ca.md`](EVIDENCE.ca.md)

---

MicroPOS es documenta com una arquitectura edge/offline-first i programa pilot, no com una plataforma POS validada en producció.
