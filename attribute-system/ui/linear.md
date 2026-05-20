# WBP_LinearAttributeBar

A horizontal or vertical progress bar widget driven by a dynamic material instance. The most versatile of the three included widgets - suitable for almost any attribute.

---

## Best Used For

Any attribute where exact values are useful to display alongside the bar, or where a traditional horizontal or vertical bar suits your HUD layout better than a radial fill.

---

## Features

- Horizontal or vertical orientation - configurable per instance
- Smooth lerp transition on value change
- Threshold color shifts - bar color changes automatically at threshold crossings
- Optional text display overlay with three modes
- Configurable threshold visuals array

---

## Setup

1. Add **WBP_LinearAttributeBar** to your HUD widget
2. Set the **AttributeTag** property to the attribute you want to display
3. Set **Orientation** to Horizontal or Vertical
4. Set **TextDisplayMode** if you want a text overlay
5. Optionally configure the **ThresholdVisuals** array
6. The widget self-binds on construct - no further wiring required

---

## Orientation

| Setting | Description |
|---|---|
| **Horizontal** | Bar fills left to right |
| **Vertical** | Bar fills bottom to top |

---

## Text Display Modes

| Mode | Displays |
|---|---|
| **None** | No text overlay |
| **Current** | Current value only (e.g. "73") |
| **Percent** | Percentage only (e.g. "73%") |
| **CurrentAndMax** | Current and max (e.g. "73 / 100") |

---

## Threshold Visuals Array

Each entry contains:

| Property | Description |
|---|---|
| **ThresholdTag** | The threshold tag that triggers this visual |
| **Color** | The bar color to shift to when this threshold is active |
| **bFlash** | Whether the bar flashes while this threshold is active |

---

## Multiplayer

Binds to **Client_OnAttributeChanged** and threshold client events automatically on construct. Updates correctly on all clients via the client RPC event system.
