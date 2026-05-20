# Preset System

Presets define which attributes an actor uses. Rather than every actor running all nine attributes, each actor only runs the attributes relevant to it.

---

## What Is a DA_AttributeSetPreset?

A **DA_AttributeSetPreset** is a DataAsset that contains an array of attribute tags. When the component initialises, it reads this preset and only creates and runs the attributes listed.

---

## Included Presets

### DA_Preset_Human
All nine attributes: Health, Stamina, Oxygen, Hunger, Hydration, Temperature, Encumbrance, Mania, Tiredness.
Use for: Player characters, human NPCs.

### DA_Preset_Animal
Five attributes: Health, Stamina, Hunger, Hydration, Temperature.
Use for: Wildlife, pets, animal companions.

### DA_Preset_Zombie
Two attributes: Health, Mania.
Use for: Undead enemies, simple AI actors.

---

# Creating Custom Presets

Creating a new preset takes under a minute.

## Step 1 - Create the DataAsset
In the Content Browser, right-click and select:
```
Miscellaneous → Data Asset → DA_AttributeSetPreset
```

## Step 2 - Add Attribute Tags
Open your new DataAsset and add the Gameplay Tags for each attribute you want this preset to include:

```
Attribute.Health
Attribute.Stamina
Attribute.YourCustomAttribute
```

## Step 3 - Assign to the Component
Select **BP_AttributeComponent** on your actor, open the Details panel, and assign your new preset to the **Attribute Set Preset** property.

The component will initialise only the attributes listed in the preset. All decay, recovery, thresholds and modifiers for unlisted attributes are ignored entirely.
