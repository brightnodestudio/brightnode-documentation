# Decay System

Decay is the automatic change of an attribute's value over time without any direct input from gameplay code.

---

## Decay Behaviours

Three decay behaviours are available, configured per attribute in the DataTable:

| Behaviour | Description |
|---|---|
| **Constant** | Value changes at a fixed rate every tick. Hunger and Hydration use this. |
| **Accelerating** | Decay rate increases over time - starts slow, gets faster. Useful for urgency escalation. |
| **Decelerating** | Decay rate decreases over time - starts fast, slows down. Useful for initial burst drain. |

---

## Configuring Decay

Each attribute row in **DT_AttributeDefinitions** exposes:

| Property | Description |
|---|---|
| **DecayRate** | How much the value changes per decay tick |
| **DecayBehaviour** | Constant, Accelerating, or Decelerating |
| **bDecayEnabled** | Whether decay runs at all for this attribute |

---

## Pausing & Resuming Decay

Decay can be paused and resumed at runtime through the public API:

```
PauseDecay (AttributeTag)       - pause a single attribute's decay
ResumeDecay (AttributeTag)      - resume a single attribute's decay
PauseAllDecay ()                - pause all attributes at once
ResumeAllDecay ()               - resume all attributes at once
```

---

## Dynamic Decay Rate

The decay rate can be changed at runtime:

```
SetDecayRate (AttributeTag, NewRate)
```

This is useful for modifiers that need to accelerate or slow a specific attribute's natural decay - for example a modifier that causes Hunger to drain faster under stress.
