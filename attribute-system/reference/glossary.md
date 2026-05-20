# Glossary

**Attribute**
A named, clamped float value managed by BP_AttributeComponent. Attributes change over time through decay, recovery, drift, and direct modification.

**BaseMax**
The default maximum value of an attribute before any modifiers are applied.

**BuildsUp Attribute**
An attribute that climbs toward max rather than draining toward zero. Mania and Tiredness are BuildsUp attributes. Decay causes them to increase; recovery causes them to decrease.

**Cascade**
A chain of consequences triggered when an attribute is depleted. For example, Hunger depleting causes the Starving modifier to apply, which drains Health each tick.

**ComputedMax**
The effective maximum of an attribute after all stat modifiers are applied. Recalculates dynamically whenever stat modifiers are added or removed.

**DA_AttributeSetPreset**
A DataAsset defining which attributes an actor uses. Assigned to BP_AttributeComponent in the Details panel.

**DA_ModifierDefinition**
A DataAsset defining a single modifier - its display name, stack rule, duration, stat modifiers, and tick modifiers.

**Decay**
The automatic change of an attribute value over time. Three behaviours: Constant, Accelerating, Decelerating.

**Delta**
The amount by which a value changes. Used in ModifyAttribute - pass a positive delta to increase, negative to decrease.

**Drift**
An attribute behaviour where the value moves toward a target rather than decaying at a fixed rate. Temperature uses drift.

**DT_AttributeDefinitions**
The DataTable containing all attribute configuration rows.

**DT_ThresholdDefinitions**
The DataTable containing all threshold configuration rows.

**Fatigue Source**
A tick modifier flagged as a fatigue source. While active, it blocks recovery on the target attribute.

**ModifierHandle**
A reference returned by ApplyModifier used to identify and remove a specific modifier instance later.

**Recovery**
The automatic restoration of an attribute value when conditions are met and no fatigue sources are blocking.

**Server Authority**
The pattern where all game state changes happen on the server and are replicated to clients. The Attribute System uses full server authority.

**Stat Modifier**
A modifier that affects an attribute's ComputedMax. Types: Additive, Multiplicative, Override.

**Threshold**
A percentage-based trigger point on an attribute. When the attribute value crosses the threshold, OnThresholdEntered fires and AutoApplyModifiers are applied.

**Tick Modifier**
A modifier that applies a delta to an attribute value every decay tick. Types: DirectDelta, DriftOffset.
