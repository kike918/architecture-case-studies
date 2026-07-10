# FalconCDT Engagement Platform — Architecture

## Purpose

Describe the public-safe architecture of the FalconCDT Engagement Platform without exposing private implementation details or client-confidential information.

## Architectural style

The current product uses a lightweight layered PHP architecture backed by MySQL/MariaDB.

```text
Web routes
    ↓
Controllers
    ↓
Services
    ↓
Repositories / Providers
    ↓
MySQL + external integrations
```

Responsibilities are separated intentionally:

- controllers coordinate requests and responses;
- services contain business logic;
- repositories contain SQL access;
- providers isolate external services;
- views do not execute SQL directly.

## Deployment model

The product currently uses a white-label multi-instance model.

```text
Client A instance
├── application
├── database
├── branding
├── rules
└── notification configuration

Client B instance
├── application
├── database
├── branding
├── rules
└── notification configuration
```

This is not shared-database multi-tenancy.

### Why

The model favors:

- simpler operational isolation;
- safer client-specific configuration;
- clearer failure boundaries;
- easier rollback reasoning;
- lower architecture complexity during product validation.

The cost is duplicated deployment and upgrade work.

## Core runtime data flow

```text
Participant
    │
    ▼
Prediction UI
    │
    ▼
Backend deadline validation
    │
    ▼
Prediction persistence
    │
    ├── audit trail
    └── lock enforcement

Official result provider
    │
    ▼
Normalization / sync layer
    │
    ▼
MySQL official result state
    │
    ▼
Scoring service
    │
    ▼
Phase leaderboard
    │
    ▼
Public ranking
```

## Phase model

The architecture treats competition phases as first-class boundaries.

```text
Phase
  ├── matches/events
  ├── scoring context
  ├── leaderboard
  ├── winner
  └── prize configuration
```

This allows one campaign to have independent ranking periods without deleting historical scores.

## Result-source separation

The architecture distinguishes official truth from optional enrichment.

```text
Official provider
    │
    ├── final status
    ├── official score
    ├── scoring trigger
    └── ranking impact

Optional enrichment provider
    │
    ├── live status
    ├── minute
    ├── venue
    ├── referee
    ├── events
    ├── statistics
    └── lineups
```

A secondary provider cannot override official scoring truth.

This avoids conflicting providers influencing the same business decision.

## Notification architecture

```text
Domain event / scheduled action
        ↓
Notification template
        ↓
Channel-specific queue
        ↓
Processor
        ├── Email
        ├── Telegram
        └── Future channels
```

Key goals:

- channel separation;
- template reuse;
- controlled retries;
- operational visibility;
- ability to process manually when needed.

## Automation boundary

n8n is treated as an external orchestrator.

```text
n8n schedule
    ↓
HTTPS request
    ↓
Protected automation endpoint
    ↓
Application service
    ↓
Domain data + notification queues
```

n8n should not connect directly to the production database for core workflows.

The application remains the owner of:

- scoring;
- phase state;
- ranking;
- winners;
- notification generation rules;
- audit behavior.

## Security boundaries

```text
Internet
   │
   ▼
Web layer restrictions
   │
   ├── private path blocking
   ├── script execution restrictions in uploads
   └── sensitive extension blocking
   │
   ▼
Application authentication / authorization
   │
   ├── admin routes
   └── participant routes
   │
   ▼
Service layer
   │
   ▼
Database
```

Automation endpoints add a separate authentication boundary through an automation secret and optional network restrictions.

## Operational architecture

The product architecture includes operational documents and procedures as first-class assets:

- database patch sequencing;
- backups;
- rollback;
- security checklist;
- deployment validation;
- release checkpoints;
- environment-specific verification.

This is especially important in hosting environments where cron, SQL modes and runtime behavior can differ from local development.

## Evolution triggers

Architecture should evolve only when evidence justifies it.

Potential triggers:

### Multi-tenancy
Consider only when client count, deployment cost and configuration consistency justify a shared control plane.

### Dedicated queues/workers
Consider when notification volume, retry behavior or latency requirements exceed the current queue-processing model.

### Containerized deployment
Consider when environment drift or multi-instance upgrade cost becomes a dominant operational burden.

### Centralized observability
Consider when production incident volume or deployment scale requires structured metrics, tracing and alerting.
