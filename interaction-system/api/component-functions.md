# Interaction Locking

Interaction Locking prevents multiple players from using the same interactable actor at the same time when exclusive access is required.

This is particularly useful for multiplayer interactions where only one player should be able to control or complete an interaction at once.

***

### What Is Interaction Locking?

When an interaction is locked, the system reserves that interactable for the player currently using it.

Other players can still detect the actor, but they cannot begin a conflicting interaction until the lock is released.

A typical locking flow is:

`Player Begins Interaction → Actor Locks → Interaction Runs → Interaction Ends → Actor Unlocks`

***

### Why Use Locking?

Not every interaction needs to be locked.

Locking is most useful for interactions where simultaneous access could cause conflicting gameplay behaviour.

Examples include:

* Opening a shared container
* Operating machinery
* Reviving a player
* Using a terminal
* Holding a lever
* Performing a timed interaction
* Manipulating a shared object

Simple interactions that can safely be triggered by multiple players may not require locking.

***

### Acquiring a Lock

When a player begins an interaction that requires exclusive access, the system attempts to lock the interactable.

If the actor is available, the interaction can continue.

If another player already owns the lock, the new interaction request is rejected.

This prevents multiple players from entering the same exclusive interaction state.

***

### Lock Ownership

A lock is associated with the player currently performing the interaction.

While that player owns the lock, other players cannot take ownership until the current interaction ends or the lock is released.

This allows the system to keep track of who is actively using the interactable.

***

### Releasing a Lock

The lock is released when the active interaction finishes.

This can happen when:

* The interaction completes
* The interaction is cancelled
* The player releases the interaction
* The interaction becomes invalid
* The current user stops interacting
* The system explicitly ends the interaction

Once released, another player can begin interacting with the actor.

***

### Locking and Sustained Interactions

Interaction locking is particularly useful with sustained interaction types.

For example, during a Hold To Complete interaction:

`Player Starts Hold → Actor Locks → Progress Runs → Interaction Completes → Actor Unlocks`

If the interaction is cancelled:

`Player Starts Hold → Actor Locks → Interaction Cancels → Actor Unlocks`

This ensures another player cannot begin the same interaction while it is already active.

***

### Locking and Focus

Locking and focus are separate concepts.

Multiple players can still focus the same actor at the same time.

The lock only determines whether a player is allowed to begin or continue an exclusive interaction.

For example:

`Player A Focuses Actor`

`Player B Focuses Actor`

`Player A Begins Interaction → Actor Locks`

`Player B Attempts Interaction → Request Rejected`

Focus remains local to each player, while interaction access is controlled by the lock.

***

### Multiplayer Authority

Interaction locking is handled authoritatively by the server.

This is important because two clients may attempt to interact with the same actor at nearly the same time.

The server determines which interaction request is accepted and updates the authoritative lock state.

A typical multiplayer flow is:

`Client Requests Interaction → Server Checks Lock → Lock Available → Interaction Begins`

If the actor is already locked:

`Client Requests Interaction → Server Checks Lock → Lock Unavailable → Interaction Rejected`

***

### Lock State Replication

Where required, lock information can be replicated so clients remain aware of the actor's current interaction state.

This allows presentation and gameplay systems to respond correctly when another player is already interacting with the actor.

The server remains the authoritative source for lock ownership.

***

### Gameplay Logic

Interaction locking manages access to the interaction itself.

Your actor does not need to manually prevent multiple players from executing the same interaction unless additional gameplay-specific restrictions are required.

This keeps access control inside the Interaction System while allowing the actor to focus only on its gameplay behaviour.

***

### When Not to Use Locking

Avoid locking interactions unnecessarily.

For example, a simple button that multiple players are allowed to press does not need exclusive ownership.

Locking should be enabled when simultaneous interaction would create conflicting, invalid, or undesirable gameplay behaviour.
