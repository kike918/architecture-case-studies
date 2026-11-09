# DCP Flow — Architecture of a Human + AI Engineering Method

🌐 **Languages:** English · [Español](README.es.md)

**Status:** Published sanitized methodology/engineering-governance case. **Evidence classification:** Documented and applied method with selected reference-project evidence; not a claim of universal adoption, independent certification or measured productivity improvement.

## Evidence taxonomy and publication-standard coverage

DCP Flow is a **methodology case**, so product maturity is **N/A**, not Deployed or Production validated. Its engineering-system design is documented and selected historical applications are described; the evidence does not quantify productivity gains.

**Fourteen-topic map:** context/problem (§2), constraints (§3), drivers (§4), boundaries and architecture (§5), key decisions/alternatives/trade-offs (§6), delivery/operations (§7), security/privacy (§8), evidence (§10 and [register](EVIDENCE.md)), lessons (§11), open questions (§12). This explicitly provides a methodology-specific alternative to a product release diagram.

## 1. Executive summary

DCP Flow is Digital Consulting Plus's versioned method for moving from a business problem to a reviewed, evidence-backed outcome while retaining engineering knowledge. Its **Engineering System** implements the technical side through cross-project standards, context-specific blueprints, reusable skills, quality gates, decision records and repository governance. Kai can interpret and operate this method but is not an independent authority.

This is a case study about the **architecture of an engineering method**, not a deployed SaaS product. Its governance design is documented; selected implementation practices have been exercised in different products, with evidence limits set by each project.

## 2. Context and problem

AI-assisted delivery can accelerate writing code while making architectural drift, non-reproducible claims and accidental mixing of incompatible technology assumptions more likely. A small organization operating business SaaS, content-first sites, fullstack TypeScript apps and ERP integrations needs reusable rules without imposing one runtime on every project.

The problem is to make technology and build-vs-reuse decisions traceable, align AI agents with the project's actual context, select risk-proportionate tests and retain human accountability for sensitive changes.

## 3. Constraints

- Different products require different domain, runtime, hosting and regulatory boundaries.
- Existing products, especially open source, must be evaluated before custom construction.
- Project truth, actual Git refs and executed tests outweigh summaries and unexecuted plans.
- Versioned documentation must distinguish normative rules from explanatory handbooks.
- Automated assistance cannot silently authorize merges, security-sensitive operations or production releases.
- Skills are contextual execution guidance, not universally applicable commands.
- Operational evidence and maintained documentation must remain affordable for a small team.

## 4. Architectural drivers

**Governance coherence, traceability, reproducibility, maintainability, contextual relevance, change safety and human accountability.**

## 5. System boundaries and authority

```text
                   Human-approved intent
                           |
                     DCP Flow method
                           |
                  Constitution / Standards
                           |
                Selected Stack Blueprint
                 + runtime/deploy profile
                           |
                 Project truth + accepted ADRs
                           |
              Eligible Skills and tool guidance
                           |
                 Implementation and evidence
                           |
                 Risk-based Quality Gates
                           |
                    Human acceptance
                           |
              Versioned learning and evolution
```

This logical model describes **decision authority**, not private execution infrastructure. The Human Handbook and public microsite explain the method but are **non-normative** projections; neither can supersede canonical standards. The tool/MCP registry informs selection, but listing a tool grants no permission to use it.

## 6. Key decisions and alternatives

| Decision | Rationale | Alternative and trade-off |
|---|---|---|
| One overarching method | Prevent competing governance systems | Separate frameworks by team could increase ambiguity |
| Solution Discovery Gate before material build | Avoid recreating mature capabilities | Always-build is initially convenient but increases cost and maintenance |
| ADOPT / CONFIGURE / INTEGRATE / EXTEND / BUILD | Document an evaluated path, not a code-first preference | Mechanical selection without evaluation would miss context and risk |
| Stack-specific blueprints | Preserve native Laravel, Astro, TypeScript and ERP conventions | A universal template encourages cross-stack leakage |
| Provider target after stack choice | GCP or hosting type does not determine application architecture | Provider-first selection can overfit infrastructure choices |
| Context-qualified skills | Only load instructions relevant to the chosen task/runtime | Loading all skills adds noise and contradictory assumptions |
| Evidence-based risk gates | Match tests and reviews to failure impact | Fixed checklists may give false assurance or unnecessary work |
| Human release gate | Keep accountability for real-world consequences | Unsupervised promotion is faster but lacks appropriate authority |

## 7. Delivery and operations model

A canonical routing sequence is problem → discovery/solution assessment → product classification → blueprint and runtime → project-specific context → minimum eligible skills → implementation → risk-proportionate checks → evidence/PR → human decision. Normal repository governance separates feature branches, integration and accepted release baselines.

Quality gates record **PASS / FAIL / NOT RUN / NOT APPLICABLE / BLOCKED**; a missing test cannot be reported as PASS. Review verdicts express readiness for a **human** decision, not permission to merge or deploy automatically.

Different environments use distinct runtime and provider profiles. A TypeScript dependency inside Laravel or a small React island inside Astro does not reclassify the host product.

## 8. Security, privacy and AI governance

The source documentation includes risk-driven attention to authorization, secrets, data migrations, supply-chain concerns, runtime safety, and evidence. Human approval is required for material or sensitive actions. The public case intentionally does not expose private agent credentials, server inventories or operational access paths.

Documented controls must not be confused with universal technical enforcement. Repository protection and agent behavior depend on the actual platform permissions and execution setup.

## 9. AI-assisted engineering

AI tools may help explore options, draft changes, run checks and summarize evidence. Their authority is scoped to the approved task and selected blueprint. Kai acts as an orchestrator within DCP Flow; it does not replace canonical decisions or human acceptance. Skills are reusable knowledge units governed by standards, not a separate method.

## 10. Evidence and validation

See [Evidence register](EVIDENCE.md). Canonical documentation supports the methodology taxonomy, blueprint catalogue, solution-discovery sequence and gate definitions. Historical reference records include Laravel SaaS, lightweight PHP and Astro delivery contexts, with explicit limits. The TypeScript application blueprint remains **EVOLVING** pending further reproducibility, CI and release evidence.

This does not establish measured improvements to lead time, defect rates, cost, or organization-wide compliance.

## 11. Results and lessons

- A single method can support multiple stacks **without merging their technical rules**.
- Reuse decisions should precede implementation to limit avoidable custom work.
- Documentation must separate what is required, what is implemented and what was observed.
- A green-looking checklist has little meaning if critical gates were not run.
- Public learning surfaces should describe canonical knowledge, not become competing sources of authority.

## 12. Unresolved questions

1. Which comparative metrics can demonstrate improved time-to-value and lower defect escape?
2. Which blueprints have sufficient repeatable release evidence to advance from EVOLVING?
3. How frequently should catalogs and links be reconciled with real project experience?
4. What minimum evidence is appropriate for differently sized projects?
5. How can automated compliance checks supplement—not replace—human review?

## Publication note

This case explains a documented engineering method and its selected historical applications. No private source, customer data, secrets, or internal infrastructure records are reproduced. See the canonical public [DCP Flow documentation](https://dcpflow.digitalconsultingplus.co/) for current published guidance.
