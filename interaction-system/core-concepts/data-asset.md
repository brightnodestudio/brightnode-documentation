# Interaction Types

The Brightnode Interaction System supports multiple interaction types, each designed for a different style of player input and gameplay behaviour.

The selected interaction type is configured through the Interaction Definition Data Asset.

***

### Press

**Press** is the simplest interaction type.

The interaction executes when the player presses the interaction input while focusing a valid interactable actor.

Typical uses include:

* Opening doors
* Activating switches
* Picking up items
* Triggering dialogue
* Using terminals
* Starting scripted events

The interaction flow is:

`Focus Actor → Press Input → Interaction Executes`

Use Press when the interaction should happen immediately.

***

### Hold To Complete

**Hold To Complete** requires the player to hold the interaction input for a configured duration.

The interaction completes once the required hold time has been reached.

Typical uses include:

* Reviving another player
* Unlocking an object
* Searching containers
* Repairing equipment
* Activating machinery
* Performing deliberate long-form actions

The interaction flow is:

`Focus Actor → Hold Input → Progress Updates → Duration Reached → Interaction Completes`

If the player releases the input before completion, the interaction can be cancelled based on the configured behaviour.

Hold To Complete works well for actions where the player should commit for a set amount of time before the gameplay event occurs.

***

### While Holding

**While Holding** remains active for as long as the player continues holding the interaction input.

Unlike Hold To Complete, there is no requirement to reach a fixed completion point.

Typical uses include:

* Continuously operating a control
* Charging or maintaining an action
* Holding a lever in position
* Running a machine while input is held
* Continuous gameplay effects

The interaction flow is:

`Focus Actor → Hold Input → Interaction Starts → Remains Active → Release Input → Interaction Ends`

Use While Holding when gameplay should remain active only while the interaction input is being held.

***

### Grab

**Grab** is used for interactable objects that the player can pick up and manipulate.

The system handles the interaction lifecycle required to begin and end a grab while exposing the necessary events for actor-specific behaviour.

Typical uses include:

* Picking up physics objects
* Moving environmental props
* Carrying objects
* Physics-based puzzles
* Object inspection or manipulation

The interaction flow is:

`Focus Actor → Interact → Grab Begins → Object Is Manipulated → Release / Drop`

Grab-specific behaviour is configured through the Interaction Definition.

***

### Choosing an Interaction Type

Choose the type based on how the player should interact with the object.

| Interaction Type | Best Used For                           |
| ---------------- | --------------------------------------- |
| Press            | Immediate actions                       |
| Hold To Complete | Timed interactions that must finish     |
| While Holding    | Actions active only while input is held |
| Grab             | Picking up and manipulating objects     |

The interaction type defines the input and lifecycle behaviour.

The actor itself still determines the gameplay result.

***

### Shared Interaction Behaviour

All interaction types use the same core framework for:

* Focus detection
* Interaction prompts
* Interaction Definitions
* Interaction state
* Multiplayer execution
* Locking
* Gameplay events

This means actors can use different interaction styles without requiring separate interaction systems.

***

### Prompt Behaviour

The prompt system automatically adapts to the active interaction type.

Depending on the configuration, the prompt can display:

* Interaction text
* Input icons
* Hold progress
* Active interaction state
* Visibility changes during sustained interactions

This allows the player to clearly understand how each interaction should be performed.
