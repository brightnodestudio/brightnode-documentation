# Attribute System

Attributes are the core data units of the system. Each attribute tracks a single float value that changes over time through decay, recovery, drift, and direct modification.

---

## What Is an Attribute?

An attribute is a named, clamped float value with configurable behaviour. Each attribute has:

| Property | Description |
|---|---|
| **Tag** | Gameplay Tag used to identify the attribute across the entire system |
| **BaseMax** | The default maximum value before any modifiers are applied |
| **ComputedMax** | The current effective maximum - recalculates dynamically when stat modifiers change |
| **MinValue** | The floor the value cannot go below (typically 0) |
| **Current Value** | The live value, always clamped between MinValue and ComputedMax |
| **bIsDepleted** | True when current value equals MinValue |
| **bIsAtMax** | True when current value equals ComputedMax |

---

## Attribute DataTable Structure

Attributes are defined in the **DT_AttributeDefinitions** DataTable. Each row represents one attribute and contains all configuration for that attribute's behaviour including decay rate, recovery rate, drift settings and more.

Modifying a row in the DataTable changes the attribute's behaviour globally without touching any Blueprint logic.

---

## The Nine Included Attributes

| Attribute | Tag | Behaviour Type |
|---|---|---|
| Health | Attribute.Health | Cascade target - damaged by other depleted attributes |
| Stamina | Attribute.Stamina | Drains on sprint, recovers at rest |
| Oxygen | Attribute.Oxygen | Zone controlled drain and recovery |
| Hunger | Attribute.Hunger | Constant slow decay |
| Hydration | Attribute.Hydration | Constant faster decay |
| Temperature | Attribute.Temperature | Drift based, zone controlled |
| Encumbrance | Attribute.Encumbrance | Set by external systems (inventory) |
| Mania | Attribute.Mania | BuildsUp - climbs toward max |
| Tiredness | Attribute.Tiredness | BuildsUp - climbs toward max |

---

## Clamping & ComputedMax

All attribute values are always clamped between **MinValue** and **ComputedMax**.

**ComputedMax** is not fixed - it recalculates whenever stat modifiers are applied or removed. This means a modifier can reduce the effective maximum of an attribute, which in turn clamps the current value down if it exceeds the new maximum.

The `bIsDepleted` and `bIsAtMax` flags are maintained automatically and update every time the value changes.

---

## BuildsUp Attributes

Mania and Tiredness work in reverse - they **build toward max** rather than draining toward zero.

- **Decay** causes the value to increase (build up)
- **Recovery** causes the value to decrease (drain back toward zero)
- Fatigue sources (tick modifiers) block recovery from running

This means all threshold logic still works identically - a high Mania value crossing 75% fires `OnThresholdEntered` exactly the same as a low Hunger value crossing 25%.

---

## Further Reading

- [Decay System](decay.md)
- [Recovery System](recovery.md)
- [Drift System](drift.md)
- [Attribute Reference](reference.md)
