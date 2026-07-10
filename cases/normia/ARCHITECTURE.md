# Normia — Architecture

## Purpose

Describe the public-safe MVP architecture of Normia. This is an architecture baseline, not a claim of production validation.

## Architectural style

Normia uses a modular Laravel monolith.

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
MySQL Private Storage Audit Service
                          │
                      Hash Chain
                          │
                     Merkle Batches
                          │
                     Anchor Adapter
                          │
                      Polygon PoS
```

The modular boundaries are conceptual first and become code modules only when real behavior justifies them.

## Core modules

Potential MVP domains include:

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

## Deployment model

The MVP uses single-tenant deployment per installation.

```text
Shared codebase
      ↓
Client installation
├── own domain
├── own environment
├── own database
├── own storage
├── own Telegram configuration
└── own Polygon configuration
```

No global `tenant_id` or multi-company logic is introduced in the MVP.

## Domain ownership

MySQL is the operational source of truth. Laravel owns business rules and state transitions.

Channels such as web, QR and Telegram do not own parallel business logic.

```text
Web ───────┐
QR ────────┼──→ Application Service → Domain Rules → Persistence → Audit Event
Telegram ──┤
Mini App ──┘
```

## n8n boundary

n8n may:

- trigger scheduled processes;
- retry idempotent invocations;
- deliver summaries;
- send notifications;
- escalate failures;
- integrate non-critical external systems.

n8n must not:

- calculate domain rules;
- decide sanitary conformity;
- write directly to business tables;
- manage blockchain nonce;
- mark blockchain finality;
- become a source of truth.

Principle:

> n8n orchestrates; Laravel governs.

## Sensitive file access

```text
Request
  ↓
Authentication
  ↓
Authorization policy
  ↓
Sensitivity check
  ↓
Temporary access or controlled stream
  ↓
Audit access when required
```

Sensitive personal files must not use permanent public URLs.

## Local audit model

Normia separates semantic audit events from cryptographic chaining.

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

The domain event keeps business context. The ledger entry keeps order and hash relationships.

## Polygon anchoring flow

```text
BATCH CLOSED
     ↓
ANCHOR_PENDING
     ↓
n8n trigger
     ↓
Laravel dispatch endpoint
     ↓
Idempotency check
     ↓
Claim batch
     ↓
Anchor job
     ↓
Transaction signer
     ↓
Polygon adapter
     ↓
RPC
     ↓
SUBMITTED
     ↓
Receipt check
     ↓
MINED
     ↓
Finality check
     ↓
CONFIRMED
```

Rules:

- receiving a `tx_hash` does not mean confirmed;
- external RPC calls do not run inside long MySQL transactions;
- dispatch is idempotent;
- duplicate batch protection exists in application and contract layers;
- no personal data goes on-chain;
- sanitary operation continues when anchoring fails.

## Minimal smart contract responsibility

The contract only records or emits evidence of an aggregated batch anchor.

Conceptual fields:

```text
projectId
batchId
merkleRoot
manifestHash
recordCount
timestamp
submitter
```

No sanitary logic, users, temperatures, documents or operational rules belong in Solidity.

## Evolution order

```text
1. Operational Golden Flow
2. Local Audit Ledger
3. Merkle batches
4. Polygon testnet
5. Polygon production
6. Re-evaluate architecture only with evidence from new real cases
```
