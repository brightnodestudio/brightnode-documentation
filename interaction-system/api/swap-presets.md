# Blueprint API

The Brightnode Interaction System is designed to require very little direct Blueprint control.

Most interaction behaviour is handled automatically by the Interaction Component, Interaction Definitions, and Interaction Interface.

The following functions are exposed for cases where focus detection or nearby interactable discovery needs to be manually enabled or disabled at runtime.

***

### Player Interaction Component

The public Blueprint API is exposed through the Player Interaction Component.

These functions control the two detection systems used by the component:

* Focus Trace
* Radius Scan

***

### Start Focus Trace

`Start Focus Trace`

Starts the focus detection system.

The component begins running the configured focus trace at the interval defined by the **Focus Trace Rate**.

Focus detection only runs for locally controlled Pawns, preventing unnecessary traces on simulated proxies.

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

#### Use When

Use this function when focus detection has previously been stopped and needs to be enabled again.

Typical examples include:

* Returning from a menu
* Re-enabling player interaction
* Respawning a player
* Leaving a gameplay state that temporarily disabled interaction

#### Behaviour

`Start Focus Trace → Start Focus Timer → Execute Focus Trace Repeatedly`

The trace continues until `Stop Focus Trace` is called.

***

### Stop Focus Trace

`Stop Focus Trace`

Stops the focus detection system by clearing the active Focus Trace timer.

Once stopped, the player will no longer perform interaction focus traces until the system is started again.

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

#### Use When

Use this function when interaction focus should be temporarily disabled.

Typical examples include:

* Opening a menu
* Entering a cutscene
* Player death
* Disabling player control
* Switching to a gameplay mode where interactions should not be available

#### Behaviour

`Stop Focus Trace → Clear Focus Timer → Focus Detection Stops`

***

### Start Radius Scan Trace

`Start Radius Scan Trace`

Starts the nearby interactable discovery system.

The component begins performing radius scans at the interval defined by the **Radius Scan Interval**.

Like focus tracing, Radius Scan discovery only runs for locally controlled Pawns.

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

#### Use When

Use this function when Radius Scan discovery has previously been stopped and needs to be enabled again.

The Radius Scan system is used to detect nearby interactable actors independently of the player's direct focus trace.

#### Behaviour

`Start Radius Scan Trace → Start Radius Scan Timer → Execute Radius Scan Repeatedly`

The scan continues until `Stop Radius Scan Trace` is called.

***

### Stop Radius Scan Trace

`Stop Radius Scan Trace`

Stops nearby interactable discovery by clearing the active Radius Scan timer.

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

#### Use When

Use this function when nearby interaction discovery should be temporarily disabled.

Typical examples include:

* Opening menus
* Player death
* Disabling the Interaction Component
* Entering gameplay states where nearby interactables are not required

#### Behaviour

`Stop Radius Scan Trace → Clear Radius Scan Timer → Radius Discovery Stops`

***

### Automatic Startup

Under normal gameplay conditions, these detection systems are managed by the Interaction Component and do not need to be manually started or stopped.

The public API exists primarily to allow projects to temporarily disable interaction detection when required by their own gameplay flow.

For example:

`Open Menu → Stop Detection`

`Close Menu → Start Detection`

***

### Local Player Behaviour

Both detection systems are designed to run only for the locally controlled Pawn.

This prevents focus traces and nearby discovery scans from running unnecessarily on simulated proxies in multiplayer games.

Gameplay interaction authority remains separate and continues to follow the server-authoritative multiplayer flow.

***

### Detection Overview

| Function                  | Purpose                              |
| ------------------------- | ------------------------------------ |
| `Start Focus Trace`       | Starts direct focus detection        |
| `Stop Focus Trace`        | Stops direct focus detection         |
| `Start Radius Scan Trace` | Starts nearby interactable discovery |
| `Stop Radius Scan Trace`  | Stops nearby interactable discovery  |

***

### Interaction Gameplay API

Gameplay interactions are not normally executed by calling public functions directly on the component.

Instead, interactable actors respond through the **Interaction Interface**.

This includes callbacks such as:

* `Call Interact`
* `Sustained Interaction Start`
* `Sustained Interaction End`
* `Hold Interaction Started`

This keeps the component API focused on system control while actor-specific gameplay remains inside the actor being interacted with.
