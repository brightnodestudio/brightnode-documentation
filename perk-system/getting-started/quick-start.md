# Quick Start Guide

Get the BN Perk System up and running in under 10 minutes.

## 1. Assign Perk System Component

Open your Character Blueprint.

Add **BPC\_PerkSystem** to the Character.

Select the Perk System Component and configure your defaults — Max Perk Count, montages, and container blueprints. Leave these as default to use the included assets.

## 2. Implement the Currency Access Interface

`Class Settings - Implemented Interfaces - BPI_CurrencyAccess`

This interface allows your character to communicate with your points system. For this guide we will use the included Currency Component.

Add **BPC\_CurrencyShowcase** to the Character Blueprint and implement all interface functions.

## 3. Add a Perk Machine

Drag a **BP\_ZombiesPerkMachine** into the level.

Assign a **PDA\_PerkDefinition** data asset to the machine.

Tick **Turned On At Spawn** to enable the machine on spawn.

Click **Rerun Construction Script** to update the actor visuals.

## 4. Setup Interaction

Set up a basic interaction trace in your character. When the trace hits a Perk Machine blueprint, call the interact function via **BPI\_PerkInteraction**.

Set up a new interact action and assign it within your mapping context.

## 5. Setup Attachment and Animation

In the character skeleton, add socket **s\_item\_l** to the **hand\_l** bone and configure the location and rotation.

Replace the showcase skeleton with your project's skeleton.

In the AnimBP, create a blend node for the arms and add an **Arms Slot**.

Set the character mesh to Manny and the AnimBP to ABP\_Manny.

## 6. Setup UI

Create a new widget **WBP\_HUD** and add it to the player viewport on Begin Play.

Inside WBP\_HUD add a Canvas Panel and add **WBP\_PerkBar**. Anchor to bottom center, alignment 0.5 / 0.5, enable Size to Content.

Override **Event On Initialized** and call Initialize on WBP\_PerkBar.

## 7. Bind Perk Events

Create four **Run On Server** events: Perk Added, Perk Removed, Drink Sequence Started, Drink Sequence Finished.

Bind these events on Begin Play from the Perk System Component.

Implement the logic for each event. See **BP\_BNPS\_Character\_Showcase** for full examples of applying perk modifiers.

You can now purchase perks, trigger the drink animation, and apply perk effects in your project.
