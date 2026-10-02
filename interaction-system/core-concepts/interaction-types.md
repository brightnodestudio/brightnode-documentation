# Interaction Defenitions

Interaction Definitions are Data Assets used to configure how an interaction behaves and how it is presented to the player.

They allow interaction behaviour to be reused across multiple actors without duplicating setup inside individual Blueprints.

***

### What Is an Interaction Definition?

Each Interactable Component references an Interaction Definition Data Asset.

The definition contains the configuration required by the Interaction System, including behaviour, timing, prompt presentation, outline settings, and interaction-specific options.

The actor itself remains responsible for the gameplay result.

For example, multiple doors can share the same Interaction Definition while each door still controls its own opening logic.

***

### Creating an Interaction Definition

In the Content Browser:

`Right Click → Miscellaneous → Data Asset`

Select the DA\_Interactable class.

Give the asset a descriptive name based on its intended use.

Examples:

* `DA_Interaction_OpenDoor`
* `DA_Interaction_Pickup`
* `DA_Interaction_HoldLever`
* `DA_Interaction_GrabObject`

The same definition can be assigned to multiple Interactable Components.

***

### Assigning a Definition

Select the Interactable Component on an actor and assign the desired Interaction Definition.

Once assigned, the component uses the settings from that Data Asset whenever the player focuses or interacts with the actor.

Changing the Data Asset updates every actor using that definition.

This makes it easy to maintain consistent behaviour across large numbers of interactable actors.

***

### Interaction Behaviour

The Interaction Definition determines the interaction type used by the component.

Supported interaction types include:

* Press
* Hold To Complete
* While Holding
* Grab

Each type uses the same core interaction framework while providing different runtime behaviour.

Interaction types are covered in more detail on the **Interaction Types** page.

***

### Prompt Configuration

The Interaction Definition also controls how the interaction is presented to the player.

Prompt settings can define information such as:

* Interaction text
* Input presentation
* Prompt visibility
* Sustained interaction progress
* Whether the prompt should remain visible while interacting

This allows presentation to be configured independently from actor gameplay logic.

***

### Outline Configuration

Interaction Definitions can control the outline presentation used when an actor becomes focused.

This allows different interaction types or actor categories to use different visual feedback without modifying the actor Blueprint.

Outline highlighting requires Custom Depth Stencil to be enabled in the project settings.

***

### Sustained Interaction Settings

Hold-based interactions include additional configuration for behaviour over time.

Depending on the interaction type, this can include settings such as:

* Interaction duration
* Progress behaviour
* Completion behaviour
* Cancellation behaviour
* Prompt visibility during interaction

These settings allow sustained interactions to be configured entirely through the Data Asset.

***

### Grab Configuration

Grab interactions expose additional settings used when interacting with movable objects.

These settings control the behaviour required by the Grab interaction type while keeping grab configuration separate from the actor's gameplay Blueprint.

Grab behaviour is covered in more detail on the **Interaction Types** page.

***

### Reusing Interaction Definitions

A major benefit of Interaction Definitions is reuse.

For example, a single `Open Door` definition can be shared by every door in a project while each door retains its own individual gameplay logic.

This keeps common interaction behaviour centralised and makes global changes much easier.

Instead of updating dozens of actors individually, update the Interaction Definition once.

***

### Data Driven Workflow

A typical workflow is:

`Create Definition → Configure Behaviour → Assign to Actor → Bind Gameplay Logic`

This keeps interaction configuration separate from gameplay implementation.

The result is a cleaner, more scalable workflow as the number of interactable actors increases.
