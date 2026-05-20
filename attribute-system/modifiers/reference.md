# Modifier Reference

Full reference for all modifiers included with the system.

---

## Status Modifiers

### Poison
Drains Health each tick. Timed duration. Stack rule: Stack.
Applied by: BP_PoisonZone on enter.

### WellFed
Additively increases Hunger's ComputedMax temporarily. Timed duration. Stack rule: Refresh.
Applied by: BP_FoodPickup on collect.

### Starving
Drains Health each tick. Applies HungerFatigue. Permanent until threshold exits.
Applied by: Hunger depleted threshold (AutoApplyModifier).

### Dehydrated
Reduces Stamina ComputedMax (multiplicative). Drains Health each tick. Applies HydrationFatigue. Permanent until threshold exits.
Applied by: Hydration depleted threshold (AutoApplyModifier).

### Drowning
Drains Health rapidly each tick. Permanent until threshold exits.
Applied by: Oxygen depleted threshold (AutoApplyModifier).

### Hypothermia
Drains Health each tick. Permanent until threshold exits.
Applied by: Temperature freezing threshold (AutoApplyModifier).

### Heatstroke
Drains Health each tick. Permanent until threshold exits.
Applied by: Temperature overheating threshold (AutoApplyModifier).

### Freezing
Drains Stamina each tick. Permanent until threshold exits.
Applied by: Temperature freezing threshold (AutoApplyModifier).

### Overheating
Drains Hydration each tick. Permanent until threshold exits.
Applied by: Temperature overheating threshold (AutoApplyModifier).

### Exhausted
Communicates exhausted state to the character. Blocks sprint. Permanent until threshold exits.
Applied by: Stamina depleted threshold (AutoApplyModifier).

---

## Fatigue Modifiers

### HungerFatigue
Increases Tiredness decay rate - Tiredness builds faster. Blocks Tiredness recovery. Permanent until Starving threshold exits.
Applied by: Starving modifier cascade.

### HydrationFatigue
Increases Tiredness decay rate - Tiredness builds faster. Blocks Tiredness recovery. Permanent until Dehydrated threshold exits.
Applied by: Dehydrated modifier cascade.

### PanicExhaustion
Dramatically increases Tiredness decay rate. Permanent until Mania Breaking threshold exits.
Applied by: Mania Breaking threshold (AutoApplyModifier).

---

## Tiredness Threshold Modifiers

### Weary
Reduces Stamina ComputedMax to 85% (multiplicative stat modifier). Applied at Tiredness 25%.

### Tired
Reduces Stamina ComputedMax to 65% (multiplicative stat modifier). Applied at Tiredness 50%.

### Exhausted (Tiredness)
Reduces Stamina ComputedMax to 40% (multiplicative stat modifier). Applied at Tiredness 75%.

### Broken
Reduces Stamina ComputedMax to 15% (multiplicative stat modifier). Applied at Tiredness 90%.
