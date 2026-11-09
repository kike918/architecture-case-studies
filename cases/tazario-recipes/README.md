# Tazario Recipes by SipDolce — Architecture Case Study

🌐 **Languages:** English · [Español](README.es.md)

**Status:** Public-review candidate (sanitized draft). **Evidence level:** Architecture and deployment preparation documented; production deployment and sustained operation **not verified**. The underlying product source remains private.

## 1. Executive summary

Tazario Recipes adapts the MIT-licensed [BrewForm](https://github.com/Ardakilic/BrewForm) foundation into a specialty-coffee recipe and learning product for SipDolce Labs. The engineering problem is to adapt an existing application to a new product identity, bilingual content, curated assets and operating model without losing provenance, historical data or maintainability.

Its solution is a TypeScript monorepo with a React/Vite browser client, a Hono API, shared validation contracts, Drizzle persistence and PostgreSQL. A container-based Google Cloud Compute Engine deployment model has been documented. **Documented deployment readiness does not establish a successful live deployment.**

## 2. Context and problem

Coffee recipes involve more than a title and ingredients: preparation parameters, brewing equipment, varieties and sensory descriptors require structured, discoverable content. Existing software provides a useful starting point, but changing the product identity and extending a third-party codebase creates integration, licensing, data-migration and maintenance risks.

The objective is to preserve the useful upstream foundation while establishing clear boundaries for the SipDolce-specific product, localized experience and operational data.

## 3. Constraints

- Small-team delivery and cost-conscious operations.
- Preserve historical recipe and media data; avoid destructive resets and unreviewed migrations.
- Keep SipDolce-specific assets and code separate from potential upstream contributions.
- Preserve the original MIT license and independent third-party content licenses.
- Support Spanish and English, without treating translation coverage as production validation.
- Keep development/test services separate from production services.
- Avoid disclosing private application source, deployment secrets, exact infrastructure layout or user data.

## 4. Architectural drivers

**Maintainability, provenance, data integrity, privacy, localization, predictable operations and controlled deployment.** Architectural simplicity is preferred to premature microservices or platform complexity.

## 5. System boundaries

**Inside the product:** browser experience and recipe/catalog domain; API and authorization boundaries; shared schema contracts; relational persistence; uploaded media and product-specific editorial content.

**External:** upstream BrewForm maintenance; third-party packages and licensed media; hosting/container registry; email or other integrations as configured.

The public diagram intentionally omits internal routes, identifiers, network topology and privileged details.

## 6. Architecture overview

```text
                       End users
                           |
                    Browser application
                    React / TypeScript
                           |
                      Application API
                       Hono / Node
                           |
                    Shared validation
                      Zod contracts
                           |
             +-------------+-------------+
             |                           |
        Data access                  Media adapter
       Drizzle / SQL                 File storage
             |
         PostgreSQL

Deployment boundary: reverse proxy / TLS -> application services
Development-only diagnostics and test services remain outside production.
```

This is a **sanitized logical diagram**, not a production network or trust-policy specification.

## 7. Architectural decisions and alternatives

| Decision | Why | Alternative / trade-off |
|---|---|---|
| Adapt BrewForm rather than rebuild immediately | Retain an existing functional starting point | Inherits upstream technical debt; requires ongoing license and change reviews |
| React + TypeScript / Hono API | Preserve compatible frontend and service boundaries | A Laravel rewrite might standardize another portfolio stack but adds migration cost without demonstrated need |
| Shared contracts + Zod | Reduce API/client interpretation drift | Requires discipline to keep contracts and runtime validation aligned |
| PostgreSQL + Drizzle | Structured relational domain and versioned schema changes | ORM convenience does not replace migration and data-impact review |
| Separate development/test and deployment environments | Protect historical data and improve repeatability | Additional operational configuration |
| Container-based GCP deployment plan | Predictable packaging and operational ownership | VM and container patching, backup/restore and monitoring remain operational responsibilities |
| Explicit upstream contribution boundary | Prevent accidental disclosure of proprietary adaptations | More work to isolate general-purpose contributions |

These are decisions reflected in the internal architectural documentation; this public case does not assert comparative performance benchmarks.

## 8. Security and privacy

API roles/authorization, session handling, secret separation, data preservation and test-DB isolation require independently verified runtime controls. A display name is not proof of administrative authorization. The documented strategy separates development services from deployment services and discourages destructive database operations.

**Open privacy debt:** internal source-of-truth documentation flags registration-consent auditability and the distinction between a cookie-choice notice and actual optional-tracker blocking. These must not be represented as resolved without implementation and test evidence. The exact security implementation is deliberately omitted here.

## 9. Delivery and operations

DCP Flow provides context-based engineering governance, short-lived branches, targeted quality gates and human acceptance. The private project documents a GCP Compute Engine deployment design using a reverse proxy, containers, application services, PostgreSQL and persistent media. Its runbook covers configuration, restoration and health-check procedures.

A deployment guide is **a plan and reproducibility aid**, not evidence that deployment, restore, monitoring or incident recovery has been successfully executed on GCP.

## 10. AI-assisted engineering and governance

AI-assisted development may support discovery, code changes, testing and documentation, but project rules assign final decisions, evidence interpretation, license checks and promotion approval to human review. Upstream contribution branches must be independent of SipDolce code/assets and reviewed before external publication.

## 11. Evidence and validation

See [Evidence register](EVIDENCE.md). Current supported classification: **architecture documented / deployment prepared**. Prototype and local engineering work are described in the private source. The public evidence reviewed here does **not** establish a controlled external pilot, successful GCP deployment, tested backup restoration or sustained production operation.

## 12. Results

The concrete outcome is a documented product-specific architecture and an operational deployment procedure. No verified uptime, adoption, latency, security-assurance or commercial impact metric is claimed.

## 13. Lessons learned

- Adapting upstream code requires explicit IP, branding and contribution boundaries.
- Data conservation and isolated tests matter as much as the frontend redesign.
- Documentation and test gates should distinguish intent, implementation and observed results.
- A finished deployment guide is an engineering milestone, not a production-success certificate.
- Content/image licensing needs its own evidence register; the upstream software license does not cover all media.

## 14. Unresolved questions

1. What GCP deployment SHA and first successful operational smoke test will be accepted?
2. What backup **restore** evidence can be safely published?
3. Which signup-consent and optional-tracker controls have passing runtime tests?
4. Are all published editorial images authorized with preserved provenance and required attribution?
5. When and how will updates from upstream BrewForm be evaluated?
6. What monitoring/incident and long-term usage evidence will support the next evidence level?

## Publication note

This text is a proposed sanitized case. No product source code, private infrastructure values, personal information, internal file paths, secrets, customer records or detailed implementation of sensitive controls are reproduced. A human sanitization and evidence review is required before merging it into the public portfolio.
