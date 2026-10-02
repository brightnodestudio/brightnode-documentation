# Changelog

### Version 2.0.0

Version 2 introduces a major update to the Brightnode Interaction System, with a stronger focus on modularity, data-driven configuration, multiplayer reliability, and runtime flexibility.

#### Added

* Runtime Interaction Definition swapping
* Custom prompt text through the Interaction Interface
* Ability to hide the interaction prompt while interacting
* Improved interaction state handling
* Improved multiplayer interaction flow
* Improved RepNotify support
* Improved prompt presentation
* Expanded Grab interaction support
* Improved physics grab behaviour
* Interaction locking improvements
* Brightnode Outline System integration support
* Gameplay Tag driven outline selection
* Additional debugging and troubleshooting support

#### Changed

* Interaction configuration moved further into Interaction Definition Data Assets
* Interaction behaviour is now more strongly separated from actor gameplay logic
* Prompt handling is more modular and data-driven
* Focus and interaction presentation are more clearly separated from gameplay execution
* Interactable actors now use a cleaner component-based workflow
* Interaction Interface usage has been expanded for gameplay callbacks and dynamic data
* Multiplayer state handling has been improved for both server and clients
* Documentation has been completely rewritten and expanded

#### Fixed

* Client interaction state updates not firing correctly when replicated components were not configured correctly
* RepNotify-related multiplayer issues
* Prompt visibility issues during sustained interactions
* Interaction state edge cases
* Multiplayer locking edge cases
* Grab interaction inconsistencies
* Various focus, prompt, and interaction flow issues
