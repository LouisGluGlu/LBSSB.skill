# Diagram Patterns

## Common DiagramPlan Fields

Each diagram entry should include:

```yaml
type: "usecase | class | sequence | communication | activity | state | component | deployment"
title: ""
filename: ""
source_requirement: ""
business_goal: ""
elements: []
relations: []
layout:
  orientation: ""
  lanes: []
  zones: []
  anchors: []
  edge_routing: ""
quality_notes: []
```

## Use Case

Express external actors and system services. Use business verb phrases. Keep system boundary clear. Use `include` for mandatory reused behavior and `extend` for optional/conditional behavior.

Before drawing, group use cases by module/responsibility. Do not fill use cases by raw grid order. Actor lines should connect to main use cases; include/extend use cases should sit near their base use cases.

Recommended zones:

- actors: left/right outside boundary;
- main use cases: center by module;
- included use cases: near base use cases;
- optional/extend use cases: side or lower edge;
- external systems: opposite side from primary actor.

## Class

Express stable structure: roles, domain entities, aggregates, and necessary support classes. Load `class-diagram-rules.md`.

If a source `.mdj` exists, preserve existing class, attribute, and operation naming. Do not translate English identifiers by default.

## Sequence

Express one scenario over time. Preferred participant chain:

```text
Actor -> Page/Boundary -> Controller -> Service -> Repository -> DB
```

Use `alt/else` for branches and dashed arrows for returns.

Mermaid generation may create a draft, but final diagrams require visual review of participant spacing, message order, branch frames, and header width.

## Communication

Express object collaboration for one scenario. Use the same objects as the matching sequence diagram when possible. Number messages continuously: `1`, `1.1`, `1.2`, `2`.

## Activity

Express workflow and decisions. Parallel or alternative user operations must be branches, not a fake serial chain. Every decision needs conditions.

## State

Express lifecycle of one object. State names are durable conditions, not operation names. Transitions require events or guards.

Keep transition labels short. Long Chinese transition text must be shortened, moved to notes, or documented outside the diagram. Resize state nodes before export.

## Component

Express deployable or logical modules/services and provided/required interfaces. Components are modules, services, adapters, databases, or external systems; not buttons or page fields.

## Deployment

Express runtime nodes and deployed artifacts. Nodes are environments, devices, containers, servers, clients, or networks; not entity classes.
