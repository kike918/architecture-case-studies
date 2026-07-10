# FalconCDT Engagement Platform

🌐 **Languages:** English · [Español](README.es.md) · [Català](README.ca.md)

**Status:** Deployed case study — public-safe architecture summary based on an operational B2B white-label engagement platform.

## 1. Executive summary

FalconCDT Engagement Platform evolved from a real prediction-game implementation into a reusable B2B engagement product for brands, businesses, communities and private campaigns.

The core architectural challenge was not simply to collect predictions. It was to support a reusable operating model with participant registration, private user areas, administrative control, deadlines, scoring, phase-based rankings, messaging, notifications, auditing, branding and deployment for multiple client instances without prematurely introducing a complex shared multi-tenant SaaS architecture.

The current solution uses a lightweight PHP/MySQL architecture with service and repository boundaries, separate white-label deployments per client instance, asynchronous-capable notification queues, protected automation endpoints and explicit separation between official result data and optional enriched match data.

**Evidence level:** `Deployed` with operational use and production-oriented hardening; some integrations and UX improvements remain roadmap items.

## 2. Context

The platform serves engagement scenarios where a business or community wants to run a branded participation dynamic around predictions, challenges, rankings, rewards or private events.

Typical requirements include participant registration, independent phases, scoring, rankings, private prediction history, administrative visibility, configurable rewards, notifications, branding, audit trails and independent deployment per client.

The first operational implementation was a private 2026 football prediction experience. The product direction then expanded toward a reusable B2B engagement platform rather than a one-off tournament site.

## 3. Problem

A reusable engagement platform must reconcile two competing needs:

1. **Product reuse:** shared scoring, ranking, administration, notification and audit capabilities.
2. **Client isolation:** different branding, rules, participants, prizes, configuration and operational timelines.

The architecture also needed to remain maintainable for a small delivery team and deployable on practical hosting without introducing infrastructure that exceeded the needs of the initial operating model.

## 4. Constraints

- small development and operating team;
- fast delivery and iteration;
- client-specific branding and configuration;
- limited justification for premature multi-tenancy;
- hosting constraints;
- external sports-data API limits and inconsistency;
- privacy of prediction history;
- auditable scoring and administrative actions;
- cron reliability concerns;
- channels with different delivery characteristics;
- production secrets kept out of source control.

## 5. Architectural drivers

- deployment simplicity;
- client isolation;
- auditability;
- maintainability;
- data-source clarity;
- controlled automation;
- privacy-aware ranking design;
- extensibility without framework overreach;
- cost control.

## 6. System boundaries

### Inside the platform

- authentication and participant management;
- user dashboard and profile;
- prediction capture;
- deadline validation and locking;
- scoring and rankings;
- phase management;
- registration/payment tracking where applicable;
- winner and prize management;
- admin dashboards;
- internal messaging;
- notification templates and queues;
- audit logs;
- automation endpoints;
- white-label configuration.

### External systems

- official sports-data provider;
- optional match-detail provider;
- SMTP provider;
- Telegram Bot API;
- n8n orchestration;
- future WhatsApp bridge.

The frontend does not directly call external sports APIs. Runtime application data is normalized into MySQL first.

## 7. Architecture overview

```text
Participants / Admins
        │
        ▼
   Web Application
   PHP + HTML/CSS/JS
        │
        ├── Controllers
        ├── Services
        ├── Repositories
        ├── Providers
        └── Views
        │
        ▼
    MySQL / MariaDB
   operational source of truth
        │
        ├── scoring & rankings
        ├── phases & winners
        ├── notification queues
        ├── configuration
        └── audit logs

External integrations
        │
        ├── official result provider
        ├── optional enrichment provider
        ├── SMTP
        ├── Telegram
        └── n8n orchestration
```

More detail: [`ARCHITECTURE.md`](ARCHITECTURE.md).

## 8. Key decisions

The main public architectural decisions are documented in [`DECISIONS.md`](DECISIONS.md).

Highlights:

- multi-instance instead of premature multi-tenancy;
- MySQL as runtime source of truth;
- one official provider for scoring decisions;
- secondary providers only for optional enrichment;
- business logic in services and SQL access in repositories;
- notifications through queues and templates;
- n8n as orchestrator, not domain owner;
- protected automation endpoints;
- privacy boundary between rankings and private prediction history.

## 9. Security and privacy

Security principles include:

- credentials and tokens remain outside Git;
- production debug mode disabled;
- private directories and sensitive extensions blocked at the web layer;
- upload directories prevent script execution;
- automation endpoints protected with a shared secret and optional IP restriction;
- known secrets redacted from logs;
- public ranking separated from private prediction history;
- sensitive administrative actions recorded through audit logging.

See [`SECURITY_AND_PRIVACY.md`](SECURITY_AND_PRIVACY.md).

## 10. Delivery and operations

The deployment model favors independent client installations, each with its own database, configuration, branding, rules, participants, prizes and notification settings.

Operational practices include documented database patches, backup and rollback procedures, release checkpoints, deployment checklists, target-environment validation and protected automation endpoints for n8n rather than direct database access.

## 11. AI-assisted development

The project has used AI-assisted development for scoped implementation, documentation, refactoring and operational workflow design.

```text
Issue / defined scope
        ↓
AI-assisted implementation or analysis
        ↓
Human review
        ↓
Manual or automated validation
        ↓
Deployment checkpoint
        ↓
Production verification
```

AI assistance does not replace production approval, secrets management, security validation or human accountability.

## 12. Evidence and validation

Evidence is summarized in [`EVIDENCE.md`](EVIDENCE.md).

| Capability | Evidence level |
|---|---|
| Authentication and role-protected routes | Deployed |
| Prediction capture and deadline enforcement | Deployed |
| Phase-based scoring and ranking | Deployed |
| Administration modules | Deployed |
| Phase closure, winners and prizes | Deployed / release-validated |
| Email notifications | Deployed |
| Telegram integration | Deployed |
| Admin daily summary | Deployed |
| External official result synchronization | Deployed |
| Optional enriched match detail | Implemented, integration-dependent |
| n8n production orchestration | Partial / environment-dependent |
| WhatsApp bridge | Roadmap |
| Fully responsive UX hardening | Roadmap |
| Shared multi-tenant architecture | Not implemented by design |

## 13. Results

The strongest validated result is architectural: the platform evolved from one real engagement dynamic into a reusable multi-instance product baseline while preserving operational simplicity.

Public-safe evidence confirms independent phases, scoring and rankings, administrative operations, audit trails, notification workflows, external result synchronization, client-specific configuration and production-oriented hardening.

No unsupported business-performance claims are included in this public case.

## 14. Lessons learned

### Multi-instance can be the correct first architecture
A separate deployment per client can be preferable to multi-tenancy while real client differences are still being validated.

### One provider should own official truth
One provider decides official results; another may enrich presentation without affecting scoring.

### Automation must not own the domain
n8n can trigger jobs and notifications, but scoring, ranking and phase state remain inside the application domain.

### Operational documentation is part of architecture
Backup, rollback, patch sequencing and release checkpoints are architectural concerns.

### Privacy boundaries matter even in engagement products
A public ranking does not require exposing participant prediction history.

## 15. Next architectural questions

- At what number of clients does multi-instance operational cost justify multi-tenancy?
- Which configuration elements belong in data, code or deployment automation?
- When does queue processing require dedicated workers?
- Should deployment move toward containerized environments?
- What telemetry is needed before deeper observability infrastructure?
- How should the platform generalize beyond sports predictions without weakening the domain model?

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

This case study intentionally excludes credentials, private endpoints, client-confidential data and proprietary source code.
