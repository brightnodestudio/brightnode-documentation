# Stacking Rules

Stacking rules define how the system behaves when a modifier that is already active gets applied again.

---

## The Four Stack Rules

| Rule | Behaviour |
|---|---|
| **Stack** | Multiple instances are allowed. Each application creates a new independent instance. |
| **Ignore** | Only one instance is allowed. Subsequent applications are silently ignored while the original remains active. |
| **Refresh** | Only one instance is allowed. Reapplication resets the duration timer on the existing instance without creating a new one. |
| **Replace** | The existing instance is removed and a fresh instance is applied. Useful for modifiers that should restart cleanly on reapplication. |

---

## Choosing the Right Rule

| Scenario | Recommended Rule |
|---|---|
| Poison that stacks from multiple sources | Stack |
| A zone effect that should only apply once | Ignore |
| A buff with a duration that refreshes on re-pickup | Refresh |
| A status effect that should always restart fresh | Replace |
