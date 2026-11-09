# Architecture Case Studies

🌐 **Languages:** English · [Español](README.es.md)

Public, sanitized architecture case studies focused on real business constraints, engineering trade-offs and practical product delivery.

> This repository documents how problems are framed, architectures are shaped and technical decisions are evaluated. It does not expose private source code, credentials, confidential client data or proprietary implementation details.

## Purpose

The goal is to present selected architecture work across digital products, business systems, offline-first applications, engagement platforms, automation, controlled distribution and traceability.

Each case study focuses on business context, constraints, architectural drivers, system boundaries, major decisions, alternatives, trade-offs, security, validation evidence and lessons learned.

## Published cases — 8

All eight cases below are **published editorially**; their technical evidence levels differ. See each case's register before inferring a production claim.

| Case | Editorial / technical status | Scope |
|---|---|---|
| [FalconCDT Engagement Platform](cases/falconcdt-engagement/README.md) | Published v1 · Deployed | White-label engagement, scoring, notifications and operational delivery |
| [DCP DownloadGate](cases/dcp-downloadgate/README.md) | Published · Deployed (documented evidence) | Controlled file distribution, temporary access and protected storage |
| [MicroPOS](cases/micropos/README.md) | Published · commercial web documented; edge Concept / pilot pending | Astro/PHP/SQLite commercial web plus separate offline-first POS architecture |
| [Normia](cases/normia/README.md) | Published · Concept/prototype baseline; development paused | Food-service compliance, corrective actions and verifiable records |
| [Rewi v0.2.1](cases/rewi/README.md) | Published · Deployed 2026-11-03; sustained validation pending | Laravel loyalty SaaS, scoped integrations, queues and release evidence |
| [Tazario Recipes](cases/tazario-recipes/README.md) | Published · implementation documented; deployment prepared, not verified | TypeScript React/Hono/Drizzle, upstream attribution and GCP plan |
| [DCP Flow](cases/dcp-flow/README.md) | Published · Methodology (product maturity N/A); application documented | Human + AI method, discovery, contextual blueprints and quality gates |
| [SipDolce Labs](cases/sipdolce-labs/README.md) | Published · v1 Deployed; subsequent editorial changes in development | Bilingual Astro SSG editorial site with bounded PHP/SQLite intake |

**No unpublished candidates are listed at this review date.** Future candidates require evidence, sanitization, architectural review and publication approval. The five product maturity levels are defined in [Publication Standard](docs/PUBLICATION_STANDARD.md); methodology cases are N/A.

## Repository structure

```text
architecture-case-studies/
├── README.md / README.es.md
├── cases/
│   ├── falconcdt-engagement/
│   ├── dcp-downloadgate/
│   ├── micropos/
│   ├── normia/
│   ├── rewi/
│   ├── tazario-recipes/
│   ├── dcp-flow/
│   ├── sipdolce-labs/
├── templates/
└── docs/PUBLICATION_STANDARD.md
```

## Latest documentation audit

[Corrective GitHub portfolio audit — 2026-11-09](docs/PORTFOLIO_AUDIT_2026-11-09.md) records evidence limits, link-check results and remaining external/runtime validation gates.

## Publication principles

- Evidence before claims.
- Decisions before diagrams.
- Context before technology.
- Trade-offs over hype.
- Sanitization before publication.
- No confidential data.
- No credentials or production secrets.
- No client-specific details without authorization.

## Case study lifecycle

```text
Candidate
   ↓
Evidence Review
   ↓
Sanitized Draft
   ↓
Architecture Review
   ↓
Public Review
   ↓
Published
   ↓
Updated when evidence changes
```

## What this repository is not

This repository is not a source-code mirror of private products, a marketing brochure, a place to publish secrets, or a claim that every documented concept is already in production.

## Status

**Phase:** Eight published cases with distinct, explicitly qualified maturity levels. Rewi, FalconCDT and DCP DownloadGate have deployment evidence; SipDolce Labs v1 is documented as deployed; Tazario GCP deployment and MicroPOS edge pilot remain unverified; Normia is paused; DCP Flow is a methodology.  
**Next milestone:** Update evidence when new releases/pilots are actually observed.

---

**Enrique Reasco Marines**  
Systems Engineer · Digital Transformation & Applied AI Consultant · Founder & Product Builder
