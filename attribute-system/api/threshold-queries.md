# Threshold Queries

Read-only functions for querying the current threshold state of attributes on **BP_AttributeComponent**. Safe to call from any context.

---

## GetActiveThresholds

Returns a **GameplayTagContainer** of all threshold tags currently active on a specific attribute.

```
GetActiveThresholds (AttributeTag: GameplayTag) → GameplayTagContainer
```

A threshold is considered active when the attribute value is at or below the threshold percentage and has not yet recovered past it.

**Example use:** Checking whether multiple thresholds are simultaneously active to drive a compound UI state - for example showing a different icon when both Hungry and Thirsty thresholds are active at the same time.

---

## GetCurrentThreshold

Returns the **single lowest active threshold tag** for a specific attribute - the most severe threshold currently crossed.

```
GetCurrentThreshold (AttributeTag: GameplayTag) → GameplayTag
```

Returns an empty tag if no threshold is currently active for that attribute.

**Example use:** Switching a UI element's visual state based on the current worst threshold - for example changing a Hunger icon colour based on whether the player is Hungry or Starving.

---

## GetHighestSeverityThreshold

Returns the highest severity active threshold tag across a specific attribute, based on the **Severity** value defined in DT_ThresholdDefinitions.

```
GetHighestSeverityThreshold (AttributeTag: GameplayTag) → GameplayTag
```

Severity is an integer you define per threshold row - higher integers are considered more severe. This function returns the tag of whichever active threshold has the highest severity value.

**Example use:** Driving a single status display that always shows the most critical active condition - useful for simplified HUDs or AI decision making based on worst current state.

---

## Usage Pattern

A common pattern for reacting to threshold state in UI:

```
Client_OnThresholdEntered (AttributeTag, ThresholdTag)
→ GetCurrentThreshold (AttributeTag)
→ Switch on ThresholdTag
→ Update widget visual per threshold
```

This keeps UI logic clean - react to the event, then query the current state rather than storing threshold state manually in the widget.
