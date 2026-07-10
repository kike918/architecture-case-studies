# Architecture Case Studies

🌐 **Languages:** English · [Español](README.es.md)

Public, sanitized architecture case studies focused on real business constraints, engineering trade-offs and practical product delivery.

> This repository documents how problems are framed, architectures are shaped and technical decisions are evaluated. It does not expose private source code, credentials, confidential client data or proprietary implementation details.

## Purpose

The goal is to present selected architecture work across digital products, business systems, offline-first applications, engagement platforms, automation and traceability.

Each case study focuses on business context, constraints, architectural drivers, system boundaries, major decisions, alternatives, trade-offs, security, validation evidence and lessons learned.

## Case roadmap

| Case | Status | Focus |
|---|---|---|
| [FalconCDT Engagement Platform](cases/falconcdt-engagement/README.md) | Published v1 | White-label engagement, scoring, notifications and operational delivery |
| MicroPOS | Planned | Offline-first POS, edge deployment and low-connectivity environments |
| [Normia](cases/normia/README.md) | Architecture baseline published; implementation in progress | Food operations, compliance, corrective actions and verifiable audit trails |

The cases are published progressively. Draft cases are not treated as completed implementations until evidence exists.

## Repository structure

```text
architecture-case-studies/
├── README.md
├── README.es.md
├── CONTRIBUTING.md
├── SECURITY.md
├── cases/
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

**Phase:** FalconCDT case published; Normia architecture baseline published with explicit implementation-in-progress evidence.  
**Next milestone:** Review evidence and architecture scope for the MicroPOS case study.

---

**Enrique Reasco Marines**  
Systems Engineer · Digital Transformation & Applied AI Consultant · Founder & Product Builder
