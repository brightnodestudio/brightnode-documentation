# Quick Start

This guide takes you from a basic BNOS setup to your first working outline.

The core workflow is:

```text
Create Gameplay Tag
        ↓
Create Outline Preset
        ↓
Assign Tag to Preset Tag
        ↓
Add Preset to Preset Library
        ↓
Request Outline Using That Tag
```

## 1. Add the Outline Component

Add the BNOS Outline Component to the relevant player Blueprint.

The component is the normal gameplay-facing entry point for applying, removing, and querying outlines.

## 2. Configure the World Manager

Ensure the BNOS World Manager is available in the level using the supplied setup.

Assign the required **Outline Preset Library**.

## 3. Create an Outline Gameplay Tag

Create a Gameplay Tag that uniquely identifies the outline you are about to create.

Example:

```text
BNOS.Outline.Enemy
```

Other examples might include:

```text
BNOS.Outline.Interactable
BNOS.Outline.Objective
BNOS.Outline.CriticalTarget
```

{% hint style="info" %}
Creating a Gameplay Tag does not create an outline preset. The tag is the identifier BNOS uses to find the preset that defines the outline.
{% endhint %}

## 4. Create an Outline Preset

Create a new BNOS Outline Preset Data Asset, or duplicate one of the supplied presets.

Configure the required behaviour:

* Visibility Mode
* Expiry
* Priority
* Outline Colour
* Outline Thickness
* Mesh Selection
* Flashing

## 5. Assign the Preset Tag

Open the preset and locate **Identity > Preset Tag**.

Assign the Gameplay Tag created in the previous step.

Example:

```text
Preset Tag = BNOS.Outline.Enemy
```

## 6. Register the Preset

Open the Outline Preset Library assigned to the World Manager.

Add the new Outline Preset to the **Outline Presets** array.

{% hint style="warning" %}
A preset must be registered in the active Preset Library before BNOS can resolve it through its Preset Tag.
{% endhint %}

## 7. Apply the Outline

From gameplay logic, obtain the player's Outline Component and call:

```text
ApplyOutline
```

Supply the target actor and the tag/request information required by the node.

For normal integration, `ApplyOutline` is the preferred entry point. The preset's Visibility Mode determines whether the request is handled as Local, Team, or Global.

## 8. Remove the Outline

Use:

```text
RemoveOutline
```

to remove a specific outline request.

Use:

```text
RemoveOutlinesForActor
```

when all applicable outline requests created by that component should be removed for an actor.

## Next Steps

Once a basic Local outline works, continue with the Core Concepts pages to configure priority, expiry, flashing, mesh selection, and multiplayer visibility.
