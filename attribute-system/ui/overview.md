# UI Widgets

Three widget templates are included, all designed to self-bind via the BPI_AttributeSystem interface on construct. No manual wiring required beyond dropping them into your HUD.

---

## Self-Binding Setup

All three widgets use the same binding pattern on construct:

```
Construct
→ Get Owning Player Pawn
→ Check implements BPI_AttributeSystem
→ Get BP_AttributeComponent via interface
→ Bind to Client_OnAttributeChanged
→ Set initial display value
```

This means widgets automatically find the correct component on the owning player without any HUD-level wiring.

---

## Threshold Visual Overrides

All three widgets support a **Threshold Visuals Array** - a configurable array of entries that define how the widget looks at each threshold:

| Property | Description |
|---|---|
| ThresholdTag | Which threshold triggers this visual |
| Color | The fill or tint color at this threshold |
| bFlash | Whether the widget flashes at this threshold |

When an attribute crosses a threshold, the widget automatically transitions to the matching visual. When the threshold exits, it returns to the default visual.

---

# WBP_RadialAttributeWidget

A circular fill widget using a dynamic material instance.

**Features:**
- Circular fill driven by attribute percentage
- Smooth lerp transition on value change
- Threshold color transitions
- Icon flash at critical thresholds
- Configurable threshold visuals array

**Best used for:** Health, Stamina, Hunger, Hydration - any attribute the player needs to monitor at a glance.

**Setup:**
1. Add to your HUD
2. Set the **AttributeTag** property to the attribute you want to display
3. Configure the **ThresholdVisuals** array if custom colors are needed
4. The widget binds and updates automatically

---

# WBP_LinearAttributeBar

A horizontal or vertical progress bar using a dynamic material instance.

**Features:**
- Horizontal or vertical orientation (configurable)
- Smooth lerp transition on value change
- Threshold color shifts
- Optional text display modes: Current, Percent, CurrentAndMax
- Configurable threshold visuals array

**Best used for:** Any attribute where exact values are useful to display, or where a traditional bar fits the UI layout.

**Setup:**
1. Add to your HUD
2. Set the **AttributeTag** property
3. Set **Orientation** to Horizontal or Vertical
4. Set **TextDisplayMode** if text overlay is desired
5. Configure **ThresholdVisuals** array if needed

---

# WBP_IconAttributeDrain

An icon-based drain widget using a dynamic material instance. The icon visually drains to represent the attribute value.

**Features:**
- Three drain directions: BottomUp, TopDown, Radial
- Full and empty color tints
- Threshold flash
- Configurable threshold visuals array

**Best used for:** Oxygen, Temperature, Mania - attributes with a strong visual metaphor that benefits from an icon rather than a bar.

**Dynamic Show/Hide:**
The Oxygen widget in the demo uses this widget with dynamic show/hide driven by the zone system - the widget is hidden by default and shown via client RPC when the player enters an oxygen zone. This pattern works with any attribute and any trigger.
