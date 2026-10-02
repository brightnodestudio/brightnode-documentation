# Focus & Detection

Focus detection determines which interactable actor the player is currently targeting.

The Player Interaction Component handles this process automatically using the configured Interaction trace channel.

***

### Interaction Trace

The Player Interaction Component performs a trace from the player's configured interaction origin.

The trace uses the custom:

`Interaction`

trace channel.

Only actors that block this channel can be detected.

This keeps interaction detection separate from other gameplay collision such as Visibility or Camera traces.

***

### Collision Requirements

For an actor to be detected, at least one of its collision-enabled components must block the `Interaction` trace channel.

For example:

* Static Mesh Component
* Skeletal Mesh Component
* Box Collision
* Sphere Collision
* Capsule Collision

If the trace passes through the actor, the actor cannot become focused.

***

### Detecting Interactable Actors

When the interaction trace hits an actor, the system checks whether that actor contains a valid Interactable Component.

If a valid component is found, the actor can become the player's current focused actor.

The Interactable Component contains the configuration required for the Interaction System to determine how that actor should behave.

***

### Current Focus

The Player Interaction Component tracks the actor that is currently focused.

Only one actor is treated as the active focus target at a time.

When focus changes, the system updates the relevant interaction presentation and runtime state.

A typical focus flow is:

`Trace Hit → Validate Interactable → Set Focus → Show Prompt / Outline`

***

### Gaining Focus

When an actor becomes focused, the system can respond by:

* Displaying the interaction prompt
* Applying the configured outline
* Updating interaction text
* Updating the displayed input icon
* Preparing the actor for interaction
* Firing focus-related events

Focus does not automatically execute the interaction.

It only determines which actor is currently available to interact with.

***

### Losing Focus

Focus is removed when the current actor is no longer a valid interaction target.

This can happen when:

* The player looks away
* The actor moves outside the interaction trace
* Collision no longer blocks the Interaction channel
* The actor becomes unavailable
* Another interactable actor becomes the active focus target

When focus is lost, the system removes any presentation associated with that actor.

This can include:

* Hiding the interaction prompt
* Removing the focus outline
* Clearing focus-related state
* Firing focus lost events

***

### Focus and Interaction

Focus determines which interactable actor receives the player's interaction request.

The basic flow is:

`Detect Actor → Gain Focus → Player Interacts → Focused Actor Handles Interaction`

If no valid actor is focused, no interaction is executed.

***

### Local Focus

Focus detection is primarily a local player responsibility.

Each player determines their own focused actor independently.

This means multiple players can look at different interactable actors at the same time without affecting each other's UI or focus presentation.

Gameplay-affecting interaction execution is handled separately through the multiplayer interaction flow.

***

### Focus Presentation

Focus can drive visual feedback such as:

* Interaction prompts
* Object outlines
* Context-sensitive text
* Input icons

These presentation systems are kept separate from the actor's gameplay logic.

The actor does not need to manually manage prompt or outline behaviour each time focus changes.

***

### Debugging Focus

If an actor is not being detected, check the following:

* The actor has an Interactable Component
* The Interactable Component has a valid Interaction Definition
* The actor's collision blocks the `Interaction` trace channel
* The actor is within the configured interaction distance
* The interaction trace is hitting the expected collision component

Using the system's debug tools can help confirm whether the trace is reaching the actor and what the system is detecting.
