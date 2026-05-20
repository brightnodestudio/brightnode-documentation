# Creating Custom Modifiers

New modifiers are created as **DA_ModifierDefinition** DataAssets - no Blueprint changes required.

---

## Step 1 - Create the DataAsset

In the Content Browser, right-click and select:
```
Miscellaneous → Data Asset → DA_ModifierDefinition
```

Name it following the existing convention, for example `DA_Mod_Poisoned` or `DA_Mod_WellRested`.

---

## Step 2 - Configure the Asset

Open your new DataAsset and fill in the properties:

| Property | Description |
|---|---|
| **DisplayName** | Name shown in the debug widget active modifiers column |
| **Icon** | Optional texture for UI display |
| **StackRule** | Stack / Ignore / Refresh / Replace |
| **Duration** | Seconds before auto-expiry. Set to 0 for permanent. |
| **StatModifiers** | Add entries for any ComputedMax effects |
| **TickModifiers** | Add entries for any per-tick value changes |

---

## Step 3 - Stat Modifier Entry

Each entry in the StatModifiers array requires:

| Field | Description |
|---|---|
| **AttributeTag** | Which attribute's ComputedMax to affect |
| **ModifierType** | Additive / Multiplicative / Override |
| **Value** | The modifier value (flat amount, multiplier, or hard cap) |

---

## Step 4 - Tick Modifier Entry

Each entry in the TickModifiers array requires:

| Field | Description |
|---|---|
| **AttributeTag** | Which attribute to affect each tick |
| **TickType** | DirectDelta / DriftOffset |
| **DeltaPerTick** | How much to change the value each tick (negative to drain) |
| **bIsFatigueSource** | If true, this modifier blocks recovery on the target attribute |

---

## Step 5 - Apply the Modifier

Apply your modifier from any Blueprint using the public API:

```
ApplyModifier (BP_AttributeComponent ref, DA_ModifierDefinition ref)
→ Returns ModifierHandle (store if you need to remove it manually)
```

Or reference it as an AutoApplyModifier in a threshold definition to have it applied automatically.
