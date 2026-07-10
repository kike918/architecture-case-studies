# Normia — Evidence Register

## Purpose

This register separates documented architecture, reference prototypes, implementation work and future validation. Normia is not yet presented as production validated.

## Evidence scale

- **Documented baseline** — product or architecture definition approved for implementation.
- **Reference prototype** — UX or flow reference, not production behavior.
- **Implementation in progress** — active coding/bootstrap work.
- **Pilot pending** — requires real operational validation.
- **Later phase** — intentionally sequenced after the Golden Flow.
- **Production validated** — not currently claimed.

## Capability matrix

| Capability | Evidence level | Public-safe basis |
|---|---|---|
| Product definition | Documented baseline | Consolidated master and project baseline exist |
| MVP architecture | Documented baseline | Architecture frozen for MVP; structural change requires ADR and human approval |
| Mobile-first task-driven UX principle | Documented baseline | Product principles and prototype direction defined |
| UX prototype | Reference prototype | v0.1 reference, explicitly non-production |
| Pilot discovery | In progress | Real pilot discovery and Sprint 0 planned/in progress |
| Modular monolith | Architecture baseline / bootstrap in progress | Laravel modular design documented |
| Single-tenant per installation | Architecture baseline | MVP deployment strategy documented |
| Identity and role model | Domain baseline | Operator, Supervisor, Admin and Auditor/Verifier responsibilities defined |
| Task execution | Golden Flow defined | End-to-end vertical slice specified |
| Temperature control | Golden Flow defined | measurement, control profile resolution and evaluation specified |
| Deviation handling | Domain model defined | compliant and non-compliant paths specified |
| Containment | Domain model defined | distinct from corrective action |
| Corrective action lifecycle | Domain model defined | explicit state lifecycle specified |
| Supervisor verification | Domain model defined | approve/return cycle specified |
| Document lifecycle | Domain baseline | versioning and document states defined |
| Private sensitive storage | Architecture baseline | controlled access pattern documented |
| Audit events | Architecture/domain baseline | candidate events and separation from ledger defined |
| Local audit ledger | Architecture defined | implementation pending |
| Hash chain | Later phase | sequenced after operational flow |
| Merkle batching | Later phase | architecture defined |
| Polygon testnet anchoring | Later phase | architecture defined |
| Polygon production anchoring | Later phase | requires prior validation |
| Telegram Bot/Mini App | Channel architecture defined | operational usefulness still to validate |
| n8n orchestration | Architecture boundary defined | implementation/operations still to validate |
| Production validation | Not claimed | pilot and implementation evidence not yet sufficient |

## Golden Flow exit evidence required

The first vertical slice should only be considered approved when:

- it works on a real phone;
- Operator and Supervisor permissions differ correctly;
- compliant and non-compliant paths work;
- historical data is not destroyed;
- domain and permission tests exist;
- audit events originate from backend behavior;
- errors do not leave impossible states;
- human review has occurred;
- documentation matches implementation.

## Claim discipline

This case may describe architecture, domain modeling and implementation direction. It must not claim regulatory certification, production scale, operational compliance improvement, audit acceptance or blockchain-backed production verification until evidence supports those claims.
