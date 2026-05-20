# Quick Start Guide

This guide gets the system running on a character in five minutes.

---

## Minimal Setup Checklist

- [ ] Add **BP_AttributeComponent** to your actor
- [ ] Implement **BPI_AttributeSystem** interface on your actor
- [ ] Assign a **DA_AttributeSetPreset** to the component
- [ ] Press Play and verify attributes appear in the debug widget (F3)

---

## Interacting With the System

Once the component is on your actor and a preset is assigned, the system is live. Use the public API to read and modify attributes from any other Blueprint.

### Getting an Attribute Value

```
Get Component (BP_AttributeComponent)
→ GetAttributeValue (AttributeTag)
→ float (current value)
```

### Modifying an Attribute

```
Get Component (BP_AttributeComponent)
→ ModifyAttribute (AttributeTag, Delta)
```

> **Note:** `ModifyAttribute` applies a **delta** - pass a negative value to reduce an attribute, positive to increase it.

### Applying a Modifier

```
Get Component (BP_AttributeComponent)
→ ApplyModifier (DA_ModifierDefinition asset reference)
→ Handle (store this if you need to remove it later)
```

---

## Binding to Events

Bind to `OnAttributeChanged` on the component to react to any attribute change in gameplay code:

```
Get Component (BP_AttributeComponent)
→ Bind Event to OnAttributeChanged
→ Custom Event (AttributeTag, OldValue, NewValue)
```

For UI, use the **Client RPC** versions of all events - these fire on the owning client and are safe to bind to from widgets.

---

## Next Steps

- Read the [Architecture Overview](../architecture/overview.md) to understand how the system is structured
- Review the [Attribute Reference](../attributes/reference.md) for all nine included attributes
- See the [Public API Reference](../api/overview.md) for every available function

---

## Support

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
