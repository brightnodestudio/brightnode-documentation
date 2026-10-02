# Quick Start Guide

This guide covers the minimum setup required to create your first working interaction.

By the end, you will have a player that can detect, focus, and interact with an actor in the level.

### 1. Add the Interaction Component to Your Player

Open your player Character or Pawn Blueprint and add the Brightnode Interaction Component.

The Interaction Component handles the player-side interaction flow, including:

* Focus detection
* Interaction requests
* Interaction state
* Prompt handling
* Multiplayer interaction flow

Once added, check the details pannel and setup the config section as you require, the component can then begin detecting interactable actors using the configured Interaction trace channel.

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

### 2. Create an Interaction Definition

Create a new Interaction Definition Data Asset.

In the Content Browser:

`Right Click → Miscellaneous → Data Asset`

Select the DA\_Interactable class.

The Interaction Definition controls how the interaction behaves and how it is presented to the player.

For your first interaction, use a simple **Instant** interaction.

### 3. Make an Actor Interactable

Open any Actor Blueprint that you want the player to interact with.

Add the Brightnode Interactable Component.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Implement the BPI\_Interactable Interface.

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Assign your Interaction Definition Data Asset to the component.

Any Actor Blueprint can become interactable by adding the component. No dedicated interactable parent class is required.

### 4. Check Collision

The actor must have collision that blocks the `Interaction` trace channel.

Select the mesh or collision component that should be detected and confirm that its collision response to `Interaction` is set to:

`Block`

If the interaction trace cannot hit the actor, the actor cannot be focused or interacted with.

### 5. Respond to the Interaction

Use the Interactable Component's events or dispatchers to execute your gameplay logic.

For example, an interaction could:

* Open a door
* Activate a switch
* Pick up an item
* Trigger dialogue
* Start an animation
* Call another gameplay system

The Interaction System determines when the interaction occurs.

Your actor determines what happens when it does.

### 6. Test the Interaction

Compile and save your Blueprints, then place the interactable actor in the level.

Start the game and look at the actor.

When the actor is detected:

* It becomes focused
* The interaction prompt appears
* The configured focus outline can be displayed
* The actor can respond to interaction events

The basic runtime flow is:

`Detect → Focus → Prompt → Interact → Execute`
