# diagram-plan.json Schema Spec

## Top Level

```json
{
  "project": {
    "name": "string",
    "sourceMdj": "string",
    "workingMdj": "string",
    "outputDir": "string",
    "sourceInventory": "string",
    "preserveExistingIdentifiers": true
  },
  "layout": {
    "strategy": "zone-based | lane-based | manual-native-repair",
    "pilotDiagram": "string",
    "allowGlobalAutoLayoutAsFinal": false
  },
  "diagrams": []
}
```

## Diagram Base

```json
{
  "id": "string optional",
  "type": "class | sequence | communication | activity | usecase | state | component | deployment",
  "title": "string",
  "filename": "string",
  "businessGoal": "string",
  "source": "string",
  "layout": {},
  "visualStatus": "Verified | Unverified: <reason> | Failed: <reason>",
  "engineeringStatus": "Verified | Unverified: <reason> | Failed: <reason>",
  "sourcePreservationStatus": "Verified | Unverified: <reason> | Failed: <reason>"
}
```

## Class Diagram

```json
{
  "type": "class",
  "groups": {},
  "classes": [
    {
      "id": "string",
      "name": "string",
      "stereotype": "string",
      "attributes": [],
      "operations": []
    }
  ],
  "relationships": [
    {
      "from": "string",
      "to": "string",
      "kind": "association | aggregation | composition | inheritance | dependency",
      "label": "string",
      "multiplicity": "string"
    }
  ]
}
```

## Sequence Diagram

```json
{
  "type": "sequence",
  "participants": [],
  "messages": [
    {
      "from": "string",
      "to": "string",
      "text": "string",
      "kind": "call | return | self",
      "guard": "string optional"
    }
  ]
}
```

## Communication Diagram

```json
{
  "type": "communication",
  "objects": [],
  "messages": [
    {
      "no": "string",
      "from": "string",
      "to": "string",
      "text": "string",
      "kind": "call | return"
    }
  ]
}
```

## Activity Diagram

```json
{
  "type": "activity",
  "nodes": [
    {
      "id": "string",
      "kind": "start | action | decision | merge | fork | join | end",
      "text": "string"
    }
  ],
  "edges": [
    {
      "from": "string",
      "to": "string",
      "label": "string"
    }
  ]
}
```
