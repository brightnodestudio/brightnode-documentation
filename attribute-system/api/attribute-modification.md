# Attribute Modification

Write functions for changing attribute values on **BP_AttributeComponent**. All write functions are multiplayer safe - they route through server RPCs automatically if called from a client context.

---

## ModifyAttribute

Applies a **delta** to an attribute's current value. This is the primary function for changing attribute values in gameplay code.

```
ModifyAttribute (AttributeTag: GameplayTag, Delta: float)
```

- Pass a **negative** delta to reduce the attribute (damage, drain, cost)
- Pass a **positive** delta to increase the attribute (restore, heal, refill)
- Routes through full threshold evaluation - `OnThresholdEntered` and `OnThresholdExited` fire correctly
- The result is clamped between MinValue and ComputedMax automatically

**Example:** Applying 25 damage to Health:
```
ModifyAttribute (Attribute.Health, -25.0)
```

**Example:** Removing encumbrance when dropping an item (store the item weight on pickup and pass it back as a negative delta):
```
ModifyAttribute (Attribute.Encumbrance, ItemWeight * -1.0)
```

> **Important:** Always use ModifyAttribute when threshold events matter. It is the only write function that runs full threshold evaluation.

---

## SetAttributeValue

Sets an attribute's current value directly to a specific value, bypassing threshold evaluation.

```
SetAttributeValue (AttributeTag: GameplayTag, NewValue: float)
```

> ⚠️ **Warning:** SetAttributeValue bypasses threshold crossing checks. `OnThresholdEntered` and `OnThresholdExited` will NOT fire. Only use this when you specifically do not need threshold events - for example setting an initial value on spawn before gameplay begins.

---

## RestoreAttribute

Restores a single attribute to its current ComputedMax. Routes through threshold evaluation so threshold exit events fire correctly as the value climbs back up.

```
RestoreAttribute (AttributeTag: GameplayTag)
```

**Example use:** A medkit that fully restores Health.

---

## RestoreAllAttributes

Restores all attributes on this component to their ComputedMax in a single call.

```
RestoreAllAttributes ()
```

**Example use:** A respawn or checkpoint reset that brings the player back to full stats.

---

## ForceSetAttribute

Sets an attribute's value directly, bypassing all clamping, modifier evaluation, and threshold checks. Use with caution - this is an absolute override.

```
ForceSetAttribute (AttributeTag: GameplayTag, NewValue: float)
```

**Example use:** Debug tools or admin commands that need to hard-set a value regardless of the current modifier state.

---

## Choosing the Right Function

| Scenario | Function to Use |
|---|---|
| Dealing damage or draining an attribute | ModifyAttribute (negative delta) |
| Restoring or healing an attribute | ModifyAttribute (positive delta) or RestoreAttribute |
| Dropping items and removing encumbrance | ModifyAttribute (negative delta equal to item weight) |
| Setting initial values on spawn | SetAttributeValue |
| Full stat reset on respawn | RestoreAllAttributes |
| Debug / admin hard override | ForceSetAttribute |
