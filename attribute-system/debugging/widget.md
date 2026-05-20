# Debug Widget

The **WBP_AttributeDebugWidget** is a development tool that gives you a live view of every attribute on the local player's component.

---

## Accessing the Debug Widget

In the demo level, press **F3** to toggle the debug widget. This is wired in **BP_DemoPlayerController**.

To add it to your own project, add a toggle input binding in your PlayerController and use **Create Widget → WBP_AttributeDebugWidget → Add to Viewport**.

---

## What It Shows

The debug widget displays a scrollable table with one row per active attribute:

| Column | Description |
|---|---|
| Attribute Name | Display name of the attribute |
| Value / Max | Current value and ComputedMax (e.g. 73.2 / 100.0) |
| Progress Bar | Visual fill bar, color coded by threshold state |
| Status | Active / Paused / No Regen |
| Active Modifiers | Comma separated list of all currently applied modifier display names |

---

## Refresh Rate

The refresh rate of the debug widget is configurable. Lower values give smoother updates; higher values reduce draw call frequency during testing.

---

# Common Issues

### Attributes not appearing in debug widget
- Verify **BP_AttributeComponent** is added to the actor
- Verify **BPI_AttributeSystem** interface is implemented on the actor
- Verify a **DA_AttributeSetPreset** is assigned to the component
- Check that **Replicates** is enabled on the actor if testing in multiplayer

### OnThresholdExited not firing when zeroing an attribute
Use `ModifyAttribute` with a negative delta equal to the current value instead of `SetAttributeValue`. SetAttributeValue bypasses threshold evaluation.

### Walk speed not changing on client after threshold
Bind to `Client_OnThresholdEntered` and `Client_OnThresholdExited` instead of the server-side dispatcher versions. Set `CharacterMovement->MaxWalkSpeed` from the client event.

### Widget not updating in multiplayer
Ensure widgets bind to `Client_OnAttributeChanged` not `OnAttributeChanged`. Server dispatchers do not fire on clients.

### Recovery not resuming after modifier removed
Check that no other fatigue source modifiers are still active. Recovery is blocked while any active fatigue source modifier is present on the attribute.

### ComputedMax not updating after modifier removed
Verify the modifier was removed via `RemoveModifier` using the correct handle, or `RemoveModifiersByAssetTag` using the correct tag. ComputedMax recalculates automatically on modifier removal.

---

## Support

If your issue is not listed here:

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
