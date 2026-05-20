# Symbol System

The symbol system spawns configurable world-space symbol actors attached to target actors in the world.

## How It Works

When a symbol is spawned on a target actor, the system creates a symbol actor and attaches it to the target. The symbol actor uses the settings defined in the assigned **DA\_SymbolPreset**.

When the symbol is cleared, the symbol actor is destroyed and removed from the target.

## DA_SymbolPreset

Each symbol style is defined as a **DA\_SymbolPreset** data asset containing:

- Preset ID — unique identifier used by the system to find the preset
- Symbol appearance and behaviour settings

## Spawning and Clearing Symbols

Use **Spawn Symbol Actor** to attach a symbol to a target actor.

Use **Clear Symbol On Actor** to remove it.

Use the helper function on **AC\_VisualMarkingSystem** to check whether a symbol is already attached before spawning — this prevents duplicate symbols on the same actor.
