# Normia — Security and Privacy

## Scope

This document summarizes public-safe security and privacy principles in the Normia architecture baseline. It does not claim production validation.

## Identity and authorization

Normia distinguishes operational roles such as Operator, Supervisor, Admin and Auditor/Verifier.

Principles:

- permissions differ by role;
- operators cannot verify their own critical actions;
- supervisors review deviations and corrective evidence;
- auditors/verifiers can inspect integrity without modifying operations;
- sensitive actions generate audit evidence when appropriate.

## Sensitive files

Certificates, medical records and personal documents belong in private storage.

Access pattern:

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
Audit when required
```

Permanent public URLs are not appropriate for sensitive documents.

## Data minimization

- no personal or sensitive data on-chain;
- blockchain anchors aggregated cryptographic commitments only;
- operational records remain off-chain;
- external channels receive only the minimum context required for the action.

## History integrity

Critical closed records are not silently deleted or overwritten.

Correction strategy:

```text
Original record
      ↓
Superseding correction
      ↓
Current effective state
```

The original remains reconstructable.

## Channel security

Web, QR and Telegram are access channels, not separate domains.

All channels must reuse:

- authentication/identity context;
- authorization policies;
- application services;
- domain validation;
- audit generation rules.

QR identifiers must provide context, not authorization by themselves.

## Automation security

n8n is not allowed direct ownership of business state.

Protected application endpoints should handle:

- authentication of automation calls;
- idempotency;
- validation;
- business service invocation;
- auditable outcomes.

## Blockchain security boundary

Anchoring introduces specific risks:

- signer key custody;
- nonce management;
- duplicate submission;
- RPC failure;
- reverted transactions;
- finality confusion.

Architecture rules include:

- `tx_hash` is not confirmation;
- long database transactions must not wrap external RPC calls;
- anchoring dispatch is idempotent;
- duplicate batch protection exists in application and contract layers;
- operation continues when anchoring is unavailable.

## Public disclosure boundary

This case does not publish:

- private keys;
- wallet credentials;
- RPC secrets;
- medical or personal records;
- client-confidential documents;
- production endpoints that should remain private;
- private source code;
- real pilot user data.
