# Case Study Template

## 1. Executive summary

State the problem, the architectural response and the current evidence level in plain language.

## 2. Context

Describe the business environment, users, operational model and relevant constraints.

## 3. Problem

Define the problem being solved. Avoid framing the problem as a technology choice.

## 4. Constraints

Document the real constraints, for example:

- connectivity;
- cost;
- team size;
- legacy systems;
- privacy;
- hardware limitations;
- delivery deadlines;
- operational complexity.

## 5. Architectural drivers

List the qualities that drive the architecture, such as:

- reliability;
- offline capability;
- maintainability;
- auditability;
- latency;
- cost control;
- deployment simplicity;
- interoperability.

## 6. System boundaries

Explain what is inside the system, what is external and where responsibilities are intentionally separated.

## 7. Architecture overview

Include a sanitized diagram and describe the main components, data flows and trust boundaries.

## 8. Key decisions

For every major decision, explain:

- decision;
- why;
- alternatives considered;
- trade-offs;
- reversal cost.

Link public ADRs when useful.

## 9. Security and privacy

Cover:

- authentication and authorization boundaries;
- sensitive data handling;
- secrets management principles;
- logging and audit concerns;
- public/private data separation;
- threat considerations relevant to the case.

## 10. Delivery and operations

Describe:

- development workflow;
- deployment model;
- observability;
- failure handling;
- update strategy;
- operational ownership.

## 11. AI-assisted development

When applicable, document:

- AI tools used;
- scope delegated;
- human review performed;
- tests executed;
- validation method.

Do not imply autonomous production approval.

## 12. Evidence and validation

Classify claims using explicit evidence:

- concept;
- prototype;
- pilot;
- deployed;
- production validated.

Include only public-safe evidence.

## 13. Results

Report measurable results only when evidence exists. Otherwise describe current validation status without inventing outcomes.

## 14. Lessons learned

Document what worked, what did not, what changed and what would be done differently.

## 15. Next architectural questions

List unresolved decisions and conditions that would trigger architecture evolution.

## Publication checklist

- [ ] No credentials, tokens or secrets.
- [ ] No production endpoints that should remain private.
- [ ] No personal data.
- [ ] No confidential client data.
- [ ] No proprietary source code copied from private repositories.
- [ ] Claims match evidence level.
- [ ] Diagrams are sanitized.
- [ ] Trade-offs are documented.
- [ ] Status is explicit.
- [ ] Client references are authorized or anonymized.
