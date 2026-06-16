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
quality_notes: []
```

## Use Case

Express external actors and system services. Use business verb phrases. Keep system boundary clear. Use `include` for mandatory reused behavior and `extend` for optional/conditional behavior.

## Class

Express stable structure: roles, domain entities, aggregates, and necessary support classes. Load `class-diagram-rules.md`.

## Sequence

Express one scenario over time. Preferred participant chain:

```text
Actor -> Page/Boundary -> Controller -> Service -> Repository -> DB
```

Use `alt/else` for branches and dashed arrows for returns.

## Communication

Express object collaboration for one scenario. Use the same objects as the matching sequence diagram when possible. Number messages continuously: `1`, `1.1`, `1.2`, `2`.

## Activity

Express workflow and decisions. Parallel or alternative user operations must be branches, not a fake serial chain. Every decision needs conditions.

## State

Express lifecycle of one object. State names are durable conditions, not operation names. Transitions require events or guards.

## Component

Express deployable or logical modules/services and provided/required interfaces. Components are modules, services, adapters, databases, or external systems; not buttons or page fields.

## Deployment

Express runtime nodes and deployed artifacts. Nodes are environments, devices, containers, servers, clients, or networks; not entity classes.
