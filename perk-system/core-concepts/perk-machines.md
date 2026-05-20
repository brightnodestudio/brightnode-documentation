# Perk Machines

Perk machines are the world actors players interact with to purchase perks. All perk machines inherit from **BP\_PerkMachine\_Base**.

## BP_PerkMachine_Base

The base class handles all core perk machine logic including:

- Interaction via BPI\_PerkInteraction
- Perk purchase validation against the currency interface
- Power state management
- Triggering the drink sequence on the player

## Creating Custom Perk Machines

Create a child class of **BP\_PerkMachine\_Base** and override:

- Mesh assignment
- Visual effects
- **ApplyLocalVisuals** function for construction script updates

Assign a **PDA\_PerkDefinition** data asset to define which perk the machine sells.

## Included Perk Machine

**BP\_ZombiesPerkMachine** is the included pre-built machine. It reads from the assigned data asset and updates its visuals via the construction script. Always click **Rerun Construction Script** after assigning or changing a data asset.

## Turned On At Spawn

When enabled the machine is active and purchasable from the moment it spawns. When disabled the machine requires power before it can be used.
