# Drift System

The drift system allows attributes to move toward a target value rather than decaying at a fixed rate. Temperature is the primary example - it drifts toward whatever the current zone dictates.

---

## How Drift Works

Instead of draining or building at a constant rate, a drifting attribute moves its current value toward a **drift target** each tick. The closer the current value is to the target, the slower the drift becomes.

This creates a natural, organic feel - temperature changes feel gradual and believable rather than mechanical.

---

## Setting a Drift Target

Drift targets are set via the public API:

```
SetDriftTarget (AttributeTag, TargetValue)
```

This is typically called by zone actors when the player enters or exits them.

---

## Zone Priority System

Multiple overlapping zones can each try to set a drift target. The system resolves conflicts via a **priority system** - each zone has a priority value and the highest priority zone always wins.

This means a heat zone inside a cold zone will correctly override the cold zone's drift target for any player inside both.

---

## Drift Offset Tick Modifiers

Modifiers can include **drift offset** values - these push the drift target rather than the attribute value directly. This allows modifiers to influence temperature drift without overriding the zone's base target.

For example, a Freezing modifier could push the drift target 10 units colder than the zone would naturally set it - simulating wet clothes or wind chill on top of the environment.

---

## Configuring Drift

Each attribute row in **DT_AttributeDefinitions** exposes:

| Property | Description |
|---|---|
| **bUsesDrift** | Whether this attribute uses drift instead of standard decay |
| **DriftRate** | How fast the value moves toward the drift target per tick |
