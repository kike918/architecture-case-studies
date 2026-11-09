# Tazario Recipes — Evidence Register

**Review cut:** 2026-11-08. **Publication status:** published with human disclosure approval (2026-11-09); technical evidence gates remain open.

| Claim | Evidence basis reviewed | Classification | Limit |
|---|---|---|---|
| Specialty-coffee product adapted from BrewForm | Private Tazario README, system map, third-party notices | Documented architecture | MIT notice must remain; does not grant rights to all third-party media |
| React/Vite, Hono, Drizzle and PostgreSQL component boundaries | Private system map and project README | Documented implementation design | This public register does not reproduce proprietary implementation or independent test logs |
| Data preservation and isolated test strategy | Private governance, definition of done and deployment guide | Documented controls/intent | Do not infer that every control has been exercised on the current release |
| Containerized GCP deployment architecture | Private GCP Compute Engine runbook and production Compose references | Deployment prepared | No observed GCP release, live health result or production usage verified in this review |
| Upstream isolation | Private source-of-truth and contribution governance | Documented policy | No blanket assertion that every historical contribution has been audited |
| Privacy and cookie consent | Private source-of-truth | Open issue | Implementation/tests must establish resolution |
| Photo rights and attribution | Private third-party notices and referenced editorial registry | Documented licensing process | Individual asset permission review remains necessary |

## Promotion gates

- [x] Human disclosure/sanitization approval (2026-11-09).
- [ ] Verify all public claims against a specific product Git SHA and executed QA evidence.
- [ ] Confirm consent and optional-tracker issues, or explicitly accept documented risk before a relevant release.
- [ ] Verify media provenance/attribution for assets distributed publicly.
- [ ] Record GCP deployment SHA, health checks and operational acceptance before changing status to **Deployed**.
- [ ] Obtain real backup-restore and sustained operations evidence before asserting **Production validated**.

**Not evidence:** planned commands, illustrative diagrams, deployment procedures, marketing claims, or unexecuted checklists.
