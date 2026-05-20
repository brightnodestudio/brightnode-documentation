# BN Perk System - Quick Start Guide

This quick start will walk you through setting up the Perk System with the Unreal Engine Third Person Template.

Use this to get the BN Perk System up and running in under 10 minutes.

## 1. Migrate the BN Perk System Folder to your Project

- Create and open your new project.
- Open the BN Perk System project.
- In the Content Browser, right click the folder: **BN\_PerkSystem**
- Choose **Asset Actions - Migrate**
- Migrate the folder into your new project's Content directory.

## 2. Enable Common UI Plugin

Enable the **Common UI** plugin.

`Edit - Plugins - Common UI`

Restart the editor when prompted.

Open:

`Project Settings - Engine - General Settings`

Set:

Game Viewport Client Class - **CommonGameViewportClient**

This is required for the Common UI input system.

## 3. Assign Perk System Component

Open the Third Person Character Blueprint.

Add **BPC\_PerkSystem** to the Character.

Select the Perk System Component — this is where you will set up the defaults and how you want the system to work.

Choose your Max Perk Count, select your montages and container blueprints, or simply leave these as default to use the included assets.

For the sake of the Quick Start guide we will be leaving the defaults.

## 4. Implement the Currency Access Interface

`Class Settings - Implemented Interfaces - BPI_CurrencyAccess`

This interface allows your character to talk to the Points system of your choice. For the Quick Start guide we will be using the included Currency Component as this is set up to be replicated and work out of the box.

Add **BPC\_CurrencyShowcase** to the Character Blueprint.

Implement all the interface functions which will allow the purchase of perks.

## 5. Add a Perk Machine

Drag a perk machine actor into the level.

You can create your own perk machines by creating a child class of **BP\_PerkMachine\_Base** and assigning your own mesh and effects. For the Quick Start guide we are going to drag in one of the pre-made **BP\_ZombiesPerkMachines**.

Assign a Data Asset.

You can create your own data assets for your own perks by creating a data asset based on **PDA\_PerkDefinition**. You can then assign all the information for your custom perk inside that data asset. For the Quick Start we will be using a pre-made data asset.

Once your data asset is assigned tick **Turned On At Spawn** to enable the machine when spawning in.

If using the BP\_ZombiesPerkMachine actor, hit **Rerun Construction Script** to update the actor.

## 6. Basic Interaction

Set up a basic interaction trace and the ability to call interact from the Perk Machine.

The Perk Machines are set up to use the **BPI\_PerkInteraction** interface. If you want to swap this for your own interaction interface or system you will need to go into **BP\_PerkMachine\_Base** and swap out the interface and the interact events.

We are going to use the included interface. We will set up a simple trace on the hit of a button and if we hit a Perk Machine blueprint we will call interact.

Set up a new interact action and assign it within the Third Person Mapping Context.

Inside the character create the interact function.

You should now be able to interact with the machine.

## 7. Setup Attachment and Animation

To get the supplied default attachment and animation working we need to do a couple of things. First let's handle attaching the drink container to the character.

Go into the character skeleton and add the socket. As we are using the included **DA\_IronStomach** we need an **s\_item\_l** socket on the skeleton. Add the socket to the **hand\_l** bone and set the location and rotation.

Let's ensure the Third Person Template Skeleton can use the provided default animations. Find the showcase skeleton at:

`BN_PerkSystem - Showcase - Character - Meshes - SK_Mannequin`

Delete this skeleton and replace references with the Third Person Template Skeleton.

Now we need to make the animation play on the character. The default drink animation montage is set to play on the arms slot. Open the AnimBP, create a blend node for the arms, and add an Arms Slot.

In the character blueprint set the skeletal mesh to Manny and the AnimBP to ABP\_Manny.

You should now correctly open and drink the can on perk purchase.

## 8. UI Feedback

Create a new widget called **WBP\_HUD** and add it to your player character viewport on Begin Play.

Inside WBP\_HUD add a Canvas Panel and then add **WBP\_PerkBar**. Anchor it to the bottom center, set the alignment to 0.5 and 0.5, enable Size to Content and move it up the canvas panel slightly.

Inside WBP\_HUD override the **Event On Initialized** function and use it to Initialize the WBP\_PerkBar.

Your perk icons should now show in your HUD.

## 9. Apply the Perk Effects

There are 4 bindings we need to make: Perk Added, Perk Removed, Drink Sequence Started, and Drink Sequence Finished.

First create an event for each — these need to be **Run On Server** events.

Next create the bindings on the character Begin Play.

Now create the actual logic for the events. For the Quick Start we will use Print Strings to print the perk and its modifier. For good examples of how to implement the perk see **BP\_BNPS\_Character\_Showcase**.

Finally create a quick button to test removing the perk.

You should now be able to buy the perk, drink the perk, and apply the perk modifiers inside the Third Person Template.
