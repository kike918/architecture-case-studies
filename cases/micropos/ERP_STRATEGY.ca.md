# MicroPOS — Estratègia d’Integració ERP

## Principi

MicroPOS és un core operacional POS amb adapters cap a sistemes de back-office.

```text
MicroPOS Core
      │
      ├── Adapter Odoo
      ├── Adapter Dolibarr
      ├── CSV Import / Export
      └── API / Webhooks
```

## Rol d’Odoo

Utilitzar Odoo quan el client necessita més profunditat ERP: inventari integrat, comptabilitat, CRM, compres, manufactura o processos Odoo existents.

Contractes candidats:

- productes;
- clients;
- vendes;
- pagaments;
- moviments d’inventari quan correspongui.

## Rol de Dolibarr

Utilitzar Dolibarr quan sigui més adequat un back-office lleuger amb fluxos simples de clients, productes, vendes i administració.

## Regles d’integració

- la venda local mai depèn de la resposta de l’ERP;
- sincronització asíncrona;
- adapters idempotents;
- mappings explícits i versionats;
- informes de reconciliació;
- ownership per entitat clarament definit;
- una caiguda de l’ERP no atura el POS local.

## Evolució recomanada

```text
1. Contract tests CSV
2. Prototip de contracte API
3. Pilot adapter Dolibarr
4. Pilot adapter Odoo
5. Eines de reconciliació
6. Perfils de mapping per client
```
