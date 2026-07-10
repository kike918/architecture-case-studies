# Normia

🌐 **Languages:** English · [Español](README.es.md) · [Català](README.ca.md)

**Status:** Architecture baseline and implementation-in-progress case study. Sprint 0, technical bootstrap and pilot discovery are underway.

## 1. Executive summary

Normia is a digital system for sanitary control, documentary compliance, operational execution and verifiable auditability in food-service operations.

The product is being designed from a real pilot context rather than as a generic SaaS abstraction. Its core problem is to connect planned controls with execution evidence, deviation handling, containment, corrective actions, supervisor verification and historical integrity.

The current architecture is a modular Laravel monolith with MySQL as the operational source of truth, web/mobile-first workflows, QR context, Telegram as a channel, n8n as an orchestrator and optional aggregated anchoring of audit evidence on Polygon PoS.

**Evidence level:** Architecture baseline + prototype/reference UX + implementation in progress. Not production validated.

## 2. Context

Small food-service operations often manage controls through paper, chats, spreadsheets and fragmented documents. The challenge is not only to store checklists, but to preserve the complete operational chain:

```text
PLAN → SCHEDULE → ASSIGN → EXECUTE → RECORD → EVALUATE
→ DETECT → CONTAIN → CORRECT → VERIFY → CONSULT → EXPORT → AUDIT
```

The initial pilot context is a real food-preparation establishment in Bogotá. The product deliberately prioritizes real operating patterns before generic multi-tenant abstraction.

## 3. Problem

For every relevant control, the system should eventually be able to answer:

- what had to be done;
- who had to do it;
- when it was due;
- what result was recorded;
- whether a deviation occurred;
- what containment was applied;
- what corrective action followed;
- who verified closure;
- whether the historical evidence still preserves integrity.

A CRUD-only checklist application does not satisfy this problem definition.

## 4. Constraints

- small implementation team;
- real-world discovery still in progress;
- mobile-first operational use;
- mixed digital maturity among users;
- sensitive documents and personal data;
- need to separate operation from compliance interpretation;
- need for immutable-history principles without blocking daily operation;
- external channels must not duplicate business logic;
- blockchain must remain outside the critical operational path;
- no premature multi-tenancy or microservices.

## 5. Architectural drivers

- operational clarity;
- traceability;
- auditability;
- privacy;
- maintainability;
- mobile usability;
- explicit domain states;
- resilience to external integration failure;
- evidence integrity;
- cost-conscious evolution.

## 6. System boundaries

### Inside Normia

- identity and access;
- people and compliance;
- documents and versions;
- training and competencies;
- areas and equipment;
- tasks and scheduling;
- BPM routines;
- temperature controls;
- sanitation;
- suppliers and reception;
- shelf life;
- deviations and non-conformities;
- containment and corrective actions;
- alerts and escalation;
- dashboards and reports;
- local audit ledger;
- optional Polygon anchoring adapter.

### External or channel boundaries

- QR identifiers;
- Telegram Bot and Mini App;
- n8n orchestration;
- private file storage;
- Polygon PoS RPC and signer infrastructure.

All channels are intended to consume shared application services and domain rules.

## 7. Architecture overview

```text
Users
  │
  ├── Web / Mobile
  ├── QR context
  └── Telegram Bot / Mini App
          │
          ▼
        Laravel
          │
   Application Services
          │
      Domain Rules
          │
  ┌───────┼───────────┐
  ▼       ▼           ▼
MySQL  Private     Audit Service
       Storage          │
                        ▼
                    Hash Chain
                        │
                        ▼
                  Merkle Batches
                        │
                        ▼
                    Anchor Adapter
                        │
                        ▼
                    Polygon PoS
```

More detail: [`ARCHITECTURE.md`](ARCHITECTURE.md).

## 8. Golden Flow

The first vertical slice to validate is:

```text
LOGIN
  ↓
TODAY
  ↓
TASK INSTANCE
  ↓
EQUIPMENT / QR CONTEXT
  ↓
TEMPERATURE MEASUREMENT
  ↓
CONTROL PROFILE RESOLUTION
  ↓
EVALUATION
  ├── COMPLIANT → TASK COMPLETED → AUDIT EVENT
  └── DEVIATION
         ↓
      NON-CONFORMITY
         ↓
      CONTAINMENT
         ↓
      CORRECTIVE ACTION
         ↓
      EVIDENCE
         ↓
      SUPERVISOR VERIFICATION
         ↓
      CLOSURE
         ↓
      AUDIT EVENTS
```

The flow is not considered validated if only isolated screens or CRUD modules exist.

## 9. Key decisions

Public decisions are documented in [`DECISIONS.md`](DECISIONS.md).

Highlights:

- modular monolith before distributed architecture;
- single-tenant deployment per installation for the MVP;
- MySQL as operational source of truth;
- Laravel owns domain rules;
- channels share application services;
- n8n orchestrates but does not own domain state;
- local audit ledger before blockchain anchoring;
- Polygon outside the critical path;
- no personal or sensitive data on-chain;
- correction by supersession rather than silent overwrite.

## 10. Security and privacy

Key principles:

- sensitive files in private storage;
- authorization before file access;
- no permanent public URLs for medical certificates or personal sensitive documents;
- no personal data on-chain;
- channel actions use the same authorization and domain rules as web flows;
- critical closed records are not silently overwritten or deleted;
- blockchain anchoring stores aggregated cryptographic commitments, not operational content.

See [`SECURITY_AND_PRIVACY.md`](SECURITY_AND_PRIVACY.md).

## 11. AI-assisted development governance

Normia uses coordinated human + AI-assisted workstreams.

```text
Kike + Codex
  backend · domain · persistence · authorization · tests · audit · Polygon

Paull + Antigravity
  UX · mobile-first flows · Livewire/Blade/Filament · browser E2E · QA

Both
  branch isolation → PR → cross-review → develop → UAT → main
```

Local models may support constrained pre-review, test suggestions and documentation, but no AI agent owns production approval.

## 12. Evidence and validation

Evidence is summarized in [`EVIDENCE.md`](EVIDENCE.md).

| Capability | Evidence level |
|---|---|
| Product master and functional baseline | Documented baseline |
| MVP architecture | Frozen architecture baseline |
| Golden Flow | Defined, implementation pending |
| UX prototype | Reference prototype |
| Pilot discovery | In progress |
| Modular monolith structure | Architecture baseline / bootstrap in progress |
| Task + temperature + deviation flow | Planned vertical slice |
| CAPA and supervisor verification | Domain model defined |
| Audit ledger | Architecture defined, implementation pending |
| Merkle batching | Architecture defined, later phase |
| Polygon anchoring | Architecture defined, later phase |
| Production validation | Not yet |

## 13. Results

The current validated result is design coherence, not production performance. Normia already has:

- a consolidated product baseline;
- explicit domain distinctions;
- frozen MVP architecture;
- prioritized Golden Flow;
- sprint roadmap;
- separate human/AI-assisted workstreams;
- evidence discipline that prevents architecture concepts from being presented as deployed functionality.

## 14. Lessons so far

### A checklist is not the domain
Execution, conformity, deviation, containment, corrective action and verification are distinct concepts.

### Blockchain cannot prove physical truth
It can strengthen evidence integrity, but trust still depends on identity, timestamps, context, supervision and operational controls.

### Channels must not create parallel logic
Web, QR and Telegram should reach the same domain services.

### The exception path is as important as the green check
The product must model what happens when a control fails, not only successful completion.

### Real pilot evidence should drive generalization
Costa Racini first; generic product abstractions only after repeated patterns are observed.

## 15. Next architectural questions

- Which domain boundaries remain stable after pilot discovery?
- What evidence is mandatory for each control severity level?
- Which events deserve ledger treatment and which remain ordinary logs?
- What batch size and cadence are appropriate for Merkle anchoring?
- When does Polygon anchoring add enough trust value to justify production cost?
- Which Telegram flows are truly useful versus duplicative?
- What changes are required after real mobile use in the kitchen environment?

## Related documents

### English
- [`ARCHITECTURE.md`](ARCHITECTURE.md)
- [`DECISIONS.md`](DECISIONS.md)
- [`SECURITY_AND_PRIVACY.md`](SECURITY_AND_PRIVACY.md)
- [`EVIDENCE.md`](EVIDENCE.md)

### Español
- [`ARCHITECTURE.es.md`](ARCHITECTURE.es.md)
- [`DECISIONS.es.md`](DECISIONS.es.md)
- [`SECURITY_AND_PRIVACY.es.md`](SECURITY_AND_PRIVACY.es.md)
- [`EVIDENCE.es.md`](EVIDENCE.es.md)

### Català
- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)
- [`SECURITY_AND_PRIVACY.ca.md`](SECURITY_AND_PRIVACY.ca.md)
- [`EVIDENCE.ca.md`](EVIDENCE.ca.md)

---

This case intentionally distinguishes documented architecture, reference prototypes, implementation progress and future validation. Normia is not presented as production validated at this stage.
