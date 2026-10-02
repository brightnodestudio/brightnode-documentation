# Brightnode Outline System Integration

The Brightnode Interaction System includes a simple demonstration outline system for focused actors.

If you are also using the **Brightnode Outline System**, the built-in focus outline logic can be replaced so interaction focus is handled directly through the full Outline System.

This integration is optional and requires both systems to be installed in the same project.

***

### Requirements

Before beginning, make sure your project contains:

* Brightnode Interaction System
* Brightnode Outline System
* Interaction Component on the player Character or Pawn
* Brightnode Outline System Player Component on the player
* Valid Outline presets configured in the Outline System

The Interaction System continues to handle focus detection.

The Outline System becomes responsible for applying and removing the actual visual outline.

***

### Integration Overview

The integration uses a Gameplay Tag supplied by the interactable actor.

That tag tells the Outline System which Outline preset should be applied.

The basic flow is:

`Actor Gains Focus → Get Outline Tag → Outline System Finds Preset → Apply Outline`

When focus is lost:

`Actor Loses Focus → Remove Outline`

This keeps the two systems separate.

The Interaction System only determines which actor is focused.

The Outline System determines how that actor should look.

***

### 1. Add the Outline System Component to the Player

Open your player Character or Pawn.

Make sure it contains the Brightnode Outline System Player Component.

The Interaction Component retrieves this component at runtime and uses it when applying or removing focus outlines.

Both components should therefore exist on the same player actor.

***

### 2. Create an Outline Tag Interface Function

Open the Interaction Interface used by your interactable actors.

Create a new function:

`GetOutlineTag`

Add an output:

| Setting | Value         |
| ------- | ------------- |
| Name    | `Outline Tag` |
| Type    | Gameplay Tag  |

This function allows every interactable actor to tell the Interaction System which Outline preset it wants to use.

The function does not apply the outline itself.

It only returns the Gameplay Tag required by the Outline System.

***

### 3. Add an Outline Tag to the Interactable Actor

Open the Blueprint for an interactable actor.

Create a new variable:

`OutlineTag`

Set its type to:

`Gameplay Tag`

Choose the tag that corresponds to the Outline preset you want this actor to use.

For example:

`Outline.Interactable`

or any tag configured within your Outline System.

The exact tag structure is determined by your project's Outline System setup.

***

### 4. Implement GetOutlineTag

Implement the `GetOutlineTag` Interface function on the interactable actor.

Return the actor's `OutlineTag` variable directly from the function.

The flow is simply:

`GetOutlineTag → Return OutlineTag`

This allows each interactable actor to provide its own Outline preset without the Interaction Component needing to know anything about that actor's visual setup.

Different actors can therefore return different tags while using the same Interaction System.

***

### 5. Update Apply Focus Outline

Open the player Interaction Component and locate:

`ApplyFocusOutline`

The default implementation uses a simple Custom Depth setup intended primarily for demonstration.

Replace the demonstration outline logic with the Brightnode Outline System integration.

Keep the existing checks for:

* `Enable Outlines`
* Valid Target Component
* `Allow Focus Outline`

Once those checks pass:

1. Get the owner of the Interaction Component.
2. Get the Brightnode Outline System Player Component from the player.
3. Call `Get Outline Tag` on the interactable actor.
4. Pass the returned Gameplay Tag into the Outline System's `Apply Outline` function.
5. Pass the focused actor as the target actor.

The resulting flow is:

`ApplyFocusOutline`

↓

`Enable Outlines?`

↓

`Target Component Valid?`

↓

`Allow Focus Outline?`

↓

`Get Outline System Player Component`

↓

`Get Outline Tag from Interactable Actor`

↓

`Apply Outline`

The Outline System then uses the returned Gameplay Tag to determine which Outline Data Asset or preset should be applied.

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

***

### 6. Update Clear Focus Outline

Next, locate:

`ClearFocusOutline`

The default implementation manually disables Custom Depth on the components previously outlined by the demonstration system.

Replace this with the Brightnode Outline System removal logic.

The new flow should:

1. Get the owner of the Interaction Component.
2. Get the Brightnode Outline System Player Component.
3. Validate the component.
4. Call `Remove Outlines for Actor`.
5. Pass the previously focused actor as the Target Actor.

The resulting flow is:

`ClearFocusOutline`

↓

`Get Outline System Player Component`

↓

`Validate Component`

↓

`Remove Outlines for Actor`

Once complete, the Interaction Component no longer needs to manually manage Custom Depth for focused actors.

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

***

### Before and After

The default Interaction System outline flow is intentionally simple.

It directly manages:

* Render Custom Depth
* Custom Depth Stencil Value
* Outlined component tracking

After integrating the Brightnode Outline System, those responsibilities move into the dedicated Outline System.

The Interaction Component instead becomes responsible only for:

* Detecting focus
* Requesting an outline
* Supplying the focused actor
* Supplying the actor's Outline Tag
* Clearing the outline when focus is lost

This produces a much cleaner separation between interaction logic and visual presentation.

***

### How the Outline Tag Is Used

The Outline Tag acts as the connection between the interactable actor and the Outline System preset it should use.

For example:

`BP_InteractableDoor`

returns:

`Outline.Interactable`

The Outline System receives that tag and uses it to resolve the corresponding Outline preset.

The Interaction System does not need to know:

* Outline colour
* Thickness
* Material settings
* Stencil values
* Outline type
* Team or global behaviour

All of that remains inside the Outline System.

***

### Example

A simple interactable button could be configured with:

`OutlineTag = Outline.Interactable`

When the player focuses the button:

`Focus Detected`

↓

`ApplyFocusOutline`

↓

`GetOutlineTag`

↓

`Outline.Interactable`

↓

`Apply Outline`

When the player looks away:

`Focus Lost`

↓

`ClearFocusOutline`

↓

`Remove Outlines for Actor`

This allows every interactable actor to choose its own Outline preset using a single Gameplay Tag.

***

### Using Different Outline Presets

Because the tag is supplied by the actor, different interactables can use completely different focus outlines.

For example:

| Actor          | Outline Tag            |
| -------------- | ---------------------- |
| Door           | `Outline.Interactable` |
| Quest Item     | `Outline.Objective`    |
| Friendly Actor | `Outline.Friendly`     |
| Hazard         | `Outline.Warning`      |

The Interaction Component does not need to change.

Each actor simply returns the appropriate tag through `GetOutlineTag`.

***

### Runtime Outline Changes

The Outline Tag can also be changed at runtime.

For example, an actor could return one tag while inactive and another after its gameplay state changes.

This works particularly well alongside runtime Interaction Definition swapping.

For example:

`Broken Machine → Repair Interaction → Repair Completes → New Interaction Definition → New Outline Tag`

This allows both interaction behaviour and focus presentation to change as the actor moves between gameplay states.

***

### Why Use This Integration?

Using the full Brightnode Outline System provides a dedicated outline presentation layer rather than keeping outline implementation inside the Interaction Component.

This gives the Interaction System access to the broader Outline System feature set while keeping both systems modular.

The final responsibility split becomes:

| System             | Responsibility                                   |
| ------------------ | ------------------------------------------------ |
| Interaction System | Detect which actor is focused                    |
| Interactable Actor | Provide its Outline Tag                          |
| Outline System     | Resolve and display the requested Outline preset |

The systems remain independent while integrating through a small, predictable interface.
