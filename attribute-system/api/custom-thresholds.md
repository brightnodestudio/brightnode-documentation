# Creating Custom Thresholds

Adding new thresholds is done entirely through the DataTable - no Blueprint changes required.

---

## Step 1 - Create a Gameplay Tag

Open **Project Settings → Gameplay Tags** and add a new tag for your threshold, following the existing naming convention:

```
Threshold.Health.Critical
Threshold.Stamina.Winded
Threshold.YourAttribute.YourThresholdName
```

---

## Step 2 - Add a Row to DT_ThresholdDefinitions

Open **DT_ThresholdDefinitions** and add a new row:

| Field | Value |
|---|---|
| AttributeTag | The attribute this threshold belongs to |
| ThresholdTag | Your new Gameplay Tag |
| Percentage | The percentage of ComputedMax that triggers this threshold (0.0 to 1.0) |
| AutoApplyModifiers | Any DA_ModifierDefinition assets to apply on entry |
| Severity | Integer - higher values are returned by GetHighestSeverityThreshold |

---

## Step 3 - React to the Threshold

Bind to `OnThresholdEntered` and `OnThresholdExited` in your gameplay code or use the client RPC versions in your UI:

```
OnThresholdEntered (AttributeTag, ThresholdTag)
→ Branch on ThresholdTag == YourNewTag
→ Custom reaction logic
```

That is all that is required. The system will evaluate your new threshold automatically from the moment it is added to the DataTable.
