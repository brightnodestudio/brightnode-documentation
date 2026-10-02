# Interaction Interface

The Brightnode Interaction System communicates with interactable actors through an Interaction Interface.

Actors implement the interface functions they need and use them to connect the Interaction System to their own gameplay logic.

This keeps gameplay behaviour separate from the core Interaction System.

***

### Overview

The Interaction System manages detection, interaction state, timing, networking, and presentation.

When gameplay needs to respond to an interaction, the appropriate Interface function is called on the actor being interacted with.

A typical flow is:

`Player Interacts → Interaction System Processes Interaction → Interface Function Called → Actor Executes Gameplay Logic`

The actor determines what the interaction actually does.

***

### Available Interaction Functions

The Interaction Interface provides the following gameplay-facing functions:

* `Call Interact`
* `Sustained Interaction Start`
* `Sustained Interaction End`
* `Hold Interaction Started`

Implement these functions inside any interactable actor that needs to respond to the corresponding interaction behaviour.

***

### Call Interact

`Call Interact` is the primary interaction callback.

Use this for gameplay that should execute when the interaction itself is triggered.

Typical uses include:

* Opening a door
* Activating a switch
* Picking up an item
* Triggering dialogue
* Using a terminal
* Starting an event

For a simple Press interaction, this is typically where the main gameplay behaviour is implemented.

Example:

`Call Interact → Open Door`

***

### Sustained Interaction Start

`Sustained Interaction Start` is called when a sustained interaction begins.

Use this for gameplay that needs to start when the player begins actively interacting.

Typical uses include:

* Starting machinery
* Beginning an animation
* Starting an audio effect
* Beginning a continuous gameplay action
* Activating an effect while interaction is maintained

Example:

`Sustained Interaction Start → Start Machine`

***

### Sustained Interaction End

`Sustained Interaction End` is called when an active sustained interaction ends.

Use this to stop or clean up behaviour that was started by `Sustained Interaction Start`.

Typical uses include:

* Stopping machinery
* Ending an animation
* Stopping audio
* Removing a gameplay effect
* Ending continuous behaviour

Example:

`Sustained Interaction End → Stop Machine`

Together, these functions provide a simple start and stop lifecycle:

`Sustained Interaction Start → Interaction Active → Sustained Interaction End`

***

### Hold Interaction Started

`Hold Interaction Started` is used by hold-based interaction behaviour.

It provides a callback when the player begins the hold interaction, allowing the actor to react before the interaction reaches its completion condition.

Typical uses include:

* Starting a hold animation
* Playing interaction feedback
* Beginning actor-specific presentation
* Preparing gameplay behaviour while the hold progresses

The completed gameplay action can then be handled separately when the interaction successfully completes.

***

### Implementing the Interface

Open the Blueprint for the actor that should respond to an interaction.

Under:

`Class Settings → Implemented Interfaces`

add the Brightnode Interaction Interface.

The available Interface functions can then be implemented within the actor Blueprint.

You only need to implement the functions relevant to that actor.

For example, a simple door using a Press interaction may only need:

`Call Interact`

while a continuously operated machine could use:

`Sustained Interaction Start`

and:

`Sustained Interaction End`

***

### Interaction Component and Interface

The Interactable Component determines that the actor can participate in the Interaction System.

The Interface determines how the actor responds when interaction events occur.

These responsibilities remain separate:

| System                 | Responsibility                                      |
| ---------------------- | --------------------------------------------------- |
| Interactable Component | Makes the actor available to the Interaction System |
| Interaction Definition | Configures how the interaction behaves              |
| Interaction Interface  | Passes interaction events to the actor              |
| Actor Blueprint        | Executes the actual gameplay logic                  |

***

### Custom Prompt Text

The Interaction Interface is also used when an Interaction Definition has **Use Custom Text** enabled.

In this case, the Interaction System asks the focused actor for its interaction text through the appropriate Interface function rather than using the default text stored in the Interaction Definition.

This allows actors to provide dynamic text such as:

`Open` / `Close`

or:

`Turn On` / `Turn Off`

based on their current gameplay state.

***

### Recommended Workflow

A typical interactable actor follows this pattern:

`Add Interactable Component → Assign Interaction Definition → Implement Interaction Interface → Add Gameplay Logic`

The Interaction System handles the interaction framework, while the actor remains responsible for its own gameplay behaviour.
