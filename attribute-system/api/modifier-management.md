# Modifier Management

Functions for applying and removing modifiers on **BP_AttributeComponent**. All write functions are multiplayer safe with server RPC companions.

---

## ApplyModifier

Applies a modifier to this component. Returns a **ModifierHandle** that can be stored and used to remove the modifier later.

```
ApplyModifier (ModifierDefinition: DA_ModifierDefinition) → ModifierHandle
```

- The modifier's stack rule is evaluated on application
- If the stack rule is Ignore and an instance already exists, the handle returned is invalid - no new instance is created
- If the modifier has a duration greater than 0 it will automatically expire and remove itself
- Store the returned handle if you need to remove the modifier manually before it expires

**Example use:** Applying Poison when a player enters a poison zone:
```
ApplyModifier (DA_Mod_Poison) → Store Handle in variable
```

---

## RemoveModifier

Removes a specific modifier instance identified by its handle.

```
RemoveModifier (Handle: ModifierHandle)
```

Use this when you need to remove a specific instance of a modifier - for example removing a zone effect when the player exits the zone, using the handle stored when it was applied.

**Example use:** Removing Poison when a player leaves the poison zone:
```
RemoveModifier (StoredPoisonHandle)
```

---

## RemoveModifiersByAssetTag

Removes **all active instances** of modifiers matching a specific asset tag, regardless of how many instances are active.

```
RemoveModifiersByAssetTag (AssetTag: GameplayTag)
```

Use this when you want to clear all instances of a modifier type without needing to track individual handles - useful for cleanup on death, respawn, or zone exit when multiple stacked instances may be present.

**Example use:** Clearing all Poison instances on respawn:
```
RemoveModifiersByAssetTag (Modifier.Poison)
```

---

## HasModifier

Returns true if at least one active modifier instance matching the asset tag is currently applied to this component.

```
HasModifier (AssetTag: GameplayTag) → bool
```

**Example use:** Checking whether the player is currently Poisoned before applying a second dose - useful when implementing custom stack logic outside the built-in stack rules.

---

## Handle Storage Pattern

When applying modifiers that need manual removal (zone effects, equipment buffs), always store the handle in a variable on the actor that applied it:

```
On Zone Enter
→ ApplyModifier (DA_Mod_ZoneEffect)
→ Set Variable: ZoneModifierHandle

On Zone Exit
→ RemoveModifier (ZoneModifierHandle)
→ Clear Variable: ZoneModifierHandle
```

This pattern ensures clean removal even if the player exits unexpectedly or multiple overlapping zones are involved.
