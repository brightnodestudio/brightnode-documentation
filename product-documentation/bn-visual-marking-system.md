# BN Visual Marking System

## Quick Start

This guide shows how to integrate the **BN Visual Marking System** into a fresh Unreal Engine Third Person Template project and get both **outlines** and **symbols** working with minimal setup.

By the end of this guide, you will be able to:

* Toggle an outline on an actor
* Spawn and clear a symbol attached to an actor
* Do everything using only the system’s callable functions

No deep engine changes, no custom rendering setup beyond stencil.

### 1. Migrate the System into Your Project

1. Create and open your N**ew** project.
2. Open the **BN Visual Marking System** project.
3. In the Content Browser, right click the folder:\
   **BN\_VisualMarkingSystem**
4. Choose **Asset Actions → Migrate**
5. Migrate the folder into your new project’s **Content** directory.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-10 074822.png" alt=""><figcaption></figcaption></figure>

### 2. Enable Custom Depth Stencil

BN Outlines rely on Unreal’s Custom Depth Stencil.

1. Open **Edit → Project Settings**
2. Search for **Custom Depth-Stencil Pass**
3. Set it to:\
   **Enabled with Stencil**

Restart the editor if prompted.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 084956 (1).png" alt=""><figcaption></figcaption></figure>

### 3. Add the Visual Marking Component

1. Open your character Blueprint (for example `ThirdPersonCharacter`)
2. Add the component:\
   **AC\_VisualMarkingSystem**
3. Compile and Save

This component is the only system-level requirement.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 112735.png" alt=""><figcaption></figcaption></figure>

### 4. Create a Simple Interaction Test

For this guide, we assume:

* Interaction is triggered via mouse click
* A simple tag check is used to identify valid targets

You can place this logic in:

* Character Blueprint
* Player Controller
* Interaction Component

Any approach is valid as long as you can identify a **Target Actor**.

### 5. Create and Register an Outline Preset

#### Create the Outline preset

1. Create a new Data Asset based on:\
   **DA\_OutlinePreset**
2. Set the **Preset ID**

Important:

* Preset IDs **must be unique** across all outline presets

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 085551.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 085821.png" alt=""><figcaption></figcaption></figure>

#### Register the Outline preset

1. Open:\
   **DA\_OutlinePresetLibrary\_Default**
2. Add your new preset to the library array
3. Save

If the preset is not in the library, it will not be discoverable by the system.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 085638.png" alt=""><figcaption></figcaption></figure>

### 6. Apply an Outline via Blueprint

To toggle an outline, call:

**Set Outline On Actor (Callable)**

Parameters:

* Target Actor
* Outline Preset
* Enabled (true or false)

This is the only function required to apply or remove outlines.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 085947.png" alt=""><figcaption></figcaption></figure>

### 7. Prepare a Test Actor

1. Place any actor in the level (for example a Static Mesh Actor)
2. If using tags, add the tag checked by your interaction logic\
   Example: `Outline`

When interacted with, the actor should now outline correctly.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 090243.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 090307.png" alt=""><figcaption></figcaption></figure>

### 8. Create and Register a Symbol Preset

#### Create the preset

1. Create a new Data Asset based on:\
   **DA\_SymbolPreset**
2. Set a **Preset ID**

Important:

* Symbol Preset IDs must be unique across all symbol presets

3. Configure the symbol settings as desired

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 090440.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 090704.png" alt=""><figcaption></figcaption></figure>

#### Register the preset

1. Open:\
   **DA\_SymbolPresetLibrary\_Default**
2. Add your new symbol preset to the library
3. Save

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 090743.png" alt=""><figcaption></figcaption></figure>

### 9. Spawn and Clear Symbols

Update your interaction logic:

1. Check whether the actor already has a symbol attached\
   (Helper functions are available for this)
2. If no symbol exists, call:

**Spawn Symbol Actor (Callable)**\
Parameters:

* Target Actor
* Symbol Preset

3. If a symbol already exists, call:

**Clear Symbol On Actor (Callable)**\
Parameters:

* Target Actor

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 091023.png" alt=""><figcaption></figcaption></figure>

### 10. Test the System

Play the level and interact with the test actor.

Expected behaviour:

* Outline toggles on and off
* Symbol spawns and clears
* Both actions are driven entirely by callable functions and presets

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 091150.png" alt=""><figcaption></figcaption></figure>

## Core Callable Functions

These are the only functions required to use the system.

**Outlines**

* Set Outline On Actor

**Symbols**

* Spawn Symbol Actor
* Clear Symbol On Actor

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 113806.png" alt=""><figcaption></figcaption></figure>

## Helper Functions

Helper functions are available on **AC\_VisualMarkingSystem** under the **Helper Functions** category.

These can be used to:

* Check if an actor is currently outlined
* Check if an actor already has a symbol

They are optional but recommended for clean toggle logic.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-06 091355.png" alt=""><figcaption></figcaption></figure>

## Common Issues

* Custom Depth Stencil must be set to **Enabled with Stencil**
* Preset IDs must be unique
* Presets must be added to their respective default libraries

## Bug Reports & Support

If you believe you have found a bug or unexpected behaviour, please report it via the official **Brightnode Studio Discord**.

For this system, bugs should be posted in the relevant bug report channel:

**#bugs-visual-marking-system**

When reporting a bug, please include:

* Unreal Engine version
* System version (if applicable)
* Clear steps to reproduce the issue
* Screenshots or short videos where possible

This helps issues get identified and fixed much faster.

Join the Discord here:\
👉 [**Discord Link**](https://discord.gg/QTM7EZHHpV)
