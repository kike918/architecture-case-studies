# MicroPOS — Registre d’Evidència

## Propòsit

Separar decisions arquitectòniques d’evidència de laboratori, pilot i futures afirmacions de producte.

## Escala

- **Baseline documentat** — direcció aprovada per a implementació.
- **Laboratori planificat** — validació hardware/software definida però no executada.
- **Prototip** — implementació experimental.
- **Pilot pendent** — requereix ús real.
- **Pilot validat** — ús controlat completat.
- **Validat en producció** — no reclamat actualment.

## Matriu

| Capacitat | Nivell |
|---|---|
| Arquitectura edge/offline-first | Baseline documentat |
| Node Raspberry Pi | Laboratori planificat |
| Venda local | Abast MVP del pilot |
| Persistència local | Baseline documentat |
| Transactional outbox | Baseline documentat |
| Sync idempotent | Baseline documentat |
| Impressió | Laboratori/pilot pendent |
| Caixa | Abast MVP |
| Inventari mínim | Abast MVP |
| Scripts de backup | Implementació planificada |
| Scripts de diagnòstic | Implementació planificada |
| Adapter Dolibarr | Prototip planificat |
| Adapter Odoo | Prototip planificat |
| n8n | Rol arquitectònic definit |
| Pilot negoci simple | Planificat |
| Pilot operació complexa | Fase posterior |
| Validació productiva | No reclamada |

## Evidència requerida

Abans d’afirmar maduresa s’ha de demostrar venda sense Internet, commit local durable, recuperació després de reinici, sincronització sense duplicats, backlog visible, backup i restore exitosos, impressió estable, diagnòstic útil i reconciliació ERP explícita.

## Disciplina d’afirmacions

No s’ha d’afirmar fiabilitat offline productiva, maduresa d’integració ERP ni estabilitat de camp de Raspberry Pi fins que es demostri.
