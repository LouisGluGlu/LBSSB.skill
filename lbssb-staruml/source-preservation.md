# Source Preservation

Use this whenever a task references an existing `.mdj`, source project, screenshot, or prior model.

## Rule

Do not recreate business models from scratch when source model data exists.
Read and preserve existing model elements first.

## Required Inventory

Before generating or repairing diagrams, inventory:

- project filename and model tree;
- diagram names and types;
- existing classes, attributes, operations, stereotypes, and visibility;
- existing actors and use cases;
- existing relationships and multiplicities;
- language/style conventions, including English identifiers.

## Preservation Rules

- Preserve English class names, attribute names, operation names, and types unless the user explicitly asks for Chinese naming.
- Preserve existing identifiers and terminology even if the new requirement text is Chinese.
- Add missing elements instead of replacing semantically equivalent existing elements.
- If a new diagram is generated from a source use case diagram, keep the source actors/use-case terms aligned.
- If translation is useful, record both forms in documentation, not by overwriting the original model vocabulary.

## When Replacement Is Allowed

Replacement is allowed only when:

- the source element is clearly wrong and the reason is recorded;
- the user asks for a clean rebuild;
- the source project cannot be read and the status is marked `Source Preservation Unverified`;
- the element is a generated duplicate created by a previous failed run.

## Manifest Fields

For any task with source data, manifest should include:

```json
{
  "sourcePreservation": {
    "sourceRead": true,
    "preservedClasses": 0,
    "preservedAttributes": 0,
    "preservedOperations": 0,
    "renamedOrTranslated": []
  }
}
```

If the source cannot be read, final status cannot claim source preservation.
