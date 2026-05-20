# Core Callable Functions

These are the only functions required to use the BN Visual Marking System. All callable functions are available on **AC\_VisualMarkingSystem**.

## Set Outline On Actor

Applies or removes an outline on a target actor.

```
Set Outline On Actor (TargetActor, OutlinePreset, Enabled)
```

- **TargetActor** - the actor to outline
- **OutlinePreset** - the DA\_OutlinePreset to use
- **Enabled** - true to apply the outline, false to remove it

## Spawn Symbol Actor

Spawns a symbol actor attached to a target actor.

```
Spawn Symbol Actor (TargetActor, SymbolPreset)
```

- **TargetActor** - the actor to attach the symbol to
- **SymbolPreset** - the DA\_SymbolPreset to use

## Clear Symbol On Actor

Removes any symbol currently attached to a target actor.

```
Clear Symbol On Actor (TargetActor)
```

- **TargetActor** - the actor to clear the symbol from
