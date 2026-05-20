# Architecture Overview

Understanding the architecture of the Attribute System will help you integrate it cleanly and extend it confidently.

---

## Component & Interface Pattern

The system is built around a **component and interface** pattern - a standard Unreal Engine approach that keeps the system decoupled from your actor classes.

- **BP_AttributeComponent** - the core component that manages all attribute state, decay, recovery, thresholds and modifiers. Drop it onto any actor.
- **BPI_AttributeSystem** - the interface your actor implements. The component communicates through this interface, meaning it works with any actor type without needing to cast to a specific class.

This means the system works equally well on characters, AI, animals, vehicles, or any other actor - as long as the component is attached and the interface is implemented.

---

## Data Driven Design

All configuration lives in **DataTables** and **DataAssets** - not in Blueprint logic. This is intentional.

| Asset Type | Purpose |
|---|---|
| DataTable | Attribute definitions, decay rates, recovery rates, threshold definitions |
| DA_AttributeSetPreset | Defines which attributes an actor uses |
| DA_ModifierDefinition | Defines a single modifier with all its properties |

Designers can open any DataTable or DataAsset and change values without touching Blueprint nodes. New attributes, thresholds, and modifiers are added through data - not code.

---

## How Attributes, Thresholds and Modifiers Relate

```
Attribute
  └── Has a current Value (clamped between MinValue and ComputedMax)
  └── Has Thresholds (percentage-based trigger points)
        └── Threshold crossed → fires OnThresholdEntered
        └── Threshold auto-applies Modifiers
              └── Modifier affects ComputedMax (Stat Modifier)
              └── Modifier applies delta each tick (Tick Modifier)
  └── Has Decay (value changes over time automatically)
  └── Has Recovery (value restores when conditions are met)
```

Everything flows in one direction. Attributes hold values. Thresholds react to those values. Modifiers change what those values can be or how they change over time.

---

## Server Authority & Multiplayer Model

The system uses a **server authority model** - all attribute changes, threshold evaluations, and modifier applications happen on the server.

- All write functions have **server RPC companions** that route through the server automatically
- Attribute state is **replicated** to all clients
- **Client RPC events** mirror all server-side dispatchers so UI and client-side reactions stay in sync

You never need to manually manage replication. Call any public API function and the system handles the network layer for you.

---

## Flow Summary

```
Gameplay Code → Public API Function
  → Server RPC (if called from client)
  → Server evaluates change
  → Attribute value updated
  → Threshold evaluation runs
  → Modifiers applied / removed as needed
  → OnAttributeChanged dispatcher fires (server)
  → Client RPC event fires (owning client)
  → UI updates via client event binding
```

---

## Support

- 💬 **Discord** - [discord.gg/VSu4A7XxA7](https://discord.gg/VSu4A7XxA7)
- 📧 **Email** - brightnodestudio@gmail.com
