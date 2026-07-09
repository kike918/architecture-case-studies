# Sanitization Guide

## Purpose

Protect clients, users, infrastructure and proprietary implementation details while still publishing useful architecture knowledge.

## Never publish

- credentials, API keys, private keys or tokens;
- production database dumps;
- personal data;
- client-confidential records;
- internal IP addresses;
- private hostnames or hidden endpoints;
- secrets-management layouts that increase attack surface;
- proprietary source copied from private repositories;
- exact security controls when disclosure would materially weaken them;
- contract, pricing or commercial information without authorization.

## Prefer abstraction

Replace:

```text
prod-api-client-x.internal.example.com
```

with:

```text
Application API
```

Replace:

```text
specific customer database table names
```

with:

```text
Operational Data Store
```

Replace exact identifiers with role-based or domain-level descriptions.

## Client references

Use one of three modes:

1. **Named and authorized** — the public name may be used.
2. **Anonymized** — describe sector and operating context without identity.
3. **Generic pattern** — extract the architecture lesson without customer context.

## Production evidence

Evidence may be presented as:

- anonymized architecture observations;
- non-sensitive performance ranges;
- public screenshots with sensitive data removed;
- synthetic examples;
- sanitized sequence diagrams;
- aggregate metrics where disclosure is safe and authorized.

## AI-assisted sanitization rule

AI tools may help identify disclosure risks, but human review is mandatory before publication.

## Final check

Before merging a public case, ask:

> Could this information expose a client, user, credential, private system, proprietary implementation or meaningful attack path?

If the answer is uncertain, do not publish until reviewed.
