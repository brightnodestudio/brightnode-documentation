# BN Interaction System

## Quick Start Guide

This quick start will walk you through setting up a **basic Press to Interact system** using the Brightnode Interaction System.

The entire setup takes only a few minutes and works in both singleplayer and multiplayer environments.

### 1. Add the System to Your Project

* Migrate the **Brightnode Interaction System** folder into your project.
* Once migrated, delete the **Showcase** folder if you do not need the example content.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 160822.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 160903.png" alt=""><figcaption></figcaption></figure>

### 2. Required Project Settings

Open **Project Settings** and apply the following:

**Custom Depth**

`Project Settings → Rendering`

Enable:

Custom Depth Stencil Pass → **Enabled with Stencil**

This is required for the outline highlighting system.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161205.png" alt=""><figcaption></figcaption></figure>

### 3. Enable Required Plugin

Enable the **Common UI** plugin.

`Edit → Plugins → Common UI`

Restart the editor when prompted.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161258.png" alt=""><figcaption></figcaption></figure>

### 4. Set the Game Viewport Client

Open:

`Project Settings → Engine → General Settings`

Set:

Game Viewport Client Class → **CommonGameViewportClient**

This is required for the Common UI input system.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162352.png" alt=""><figcaption></figcaption></figure>

### 5. Setup the Interaction Trace Channel

Open:

`Project Settings → Collision`

Add a new **Trace Channel**:

Name\
`Interaction`

Default Response\
`Block`

Interactable meshes must block this channel in order to be detected.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 173649.png" alt=""><figcaption></figcaption></figure>

### 6. Setup Common UI Controller Data

Open the **Common Input Settings** and add the included controller data assets:

Add:

* **Keyboard Input Data**
* **Gamepad Input Data**

These are included with the system and provide the interaction icons used by the UI.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 163851.png" alt=""><figcaption></figcaption></figure>

### 7. Create an Interactable Actor

Create a new Blueprint that inherits from:

`BP_BaseInteractable`

This blueprint will represent your interactable object in the world.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161333.png" alt=""><figcaption></figcaption></figure>

### 8. Create an Interaction Data Asset

Create a new Data Asset using:

`DA_Interactable`

Inside the asset you can define:

* Interaction type (Press, Hold, Grab, etc)
* UI text
* Icons
* Interaction behavior settings

For this quick start, configure it as a **Press Interaction**.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161416.png" alt=""><figcaption></figcaption></figure>

### 9. Apply the Data Asset

Open your **Interactable Blueprint** and:

1. Assign the **DA\_Interactable** you created.
2. Configure any additional settings if required.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161729.png" alt=""><figcaption></figcaption></figure>

### 10. Add a Mesh

Add a mesh component to your interactable blueprint.

Ensure the mesh collision:

Blocks the **Interaction** trace channel.

This allows the interaction trace to detect the object.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161818.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161825.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161846.png" alt=""><figcaption></figcaption></figure>

### 11. Place the Actor in the World

Drag your interactable blueprint into the level.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161901.png" alt=""><figcaption></figcaption></figure>

### 12. Setup the Player Character

Open your **Character Blueprint**.

Add the component:

`AC_BNInteractionSystem`

This component handles all interaction tracing and logic.

Configure:

**Focus Trace Settings**\
Controls the forward interaction trace.

**Radius Scan Settings (Optional)**\
Allows nearby interactables to be detected even when not directly looked at.

**Outline Settings (Optional)**\
Enable outlines if you want interactables to highlight when focused.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161913.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161931.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 161942.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162005.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162014.png" alt=""><figcaption></figcaption></figure>

### 13. Setup the Player Controller

Open your **Player Controller**.

Add the **Interaction Mapping Context** to your input system.

This enables the interaction input used by the system.

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162036.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162104.png" alt=""><figcaption></figcaption></figure>

### 14. Implement Interaction Logic

Open your **Interactable Blueprint**.

Inside the blueprint implement the interface function:

`Call Interact`

Add whatever gameplay logic you want to happen when the player interacts with the object.

Examples include:

* Opening a door
* Picking up an item
* Activating a switch

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 162833.png" alt=""><figcaption></figcaption></figure>

### Result

You now have a **fully functional Press to Interact system**.

When the player looks at the interactable object:

* The interaction prompt appears
* The object can highlight (if outlines are enabled)
* Pressing the interaction key triggers the interact logic

<figure><img src="../.gitbook/assets/Screenshot 2026-03-10 163931.png" alt=""><figcaption></figcaption></figure>

## Creating a Hold to Interact Item

## Creating and Interact While Held Item

## Creating a Physics Grab Item

## Swapping Interact Presets at Runtime

## Common Issues

### Interaction Prompt Does Not Appear

**1. Mesh Collision**

Ensure the mesh on the interactable actor **blocks the Interaction trace channel**.

Open the mesh component and verify:

Collision → Trace Responses → **Interaction = Block**

If the mesh does not block the interaction trace, the system cannot detect it.

**2. Interaction Component Missing**

Your character must contain the interaction component.

Open your Character Blueprint and confirm it includes:

`AC_BNInteractionSystem`

Without this component, the player cannot scan for interactables.

**3. Focus Trace Distance**

If the player is too far away, the trace will not hit the object.

Check the Focus Trace settings inside the interaction component and increase the distance if necessary.

**4. Data Asset Not Assigned**

Each interactable must have a **DA\_Interactable** data asset assigned.

Open the interactable blueprint and confirm the data asset reference is set.

### Interaction Input Does Not Work

If the prompt appears but pressing the key does nothing, check the following:

**1. Mapping Context**

The **Interaction Mapping Context** must be added inside the Player Controller.

If this mapping context is not active, the interaction input will never fire.

**2. Interact Logic Not Implemented**

The interactable must implement the interaction logic.

Open the interactable blueprint and implement the function:

`Call Interact`

Add the gameplay logic you want to trigger when the player interacts.

### Outlines Are Not Showing

If outlines are not visible on interactables:

**1. Custom Depth Must Be Enabled**

Open:

Project Settings → Rendering

Set:

Custom Depth Stencil Pass → **Enabled with Stencil**

**2. Outlines Must Be Enabled in the Interaction Component**

Inside `AC_BNInteractionSystem`, ensure:

Enable Outlines = **True**

### Interaction Widget Does Not Display Correctly

If the interaction UI does not appear or behaves incorrectly:

**1. Common UI Plugin**

Ensure the **Common UI** plugin is enabled.

**2. Game Viewport Client**

Open:

Project Settings → Engine → General Settings

Set:

Game Viewport Client Class → **CommonGameViewportClient**

**3. Controller Data Assets**

Ensure the provided **Keyboard** and **Controller** data assets are added to the Common Input settings.

Without these, the UI may not display the correct input icons.

### Interactions Work in Singleplayer but Not Multiplayer

The system is built to be server authoritative. If something works locally but not in multiplayer, usually one of these is missing:

**1. Interaction Logic Running Only on Client**

Gameplay logic should run on the **server**.

If your interaction changes the world state, ensure the logic runs through the server.

**2. Replication Not Enabled**

If the interaction modifies actors, ensure the actor has:

Replicates = **Enabled**

### Interactable Remains After Actor Is Destroyed

If the interaction prompt remains after the interactable actor is destroyed, ensure the actor is properly destroyed using:

`Destroy Actor`

The prompt actor will automatically clean itself up when the interactable is removed.

## Bug Reports & Support

If you believe you have found a bug or unexpected behaviour, please report it via the official **Brightnode Studio Discord**.

For this system, bugs should be posted in the relevant bug report channel:

**#bugs-interaction-system**

When reporting a bug, please include:

* Unreal Engine version
* System version (if applicable)
* Clear steps to reproduce the issue
* Screenshots or short videos where possible

This helps issues get identified and fixed much faster.

Join the Discord here:\
👉 [**Discord Link**](https://discord.gg/QTM7EZHHpV)
