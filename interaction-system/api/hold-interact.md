# Multiplayer

The Brightnode Interaction System is designed for multiplayer projects and uses a server-authoritative interaction flow.

Player-facing systems such as focus detection and prompts remain local, while gameplay-affecting interaction execution is validated and handled by the server.

***

### Multiplayer Overview

A typical multiplayer interaction follows this flow:

`Local Focus → Player Input → Server Request → Server Validation → Interaction Execution → Replicated State`

This keeps interaction feedback responsive for the local player while ensuring gameplay actions remain authoritative.

***

### Local Focus Detection

Focus detection is handled locally for each player.

Each client independently determines which interactable actor they are currently looking at.

This includes:

* Interaction tracing
* Current focused actor
* Prompt visibility
* Input icon display
* Focus outlines

One player's focus does not affect another player's focus.

Multiple players can focus the same actor at the same time.

***

### Interaction Requests

When the player attempts to interact, the local Interaction Component sends the interaction request through the multiplayer flow.

The server then determines whether the interaction is valid.

Validation can include checks such as:

* The actor is interactable
* The interaction is currently available
* The player is allowed to interact
* The actor is not locked by another player
* The requested interaction state is valid

If validation succeeds, the server executes the interaction.

***

### Server Authority

Gameplay-affecting interactions are handled authoritatively by the server.

This means the server controls the final interaction result rather than trusting the client to execute gameplay directly.

Examples include:

* Activating gameplay logic
* Starting sustained interactions
* Completing interactions
* Cancelling interactions
* Lock ownership
* Updating replicated interaction state

This provides a consistent interaction flow across all connected players.

***

### Replicated Interaction State

Interaction state is replicated where required so clients remain synchronised with the server.

Replicated state can be used to update:

* Interaction presentation
* Active interaction state
* Completion behaviour
* Cancellation behaviour
* Lock state
* Gameplay feedback

The server remains the authoritative source of the replicated value.

***

### RepNotify Updates

Replicated interaction state can use RepNotify to trigger local responses when the server changes a value.

This allows client-side systems to react to authoritative state changes without manually polling the server.

Typical uses include:

* Updating prompts
* Responding to interaction state changes
* Refreshing presentation
* Triggering local feedback

The component containing replicated properties must itself be configured to replicate.

If the component does not replicate, its RepNotify events will not reach clients.

***

### Interaction Locking

Interaction locks are also controlled by the server.

When an interaction requires exclusive access, the server determines whether the actor is available and assigns ownership of the lock.

For example:

`Player A Requests Interaction → Server Grants Lock`

`Player B Requests Interaction → Server Detects Existing Lock → Request Rejected`

When Player A finishes or cancels the interaction, the lock is released.

This prevents conflicting interactions when multiple clients attempt to use the same actor.

***

### Sustained Interactions

Hold To Complete and While Holding interactions rely on the same authoritative multiplayer flow.

A typical sustained interaction can follow:

`Client Begins Interaction → Server Starts Interaction → State Replicates → Interaction Continues → Server Completes or Cancels`

The local player can still receive responsive UI feedback while the server maintains authority over the gameplay state.

***

### Press Interactions

Press interactions generally have a shorter lifecycle:

`Client Requests Interaction → Server Validates → Server Executes → State Updates`

These interactions can appear immediate to the player while still being executed authoritatively.

***

### Grab Interactions

Grab interactions also use the multiplayer interaction flow.

The interaction request and grab state are validated through the server so ownership and state remain consistent between clients.

Any additional physics or movement replication required by the grabbed actor should still follow normal Unreal Engine networking rules.

***

### Local Presentation vs Server Gameplay

A useful way to think about the multiplayer architecture is:

| Local Player       | Server                 |
| ------------------ | ---------------------- |
| Focus detection    | Interaction validation |
| Prompt display     | Gameplay execution     |
| Input icons        | Interaction state      |
| Focus outline      | Lock ownership         |
| Local presentation | Authoritative results  |

This separation keeps UI responsive while protecting gameplay logic from client-side authority.

***

### Multiplayer Debugging

If an interaction works as the server but not as a client, check:

* The relevant components are set to replicate
* The actor itself is replicated where required
* Replicated properties are being changed on the server
* RepNotify is configured correctly
* The client interaction request reaches the server
* The actor is not currently locked
* The interaction is valid on the server
* Client-side presentation is not being mistaken for gameplay execution

Running the game with both server and client windows visible can make interaction state and replication issues much easier to diagnose.
