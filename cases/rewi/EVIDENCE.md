# Rewi v0.2.1 — Public Evidence Register

**Cut-off:** 2026-11-09. **Evidence classification:** Deployed; **not** Production validated.

| Claim | Private source reviewed (read-only) | Observed/documented evidence | Limitation |
|---|---|---|---|
| v0.2.1 application deployed | Product release notes `docs/releases/v0.2.1.md`; operational checkpoint `ai/CURRENT_STATE.md` | Production deployment documented for 2026-11-03 | Documentation snapshot, not an independent real-time audit |
| Basic operational health | Same release notes | Application healthy, health endpoint HTTP 200; workers and scheduler started | Does not imply sustained uptime or full workflow coverage |
| Campaign-image support | Same release notes | Media path corrected, public JPEG HTTP 200 and browser visibility confirmed | Does not certify every media type, user role or campaign |
| Database and deployment changes | Same release notes | Image-related additive migration recorded as applied; image build PASS | No blanket claim of end-to-end regression across all flows |
| Backup integrity | Same release notes | Backup artifacts, generation and size checks documented | **No real production restore test evidenced** |
| Integration and tenancy architecture | Private `docs/integrations/API.md` | Documented scope-separated API contracts, business-derived identity, bounded reads and idempotency | Contract presence does not prove every provider is configured or operating |
| Engineering governance | Private project documentation and DCP Flow | Release acceptance and historical check evidence | Historical PASS on other SHAs is not a PASS for the entire production release |

## Promotion criteria

- [x] Deployed status backed by dated internal release evidence.
- [ ] Sustained production measurements and meaningful user-operation evidence.
- [ ] Documented production restore exercise.
- [ ] Exact-release regression and provider delivery evidence for claims requiring it.
- [ ] Independent privacy/security compliance review before asserting certification.

**Editorial rule:** historical NO-GO statements in the product's root README are superseded by the later operational checkpoint; they must not be recast as current blockers. No changes were made to the private product repository.
