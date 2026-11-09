# SipDolce Labs — Evidence Register

**Review cut:** 2026-11-09. Source project was consulted read-only.

| Claim | Read-only source | Evidence and limitation |
|---|---|---|
| v1 public website deployed | `sipdolcelabs-web@dev/README.md`, `ai/CURRENT_STATE.md` | Release v1 closed on `main`, Hostinger operational as documented; this review did not conduct live deployment testing |
| Astro + TypeScript editorial boundary | `docs/ARCHITECTURE.md`, ADR-0002 | Static SSG and typed catalog model documented; Markdown/Zod collections are not active catalog sources |
| Transactional companion | Architecture, runbook and current-state documents | PHP/SQLite WAL and outbox documented; do not infer a CMS or standalone product |
| Build and QA | `ai/CURRENT_STATE.md` | 138 static pages and 36 backend tests reported PASS at project checkpoint; not independently rerun here |
| Subsequent CoffeeTech updates | `README.md`, `ai/CURRENT_STATE.md` | SLL-WEB-01 integrated on `dev`, not promoted to new Hostinger release in reviewed checkpoint |
| Rights and legal review | `docs/ASSET_PROVENANCE.md`, `docs/LEGAL_AND_TRUST.md`, current-state | Historical documents contain earlier open legal questions; later checkpoint records entity identification resolved. Neither implies all rights/privacy reviews completed |
| Future recipes/podcast systems | ADR-0002 and current-state | Evaluation of separate services; not proof of production integration |

## Evidence gates
- [x] Separate released v1 from subsequent `dev` work.
- [x] Preserve actual TypeScript-first and PHP/SQLite boundaries.
- [ ] Verify next release SHA and live Hostinger smoke.
- [ ] Independently validate rights, legal text and accessibility where claims require them.
- [ ] Verify integrations before declaring them in production.

**Classification:** Deployed website v1 (documented); later editorial changes in development; no claim of sustained production validation.
