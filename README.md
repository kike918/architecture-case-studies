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
| [Normia](cases/normia/README.md) | Architecture baseline published; implementation status under review | Food operations, compliance, corrective actions and verifiable audit trails |

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
│   ├── falconcdt-engagement/
│   ├── micropos/
│   └── normia/
├── templates/
│   ├── CASE_STUDY_TEMPLATE.md
│   └── ADR_TEMPLATE.md
└── docs/
    ├── PUBLICATION_STANDARD.md
    └── SANITIZATION_GUIDE.md
```

## Planned case studies (not yet published)

The following candidates require separate evidence, architecture and sanitization reviews before publication:

| Candidate | Editorial status | Proposed architectural focus |
|---|---|---|
| Rewi | Candidate — evidence review pending | Laravel SaaS, business isolation, payments, operational flows and deployment gates |
| Tazario Recipes | Candidate — evidence review pending | React/Hono/Drizzle monorepo, upstream separation, attribution, data boundaries and QA |
| DCP Flow | Candidate — evidence review pending | Human + AI engineering governance, context-specific blueprints, skills and quality gates |
| SipDolce Labs | Candidate — scope review pending | Astro-based editorial architecture, bilingual content and integrations |

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

**Phase:** FalconCDT and DCP DownloadGate deployed cases published; Normia architecture baseline published with implementation status under review; MicroPOS edge/offline-first baseline published with Raspberry Pi pilot planned.  
**Next milestone:** Execute the MicroPOS Raspberry Pi lab and update its evidence register with measured results.

---

**Enrique Reasco Marines**  
Systems Engineer · Digital Transformation & Applied AI Consultant · Founder & Product Builder
