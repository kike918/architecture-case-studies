# MicroPOS — ERP Integration Strategy

## Principle

MicroPOS is an operational POS core with adapters to external back-office systems.

```text
MicroPOS Core
      │
      ├── Odoo Adapter
      ├── Dolibarr Adapter
      ├── CSV Import / Export
      └── API / Webhooks
```

## Odoo role

Use Odoo when the customer needs broader ERP depth such as integrated inventory, accounting, CRM, purchasing, manufacturing or established Odoo processes.

The adapter should synchronize only explicit contracts such as:

- products;
- customers;
- sales;
- payments;
- stock movements where appropriate.

## Dolibarr role

Use Dolibarr where a lighter back-office footprint is more appropriate and the customer needs simpler customer, product, sales and administrative workflows.

## Integration rules

- local sale completion never depends on ERP response;
- synchronization is asynchronous;
- adapters are idempotent;
- mappings are explicit and versioned;
- reconciliation reports are available;
- source ownership is defined per entity;
- ERP outage must not stop local POS operation.

## Recommended evolution

```text
1. CSV contract tests
2. API contract prototype
3. Dolibarr adapter pilot
4. Odoo adapter pilot
5. Reconciliation tooling
6. Customer-specific mapping profiles
```

The lighter integration should be validated first before increasing complexity.
