# FalconCDT Engagement Platform — Security and Privacy

## Scope

This document summarizes public-safe security and privacy principles reflected in the platform architecture. It does not disclose private infrastructure details, credentials, internal endpoints or client-confidential configurations.

## 1. Authentication and authorization

The application separates participant and administrator responsibilities.

Public-safe principles:

- authenticated sessions are required for protected user areas;
- administrator routes are protected by role checks;
- participant routes do not inherit administrative privileges;
- account state can affect access;
- privileged actions are intended to remain auditable.

## 2. Secrets management

The repository must not contain:

- `.env` files;
- SMTP credentials;
- Telegram tokens;
- automation secrets;
- API keys;
- private backups;
- production logs;
- uploaded user files.

Configuration secrets remain environment-specific and outside version control.

## 3. Web-layer hardening

The deployment model includes web-server rules intended to:

- block private application directories from direct web access;
- prevent execution of scripts from upload directories;
- block sensitive file extensions and metadata files;
- reduce accidental exposure of configuration and operational documentation.

## 4. Automation endpoint protection

Automation flows use protected application endpoints instead of direct external access to the production database.

Security controls include:

- shared automation secret;
- optional network/IP restriction;
- application-layer authorization boundary;
- no exposure of database credentials to workflow automation.

## 5. Logging and redaction

Operational logs should not become a secondary secret store.

The platform direction includes:

- redaction of known secret values from error output;
- avoiding raw credential dumps;
- separating debugging needs from production-safe logs;
- keeping production debug mode disabled.

## 6. Participant privacy

The platform intentionally separates:

```text
Public ranking
        ≠
Public detailed prediction history
```

A participant may appear in aggregate standings while detailed prediction history remains private to authorized contexts.

This supports engagement without unnecessarily exposing user behavior.

## 7. External providers

External APIs are treated as untrusted integration boundaries.

Principles:

- API keys remain outside the repository;
- external payloads are normalized before domain use;
- secondary providers cannot silently override official scoring truth;
- unavailable optional providers should degrade gracefully rather than break the entire public application.

## 8. Upload and content handling

Public-safe controls include:

- upload-directory execution restrictions;
- separation of generated/uploaded files from application code;
- allowlist-based sanitization for rich HTML content.

## 9. Operational risks

Relevant risks include:

- environment drift between local and hosting SQL configuration;
- missed database patches;
- timezone mismatches;
- notification credential misconfiguration;
- external provider outages;
- queue-processing failures;
- accidental production debug enablement.

These risks are handled through release checkpoints, checklists, environment verification and rollback documentation rather than assuming perfect infrastructure.

## 10. Public disclosure boundary

This case study intentionally does not publish:

- production credentials;
- private endpoints;
- internal server paths;
- database schema details that create unnecessary attack surface;
- private client configurations;
- production logs;
- personal participant data.
