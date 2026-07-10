# MicroPOS — Estrategia de Integración ERP

## Principio

MicroPOS es un core operacional POS con adapters hacia sistemas de back-office.

```text
MicroPOS Core
      │
      ├── Adapter Odoo
      ├── Adapter Dolibarr
      ├── CSV Import / Export
      └── API / Webhooks
```

## Rol de Odoo

Usar Odoo cuando el cliente requiere mayor profundidad ERP: inventario integrado, contabilidad, CRM, compras, manufactura o procesos Odoo existentes.

Contratos candidatos:

- productos;
- clientes;
- ventas;
- pagos;
- movimientos de inventario cuando aplique.

## Rol de Dolibarr

Usar Dolibarr cuando sea más apropiado un back-office ligero con flujos simples de clientes, productos, ventas y administración.

## Reglas de integración

- la venta local nunca depende de la respuesta del ERP;
- sincronización asíncrona;
- adapters idempotentes;
- mappings explícitos y versionados;
- reportes de reconciliación;
- ownership por entidad claramente definido;
- caída del ERP no detiene el POS local.

## Evolución recomendada

```text
1. Contract tests CSV
2. Prototipo de contrato API
3. Piloto adapter Dolibarr
4. Piloto adapter Odoo
5. Herramientas de reconciliación
6. Perfiles de mapping por cliente
```
