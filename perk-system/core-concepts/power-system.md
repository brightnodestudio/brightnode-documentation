# Power System

The power system allows perk machines to be locked until a power switch is activated, replicating the classic Zombies power mechanic.

## Power Switch Base

All power switches inherit from **BP\_PowerSwitch\_Base**. The base class handles:

- Interaction via BPI\_PerkInteraction
- Notifying all assigned powered actors when activated

## BP_PowerLever

The included pre-built power switch. Drag it into the level and assign your perk machines to the **Powered Actors** array in the Details panel.

## Configuring a Powered Machine

On the perk machine:

- Set **Requires Power** = true
- Set **Turned On At Spawn** = false

The machine will be inactive until the power switch is triggered.

## Custom Power Switches

Create a child class of **BP\_PowerSwitch\_Base** and assign your own mesh, collision, and implement the **ApplyLocalVisuals** function.

If you want to use your own interaction system instead of BPI\_PerkInteraction, replace the interface interact call in **BP\_PowerSwitch\_Base** with your own interact call.
