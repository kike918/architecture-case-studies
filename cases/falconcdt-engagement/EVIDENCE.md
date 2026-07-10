# FalconCDT Engagement Platform — Evidence Register

## Purpose

This register maps public claims in the case study to evidence levels. It is intentionally conservative: roadmap items are not presented as completed capabilities.

## Evidence scale

- **Concept** — documented idea or architecture direction.
- **Prototype** — implemented experimentally, not yet used operationally.
- **Pilot** — validated in controlled real-world use.
- **Deployed** — present in an operational deployment.
- **Production validated** — repeatedly verified in production operation with stronger evidence.

## Capability evidence matrix

| Capability | Evidence level | Public-safe evidence basis |
|---|---|---|
| User registration and login | Deployed | Operational release checkpoint documents registration, login, session protection and roles |
| User dashboard and profile | Deployed | Release checkpoint lists dashboard, profile and notification preferences |
| Prediction capture | Deployed | Operational product flow and user area documented |
| Deadline validation | Deployed | Backend deadline validation and automatic lock documented |
| Phase-based scoring | Deployed | Scoring and ranking by phase documented as operational |
| Separate rankings by phase | Deployed | Operational checkpoint confirms phase separation and rankings |
| Public ranking with private history | Deployed | Public ranking and private user history separation documented |
| Admin participant management | Deployed | CRUD and participant status operations documented |
| Payment/registration administration | Deployed | Admin payment operations documented |
| Match/event administration | Deployed | CRUD and filtering documented |
| Result administration | Deployed | Regular time, extra time and penalty metadata flows documented |
| Prediction audit | Deployed | Global and per-prediction audit views documented |
| General audit logging | Deployed | Application-level audit log documented |
| Phase closure | Deployed / release validated | Formal phase closure and result validation documented |
| Winners and prizes | Deployed / release validated | Winner declaration, notification and prize handling documented |
| Email delivery | Deployed | SMTP tested and queue processing documented |
| Telegram delivery | Deployed | Individual/group integration and queue processing documented |
| Editable notification templates | Deployed | Multichannel templates documented |
| Admin daily summary | Deployed | Email/Telegram daily summary with deduplication documented |
| Automation dashboard | Deployed | Manual execution and automation run visibility documented |
| Protected automation endpoints | Deployed | Application protection through automation secret documented |
| Official result sync | Deployed | Operational external result sync with MySQL normalization documented |
| Optional enriched match details | Implemented / integration dependent | Secondary provider integration documented with graceful fallback |
| CSV exports | Deployed | Admin exports documented as operational |
| White-label configuration | Deployed baseline | Branding and commercial configuration documented |
| Multi-instance deployment model | Deployed | Product model and deployment isolation documented |
| Shared multi-tenancy | Not implemented | Explicitly excluded from current architecture |
| n8n production orchestration | Partial | Application endpoints and workflows documented; environment rollout still dependent on deployment/configuration |
| WhatsApp bridge | Roadmap | Prepared/stub only; not claimed as production delivery |
| Global responsive UX hardening | Roadmap | Explicit remaining work item |

## Evidence boundaries

This public register does not expose:

- private repository source code;
- production URLs that should remain private;
- credentials or tokens;
- real participant data;
- confidential client configurations;
- infrastructure secrets.

## Claim discipline

The public case study may state that the platform has been deployed and used operationally, but it must not claim unsupported scale, revenue, conversion improvement, user growth or uptime metrics unless those numbers are separately validated and approved for publication.
