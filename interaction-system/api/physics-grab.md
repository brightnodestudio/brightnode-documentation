# Grab Interactions

Grab interactions allow the player to pick up and manipulate physics-enabled objects using the same Interaction System used for standard interactions.

Grab behaviour is configured through the Interaction Definition and handled through the normal focus, interaction, locking, and multiplayer flow.

***

### Overview

A Grab interaction begins when the player interacts with an actor configured to use the Grab interaction type.

The basic flow is:

`Focus Object → Interact → Grab Begins → Object Is Held → Interaction Ends → Object Is Released`

The Interaction System manages the grab lifecycle, while Unreal Engine physics controls the physical movement of the grabbed object.

***

### Creating a Grabbable Actor

To make an actor grabbable:

1. Add an Interactable Component to the actor.
2. Assign an Interaction Definition configured to use the **Grab** interaction type.
3. Ensure the actor can be detected by the `Interaction` trace channel.
4. Enable **Simulate Physics** on the component that will be grabbed.
5. Ensure the grabbed component has a valid physics mass.

No dedicated grab actor class is required.

Any suitable actor can participate in Grab interactions by using the standard Interactable Component.

***

### Physics Requirements

Grab interactions rely on Unreal Engine physics.

The component being grabbed must have:

* **Simulate Physics** enabled
* Collision enabled
* A valid physics mass
* Collision configured to block the `Interaction` trace channel

The object's mass affects how it behaves while being grabbed and manipulated.

Mass can be controlled through the component's normal Unreal Engine physics settings, including its calculated mass or **Mass Override**.

If **Simulate Physics** is disabled, the component cannot behave as a physics-based grabbed object.

If the component does not have an appropriate mass, the grab behaviour may not respond as expected.

***

### Grab Behaviour

When the player interacts with a valid grabbable actor, the system begins the Grab interaction.

While the interaction remains active, the physics-enabled component is held and manipulated according to the configured grab behaviour.

When the interaction ends, the component is released and returns to normal physics behaviour.

A typical flow is:

`Grab Starts → Physics Object Held → Player Manipulates Object → Grab Ends → Physics Object Released`

***

### Interaction Definition

Grab-specific behaviour is configured through the Interaction Definition Data Asset.

This allows the same grab configuration to be reused across multiple actors.

For example, multiple physics props can share the same Grab Interaction Definition while retaining their own:

* Mesh
* Collision
* Mass
* Physics properties
* Gameplay behaviour

This keeps grab configuration separate from the actor itself.

***

### Focus Behaviour

Before an object can be grabbed, it must first become the player's focused interactable.

The normal focus flow still applies:

`Trace Hit → Validate Interactable → Gain Focus → Show Prompt → Grab`

This means Grab interactions use the same focus presentation as other interaction types, including:

* Interaction prompts
* Input icons
* Focus outlines
* Custom interaction text

***

### Releasing an Object

A grabbed object is released when the Grab interaction ends.

Depending on the interaction flow, this can happen when:

* The player releases the interaction
* The interaction is ended manually
* The grab becomes invalid
* The player can no longer maintain the interaction
* The server ends the interaction

Once released, the component returns to normal physics behaviour.

***

### Interaction Interface

Grab interactions can still use the Interaction Interface to trigger actor-specific gameplay behaviour.

This allows the actor to respond to the grab without placing custom gameplay logic inside the Interaction System.

For example, an actor could:

* Play a sound when grabbed
* Change material while held
* Enable or disable an effect
* Update gameplay state
* Notify another gameplay system

The Interaction System manages the grab lifecycle, while the actor remains responsible for any additional gameplay behaviour.

***

### Interaction Locking

Grab interactions typically require exclusive access.

When interaction locking is enabled, only one player can actively grab the object at a time.

For example:

`Player A Grabs Object → Object Locks`

`Player B Attempts Grab → Request Rejected`

`Player A Releases Object → Lock Released`

This prevents multiple players from attempting to control the same physics object simultaneously.

***

### Multiplayer Behaviour

Grab interactions use the same server-authoritative interaction flow as other interaction types.

A typical multiplayer flow is:

`Client Requests Grab → Server Validates → Grab Begins → State Replicates → Grab Ends`

The Interaction System handles the interaction request, state, and locking.

The grabbed actor and its physics behaviour should still be configured using Unreal Engine's normal replication rules where required.

For multiplayer projects, ensure the relevant actor and components are configured appropriately if their movement or physics state needs to be visible to other clients.

***

### Common Uses

Grab interactions are suitable for:

* Physics props
* Puzzle objects
* Moveable environmental objects
* Carryable items
* Object inspection
* Physics-based gameplay

Because Grab uses the same interaction framework as the rest of the system, grabbed objects still benefit from focus detection, prompts, outlines, Interaction Definitions, locking, and multiplayer support.
