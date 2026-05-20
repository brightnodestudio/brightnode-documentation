# BN Interaction System - Quick Start Guide

This quick start will walk you through setting up a basic Press to Interact system using the Brightnode Interaction System.

The entire setup takes only a few minutes and works in both singleplayer and multiplayer environments.

## 1. Add the System to Your Project

- Migrate the **Brightnode Interaction System** folder into your project.
- Once migrated, delete the Showcase folder if you do not need the example content.

## 2. Required Project Settings

Open Project Settings and apply the following.

**Custom Depth**

`Project Settings - Rendering`

Enable:

Custom Depth Stencil Pass - **Enabled with Stencil**

This is required for the outline highlighting system.

## 3. Enable Required Plugin

Enable the **Common UI** plugin.

`Edit - Plugins - Common UI`

Restart the editor when prompted.

## 4. Set the Game Viewport Client

Open:

`Project Settings - Engine - General Settings`

Set:

Game Viewport Client Class - **CommonGameViewportClient**

This is required for the Common UI input system.

## 5. Setup the Interaction Trace Channel

Open:

`Project Settings - Collision`

Add a new Trace Channel:

- Name: `Interaction`
- Default Response: `Block`

Interactable meshes must block this channel in order to be detected.

## 6. Setup Common UI Controller Data

Open the Common Input Settings and add the included controller data assets:

- Keyboard Input Data
- Gamepad Input Data

These are included with the system and provide the interaction icons used by the UI.

## 7. Create an Interactable Actor

Create a new Blueprint that inherits from:

`BP_BaseInteractable`

This blueprint will represent your interactable object in the world.

## 8. Create an Interaction Data Asset

Create a new Data Asset using:

`DA_Interactable`

Inside the asset you can define:

- Interaction type (Press, Hold, Grab, etc)
- UI text
- Icons
- Interaction behaviour settings

For this quick start, configure it as a Press Interaction.

## 9. Apply the Data Asset

Open your Interactable Blueprint and:

1. Assign the DA\_Interactable you created.
2. Configure any additional settings if required.

## 10. Add a Mesh

Add a mesh component to your interactable blueprint.

Ensure the mesh collision blocks the **Interaction** trace channel. This allows the interaction trace to detect the object.

## 11. Place the Actor in the World

Drag your interactable blueprint into the level.

## 12. Setup the Player Character

Open your Character Blueprint.

Add the component:

`AC_BNInteractionSystem`

This component handles all interaction tracing and logic.

Configure:

- **Focus Trace Settings** - Controls the forward interaction trace.
- **Radius Scan Settings (Optional)** - Allows nearby interactables to be detected even when not directly looked at.
- **Outline Settings (Optional)** - Enable outlines if you want interactables to highlight when focused.

## 13. Setup the Player Controller

Open your Player Controller.

Add the **Interaction Mapping Context** to your input system. This enables the interaction input used by the system.

## 14. Implement Interaction Logic

Open your Interactable Blueprint.

Implement the interface function:

`Call Interact`

Add whatever gameplay logic you want to happen when the player interacts with the object. Examples include opening a door, picking up an item, or activating a switch.

## Result

You now have a fully functional Press to Interact system.

When the player looks at the interactable object:

- The interaction prompt appears
- The object can highlight (if outlines are enabled)
- Pressing the interaction key triggers the interact logic
