# Quick Start Guide

This guide walks you through setting up a basic Press to Interact system. The entire setup takes only a few minutes and works in both singleplayer and multiplayer.

## 1. Create an Interactable Actor

Create a new Blueprint inheriting from **BP\_BaseInteractable**.

## 2. Create an Interaction Data Asset

Create a new Data Asset using **DA\_Interactable** and configure:

- Interaction type — set to Press for this guide
- UI text
- Icons
- Interaction behaviour settings

## 3. Apply the Data Asset

Open your Interactable Blueprint and assign the DA\_Interactable you created.

## 4. Add a Mesh

Add a mesh component to your interactable blueprint. Ensure the mesh collision blocks the **Interaction** trace channel.

## 5. Place the Actor in the World

Drag your interactable blueprint into the level.

## 6. Setup the Player Character

Open your Character Blueprint and add the component **AC\_BNInteractionSystem**.

Configure:

- **Focus Trace Settings** - controls the forward interaction trace
- **Radius Scan Settings (Optional)** - detects nearby interactables not directly looked at
- **Outline Settings (Optional)** - highlights interactables when focused

## 7. Setup the Player Controller

Add the **Interaction Mapping Context** to your input system in the Player Controller.

## 8. Implement Interaction Logic

Open your Interactable Blueprint and implement the interface function **Call Interact**. Add the gameplay logic you want to trigger — opening a door, picking up an item, activating a switch.

## Result

When the player looks at the interactable:

- The interaction prompt appears with the correct input icon
- The object highlights if outlines are enabled
- Pressing the interaction key triggers the Call Interact logic
