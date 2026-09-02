# Quick Start Guide

This guide takes you from a basic BNOS setup to your first working outline.

The core workflow is:

```
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

## 1. Set Custom Depth-Stencil Pass

In Project Settings set Custom Depth-Stencil Pass to Enabled with Stencil.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## 2. Add the Outline Component

Add the BNOS Outline Component to the relevant player Blueprint. Ensure Auto Initialise is set to True.

The component is the normal gameplay-facing entry point for applying, removing, and querying outlines.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 2. Configure the World Manager

Ensure the BNOS World Manager is available in the level using the supplied setup.

Assign the required **Outline Preset Library**.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## 3. Create an Outline Gameplay Tag

Create a Gameplay Tag that uniquely identifies the outline you are about to create.

Example:

```
BNOS.Outline.Enemy
```

Other examples might include:

```
BNOS.Outline.Interactable
BNOS.Outline.Objective
BNOS.Outline.CriticalTarget
```

{% hint style="info" %}
Creating a Gameplay Tag does not create an outline preset. The tag is the identifier BNOS uses to find the preset that defines the outline.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## 5. Assign the Preset Tag

Open the preset and locate **Identity > Preset Tag**.

Assign the Gameplay Tag created in the previous step.

Example:

```
Preset Tag = BNOS.Outline.Enemy
```

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

## 6. Register the Preset

Open the Outline Preset Library assigned to the World Manager.

Add the new Outline Preset to the **Outline Presets** array.

{% hint style="warning" %}
A preset must be registered in the active Preset Library before BNOS can resolve it through its Preset Tag.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## 7. Apply the Outline

From gameplay logic, obtain the player's Outline Component and call:

```
ApplyOutline
```

Supply the target actor and the tag/request information required by the node.

For normal integration, `ApplyOutline` is the preferred entry point. The preset's Visibility Mode determines whether the request is handled as Local, Team, or Global.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## 8. Remove the Outline

Use:

```
RemoveOutline
```

to remove a specific outline request.

Use:

```
RemoveOutlinesForActor
```

when all applicable outline requests created by that component should be removed for an actor.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## Next Steps

Once a basic Local outline works, continue with the Core Concepts pages to configure priority, expiry, flashing, mesh selection, and multiplayer visibility.
