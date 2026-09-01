# Creating an Outline Preset

Outline Presets are Data Assets that define how an outline behaves.

## Create the Asset

Create a new BNOS Outline Preset Data Asset or duplicate a supplied example.

Use a descriptive asset name, for example:

```text
PDA_BNOS_Outline_Enemy
PDA_BNOS_Outline_Interactable
PDA_BNOS_Outline_Objective
```

## Configure Identity

Assign the preset's unique **Preset Tag** and choose its **Visibility Mode**.

## Configure Behaviour

Set the required:

* Lifetime
* Priority
* Outline visuals
* Mesh selection
* Flashing behaviour

## Register the Preset

Add the finished Data Asset to the **Outline Presets** array of the active Outline Preset Library.

The preset is now available to BNOS through its Preset Tag.
