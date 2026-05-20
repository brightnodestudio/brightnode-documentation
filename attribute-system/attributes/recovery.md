# Recovery System

Recovery is the automatic restoration of an attribute's value when conditions are met.

---

## How Recovery Works

When an attribute is below its ComputedMax and no active fatigue sources are blocking recovery, the attribute will automatically recover at its configured rate after the recovery delay has elapsed.

For **BuildsUp** attributes (Mania and Tiredness), recovery works in reverse - it drains the value back toward zero rather than restoring it toward max.

---

## Configuring Recovery

Each attribute row in **DT_AttributeDefinitions** exposes:

| Property | Description |
|---|---|
| **RecoveryRate** | How much the value restores per recovery tick |
| **RecoveryDelay** | How long after the last change before recovery begins |
| **bRecoveryEnabled** | Whether recovery runs at all for this attribute |

---

## Blocking Recovery

Recovery is automatically blocked while **active fatigue sources** are present. Fatigue sources are tick modifiers flagged as fatigue sources in their **DA_ModifierDefinition**.

Examples:
- **Tiredness** will not recover while the character is Starving (HungerFatigue tick modifier active)
- **Mania** will not recover while inside a darkness zone (darkness tick modifier active)

This creates a natural dependency chain - fix the root cause first before recovery can resume.

---

## Pausing & Resuming Recovery

Recovery can be paused and resumed at runtime:

```
PauseRecovery (AttributeTag)    - pause a single attribute's recovery
ResumeRecovery (AttributeTag)   - resume a single attribute's recovery
```
