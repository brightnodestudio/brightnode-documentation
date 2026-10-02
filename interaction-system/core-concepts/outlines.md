# Interaction Prompts

Interaction Prompts provide visual feedback when the player focuses an interactable actor.

The prompt system is driven by the active Interaction Definition and is kept separate from gameplay logic, allowing prompt behaviour to be reused consistently across different actors.

***

### Prompt Overview

When the player focuses a valid interactable actor, the system can display an interaction prompt containing information such as:

* Interaction text
* Input icon
* Interaction progress
* Current interaction state
* Context-specific presentation

The prompt updates automatically as the interaction changes.

***

### Common UI Integration

The Interaction System uses Unreal Engine's Common UI framework for input presentation.

Common UI allows the prompt to display the correct input icon for the player's current input method.

For example:

* Keyboard and Mouse
* Xbox Controller
* PlayStation Controller

The required Common UI setup is covered in the **Installation & Setup** page.

***

### Prompt Anchor

The Prompt Anchor controls where the interaction prompt is positioned for the focused actor.

It provides the connection between the interactable actor and the prompt presentation shown to the player.

This allows interaction prompts to appear in a consistent location relative to the actor without requiring custom UI logic inside each Blueprint.

***

### Prompt Widget

The Prompt Widget is responsible for displaying the interaction information to the player.

It can present:

* Interaction name or action text
* Input icon
* Hold progress
* Sustained interaction feedback
* Visibility changes

The widget reacts to interaction state rather than controlling gameplay itself.

***

### Prompt Text

Prompt text can be configured directly through the Interaction Definition or supplied dynamically by the actor being interacted with.

By default, the prompt uses the text defined in the Interaction Definition.

If **Use Custom Text** is enabled, the system instead retrieves the prompt text from the interaction interface function implemented by the focused actor.

This allows an actor to provide context-sensitive interaction text at runtime.

For example:

* Open
* Close
* Turn On
* Turn Off
* Pick Up
* Drop

The same Interaction Definition can therefore be reused across multiple actors while each actor provides its own prompt text when required.

A typical custom text flow is:

`Gain Focus → Use Custom Text Enabled → Call Interface Function → Display Returned Text`

***

### Input Icons

The prompt can display the input associated with the interaction using Common UI.

The displayed icon updates based on the player's current input device.

For example, switching from keyboard to gamepad can automatically update the prompt from a keyboard key to the appropriate controller button.

***

### Hold Progress

Hold To Complete interactions can display progress while the player holds the interaction input.

This gives the player clear feedback about how close the interaction is to completion.

The progress display is driven by the interaction state and configured hold duration.

***

### Prompt Visibility

Prompt visibility is controlled automatically as focus and interaction state change.

A prompt can be shown when:

* An actor gains focus
* The interaction becomes available
* The player begins a sustained interaction
* Interaction progress is updated

A prompt can be hidden when:

* Focus is lost
* The actor is no longer interactable
* The interaction completes
* The interaction is cancelled
* The active Interaction Definition requests that it is hidden during interaction

***

### Hide Prompt While Interacting

Interaction Definitions can be configured to hide the prompt while an interaction is active.

This is useful for sustained interactions where the prompt is no longer needed once the player has committed to the action.

For example:

`Focus Actor → Prompt Appears → Interaction Starts → Prompt Hides → Interaction Ends → Prompt Returns`

If the actor remains focused after the interaction finishes, the prompt can become visible again.

This setting allows prompt behaviour to be controlled per interaction without modifying the widget or actor Blueprint.

***

### Focus and Prompt Behaviour

The prompt is directly linked to the player's current focused actor.

A typical flow is:

`Gain Focus → Read Interaction Definition → Show Prompt → Interact → Update Prompt → Lose Focus → Hide Prompt`

Only the local player's prompt presentation is affected.

Other players manage their own focus and prompts independently.

***

### Customising the Prompt

The included prompt system can be customised to match the visual style of your project.

Because gameplay logic is separate from presentation, the prompt widget can be replaced or restyled without changing how interactions execute.

Typical customisations include:

* Layout
* Fonts
* Icons
* Animations
* Progress indicators
* Background styling
* Visibility transitions
