# Stat Modifiers

Stat modifiers affect an attribute's **ComputedMax** - the effective ceiling of the attribute's current value. They do not change the current value directly, but by reducing or increasing the maximum they can indirectly clamp or expand the usable range of an attribute.

---

## How Stat Modifiers Work

When a stat modifier is applied, the system recalculates **ComputedMax** for the target attribute. If the current value exceeds the new ComputedMax it is clamped down to match. When the modifier is removed, ComputedMax recalculates again and the current value can recover back up naturally.

---

## The Three Stat Modifier Types

### Additive
Adds a flat value to the attribute's BaseMax.

```
ComputedMax = BaseMax + AdditiveValue
```

**Example:** WellFed adds +20 to Hunger's BaseMax, allowing the player to hold more Hunger than the base maximum temporarily.

Multiple additive modifiers stack - each one adds its value on top.

---

### Multiplicative
Applies a percentage multiplier to BaseMax. When multiple multiplicative modifiers are active, the **most restrictive one wins** - they do not stack multiplicatively.

```
ComputedMax = BaseMax * LowestMultiplier
```

**Example:** Dehydrated applies a 0.75 multiplier to Stamina's BaseMax, reducing maximum Stamina to 75% of normal. The Tiredness threshold modifiers (Weary, Tired, Exhausted, Broken) also use multiplicative modifiers - if both Dehydrated and Broken are active, the most restrictive multiplier (Broken at 0.15) wins.

---

### Override
Sets a hard cap on the attribute's ComputedMax regardless of all other modifiers.

```
ComputedMax = OverrideValue (ignores BaseMax and all other modifiers)
```

**Example:** An Override modifier of 50.0 on Health means the player can never exceed 50 Health regardless of any additive or multiplicative modifiers also present.

Use Override sparingly - it is an absolute cap and will always win over Additive and Multiplicative modifiers.

---

## Configuring a Stat Modifier

Inside a **DA_ModifierDefinition** asset, add an entry to the **StatModifiers** array:

| Field | Description |
|---|---|
| **AttributeTag** | Which attribute's ComputedMax to affect |
| **ModifierType** | Additive, Multiplicative, or Override |
| **Value** | Flat amount (Additive), multiplier 0.0-1.0 (Multiplicative), or hard cap value (Override) |

---

## When ComputedMax Updates

ComputedMax recalculates automatically whenever:
- A stat modifier is applied
- A stat modifier is removed
- A stat modifier expires via timed duration

You never need to manually trigger a recalculation.
