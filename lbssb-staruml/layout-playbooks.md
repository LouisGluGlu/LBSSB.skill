# Layout Playbooks

These playbooks define human-like layout strategy before MCP drawing.

## General Method

1. Build `DiagramPlan`: elements and relationships.
2. Build `LayoutPlan`: zones, lanes, anchor points, expected line routes.
3. Draw a pilot diagram or the highest-risk diagram first.
4. Export PNG and inspect visually.
5. Repair locally using move/resize/edge routing.
6. Reuse the proven layout pattern for the remaining diagrams.

Do not batch-generate every diagram before seeing one exported result.

## Use Case Layout

Use zones:

- left/right margins: actors;
- center: main business use cases;
- inner secondary ring: included use cases;
- lower or side area: optional/extend use cases;
- boundary rectangle: system scope.

For single-actor diagrams, group by business module:

- account;
- order;
- borrow/return;
- teacher appointment;
- evaluation/ranking.

Actor lines should connect to module entry use cases. Shared includes stay close to the base use case.

## Class Layout

Recommended zones:

- top: role/user inheritance;
- center: core domain trunk;
- left: order and borrowing aggregates;
- right: teacher appointment aggregate;
- bottom: payment/evaluation/support objects;
- edges: service/repository/gateway when needed.

Procedure:

1. Place classes by zone.
2. Size boxes based on attributes and operations.
3. Draw inheritance first.
4. Draw short aggregate/composition relations.
5. Draw cross-aggregate associations.
6. Add multiplicity labels.
7. Add dependencies only if they clarify architecture.

Avoid global layout after step 1 unless it is followed by a full local repair pass.

## State Layout

Use lifecycle rows or columns:

- initial state;
- normal active states;
- blocked/exception states;
- terminal states.

Keep transition labels short:

- good: `publish`, `full`, `cancel`, `timeout`;
- bad: `教师关闭或时间截止后系统处理所有预约`.

If Chinese labels are long, expand state boxes and route transition labels away from nodes.

## Sequence Layout

Use stable participant order:

```text
Actor -> Boundary/Page -> Controller/Service -> Repository/Gateway -> DB/External
```

Keep lifeline gap wide enough for Chinese names.
Use fragments for branches. Do not encode all business logic as free-floating message text.

## Repair Priority

Repair in this order:

1. clipped text;
2. line-through-label defects;
3. unreadable actor or class relationships;
4. missing grouping/layering;
5. excess decorative detail.
