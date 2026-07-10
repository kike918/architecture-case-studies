# FalconCDT Engagement Platform

**Status:** Deployed case study — public-safe architecture summary based on an operational B2B white-label engagement platform.

## 1. Executive summary

FalconCDT Engagement Platform evolved from a real prediction-game implementation into a reusable B2B engagement product for brands, businesses, communities and private campaigns.

The core architectural challenge was not simply to collect predictions. It was to support a reusable operating model with participant registration, private user areas, administrative control, deadlines, scoring, phase-based rankings, messaging, notifications, auditing, branding and deployment for multiple client instances without prematurely introducing a complex shared multi-tenant SaaS architecture.

The current solution uses a lightweight PHP/MySQL architecture with service and repository boundaries, separate white-label deployments per client instance, asynchronous-capable notification queues, protected automation endpoints and explicit separation between official result data and optional enriched match data.

**Evidence level:** `Deployed` with operational use and production-oriented hardening; some integrations and UX improvements remain roadmap items.

## 2. Context

The platform serves engagement scenarios where a business or community wants to run a branded participation dynamic around predictions, challenges, rankings, rewards or private events.

Typical requirements include:

- participant registration and authentication;
- independent phases with separate rankings;
- deadline enforcement;
- scoring rules;
- public ranking without exposing private prediction history;
- administrative visibility;
- configurable prizes and commercial settings;
- email and Telegram communication;
- client-specific branding;
- audit trails;
- operational dashboards;
- independent deployment per client.

The first operational implementation was a private 2026 football prediction experience. The product direction then expanded toward a reusable B2B engagement platform rather than a one-off tournament site.

## 3. Problem

A reusable engagement platform must reconcile two competing needs:

1. **Product reuse:** shared scoring, ranking, administration, notification and audit capabilities.
2. **Client isolation:** different branding, rules, participants, prizes, configuration and operational timelines.

The architecture also needed to remain maintainable for a small delivery team and deployable on practical shared/cloud hosting without introducing infrastructure that exceeded the needs of the initial operating model.

## 4. Constraints

The main constraints were:

- small development and operating team;
- need for fast delivery and iteration;
- real client-specific branding and configuration;
- limited justification for premature multi-tenancy;
- shared-hosting deployment constraints;
- external sports-data API limits and inconsistency;
- need to preserve user privacy around prediction history;
- need for auditable scoring and administrative actions;
- cron reliability concerns in the hosting environment;
- notification channels with different delivery characteristics;
- requirement to avoid production secrets in source control.

## 5. Architectural drivers

The strongest drivers were:

- **deployment simplicity**;
- **operational isolation between clients**;
- **auditability**;
- **maintainability**;
- **data-source clarity**;
- **controlled automation**;
- **privacy-aware ranking design**;
- **extensibility without framework overreach**;
- **cost control**.

## 6. System boundaries

### Inside the platform

- authentication and participant management;
- user dashboard and profile;
- prediction capture;
- deadline validation and locking;
- scoring and rankings;
- phase management;
- payments/registration tracking where applicable;
- winner and prize management;
- administrative dashboards;
- internal messaging;
- notification templates and queues;
- audit logs;
- automation endpoints;
- white-label configuration.

### External systems

- official sports-data provider;
- optional match-detail data provider;
- SMTP provider;
- Telegram Bot API;
- n8n for external orchestration;
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

The deployment model currently favors independent client installations. Each instance can have its own:

- database;
- configuration;
- branding;
- rules;
- participants;
- prizes;
- notification settings.

This creates stronger operational isolation and simpler reasoning at the cost of duplicated deployment and maintenance work.

Operational practices include:

- documented database patches;
- backup and rollback procedures;
- release checkpoints;
- deployment checklists;
- manual validation in the target hosting environment;
- protected automation endpoints for n8n rather than direct database access.

## 11. AI-assisted development

The project has used AI-assisted development for scoped implementation, documentation, refactoring and operational workflow design.

The intended governance model is:

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

Current evidence supports the following classifications:

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

The strongest validated result is architectural rather than promotional: the platform evolved from one real engagement dynamic into a reusable multi-instance product baseline while preserving operational simplicity.

Public-safe evidence confirms that the platform supports:

- independent phases;
- scoring and rankings;
- administrative operations;
- audit trails;
- notification workflows;
- external result synchronization;
- client-specific configuration and branding;
- production-oriented hardening and rollback documentation.

No unsupported business-performance claims are included in this public case.

## 14. Lessons learned

### 1. Multi-instance can be the correct first architecture

A separate deployment per client can be preferable to multi-tenancy when the product is still validating real client differences and operational ownership.

### 2. One provider should own official truth

Using multiple external providers is useful only when responsibilities are explicit. One provider decides official results; another may enrich presentation without affecting scoring.

### 3. Automation must not own the domain

n8n can trigger jobs, retries and notifications, but core scoring, ranking and phase state remain inside the application domain.

### 4. Operational documentation is part of architecture

Backup, rollback, patch sequencing and release checkpoints are architectural concerns when deployment environments are constrained.

### 5. Privacy boundaries matter even in engagement products

A public ranking does not require exposing participant prediction history.

## 15. Next architectural questions

The main questions that could trigger future evolution are:

- At what number of clients does multi-instance operational cost justify multi-tenancy?
- Which configuration elements belong in data, code or deployment automation?
- Should notifications evolve into a dedicated provider abstraction with retry policies and delivery metrics?
- When does queue processing require a dedicated worker model?
- Should deployment move from shared hosting toward containerized standardized environments?
- What telemetry is needed before introducing deeper observability infrastructure?
- How should the platform generalize beyond sports predictions into broader engagement mechanics without weakening the domain model?

## Related documents

- [`ARCHITECTURE.md`](ARCHITECTURE.md)
- [`DECISIONS.md`](DECISIONS.md)
- [`SECURITY_AND_PRIVACY.md`](SECURITY_AND_PRIVACY.md)
- [`EVIDENCE.md`](EVIDENCE.md)

---

This case study intentionally excludes credentials, private endpoints, client-confidential data and proprietary source code.
