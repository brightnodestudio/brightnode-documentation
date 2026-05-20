# Modifier System

Modifiers are temporary or permanent effects applied to an actor's attributes. They are the mechanism behind all threshold cascades, zone effects, item buffs, and status conditions in the system.

---

## Two Modifier Types

### Stat Modifiers
Stat modifiers affect an attribute's **ComputedMax** - the effective ceiling of the attribute's value. Three sub-types are available:

| Sub-type | Behaviour |
|---|---|
| **Additive** | Adds a flat value to the attribute's BaseMax |
| **Multiplicative** | Applies a percentage of BaseMax - the most restrictive active multiplier wins |
| **Override** | Sets a hard cap on the attribute's max, ignoring all other modifiers |

### Tick Modifiers
Tick modifiers apply a **delta to the attribute value** every decay tick - effectively a continuous drain or gain effect.

Two sub-types are available:

| Sub-type | Behaviour |
|---|---|
| **Direct Delta** | Changes the attribute value directly each tick (e.g. Poison draining Health) |
| **Drift Offset** | Pushes the drift target rather than the value - used for temperature modifiers |

---

## DA_ModifierDefinition Structure

All modifiers are defined as **DA_ModifierDefinition** DataAssets. Each asset contains:

| Property | Description |
|---|---|
| **DisplayName** | Human readable name shown in the debug widget |
| **Icon** | Optional icon for UI display |
| **StackRule** | How multiple applications of this modifier are handled |
| **Duration** | How long the modifier lasts (0 = permanent until manually removed) |
| **StatModifiers** | Array of stat modifier entries |
| **TickModifiers** | Array of tick modifier entries |

---

## Timed Modifiers

Modifiers with a **Duration** greater than zero automatically expire and remove themselves after that duration has elapsed. The `OnModifierRemoved` event fires when this happens.

Timed modifiers interact with stacking rules - a modifier with the Refresh stack rule will reset its timer on reapplication rather than creating a new instance.
