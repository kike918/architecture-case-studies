# GitHub Portfolio — Corrective Documentation Audit (2026-11-09)

**Scope:** `digitalconsultingplus/.github`, `kike918/kike918`, and `kike918/architecture-case-studies`. Product repositories were consulted **read-only** for dated evidence; no product source, pipelines or deployment environments were changed.

**Method:** GitHub `main` trees and Markdown content; existence resolution for relative file links; targeted cross-language consistency checks; dated product documentation comparisons; secret-pattern search. Externally hosted sites are reported separately. This is **not** a live security penetration test, full history secret scan, CI rerun, legal assessment or uptime certification.

## Corrective changes

1. MicroPOS Catalan README/evidence now distinguish the documented commercial Astro/PHP/SQLite website and CRM from the proposed Raspberry Pi offline-first edge POS, matching EN/ES.
2. MicroPOS EN/ES/CA document actual constraints, security boundaries, alternatives, trade-offs, outstanding pilot evidence and mappings to the publication standard.
3. DCP Flow EN/ES explicitly classify as a methodology case with product maturity **N/A**, and map the publication topics.
4. The publication standard preserves five canonical product maturity labels; "deployment prepared" and "documented architecture" remain qualifiers, not invented evidence levels.
5. The public EN/ES index now shows **eight published cases together**, with technical maturity separated from editorial publication.

## Post-correction audit matrix

| Control | Result | Basis / limitation |
|---|---|---|
| Scope isolation | PASS | Only public documentation in authorized repos is changed |
| Case inventory | PASS | Eight published case folders and EN/ES public entries |
| EN/ES/CA MicroPOS claim parity | PASS (document review) | README and evidence register distinguish commercial/edge tracks in all three languages |
| Methodology evidence taxonomy | PASS (document review) | DCP Flow product maturity N/A, adoption evidence bounded |
| Relative-link target resolution | PASS (static) | First full pass: 104 Markdown files, 218 relative links, zero missing targets; final changed paths rechecked separately |
| Credential-pattern scan | PASS (limited) | No matches for selected token/private-key/path patterns in the scanned Markdown; not a Git-history or binary scan |
| External links and live websites | PARTIAL | Public SipDolce Labs and MicroPOS pages retrieved; Rewi and DCP Flow not accessible to the web verifier; cannot infer outages |
| Markdown anchor fragments, rendering and automated lint | NOT RUN | Target-resolution scan does not parse headings, Markdown rendering or anchors |
| CI/runtime, restoration and security validation of product apps | NOT RUN | Not in documentation audit scope |
| Corporate `.github` `dev` sync and obsolete branches | REQUIRES SEPARATE GIT CHECK | See below; clean only verified merged branches, never assume diverged status means missing work |

## Evidence maturity, not release certification

| Case | Editorial status | Technical evidence boundary |
|---|---|---|
| FalconCDT Engagement | Published | Deployment evidence documented; no universal sustained validation claim |
| DCP DownloadGate | Published | Deployed use case documented; no private details exposed |
| MicroPOS | Published | Commercial web/mini CRM documented; edge POS Concept and unexecuted pilot |
| Normia | Published | Baseline and prototype/technical bootstrap; development paused |
| Rewi v0.2.1 | Published | Deployed 2026-11-03 documented; sustained validation and real PROD restore not established |
| Tazario Recipes | Published | Architecture/implementation documented; GCP deployment prepared, not verified |
| DCP Flow | Published | Methodology N/A on product maturity; selected applications documented, effects not quantified |
| SipDolce Labs | Published | v1 public deployment documented; later `dev` editorial changes not promoted at review cut |

## Governance follow-up

The corporate `.github` `dev` branch was observed six commits behind `main` in the initial audit. Confirm whether it is an actively maintained integration branch and reconcile by **fast-forward only** if it has no unique commits. Several historical `docs/*` branches from squash-merged PRs remain on remote repositories; a diverged comparison alone cannot justify deletion. Branch deletion requires individual PR/ref checks and is not a prerequisite for truthful public case content.

## Verification rule

Every substantive claim remains bound to the source's date and actual evidence. An application being publicly reachable or a CI job reporting PASS is not, by itself, proof of sustained production validation. Future updates must change the case/evidence register only when new verified release, pilot, restore or usage evidence exists.
