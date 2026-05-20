# Perk Machine Power (Optional)

This section walks through setting up a power switch to control perk machines, just like in Call of Duty Zombies.

## Power Switch Actor

Drag the pre-made **BP\_PowerLever** into the world, or create a child of **BP\_PowerSwitch\_Base** and assign a mesh, set up collisions, and create the ApplyLocalVisuals function. For this guide we will drag in the pre-made BP\_PowerLever.

BP\_PowerSwitch\_Base uses **BPI\_PerkInteraction**. If you want to use your own interaction system you will need to replace the interface interact call with your own.

Once the power lever actor is in the world, assign the **BP\_ZombiesPerkMachine** in the Powered Actors array in the Details panel.

## Perk Machine Actor

Select the BP\_ZombiesPerkMachine and enable **Requires Power**. Also untick **Turned On At Spawn**.

That is all the setup required. You will now not be able to purchase the perk from the machine until you activate the lever.
