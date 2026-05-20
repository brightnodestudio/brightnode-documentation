# Event Dispatchers

The system fires events at every meaningful state change. All server-side dispatchers have client RPC mirrors for UI and client-side reactions.

---

## Server Side Dispatchers

Bind to these from gameplay code running on the server or from actor Blueprints:

| Dispatcher | Parameters | Fires When |
|---|---|---|
| OnAttributeChanged | AttributeTag, OldValue, NewValue | Any attribute value changes |
| OnThresholdEntered | AttributeTag, ThresholdTag | An attribute crosses a threshold downward |
| OnThresholdExited | AttributeTag, ThresholdTag | An attribute recovers past a threshold upward |
| OnAttributeDepleted | AttributeTag | An attribute reaches MinValue |
| OnAttributeFull | AttributeTag | An attribute reaches ComputedMax |
| OnModifierApplied | Handle | A modifier is successfully applied |
| OnModifierRemoved | Handle | A modifier is removed (manually or via expiry) |
| OnInitialized | - | The component finishes initializing all attributes |

---

## Client RPC Events

Every server dispatcher has a client RPC mirror that fires on the owning client. These are the events to bind to from UI widgets and client-side Blueprint logic:

| Client Event | Mirrors |
|---|---|
| Client_OnAttributeChanged | OnAttributeChanged |
| Client_OnThresholdEntered | OnThresholdEntered |
| Client_OnThresholdExited | OnThresholdExited |
| Client_OnAttributeDepleted | OnAttributeDepleted |
| Client_OnAttributeFull | OnAttributeFull |
| Client_OnModifierApplied | OnModifierApplied |
| Client_OnModifierRemoved | OnModifierRemoved |
| Client_OnInitialized | OnInitialized |

---

## Binding Events in Blueprint

### From an Actor Blueprint
```
BeginPlay
→ Get BP_AttributeComponent
→ Bind Event to OnAttributeChanged
→ Custom Event node (AttributeTag, OldValue, NewValue)
→ Your logic here
```

### From a Widget Blueprint
Bind to the **Client RPC** version of the event - never the server dispatcher from a widget:
```
Construct
→ Get Owning Player Pawn
→ Get BP_AttributeComponent
→ Bind Event to Client_OnAttributeChanged
→ Custom Event node
→ Update widget display
```

> **Multiplayer note:** Always use Client RPC events in widgets. Server dispatchers may not fire on the client and will cause UI to desync in multiplayer sessions.
