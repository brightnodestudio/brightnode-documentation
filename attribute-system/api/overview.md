# Public API Reference

All functions available on **BP_AttributeComponent** for use in gameplay code. All write functions are multiplayer safe with server RPC companions - call them from any context.

---

## Attribute Queries

### GetAttributeValue
Returns the current value of an attribute.
```
GetAttributeValue (AttributeTag: GameplayTag) → float
```

### GetAttributePercent
Returns the current value as a percentage of ComputedMax (0.0 to 1.0).
```
GetAttributePercent (AttributeTag: GameplayTag) → float
```

### GetAttributeMax
Returns the current ComputedMax of an attribute.
```
GetAttributeMax (AttributeTag: GameplayTag) → float
```

### GetAttributeMin
Returns the MinValue of an attribute.
```
GetAttributeMin (AttributeTag: GameplayTag) → float
```

### IsAttributeValid
Returns true if the attribute exists on this component's preset.
```
IsAttributeValid (AttributeTag: GameplayTag) → bool
```

### GetAllAttributes
Returns an array of all attribute tags active on this component.
```
GetAllAttributes () → GameplayTagContainer
```

---

## Attribute Modification

### ModifyAttribute
Applies a delta to an attribute's current value. Pass a negative value to reduce. Routes through threshold evaluation - always use this instead of SetAttributeValue when threshold events matter.
```
ModifyAttribute (AttributeTag: GameplayTag, Delta: float)
```

### SetAttributeValue
Sets an attribute's current value directly. Bypasses threshold evaluation - use only when threshold events are not needed.
```
SetAttributeValue (AttributeTag: GameplayTag, NewValue: float)
```

> ⚠️ **Warning:** SetAttributeValue bypasses threshold crossing checks. OnThresholdEntered and OnThresholdExited will not fire. Use ModifyAttribute when threshold events are required.

### RestoreAttribute
Restores an attribute to its ComputedMax.
```
RestoreAttribute (AttributeTag: GameplayTag)
```

### RestoreAllAttributes
Restores all attributes on this component to their ComputedMax.
```
RestoreAllAttributes ()
```

### ForceSetAttribute
Sets an attribute's value directly, bypassing all clamping and modifier evaluation. Use with caution.
```
ForceSetAttribute (AttributeTag: GameplayTag, NewValue: float)
```

---

## Threshold Queries

### GetActiveThresholds
Returns all currently active threshold tags for an attribute.
```
GetActiveThresholds (AttributeTag: GameplayTag) → GameplayTagContainer
```

### GetCurrentThreshold
Returns the current lowest active threshold tag for an attribute.
```
GetCurrentThreshold (AttributeTag: GameplayTag) → GameplayTag
```

### GetHighestSeverityThreshold
Returns the highest severity active threshold tag across all attributes or for a specific attribute.
```
GetHighestSeverityThreshold (AttributeTag: GameplayTag) → GameplayTag
```

---

## Modifier Management

### ApplyModifier
Applies a modifier to this component. Returns a handle used to remove it later.
```
ApplyModifier (ModifierDefinition: DA_ModifierDefinition) → ModifierHandle
```

### RemoveModifier
Removes a specific modifier instance by handle.
```
RemoveModifier (Handle: ModifierHandle)
```

### RemoveModifiersByAssetTag
Removes all active modifier instances matching a specific asset tag.
```
RemoveModifiersByAssetTag (AssetTag: GameplayTag)
```

### HasModifier
Returns true if a modifier matching the asset tag is currently active.
```
HasModifier (AssetTag: GameplayTag) → bool
```

---

## Decay Control

### PauseDecay
Pauses decay for a specific attribute.
```
PauseDecay (AttributeTag: GameplayTag)
```

### ResumeDecay
Resumes decay for a specific attribute.
```
ResumeDecay (AttributeTag: GameplayTag)
```

### PauseAllDecay
Pauses decay for all attributes on this component.
```
PauseAllDecay ()
```

### ResumeAllDecay
Resumes decay for all attributes on this component.
```
ResumeAllDecay ()
```

### SetDecayRate
Dynamically changes the decay rate for a specific attribute at runtime.
```
SetDecayRate (AttributeTag: GameplayTag, NewRate: float)
```

### SetDriftTarget
Sets the drift target value for a drifting attribute. Used by zone actors.
```
SetDriftTarget (AttributeTag: GameplayTag, TargetValue: float)
```

---

## Recovery Control

### PauseRecovery
Pauses recovery for a specific attribute.
```
PauseRecovery (AttributeTag: GameplayTag)
```

### ResumeRecovery
Resumes recovery for a specific attribute.
```
ResumeRecovery (AttributeTag: GameplayTag)
```
