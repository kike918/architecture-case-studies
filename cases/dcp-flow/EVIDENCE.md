# DCP Flow — Evidence Register

**Review date:** 2026-11-09. **Type:** Methodology/governance case (not a product deployment). **Evidence:** documented method and selected historical project references.

| Claim | Canonical read-only source | Status and limits |
|---|---|---|
| DCP Flow is one method; Engineering System is its technical layer | `dcp-flow/README.md` and `DOCUMENTATION.es.md` | Documented normative structure; not a second framework |
| Evaluate before custom build | `standards/solution-discovery-gate.es.md` | Standard marked EVOLVING; ADOPT/CONFIGURE/INTEGRATE/EXTEND/BUILD governed there |
| Context-sensitive quality gates | `standards/quality-gates.es.md` | Risk/evidence model documented; checks are not automatically executed everywhere |
| Separation of stacks | `blueprints/README.es.md`, `ai/skills/routing.es.md` | Laravel, Astro/Web, Fullstack TypeScript and ERP blueprints; eligible skills only |
| TypeScript maturity | `blueprints/fullstack-typescript/README.es.md` | EVOLVING, not a universal or fully validated default |
| Documented historical reuse and learning | `ai/reference-evidence/2026-10-12-cross-project-experience.md` | Dated reference, not proof of current production behavior or quantified benefits |
| Non-normative public presentation | `dcp-flow-docs/README.md` | Public microsite curates guidance; it does not override canonical methodology |

## Evidence gates for future improvements

- [x] Canonical structural and policy sources inspected.
- [x] English/Spanish case with explicitly scoped claims.
- [ ] Independently measure lead time, escaped defects, operational cost and reuse.
- [ ] Verify individual product/release gates before attributing outcomes.
- [ ] Periodically review cross-language and public-site parity.

**Important:** the five standard case evidence levels (Concept/Prototype/Pilot/Deployed/Production validated) describe product/system maturity; this method case must not be labelled `Production validated` merely because some projects using it are deployed.
