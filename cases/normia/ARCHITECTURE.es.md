# Normia — Arquitectura

## Propósito

Describir la arquitectura pública y sanitizada del MVP de Normia. Es una línea base arquitectónica, no una afirmación de validación productiva.

## Estilo arquitectónico

Normia usa un monolito modular en Laravel.

```text
Web / QR / Telegram
        │
        ▼
      Laravel
        │
 Application Services
        │
    Domain Rules
        │
 ┌──────┼───────────────┐
 ▼      ▼               ▼
MySQL Storage privado Audit Service
                          │
                      Hash Chain
                          │
                     Merkle Batches
                          │
                     Anchor Adapter
                          │
                      Polygon PoS
```

Los límites modulares son primero conceptuales y solo se convierten en módulos de código cuando existe comportamiento real que los justifica.

## Módulos core

Dominios candidatos del MVP:

- Identity;
- People;
- Compliance;
- Documents;
- Equipment;
- Tasks;
- Temperature;
- Sanitation;
- Reception;
- Shelf Life;
- Corrective Actions;
- Audit.

## Modelo de despliegue

El MVP usa despliegue single-tenant por instalación.

```text
Codebase común
      ↓
Instalación cliente
├── dominio propio
├── ambiente propio
├── base de datos propia
├── storage propio
├── configuración Telegram propia
└── configuración Polygon propia
```

No se introduce `tenant_id` global ni lógica multiempresa en el MVP.

## Propiedad del dominio

MySQL es la fuente de verdad operacional. Laravel gobierna reglas de negocio y transiciones de estado.

```text
Web ───────┐
QR ────────┼──→ Application Service → Domain Rules → Persistence → Audit Event
Telegram ──┤
Mini App ──┘
```

## Límite de n8n

n8n puede disparar procesos programados, reintentar invocaciones idempotentes, entregar resúmenes, enviar notificaciones, escalar fallos e integrar sistemas externos no críticos.

n8n no debe calcular reglas de dominio, decidir conformidad sanitaria, escribir directamente en tablas de negocio, gestionar nonce blockchain, marcar finality ni convertirse en fuente de verdad.

> n8n orquesta; Laravel gobierna.

## Archivos sensibles

```text
Request
  ↓
Autenticación
  ↓
Política de autorización
  ↓
Validación de sensibilidad
  ↓
Acceso temporal o stream controlado
  ↓
Auditoría cuando aplique
```

## Modelo de auditoría local

```text
audit_events
      ↓
audit_ledger_entries
      ↓
audit_batches
      ↓
audit_batch_members
      ↓
anchor_attempts
```

El evento conserva semántica de negocio; la entrada de ledger conserva orden y relaciones hash.

## Flujo de anclaje Polygon

```text
BATCH CLOSED → ANCHOR_PENDING → n8n trigger → Laravel dispatch
→ idempotency check → claim batch → anchor job → signer
→ Polygon adapter → RPC → SUBMITTED → receipt → MINED
→ finality check → CONFIRMED
```

Reglas:

- recibir `tx_hash` no equivale a confirmación;
- no ejecutar RPC externo dentro de transacciones MySQL largas;
- dispatch idempotente;
- protección contra batch duplicado en aplicación y contrato;
- sin datos personales on-chain;
- la operación sanitaria continúa aunque falle el anchor.

## Smart contract mínimo

Responsabilidad única: registrar o emitir evidencia del anclaje de un batch agregado.

```text
projectId
batchId
merkleRoot
manifestHash
recordCount
timestamp
submitter
```

No incluir reglas sanitarias, documentos, usuarios ni temperaturas en Solidity.

## Orden de evolución

```text
1. Golden Flow operacional
2. Audit Ledger local
3. Merkle batches
4. Polygon testnet
5. Polygon producción
6. Revaluar arquitectura solo con evidencia real
```
