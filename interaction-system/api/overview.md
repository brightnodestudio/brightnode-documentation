# Interaction State

Interaction State represents the current stage of an active interaction.

The Interaction System uses state to keep gameplay behaviour, prompt presentation, sustained interactions, and multiplayer updates synchronised.

***

### State Overview

As an interaction progresses, the system updates its current state.

These state changes allow other parts of the system to respond consistently without needing to directly manage the full interaction flow.

Interaction State can be used to drive:

* Interaction start and end behaviour
* Sustained interaction progress
* Prompt visibility
* Completion
* Cancellation
* Multiplayer synchronisation
* Gameplay events

***

### Interaction Lifecycle

A typical interaction lifecycle follows this flow:

`Focused → Interaction Starts → Interaction Active → Interaction Completes or Cancels → Returns to Idle`

The exact lifecycle depends on the selected Interaction Type.

For example, a Press interaction may complete immediately, while a Hold To Complete interaction remains active until its required duration is reached.

***

### Starting an Interaction

When the player begins interacting with a valid focused actor, the system updates the current interaction state.

This allows the system to:

* Mark the interaction as active
* Notify the interactable actor
* Update the prompt
* Begin sustained interaction behaviour
* Replicate the new state where required

The actor can then respond through the exposed interaction events.

***

### Active Interaction

While an interaction is active, the system maintains the state required by the selected interaction type.

For sustained interactions, this can include:

* Tracking interaction progress
* Updating UI
* Maintaining hold behaviour
* Monitoring cancellation conditions
* Keeping the actor locked if required

The active state continues until the interaction completes, ends, or is cancelled.

***

### Completing an Interaction

An interaction enters its completed state when its required conditions have been met.

For example:

* A Press interaction executes immediately
* A Hold To Complete interaction reaches its required duration
* A gameplay condition confirms successful completion

When completion occurs, the system can:

* Trigger completion events
* Update the prompt
* Release interaction locks
* Replicate the completed state
* Return the interaction to its resting state

***

### Cancelling an Interaction

An active interaction can be cancelled before completion.

Cancellation can occur when:

* The player releases the input early
* Focus is lost
* The actor becomes unavailable
* Another gameplay condition invalidates the interaction
* The server rejects the interaction

When cancelled, the system stops the active interaction and updates the relevant state and presentation.

***

### State and Interaction Types

Different interaction types use state differently.

#### Press

Press interactions generally move through the lifecycle immediately.

`Start → Execute → Complete`

#### Hold To Complete

Hold To Complete remains active while progress is accumulated.

`Start → Active → Progress → Complete`

If interrupted:

`Start → Active → Cancel`

#### While Holding

While Holding remains active for as long as the input is held.

`Start → Active → End`

#### Grab

Grab uses state to track when an object is being actively held or released.

`Start → Grab Active → Release`

***

### State and Prompts

Interaction State directly affects prompt presentation.

For example, the prompt can:

* Show when focus begins
* Update while an interaction is active
* Display hold progress
* Hide while interacting
* Return after completion
* Hide when the interaction ends

This allows the UI to react to the interaction lifecycle automatically.

***

### State Events

State changes are exposed through the system's events and dispatchers.

These can be used by gameplay Blueprints to react to changes in the interaction lifecycle without needing to track the state manually.

For example, an actor could respond when:

* Interaction begins
* Interaction becomes active
* Interaction completes
* Interaction is cancelled
* Interaction ends

The exact events available are documented in the API Reference.

***

### Multiplayer State

In multiplayer, interaction state is handled through the system's replicated flow.

Gameplay-authoritative state changes occur on the server and are replicated to clients where required.

Replicated state updates allow client-side systems such as UI and presentation to stay synchronised with the authoritative interaction state.

A typical multiplayer state flow is:

`Client Interaction Request → Server Updates State → State Replicates → Client Responds`

***

### RepNotify Behaviour

Replicated interaction state can use RepNotify to trigger local updates when the value changes.

This is particularly useful for:

* Prompt updates
* Interaction presentation
* State-driven events
* Client-side feedback

For RepNotify behaviour to work correctly, the component holding the replicated state must itself be configured to replicate.
