# Threshold System

Thresholds are percentage-based trigger points that fire events and automatically apply or remove modifiers when an attribute crosses them.

---

## What Is a Threshold?

A threshold is a defined percentage of an attribute's ComputedMax. When the attribute's current value crosses that percentage - either going down or coming back up - the threshold system fires events and manages any associated modifiers automatically.

---

## DT_ThresholdDefinitions Structure

Thresholds are defined in the **DT_ThresholdDefinitions** DataTable. Each row represents one threshold and contains:

| Property | Description |
|---|---|
| **AttributeTag** | Which attribute this threshold belongs to |
| **ThresholdTag** | Gameplay Tag identifying this threshold |
| **Percentage** | The percentage of ComputedMax that triggers this threshold |
| **AutoApplyModifiers** | Array of DA_ModifierDefinition assets to apply on entry |
| **Severity** | Used by GetHighestSeverityThreshold for priority queries |

---

## How Threshold Evaluation Works

Every time an attribute value changes, the system evaluates all thresholds for that attribute:

1. Calculate the current percentage (CurrentValue / ComputedMax)
2. Compare against all defined threshold percentages
3. For any threshold that has been newly crossed downward → fire `OnThresholdEntered`
4. For any threshold that has been newly exited upward → fire `OnThresholdExited`
5. Apply or remove AutoApplyModifiers accordingly

Threshold state is maintained per-attribute so the system knows which thresholds are currently active at any time.

---

## AutoApplyModifiers

Each threshold can define an array of **AutoApplyModifiers** - DA_ModifierDefinition assets that are automatically applied when the threshold is entered and automatically removed when the threshold is exited.

This is the mechanism behind all cascade effects in the system. You never need to manually apply or remove cascade modifiers - the threshold system handles it entirely.

---

## Events

```
OnThresholdEntered (AttributeTag, ThresholdTag)   - fires on server when threshold is entered
OnThresholdExited (AttributeTag, ThresholdTag)    - fires on server when threshold is exited
```

Client RPC versions of both events fire on the owning client for UI and client-side reactions.

---

## Querying Threshold State

```
GetActiveThresholds (AttributeTag)              - returns array of currently active threshold tags
GetCurrentThreshold (AttributeTag)              - returns the current lowest threshold tag
GetHighestSeverityThreshold (AttributeTag)      - returns the highest severity active threshold
```
