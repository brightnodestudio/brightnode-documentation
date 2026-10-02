# Architecture Overview

The Brightnode Interaction System is built around a small set of modular components, each with a clearly defined responsibility.

The goal is to keep interaction detection, gameplay execution, presentation, and multiplayer logic separate so the system can be reused across many different actor types and gameplay scenarios.

### System Overview

At a high level, the interaction flow is:

`Player Interaction Component → Focused Interactable → Interaction Definition → Interaction Execution → Prompt / State Updates`

Each part of the system handles a specific layer of the interaction process.

### Player Interaction Component

The Player Interaction Component is added to the player Character or Pawn.

It is responsible for player-side interaction behaviour, including:

* Performing interaction traces
* Detecting valid interactable actors
* Managing the currently focused actor
* Handling interaction requests
* Tracking interaction state
* Managing sustained interactions
* Updating interaction prompts
* Handling client and server interaction flow

The player component acts as the main runtime controller for interaction.

### Interactable Component

The Interactable Component is added to any actor that should support interaction.

It is responsible for defining that actor as interactable and exposing the events used to connect the Interaction System to gameplay logic.

Any Actor Blueprint can become interactable simply by adding this component.

This avoids the need for dedicated interactable parent classes and allows the system to work with existing gameplay actors.

### Interaction Definition

Each Interactable Component references an Interaction Definition Data Asset.

The Interaction Definition controls how the interaction behaves and how it is presented to the player.

It contains settings such as:

* Interaction type
* Interaction timing
* Prompt information
* Interaction behaviour
* Sustained interaction settings
* Grab settings
* Outline and presentation settings

Using Data Assets keeps interaction configuration separate from actor logic and allows the same interaction setup to be reused across multiple actors.

### Focus & Detection

The Player Interaction Component performs traces using the `Interaction` trace channel.

When a valid interactable actor is detected, it becomes the player's current focus.

Focus controls presentation and determines which actor will receive the next interaction request.

Typical focus behaviour includes:

* Showing the interaction prompt
* Applying focus highlighting
* Updating prompt information
* Removing presentation when focus is lost

Focus is handled independently from the gameplay action performed by the actor.

### Interaction Execution

When an interaction is triggered, the Interaction System determines how that interaction should behave based on its Interaction Definition.

Examples include:

* Instant
* Timed
* Sustained
* Grab

The system manages the interaction lifecycle, while the interactable actor responds through its events or dispatchers.

This means the Interaction System controls **when** an interaction happens, while the actor controls **what** the interaction does.

### Interaction Prompts

Interaction prompts are handled separately from gameplay logic.

The prompt system uses the active Interaction Definition to determine what should be displayed to the player.

Prompt behaviour can include:

* Interaction text
* Input icons
* Hold progress
* Visibility changes
* State-based updates
* Hiding during sustained interactions

This keeps UI presentation decoupled from the interactable actor itself.

### Interaction State

The system tracks the current runtime state of an interaction so other parts of the system can respond consistently.

Interaction state is used for things such as:

* Starting interactions
* Sustained interaction progress
* Completion
* Cancellation
* Prompt presentation
* Multiplayer synchronisation

State changes can be observed through the system's exposed events and dispatchers.

### Multiplayer Architecture

The Interaction System is designed around server-authoritative execution.

A typical multiplayer flow is:

`Local Focus → Local Input → Server Request → Server Validation → Interaction Execution → Replicated State`

Focus and prompt presentation are primarily local to the player.

Gameplay-affecting interaction execution is handled through the server.

This keeps interaction feedback responsive while ensuring gameplay actions remain authoritative in multiplayer.

### Separation of Responsibilities

The system is designed so each layer has a single primary responsibility:

| System                       | Responsibility                                    |
| ---------------------------- | ------------------------------------------------- |
| Player Interaction Component | Detection and interaction control                 |
| Interactable Component       | Makes an actor interactable                       |
| Interaction Definition       | Configures interaction behaviour                  |
| Prompt System                | Displays interaction feedback                     |
| Actor Gameplay Logic         | Determines the gameplay result                    |
| Server                       | Validates and executes authoritative interactions |

This separation makes the system easier to extend and allows interaction behaviour to be added to existing actors without restructuring their gameplay logic.
