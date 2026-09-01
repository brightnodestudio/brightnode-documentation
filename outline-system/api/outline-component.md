# Outline Component API

The Outline Component is the recommended gameplay-facing API.

## Outlines

### ApplyOutline

Applies an outline request to the specified actor using the supplied outline information.

This is the normal entry point for Local, Team, and Global presets.

### RemoveOutline

Removes a specific outline request previously applied through the component.

### RemoveOutlinesForActor

Removes all applicable outline requests created by this component for the specified actor.

### IsActorOutlinedForThisPlayer

Returns whether the specified actor currently has an active outline visible to this player.

## Team

### SetTeamTag

Sets the Gameplay Tag identifying the player's team.

### GetTeamTag

Returns the player's current Team Tag.

## Utility

### SetThroughWallOutlinesEnabled

Enables or disables through-wall outline rendering for the player.

### SetActiveCamera

Sets the camera used for camera-dependent outline rendering and visibility.

Call this when your project changes the player's active gameplay camera.
