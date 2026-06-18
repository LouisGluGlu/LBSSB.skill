# Class Diagram Rules

## Positioning

A class diagram is not a database-table pile and not a BCE four-layer dump. It first expresses the domain model, then role inheritance, then control/service/repository support.

If the project has an existing `.mdj`, the class diagram is also a preservation task. Existing class names, English attributes, English operations, types, stereotypes, and visibility are part of the source model and must not be silently replaced by newly generated Chinese-only content.

## Required ClassDiagramPlan

Create this before drawing:

```yaml
groups:
  role_area:
    classes: []
    purpose: "actors/users/permission inheritance"
  core_domain_area:
    classes: []
    purpose: "entities and aggregates that define the system"
  structure_area:
    classes: []
    purpose: "composition structures such as BOM, order lines, route steps"
  process_area:
    classes: []
    purpose: "workflow or lifecycle objects"
  support_area:
    classes: []
    purpose: "service, repository, gateway, policy, generator"
must_draw_relations:
  - from: ""
    to: ""
    kind: "association | aggregation | composition | inheritance | dependency"
    multiplicity: ""
    reason: ""
hidden_or_optional_relations:
  - from: ""
    to: ""
    reason: ""
routing_rules:
  role_inheritance: "top, with whitespace"
  core_domain: "center"
  composition: "short and local"
  technical_dependency: "edge-routed"
source_preservation:
  preserve_existing_identifiers: true
  translate_only_when_requested: true
```

## Priorities

- P0: core entity relationships and multiplicities.
- P1: existing source identifiers and class member definitions.
- P2: role inheritance.
- P3: control/service/repository classes.
- P4: View dependency lines.

If space is limited, remove P4 first, then compress P3. Do not sacrifice P0 or P1.

## Layout

- Put role inheritance at the top with clear whitespace.
- Put the domain trunk in the visual center.
- Keep composition relationships short; do not cross the entire diagram.
- Route technical dependencies around the edge, not through the core domain.
- Keep multiplicity labels away from class borders and lines.
- Keep Repository and Service visually smaller than core entities.
- Keep inheritance arrows away from class names.
- Keep association lines out of the class title compartment.
- Do not run global auto-layout after semantic grouping unless you immediately inspect and repair the exported PNG.
- Size each class box from the longest visible attribute/operation before routing relationships.
- Keep source-language style consistent; do not mix translated attributes with preserved English operations in the same class unless documented.

## Class Layout Repair Actions

Apply these actions when a class diagram fails readability gates:

1. Move the role inheritance area to the top center with enough vertical whitespace.
2. Move the core domain area to the visual center and keep aggregate roots prominent.
3. Move support classes such as Controller, Service, Repository, Gateway, Policy, and Generator to the edges.
4. Delete non-essential View dependency lines, especially lines that cross the core domain.
5. Merge multiple Repository dependencies into `RepositoryGateway` when the diagram is dependency-heavy.
6. Reposition multiplicity labels so they do not touch class borders, arrowheads, or other labels.
7. Export PNG and review. If gates still fail, repair locally instead of redrawing the whole diagram.

## Source Preservation Repair Actions

Apply when a generated class diagram loses source vocabulary:

1. Re-read the source model or source inventory.
2. Restore original class names, attributes, operations, and types.
3. Add Chinese explanations only in documentation or notes unless requested in the model.
4. Record restored counts in manifest `sourcePreservation`.
5. Re-export and re-check visual layout because restored English identifiers may change box widths.

## Dependency Compression

- If a dependency is obvious from an operation signature, it does not always need a line.
- Multiple Control-to-Repository dependencies may be replaced by `RepositoryGateway`.
- View-to-Control dependencies should keep only important entry points.
- Do not draw every UI button as a dependency.

## Forbidden

- Inheritance line over text.
- Relationship line through class name area.
- Random composition diamonds.
- Action names as classes.
- Unbounded class count.
- Technical helper classes dominating the domain model.
- A nice PNG while the native `.mdj` class diagram remains unreadable.

## Quality Gates

Default:

- Recommended class count: 18-28.
- Maximum class count: 32.
- Recommended relationship count: 18-32.
- Maximum relationship count: 36.
- Line-through-box count: `<= 3`.
- Obvious crossings: `<= 7`.
- Isolated classes: `0`.
- Action classes: `0`.
- Core relationship completeness: `>= 90%`.

Quick single-diagram task:

- Maximum class count: 26.
- Maximum relationship count: 28.
- Line-through-box count: `<= 2`.
- Obvious crossings: `<= 5`.

## Review Order

1. Confirm domain objects.
2. Confirm source identifiers and class members are preserved.
3. Confirm aggregate/composition relationships.
4. Confirm inheritance.
5. Confirm multiplicities.
6. Add only necessary support classes.
7. Route lines and labels.
8. Export and inspect PNG.
9. Verify native `.mdj` remains editable and readable.
