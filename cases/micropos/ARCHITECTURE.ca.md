# MicroPOS — Arquitectura

## Propòsit

Definir l’arquitectura pública edge/offline-first de MicroPOS i del pilot amb Raspberry Pi.

## Estil arquitectònic

MicroPOS separa el camí transaccional de la disponibilitat de l’ERP extern.

```text
POS UI
  ↓
Servei d’aplicació local
  ↓
Base operacional local
  ↓
Transactional Outbox
  ↓
Sync Worker
  ↓
Cloud Sync API
  ↓
Capa d’integració
  ├── Adapter Odoo
  └── Adapter Dolibarr
```

## Responsabilitats edge

El node Raspberry Pi del pilot serà responsable de disponibilitat local, persistència transaccional, impressió, outbox, reintents de sincronització, backups locals, recuperació d’arrencada i diagnòstic.

## Responsabilitats cloud

- recepció d’esdeveniments sincronitzats;
- processament idempotent;
- monitoratge central;
- backup remot;
- agregació de reporting;
- integració ERP;
- orquestració no crítica amb n8n.

## Model de sincronització

```text
BEGIN LOCAL TRANSACTION
  ├── guardar venda
  ├── guardar pagament
  ├── registrar moviment local d’estoc
  └── afegir esdeveniment outbox
COMMIT

Sync worker
  ↓
POST amb idempotency key
  ↓
Cloud valida i processa
  ↓
ACK
  ↓
Outbox marca sincronitzat
```

## Supòsits de fallada

La xarxa pot desaparèixer durant hores, l’energia pot fallar, els requests es poden duplicar, les APIs ERP poden no estar disponibles, la impressora es pot desconnectar i pot ser necessari restaurar l’emmagatzematge local.

## Principi operatiu

> Vendre localment, persistir amb seguretat, sincronitzar de manera idempotent i reconciliar explícitament.
