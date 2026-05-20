# WBP_RadialAttributeWidget

A circular fill widget driven by a dynamic material instance. Designed for attributes the player needs to monitor at a glance.

---

## Best Used For

Health, Stamina, Hunger, Hydration - any attribute where a circular fill communicates state clearly and fits your HUD layout.

---

## Features

- Circular fill driven by attribute percentage via dynamic material
- Smooth lerp transition on value change - fill animates rather than snapping
- Threshold color transitions - fill color shifts automatically when thresholds are crossed
- Icon flash at critical thresholds - draws attention at low values
- Configurable threshold visuals array

---

## Setup

1. Add **WBP_RadialAttributeWidget** to your HUD widget
2. In the Details panel set the **AttributeTag** property to the attribute you want to display (e.g. `Attribute.Health`)
3. Optionally configure the **ThresholdVisuals** array with per-threshold colors and flash settings
4. The widget self-binds on construct - no further wiring required

---

## Threshold Visuals Array

Each entry in the ThresholdVisuals array contains:

| Property | Description |
|---|---|
| **ThresholdTag** | The threshold tag that triggers this visual |
| **Color** | The fill color to transition to when this threshold is active |
| **bFlash** | Whether the widget flashes while this threshold is active |

Visuals transition automatically when `Client_OnThresholdEntered` fires and revert when `Client_OnThresholdExited` fires.

---

## Multiplayer

The widget binds to **Client_OnAttributeChanged** and **Client_OnThresholdEntered / Exited** automatically on construct. It updates correctly on all clients via the client RPC event system with no additional setup.
