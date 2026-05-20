# Creating Custom Presets

Custom presets let you define exactly which attributes any actor uses. A zombie that only needs Health and Mania, an animal that needs Health and Temperature, or a vehicle with a completely custom attribute set - all handled through a DataAsset with no Blueprint changes required.

---

## Step 1 - Create the DataAsset

In the Content Browser, right-click and navigate to:

```
Miscellaneous → Data Asset
```

In the asset class picker, search for and select **DA_AttributeSetPreset**. Name your asset following the existing convention - for example `DA_Preset_Survivor` or `DA_Preset_Wildlife`.

---

## Step 2 - Add Attribute Tags

Open your new DataAsset. You will see an **Attributes** array - add a Gameplay Tag entry for each attribute you want this preset to include.

Available built-in attribute tags:

```
Attribute.Health
Attribute.Stamina
Attribute.Oxygen
Attribute.Hunger
Attribute.Hydration
Attribute.Temperature
Attribute.Encumbrance
Attribute.Mania
Attribute.Tiredness
```

Add only the tags relevant to this actor type. Attributes not listed in the preset are completely ignored by the component - no decay, no threshold evaluation, no memory overhead.

---

## Step 3 - Assign to the Component

Select **BP_AttributeComponent** on your actor in the Components panel. In the Details panel find the **Attribute Set Preset** property and assign your new DataAsset.

Press Play and open the debug widget (F3) - only the attributes listed in your preset will appear.

---

## Step 4 - Verify Thresholds

Thresholds are defined globally in **DT_ThresholdDefinitions** and evaluated per attribute. If your preset includes an attribute that has thresholds defined, those thresholds will be active automatically. No additional setup is needed.

If your preset excludes an attribute, any thresholds defined for that attribute are simply never evaluated.

---

## Example Custom Presets

### Survivor (Hardcore)
All nine attributes plus higher decay rates configured in the DataTable for a more punishing experience.
```
Attribute.Health
Attribute.Stamina
Attribute.Oxygen
Attribute.Hunger
Attribute.Hydration
Attribute.Temperature
Attribute.Encumbrance
Attribute.Mania
Attribute.Tiredness
```

### Guard NPC
A simple NPC that only needs Health and Stamina.
```
Attribute.Health
Attribute.Stamina
```

### Wildlife
Animals that need sustenance and temperature sensitivity.
```
Attribute.Health
Attribute.Stamina
Attribute.Hunger
Attribute.Hydration
Attribute.Temperature
```
