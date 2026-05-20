# Tick Modifiers

Tick modifiers apply a **delta to an attribute value every decay tick**. They are the mechanism behind all sustained drain and gain effects - poison draining Health, hunger cascade draining Health, temperature modifiers pushing drift targets.

---

## How Tick Modifiers Work

Every decay tick, the system iterates all active tick modifiers on the component and applies their delta to the target attribute. This happens automatically - no Blueprint logic required once the modifier is applied.

Multiple tick modifiers targeting the same attribute all apply independently each tick. Their effects are cumulative.

---

## The Two Tick Modifier Types

### Direct Delta
Changes the attribute value directly by the configured amount each tick.

```
AttributeValue += DeltaPerTick (each decay tick)
```

Pass a **negative** DeltaPerTick to drain an attribute. Pass a **positive** value to restore it.

**Examples:**
- Poison: `-2.0` delta per tick on Health - drains Health each tick
- Drowning: `-5.0` delta per tick on Health - drains Health rapidly each tick
- A healing spring: `+3.0` delta per tick on Health - restores Health each tick

---

### Drift Offset
Pushes the **drift target** of a drifting attribute rather than the value directly. Only relevant for attributes using the drift system (Temperature).

```
DriftTarget += DriftOffsetPerTick
```

**Example:** A Freezing modifier applies a drift offset that pushes the Temperature drift target colder than the zone alone would set it - simulating wind chill or wet clothing on top of the environment temperature.

---

## Fatigue Source Flag

Each tick modifier entry has a **bIsFatigueSource** boolean. When set to true, this modifier blocks recovery on the target attribute while it is active.

**Example:** HungerFatigue has bIsFatigueSource set to true on Tiredness - while the character is Starving, Tiredness cannot recover even if other recovery conditions are met.

---

## Configuring a Tick Modifier

Inside a **DA_ModifierDefinition** asset, add an entry to the **TickModifiers** array:

| Field | Description |
|---|---|
| **AttributeTag** | Which attribute to affect each tick |
| **TickType** | DirectDelta or DriftOffset |
| **DeltaPerTick** | How much to change per tick - negative to drain, positive to restore |
| **bIsFatigueSource** | If true, blocks recovery on the target attribute while active |

---

## Tick Rate

Tick modifiers apply on the **decay tick** - the same tick interval that drives attribute decay. This rate is consistent across all attributes and all tick modifiers, keeping behaviour predictable and easy to tune in the DataTable.
