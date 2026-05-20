# Helper Functions

Helper functions are available on **AC\_VisualMarkingSystem** under the Helper Functions category. They are optional but recommended for clean toggle logic.

## Is Actor Outlined

Returns true if the target actor currently has an outline applied.

```
Is Actor Outlined (TargetActor) -> bool
```

Use this before calling Set Outline On Actor to implement clean toggle behaviour.

## Actor Has Symbol

Returns true if the target actor currently has a symbol attached.

```
Actor Has Symbol (TargetActor) -> bool
```

Use this before calling Spawn Symbol Actor to prevent duplicate symbols being attached to the same actor.
