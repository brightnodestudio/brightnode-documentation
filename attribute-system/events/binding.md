# Binding Events in Blueprint

The system communicates state changes through event dispatchers. This page covers the correct patterns for binding to those events in different Blueprint contexts.

---

## The Golden Rule

Always bind to **server-side dispatchers** from gameplay code running on the server.
Always bind to **Client RPC events** from widgets and any client-side logic.

Mixing these up is the most common source of UI desyncing in multiplayer.

---

## Binding From an Actor Blueprint

Use this pattern to react to attribute changes in gameplay code - for example triggering animations, sound cues, or AI state changes:

```
Event BeginPlay
→ Get BP_AttributeComponent (GetComponentByClass)
→ Bind Event to OnAttributeChanged
    → Custom Event: On Attribute Changed (AttributeTag, OldValue, NewValue)
    → Your gameplay logic here
```

For threshold reactions in gameplay code:
```
Event BeginPlay
→ Get BP_AttributeComponent
→ Bind Event to OnThresholdEntered
    → Custom Event: On Threshold Entered (AttributeTag, ThresholdTag)
    → Switch on ThresholdTag
    → Your reaction per threshold
```

---

## Binding From a Widget Blueprint

Widgets must always use **Client RPC events**. Bind on Construct and ensure you are getting the component from the owning player pawn:

```
Event Construct
→ Get Owning Player Pawn
→ Cast / Check implements BPI_AttributeSystem
→ Get BP_AttributeComponent
→ Bind Event to Client_OnAttributeChanged
    → Custom Event: On Attribute Changed (AttributeTag, OldValue, NewValue)
    → Filter by AttributeTag if this widget only cares about one attribute
    → Update widget display
```

---

## Filtering by Attribute Tag

When one event binding covers multiple attributes, use a Branch or Switch on the AttributeTag to filter:

```
On Attribute Changed (AttributeTag, OldValue, NewValue)
→ Switch on GameplayTag (AttributeTag)
    → Attribute.Health → Update Health bar
    → Attribute.Stamina → Update Stamina bar
    → Attribute.Hunger → Update Hunger bar
```

---

## Binding to OnInitialized

The component fires `OnInitialized` (and `Client_OnInitialized`) once all attributes are set up and ready. Bind to this before making any attribute queries to ensure the component is fully ready:

```
Event Construct
→ Get BP_AttributeComponent
→ Bind Event to Client_OnInitialized
    → Custom Event: On Initialized
    → Now safe to call GetAttributeValue, GetAttributePercent etc.
    → Set initial widget values
```

---

## Unbinding on Destruct

If your widget or actor can be destroyed while the component still exists, unbind your events on Destruct to avoid dangling references:

```
Event Destruct
→ Get BP_AttributeComponent
→ Unbind Event from Client_OnAttributeChanged
```
