# Common Issues

Solutions to the most frequently encountered problems when integrating the Brightnode Attribute System.

---

## Attributes Not Appearing in Debug Widget

**Symptoms:** F3 debug widget shows no attributes, or shows fewer attributes than expected.

**Causes and fixes:**

- **No preset assigned** - Select BP_AttributeComponent in the Details panel and ensure a DA_AttributeSetPreset is assigned to the Attribute Set Preset property
- **Interface not implemented** - Open your actor's Class Settings and confirm BPI_AttributeSystem is listed under Implemented Interfaces
- **Component not found** - Confirm BP_AttributeComponent is added as a component on the actor, not just referenced as a variable
- **Actor not replicating** - In multiplayer, ensure Replicates is enabled in the actor's Class Defaults

---

## OnThresholdExited Not Firing When Zeroing an Attribute

**Symptoms:** Dropping all encumbrance or resetting an attribute to zero does not fire threshold exit events.

**Cause:** `SetAttributeValue` bypasses threshold evaluation entirely.

**Fix:** Use `ModifyAttribute` with a negative delta equal to the current value:

```
GetAttributeValue (AttributeTag) → float
float * -1.0
ModifyAttribute (AttributeTag, negative float)
```

This routes the change through threshold evaluation so OnThresholdExited fires correctly.

---

## Walk Speed Not Updating on Client After Threshold

**Symptoms:** Walk speed changes correctly in standalone but not on the owning client in multiplayer.

**Cause:** Binding to the server-side `OnThresholdEntered` / `OnThresholdExited` dispatcher. Server dispatchers do not fire on clients.

**Fix:** Bind to `Client_OnThresholdEntered` and `Client_OnThresholdExited` instead. Set `CharacterMovement → MaxWalkSpeed` from the client event.

---

## UI Widget Not Updating in Multiplayer

**Symptoms:** Attribute bars and icons update correctly in standalone but stay static for clients in multiplayer.

**Cause:** Widget is binding to `OnAttributeChanged` (server dispatcher) instead of `Client_OnAttributeChanged`.

**Fix:** In your widget's Construct event, bind to `Client_OnAttributeChanged` - not the server dispatcher. All widget bindings must use the Client_ prefixed event versions.

---

## Recovery Not Resuming After Modifier Removed

**Symptoms:** An attribute stops recovering and does not resume even after the blocking modifier is removed.

**Cause:** Another fatigue source modifier is still active on the same attribute. Recovery is blocked while any active modifier with `bIsFatigueSource = true` is present.

**Fix:** Call `HasModifier` for each known fatigue source to confirm all are removed. Use `RemoveModifiersByAssetTag` for a clean sweep if needed.

---

## ComputedMax Not Updating After Modifier Removed

**Symptoms:** Stamina maximum stays reduced even after the modifier causing the reduction should be gone.

**Cause:** The modifier was not removed correctly - either the wrong handle was used with `RemoveModifier` or the AssetTag used with `RemoveModifiersByAssetTag` does not match.

**Fix:**
- Confirm the handle stored on apply matches the one passed to RemoveModifier
- Confirm the AssetTag in RemoveModifiersByAssetTag exactly matches the tag on the DA_ModifierDefinition asset
- Use the debug widget to check the Active Modifiers column - if the modifier still appears there it has not been removed

---

## Component Not Found on Client

**Symptoms:** `GetComponentByClass` returns null on the client, or attribute queries return 0.

**Cause:** The actor does not have Replicates enabled.

**Fix:** Open the actor's Class Defaults and enable **Replicates**. The component will not be accessible on clients if the owning actor does not replicate.

---

## Drift Not Changing When Entering a Zone

**Symptoms:** Temperature (or other drifting attribute) does not change when the player enters a temperature zone.

**Cause:** Either `SetDriftTarget` is not being called correctly, or the zone overlap is not firing.

**Fix:**
- Confirm the zone's overlap event is firing (add a Print String to the overlap to verify)
- Confirm `SetDriftTarget` is being called on the correct component reference on the server
- Confirm the AttributeTag passed to SetDriftTarget matches the attribute tag in the preset

---

## Still Stuck?

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
