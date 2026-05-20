# Common Issues - Interaction System

## Interaction Prompt Does Not Appear

**1. Mesh Collision**

Ensure the mesh on the interactable actor blocks the Interaction trace channel.

`Collision - Trace Responses - Interaction = Block`

**2. Interaction Component Missing**

Confirm your Character Blueprint includes `AC_BNInteractionSystem`.

**3. Focus Trace Distance**

Check Focus Trace settings inside the interaction component and increase the distance if needed.

**4. Data Asset Not Assigned**

Confirm a DA\_Interactable data asset is assigned to the interactable blueprint.

## Interaction Input Does Not Work

**1. Mapping Context**

The Interaction Mapping Context must be added inside the Player Controller.

**2. Interact Logic Not Implemented**

Open the interactable blueprint and implement the function `Call Interact`.

## Outlines Are Not Showing

**1. Custom Depth Not Enabled**

`Project Settings - Rendering - Custom Depth Stencil Pass - Enabled with Stencil`

**2. Outlines Not Enabled on Component**

Inside `AC_BNInteractionSystem`, ensure Enable Outlines = True.

## Interaction Widget Does Not Display Correctly

**1. Common UI Plugin** - Ensure the Common UI plugin is enabled.

**2. Game Viewport Client** - Set to CommonGameViewportClient in Project Settings.

**3. Controller Data Assets** - Ensure Keyboard and Controller data assets are added to Common Input settings.

## Interactions Work in Singleplayer but Not Multiplayer

**1. Logic Running Only on Client** - Gameplay logic that changes world state must run on the server.

**2. Replication Not Enabled** - Ensure the interactable actor has Replicates = Enabled.

## Interactable Remains After Actor Is Destroyed

Use `Destroy Actor` to destroy the interactable. The prompt actor cleans itself up automatically when the interactable is removed.

## Bug Reports

Report bugs in the Brightnode Studio Discord in the **#bugs-interaction-system** channel.

💬 [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
