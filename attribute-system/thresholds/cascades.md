# Threshold Cascades

Cascades are the chains of consequence that make the survival system feel interconnected. No single attribute exists in isolation - depleting one will eventually damage others.

---

## How Cascades Work

A cascade is simply a threshold whose AutoApplyModifiers include a tick modifier targeting a different attribute. When Hunger depletes, the Starving modifier is applied - and Starving contains a tick modifier that drains Health every tick.

The cascade is entirely data driven. No custom Blueprint logic is required to create new cascades - just define the threshold and its AutoApplyModifiers.

---

## Included Cascade Chains

### Hunger → Health & Tiredness
```
Hunger reaches 0%
→ Starving modifier applied
  → Health drains each tick
  → HungerFatigue modifier applied (Tiredness decay rate increased)
```

### Hydration → Stamina & Health
```
Hydration reaches 0%
→ Dehydrated modifier applied
  → Stamina ComputedMax reduced (stat modifier)
  → Health drains each tick
  → HydrationFatigue modifier applied (Tiredness decay rate increased)
```

### Oxygen → Health
```
Oxygen reaches 0%
→ Drowning modifier applied
  → Health drains rapidly each tick
```

### Temperature (Cold) → Stamina & Health
```
Temperature reaches freezing threshold
→ Freezing modifier applied (Stamina drains each tick)
→ Hypothermia modifier applied (Health drains each tick)
```

### Temperature (Hot) → Hydration & Health
```
Temperature reaches overheating threshold
→ Overheating modifier applied (Hydration drains each tick)
→ Heatstroke modifier applied (Health drains each tick)
```

### Tiredness → Stamina Max (Four Stage)
```
Tiredness reaches 25% → Weary → Stamina max reduced to 85%
Tiredness reaches 50% → Tired → Stamina max reduced to 65%
Tiredness reaches 75% → Exhausted → Stamina max reduced to 40%
Tiredness reaches 90% → Broken → Stamina max reduced to 15%
```

### Mania → Tiredness
```
Mania reaches 100%
→ PanicExhaustion modifier applied
  → Tiredness decay rate increases rapidly
```

### Stamina → Sprint State
```
Stamina reaches 0%
→ Exhausted modifier applied
  → Sprint blocked, exhausted state communicated to character
```

---

## The Worst Case Scenario

All cascades are additive and simultaneous. A character who is Starving, Dehydrated, Freezing and Broken from Tiredness will be experiencing:

- Health draining from three separate tick modifiers simultaneously
- Stamina max crushed to 15% from Tiredness
- Stamina also draining from the Freezing modifier
- Hydration draining from the Overheating or normal decay
- Sprint locked out from Stamina depletion

This compounds naturally from the data - no special case logic required.
