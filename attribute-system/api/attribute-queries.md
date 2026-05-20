# Attribute Queries

Read-only functions for retrieving attribute state from **BP_AttributeComponent**. These are safe to call from any context - client or server - as they only read replicated state.

---

## GetAttributeValue

Returns the current value of an attribute as a float.

```
GetAttributeValue (AttributeTag: GameplayTag) → float
```

**Example use:** Reading the current Health value to decide whether to play a low health animation.

---

## GetAttributePercent

Returns the current value as a normalised percentage of ComputedMax, between 0.0 and 1.0.

```
GetAttributePercent (AttributeTag: GameplayTag) → float
```

**Example use:** Driving a progress bar fill amount directly without needing to divide manually.

---

## GetAttributeMax

Returns the current **ComputedMax** of an attribute - the effective maximum after all stat modifiers are applied.

```
GetAttributeMax (AttributeTag: GameplayTag) → float
```

**Example use:** Displaying the current maximum alongside the current value in a UI text element (e.g. "73 / 85").

---

## GetAttributeMin

Returns the **MinValue** of an attribute - the floor the value cannot go below. Typically 0.0 for all attributes.

```
GetAttributeMin (AttributeTag: GameplayTag) → float
```

---

## IsAttributeValid

Returns true if the specified attribute tag exists on this component's assigned preset. Use this to safely guard attribute queries before calling them.

```
IsAttributeValid (AttributeTag: GameplayTag) → bool
```

**Example use:** Checking whether an AI actor using the Animal preset has a Mania attribute before trying to read it.

---

## GetAllAttributes

Returns a **GameplayTagContainer** containing all attribute tags currently active on this component based on the assigned preset.

```
GetAllAttributes () → GameplayTagContainer
```

**Example use:** Iterating all attributes on a component to populate a dynamic UI list or debug display.

---

## Usage Notes

- All query functions are safe to call on both server and client
- Queries return replicated state - values are accurate on clients without any additional setup
- Always use `IsAttributeValid` before querying an attribute if you are not certain the preset includes it
