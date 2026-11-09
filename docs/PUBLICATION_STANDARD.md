# Publication Standard

## Purpose

Define the minimum quality bar for architecture case studies published in this repository.

## Required sections

Every published case must include:

1. context;
2. problem;
3. constraints;
4. architectural drivers;
5. system boundaries;
6. architecture overview;
7. key decisions;
8. alternatives considered;
9. trade-offs;
10. security and privacy considerations;
11. delivery/operations model;
12. evidence level;
13. lessons learned;
14. unresolved questions.

## Evidence labels

Use one of these labels explicitly:

- **Concept** — idea or architecture proposal, not implemented.
- **Prototype** — limited technical or UX validation.
- **Pilot** — tested with a real operating context or controlled user group.
- **Deployed** — running in a real environment.
- **Production validated** — operating with sustained real usage and evidence.

A case may contain components at different evidence levels. State this clearly.

## Writing standard

Good case studies explain why a decision was made under specific constraints.

Avoid:

- generic technology lists;
- architecture diagrams without decisions;
- inflated claims;
- vendor hype;
- invented metrics;
- hidden assumptions;
- presenting roadmaps as delivered outcomes.

## Diagram standard

Every diagram should:

- have a title;
- show system boundaries;
- distinguish internal and external systems;
- make primary data flows understandable;
- avoid private infrastructure details;
- avoid credentials, hostnames or sensitive topology.

## Review gate

Before publication:

```text
Evidence review
      ↓
Sanitization review
      ↓
Architecture review
      ↓
Language clarity review
      ↓
Publish
```

## Update policy

Published cases should be updated when:

- architecture materially changes;
- evidence level improves;
- a prior claim becomes inaccurate;
- a major decision is superseded;
- new lessons materially change the interpretation of the case.


## Applying evidence levels across composite and methodological cases

The five product/system evidence labels above are **the only maturity levels**. Phrases such as *documented baseline*, *deployment prepared*, *implementation documented* or *pilot planned* are **qualifiers**, not additional evidence levels.

- Assign a canonical level to each materially different system boundary when a case spans multiple tracks (e.g. commercial website vs. independent edge POS). A planned architecture is **Concept**, even if implementation is intended.
- `Deployed` requires dated evidence of a release in a real environment; this is narrower than `Production validated`, which requires sustained operating evidence.
- A deployment runbook or prepared infrastructure alone does not prove deployment.
- Methodology or governance cases (for example DCP Flow) are **non-product cases**. Mark them **Methodology / Not applicable** for product maturity and document adoption examples and evidence limitations. Do not invent a `Deployed` or `Production validated` status for the method based on products that use it.
- Keep editorial publication status (**Published**, **Draft**) separate from technical maturity. A published case can still describe an unbuilt **Concept**.

## Compliance mapping and evidence register

A case does **not** need fourteen numbered headers, but each of the fourteen required topics must be identifiable in its main README **or** an explicitly linked companion document. Every published case should contain a short mapping, or clearly named headings, that allow a reviewer to identify all required topics without inference.

For composite products, record the implementation track and the planned track separately in the evidence register. Where evidence is historical, identify its date or source and do not claim live verification.

## Case inventory and language parity

The public index must list all published cases together. Reserve a separate area for actual unpublished candidates. Case material may be bilingual EN/ES; if a case already provides a Catalan README/evidence register, maintain **material claim parity** across EN/ES/CA when updating implementation status or maturity. Translations do not require identical wording, but must not disagree on what is shipped or validated.
