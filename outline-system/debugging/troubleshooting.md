# Common Issues

## No Outline Appears

Check:

1. Custom Depth-Stencil Pass is set to Enabled with Stencil in the PRoject Settings
2. The Outline Component exists on the relevant player.
3. The component initialized successfully.
4. The Outline Post Process Material is assigned.
5. The target has an appropriate mesh component.
6. The Gameplay Tag exists.
7. The tag is assigned to the intended preset's **Preset Tag**.
8. The preset is registered in the active Outline Preset Library.
9. Mesh Selection settings match the target actor.
10. Required Component Tags exist when using tag-based selection.
11. The active camera is correct if your project changes cameras.
12. Enable **Show Debug** and inspect the output.

## Team Outline Does Not Appear

Check the player's Team Tag, the preset's Visibility Mode, World Manager configuration, and the intended multiplayer execution path.

## Global Outline Does Not Appear for Other Players

Check that the preset uses Global visibility, the World Manager is configured, and receiving players have initialized Outline Components.

## Wrong Mesh Is Outlined

Review Mesh Selection Mode and Required Mesh Tags. Required Mesh Tags are Component Tags.

## Outline Does Not Expire

Verify:

```
Has Expiry = True
Expiry Duration > 0
```

A different active request may still be keeping the actor outlined.

## Outline Appears Not to Remove

An actor can have more than one active outline request. Removing one request does not necessarily remove all remaining requests.

## Flashing Timing Looks Wrong

Adjust Flash On Duration and Flash Off Duration. Flash Tick Rate controls processing frequency rather than the intended flash duration.

## Through-Wall Behaviour Is Wrong

Check the component's through-wall setting and any runtime calls to `SetThroughWallOutlinesEnabled`.
