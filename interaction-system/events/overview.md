# Swapping Interaction Definitions at Runtime

Interaction Definitions can be changed at runtime to alter how an actor behaves after its gameplay state changes.

This allows the same actor to move between completely different interaction types without replacing the actor, changing its parent class, or rebuilding its interaction logic.

***

### Overview

An Interactable Component does not need to use the same Interaction Definition for the entire lifetime of the actor.

The active Data Asset can be replaced at runtime whenever the actor's gameplay state changes.

For example, an object might initially require a timed repair interaction, then switch to a simple Press interaction once it has been repaired.

The flow could be:

`Broken → Hold To Repair → Repair Completes → Swap Interaction Definition → Press To Use`

This makes Interaction Definitions useful not only for configuration, but also for representing different interaction states of the same actor.

***

### Repair Example

The Showcase repair cogs example demonstrates this pattern.

While the machine is broken, it uses a repair-focused Interaction Definition configured as a timed interaction.

The player must hold the interaction input until the repair completes.

The initial behaviour is:

`Focus Machine → Hold To Repair → Progress Completes → Machine Repaired`

Once the repair succeeds, the actor swaps its active Interaction Definition.

The new definition uses an instant Press interaction and allows the player to turn the repaired machine on and off.

The resulting flow becomes:

`Repair Definition → Repair Completes → Swap Definition → On / Off Definition`

The actor itself has not changed.

Only the Interaction Definition controlling its current behaviour has changed.

***

### Why Swap Interaction Definitions?

Swapping Data Assets allows an actor's interaction behaviour to evolve with gameplay state.

A new Interaction Definition can change things such as:

* Interaction type
* Prompt text
* Hold duration
* Prompt visibility
* Outline presentation
* Sustained interaction behaviour
* Grab behaviour
* Other interaction-specific configuration

This avoids filling a single Interaction Definition with large amounts of conditional behaviour.

Instead, each Data Asset can represent one clear interaction state.

***

### Example State Setup

A repairable machine could use two Interaction Definitions:

#### Broken State

`DA_Interaction_RepairMachine`

Configured with:

* Hold To Complete
* Repair prompt text
* Repair hold duration
* Hold progress display

#### Repaired State

`DA_Interaction_UseMachine`

Configured with:

* Press
* Instant interaction
* On / Off prompt behaviour
* No repair progress

When the repair completes, the actor changes from the first definition to the second.

***

### Runtime Flow

A typical runtime Data Asset swap looks like:

`Interaction Completes → Update Gameplay State → Assign New Interaction Definition`

Once the new definition is assigned, future interaction behaviour uses the new configuration.

For example:

`Broken Machine`

↓

`Hold Interaction Started`

↓

`Repair Completes`

↓

`Set Repaired = True`

↓

`Assign Use Machine Interaction Definition`

↓

`Player Can Now Press To Turn Machine On / Off`

***

### Dynamic Prompt Behaviour

Changing the Interaction Definition also allows the prompt to change alongside the gameplay state.

Before repair:

`Hold to Repair`

After repair:

`Turn On`

Once running:

`Turn Off`

The actor can combine Data Asset swapping with **Use Custom Text** when even more dynamic prompt behaviour is required.

For example, the repaired machine can retain the same Press Interaction Definition while the actor's Interface function dynamically returns either:

`Turn On`

or:

`Turn Off`

depending on its current state.

This allows the two techniques to work together:

* Swap Interaction Definitions when the interaction behaviour itself changes.
* Use Custom Text when only the displayed action text needs to change.

***

### When to Swap Definitions

Runtime Data Asset swapping is useful when an actor moves between substantially different interaction behaviours.

Examples include:

* Broken → Repaired
* Locked → Unlocked
* Empty → Filled
* Inactive → Operational
* Repair → Use
* Assemble → Activate
* Search → Collect
* Disabled → Interactive

If only the prompt text changes but the interaction behaviour remains the same, using **Custom Text** may be simpler.

If the interaction type, timing, presentation, or behaviour changes, swapping the Interaction Definition is usually the cleaner approach.

***

### Keeping Actor Logic Separate

The actor should still own its gameplay state.

For example, the machine decides whether it is:

`Broken`

`Repaired`

`Running`

The Interaction Definition only controls how the player interacts with that current state.

This maintains the separation between gameplay state and interaction configuration.

A useful way to think about it is:

| Actor                       | Interaction Definition               |
| --------------------------- | ------------------------------------ |
| What state am I in?         | How can the player interact with me? |
| Am I repaired?              | Hold or Press?                       |
| Am I powered on?            | What prompt should be shown?         |
| What gameplay happens next? | How should the interaction behave?   |

***

### Multiplayer Considerations

In multiplayer projects, the gameplay state that determines which Interaction Definition should be active should remain authoritative.

If a repair completes on the server, the server should update the relevant gameplay state and ensure clients receive the resulting interaction configuration where required.

This keeps all players synchronised with the actor's current interaction behaviour.

***

### Recommended Pattern

For actors with multiple interaction states:

1. Create a separate Interaction Definition for each substantially different behaviour.
2. Keep the actor's actual gameplay state inside the actor.
3. Swap the active Interaction Definition when that gameplay state changes.
4. Use Custom Text for smaller presentation changes that do not require a different interaction behaviour.

This keeps each Interaction Definition focused, reusable, and easy to understand.

***

### Example

A complete repairable machine flow could be:

`Broken`

↓

`DA_Repair`

↓

`Hold To Complete`

↓

`Repair Completed`

↓

`Set Machine Repaired`

↓

`Swap To DA_UseMachine`

↓

`Press`

↓

`Turn On / Turn Off`

This pattern can be reused anywhere an interactable actor changes how the player should interact with it over time.
