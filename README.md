# Architecture Case Studies

🌐 **Languages:** English · [Español](README.es.md)

Public, sanitized architecture case studies focused on real business constraints, engineering trade-offs and practical product delivery.

> This repository documents how problems are framed, architectures are shaped and technical decisions are evaluated. It does not expose private source code, credentials, confidential client data or proprietary implementation details.

## Purpose

The goal is to present selected architecture work across digital products, business systems, offline-first applications, engagement platforms, automation, controlled distribution and traceability.

Each case study focuses on business context, constraints, architectural drivers, system boundaries, major decisions, alternatives, trade-offs, security, validation evidence and lessons learned.

## Case roadmap

| Case | Status | Focus |
|---|---|---|
| [FalconCDT Engagement Platform](cases/falconcdt-engagement/README.md) | Published v1 | White-label engagement, scoring, notifications and operational delivery |
| [DCP DownloadGate](cases/dcp-downloadgate/README.md) | Published; deployed evidence | Controlled private file distribution, temporary access, protected hosting boundaries and auditability |
| [MicroPOS](cases/micropos/README.md) | Architecture baseline published; Raspberry Pi pilot planned | Offline-first POS, edge deployment, ERP adapters and low-connectivity resilience |
| [Normia](cases/normia/README.md) | Architecture baseline published; development paused | Food operations, compliance, corrective actions and verifiable audit trails |

The cases are published progressively. Architecture baselines are not treated as production validation until evidence exists.

## Repository structure

```text
architecture-case-studies/
├── README.md
├── README.es.md
├── CONTRIBUTING.md
├── SECURITY.md
├── cases/
│   ├── dcp-downloadgate/
│   ├── dcp-flow/
│   ├── falconcdt-engagement/
│   ├── micropos/
│   ├── normia/
│   ├── rewi/
│   ├── sipdolce-labs/
│   └── tazario-recipes/
├── templates/
│   ├── CASE_STUDY_TEMPLATE.md
│   └── ADR_TEMPLATE.md
└── docs/
    ├── PUBLICATION_STANDARD.md
    └── SANITIZATION_GUIDE.md
```

## Additional published cases and candidates

The following cases include published technical narratives and unpublished candidates. Publication does not imply production validation:

| Case / candidate | Editorial status | Architectural focus |
|---|---|---|
| [Rewi v0.2.1](cases/rewi/README.md) | Published case — Deployed (2026-11-03); not Production validated | Laravel loyalty SaaS, tenancy boundaries, scoped integrations, asynchronous work and release evidence |
| [Tazario Recipes](cases/tazario-recipes/README.md) | Published architecture case — GCP deployment prepared, production unverified | React/Hono/Drizzle monorepo, upstream MIT attribution, isolated persistence, deployment plan and evidence limits |
| [DCP Flow](cases/dcp-flow/README.md) | Published methodology case — documented application, outcomes not quantified | Human + AI engineering governance, solution discovery, stack-specific blueprints, skills and evidence-driven gates |
| [SipDolce Labs](cases/sipdolce-labs/README.md) | Published case — v1 website deployed; later changes remain in development | Astro/TypeScript bilingual SSG, bounded PHP/SQLite intake and editorial publishing governance |

A candidate is not a published case or a production-validation claim. [DCP Flow documentation](https://dcpflow.digitalconsultingplus.co/) provides public methodological context.

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

**Phase:** FalconCDT, DCP DownloadGate and Rewi have published cases with deployment evidence (at different validation levels); Normia development remains paused; MicroPOS Raspberry Pi pilot remains planned. Tazario Recipes has published architecture and documented deployment preparation, without confirmed production operation.  
**Next milestone:** Refresh evidence for existing cases as releases and controlled pilots are completed, including the next SipDolce Labs editorial release and MicroPOS edge lab.

---

**Enrique Reasco Marines**  
Systems Engineer · Digital Transformation & Applied AI Consultant · Founder & Product Builder
