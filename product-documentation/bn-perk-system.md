# BN Perk System

## Quick Start Guide

This quick start will walk you through setting up the Perk System with the unreal engine Third Person Template.

Use this to get the **BN Perk System** up and running in under 10 minutes.

### 1. Migrate the BN Perk System Folder to your Project

* Create and open your N**ew** project.
* Open the **BN Perk System** project.
* In the Content Browser, right click the folder:\
  **BN\_PerkSystem**
* Choose **Asset Actions → Migrate**
* Migrate the folder into your new project’s **Content** directory.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 083136.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 083156.png" alt=""><figcaption></figcaption></figure>

### 2. Enable Common UI Plugin

Enable the **Common UI** plugin.

`Edit → Plugins → Common UI`

Restart the editor when prompted.

Open:

`Project Settings → Engine → General Settings`

Set:

Game Viewport Client Class → **CommonGameViewportClient**

This is required for the Common UI input system.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 083643.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 083752.png" alt=""><figcaption></figcaption></figure>

### 3. Assign Perk System Component

Open the Third Person Character Blueprint.

Add the BPC\_PerkSystem to the Character.

Select the Perk System Component, this is where you will setup the defaults and how you want the system to work.

Choose your Max Perk Count, select your montages and container blueprints, or simply leave these as default to utilise the included assets.

For the sake of the quick start guide we will be leaving the defaults.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 084315.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 084327.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 084453.png" alt=""><figcaption></figcaption></figure></div>

### 4. Implement the Currency Access Interface

Class Settings -> Implemented Interfaces -> BPI\_CurrencyAccess

This interface will allow your character to talk to the Points system of your choice, for the sake of the Quick Start guide we will be utilising the included Currency Component as this is set up to be replicated and work out the box.

Add the BPC\_CurrencyShowcase to the Character Blueprint.

Implement all the interface functions which will allow the purchase of perks.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 085249.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 085300.png" alt=""><figcaption></figcaption></figure></div>

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 085035.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 085340.png" alt=""><figcaption></figcaption></figure></div>

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 090945.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 091231.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 091247.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 091330.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 091350.png" alt=""><figcaption></figcaption></figure></div>

### 5. Add a Perk Machine

Drag a perk machine actor into the level.

You can create your own perk machines by creating a child class of BP\_PerkMachine\_Base and assigning your own mesh and effects. For the sake of the Quick Start guide we are going to drag in one of the pre made BP\_ZombiesPerkMachines.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 091824.png" alt=""><figcaption></figcaption></figure>

Assign a Data Asset.

Again you can create your own data assets for your own perks, this is done by creating a data asset based on PDA\_PerkDefinition. You can then assign all the information for your custom perk inside that data asset. For the sake of the Quick Start though we will be using a pre done data asset.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 092423.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 092023.png" alt=""><figcaption></figcaption></figure></div>

Once your data asset is assigned tick turned on at spawn to enable the machine when spawning in.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 092143.png" alt=""><figcaption></figcaption></figure>

If using the BP\_ZombiesPerkMachine actor, hit Rerun Construction Script and this will update the actor.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 092229.png" alt=""><figcaption></figcaption></figure>

You will now have setup perk machine in the level.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 092240.png" alt=""><figcaption></figcaption></figure>

### 6. Basic Interaction

Setup a basic interaction trace and the ability to call interact from Perk Machine.

Currently the Perk Machines are setup to utilise the BPI\_PerkInteraction interface, if you want to swap this for your own interaction interface/system you will need to go into BP\_PerkMachine\_Base and swap out the interface and the interact events.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 093002.png" alt=""><figcaption></figcaption></figure>

We are going to utilise the included interface, we will setup a simple trace on the hit of a button and if we hit a Perk Machine blueprint we will call interact.

Setup a new interact action and assign it within the third person mapping context.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 093214.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 093309.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 093320.png" alt=""><figcaption></figcaption></figure></div>

Inside the character create the interact function.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 093612.png" alt=""><figcaption></figcaption></figure>

You should now be able to interact with the machine.

### 7. Setup Attachment and Animation

In order to get the supplied default attachment and animation to work we need to do a couple of things. Firstly lets handle attaching the drink container to the character. If you are using your own drink container mesh and animation this will be the same but obviously with your own values and animation sequences.

Go into the character skeleton and add the socket. As we are using the included DA\_IronStomach we need a s\_item\_l socket on the skeleton. Add to the socket to the hand\_l bone and set the location and rotation.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 103058.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 103114.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 103150.png" alt=""><figcaption></figcaption></figure></div>

Lets ensure the Third Person Template Skeleton can use the provided default animations. Find the showcase skeleton BN\_PerkSystem -> Showcase -> Character -> Meshes -> SK\_Mannequin. Delete this skeleton and replace references with the Third Person Template Skeleton.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 104717.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 104546.png" alt=""><figcaption></figcaption></figure></div>

Now we need to make the animation play on the character. The default drink animation montage is set to play on the arms slot as the animation is arms only. What we need is an arms slot within the AnimBP so lets open the AnimBP create a blend node for the arms and add an Arms Slot.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 104203.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105052.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105058.png" alt=""><figcaption></figcaption></figure></div>

The Animation may look weird using the quin mesh, so in the character blueprint set the skeletal mesh to Manny and the AnimBP to ABP\_Manny.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105144.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105407.png" alt=""><figcaption></figcaption></figure></div>

Now you should correctly open and drink the can on perk purchase.

### 8. UI Feedback

Now lets setup some basic UI using the included widgets to show the perk being added to the character.

Create a new widget called WBP\_HUD and add this to your player character viewport on begin play.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105806.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 105816.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110001.png" alt=""><figcaption></figcaption></figure></div>

Inside WBP\_HUD add a Canvas Panel and then add the WBP\_PerkBar. Anchor it to the bottom center, set the alignment to 0.5 and 0.5, enable size to content and move it up the canvas panel slightly.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110118.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110322.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110336.png" alt=""><figcaption></figcaption></figure></div>

Inside WBP\_HUD override the Event On Initialized Function and use it to Initialize the WBP\_PerkBar.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110628 (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110701.png" alt=""><figcaption></figcaption></figure></div>

Now your perk icons should show in your HUD.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 110720.png" alt=""><figcaption></figcaption></figure>

### 9. Apply the Perk Effects

Here we are going apply the actual perk effects to the Character. There are 4 bindings we need to make and these are for Perk Added, Perk Removed, Drink Sequence Started and Drink Sequence Finished.

First we will create and event for each, these need to be Run On Server events.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 111327.png" alt=""><figcaption></figcaption></figure>

Next we will create the bindings on the character begin play.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 111454.png" alt=""><figcaption></figcaption></figure>

Now we will create the actual logic for the events. For the sake of the quick start we will use print strings to print the perk and its modifier however for good examples on how to implement the perk you can see the BP\_BNPS\_Character\_Showcase blueprint.

<div><figure><img src="../.gitbook/assets/Screenshot 2026-04-03 111754.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2026-04-03 111900.png" alt=""><figcaption></figcaption></figure></div>

Finally lets create a quick button to test removing the perk.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 111959.png" alt=""><figcaption></figcaption></figure>

And thats it! You should now be able to buy the perk, drink the perk and apply the perk modifiers inside the Third Person Template.

## Perk Machine Power (Optional)

Okay so you have the Perk Machine in the world and you want to be able to turn it on via a power switch just like in Call of Duty Zombies. We will walk through that process here using what we made in the Quick Start guide.

### Power Switch Actor

First we need to either drag the pre made BP\_PowerLever into the world or create a child of BP\_PowerSwitch\_Base and assign a mesh, setup colissions and create the ApplyLocalVisuals function. For this guide we will drag in the pre made BP\_PowerLever.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 112649.png" alt=""><figcaption></figcaption></figure>

The BP\_PowerSwitchBase again uses BPI\_PerkInteraction, if you want to use your own interaction system you would need to replace the interface interact call with your own interact call.

Once the power lever actor is in the world assign the BP\_ZombiesPerkMachine in the powered actors array in the details panel.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 112923.png" alt=""><figcaption></figcaption></figure>

### Perk Machine Actor

Select the BP\_ZombiesPerkMachine and RequiresPower also untick Turned on at Spawn.

<figure><img src="../.gitbook/assets/Screenshot 2026-04-03 113023.png" alt=""><figcaption></figcaption></figure>

That should be all setup, you will now not be able to purchase the perk from the machine until you turn on the lever.

## Common Issues

### Perk machine does nothing when interacting

**Cause:** Interaction not set up correctly

**Fix:**

* Ensure your character is calling **Interact**
* Confirm your trace is hitting the perk machine
* Verify the machine uses `BPI_PerkInteraction`
* Add a Print String on interact to confirm it fires

### Cannot purchase perk

**Cause:** Currency interface not implemented or failing

**Fix:**

* Ensure your character implements:
  * `BPI_CurrencyAccess`
* Confirm all interface functions are filled in
* If using the showcase component:
  * Make sure `BPC_CurrencyShowcase` is added to the character

### Perk is purchased but no effect happens

**Cause:** Perk events not bound or logic not implemented

**Fix:**

* Ensure you have bound:
  * `OnPerkAdded`
  * `OnPerkRemoved`
* Confirm your events are:
  * **Run on Server**
* Add a Print String inside your event to verify it fires

### Perk icons not appearing in UI

**Cause:** HUD or Perk Bar not initialized

**Fix:**

* Ensure `WBP_HUD` is added to the viewport on Begin Play
* Confirm:
  * `WBP_PerkBar` is inside the HUD
  * `Initialize` is called on the Perk Bar
* Check anchor is set to bottom center with alignment (0.5, 0.5)

### Drink animation does not play

**Cause:** Missing socket, montage, or AnimBP setup

**Fix:**

* Ensure socket exists:
  * `s_item_l` on `hand_l`
* Confirm montage is assigned in the Perk Component
* Verify AnimBP includes:
  * Arms slot
* Ensure character is using:
  * Manny mesh
  * `ABP_Manny`

### Drink animation looks broken or misaligned

**Cause:** Skeleton mismatch or incorrect setup

**Fix:**

* Replace the showcase skeleton with the Third Person skeleton
* Ensure animation is using the correct skeleton
* Recheck socket transform on `hand_l`

### Perk machine visuals not updating

**Cause:** Construction script not refreshed

**Fix:**

* Select the perk machine in the level
* Click **Rerun Construction Script**

### Perk machine is not powered

**Cause:** Power system not configured

**Fix:**

* If using power:
  * Ensure machine has **Requires Power = true**
  * Ensure **Turned On At Spawn = false**
  * Assign the machine to the power switch
* Confirm power switch is calling interact correctly

### Interaction prompt not updating

**Cause:** UI not refreshed after state change

**Fix:**

* Refresh prompt after:
  * Purchase
  * Power toggle
* Re-run your prompt update logic

### Clients not seeing correct behaviour

**Cause:** Replication setup incomplete

**Fix:**

* Ensure:
  * Character replicates
  * Perk Component replicates
* Apply gameplay logic on the **server**
* Use replicated variables or events to update clients

### Debug Tip

If something isn’t working, check these three things first:

1. Is the interaction firing?
2. Is the logic running on the server?
3. Is the result being replicated or sent to the client?

## Bug Reports & Support

If you believe you have found a bug or unexpected behaviour, please report it via the official **Brightnode Studio Discord**.

For this system, bugs should be posted in the relevant bug report channel:

**#bugs-perk-system**

When reporting a bug, please include:

* Unreal Engine version
* System version (if applicable)
* Clear steps to reproduce the issue
* Screenshots or short videos where possible

This helps issues get identified and fixed much faster.

Join the Discord here:\
👉 [**Discord Link**](https://discord.gg/QTM7EZHHpV)
