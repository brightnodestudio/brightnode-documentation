# Attribute Reference

Full reference for all nine attributes included in the system.

---

## Health

**Tag:** `Attribute.Health`
**Behaviour:** Cascade target
**Preset:** Human

Health represents physical condition. It has no natural decay - it is damaged exclusively through modifier cascades from other depleted attributes. Keep all other attributes in check and Health will look after itself.

**Threshold Cascades Into Health:**
- Hunger depleted → Starving modifier (Health drain)
- Hydration depleted → Dehydrated modifier (Health drain)
- Oxygen depleted → Drowning modifier (rapid Health drain)
- Temperature freezing → Hypothermia modifier (Health drain)
- Temperature overheating → Heatstroke modifier (Health drain)

---

## Stamina

**Tag:** `Attribute.Stamina`
**Behaviour:** Drains on sprint, recovers at rest
**Preset:** Human, Animal

Stamina is physical energy. It drains while sprinting and recovers when the character is at rest. The Tiredness attribute progressively reduces Stamina's ComputedMax through four thresholds, meaning an exhausted character has significantly less Stamina available than a rested one.

**Threshold:**
- Exhausted (0%) → Applies Exhausted modifier, blocks sprint

---

## Oxygen

**Tag:** `Attribute.Oxygen`
**Behaviour:** Zone controlled
**Preset:** Human, Animal

Oxygen drains inside oxygen-depriving zones (underwater, gas zones) and recovers when the character exits. The Oxygen UI widget shows and hides dynamically based on zone presence via client RPC events.

**Threshold:**
- Drowning (0%) → Applies Drowning modifier (rapid Health drain)

---

## Hunger

**Tag:** `Attribute.Hunger`
**Behaviour:** Constant slow decay
**Preset:** Human

Hunger drains slowly and constantly at all times. Depletion triggers a cascade that damages Health and accelerates Tiredness.

**Thresholds:**
- Starving (0%) → Applies Starving modifier (Health drain) + HungerFatigue (Tiredness builds faster)

---

## Hydration

**Tag:** `Attribute.Hydration`
**Behaviour:** Constant faster decay
**Preset:** Human

Hydration drains faster than Hunger. Depletion reduces Stamina max and drains Health simultaneously - the double penalty makes Hydration the most immediately punishing of the two sustenance attributes.

**Thresholds:**
- Dehydrated (0%) → Applies Dehydrated modifier (Stamina max reduced + Health drain) + HydrationFatigue (Tiredness builds faster)

---

## Temperature

**Tag:** `Attribute.Temperature`
**Behaviour:** Drift based, zone controlled
**Preset:** Human, Animal

Temperature drifts toward the target set by the current highest-priority zone. It does not decay or recover in the traditional sense - it simply moves toward its target. Extreme values in either direction cascade into Health through separate modifier chains.

**Thresholds:**
- Freezing (low %) → Applies Freezing modifier (Stamina drain) + Hypothermia (Health drain)
- Overheating (high %) → Applies Overheating modifier (Hydration drain) + Heatstroke (Health drain)

---

## Encumbrance

**Tag:** `Attribute.Encumbrance`
**Behaviour:** Set by external systems
**Preset:** Human

Encumbrance tracks carry weight. It has no natural decay or recovery - it is set directly by inventory or equipment systems via `ModifyAttribute` or `SetAttributeValue`. Threshold crossings trigger movement speed changes on the character.

**Thresholds:**
- Heavy (75%) → Movement speed reduced
- Overburdened (100%) → Cannot pick up further items

> **Important:** Always use `ModifyAttribute` with a negative delta to remove encumbrance when dropping items. Using `SetAttributeValue` to zero the attribute bypasses threshold evaluation and `OnThresholdExited` will not fire.

---

## Mania

**Tag:** `Attribute.Mania`
**Behaviour:** BuildsUp - climbs toward max in darkness
**Preset:** Human, Zombie

Mania represents mental stability. It builds in darkness and recovers slowly in light. As a BuildsUp attribute it climbs toward max rather than draining - recovery pulls it back toward zero. Reaching the Breaking threshold triggers PanicExhaustion, causing Tiredness to spike rapidly.

**Thresholds:**
- Unsettled (50%) → Visual warning
- Anxious (75%) → Stronger visual warning
- Breaking (100%) → Applies PanicExhaustion modifier (Tiredness builds rapidly)

---

## Tiredness

**Tag:** `Attribute.Tiredness`
**Behaviour:** BuildsUp - climbs toward max over time
**Preset:** Human

Tiredness builds constantly - just existing accumulates fatigue. As a BuildsUp attribute it climbs toward max. Four progressive thresholds each reduce Stamina's ComputedMax further, until a Broken character has almost no Stamina available at all. Rest is the only cure.

**Thresholds:**
- Weary (25%) → Stamina max reduced to 85%
- Tired (50%) → Stamina max reduced to 65%
- Exhausted (75%) → Stamina max reduced to 40%
- Broken (90%) → Stamina max reduced to 15%
