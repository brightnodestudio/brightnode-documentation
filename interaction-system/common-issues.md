# Common Issues - Interaction System

## Interaction Prompt Does Not Appear

**1. Mesh Collision**

Ensure the mesh on the interactable actor blocks the Interaction trace channel.

Open the mesh component and verify:

`Collision - Trace Responses - Interaction = Block`

**2. Interaction Component Missing**

Your character must contain the interaction component.

Open your Character Blueprint and confirm it includes `AC_BNInteractionSystem`. Without this component the player cannot scan for interactables.

**3. Focus Trace Distance**

If the player is too far away the trace will not hit the object. Check the Focus Trace settings inside the interaction component and increase the distance if necessary.

**4. Data Asset Not Assigned**

Each interactable must have a DA\_Interactable data asset assigned. Open the interactable blueprint and confirm the data asset reference is set.

## Interaction Input Does Not Work

If the prompt appears but pressing the key does nothing:

**1. Mapping Context**

The Interaction Mapping Context must be added inside the Player Controller. If this mapping context is not active the interaction input will never fire.

**2. Interact Logic Not Implemented**

The interactable must implement the interaction logic. Open the interactable blueprint and implement the function `Call Interact`. Add the gameplay logic you want to trigger when the player interacts.

## Outlines Are Not Showing

**1. Custom Depth Must Be Enabled**

`Project Settings - Rendering - Custom Depth Stencil Pass - Enabled with Stencil`

**2. Outlines Must Be Enabled in the Interaction Component**

Inside `AC_BNInteractionSystem`, ensure Enable Outlines = True.

## Interaction Widget Does Not Display Correctly

**1. Common UI Plugin**

Ensure the Common UI plugin is enabled.

**2. Game Viewport Client**

`Project Settings - Engine - General Settings - Game Viewport Client Class - CommonGameViewportClient`

**3. Controller Data Assets**

Ensure the provided Keyboard and Controller data assets are added to the Common Input settings. Without these the UI may not display the correct input icons.

## Interactions Work in Singleplayer but Not Multiplayer

**1. Interaction Logic Running Only on Client**

Gameplay logic should run on the server. If your interaction changes the world state ensure the logic runs through the server.

**2. Replication Not Enabled**

If the interaction modifies actors ensure the actor has Replicates = Enabled.

## Interactable Remains After Actor Is Destroyed

Ensure the actor is properly destroyed using `Destroy Actor`. The prompt actor will automatically clean itself up when the interactable is removed.

## Bug Reports

Report bugs in the Brightnode Studio Discord in the **#bugs-interaction-system** channel.

Please include Unreal Engine version, steps to reproduce, and screenshots or video where possible.

💬 [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
