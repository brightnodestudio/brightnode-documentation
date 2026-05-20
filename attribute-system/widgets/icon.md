# WBP_IconAttributeDrain

An icon-based drain widget driven by a dynamic material instance. The icon visually drains to represent the attribute value - ideal for attributes with a strong visual metaphor.

---

## Best Used For

Oxygen, Temperature, Mania - attributes where an icon draining conveys the feeling of the attribute better than a bar or radial fill.

---

## Features

- Three drain directions: BottomUp, TopDown, Radial
- Full and empty color tints - icon color shifts between configured tints as the value changes
- Threshold flash - draws attention at critical thresholds
- Configurable threshold visuals array
- Supports dynamic show/hide driven by zone or gameplay events

---

## Setup

1. Add **WBP_IconAttributeDrain** to your HUD widget
2. Set the **AttributeTag** property to the attribute you want to display
3. Set **DrainDirection** to BottomUp, TopDown, or Radial
4. Set **FullColor** and **EmptyColor** tints
5. Optionally configure the **ThresholdVisuals** array
6. The widget self-binds on construct - no further wiring required

---

## Drain Directions

| Direction | Description |
|---|---|
| **BottomUp** | Icon drains from the bottom upward - empty at bottom, full at top |
| **TopDown** | Icon drains from the top downward - empty at top, full at bottom |
| **Radial** | Icon drains in a circular sweep - useful for Oxygen or time-based indicators |

---

## Dynamic Show & Hide

The Oxygen widget in the demo uses WBP_IconAttributeDrain with dynamic show/hide. The widget is hidden by default and shown via a client RPC event when the player enters an oxygen zone - then hidden again on exit.

This pattern works with any attribute and any trigger:

```
On Zone Enter
→ Client RPC to owning player
→ Set Oxygen Widget Visibility: Visible

On Zone Exit
→ Client RPC to owning player
→ Set Oxygen Widget Visibility: Hidden
```

---

## Threshold Visuals Array

Each entry contains:

| Property | Description |
|---|---|
| **ThresholdTag** | The threshold tag that triggers this visual |
| **Color** | The icon tint color at this threshold |
| **bFlash** | Whether the icon flashes while this threshold is active |

---

## Multiplayer

Binds to **Client_OnAttributeChanged** and threshold client events automatically on construct. Show/hide logic should also be driven from client RPC events to stay in sync across clients.
