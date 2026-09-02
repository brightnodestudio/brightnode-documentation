# Outline Component API

The Outline Component is the recommended gameplay-facing API.

## Outlines

### ApplyOutline

Applies an outline request to the specified actor using the supplied outline information.

This is the normal entry point for Local, Team, and Global presets.

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### RemoveOutline

Removes a specific outline request previously applied through the component.

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### RemoveOutlinesForActor

Removes all applicable outline requests created by this component for the specified actor.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

### IsActorOutlinedForThisPlayer

Returns whether the specified actor currently has an active outline visible to this player.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## Team

### SetTeamTag

Sets the Gameplay Tag identifying the player's team.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### GetTeamTag

Returns the player's current Team Tag.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

## Utility

### SetThroughWallOutlinesEnabled

Enables or disables through-wall outline rendering for the player.

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

### SetActiveCamera

Sets the camera used for camera-dependent outline rendering and visibility.

Call this when your project changes the player's active gameplay camera.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>
