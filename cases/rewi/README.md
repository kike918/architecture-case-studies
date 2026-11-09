# Rewi — Digital Loyalty SaaS Architecture

🌐 **Languages:** English · [Español](README.es.md)

**Status:** Published sanitized architecture case. **Evidence level: Deployed** (documented production release on 2026-11-03). **Not Production validated** under this repository's standard: sustained usage, complete functional coverage and a real production restore have not been established by the reviewed evidence.

## 1. Executive summary

Rewi is a loyalty SaaS designed to help small businesses operate digital stamp campaigns, customer cards and reward redemptions. Its architecture separates merchant-scoped product operations, platform administration, integration identities and background notifications. The engineering challenge is to support real business workflows while limiting cross-business data exposure and keeping deployment changes auditable.

The private product records a **v0.2.1 production deployment on November 3, 2026**, with operational health and campaign-image delivery checks. This case documents the architectural decisions and the limits of that evidence rather than reproducing source code.

## 2. Context

A merchant loyalty product must coordinate campaigns, customers, progress and rewards, while platform operators manage plans, limits and business lifecycle. Integrations and asynchronous communications add further boundaries: a third-party caller must not choose another merchant's data, and delivering a message must not become the source of truth for a completed loyalty transaction.

## 3. Problem and constraints

The product needs clear tenancy boundaries across business-facing screens and APIs; auditable loyalty events and administrative actions; predictable plan/usage controls; safe payment/provider configuration; reliable asynchronous operations; and a deployable system for a small engineering team.

Constraints include operational budget, incremental delivery, private business/customer information, external provider dependencies, evolving features and the requirement to retain a comprehensible release trail.

## 4. Architectural drivers

**Tenant isolation, correctness of reward accounting, security, maintainability, observability, predictable deployment and traceable decisions.** Not every workflow has the same evidence or release maturity.

## 5. System boundaries

- **Merchant domain:** campaigns, customer association, loyalty cards, stamps, rewards and redemptions.
- **Platform control:** plans, usage policies, merchant governance and privileged management operations.
- **Integration boundary:** separate business-scoped and platform-scoped credentials, policies and API contracts.
- **Asynchronous boundary:** notifications, outbound events, delivery retries and scheduled work.
- **External boundary:** messaging, payment and hosting providers; providers do not own the core loyalty ledger.

## 6. Sanitized logical architecture

```text
        Business users / customers     Platform operators
                  |                            |
                  +-------- Web UI ------------+
                               |
                       Application layer
                      Laravel / Livewire
                               |
                  Domain actions + policies
                               |
              +----------------+----------------+
              |                |                |
         Loyalty records  Platform control  Integration APIs
              |                |                |
              +--------- PostgreSQL ------------+
                               |
                        Queued work/events
                               |
                      Workers + scheduler
                               |
                  External delivery providers

        Boundary: controlled container / reverse-proxy deployment
```

The diagram is conceptual and omits hostnames, network addresses, sensitive infrastructure topology and non-public implementation details.

## 7. Key decisions, alternatives and trade-offs

| Decision | Why | Alternative / limitation |
|---|---|---|
| Laravel application with Livewire/Blade | Consolidate domain operations and UI delivery within a maintainable application | A separate SPA/API could add deployment and contract overhead without clear initial benefit |
| Central domain actions for mutations | Keep writes consistent across UI and integrations | Requires disciplined reuse and tests to avoid bypass paths |
| Business-scoped integration credentials | Resolve the business from the caller's identity rather than an arbitrary supplied identifier | Additional credential lifecycle, quotas and policy review |
| Separate privileged platform API | Avoid treating platform automation as an ordinary merchant | Strict privilege separation and audit requirements |
| Idempotent mutations and bounded reads | Reduce duplicate effects and uncontrolled retrieval | Complexity in replay protection and client behavior |
| Queues, workers and scheduler | Decouple external delivery from completed business transactions | Retries, monitoring and provider failures need operational handling |
| Containerized deployment and incremental release gates | Preserve reproducibility and a controlled deployment trail | Operational maintenance and backup-restore verification remain necessary |

These choices reflect documented contracts and release evidence; the case does not assert unmeasured scalability or perfect isolation.

## 8. Alternatives considered

A fully split microservices system or a separate frontend-only stack may have expanded independent deployment options. For the documented stage, the added operational surface would have required stronger justification. Direct provider calls in request paths would simplify some initial integrations but create latency and reliability coupling. The documented architecture prefers asynchronous boundaries for such work.

## 9. Security and privacy considerations

Business integration identity is distinct from privileged platform identity; authorization scopes, bounded reads, idempotency on specified mutations and audit trails are part of the documented API contracts. Public case details intentionally omit credential formats, production endpoints, internal naming and exact hardening controls.

Customer contact data, consent, messaging permissions and third-party service terms require independent compliance review. Documented mechanisms do **not** constitute an independent penetration test, complete privacy audit or universal provider activation.

## 10. Delivery and operations

The product is governed by versioned releases, reviewed changes and separate deployment acceptance steps. Internal release records report the v0.2.1 application image built and deployed, an additive campaign-image migration applied, application health returning HTTP 200, background workers/scheduler running, and an uploaded campaign image served successfully after a persistent-storage routing fix.

The evidence concerns a dated release checkpoint. It is not a live uptime monitor and should not be used to promise current service availability.

## 11. AI-assisted development governance

DCP Flow structures human + AI-assisted work through context-specific engineering rules, quality checks, evidence collection and human acceptance. Code changes, provider actions and production promotion remain subject to review; AI participation does not replace executable tests, security scrutiny or operational approval.

## 12. Evidence and validation

See [Evidence register](EVIDENCE.md). The November 3, 2026 release documents **Deployed** status for the application and tested image delivery. Some previous functional tests and local integration checks are separately recorded, but a comprehensive post-incident regression, verified production restore and sustained real-user operating results are **not** demonstrated by the referenced release notes.

## 13. Results and lessons learned

- A confirmed deployment, health check and media-path smoke test are meaningful evidence, but narrower than production certification.
- Long-running queues and external providers require explicit operational boundaries.
- API tenant resolution and domain-action reuse help prevent alternate integration paths from bypassing business rules.
- Persistent media mounts and reverse-proxy paths must be reconciled as part of release operations, not assumed from a successful image build.
- Backups being present and checked for integrity do not demonstrate restoration capability.

No adoption, conversion, revenue, latency or uptime metrics are claimed without supporting records.

## 14. Unresolved questions

1. What measured sustained-use period and operating metrics will justify **Production validated**?
2. What safely publishable evidence confirms a genuine backup restoration exercise?
3. Which full cross-role and provider scenarios have been re-run against the exact deployed release?
4. What retention, consent and message-delivery governance requires additional review?
5. What capacity/queue/provider-failure thresholds would justify architectural changes?

## Publication and disclosure note

Sanitized architecture narrative, not a source-code mirror, product security report or specification for bypassing controls. Private application code, credentials, private infrastructure, customer data, internal file paths and privileged operational instructions are excluded. Public disclosure approval does not imply that all technical validation gates are closed.
