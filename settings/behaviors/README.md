# Behavior Trees JSON Format

This directory contains JSON definitions for AI behavior trees.

## File Structure

Each behavior file defines a single behavior tree:

```json
{
  "name": "entity_name",
  "description": "Optional description",
  "tree": { /* behavior tree definition */ }
}
```

## Available Node Types

### Control Nodes

| Type | Description | Fields |
|------|-------------|--------|
| `Select` | Try children in order until one succeeds | `children: []` |
| `Sequence` | Run children in order until one fails | `children: []` |
| `While` | Repeat body while condition runs | `condition: {}, body: []` |
| `If` | Conditional branch | `condition: {}, success: {}, failure: {}` |
| `WhenAll` | Wait for all children to succeed | `children: []` |
| `WhenAny` | Wait for any child to succeed | `children: []` |

### Leaf Nodes

| Type | Description | Fields |
|------|-------------|--------|
| `Action` | Execute named action | `name: "ActionName"` |
| `Wait` | Wait for duration | `duration: f64` |
| `WaitForever` | Wait indefinitely | none |

## Available Actions

### Targeting (Conditions)
- `HasAttackTarget` - Returns Running if target exists
- `HasNotAttackTarget` - Returns Running if no target
- `HasScaryTarget` - Returns Running if scary target exists
- `HasNotScaryTarget` - Returns Running if no scary target
- `LookOnTarget` - Rotate towards attack target

### Movement
- `PrepareFreeState` - Choose random patrol point
- `MoveFreeState` - Move to patrol point
- `WaitFreeState` - Wait at patrol point

### Combat
- `PrepareAttack` - Setup attack parameters
- `MoveToAttackTarget` - Move towards target
- `MoveToAttackTargetPath` - Move using pathfinding
- `AttackAnimation` - Send attack animation
- `PreAttackTimeout` - Wait before attack
- `AttackTarget` - Execute attack
- `PostAttackTimeout` - Wait after attack
- `BreakAttackSequenceTimeout` - Break long chase

### Pathfinding
- `DropPath` - Clear current path

### Special
- `PrepareScaryState` - Calculate escape point
- `MoveOutOfScaryTarget` - Run away
- `PostScaryTimeout` - Cooldown after escape

## Example: Aggressive Mob

```json
{
  "name": "spider",
  "tree": {
    "type": "Select",
    "children": [
      {
        "type": "While",
        "condition": { "type": "Action", "name": "HasAttackTarget" },
        "body": [{
          "type": "Sequence",
          "children": [
            { "type": "Action", "name": "PrepareAttack" },
            { "type": "Action", "name": "MoveToAttackTarget" },
            { "type": "Action", "name": "AttackAnimation" },
            { "type": "Action", "name": "PreAttackTimeout" },
            { "type": "Action", "name": "AttackTarget" },
            { "type": "Action", "name": "PostAttackTimeout" }
          ]
        }]
      },
      {
        "type": "While",
        "condition": { "type": "Action", "name": "HasNotAttackTarget" },
        "body": [{
          "type": "Sequence",
          "children": [
            { "type": "Action", "name": "PrepareFreeState" },
            { "type": "Action", "name": "MoveFreeState" },
            { "type": "Action", "name": "WaitFreeState" }
          ]
        }]
      }
    ]
  }
}
```
