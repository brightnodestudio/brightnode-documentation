# BN Visual Marking System - Quick Start Guide

This guide shows how to integrate the BN Visual Marking System into a fresh Unreal Engine Third Person Template project and get both outlines and symbols working with minimal setup.

By the end of this guide you will be able to:

- Toggle an outline on an actor
- Spawn and clear a symbol attached to an actor
- Do everything using only the system's callable functions

## 1. Migrate the System into Your Project

1. Create and open your new project.
2. Open the BN Visual Marking System project.
3. In the Content Browser, right click the folder: **BN\_VisualMarkingSystem**
4. Choose **Asset Actions - Migrate**
5. Migrate the folder into your new project's Content directory.

## 2. Enable Custom Depth Stencil

BN Outlines rely on Unreal's Custom Depth Stencil.

1. Open **Edit - Project Settings**
2. Search for **Custom Depth-Stencil Pass**
3. Set it to: **Enabled with Stencil**

Restart the editor if prompted.

## 3. Add the Visual Marking Component

1. Open your character Blueprint
2. Add the component: **AC\_VisualMarkingSystem**
3. Compile and Save

This component is the only system-level requirement.

## 4. Create a Simple Interaction Test

For this guide we assume interaction is triggered via mouse click and a simple tag check is used to identify valid targets.

You can place this logic in the Character Blueprint, Player Controller, or Interaction Component. Any approach is valid as long as you can identify a Target Actor.

## 5. Create and Register an Outline Preset

**Create the Outline Preset**

1. Create a new Data Asset based on: **DA\_OutlinePreset**
2. Set the Preset ID

Preset IDs must be unique across all outline presets.

**Register the Outline Preset**

1. Open: **DA\_OutlinePresetLibrary\_Default**
2. Add your new preset to the library array
3. Save

If the preset is not in the library it will not be discoverable by the system.

## 6. Apply an Outline via Blueprint

To toggle an outline call:

**Set Outline On Actor (Callable)**

Parameters:

- Target Actor
- Outline Preset
- Enabled (true or false)

This is the only function required to apply or remove outlines.

## 7. Prepare a Test Actor

1. Place any actor in the level
2. If using tags, add the tag checked by your interaction logic

When interacted with the actor should now outline correctly.

## 8. Create and Register a Symbol Preset

**Create the Preset**

1. Create a new Data Asset based on: **DA\_SymbolPreset**
2. Set a Preset ID

Symbol Preset IDs must be unique across all symbol presets.

3. Configure the symbol settings as desired.

**Register the Preset**

1. Open: **DA\_SymbolPresetLibrary\_Default**
2. Add your new symbol preset to the library
3. Save

## 9. Spawn and Clear Symbols

Update your interaction logic:

1. Check whether the actor already has a symbol attached (Helper functions are available for this)
2. If no symbol exists call: **Spawn Symbol Actor (Callable)** with Target Actor and Symbol Preset
3. If a symbol already exists call: **Clear Symbol On Actor (Callable)** with Target Actor

## 10. Test the System

Play the level and interact with the test actor.

Expected behaviour:

- Outline toggles on and off
- Symbol spawns and clears
- Both actions are driven entirely by callable functions and presets
