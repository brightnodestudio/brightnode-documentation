# Multiplayer Overview

The Attribute System is built multiplayer-first. All attribute state lives on the server and replicates to clients automatically.

---

## Server Authority Model

Every attribute change, threshold evaluation, modifier application, and decay tick happens on the **server**. Clients never modify attribute state directly.

All public API write functions automatically route through server RPCs if called from a client context. You do not need to manually manage this - call any function from any context and the system handles the network layer.

---

## Replicated State

The following state is replicated to all clients:
- Current attribute values
- Active threshold states
- Active modifier list

This means any client can read accurate attribute data at any time using the query functions.

---

## Client RPC Events

Because attribute changes happen on the server, UI updates are driven by **client RPC events** rather than direct binding to replicated properties. Every server-side dispatcher has a client RPC mirror that fires specifically on the owning client.

Always bind UI widgets and client-side reactions to the **Client_** prefixed event versions.

---

## Common Multiplayer Pitfalls

### Walk speed not updating on client after threshold exit
The `CharacterMovement->MaxWalkSpeed` must be set on the owning client. Bind to `Client_OnThresholdExited` rather than the server dispatcher and set walk speed there.

### UI not updating in multiplayer
Ensure your widgets are binding to `Client_OnAttributeChanged` and not the server-side `OnAttributeChanged` dispatcher.

### SetAttributeValue not firing threshold events
`SetAttributeValue` bypasses threshold evaluation entirely. Use `ModifyAttribute` with a calculated delta instead when threshold events are required.

### Component not found on client
Ensure your actor has **Replicates** enabled in its Class Defaults. The component will not be accessible on clients if the actor itself does not replicate.
