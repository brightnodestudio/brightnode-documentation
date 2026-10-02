# Debugging & Troubleshooting

This page covers common setup and runtime issues that can prevent the Brightnode Interaction System from behaving as expected.

When troubleshooting, work through the system in order:

`Collision → Detection → Focus → Interaction Definition → Interface → Interaction State → Multiplayer`

This usually makes it much easier to isolate where the problem is occurring.

***

### Actor Is Not Detected

If an interactable actor cannot be focused, check:

* The actor has an Interactable Component.
* A valid Interaction Definition is assigned.
* The actor has collision enabled.
* The detected component blocks the `Interaction` trace channel.
* The actor is within the configured interaction distance.
* Focus detection is currently running.
* The player Pawn is locally controlled.

If the interaction trace cannot hit the actor, the Interaction System cannot detect it.

***

### Interaction Trace Hits the Wrong Object

If focus is being given to an unexpected actor or component, check:

* Which collision component is blocking the `Interaction` trace channel.
* Whether another object is positioned between the player and the intended target.
* Whether unnecessary components are also set to block the Interaction channel.
* Whether the intended interactable collision is exposed clearly to the trace.

Where possible, only the components that should participate in interaction detection should block the `Interaction` trace channel.

***

### Interaction Prompt Does Not Appear

If the actor becomes focused but no prompt appears, check:

* Common UI is enabled.
* `CommonGameViewportClient` is configured.
* Common Input controller data has been added.
* The actor has a valid Interaction Definition.
* Prompt presentation is enabled for the interaction.
* The prompt is not currently configured to hide during interaction.
* The Prompt Anchor and Prompt Widget are valid.
* The focused actor is returning valid prompt information.

If **Use Custom Text** is enabled, also confirm that the actor implements the required Interaction Interface function and returns valid text.

***

### Common UI Input Icon Does Not Appear

If the prompt appears but the input icon is missing, check:

* The Common UI plugin is enabled.
* Keyboard and Gamepad controller data are configured.
* The correct input action is being referenced.
* The active input device has a valid input brush or icon configured.
* Common UI is detecting the current input method correctly.

Input icons are provided through Common UI rather than being hard-coded into the Interaction System.

***

### Custom Prompt Text Does Not Update

If **Use Custom Text** is enabled but the expected text is not displayed, check:

* The actor implements the Interaction Interface.
* The custom text interface function is implemented.
* The function returns valid text.
* The actor's gameplay state is current.
* The prompt is being refreshed after the state changes.

For example, an actor that can toggle between On and Off may need to return:

`Turn On`

or:

`Turn Off`

based on its current state.

If the interaction behaviour itself has not changed, Custom Text is generally preferable to swapping the entire Interaction Definition.

***

### Outline Does Not Appear

If focus works but the outline does not appear, first check:

`Project Settings → Rendering`

Ensure:

`Custom Depth-Stencil Pass`

is set to:

**Enabled with Stencil**

Also check:

* The Interaction Definition allows focus outlining.
* The expected mesh or component supports Custom Depth rendering.
* Outlines are enabled in the Interaction Component.
* The actor is actually focused.

If using the Brightnode Outline System integration, also check the integration-specific section below.

***

### Brightnode Outline System Integration Does Not Work

If the full Brightnode Outline System does not apply a focus outline, check:

* Both the Interaction System and Outline System are installed.
* The player contains the Brightnode Outline System Player Component.
* The Interaction Component can find that component.
* `ApplyFocusOutline` has been updated to call the Outline System.
* `ClearFocusOutline` has been updated to remove outlines through the Outline System.
* The interactable actor implements `GetOutlineTag`.
* `GetOutlineTag` returns a valid Gameplay Tag.
* That Gameplay Tag has a matching Outline preset configured in the Outline System.

The expected flow is:

`Focus Actor → GetOutlineTag → Apply Outline`

If the tag returned is `None`, invalid, or has no corresponding preset, the Outline System cannot determine what outline to apply.

***

### GetOutlineTag Returns the Wrong Tag

If the wrong outline is being applied, check:

* The actor's `OutlineTag` variable.
* The value returned by `GetOutlineTag`.
* Whether the actor has changed gameplay state at runtime.
* Whether the expected tag maps to the correct Outline preset.

Because the tag is supplied by the interactable actor, incorrect tag values will result in incorrect Outline presets.

***

### Interaction Does Not Fire

If focus and prompts work but the gameplay interaction does nothing, check:

* The actor implements the Interaction Interface.
* The appropriate Interface function is implemented.
* The assigned Interaction Definition uses the intended Interaction Type.
* The actor is not currently locked.
* The interaction is valid for the current actor state.
* Gameplay logic is connected to the relevant Interface function.

For a standard Press interaction, confirm that the actor responds to:

`Call Interact`

The Interaction System controls when the interaction occurs, but the actor still needs to implement what actually happens.

***

### Hold Interaction Does Not Complete

If a Hold To Complete interaction starts but never completes, check:

* The Interaction Definition uses Hold To Complete.
* The hold duration is valid.
* The interaction remains active for the full duration.
* Focus is not being lost during the hold.
* The interaction is not being cancelled.
* The actor remains valid during the interaction.
* Another player has not taken or blocked interaction ownership.

Also confirm that interaction progress is advancing rather than being reset.

***

### Hold Interaction Starts but Gameplay Does Not Respond

If the hold begins correctly but your actor does not react at the start of the hold, confirm that:

`Hold Interaction Started`

is implemented on the actor's Interaction Interface.

This callback is separate from the eventual successful interaction completion.

Use it for behaviour that should begin immediately when the player starts holding.

***

### Sustained Interaction Does Not Start

If a While Holding interaction does not begin correctly, check:

* The Interaction Definition uses the correct sustained interaction type.
* `Sustained Interaction Start` is implemented.
* The interaction request reaches the actor.
* The actor is not locked.
* The interaction state successfully enters its active state.

***

### Sustained Interaction Does Not End

If a sustained interaction remains active after the player releases the input, check:

* `Sustained Interaction End` is implemented.
* The interaction end flow is reaching the Interaction Component.
* The current interaction state is being reset.
* Any interaction lock is released.
* Any actor-specific gameplay started during `Sustained Interaction Start` is also stopped.

A typical actor flow should be:

`Sustained Interaction Start → Gameplay Active → Sustained Interaction End`

***

### Runtime Interaction Definition Does Not Change

If an actor swaps Interaction Definitions but continues behaving like the previous one, check:

* The new Data Asset is actually being assigned.
* The correct Interactable Component is being updated.
* The new Interaction Definition contains the intended Interaction Type.
* Prompt presentation has refreshed after the swap.
* The actor's gameplay state was updated correctly.
* Multiplayer state is synchronised if the change is authoritative.

A typical flow should be:

`Gameplay State Changes → Assign New Interaction Definition → Future Interactions Use New Definition`

For example:

`Repair Completes → Swap Repair Definition for Press Definition`

***

### Prompt Still Shows Old Data After a Definition Swap

If the Interaction Definition changes but the prompt still shows old information, check whether the prompt has refreshed after the Data Asset swap.

The actor may already be focused when the definition changes.

In this case, make sure the current prompt state is updated so it reads from the newly assigned Interaction Definition.

***

### Grab Interaction Does Not Work

If an object can be focused but cannot be grabbed, check the component being grabbed has:

* **Simulate Physics** enabled.
* Collision enabled.
* A valid physics mass.
* Collision configured to block the `Interaction` trace channel.
* A valid Grab Interaction Definition assigned.

The grabbed component must be physics-enabled.

If **Simulate Physics** is disabled, the object cannot behave as a physics-based grabbed object.

***

### Grabbed Object Has No Weight or Feels Incorrect

Grab behaviour depends on the physics mass of the grabbed component.

Check:

* The calculated mass.
* **Mass Override** if one is being used.
* The mesh's physics setup.
* Collision configuration.
* Physics constraints.

Very light or very heavy objects may behave differently while being manipulated.

Make sure each grabbable object has a sensible mass for the intended gameplay behaviour.

***

### Grabbed Object Behaves Incorrectly in Multiplayer

If grabbing works locally but movement is inconsistent between players, check:

* The actor is replicated where required.
* Physics or movement replication is configured correctly.
* The correct client or server owns the relevant movement.
* The Interaction System state is being replicated.
* Normal Unreal Engine physics replication requirements are being followed.

The Interaction System controls the grab lifecycle, but physics movement itself still follows Unreal Engine networking rules.

***

### Radius Scan Does Not Find Nearby Interactables

If nearby interactable discovery is not working, check:

* Radius Scan discovery is currently running.
* `Stop Radius Scan Trace` has not been called.
* The player Pawn is locally controlled.
* The actor is inside the configured scan radius.
* The actor has a valid Interactable Component.
* Any filtering requirements used by the Radius Scan are satisfied.

If scanning has been stopped, restart it using:

`Start Radius Scan Trace`

***

### Focus Detection Has Stopped

If interactions previously worked but the player no longer detects anything, check whether:

`Stop Focus Trace`

has been called.

This may happen intentionally during:

* Menus
* Cutscenes
* Player death
* Gameplay transitions
* Temporary interaction disabling

When normal gameplay resumes, call:

`Start Focus Trace`

to restart detection.

***

### Focus Trace or Radius Scan Runs on the Wrong Pawn

Both focus detection and Radius Scan discovery are designed to run only for locally controlled Pawns.

If testing multiplayer, make sure you are looking at the correct client instance.

Simulated proxies should not run these detection systems.

This prevents unnecessary traces and scans from running for remote player representations.

***

### Interaction Is Permanently Locked

If an actor remains unavailable after an interaction has ended, check:

* The interaction completed correctly.
* The interaction cancellation path ran correctly.
* The sustained interaction received its end callback.
* The lock was released.
* The locking player is still valid.
* The server has the expected lock ownership state.

Every lock acquisition should have a corresponding completion, cancellation, or release path.

***

### Another Player Cannot Interact

If one player can interact but another cannot, check:

* Whether the actor is currently locked.
* Whether the previous player's interaction ended correctly.
* Whether the second player's request reaches the server.
* Whether the server considers the interaction valid.
* Whether the Interactable Component and Actor replicate where required.

Remember that multiple players can focus the same actor while only one player owns an exclusive interaction lock.

***

### Works as Server but Not as Client

If the interaction behaves correctly as the server but not as a client, check:

* The relevant Actor replicates.
* The relevant components are set to replicate.
* Replicated properties are changed on the server.
* RepNotify is configured correctly.
* The client's interaction request reaches the server.
* The server accepts the request.
* The actor is not locked by another player.
* Client-side presentation is not being confused with authoritative gameplay execution.

This is one of the most common multiplayer setup issues.

***

### RepNotify Does Not Fire on Client

If RepNotify appears to work on the server but not on clients, check the component that owns the replicated variable.

The component itself must have replication enabled.

Also confirm:

* The owning Actor replicates.
* The property is configured for replication.
* The value changes on the server.
* The client receives the replicated component.
* The value actually changes to a different value.

If the component does not replicate, its replicated properties cannot update correctly on clients.

***

### Interface Function Does Not Fire

If an Interaction Interface function does not appear to execute, check:

* The actor implements the correct Interaction Interface.
* You implemented the function on the actor being interacted with.
* The interaction type actually calls that function.
* The server or client context is what you expect.
* The gameplay logic has not been placed on a different actor by mistake.

Remember that the Interface callbacks are sent to the interactable actor.

***

### Multiple Interactable Components on One Actor

For most actors, a single Interactable Component is recommended.

If an actor contains multiple Interactable Components, make sure the system is using the one you expect.

Multiple independent components can make it less obvious which Interaction Definition, state, or prompt should be considered active.

Use multiple Interactable Components only when the actor genuinely requires separate interaction behaviours.

***

### Common UI Appears to Stop Working

If prompts were previously working but disappear after changing UI or viewport settings, recheck:

`Project Settings → Engine → General Settings`

Ensure:

`Game Viewport Client Class`

is still set to:

`CommonGameViewportClient`

Also confirm the Common UI plugin and Common Input controller data remain configured.

***

### Recommended Debugging Order

When an interaction is not working, check the system in this order:

1. Collision
2. Interaction trace or Radius Scan
3. Focus
4. Interaction Definition
5. Prompt presentation
6. Interaction Interface
7. Interaction state
8. Locking
9. Replication
10. Actor-specific gameplay logic

This prevents spending time debugging multiplayer or gameplay logic when the actor is simply not being detected in the first place.

***

### Still Having Problems?

If the issue remains after working through the relevant sections above, gather:

* The Interaction Type being used.
* A screenshot of the Interactable Component.
* A screenshot of the Interaction Definition.
* The actor's collision settings.
* The relevant Interaction Interface implementation.
* Whether the issue occurs in Single Player, Server, Client, or all modes.
* Any relevant runtime Data Asset swapping.
* Any relevant lock or replication state.

Providing this information makes most interaction issues much easier to diagnose.

For additional support:

* [Discord](https://discord.gg/R6zJkHx6x7)
* Email: [brightnodestudio@gmail.com](mailto:brightnodestudio@gmail.com)
