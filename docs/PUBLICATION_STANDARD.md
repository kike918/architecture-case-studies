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
