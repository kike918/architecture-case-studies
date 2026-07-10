# Normia — Arquitectura

## Propòsit

Descriure l’arquitectura pública i sanititzada de l’MVP de Normia. És una línia base arquitectònica, no una afirmació de validació productiva.

## Estil arquitectònic

Normia utilitza un monòlit modular en Laravel.

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
MySQL Storage privat  Audit Service
                          │
                      Hash Chain
                          │
                     Merkle Batches
                          │
                     Anchor Adapter
                          │
                      Polygon PoS
```

Els límits modulars són primer conceptuals i només es converteixen en mòduls de codi quan hi ha comportament real que els justifica.

## Mòduls core

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

## Model de desplegament

L’MVP utilitza desplegament single-tenant per instal·lació.

```text
Codebase comú
      ↓
Instal·lació client
├── domini propi
├── ambient propi
├── base de dades pròpia
├── storage propi
├── configuració Telegram pròpia
└── configuració Polygon pròpia
```

No s’introdueix `tenant_id` global ni lògica multiempresa a l’MVP.

## Propietat del domini

MySQL és la font de veritat operacional. Laravel governa regles de negoci i transicions d’estat.

```text
Web ───────┐
QR ────────┼──→ Application Service → Domain Rules → Persistence → Audit Event
Telegram ──┤
Mini App ──┘
```

## Límit de n8n

n8n pot activar processos programats, reintentar invocacions idempotents, lliurar resums, enviar notificacions, escalar fallades i integrar sistemes externs no crítics.

n8n no ha de calcular regles de domini, decidir conformitat sanitària, escriure directament a taules de negoci, gestionar nonce blockchain, marcar finality ni convertir-se en font de veritat.

> n8n orquestra; Laravel governa.

## Fitxers sensibles

```text
Request
  ↓
Autenticació
  ↓
Política d’autorització
  ↓
Validació de sensibilitat
  ↓
Accés temporal o stream controlat
  ↓
Auditoria quan correspongui
```

## Model d’auditoria local

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

L’esdeveniment conserva semàntica de negoci; l’entrada de ledger conserva ordre i relacions hash.

## Flux d’ancoratge Polygon

```text
BATCH CLOSED → ANCHOR_PENDING → n8n trigger → Laravel dispatch
→ idempotency check → claim batch → anchor job → signer
→ Polygon adapter → RPC → SUBMITTED → receipt → MINED
→ finality check → CONFIRMED
```

Regles:

- rebre `tx_hash` no equival a confirmació;
- no executar RPC extern dins de transaccions MySQL llargues;
- dispatch idempotent;
- protecció contra batch duplicat a aplicació i contracte;
- sense dades personals on-chain;
- l’operació sanitària continua encara que falli l’anchor.

## Smart contract mínim

Responsabilitat única: registrar o emetre evidència de l’ancoratge d’un batch agregat.

```text
projectId
batchId
merkleRoot
manifestHash
recordCount
timestamp
submitter
```

No incloure regles sanitàries, documents, usuaris ni temperatures en Solidity.

## Ordre d’evolució

```text
1. Golden Flow operacional
2. Audit Ledger local
3. Merkle batches
4. Polygon testnet
5. Polygon producció
6. Reavaluar arquitectura només amb evidència real
```
