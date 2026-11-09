# SipDolce Labs — CoffeeTech Editorial Platform Architecture

🌐 **Languages:** English · [Español](README.es.md)

**Status:** Published sanitized architecture case. **Evidence:** v1 website deployment documented on Hostinger; subsequent editorial/portfolio changes integrated in `dev` and **not yet promoted to a new production release** at the 2026-11-09 review. The public website and the latest integration branch are different release states.

## 1. Executive summary
SipDolce Labs is a bilingual public editorial and research-oriented website covering coffee science, CoffeeTech and related experimentation. Its architecture deliberately avoids treating an editorial website as a SaaS, ERP, recipe engine or online store. A static Astro/TypeScript frontend publishes curated content while a bounded PHP/SQLite companion processes contact, newsletter and collaboration requests.

## 2. Context and problem
An evolving coffee-knowledge platform must add recipes, media, projects and scientific content without rebuilding screens for every entry. At the same time, user submissions need durable handling, rights and provenance require editorial review, and illustrative mockups must never be presented as achieved results.

## 3. Constraints
- Bilingual ES/EN content and stable URLs.
- Cost-conscious shared hosting and small-team operations.
- Preserve the existing design and TypeScript catalogs.
- Separate public static pages from private transactional data.
- Keep logos and licensed assets distinct from conceptual mockups.
- Avoid publishing unverified scientific, commercial or legal claims.
- Versioned releases, human approval and rollback capability.

## 4. Architectural drivers
**Simplicity, editorial throughput, accessibility, privacy, reproducibility, provenance and low operational overhead.**

## 5. System boundaries
Inside the editorial website: static pages, templates, typed catalogs, language content, SEO metadata and assets. A separate companion handles form submission persistence and queued external integration events. Outside the website: the independent Tazario Recipes product, prospective podcast platforms, media providers, research sources and third-party rights holders.

## 6. Sanitized architecture
```text
            Editors / reviewed content
                       |
          Typed ES/EN editorial records
                       |
           Astro SSG build (TypeScript)
                       |
       Static pages + SEO + approved media
                       |
                Public browser
                       |
           Form and proposal submissions
                       |
             Bounded PHP companion
                 |           |
          Private SQLite   Integration outbox
                               |
                        External services
```
This logical model omits hosting paths, API route details, secrets and private deployment topology.

## 7. Key decisions and trade-offs
| Decision | Reason | Alternative / limitation |
|---|---|---|
| Astro static-first | Fast, low-maintenance content delivery | Content changes require review and rebuild |
| Typed TypeScript catalogs | Existing editorial data and templates already work | Non-technical concurrent editing remains more cumbersome |
| Preserve templates and stable slugs | Reduce unnecessary rewrite and broken URLs | Schema and bilingual parity need ongoing validation |
| PHP + private SQLite for submissions | Durable transactional intake on existing shared hosting | Requires backup discipline, controlled storage and operational ownership |
| Asynchronous integration outbox | Decouple intake persistence from external delivery | Retries and delivery evidence remain operational concerns |
| No immediate CMS or editorial database | Avoid duplicated data models and administrative attack surface | Reassess when measured editing volume/permissions justify it |
| Separate Tazario Recipes | Protect product boundaries and independent deployment lifecycles | Future integration needs its own contract and review |

## 8. Alternatives considered
Markdown Content Collections exist as a schema capability but are **not** the active source for existing catalogs. A CMS, a relational editorial database or a broader application rewrite would add migration and maintenance costs without a demonstrated need. Independent tools for recipes, podcasts and videos are research candidates, **not automatically deployed integrations**.

## 9. Security, privacy and rights
The source architecture describes private transactional storage outside the public static artifact, controlled form handling, consent-related analytics work and a review policy for legal content and media provenance. Documentation of a control is not a comprehensive security or legal certification. Original brand assets are distinguished from concept mockups; rights for externally sourced images and scientific claims need case-by-case verification.

## 10. Delivery and operations
DCP Flow governs short-lived branches, review, risk-based tests, release approval and deployment. The documented release flow builds a static artifact, preserves transactional data, deploys to shared hosting, checks public functionality and retains rollback options. An earlier v1 public release is recorded as closed. The later SLL-WEB-01 CoffeeTech portfolio changes are recorded as integrated into `dev`, **not yet released to production**.

## 11. AI-assisted delivery
AI may help draft or structure bilingual content, suggest edits and check consistency, but factual accuracy, brand identity, rights, publishing approvals and release responsibility remain human. A concept image is a design reference, not evidence of a completed event or product.

## 12. Evidence and validation
See [Evidence register](EVIDENCE.md). The 2026-11-09 source checkpoint reports a completed v1 public release, an Astro static build of 138 pages, backend test evidence and separate subsequent changes in development. These figures are historical source-reported results, **not independently rerun in this public documentation review**.

## 13. Outcomes and lessons
The architectural result is an editorial platform with an intentionally bounded transactional companion, not an unnecessary custom CMS. Separating content editing from integration persistence reduces coupling. Keeping TypeScript-first publishing is a deliberate, reversible decision conditioned on measured editorial needs. A released website and unpromoted branch changes must be reported separately.

## 14. Unresolved questions
1. What commit and public smoke evidence will confirm the next Hostinger release?
2. Which content workflows warrant new editorial tools, if measured volume increases?
3. Which media and research references need independent provenance or licensing verification?
4. Which accessibility, privacy and consent flows have independently verified coverage?
5. When would a documented API integration to Tazario Recipes be preferable to a static reference?

## Publication note
Sanitized case based on read-only technical documentation. No private source, secrets, internal infrastructure paths, customer submissions or unapproved media are reproduced.
